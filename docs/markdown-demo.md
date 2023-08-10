# Markdown Examples

## Table of Contents

__Basic Markdown Syntax:__  
[Headings h1 - h6](#headings)  
[Line breaks, Paragraphs and Blockquotes](#line-breaks-paragraphs-and-blockquotes)  
[Italic and Bold](#italic-and-bold)  
[Code and Code blocks](#code-and-code-blocks)  
[Links](#links)  
[Images](#images)  

__GitHub Flavored Markdown:__   
[HTML and inline style](#html-and-inline-style)  
[Strikethrough](#strikethrough)  
[Task Lists](#task-list)  
[Tables](#table)  
_________________________________________

## BASIC MARKDOWN SYNTAX

## Headings

\# h1  
\## h2  
\### h3  
\#### h4  
\##### h5  
\###### h6  

### Altnernate Syntax for h1 and h2:

h1  
\=  

h2  
\-
_________________________________________

## Line breaks, Paragraphs and Blockquotes

This is line 1. It ends with two spaces.  
Line 2 ends with an HTML break tag.<br>
This is line 3.
This is also line 3.

This is paragraph 1.

This is paragraph 2.

> This is a blockquote.
_________________________________________

## Italic and Bold

This is *italic*. So is _this_.  
This is **bold**. So is __this__.  
This is both ***bold and italic***. So is ___this___.  
_________________________________________

## Code and Code Blocks

This is `monospaced computer code`.

Below is a block of code:

    function double(num) { 
      return num * 2; 
    }; 
    double(2);

### GitHub Flavored Markdown Code Blocks:
- Can be fenced with 3 backtics or tildes.  
- And can do language syntax highlighting.

``` javascript
function triple(num) { 
  return num * 3; 
}; 
double(2);
```
_________________________________________

## Lists

### Unordered list

- First Item.
- Second Item.
- Third Item.
  - Intented item.
  - Second indented item.

### Ordered list

1. Item 1
2. Item 2
3. Item 3
    1. Indented item 1.
    2. Indented item 2.

Text  

4. Item 4
_________________________________________

## Links

This is a link to [example.com](https://example.com)

Or you can use regular html <a href="https://example.com">example.com</a>

GitHub automatically creates a link from a URL: https://example.com  
_________________________________________

## Images

- Image alt text is displayed if the image doesn't load.
- Title is optional. It displays when hovering over an image.
- You can not set height or width with Markdown, so use the HTML img tag if you need to set those.

![Git icon](../images/git-icon.svg "Git") 
<img src="../images/github-mark.png" alt="GitHub icon" width="100" height="100" title="GitHub">
<br><br>
_________________________________________

## GITHUB FLAVORED MARKDOWN

## HTML and inline style
GitHub supports the use of basic HTML tags and inline style attributes.

This text is <span style="color: red">red</span>.
_________________________________________

## Strikethrough
Remove this line: ~~Unwanted text here.~~
_________________________________________

## Task List

- [ ] unchecked item
- [x] checked item

Note, task lists are supported on GitHub but not by VS Code's Markdown converter.
_________________________________________

## Table

First Header | Second Header | Third Header
------------ | ------------- | ------------
Cell 1 content | Cell 2 content | Cell 3 content
Cell 1 content | Cell 2 content | Cell 3 content