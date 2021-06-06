---
title: "Markdown Syntax"
date: 2021-06-04T22:26:01+09:00
draft: true
---


> This post demonstrates basic markdown syntaxes.  
All references come from: [Markdown Guide](https://www.markdownguide.org/basic-syntax/) & [마크다운 문법](https://simhyejin.github.io/2016/06/30/Markdown-syntax/)


---


<br>

## 1. Headings

MARKDOWN        |RESULTS         
----------------|-------------------
`# Heading 1`   |<h1 style="text-decoration:none;">Heading 1</h1>
`## Heading 2`  |<h2>Heading 2</h2>
`### Heading 3` |<h3>Heading 3</h3>
`#### Heading 4`|<h4>Heading 4</h4>

\
\.

## 2. Paragraphs

MARKDOWN        |RESULTS         
----------------|-------------------
`Hello, I'm woogieboogie. My former major is arhcitecutre, but I just started coding to build things online! I'm a crypto enthusiast and love house music (especially the ones from france - french house.)`   | Hello, I'm woogieboogie. My former major is arhcitecutre, but I just started coding to build things online! I'm a crypto enthusiast and love house music (especially the ones from france - french house.)

\
\.

## 3. Line Breaks

MARKDOWN        |RESULTS         
----------------|-------------------
`This is the first line` >**spacebar*2 + return**< `And this is the second line`   | This is the first line. <br/> And this is the second line

\
\.

## 4. Emphasis
Type         |MARKDOWN           |RESULTS         
-------------|-------------------|-------------------
Bold         |`**Hello World**`  |**Hello World**
Italic       |`*Hello World*`    |*Hello World*
Bold & Italic|`***Hello World***`|***Hello World***

\
\.

## 5. Blockquotes
> To create Blockquotes: &nbsp; **just type ">" in front and that will do the magic.** <br>
> To continue blockquote with a **long paragraph, just continue to type ">" every line in front.**

\
\.

## 6. Nested Blockquotes & with other Elements
To create nested Blockquotes:
```
> Blockquotes can be nested by adding another ">", meaning you will have to add ">>"
>> This would be the nested blockquotes. So easy.
```

Results are:
> Blockquotes can be nested by adding another ">", meaning you will have to add ">>" before starting your line.
>> This would be the nested blockquotes. So easy.

Blockquotes can contain other Markdown formatted elements,<br>
***BUT NOT ALL - you need to examine which elements works nested in blockquotes.**
> Blockquotes can contain other elements:
>>`` ``` ``<br>
`def python:`<br>
`print(x)`<br>
`` ``` ``
>>> - As well as unordered lists
>>>> * Can be nested easily!

\
\.

## 7. Lists
Type            |MARKDOWN           |RESULTS         
----------------|-------------------|-------------------
Ordered Lists   |`1. First list`<br>`2. Second list`<br>`3. Third list`<br>`4. Fourth list`   |1. First list<br>2. Second list<br>3. Third list<br>4. Fourth list
Unordered Lists |`* First list`<br>`* Second list`<br>`* Third list`<br>`* Fourth list`       |- First list<br>- Second list<br>- Third list<br>- Fourth list
Indented Lists  |`1. First item`<br>`2. Second item`<br>`3. Third item`<br>&nbsp;&nbsp;&nbsp;&nbsp;`1. Indented item`<br>&nbsp;&nbsp;&nbsp;&nbsp;`2. Indented item`<br>`4. Fourth item`|<ol style="margin:0px;"><li>First item</li><li>Second item</li><li>Third item<ol><li>Indented item</li><li>Indented item</li></ol></li><li>Fourth item</li></ol>

\
\.

## 8. Lists - Elements in Lists
> **Preserve a line in between & Indent the element four spaces(or a tab)** to add another element in a list while preserving the coninuity of the list.

```
*   This is the first list item.
*   Here's the second list item.

    I need to add another paragraph below the second list item.
    > A blockquote would look great below the second list item.

*   And here's the third list item.
```
The results are:

*   This is the first list item.
*   Here's the second list item.

    I need to add another paragraph below the second list item.
    > A blockquote would look great below the second list item.

*   And here's the third list item.

\
\.

## 9. Code & Code Blocks
TYPE       | MARKDOWN              |RESULTS         
-----------|-----------------------|-----------------
Code       |`` `print(a+b)` ``     | `print(a+b)` 
Code Blocks|&nbsp;&nbsp;&nbsp;&nbsp;`<div>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<html>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<head>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</head>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</html>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;`</div>` <br>**four spaces / tab indentation before each line* | `<div>`<br>  &nbsp;&nbsp;`<html>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;`<head>`<br>  &nbsp;&nbsp;&nbsp;&nbsp;`</head>`<br>  &nbsp;&nbsp;`</html>`<br>`</div>`<br>**spaces excluded & html tags are not rendered and showed as raw tags.*

> We can also use **triple backtics** to render code blocks.
> Just wrap your code block with triple backtics and it's done.<br>
<br>`` ``` ``<br>def __init__():<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;print(a+b)<br>`` ``` ``


And the result would be:
```
def init(a,b):
    print(a+b)
```

\
\.

## 10. Tables
> To create Tables: <br><br> Header 1  | Header 2 <br> ----------------- | --------------- <br> Content 1 | Content 3<br>Content 2 | Content 4

Results are:
Header 1  | Header 2
--------- | ---------
Content 1 | Content 3
Content 2 | Content 4

\
\.

## 11. Horizontal Rules

> `***` | `---` creates Horizontal Rules as shown below:
***

\
\.

## 12. Links
MARKDOWN        |RESULTS         
----------------|-------------------
`[woogieboogie.dev](woogieboogie-jl.github.io)`|[woogieboogie.dev](https://woogieboogie-jl.github.io)

\
\.

## 13. Images
> Assuming a wanted image file is in path(relative) "/images/Seoul.jpg", format below will render the image:<br>
>> **`![Seoul, the cyberpunk village](/images/Seoul.jpg)`**

![Seoul, the cyberpunk village](/images/Seoul.jpg)

>To add a link to an image, enclose the Markdown for the image in brackets, and then add the link in parentheses.
>> **`[![woogieboogie's blog!](/images/logo.png)](https://woogieboogie-jl.github.io)`**

[![woogieboogie's blog!](/images/logo.png)](https://woogieboogie-jl.github.io)

\
\.

## 14. Escaping Characters
>If you want to denote certain phrase / word and the whole phrase includes one or more bactticks, 
>Try to enclose the phrase with double backticks (``)

MARKDOWN        |RESULTS         
----------------|-------------------
``Use `code` in your Markdown file``<span>``</span> |``Use `code` in your markdown file``

\
\.

## 15. HTML
 
> You can use HTML tags in many Markdown apps (including Hugo's Goldmark). There are situations where using HTML tags is much more productive then to continue on endless markdown formatting. Changing image sizes, Nested contents in ables, and etc.. there will be much more options if you can mix them wisely. <br>
><br>
> **You can just place the tags in the text of your Markdown-formatted file to use HTML tags:**
>>`This **word** is bold. This <em>word</em> is italic.`

#### Results:
>This word is bold. This *word* is italic.

\
\.

