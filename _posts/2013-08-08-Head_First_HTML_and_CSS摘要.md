---
title: Head First HTML and CSS 摘要
layout: post
guid: urn:uuid:6d5ff453-e05b-466f-82cc-0a63a664a39d
tags:
  - 程序
---


##1 Getting to know HTML /The Language of the Web

In Chapter 1 we kicked the tires of HTML and found it to be a nice
markup language (the “ML” in HTML) for describing the structure of web pages. Now
we’re going to check out the “HT” in HTML, hypertext, which will let us break free of
a single page and link to other pages. Along the way we’re going to meet a powerful
new element, the &lt;a> element

* paragraph of text 段落 &lt;p>

* quotes引用&lt;q>  
The &lt;blockquote> element is a block element and the &lt;q> element is an inline element

* break 换行&lt;br>  
void elements：Elements that don’t have any content by design are called void elements.
“void” comes from computer science and means “no value.”

* list item 列&lt;li> ordered list &lt;ol> unordered list &lt;ul>  
definition list &lt;dl>term&lt;dt>description&lt;dd>

a list is really a group of items: the &lt;li> element is used to identify each item, and the &lt;ol> element is used to group them together.

**To understand the nesting relationships, draw a picture**

***
##2 Going further with hypertext /Meeting the “HT” in HTML
&lt;img src="../images/red.jpg"> ..回到父文件夹

***
##3 Building blocks /Web Page Construction
In this chapter we’re going to ramp up construction: you’re going to take a web page from conception
to blueprint, pour the foundation, build it, and even put on some finishing touches.

P87问题：为何要专门用&lt;q>，而不用“”表示应用，这是故意搞复杂么？  
1.引号不一定是引用。如 a “remixed” quote  
2.标记语言，要体现标记的作用，给内容分类好，让浏览器知道是什么。
***

##4 getting connected /A Trip to Webville
protocol ：//website name/absolute path  
http://www.starbuzzcoffee.com/  即是根文件夹

&lt;a href="http://wickedlysmart.com/buzz" title="Read all about caffeine on the Buzz">Caffeine Buzz&lt;/a>  
target="_blank"即在新窗口或标签页打开

同一页 link to elements with ids  
&lt;a href="index.html#chai">See Chai Tea&lt;/a>  

&lt;a> now can be used to create links from all kinds of things.  

***

##5 Adding images to your pages  /Meeting the Media

JPEG, PNG, and GIF are the three formats for images that are widely supported by web browsers.

&lt;img src="http://wickedlysmart.com/pencil.png" alt="The typical new pencil can draw a line 35 miles long." width="48" height="100">

>不要用这种方式改变图片显示大小，浏览器还是要下载原图片  
you’re still downloading the full-size image,and making the browser do the work to resize the imag  

>If you’re setting the image width and height to the correct dimensions, then it is really just informational. However, if you are using the width and height to resize he image in the browser, then you are using these attributes for presentation. In that case, it’s probably better to consider using CSS to achieve the same result.

显示缩略图，点击出现大图  
&lt;a href="html/seattle_downtown.html">&lt;img src="thumbnails/seattle_downtown.jpg"alt="An iPod in downtown Seattle, WA">&lt;/a>

***
##6 Standards and all that jazz /Getting Serious with HTML
&lt;!doctype html>

&lt;meta charset="utf-8">


<http://validator.w3.org> 测试html

***
##7 Getting started with CSS /Adding a Little Style
<br>
###Getting CSS into your HTML:
1. &lt;style>&lt;/style>
2. &lt;link type="text/css" rel="stylesheet" href="lounge.css">

###The world’s smallest and fastest guide to how styles are applied
1. First, do any selectors select your element?
2. If there are no selectors that match your element, then you rely on inheritance
3. Then use the default
4. What if multiple selectors select an element? if one rule is more **specific** than the others, then it wins.
   P460 **To calculate the specificity**  ids>classes>element
5. And if we still don’t have a clear winner?
>If you can’t resolve a conflict because two selectors are equally specific, you use the ordering of the rules in your stylesheet file; that is, you use the rule listed last in the CSS file (nearest the bottom).



