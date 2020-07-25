# Java Servlet | HTTP request and response

- Goal
  - Create my first servlet to provide a simple service

---

### HTTP request and response

- In our project, what http methods shall we use in the following cases?
  -	Search for events nearby, giving a geo location, return a list of events. [GET]
  -	Recommend events for the user, giving user information, return a list of recommended events. [GET]
  -	Get user favorite events, giving user information, return a list of favorite events. [GET] 
  -	Set/Unset user favorite events, giving user information and events to set/unset, 
    return OK if operation is successfully done. [POST/DELETE]
  -	Login [POST], 因为你如果用 `get` 发起请求，比如你要登录 chase bank, 它在 login 的时候，用
    `get` method, 把我们的账号密码 全部显现在 url 后面， 如果有人看到，这是非常危险的， 而 `post`
    会在单独的 request body 里。 不会在 url 里.
    - 所以 sigup 肯定也是用 `post`
 
![](img/2020-07-24-19-59-45.png)
![](img/2020-07-24-20-00-26.png)

- HTTP supports all CRUD (Create/Read/Update/Delete) operations. 
  Two commonly used methods are:
  - **GET  - Request** data from server.
  - **POST - Update** data on server.  


## Endpoint

![](img/2020-07-24-20-13-44.png)

- A URL is used to uniquely identify a resource over the web. URL has the following syntax:
  - `protocol://hostname:port/endpoint?query`
  - `http://www.laioffer.com:80/index.html`



## HTTP request/response body

![](img/2020-07-24-20-15-14.png)
![](img/2020-07-24-20-15-27.png)

- A message body is the one which carries the actual HTTP request data 
  (including form data and uploaded etc.) and HTTP response data from 
  the server ( including files, images etc). Normally we don’t return static HTML code 
  to frontend directly because it should be created by frontend developer. 
  We just need to return correct data that should be displayed by frontend. 
  In our project, we’ll use JSON as for body format.

---

## Create First Java Servlet

- Step 1, open Eclipse. Right click on your project `Jupiter`, choose New->Servlet. 

- Step 2, name it `SearchItem` and the package name is `rpc`, then click Finish.

![](img/2020-07-24-21-04-57.png)

- Eclipse will automatically create a Java class called SearchItem in package rpc for you. 

![](img/2020-07-24-21-06-03.png)

- Step 3, At line 13, change the url mapping to “/search”.

- Step 4, Save your change and right click on ‘Tomcat v9.0 Server at localhost’, 
  choose `Start`.


![](img/2020-07-24-21-09-19.png)

![](img/2020-07-24-21-20-18.png)

#### Or you can test it in Postman:

![](img/2020-07-24-21-23-01.png)


- Step 6, update doGet to return data in HTML format.





