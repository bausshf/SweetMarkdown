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

## *boldtext*
Represents bold text.

Example:
```
*My bold text*
```

## /italictext/
Represents italic text.

Example:
```
/My italic text/
```

## ---
Represents a line-break (hr-tag)

Example:
```
---
```

## {url}
Represents a link.

Example:
```
{https://github.com/bausshf/SweetMarkdown}
```

## <>
Represents a page-break.

Example:
```
<>
```

## [styles]
Represents styling.

Example:
```
[font-size: 12|color: blue]
```

## []
Represents the ending of styling.

Example:
```
[]
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

## /** **/
Represents a multiline comment.

Multiline comments are not included in the final document.

Example:
```
/**
This is my multiline comment.
**/
```

## !html html!
Represents a html block.

Example:
```
!html
<p>This is a html paragraph.</p>
html!
```

## :imagesrc:
Represents an image.

Example:
```
:myimage.png:
```
