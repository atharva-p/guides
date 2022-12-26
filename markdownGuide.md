# Markdown Guide

## Headings and paragraphs

To create headings, use hashes before the word. The number of hashes determine the size of the heading

```
# heading 1
### heading 3
```

Put a blank line before and after the heading of the document

Put a blank line before and after to separate paragraphs as well.

Do not indent paragraphs

---

## Bold

to make bold, use **double asterisks** (without any space between the asterisks and the word)
`**this will be bold** `

## Italics

to make any text italics, use _single asterisks_

## Bold and italics together

to do this, use **_three asterisks_**

## Subscript and superscript

Use the `<sub> </sub>` and the `<sup></sup>` tags. This is only for github markdown and others that support it.

---

## Escaping Characters

To display a literal character that would otherwise be used to format text in a Markdown document, add a backslash (`\`) in front of the character.

```
\* Without the backslash, this would become an underordered list
```

---

## Blockquotes

to add a blockquote use right arrows

> This is a blockquote

`> This is a blockquote`

> This is a nested blockquote
>
> > Nested Blockquote

## Lists

Ordered lists (use numbers)

1. first
2. second
   Unordered lists (use dashes)

- underordered element
- another underordered element

## Code blocks

To create a codeblock, use triple backticks

```
<html>
<link rel = "stylesheet" href="./index.css">
</html>
```

#### Inline code

An inline code may be created by enclosing the line in `double backticks or single backticks`

##### Using backticks inside inline code

Backticks are allowed in code blocks but may exhibit improper behavior in inline code.

For more information, [click here](https://stackoverflow.com/a/71150969/16465011)

## Horizontal rules

Use three dashes or three asterisks to create horizontal rules.
Put blank lines before and after horizontal rules

---

## Links

To create a link, enclose the link text in brackets and then the href or URL should be in parenthesis.
To go to google, [click here](https://google.com).

```
To go to google, [click here](https://google.com).
```

### Relative links

These are links relative to the project directory and should be prefered over absolute links to link to files within your project directory.

For example, `[click here](../assets/photos/filename.png)` is a relative link. Use the following reference

```
/   = Root directory
.   = This location
..  = Up a directory
./  = Current directory
../ = Parent of current directory
../../ = Two directories backwards
```

### Reference style links

> NOTE: Some markdown editors/viewers may not have support for this type, although it is supported in github markdowns

This is a [reference-style-link] [1]
[1]: https://google.com

```
This is a [reference-style-link] [someID]
[someID]: https://google.com
```

### Links best practices

Markdown applications don’t agree on how to handle spaces in the middle of a URL. For compatibility, try to URL encode any spaces with `%20`

```
[link](https://www.example.com/my%20great%20page)
```

---

## Images

You can display an image by adding ! and wrapping the alt text in `[ ]`. Then wrap the link for the image in parentheses `()`

```
![This is an image](https://myoctocat.com/assets/images/base-octocat.svg)
```

---

## Footnotes

Additional notes can be added to statements but in a way that does not clutter the body of the document. These notes are usually shown at the end of the document. To create a footnote, use `[^1]` syntax

```
Here is a simple footnote[^1].

A footnote can also have multiple lines[^2].

You can also use words, to fit your writing style more closely[^note].

[^1]: My reference.
[^2]: Every new line should be prefixed with 2 spaces.
  This allows you to have a footnote with multiple lines.
[^note]:
    Named footnotes will still render with numbers instead of the text but allow easier identification and linking.
    This footnote also has been made with a different syntax using 4 spaces for new lines.
```

---
