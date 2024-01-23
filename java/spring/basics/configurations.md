# Java Based config
    Maven
        o.sf::spring-core
        o.sf::spring-context
        o.aspectj::aspectweaver
        o.slf4j::slf4j-log4j12
    Class
        ApplicationContext
            AC.getBean()
        AnnotationApplicationContext(ApplicationConfig.class)


    Annotations
    [Variable]
        @Value("Hello")
        @Value("${app.hello}")
        @Autowired (Consturctors)
        @Profile

    [Function]
        @Bean
        @PostConstruct
        @PreDestroy
        @PointCut

    [Class/Interface]
        @Configuration
        @PropertySource("classpath:application.properties")
        @Component
        @Service
        @EnableAspectJAutoProxy
        @Target
        @Retention
        @Aspect
        @Before
        @AfterReturning
        @Around


# Xml Based config


# Envirornment
    15 layers of order
    src/main/resources/application.properties

    Runtime parameters
    application.properties

# Profiles
    -Dspring.proifles.active=prod

# Spring Expression Language
    @Value("#{new Boolean(environment['spring.profiles.active']!='dev')}")

# Bean Scopes
    Singleton (Default)
        One Instance per context definition
        State Data
    Prototype
        New instance every time it is referenced
        Definition is stored in Ioc, instances are not
        transient data
    Session
        Applies to web environment only
        One Instance of bean per user session
    Request
        Applies to web environment only
        One Instance of bean per request

# Proxies (Spring 4.0)
    Aspected behavior
    Everything is a proxy

    Behavior added to classes only impacted by calls through the proxy
    Private Methods/Internal calls
    Proxies are not avilable during initialization or after object destruction started


# Component Scanning
    Indicates that a class should be loaded into the BeanFactory
    CS scans a base package and loads configuration automatically for each bean it finds
    @ComponentScan(basePackages="c.t.mybase")

    @Component
    @Service
    @Entity

    Dependency Injection(DI)  is achieved @Autowired
    @Qualifier is used when multiple implementation of interface are needed
    @Value

    SpringBoot:
        Base package is defined as     @ComponentScan(basePackages="c.t.mybase")


# Lifecycle Phases

    A. Initialization [When ApplicationContext is creating]
        BeanFactory initialize Phase
            1. Load Bean definitions
                Java Configuration
                XML Configuration
                Component Scanning and Auto Configuration
                Bean Definitions from all sources
                Id is used to create the index for the Factory
                BeanFactory contains only references after initialization.
            2. Post-Process Bean definitions
                Can modify or transform any bean in the factory prior to instatiation.
                BeanFactoryPostProcessor interface (Custom Component to impact BeanFactory)
                eg: PropertySourcesPlaceHolderConfigurer

                Bean Factory Post Processor and Java Configuration


        Bean initialization and instatiation (Priming the Bean Factory)

            1. Instatiate a Bean (Eager[By Default] Vs Lazy)
                Constructors -- After all beans have been instatiated
                Setters are called
                Autowiring occurs (non-constructor based)

            2. Bean Post-Processor (Final point of configuration manipulation)
                pre-init -- Intializer (@PostConstruct)
                BeanPostProcessor Interface [class of beans]
                    Before and After
            3. Bean Post-Processor
                post-init
            4. Ready to use
            5. Context-Aware Beans


    B. Use/Runtime
        ApplicationContext servces as proxies to the original class
        ApplicationContext maintain handle to each bean(Singleton)

    C. Destruction [When ApplicationContext start to close]
        @PreDestroy method is called.
