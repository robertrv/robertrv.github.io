---
title: "xUnit parameters annotation based"
date: 2014-11-29
categories: 
  - "software-development"
tags: 
  - "test"
  - "xunit"

---

Recently I needed to do some work on testing which requires special scenario which didn't find quite usual, so I though that could be valuable to share with the blog readers (if any) so anyone can benefit from the code or help with better solution.

# The problem

I was trying to create some infrastructure classes to be able to test with the following restrictions:

- Execute a bunch of tests with any super class
    - Is it possible that I will need spring or any other IoC framework, so probably we will have to inherit from this.
- Each test will have 'n' methods and each one can have different configuration or even we want to execute the same method with multiple parameter.
    - The different configuration will be specified at method or class level or mixed.
- Ideally I don't want to have to declare special constructor (which will be inherited or replicated) or special parameters on the method. The reason is because this will possibly maintained in a future by other people, so the easier to keep adding new tests the best.

What I wanted to achieve was finally something like

```java
    @WorldWay
    @CalifornicationWay
    @BroWay
    @Test
    public void helloAllStyles() {
        System.out.println("\tProper test " + greeter.sayHello("Mum"));
    }
```

So that I will get an output where the test method will be executed three times each one with an specific strategy:

```
Proper test Hey Bro! What's up Mum?
Proper test Hello Motherfuckeer! akka Mum
Proper test Hello Mum
```

# Options

I did consider options like junit parametrized tests or equivalent testng data providers but as a general rule causes too much couple between the infraestructure and the tests. So every time I wanted to create a new test I will have to follow some inherited rules, like have a constructor with parameters or pass the parameters on the test method itself or even remember to annotate my methods with some specific _@Test(dataprovider="something")_. So I finally decided to dig a little bit more on options given by both testng & junit.

## TestNG

With this framework I looked arround the different annotations and options to execute multiple times the same test method, so finally I came out with the following steps:

