## lombok @Accessors注解的用法

Accessor的中文含义是存取器，@Accessors注解用来配置lombok如何产生和显示getter和setter的方法。

该注解既可以注解在类上也可以注解在属性上。

@Accessors有三个属性

fluent
chain
prefix
下面用代码举例说明。

---


### fluent

- fluent的中文含义是流畅的，设置为true，则getter和setter方法的方法名都是基础属性名，且setter方法返回当前对象。代码如下：

```java
@Data
@Accessors(fluent = true)
public class Person {
    private Long id;
    private String name;
    
    // 生成的getter和setter方法如下，方法体略
    public Long id() {}
    public Person id(Long id) {}
 
    public String name() {}
    public Person name(String name) {}
}
```






---

### chain

- chain的中文含义是链式的，设置为true，则setter方法返回当前对象。代码如下：


```java
@Data
@Accessors(chain = true)
public class Person {
    private Long id;
    private String name;
    
    // 生成的setter方法如下，方法体略
    public Person setId(Long id) {}
    public Person setName(String name) {}
}
 
//这里加个举例说明，按如下调用后 就将person对象的id设置成1，姓名设置成 "李明"。
Person person=new Person();
person.setId(1).setName("李明");
```


---

### prefix

- prefix的中文含义是前缀，用于生成getter和setter方法的字段名会忽视指定前缀（遵守驼峰命名）。代码如下：


```java
@Data
@Accessors(prefix = "p")
class Person {
	private Long pId;
	private String pName;
 
	// 生成的getter和setter方法如下，方法体略
	public Long getId() {}
	public void setId(Long id) {}
 
	public String getName() {}
	public void setName(String name) {}
}
```
