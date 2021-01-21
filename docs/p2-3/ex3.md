## 

- 两种处理异常手段： 1. 返回给前端，2. 记录日志

---

## 已知exception, 未知exception


---

## 自定义 HTTPException


```java
public class HttpException extends RuntimeException {
    protected Integer code;
    protected Integer httpStatusCode = 500;
}
```


```java
public class NotFoundException extends HttpException {
    public NotFoundException(int code){
        this.httpStatusCode = 404;
        this.code = code;
    }
}
```

```java
//被禁用的异常
public class ForbiddenException extends HttpException {
    public ForbiddenException(int code){
        this.code = code;
        this.httpStatusCode = 403;
    }
}
```

- `HttpException extends RuntimeException`, ` NotFoundException extends HttpException`
