### css 检查工具
>Those W3C boys and girls aren’t just sitting
around on their butts, they’ve been working hard.  
You can find their CSS validator at:
<http://jigsaw.w3.org/css-validator/>

***
## 8 styling with fonts and colors / Expanding Your Vocabulary
<br>
### font
body {  
font-family: Verdana, Geneva, Arial, sans-serif;  若前3个都没有，则用浏览器默认的'sans-serif'字体  
}  
The font-family property gives you a way to create a list of preferred fonts.

#### How Web Fonts work
1. the browser first retrieves an HTML page that references them
2. The browser then retrieves the Web Font files needed for the page.
3. ith the font retrieved, the browser uses the font when it displays the page.

#### How to add a Web Font to your page...
P325 
*Add the @font-face property to your CSS*
>@font-face{  
font-family: "Emblema  
src: url("http://wickedlysmart.com/hfhtmlcss/chapter8/journal/EmblemaOne-Regular.woff"),  
url("http://wickedlysmart.com/hfhtmlcss/chapter8/journal/EmblemaOne-Regular.ttf");  
}

###font 属性
* font-size: font-size: 14px;     父元素的 150%；1.5em;   keywords=medium 共七级

* font-weight: bold; normal;

* font-style: oblique;  italic;  



###  Color
1. by name: There are 16 basic colors and 150 extended colors;
2. in red, green, and blue values
>background-color: rgb(80%, 40%, 0%);  因为全满是（255，255，255）  
background-color: rgb(204, 102, 0);  
background-color: #cc6600;  因为这就是16进制的(204=12x16+12,102=6x16+6,0)  

### text-decoration: 
underline; 或者 `border-bottom: thin dotted #888888;`

***
##9 the box model /Getting Intimate with Elements

>To do advanced web construction, you really need to know your building materials. In this chapter we’re going to take a close look at our building materials: the HTML elements. We’re going to put block and inline elements right under the microscope and see what they’re made of. You’ll see how you can control just about every aspect of how an element is constructed with CSS.

### Box Model
>All elements are treated as boxes: 
paragraphs, headings, block quotes,lists, list items, and so on. Even inline elements like &lt;em> and links are treated by CSS as boxes.

The **width property** specifies the width for the content area only.
To *figure out the width of the entire box*, you need to add the width of the content area to the width of the left and right margins, the left and right padding, and the border width.

元素默认的宽度  
Q:If I don’t set the width of an element, then where does the width come from?  
A:The default width for a block element is “auto”, which means that it will expand to fill whatever space is available.   

盒子模型无margin,padding,borders则content占据整个盒子  
Q:What if I don’t have any margin, padding, or borders?  
A:Then your content gets to use the entire width of the box.

宽度设为百分比：以容器的宽度计算  
Q:What are the different ways I can specify widths?  
A:You can specify an actual size— usually in pixels—or you can specify a percentage. If you use a percentage, then the width is calculated as a percentage of the width of the container the element is in(which could be the &lt;body>, a &lt;div>, etc.).

高度应默认，否则content会溢出至其他元素  
Q:What about the height?  
A:In general, the height of an element is left at the default, which is auto, and the browser expands the content area vertically so all of the content is visible. You can explicitly set a height, but you risk having the bottom of your content overflow into other elements if your height isn’t big enough to contain it. In general, leave your element heights unspecified so they default
to auto.



###Padding, border, and margins
<br>

####A two-minute guide to borders
* border-style: groove;等共八种
* border-width: thin;medium;thick  或 px
* border-color:
* border-radius: 15px;  具体 border-top-left-radius: 3em;

#### id vs class
> Why do I need an id just to prove something is unique on the page? I could use a class exactly the same way, right?  
1. id团队人员不会误改   
2. when you start positioning elements on a page, you’ll need each element you want to position to have a unique id.  

