# Creating Project Documentation with `mkdocs`

With the [MkDocs](https://www.mkdocs.org) package, you can easily add markdown-based documentation to your Python project. Just add the `mkdocs` package to your environment using your preferred package manager (e.g. with the `add` command if you're using `uv`).

Then, run:

- `mkdocs new .`

This command creates a `docs` folder and a `mkdocs.yml` file in your existing project root directory.

If you want to create a new project from scratch, you can instead run:

- `mkdocs new <project-name>`

This will create a new project folder and, inside that folder, add the new `docs` directory and the `mkdocs.yml` file.

---

### The `docs` Folder

This is where the markdown files documenting your project are going to be stored. MkDocs initializes this folder with an `index.md` file that contains some example content.

---

### The `mkdocs.yml` File

The `mkdocs.yml` file contains structural and layout-related configuration for your documentation site. Initially, it’s very minimal — usually just containing the site’s name.

To customize the look and structure of your documentation, you can extend this file. For example, if you want to change the theme and you have four markdown files (`index.md`, `usage.md`, `api.md`, and `faq.md`) in the `docs` folder, your `mkdocs.yml` could look like this:

```yaml
site_name: My Project
theme:
  name: mkdocs

nav:
  - Home: index.md
  - Usage: usage.md
  - API Reference: api.md
  - FAQ: faq.md
```

These entries define the site navigation. Titles like "Home" and "Usage" will appear in the preview header of your documentation site.

### Using Other Themes

Besides the default mkdocs theme, you can use other themes such as:

- readthedocs

- material (from the mkdocs-material package)

To use the Material theme, install the mkdocs-material package (e.g. with `uv add mkdocs-material`). You can find more about it [here](https://albrittonanalytics.com/getting-started/).


### Syntax Highlighting and Extensions

To enable syntax highlighting for Python code and customize the appearance of images or other elements, you can add extensions to the markdown_extensions section in your mkdocs.yml file.

Here's an example configuration:

```
markdown_extensions:
  - attr_list
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```

- `attr_list` allows HTML-style attribute lists (e.g., for styling images),
- `pymdownx.*` extensions enhance code highlighting and markdown features.