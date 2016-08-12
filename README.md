### Use Sqlite in SpringBoot 1.4.0-RELEASE with Hibernate (5.0.9) 

It's an adaptation of Gwen SqliteDialect(https://github.com/gwenn/sqlite-dialect)

[![Build Status][1]][2]

##Springboot
For version 1.4.0-RELEASE  
Add JPA Dependency to pom file and Sqlite JDBC  
```xml
       <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.xerial</groupId>
            <artifactId>sqlite-jdbc</artifactId>
            <version>3.8.9.1</version>
            <!--scope>provided</scope-->
        </dependency>
```

Declare DataSource (Update Path and FileName here is nameOfFile.db )  
```java
import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;  
import org.springframework.context.annotation.Bean;  
import org.springframework.context.annotation.Configuration;  

import javax.sql.DataSource;  

@Configuration  
public class DatabaseConfig {  

    @Bean  
    public DataSource dataSource() {  
        DataSourceBuilder dataSourceBuilder = DataSourceBuilder.create();  
        dataSourceBuilder.driverClassName("org.sqlite.JDBC");  
        dataSourceBuilder.url("jdbc:sqlite:nameOfFile.db");  
        return dataSourceBuilder.build();  
    }
}
```
Edit application.properties and add jpa parameters:  
```properties
spring.jpa.database-platform=org.hibernate.dialect.SQLiteDialect  
spring.jpa.hibernate.ddl-auto=create-drop  
```

[1]: https://secure.travis-ci.org/diyfr/sqlite-dialect.png  
[2]: http://www.travis-ci.org/diyfr/sqlite-dialect  

