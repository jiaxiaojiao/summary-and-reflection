## Spring 5概述
## Spring 5 Framework体系结构
## Spring5 环境搭建

IOC
- 容器基本实现和组成
- 装配Bean的方式： xml ，注解，JavaConfig
- BeanFactory源码分析
- BeanDefinition源码分析
- Bean生命周期
- 依赖实现

AOP
- 面向切面的基础：动态代理，Spring对AOP的支持（注解，xml）
- AOP源码分析：ProxyFactory源码解析，AOPProxy源码解析（JDKDynamicAOPProxy，Cglib2AOPProxy），拦截与织入（advice源码分析，Interceptor源码分析）
- Transaction事务分析：事务的基础，Spring对事务的支持，源码分析
- Spring Cache框架源码分析