## Spring IOC的核心机制：实例化与注入

### SpringBoot 最基础的编程模式 @Component + @Autowired

- `@Component` 会被加入到容器，做点实例：

- `missyou/sample/hero/`

```java
@Component
public class Diana {
    public void q(){
        System.out.println("Diana Q");
    }

    public void w(){
        System.out.println("Diana W");
    }

    public void e(){
        System.out.println("Diana E");
    }

    public void r(){
        System.out.println("Diana R");
    }
}

```

- 加上`@Component` springboot 就会自动把它加入容器，

- 现在我们使用 注入 `inject` 到 `api/v1/BannerController`

```java
@RestController
@RequestMapping("v1/banner")
public class BannerController {

    @Autowired
    private Diana diana;

    @GetMapping("/test")
    public String test(){
        diana.r();
        return "Hello World!";
    }
}
```

- `@Autowired`, 可以不用 new 一个实例，直接 call method

![](img/2021-01-04-15-44-04.png)

- console, show `Diana R`

---


## 标记上 @Service, 也将被 inject into container

- service/BannerService

```java
@Service
public class BannerService {
}



@RestController
@RequestMapping("v1/banner")
public class BannerController {

    @Autowired
    private Diana diana;

    @Autowired
    private BannerService bannerService;

    @GetMapping("/test")
    public String test(){
        diana.r();
        return "Hello World!";
    }
}
```

---

## stereotype annotations 模式注解

```java
@Component 组件/类/bean 类的实例化 new

@Service   
@Controller
@Repository

@Configuration
```

- 底下四个都是以第一个 Component为基础























































