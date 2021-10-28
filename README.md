# string-boot-cheatsheet

## Database Migration
Springboot can work with **Hibernate**(ORM library) to create database tables from `JPA Entity` classes. However, it doesn't have database migration management. As it doesn't generate migration script, tracking db changes is impossible. So, alternatives of this library are **Liquibase** , **Flyway**. 

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
2. create folder `db\changelog` inside project `resources` folder. Migration scripts will be reside in  `changelog` folder. Now we will follow [liquibase best practice](https://www.liquibase.org/get-started/best-practices) where there will be a root configuration file `changelog-root.xml` (choose any name) that manages all migration files.
```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <databaseChangeLog
          xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:pro="http://www.liquibase.org/xml/ns/pro"
          xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
          http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-4.1.xsd
          http://www.liquibase.org/xml/ns/pro
          http://www.liquibase.org/xml/ns/pro/liquibase-pro-4.1.xsd">
          <!-- path specifies changelog file's location -->
          <includeAll path="db/changelog/changes/"/>
     </databaseChangeLog>
```