- Used an annotation transformer to change the @Test annotations to become declare (in case the don't declare another yet) an static data provider.

```java
@Override
public void transform(ITestAnnotation annotation, Class testClass, Constructor testConstructor, Method testMethod) {
    if (interestingMethod(testMethod)) {
        if (!annotation.getDataProvider().isEmpty() || annotation.getDataProviderClass() != null) {
            if (filterUsefulAnnotations(testMethod).size() == 1) {
                // TODO make it work with data provider if there is just one annotation which we are interested in.
            }
            throw new IllegalStateException("Cannot work with data providers | provider class");
        }
        annotation.setDataProviderClass(StaticDataProvider.class);
        annotation.setDataProvider(StaticDataProvider.PROVIDER_NAME);
    }
}
```

- This will instruct testng to execute the test method as many time as annotations we are really intereted in (after some playing to filter the proper annotation). To do this and not pass the parameter to the method (remember I don't want to add a parameter to each test method) I tweaked return a list of empty objects:

```java
    @DataProvider(name = PROVIDER_NAME)
    public static Object[][] provider(Method method, @TestInstance Object instance) {
        if (!AnnotationQueueListener.class.isAssignableFrom(instance.getClass())) {
            throw new IllegalArgumentException("Test instance must implement the proper interface");
        } else {
            Queue<Class<? extends Annotation>> annotations = AnnotationTransformer.filterUsefulAnnotations(method);

            AnnotationQueueListener initializer = (AnnotationQueueListener) instance;
            initializer.initialize(annotations);

            Object[][] result = new Object[annotations.size()][0];
            for (int i = 0; i < result.length; i++) {
                result[i] = new Object[]{};
            }
            return result;
        }
    }
```

- So now we just need to tell the test which is the current strategy to use. To do this had already injected a queue of annotations on the test instance (on the previous code), which will be consumed by the test method using a @BeforeMethod method. So in the method itself we will see:

```java
    private Queue<Class<? extends Annotation>> annotations;

    @BeforeMethod
    public void prepare(Method method) {
        greeter = createGreeting(annotations.remove());
        testName = String.format("%s_%s", method.getName(), greeter.getClass().getSimpleName());
    }

    @Override
    public void initialize(Queue<Class<? extends Annotation>> annotations) {
        this.annotations = annotations;
    }

    private Greeting createGreeting(Class<? extends Annotation> annotation) {
        if (BroWay.class.equals(annotation)) {
            return new Bro();
        } else if (CalifornicationWay.class.equals(annotation)) {
            return new Californication();
        } else if (WorldWay.class.equals(annotation)) {
            return new World();
        } else {
            throw new IllegalStateException("Could not initialize this type, your test must be annotated with TestNG @Test annotation and the ");
        }
    }
```

As you can see the code used to achieve this is not so complex but the result is also not so clean because we have to add on the test the logic on the before method to get the proper element withing a queue that we are not really controlling, is just part of the test instance.

This also had the bad side that the main element which expands each test method in multiple test methods is an static method, which will not easily had context and any initialization using IoC can be dangerous and more complex.

## JUnit

In order to achieve this we looked arround at the options and the easiest seemed to be to use a Runner, which matches with the same approach spring used (which also is something we want to use in a future).

So to achieve this the work needed was bit more extense:

- Create a Runner which inherits from _BlockJUnit4ClassRunner_ which let us change the getChildren method the same way jUnit does to get the list of children in case of a parametrized test

```java
    @Override
    protected List<FrameworkMethod> getChildren() {
        List<FrameworkMethod> children = super.getChildren();
        List<FrameworkMethod> result = new LinkedList<FrameworkMethod>();
        for (FrameworkMethod child : children) {
            for (Class<? extends Annotation> annotation : annotations) {
                prepareAnnotation(result, child, annotation);
            }
        }
        return result;
    }
```

- Then on each children method we create a new FrameworkMethod where we modify the annotation the method can see (that is the **key difference with TestNG** because we can change the final method executed by the xUnit Framework)

```java
    private void prepareAnnotation(List<FrameworkMethod> result, FrameworkMethod child, Class<? extends Annotation> annotationType) {
        if (child.getAnnotation(annotationType) != null) {
            result.add(cloneMethod(child.getMethod(), annotationType));
        }
    }

    private FrameworkMethod cloneMethod(Method method, final Class<? extends Annotation> toKeep) {
        return new FrameworkMethod(method){
            @Override
            public Annotation[] getAnnotations() {
                Annotation[] annotations = super.getAnnotations();
                List<Annotation> result = new LinkedList<Annotation>();
                for (Annotation annotation : annotations) {
                    if (annotation.annotationType().getAnnotation(GreetingAnnotation.class) == null ||
                            annotation.annotationType().equals(toKeep)) {
                        result.add(annotation);
                    }
                }
                return result.toArray(new Annotation[result.size()]);
            }
        };
    }
```

- Finally on the test class itself we can ask the method what is its annotation because will have just one of the ones that we are intereted

```java
    @Before
    public void before() {
        if (annotations.contains(CalifornicationWay.class)) {
            greeter = new Californication();
        } else if (annotations.contains(WorldWay.class)) {
            greeter = new World();
        } else if (annotations.contains(BroWay.class)) {
            greeter = new Bro();
        } else {
            throw new IllegalStateException("Not greeter found");
        }
    }
```

With this solution we still need a @Before (which can be avoided) but we don't need any queue to keep track of which annotation should we use during method execution.

# Conclusion

This let us do a solution where all tests can be just annotated and will be executed the exact number of times we are really interested in. Still some works needs to be done to clean the solution and maybe add some more proteccions but the the first implementation can be seen on my [github](https://github.com/robertrv/prekrasting/tree/testing/xUnitParamByAnnotations). I'll try to get an update on this adding some of this missing parts.
