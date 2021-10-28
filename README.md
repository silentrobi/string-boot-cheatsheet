# string-boot-cheatsheet

## Database Migration
Springboot can work with **Hibernate**(ORM library) to create database tables from `JPA Entity` classes. However, it doesn't have database migration management. As It doesn't generate migration script, to track db changes is impossible. So, alternatives of this library are **Liquibase** , **Flyway**. 

## Liquibase
Steps:
- Add `liquibase` dependency and plugin to `pom.xml`
```xml
     <dependencies>
        <!--Add in dependencies section -->
        <dependency>
            <groupId>org.liquibase</groupId>
            <artifactId>liquibase-core</artifactId>
        </dependency>
     <dependencies>
     <build>
        <plugins>
          <!--Add in plugins section -->
            <plugin>
                <groupId>org.liquibase</groupId>
                <artifactId>liquibase-maven-plugin</artifactId>
                <version>4.3.2</version>
                <configuration>
                    <!--set values for Liquibase properties and settings
                    for example, the location of a properties file to use-->
                    <propertyFile>src/main/resources/liquibase.properties</propertyFile>
                </configuration>
            </plugin>
        </plugins>
    </build>
```
