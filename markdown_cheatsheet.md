# Markdown Cheatsheet

### Headings

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

### Emphasis

```markdown
*Italic* or _Italic_
**Bold** or __Bold__
***Bold and Italic***
~~Strikethrough~~
```

### Lists

Indent two spaces for sublist

#### Unordered

```markdown
- Item 1
- Item 2
  - Subitem 1
  - Subitem 2
```

Or

```markdown
* Item 1
* Item 2
  * Subitem 1
  * Subitem 2
```

#### Ordered

```markdown
1. First
2. Second
3. Third
```

### Links

```markdown
[some text](https://www.your-website.com)
```

### Images

```markdown
![Alt Text](https://example.com/image.jpg)
```

## Linking to Headings (anchors)

You can create links to headings within the same Markdown document using anchor links.

```markdown
[Link Text](#heading-text)
```

Where `#heading-text` is the slugified version of the heading.

### Slugification Rules (as commonly used by GitHub and others)

| Rule                                                  | Example                                   |
| ----------------------------------------------------- | ----------------------------------------- |
| Lowercase everything                                  | `## My Heading` → `#my-heading`           |
| Remove punctuation                                    | `## Hello, World!` → `#hello-world`       |
| Replace spaces with dashes                            | `## Getting Started` → `#getting-started` |
| Collapse multiple spaces to one dash                  | `## A  B` → `#a-b`                        |
| Remove special characters (each space becomes a dash) | `## C# & .NET` → `#c--net`                |

### Code

#### Inline Code

```markdown
Here is some `inline code`.
```

#### Code Block

<pre>
```python
def hello():
    print("Hello, world!")
```
</pre>

### Common Language Identifiers

| Language     | Identifier         | Language | Identifier     |
| ------------ | ------------------ | -------- | -------------- |
| Bash / Shell | `bash`, `sh`       | C        | `c`            |
| Python       | `python`           | C++      | `cpp`          |
| JavaScript   | `javascript`, `js` | C#       | `csharp`, `cs` |
| TypeScript   | `typescript`, `ts` | PHP      | `php`          |
| HTML         | `html`             | Ruby     | `ruby`         |
| CSS          | `css`              | Go       | `go`           |
| JSON         | `json`             | Rust     | `rust`         |
| YAML         | `yaml`, `yml`      | SQL      | `sql`          |
| Markdown     | `markdown`         | Swift    | `swift`        |
| Java         | `java`             |          |                |

### Blockquotes

```markdown
> This is a block quote.
```

### Horizontal Rule

```markdown
---
```

### Tables

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

### Task Lists

```markdown
- [x] Task 1
- [ ] Task 2
```

### Footnotes

```markdown
This is a sentence with a footnote.[^1]
[^1]: This is the footnote text.
```