####非桌面浏览器下的css (Stylesheets—they’re not just for desktop browsers anymore...) P400
&lt;link href="lounge-mobile.css" rel="stylesheet" media="screen and (max-device-width: 480px)">  
&lt;link href="lounge-print.css" rel="stylesheet" media="print">  
&lt;link rel="stylesheet" href="lounge-tablet-landscape.css" media=" screen and (max-device-width: 1024px) and (orientation:landscape)">

rather than using media queries in link tags, you can also use them right in your CSS.
>@media screen and (max-device-width: 480px) {  
/#guarantee {  
margin-right: 30px;  
}

***
##10 divs and spans /Advanced Web Construction
<br>
###Let’s explore how we can divide a page into logical sections
1. Identifying your logical sections 
2. Using div s to mark sections
3. Labeling the divs

### test-align: center; 对div子block元素中content影响
>All the text inside the &lt;div>
element is in nested block elements, but it is
all aligned now. That’s because these block
elements inherit the text-align property
from the &lt;div>. So here’s the difference:
rather than the &lt;div> itself aligning the
text in the headings and the paragraphs
(which it won’t do because these are block
elements), the headings and paragraphs
are inheriting the text-align value of
“center”, and then aligning their own content
to center.

**line-height**: 1;  
对每一级line-height都是 1 times its own font size;  

### 盒子模型设定的shortcut P442
>Q:Should I always use shorthand? 简写必要么？
A:Not necessarily. Some people find the long form more
readable. Shorthands do have the advantage of reducing the size
of your CSS files, and certainly they are more quickly entered
because they require less typing. However, when there is a
problem, they are a little more difficult to “debug” if you have
incorrect values or the wrong order. So, you should use whichever
form is more comfortable because they are both perfectly valid.

### span 与 strong的不同用处
Q:When do I use a &lt;span> rather  than another inline element like &lt;em> or  &lt;strong>?   
A:(mark up your content) VS (to change the style of certain words)

###什么是 行内元素，我可以给行内元素设定 宽度 等属性么
Q:Can I set properties like width on &lt;span> elements? Actually, what about **inline elements** in general?
>A：You can set the width of inline elements like &lt;span>, &lt;em>, and &lt;strong>, but you won’t notice any effect until you position them. You can also add margin and padding to these elements, as well as a border. Margins and padding on inline elements work a little differently from block elements—if you add a margin on all sides of an inline element, you’ll only see space added to the left and right. You can add padding to the top and bottom of an inline element, but the padding doesn’t affect the spacing of the other inline elements around it, so the padding will overlap other inline elements.
>Images are a little different from other inline elements. The width, padding, and margin properties all behave more like they do for a block element. Remember from Chapter 5: if you set the width of an image using either the width attribute in the &lt;img> element or the width property in CSS, the browser scales the image to fit the width you specify. This can sometimes be handy if
you can’t edit the image yourself to change the dimensions, and you want the image to appear bigger or smaller on the page. But remember, if you rely on the browser to scale your image, you may be downloading more data than you need (if the image is larger than you need).

### 伪类的应用 A link can be in a few states: it can be unvisited, visited, or in the hover state 
1. 什么是伪类？  
a:link,a:visited, and even a:hover all allow you to specify style, just like they were classes. So, those are pseudo-classes. In other words, you can style pseudo-classes, but no one ever types them into their HTML.

2. 怎么实现的？  
The browser goes through and adds all your &lt;a> elements to the right pseudo-classes.

###关于“层级"样式表 talk about the “cascade”? P457
1. Gather all your stylesheets together.
2. Find all the declarations that match.
3. Now take all your matches, and sort them.
4. Now sort all the declarations by how specific they are.
5. Finally, sort any conflicting rules in the order they appear in their individual stylesheets.


***
## 11 layout and positioning /Arranging Elements
<br>

### FLow 浏览器如何排列布置html元素
1. block的flow  
Each block element is taken in the order it appears in the markup, and placed on the page.

2. inline元素的flow  
Inline elements are flowed next to each other, horizontally, from top left to bottom right.
text is a special case of an inline element. The browser breaks it into inline elements that are the right size to fit the space.

