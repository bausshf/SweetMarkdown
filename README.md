# What is Sweet markdown?
Sweet markdown is a markdown language fit for creating e-books by generating dynamic book pages in html, that are exportable as pdf.

It provides a simple markdown syntax that allows for dynamic tweaking of content the way you'd like.

It support things such as markdown comments, code-blocks, styling of blocks, all content, metadata-settings and language specifications for code-blocks etc.

A simple example would be:
## settings.smd
```
/**
A simple settings file.
**/
(pagenumbers: true)
(fontsize: 14)

// Imports d.smd 
&d.smd
```

## d.smd
```
/**
A D language implementation for code-blocks.
**/
(code-block keywords: D|#0000ff|public,private,protected,final,byte,short,int,long,ubyte ...)
(code-block color: D|"|"|#ff0000)
(code-block color: D|'|'|#ff0000)
(code-block color: D|//|\n|#00ff00)
(code-block color: D|/*|*/|#00ff00)
(code-block color: D|/+|+/|#00ff00)
```

## mybook.smd
```
// Imports settings.smd
&settings.smd

#My title

*Welcome* to my example /e-book/.

[font-size: 10|color: #0000ff]Find the source at: {https://github.com/bausshf/SweetMarkdown}[]

// Forces a page break so the code example goes on a new page.
<>

## Hello World in D

'''D
import std.stdio;

// Hello World Example
void main() {
    writeln("Hello World!");
}
'''
```

# Syntax-reference

## #title
Represents a title.

Example:
```
#My title
```
Output:
```
<h1>My title</h1>
```

## *boldtext*
Represents bold text.

Example:
```
*My bold text*
```
Output:
```
<b>My bold text</b>
```

## /italictext/
Represents italic text.

Example:
```
/My italic text/
```
Output:
```
<i>My italic text</i>
```


## ---
Represents a line-break (hr-tag)

Example:
```
---
```

Output:
```
<hr>
```

## {url} or {name:url}
Represents a link.

Example:
```
{https://github.com/bausshf/SweetMarkdown}
{sweet-markdown:https://github.com/bausshf/SweetMarkdown}
```
Output:
```
<a href="https://github.com/bausshf/SweetMarkdown">https://github.com/bausshf/SweetMarkdown</a>
<a href="https://github.com/bausshf/SweetMarkdown">sweet-markdown</a>
```


## <>
Represents a page-break.

Example:
```
<>
```
Output:
```
<p style="page-break-after:always;"></p>
```

## [styles]
Represents styling.

Example:
```
[font-size: 12|color: blue]
```
Output:
```
<span style="font-size: 12px; color: blue;">
```

## []
Represents the ending of styling.

Example:
```
[]
```
Output:
```
</span>
```


## '''language
Represents a code-block.

Example:
```
'''D
import std.stdio;

// Hello World Example
void main() {
    writeln("Hello World!");
}
'''
```

Output: (Excluded syntax-highlit styling)
```
<div class="smd-code-block">
<pre><code>
import std.stdio;

// Hello World Example;
void main() {
    writeln("Hello World!");
}
</code></pre>
</div>
```

## &resource
Represents a resource.

There are 4 types of resources.

* .js
  * Will be included as script tag.
* .html/.htm/.xhtml
  * Will be mixed in as html when mixed in using mixin statements.
* .smd
  * Will include settings from the specified sweet-markdown file.
  * Content can be mixed in using a mixin statement.
* .css
  * Will include a stylesheet
  * Pagenumbers can include stylesheets with =pn:stylesheet.css=
  
Example:
```
&settings.smd
```

## =resource=
Represents a resource mixin, which will mixin the content of the specified resource.

Example:
```
=copyrightstatement.smd=
```

Note: There is a special resource that can be used: =pn= which will insert page number. (Only if pagenumbers are defined)

To style the pagenumber use =pn:stylingresource.css=

## (setting:value)
Represents a metadata setting.

Example:
```
(pagenumbers: true)
```

Settings:
* pagenumbers (true/false)
  * Defines a boolean value whether page numbers should be displayed or not.
* code-block type (value)
  * Code-block settings are advanced. There will be more details on them later.
* fontsize (value)  
  * Will set a specific font-size for the page. (Default is pixels, supports specifications such as em ex. 14em)
  
## **
Represents a singleline comment.

Comments are not included in the final document.

Example:
```
** This is my comment.
```
Output:
```

```

## /** **/
Represents a multiline comment.

Multiline comments are not included in the final document.

Example:
```
/**
This is my multiline comment.
**/
```
Output:
```

```

## !html html!
Represents a html block.

Example:
```
!html
<p>This is a html paragraph.</p>
html!
```
Output:
```
<p>This is a html paragraph.</p>
```

## :imagesrc:
Represents an image.

Example:
```
:myimage.png:
```
Output:
```
<img src="myimage.png" alt="">
```

## \s
Represents a space either before or after a line.

Example:
```
\sThis text is indent by one space.
```
Output:
```
&nbsp;
```

## \t
Represents a tab (Default is 4 spaces, but can be controlled with the 'tab-count' setting.) either before or after a line.

Example:
```
\tThis text is indent by one tab.
```
Output:
```
&nbsp;&nbsp;&nbsp;&nbsp;
```

## -*
Represents a dotted list.

Each * represents the indentation of the item

Example:
```
-* This is the first item.
-** This is a child to the first item
-* This is the second item
```
Output:
```
<ul>
  <li>This is the first item.
    <ul>
      <li>This is a child to the first item</li>
    </ul>
  </li>
  <li>This is the second item.</li>
</ul>
```

## -#
Represents a numeric list.

Each # represents the indentation of the item.

Example:
```
-# This will have number 1
-## This is an inner child, but will also have number 1
-# This will have number 2
```
Output:
```
<ol>
  <li>This will have number 1
    <ol>
      <li>This is an inner child, but will also have number 1</li>
    </ol>
  </li>
  <li>This will have number 2</li<
</ol>
```

## |column|column|...|
Represents a table.

Example:
```
|Header-column-1|Header-column-2|
|Row-1-column-1|Row-1-column-2|
|Row-2-column-1|Row-2-column-2|
```
Output:
```
<table>
  <tr>
    <th>Header-column</h>
    <th>header-column-2</th>
  </tr>
  <tr>
    <td>Row-1-column-1</td>
    <td>Row-1-column-2</td>
  </tr>
  <tr>
    <td>Row-2-column-1</td>
    <td>Row-2-column-2</td>
  </tr>
</table>
```
