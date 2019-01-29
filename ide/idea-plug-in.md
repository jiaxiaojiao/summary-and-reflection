# IDEA 插件的使用

## MyBatis Generator
```text
    在IDEA中使用 MyBatis Generator生成实体类和mapper配置文件
```
- pom.xml 文件的build节点
- resources目录新建 generatorConfig.xml
- 加入maven配置，在 Command line中加入 mybatis-generator:generate -e
- 启动项目