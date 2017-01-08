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
