---

layout:     post
title:      spring常用注解说明
date:       2018-11-07
author:     Yuegg
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - blog
---
#spring常用注解说明
---

使用注解前需要开启自动扫描功能，其中base-package为需要扫描的包(含子包)。

`<context:component-scan base-package="xxx.xxx.xxx"/>`

##声明Bean注解
1. `@Component`  注解在类上，泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注。
2. `@Service` 注解在类上，用于标注业务层组件。
3. `@Controller` 注解在类上，用于标注控制层组件，与前端交互。
4. `@Repository` 注解在类上，用于标注数据访问组件，即DAO组件。

##注入Bean注解
1. `@Autowired` 属于Spring 的org.springframework.beans.factory.annotation包下,可以对成员变量、方法、构造函数、类，进行注释。默认按类型装配(ByType),注解在set方法上或属性上如果想使用按名称装配，可以结合@Qualifier注解一起使用。
2. `@Resource` 与`@Autowired`类似，属于JSR-250位于java.annotation包下，默认按名称装配（ByName）。

##Java配置注解
1. `@Configuration ` 注解在类上，声明当前类是一个配置类，相当于一个Spring配置的xml文件。把一个类作为一个IoC容器。
> 和@Bean搭配使用，某个方法头上如果注册了@Bean，就会作为这个Spring容器中的Bean。
2. `@Bean` 注解在方法上，声明当前方法的返回值为一个Bean。
3. `@ComponentScan` 注解在类上，自动声明报下所有使用`@Service`、`@Compent`、`@Repository`、`@Controller`的类，并注册为Bean。
4. `@Lazy(true)` 标识延迟初始化。
5. `@Primary` 自动装配时当出现多个Bean候选者时，被注解为@Primary的Bean将作为首选者，否则将抛出异常。

##AOP注解
1. `@Aspect` 注解在类上，声明是一个切面。
2. `@After` 注解在方法上，声明建言。
3. `@Before` 注解在方法上，声明建言。
4. `@Around` 注解在方法上，声明建言。
5. `@PointCut` 注解在方法上，定义拦截规则，声明切点。

##常用配置
###Bean的Scope
1. `@Scope` 注解在类上，用于指定scope作用域的描述的是Spring容器如何新建Bean的实例的。实例：
	1. `Singleton` 一个spring容器中只有一个Bean的实例，此为Spring的默认配置，全容器共享一个实例。
	2. `Prototype` 每次调用新建一个Bean实例。
	3. `Request` Web项目中，给每一个http request新建一个Bean实例。
	4. `Session` Web项目中，给每一个http session新建一个Bean实例。
	5. `GlobalSession` 这个只在portal应用中有用，给每一个global http session 新建一个Bean实例。

###Spring EL和资源调用
1. `@Value` 注解在变量上，调用资源（普通文件，网址，配置文件，系统环境变量等）。
2. `@PropertySource` 注解在类上，注入配置文件来制定文件地址。

###Bean的初始化和销毁
1. `@Bean` 注解在方法上，`@Bean(initMethod="init",destroyMethod="destory")`在构造函数执行后执行，在Bean销毁之前执行。
2. `@PostConstruct` 注解在方法上，在构造函数执行后执行。
3. `@PreDestroy` 注解在方法上，在Bean销毁之前执行。
4. `@DependsOn` 注解在方法上，定义Bean初始化及销毁时的顺序。

###Profile
1. `@Profile` 注解在类、方法上，在不同的情况下选择实例化不同的Bean。

##事件
###多线程
1. `@EnableAsync` 注解在配置类上，开启对异步任务的支持。
2. `@Async` 注解在实际执行的Bean方法中，声明这是一个异步任务。

###计划任务（定时任务）
1. `@EnableScheduling` 注解在配置类上，开启对计划任务（定时任务）的支持。
2. `@Scheduled` 注解在实际执行的方法上，在要执行计划任务的方法上通过@Scheduled 声明这是一个计划任务。包含：cron 、fixDelay、fixRate等类型。
	1. `@Scheduled(cron="0 25 11 ？ * *")` cron是linux和unix系统下的定时任务
	2. `@Scheduled(fixedDelay=5000)` 延迟5秒执行
	3. `@Scheduled(fixedRate=5000)` 每隔5秒执行一次
##SpringMVC注解
1. `@Controller` 注解在类上，表面这个类是SpringMVC里面的Controller，将其声明为Spring的一个Bean，Dispatcher Servlet会自动扫描注解了此注解的类，并将Web请求映射到@RequestMappin的方法上。
2. `@RequestMapping` 注解在类或方法上，用来映射Web请求(访问路径和参数)、处理类和方法的。
3. `@ResponseBody` 注解在类或方法上，作用在类上表明将返回类型直接输入到HTTPresponse body中；作用在方法上，输出JSON格式的数据。
4. `@RequestBody` 注解在参数前，request的参数在请求体内。


