## 全局异常处理机制导学

- 来写一个异常

- 添加两个注解： `@ControllerAdvice`, ` @ExceptionHandler(value=Exception.class)`

```java
@ControllerAdvice
public class GlobalExceptionAdvice {

    @ExceptionHandler(value=Exception.class)
    public void handleException(HttpServletRequest req, Exception ex) {
        System.out.println("hello");
    }
}



@RestController
@RequestMapping("/v1/banner")
public class BannerController {

    @Autowired
    private ISkill iSkill;

    @GetMapping("/test")
    public String test() throws Exception{
        iSkill.r();
        throw new Exception("Error.");
    }
}
```

![](img/2021-01-05-11-33-02.png)


---

### UnifyResponse 统一错误响应

```json
{
    code:10001
    message:xxxx
    request: GET url
}
```



























































