###How to float an element
1. give it an identity
2. give it a width
3. float it  
漂浮的元素不再属于正常流，其下是正常流的block元素，但这些block元素中的inline元素会知道漂浮元素的边界，在其周围flow


###布局 CSS layout toolbox
<br>
 
####两栏布局 The Floating Layout
>sidebar float;  
main margin-right 算好距离；  
footer clear:right;

**改进为 The Jello Layout** 布局(页面居中，浏览器左右留白)
Liquid and frozen designs:整个body下是一个包含所有其他元素的div，并给定宽度；  
margin-left: auto;  
margin-right: auto;  

####绝对位置布局 The Absolute Layout
>By setting the sidebar to a specific width, and positioning it
to the right of the main content, we have a main content area that
expands and contracts with the size of the page, and a sidebar that
stays fixed in size and is anchored to the right side of the browser
window. This is a great choice for layouts when you want one
part of your page to be fixed in size and one part to expand and
contract, or when you need an element to be located at a precise
location 

####css表格布局 CSS table display ：
P513 逻辑包含图：  
div table;(display: table;)  
table其下是div Row;(display: table-row;)  
Row  其下是div column;(display: table-cell;)（vertical-align: top;）  
（You can set the width of each column By using percentages ）  

>`&lt;div id="tableContainer">`  
  `&lt;div id="tableRow">`  
   `&lt;div id="main">`  
    /...
   `&lt;/div>`  
   `&lt;div id="sidebar">`  
    /...
   `&lt;/div>`  
 `&lt;/div>`  
`&lt;/div>`

### Position 

1. abusolute 相对页面定位  
the flowed elements don’t know about the absolutely positioned elements at all, so the inline content in the flowed elements doesn’t wrap around the absolutely positioned elements.
2. fixed 相对浏览器定位
3. relative 还在flow中:  
the element is left in the flow of the page (where it would normally be), and then shifted by the amount you specify.

***
## 12 html5 markup /Modern HTML
<br>
###将一些特定的div 功能化，更好的体现mark up，让浏览器更懂如何处理
&lt;nav> &lt;header> &lt;footer> &lt;aside>  
&lt;article> &lt;section>  
&lt;progress>&lt;meter>&lt;canvas>&lt;figure>&lt;mark>  
&lt;time>（&lt;time datetime="2012-03-12">3/12/2012&lt;/time>）  
而后css中，和body一样写css,即 footer{}即可。

### &lt;video> 的用法
P586 视频种类（webm,mp4,ogg）及包含的编码
>video用法  
&lt;video controls autoplay width="512" height="288" poster="images/poster.png"  >  
&lt;source src="video/tweetsip.mp4" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'>  
&lt;source src="video/tweetsip.webm" type='video/webm; codecs="vp8, vorbis"'>  
&lt;source src="video/tweetsip.ogv" type='video/ogg; codecs="theora, vorbis"'>  
&lt;p>Sorry, your browser doesn't support the video element&lt;/p>  
&lt;/video>

##13 tables and more lists/Getting Tabular
<br>
### HTML表格及嵌套
&lt;table>  (border: thin solid black;caption-side: bottom;border-collapse: collapse;)  
&lt;caption>  
&lt;tr>  
&lt;th>  
&lt;td>  

####css中如何隔行选元素（ nth-child伪类 ）
p:nth-child(even) {background-color: red;}  
p:nth-child(odd) {background-color: green;}  

####Giving the list some style 列表自定义图标
list-style-type: disc;circle;square; 或自定义图片 list-style-image: url(images/backpack.gif);

***

##14 HTML表单/交互  （html forms /Getting Interactive）
<br>

###表单包含种类
1. 文字表单  
text input：  &lt;input type="text" name="fullname">  
textarea:     &lt;textarea name="comments" rows="10" cols="48">&lt;/textarea>  
email input:  &lt;input type="email"> 在移动设备下，可能会调用对应输入界面  
tel input:    &lt;input type="tel">  
url input:    &lt;input type="url">  

