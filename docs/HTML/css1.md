## CSS II   

### Box Model

![](img/2020-08-16-13-02-15.png)


- The CSS box model is essentially a box that wraps around every HTML element. 
  It consists of: margins, borders, padding, and the actual content. 

- Explanation of the different parts:
  - Content - The content of the box, where text and images appear
  - Padding - Clears an area around the content. The padding is transparent
  - Border - A border that goes around the padding and content
  - Margin - Clears an area outside the border. The margin is transparent

- Every element on a page is a rectangular box.

- There are actually two types of box model, one is W3C standard, the other is IE model. 
  Basically they all calculate the element width and height based on the content width, 
  content height, padding and border, but their formula are different:

- **1. W3C standard**
  - <U>outer box (element space size)</U>
  - Element space width = content width + padding + border + margin
  - Element space height = content height + padding + border + margin

  - <U>inner box (element size)</U>
  - Element width = content width + padding + border
  - Element height = content height + padding + border



- **2. IE box model**
  - <U>outer box (element space size)</U>
  - Element space width = content width + margin 
  - Element space height = content height + margin
  - (content width including padding and border)


![](img/2020-08-21-15-35-09.png)





- **3. Margin Collapsing**


![](img/2020-08-21-15-36-29.png)

![](img/2020-08-21-15-49-32.png)

- [Test Margin Collapse](https://css-tricks.com/what-you-should-know-about-collapsing-margins/)


---

## 2. Floating

- The float CSS property specifies that an element should be placed along the left or 
  right side of its container, allowing text and inline elements to wrap around it. 
  The element is removed from the normal flow of the web page, though still remaining 
  a part of the flow.

- **How floated elements are positioned：**
  - when an element is floated, it is taken out of the normal flow of the 
    document (though still remaining part of it). It is shifted to the left, 
    or right, until it touches the edge of its containing box, 
    or another floated element.



- **Syntax**
  - float: none|left|right|inherit;

  - The float property can have one of the following values:
    - left - The element floats to the left of its container
    - right- The element floats to the right of its container
    - none - The element does not float 
      (will be displayed just where it occurs in the text). This is default
    - inherit - The element inherits the float value of its parent
  
- **Important facts:**
  - 1.	float first
    - When a container has multiple elements, some of them are floating, some of them 
      are not, remember to put all the floating elements in front of the 
      non-floating ones! Browsers try to figure out the spacing for those 
      floating ones first.

![](img/2020-08-21-16-41-24.png)

- float: 分为 left float, right float
  - float 会 导致 父容器高度塌陷
    - block 元素 无法探知 float 元素的位置
      - 但是 inline | inline-block | float   是可以探知 float 的位置


- clear :
  - The clear property specifies on which sides of an element floating elements 
    are not allowed to float.
    - `.clear { clear: both; /* it can be left|right|both */ }`


![](img/2020-08-21-17-12-32.png)


- **inline-block**
  - Floating works great, but as you see we need to apply the `.clear` to clear out the 
    floating even for a block element. There is another way to achieve the floating 
    effect, that is to use inline-block display.
  - similar to inline, inline-block allows multiple elements to layout on the same line, 
    the beauty of it is that elements can automatically wrap around if the wrapper 
    container is too small, and if you add a block element right after an inline-block 
    element, we don’t need to use the ugly `.clear` fix.

- https://developer.mozilla.org/en-US/docs/Web/CSS/overflow


---

## 3. Position

- **static (default)**
  - Default value, means the element is not positioned! A static element is said to 
    be not positioned and an element with its position set to anything else is said to 
    be positioned.


- **relative**
  - The top, right, bottom and left properties of a relatively-positioned element will 
    cause it to be adjusted away from **its original position**. Other content will 
    not be adjusted to fit into any gap left by the element.

![](img/2020-08-21-21-24-08.png)


- **absolute**
  - The top, right, bottom and left properties of an absolute-positioned element will 
    cause it to be positioned relatively to **the nearest positioned ancestor**.

![](img/2020-08-21-21-28-41.png)



- **fixed**
  - A fixed element is positioned **relative to the viewport**, which means it always 
    stays in the same place even if the page is scrolled. 




- create `relative-position.html`


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relative-Position</title>
    <style>
        body,div{
            padding:0;
            margin:0;
        }
        div{
            border: 1px solid blue;
        }

        .rl{
            width: 200px;
            height: 200px;

            /* step 1 相对定位 */
            /* 设置了相对定位之后， 容器的css就可以设置left, right, top, bottom属性 */
            position: relative;
            /* 相对于元素原来的位置 */
            left: 10px;
            top: 20px;
        }

        /* step 2 绝对定位 */
        .ab{
            width: 200px;
            height: 100px;
            background-color: lightpink;

            /* step 2.1 */
            position: absolute;
            top: 30px;
            left: 100px;
        }

        /* tep 3 设置父容器定位 */
        .parent{
            width: 400px;
            height: 500px;
            background-color: lightgray;

            /* step 4 加上定位 */
            position: relative;
        }

        /* step 5 fix position */
        .f{
            position: fixed;
            top:0;
            right: 0;
            height: 100px;
            width: 100px;
            background-color: lavender;
        }
    </style>
</head>
<body>
    <!-- step 1 相对定位 -->
    <div class="rl">
        this is a div - Relative-Position
    </div>

    <!-- step 2 绝对定位 -->
    <div class="ab">
        this is a div - absolute-Position
    </div>

    <!-- step 3 设置父容器定位 comment掉上面的ab -->
    <div class="parent">
        <div class="ab">
            this is a div - absolute position
        </div>
    </div>

    <!-- step 5 fix position -->
    <div class="f">
        fix position
    </div>

</body>
</html>
```


![](img/2020-08-21-21-48-19.png)

- [example](http://jsbin.com/xepegoh/5/edit?html,css,output)


---


## Z-index

- The z-index property specifies the stack order of an element.

- An element with greater stack order is always in front of an element with a lower stack order.
  - Note: z-index only works on positioned elements (position:absolute, position:relative, 
    or position:fixed).

![](img/2020-08-21-21-50-37.png)    


- create `z-index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>z-index</title>

    <style>
        .ab{
            position: absolute;
            height: 200px;
            width: 200px;
            border: 1px solid lightblue;
        }

        .d1{
            /* 中间层 */
            z-index: 100;
            left: 100px;
            top: 100px;
            background-color: ligthblue;
        }
        .d2{
            /* 最高层 */
            z-index: 200;
            background-color: lightpink;
        }
        .d3{
            /* 最底层 */
            z-index: 4;
            left: 20px;
            top: -30px;
            background-color: lightgreen;
        }
    </style>
</head>
<body>
    <div class="ab d1">中间层</div>
    <div class="ab d2">最高层</div>
    <div class="ab d3">最底层</div>
</body>
</html>
```

![](img/2020-08-21-21-57-16.png)


---

- [**4. Project HTML+CSS Part**](http://jsbin.com/rafomem/20/edit?html,css,output)




