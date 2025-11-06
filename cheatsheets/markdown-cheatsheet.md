# Markdown Cheatsheet

## Best Practices
- Use `#` for headers, not `=` or `-`
- Use `**bold**` instead of `__bold__`
- Use `*italic*` instead of `_italic_`
- Use fenced code blocks with language specification
- Use tables for structured data
- Keep line length reasonable (80-100 characters)
- Use meaningful link text
- Include alt text for images

## Headers
```markdown
# H1 Header
## H2 Header
### H3 Header
```

## Text Formatting
```markdown
**Bold text**
*Italic text*
***Bold and italic***
~~Strikethrough~~
`Inline code`
```

## Blockquotes
```markdown
> This is a blockquote
> 
> Multiple lines
> 
> > Nested blockquote
> 
> Regular paragraph after blockquote
```

## Unordered Lists
```markdown
- Item 1
- Item 2
  - Nested item
  - Another nested item
- Item 3
```

## Ordered Lists
```markdown
1. First item
2. Second item
   1. Nested numbered
   2. Another nested
3. Third item
```

## Task Lists
```markdown
- [x] Completed
- [ ] Pending
```

## Links
```markdown
[Link text](https://example.com)
[Link with title](https://example.com "Title text")
[Reference link][ref]
[ref]: https://example.com "Reference title"
```
## Images
```markdown
![Alt text](image.jpg)
![Alt text](image.jpg "Image title")
![Reference image][img-ref]
[img-ref]: image.jpg "Reference image title"
```

## Horizontal Rules
```markdown
---
***
___
```

## Line Breaks
```markdown
Line 1  
Line 2 (two spaces at end)

Line 1
Line 2 (empty line between)
```

## Escaping Characters
```markdown
\*Not italic\*
\# Not a header
\[Not a link\]
```

## Code Block
```markdown
    ```language
    // Code here
    function example() {
      return "Hello World";
    }
    ```
```

## Tables
```markdown
| Left | Center | Right |
|:-----|:------:|------:|
| L1   |   C1   |    R1 |
| L2   |   C2   |    R2 |
```

## Definition Lists
```markdown
Term 1
: Definition 1
: Definition 2

Term 2
: Definition 3
```

## Footnotes
```markdown
Text with footnote[^1]

[^1]: Footnote content
```

## Abbreviations
```markdown
*[HTML]: HyperText Markup Language
*[CSS]: Cascading Style Sheets
```

## Highlight
```markdown
I need to highlight these ==very important words==.
```

## Subscript/Superscript
```markdown
H~2~O
X^2^
```

## Emoji
:smile: :heart: :joy: :rocket: :+1: :-1:

(See also [Complete list of GitHub Markdown Emojis](https://gist.github.com/rxaviers/7360908))

## HTML (when needed)
```markdown
<details>
<summary>Click to expand</summary>

Hidden content here
</details>

<kbd>Ctrl</kbd> + <kbd>C</kbd>

<mark>Highlighted text</mark>
```