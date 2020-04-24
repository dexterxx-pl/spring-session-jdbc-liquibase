# spring-session-jdbc-liquibase
Liquibase changeset JDBC schema for Spring Session model.

I didn't found liquibase changeset script which imitates 
[Spring Session JDBC schema initialize SQL scripts](https://github.com/spring-projects/spring-session/tree/master/spring-session-jdbc/src/main/resources/org/springframework/session/jdbc)...
so I made it.

## Compatibility 

Should be compatible with all database engines [supported by Liquibase](https://www.liquibase.org/databases.html).

```xml
<dbms="db2"/>
<dbms="derby"/>
<dbms="h2"/>
<dbms="hsqldb"/>
<dbms="mysql"/>
<dbms="mariadb"/>
<dbms="oracle"/>
<dbms="postgresql"/>
<dbms="sqlite"/>
<dbms="mssql"/>
<dbms="sybase"/>
```

Tested only with PostgreSQL and H2.

Blob type insired from original Spring sources.

## How to use (Spring Boot example)

1. Download [changeset-000.xml](changeset-000.xml) to your liquibase directory and adjust to your needs.
1. Include in your Spring Boot application configuration:
    ```properties
    spring.session.store-type=jdbc
    spring.session.jdbc.initialize-schema=never
    ```
   Remember that you need to have defined `spring.datasource`. Obvious. 
1. Make sure you have defined dependencies in `pom.xml`:
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.session</groupId>
        <artifactId>spring-session-jdbc</artifactId>
    </dependency>
   ```
   Yes, `spring-session-jdbc` is mandatory.
1. (optional, suggested) Put `@EnableJdbcHttpSession` on your preferred Configuration bean/class.

    Not sure why and I didn't checked, but without that It also works.
    
1. Done. Run app and test. If doesn't work make sure you'd recompiled project /
cleared caches / killed jdk processes or reinstalled OS. GL.  
