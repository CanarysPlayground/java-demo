# Java-web-application

### Introduction
The repository `Java-web-application` appears to be a Java web application built using Spring Boot.

### Prerequisites
- **Java JDK:** Given that the primary language for the application is Java, you would need a Java Development Kit (JDK) installed on your machine. The version of JDK required would typically be specified in the project's documentation.

- **Maven or Gradle:** These are popular build tools for Java projects and one of them is likely to be used in this project. You can confirm this by checking if the repository includes a pom.xml (for Maven) or build.gradle (for Gradle) file.

- **Spring Boot:** The project likely uses the Spring Boot framework, so knowledge of how to work with Spring Boot applications would be beneficial.

- **An IDE that supports Spring Boot:** You would need an Integrated Development Environment (IDE) to work on the project. Spring Tool Suite, IntelliJ IDEA, and Eclipse are examples of IDEs that have good support for Spring Boot.

- **A Web Browser:** Since part of the code is written in HTML, you would need a web browser to view the HTML pages rendered by the application.

### Exercise

The following example introduces a known security vulnerability (SQL Injection) into your codebase.

You will modify the existing simple web application by adding a new feature that introduces an SQL Injection vulnerability. 

**Step 1:** Create a branch called `sql-injection-fix`.

**Step 2:** Add the below code to this path - `src/main/java/com/example/securewebapp/HomeController.java` (Remove full code and replace)

```
package com.example.securewebapp;

import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import java.sql.ResultSet;
import java.util.List;

@RestController
public class HomeController {

    private final JdbcTemplate jdbcTemplate;

    public HomeController(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    @GetMapping("/")
    public String home() {
        return "home";
    }

    // Vulnerable to SQL Injection
    @GetMapping("/search")
    public List<String> searchUsers(@RequestParam String username) {
        String sql = "SELECT * FROM users WHERE username = '" + username + "'";
        return jdbcTemplate.query(sql, (resultSet, i) -> resultSet.getString("username"));
    }
}
```
**Step 3:** Raise a pull request to the `main` branch.