2. 提交submit input: &lt;input type="submit">  

3. 选择  


* radio input:  &lt;input type="radio" name="hotornot" value="hot">&lt;input type="radio" name="hotornot" value="not">  
* checkbox input:  
>&lt;input type="checkbox" name="spice" value="Salt">  
&lt;input type="checkbox" name="spice" value="Pepper">  
&lt;input type="checkbox" name="spice" value="Garlic">  
* 下拉选择框 select:  
&lt;select name="characters">  
  &lt;option value="Jersey">New Jersey&lt;/option>  
  &lt;option value="John">John Parker&lt;/option>  
&lt;/select>  
* Number input: &lt;input type="number" min="0" max="20"> 数字框  
* range input： &lt;input type="range" min="0" max="20" step="5">  滑动条  
* color input:  &lt;input type="color">  
* date input:   &lt;input type="date">  

例子：
>&lt;form action="http://wickedlysmart.com/hfhtmlcss/contest.php" method="POST">  
（这个action，就是提交的表单的去向，由该文件处理）  
&lt;p>  
 Choose your beans:  
  &lt;select name="beans">  
  &lt;option value="Guatemala">Organic Guatemala&lt;/option>  
  &lt;option value="Kenya">Kenya&lt;/option>  
  &lt;/select>  
&lt;/p>

  &lt;p>Ship to: &lt;br>  
   Name: &lt;input type="text" name="name"> &lt;br>  
   Address: &lt;input type="text" name="address"> &lt;br>  
   Phone: &lt;input type="tel" name="phone"> &lt;br>  
  &lt;/p>

  &lt;p>  
   &lt;input type="submit" value="Order Now">  
  &lt;/p>  
&lt;/form>  

### Post 和 Get 的区别
1. post是浏览器将你表单作为request一部分发送，用户不可见
2. get是将表单信息作为URL一部分，再发起request。

####为啥提交信息也叫GET。  
Q:Why is it called GET if we’re sending something to the server?  
A: Good question. What’s the main job of a browser? To get web pages from a server. And when you are using GET, the browser is just going about getting a web page in the normal way it always does, except that, in the case of a form, it has appended some
more data to the end of the URL. Other than that, the browser just acts like it’s a normal request. 
With POST, on the other hand, the browser actually creates a little data package and sends it to the server.

####什么时候用GET，什么时候用POST  
Q:So why would I use POST over GET, or vice versa?  
A：1.如果你需要用户能够bookmark提交表单后的页面，用GET。比如bookmark返回的搜索结果，下次直接能看到，不用重新提交表单。（因为bookmard的当前url里面已经包含所有表单信息了）  
2.安全用Post  
3.textarea之类数据量大的用post  

***
## 附录：10个未包含的话题 （Appendix: leftovers /The Top Ten Topics(We Didn’t Cover)）

1.  **More CSS selectors**  
<http://www.w3school.com.cn/cssref/css_selectors.asp>

2. **Vendor-specific CSS properties**  
例子：  
>div {  
transform: rotate(45deg);  
-webkit-transform: rotate(45deg);  
-moz-transform: rotate(45deg);  
-o-transform: rotate(45deg);  
-ms-transform: rotate(45deg);  
}

3. **CSS transforms and transitions**  
通过box 和 box:hover 使图形翻转

4. **Interactivity**  
包含js，的交互

5. **HTML5 APIs and web apps**  
 HTML5 comes with a whole new set of application programming interfaces (APIs for short) that are accessible through JavaScript.  
 These APIs open up a whole new universe of expression and functionality to your web pages. 

6. **More on Web Fonts**

7. **Tools for creating web pages**

8. **XHTML5**

9. **Server-side scripting**  
Web languages are constantly evolving; PHP, Python, Perl, Node.js, Ruby on Rails, and JavaServer Pages (JSPs) are all commonly used

10. **Audio**  
类似&lt;video>  
>&lt;audio src="song.mp3" id="boombox" controls>  
Sorry but audio is not supported in your browser.
&lt;/audio>



















































































