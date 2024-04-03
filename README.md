# Java-web-application

The following example introduces a known security vulnerability (SQL Injection) into your codebase.

**Modified:** src/main/java/com/example/securewebapp/HomeController.java

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
