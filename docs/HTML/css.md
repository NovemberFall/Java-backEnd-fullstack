## CSS 1


- What is CSS?
  - CSS stands for Cascading Style Sheets.
  - describes how HTML elements (titles, images, paragraph...) 
    are to be displayed on screen, paper, or in other media


- How to add CSS to HTML?
  
- Inline Styles （Highest priority）
  `<h1 style="color:blue;">This is a heading</h1>`

- Internal(内部的) Style（Priority lower than inline style）

```css
<head>  
    <style>    
        h1 {	
            color: maroon;    
        }   
    </style>
</head>
```

- External(外部的) Style（Priority lower than internal style）
  - Each page must include a reference to the external style sheet file inside the 
    `<link>` element
  - The `<link>` element goes inside the `<head>` section:


```html
<head>  
    <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

### 总结：

- inline, 是在行内写css, 很少用
- internal, 使用style, 并且是放在 `<head>` 里的， 也是很少用
- external, 这个工业界经常使用， 用 link 

---
![](img/2020-07-22-21-48-05.png)

- The selector  
  -  points to the HTML element you want to style.  
- The declaration block 
  - contains one or more declarations separated by semicolons.
  - each declaration includes a CSS property name and a value, separated by a colon.
  - always ends with a semicolon
  - declaration blocks are surrounded by curly braces.

---

#### class exercise 1:

```html
<!-- set h1 tag font color as red, using inline style-->
<h1 style=”color:red;”>I like web development</h1>

<!-- set p tag background color to blue, using internal style-->
<p style=”background-color:blue”>I am a paragraph</p>

<!-- set span font size to 24px, using internal style-->
<span style=”font-size:24px;”>I am a span</span>
```

---

## CSS Selectors

1.	all elements *
2.	element
3.	#id 
4.	.class
5.	element element
6.	element, element
7.	element > element
8.	[attribute]
9.	pseudo classes
10.	pseudo elements

- [具体可以参考 w3c](https://www.w3schools.com/cssref/css_selectors.asp)

---

- all elements *

```css
* {
    color: blue;
}
```

- element:
  - The element selector selects elements based on the element name.
  -	e. g. p selects all `<p>` elements

```css
p {
    color: blue;
}
```

- #id
  - The id selector uses the id attribute of an HTML element to select a specific element.
  -	The id of an element should be unique within a page, 
    so the id selector is used to select one unique element!
  -	To select an element with a specific id, write a hash (#) character, 
    followed by the id of the element.
  -	Must contain at least one character
  -	Must not contain any space characters
  
- e.g. #firstname - selects the element with id="firstname"

```css
<li id="">CA</li> 

#li-ca {
      color: blue;
}
```

---

- class
  -	The class selector selects elements with a specific class attribute.
  -	To select elements with a specific class, write a period (.) character, 
    followed by the name of the class.

- e.g. .intro - selects all elements with class="intro"

---

#### Exercise 2:

```html
<!-- h1 - set font to 30px， font size to 30px-->

<!-- date - set font color to purple， font size to 24px -->

<!-- author - set font color to green， font size to 24px -->

<!-- news content - set font color to blue， font size to 18px-->
```


- Answer:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
<!-- 标题 - 颜色为红色， 字体为30px-->
<!-- 日期 - 颜色为紫色， 字体为24px -->
<!-- 作者 - 颜色为绿色， 字体为24px -->
<!-- 新闻内容 - 颜色为兰色， 字体为18px-->


<h1>Amazon picks 20 finalists for its second headquarters</h1>
<p>by <span class="author">Kaya Yurieff</span> from cnn <span class="date">January 18, 2018: 10:44 AM ET</span> </p>
<p>Amazon has released a "short" list of cities it's considering for its second headquarters.</p>
<p>The 20 potential cities are Atlanta; Austin; Boston; Chicago; Columbus, Ohio; Dallas; Denver; Indianapolis; Los Angeles; Miami; Montgomery County, Maryland; Nashville; Newark; New York City; Northern Virginia; Philadelphia; Pittsburgh; Raleigh; Toronto and Washington, D.C.</p>

</body>
</html>
```

```css
h1 {
  color: red;
  font-size: 30px;
}
p {
  color: blue;
  font-size: 18px;
}
.author {
  color: green;
  font-size: 24px;
}
.date {
  color: purple;
  font-size: 24px;
}
/* You can also use ID selector to write your CSS as well */
```

