# Markdown Cheatsheet

## Headings

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

## Emphasis

```markdown
*Italic* or _Italic_
**Bold** or __Bold__
***Bold and Italic***
```

## Lists

### Unordered

```markdown
- Item 1
- Item 2
  - Subitem 1
  - Subitem 2
```

### Ordered

```markdown
1. First
2. Second
3. Third
```

## Links

```markdown
[OpenAI](https://www.openai.com)
```

## Images

```markdown
![Alt Text](https://example.com/image.jpg)
```

## Code

### Inline Code

```markdown
Here is some `inline code`.
```

### Code Block

<pre>
```python
def hello():
    print("Hello, world!")
```
</pre>

## Blockquotes

```markdown
> This is a quote.
```

## Horizontal Rule

```markdown
---
```

## Tables

Explanation:
    Each row of the table is written on a new line.
    Columns are separated by vertical bars (|).
    The second row defines how the column contents are aligned:
        --- = default (left-aligned)
        :--- = left-aligned
        :---: = center-aligned
        ---: = right-aligned

```markdown
| Syntax | Description |
|--------|-------------|
| Header | Title       |
| Cell   | Text        |
```

## Task Lists

```markdown
- [x] Task 1
- [ ] Task 2
```
