Spring In Enterprise
    No Need of heavy application servers
    Provides abstractions for enterprise systems
    Focus on business logic
Dependency Management
    Spring manages runtime dependencies
    Configure or create them once, maintains by Application Context

    if your class cannot operate without the dependency, it should be injected via constructors.
    If your class can treat the dependency as optional or can accept multiple but variable concrete instances of the dependency,
    then it can be injected via setter injection.

# POJO (Plain Old Java Object )
    With Both Attributes and Methods operating on those arrtibutes.
# Bean (From EJB)
    Simple Objects with only Setters/Getters
# Spring Bean
    POJOs configured with Application Context
# DTO (Data Transfer Objects)
    JavaBeans used to move the state between layers
# DAO (Data Access Object)

----------

Common Patterns accross different use-cases

(Auto) Configuration by components  scanning or Java

Inversion of Control (IOC)

    Configuration is building IOC container
    IOC provides mechanism of depedency Injection (Move aways traditional object creation process)
    ApplicatoinContext wrps the BeanFactory(IOC contaniner Server), which serves the beans to the runtime application.
    Spring Boot provides auto-configuration of the ApplicationContext.

    Reduce object coupling

# Application Context
    Purpose::
        Central element of Spring Application
        Encapsulate the BeanFactory (IOC Container)
        Provides metadata for bean creation
        Provides mechanism for creation of beans in the correct order.

# IOC Container
    Provides all facilites for bean creation at startup and runtime.
    BeanFactory handles all singleton beans
    Multiple Application Contexts
    Parent Context can handle child context, not the other way around.
