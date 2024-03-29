# *

https://en.wikipedia.org/wiki/Markup_language

## xml

The XML declaration show be the top line. [ref](https://stackoverflow.com/questions/19889132/error-the-processing-instruction-target-matching-xxmmll-is-not-allowed)

What does `<![CDATA[]]>` mean? [CDATA stands for Character Data](https://stackoverflow.com/a/2784200/11844003), and it means that the data in between these strings includes data that _could_ be interpreted as XML markup, but should not be.

## tex

[latex & markdown mix?](https://stackoverflow.com/questions/2188884/how-can-i-mix-latex-in-with-markdown)

[intellij texify plugin installation instructions](https://github.com/Hannah-Sten/TeXiFy-IDEA#installation-instructions)

[write mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics)

## markdown

- [backtick in markdown](https://meta.stackexchange.com/questions/82718/how-do-i-escape-a-backtick-within-in-line-code-in-markdown) with 3 ways:

  ```txt
  ``foo` ``
  `` `foo``
  `` ` ``
  ```

- [`U+262E` -> `&#9774;`](https://stackoverflow.com/questions/34538879/unicode-in-github-markdown/36616878). Check also another answer by llyich: "use either decimal or hex code point or HTML entity name (if exists) of a unicode character"

- Markdown is used primarily to generate HTML, and HTML collapses white spaces by default. Use _\&nbsp;_ instead of space characters.[check the top answer](https://stackoverflow.com/questions/15721373/how-do-i-ensure-that-whitespace-is-preserved-in-markdown)

- [link to header rules](https://stackoverflow.com/a/51226139/11844003):
  1. All text is converted to lowercase
  2. All non-word text (e.g., punctuation, HTML) is removed.
  3. All spaces are converted to hyphens.
  4. Two or more hyphens in a row are converted to one.
  5. If a header with the same ID has already been generated, a unique incrementing number is appended, starting at 1.

- draw checkbox in table? [you can use html entity `&check;` \(\&check\); and `&cross;` \(\&cross;\)](https://stackoverflow.com/a/60687493/11844003)

- highlight shell commands? [credits](https://stackoverflow.com/a/52586193)
  - Shell: console, shell
  - Bash: bash, sh, zsh
  - PowerShell: powershell, ps
  - DOS: dos, bat, cmd

An option to highlight a "Note" and "Warning" using blockquote? [GitHub Only](https://github.com/community/community/discussions/16925)

```markdown
> **Note**
> This is a note

> **Warning**
> This is a warning
```
