## 异常分类

- Throwable      (所有都继承与它)

- Error           (错误，程序无法运行)
- Exception       (异常, 程序可以运行)
  - exception, 1/0


- CheckedException         (在代码里进行处理，不处理编译无法通过)
- RuntimeException         (不强制要求处理，在编译阶段可能发现不了。)


- HttpException extends RuntimeException 
- APIException extends Exception        (实际上是一个CheckedException)
