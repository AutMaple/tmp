# SprintBoot 常用注解

- @SpringBootApplication: 该注解在 Sprint Boot 应用的主类上使用，表示这是一个 Sprint Boot 应用。它组合了 @Configuration， @EnableAutoConfiguration 和 @ComponentScan 注解
- @Configuration: 表明该类是一个配置类，通常会在配置类中会通过 @Bean 注解注入一些第三方的 Bean 或者是自定义的 Bean。
- @Import: 提供和 XML 配置中 `<import/>` 标签一样的功能。它可以导入普通的 compoennt, @Configuration 注解修饰的配置类, 以及 ImportSelector 或者 ImportBeanDefinitionRegistrar 接口的实现类
- @Conditional: 当条件满足时，才会往 Spring 容器中注入对应的 Bean，要求注解的参数实现 Condition 接口
- @EnableAutoConfiguration: 开启自动化配置，比如找到各 jar 包中 `META-INF/spring.factories` 文件，并根据 spring.factories 中声明的自动配置类，加载对应的配置到 spring 容器中。这些自动配置类就是使用 @Configuration, @Conditional 等注解修饰的配置类。Spring 会根据里面配置，选择性加载对应的 Bean 到 spring 容器中
- @Autowired: 根据类型进行注入
- @EnableConfigurationProperties: 启用一个或者是多个属性配置类, 所谓的属性配置类就是被 @ConfigurationProperties 注解修饰的类，@ConfigurationProperties 注解修饰的类的属性可以通过 application.yaml 或者 application.properties 文件进行配置
- @ConfigurationPropertiesScan: 该注解用于扫描指定包下面的所有配置属性类
- @ComponentScan: 用于扫描指定包及其子包下面的所有组件

# 配置文件

sprint boot 使用 `application.yaml` 或者 `application.properties` 作为配置文件。并且支持根据不同的环境加载不同的配置文件以及用户自定义配置项。用户自定义配置项需要使用 @EnableConfigurationProperties 注解开启配置属性类以及使用 @ConfigurationProperties 注解定义配置项的前缀以及对应的配置。

配置项的优先级从高到低(只列举部分)：

- 命令行参数
- Java 系统属性
- 操作系统环境变量
- `application-<profile>.properties/yaml`
- `application.properties/yaml`

# SpringBoot 中使用了那些设计模式？

- 工厂模式： BeanFactory, 用于创建对象
- 策略模式： 这个模式用的是非常多，比如我们可以使用 xml 配置，也可以使用注解配置
- 代理模式：AOP 就是一个典型的代理模式
- 观察者模式： SpringBoot 的事件机制就是一个发布订阅模式的实现。它提供了 ApplicationEventPublisher 和 ApplicationListener 接口
- 模板方法模式：SpringBoot 中提供的 Bean 声明周期相关的接口，这些接口都是模板方法模式的运用
- 中介者模式：SpringMVC 中的 dispatcher servlet 采用的就是中介者模式，SpringMVC 中的 View，Model， Controler 等组件相互之间都不直接打交道，而是通过 Dispatche servelet 进行通信

# Spring Bean 的生命周期



