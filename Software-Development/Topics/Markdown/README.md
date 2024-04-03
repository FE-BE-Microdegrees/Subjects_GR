# Markdown

- [Markdown](#markdown)
  - [Learning Outcomes](#learning-outcomes)
  - [What is Markdown?](#what-is-markdown)
  - [What is a Markup Language?](what-is-a-markup-language?)
  - [Advantages of Markdown:](#advantages-of-markdown)
  - [Disadvantages of Markdown:](#disadvantages-of-markdown)
  - [When to Use Markdown:](#when-to-use-markdown)
  - [Basic Markdown Syntax:](#basic-markdown-syntax)
    - [Headings:](#headings)
    - [Emphasis:](#emphasis)
    - [Lists:](#lists)
      - [Unordered:](#unordered)
      - [Ordered:](#ordered)
    - [Links:](#links)
    - [Images:](#images)
    - [Blockquotes:](#blockquotes)
    - [Inline Code:](#inline-code)
    - [Code Blocks:](#code-blocks)
    - [Horizontal Rule:](#horizontal-rule)
    - [Tables:](#tables)
    - [Task Lists:](#task-lists)
  - [Excercises](#excercises)

## Learning Outcomes

After completing this topic, you'll be able to:

- describe what Markdown is and why it's useful;
- identify the pros and cons of Markdown;
- use Markdown to format text;
- use Markdown for documentation, blogging, and other purposes.
- use Markdown in Github.

## What is Markdown?

Markdown is a lightweight markup language with a simple text formatting syntax. It was created by John Gruber in 2004. The main goal of Markdown was to make it easy for people to write and format text in a way that is freely readable and can be converted to HTML (or other output formats).

## What is a Markup Language?

A markup language is a language used for formatting or structuring text by adding markers or tags. Markers are usually some symbols or combinations of symbols added to the text to define what formatting or structure some text should have. Markup languages are widely used in documentation, web page creation, blogging, and many other contexts.

Common markup languages include:

- HTML
- XML
- LaTeX
- Markdown
- etc.

## Advantages of Markdown:

- **Simplicity:** Markdown is easy to learn and use. Its syntax is intuitive, meaning that even non-technical people can easily start writing in this format.
- **Readability:** Markdown documents consist of plain text, therefore they are readable even without converting to another format.
- **Portability:** Since these are plain text files, Markdown documents are OS-agnostic and can be opened with any text editor.
- **Flexible Output:** Markdown can be converted to a variety of formats, including HTML, PDF, and even MS Word or LaTeX format.
- **Widespread Use:** Many platforms, such as GitHub, Reddit, Stack Exchange, and even messaging applications like Slack and Discord, support Markdown. It is also a popular choice for documentation and blogging.
- **Version Control Friendly:** Being plain text, Markdown works seamlessly with version control systems like Git.
- **No Need for Specialized Software:** Markdown can be written in any text editor. Additionally, there are specialized Markdown editors that offer additional features, such as preview and quick conversion.


## Disadvantages of Markdown:

- **Limited Styling:** While Markdown easily handles basic formatting, it is not suitable for composing documents that require complex styles or layouts.
- **Inconsistencies:** There are several variations of Markdown, and not all tools support every feature. For example, GitHub's Markdown processing may be slightly different from other platforms.
- **Not Ideal for Large Documents:** While Markdown can certainly be used for larger documents, it might not be as manageable or structured as other formats created for this purpose.
- **No Built-in Preview:** Without using a specialized Markdown editor, it is not possible to preview the formatted output without converting it. However, it's possible to install plugins to some editors that enable preview, like VS Code with the Markdown All in One plugin.

## When to Use Markdown

- **Documentation:** Many open-source projects use Markdown for their README files and documentation, as it is simple and GitHub supports it by default.
- **Blogging:** Many blog platforms and static site generators support Markdown, as it is readable and user-friendly.
- **Note-taking:** Markdown is great for taking structured notes. There are several note-taking applications that support Markdown formatting.
- **Online Discussions:** Platforms like Reddit and Stack Exchange use Markdown for formatting text in comments and posts.
- **Writing Books:** Some authors use Markdown for writing books, especially technical books, as it is simple and allows for conversion into various formats.
- **Presentations:** Tools like Reveal.js or Marp allow creating presentations using Markdown.
- **Educational Materials:** Markdown is suitable for creating educational materials, such as tutorials, cheat sheets, and more. This format is easy to write and read, and it can be converted into various formats. If something changes in the source material, you only need to update the Markdown file and regenerate the output.

In summary, Markdown is an excellent choice for projects that require basic formatting without the additional overhead of more complex markup languages. Its simplicity and readability are the main strengths of Markdown, but for more complex layouts or extensive styling, other formats might be more appropriate.

## Basic Markdown Syntax:

Here's a quick reference to basic Markdown syntax:

### Headings:

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

### Emphasis:

```markdown
*italic* or _italic_
**bold** or __bold__
**_italic and bold_** or *__italic and bold__*
~~strikethrough~~
```

### Lists:

#### Unordered:

```markdown
* Item 1
* Item 2
  * Subitem 2.1
  * Subitem 2.2
```

or 

```markdown
- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2
```

#### Ordered:

```markdown
1. First item
2. Second item
   1. Subitem 2.1
   2. Subitem 2.2
```

### Links:

```markdown
[Google](https://www.google.com)
```

### Images:

```markdown
![Alt text](url_to_image)
```

### Blockquotes:

```markdown
> This is a blockquote.
```

### Inline Code:

```markdown
Here is `inline code`.
```

### Code Blocks:

Using three backticks:

<pre>
```
function example() {
  console.log("example");
}
```
</pre>

Or with syntax highlighting:

<pre>
```javascript
function example() {
  console.log("example");
}
```
</pre>

### Horizontal Rule:

```markdown
---
```

or 

```markdown
***
```

### Tables:

```markdown
| Header 1 | Header 2 |
| -------- | -------- |
| Cell1    | Cell2    |
| Cell3    | Cell4    |
```

### Task Lists:

```markdown
- [x] Task 1 (completed)
- [ ] Task 2 (not completed)
```

Remember, different platforms or flavors of Markdown might have additional features or slight variations, but the above covers the basic and commonly-used syntax.

Read more from [Markdown Guide](https://www.markdownguide.org/).

## Excercises

- Create `README.md` file into your repository and write a short introduction about yourself using Markdown syntax.
- Make sure to use at least 3 different Markdown syntaxes (e.g. headings, lists, links, images, etc.).
- Commit and push your changes to your repository.
- Check your repository on GitHub and make sure that your `README.md` file is rendered properly.
