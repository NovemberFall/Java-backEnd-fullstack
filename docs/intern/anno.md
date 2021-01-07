## Hibernate @Entity, @Table, @Id, and @GeneratedValue annotations 

```java
package com.zetcode.model;

import java.util.Objects;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "cities")
public class City {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private int population;

    public City() {
    }

    public City(String name, int population) {
        this.name = name;
        this.population = population;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getPopulation() {
        return population;
    }

    public void setPopulation(int population) {
        this.population = population;
    }

    @Override
    public int hashCode() {
        int hash = 7;
        hash = 79 * hash + Objects.hashCode(this.id);
        hash = 79 * hash + Objects.hashCode(this.name);
        hash = 79 * hash + this.population;
        return hash;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        final City other = (City) obj;
        if (this.population != other.population) {
            return false;
        }
        if (!Objects.equals(this.name, other.name)) {
            return false;
        }
        return Objects.equals(this.id, other.id);
    }

    @Override
    public String toString() {

        var builder = new StringBuilder();
        builder.append("City{id=").append(id).append(", name=")
                .append(name).append(", population=")
                .append(population).append("}");

        return builder.toString();
    }
}
```



- This is the City entity. Each entity must have at least two annotations defined: `@Entity` and `@Id`.
  - The @Entity annotation specifies that the class is an entity and is mapped to a database table. 
  - The @Table annotation specifies the name of the database table to be used for mapping.
  - The @Id annotation specifies the primary key of an entity and the 
    @GeneratedValue provides for the specification of generation strategies for the values of primary keys.

---

```sql
-- resources/import.sql
INSERT INTO cities(name, population) VALUES('Bratislava', 432000);
INSERT INTO cities(name, population) VALUES('Budapest', 1759000);
INSERT INTO cities(name, population) VALUES('Prague', 1280000);
INSERT INTO cities(name, population) VALUES('Warsaw', 1748000);
INSERT INTO cities(name, population) VALUES('Los Angeles', 3971000);
INSERT INTO cities(name, population) VALUES('New York', 8550000);
INSERT INTO cities(name, population) VALUES('Edinburgh', 464000);
INSERT INTO cities(name, population) VALUES('Berlin', 3671000);
```



- The schema is automatically created by Hibernate; 
  later, the import.sql file is executed to fill the table with data.

---


```java
// com/zetcode/repository/CityRepository.java
package com.zetcode.repository;

import com.zetcode.model.City;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface CityRepository extends CrudRepository<City, Long> {

}
```



- The @Repository annotation is used to define a repository.


---

```java
// com/zetcode/service/ICityService.java
package com.zetcode.service;

import com.zetcode.model.City;
import java.util.List;

public interface ICityService {

    List<City> findAll();
}
```

- ICityService provides a contract method to get all cities.

---

```java
//com/zetcode/service/CityService.java
package com.zetcode.service;

import com.zetcode.model.City;
import com.zetcode.repository.CityRepository;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class CityService implements ICityService {

    @Autowired
    private CityRepository cityRepository;

    @Override
    public List<City> findAll() {

        return (List<City>) cityRepository.findAll();
    }
}
```

- The `@Service` annotation declares CityService to be a service class; a class that provides business services. 
  The `@Autowired` annotation marks cityRepository field to be injected with CityRepository.

---


```java
com/zetcode/controller/MyController.java
package com.zetcode.controller;

import com.zetcode.service.ICityService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

import java.util.HashMap;
import java.util.Map;

@Controller
public class MyController {

    @Autowired
    private ICityService cityService;

    @RequestMapping("/")
    public String index(Model model) {

        return "index";
    }

    @RequestMapping("/cities")
    public ModelAndView showCities() {

        var cities = cityService.findAll();

        Map<String, Object> params = new HashMap<>();
        params.put("cities", cities);

        return new ModelAndView("showCities", params);
    }
}
```

- The `@Controller` annotation marks a class as a web controller. The `@RequestMapping` maps HTTP request 
  with a path to a controller method. In the second case, it maps the /cities URL to the showCities() method.

---


```html
<!-- resources/templates/index.ftlh -->
<!DOCTYPE html>
<html>
    <head>
        <title>Home page</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
    </head>
    <body>
        <a href="cities">Show cities</a>
    </body>
</html>
```


- This is the index.ftlh template file. It contains a link to create a request to show all cities.


---


```html
<!-- resources/templates/showCities.ftlh -->
<!DOCTYPE html>
<html>
    <head>
        <title>Cities</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="stylesheet" href="css/style.css">
    </head>
    <body>
        <h2>List of cities</h2>

        <table>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Population</th>
            </tr>

            <#list cities as city>
                <tr>
                    <td>${city.id}</td>
                    <td>${city.name}</td>
                    <td>${city.population}</td>
                </tr>
            </#list>
        </table>
    </body>
</html>
```

- This is the showCities.ftlh template file. It uses FreeMarker `#list` **macro** to display all city objects.

---


```java
com/zetcode/Application.java
package com.zetcode;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```


- The `@SpringBootApplication` enables auto-configuration and component scanning.
  - `mvn spring-boot:run`



































