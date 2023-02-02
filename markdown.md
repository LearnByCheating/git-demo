# Markdown Examples

## Table of Contents

Basic Markdown Syntax:  
[Headings h1 - h6](#headings)  
[Line breaks, Paragraphs and Blockquotes](#line-breaks-paragraphs-and-blockquotes)  
[Italic and Bold](#italic-and-bold)  
[Code and Code blocks](#code-and-code-blocks)  
[Links](#links)  
[Images](#images)  
GitHub Flavored Markdown:  
[Task List](#task-list)  
[Table](#table)  

---

## BASIC MARKDOWN SYNTAX
---

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

---

## Line breaks, Paragraphs and Blockquotes

This is line 1. It ends with two spaces.  
Line 2 ends with an HTML break tag.<br>
This is line 3.
This is also line 3.

This is paragraph 1.

This is paragraph 2.

> This is a blockquote.

---

## Italic and Bold

This is *italic*. So is _this_.  
This is **bold**. So is __this__.  
This is both ***bold and italic***.  

---

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

---

## Lists

### Unordered list

- First Item.
- Second Item.
- Third Item.
  - Intented item.
  - Second indented item.

### Ordered list

1. Item 1
1. Item 2
1. Item 3
    1. Indented item 1.
    1. Indented item 2.

---

## Links

This is a link to [example.com](https://example.com)

GitHub automatically creates a link from a URL: https://example.com  

---

## Images

- Image alt text is displayed if the image doesn't load.
- Title is optional. It displays when hovering over an image.
- You can not set height or width with Markdown, so use the HTML img tag if you need to set those.

![Git icon](/images/git-icon.svg "Git") 
<img src="images/github-mark.png" alt="GitHub icon" width="100" height="100" title="GitHub">
<br><br>

---
## GITHUB FLAVORED MARKDOWN
---

## Supports basic HTML tags and inline style attributes
This text is <span style="color: red">red</span>.

---

## Strikethrough
Remove this line: ~~Unwanted text here.~~

---

## Task List

- [ ] unchecked item
- [x] checked item

---

## Table

First Header | Second Header | Third Header
------------ | ------------- | ------------
Cell 1 content | Cell 2 content | Cell 3 content
Cell 1 content | Cell 2 content | Cell 3 content
