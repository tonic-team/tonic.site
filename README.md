# Tonic Site

[![Netlify Status](https://api.netlify.com/api/v1/badges/19f789eb-dc29-44bf-bd8f-c676f7eeeb27/deploy-status)](https://app.netlify.com/sites/gin-tonic/deploys)
[![Mega-Linter](https://github.com/tonic-team/tonic.site/workflows/Mega-Linter/badge.svg?branch=main)](https://github.com/tonic-team/tonic.site/actions?query=workflow%3AMega-Linter+branch%3Amain)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

This repository is the source of the [Tonic site]
which presents and documents the Tonic template project.
It is built using [blogdown] and [Hugo].

## Development

You can fork this repo and contribute changes via PR.
For smaller content changes you can use the edit page button on the respective page.
But for bigger changes or new pages you should setup the repo for local development:

### Prequisites

- [Install R][r] and [RStudio] (optional)
- In R, install the [blogdown package][blogdown]: `install.packages("blogdown")`
- [Install Hugo][hugo], or try `blogdown::install_hugo()` in R

### Local setup

- Fork this repo and clone your fork
- Start R in the cloned repo
- We use [prettier] and [markdownlint] to enforce a consistent and readable coding style.
  If you're using [Visual Studio Code][vscode] for coding, you can install integration extensions for both tools,
  but there are also integrations for more editors.
- Please setup [pre-commit] and run `pre-commit install` in your repo
  to format and lint your staged files before committing them.
- Create a local branch before you commit changes.
- Run the development server in R: `blogdown::serve_site()`.
  If you add or edit files, the local dev server will reload in the browser.
- Edit and view the results locally.
- Commit your changes, push the branch to your fork, and create a PR.
- If some CI checks fail, try to fix the detected issues until CI is happy and the PR can be merged.

### Edit content

Page files are written in markdown or R markdown and organized in the content folder.
The folder names represent the URL segments, and the menu is built from the folder structure.

- Section pages are located at `content/<section-name>/_index.md`.
  The underscore is important, and the metadata block should contain `chapter: true`.
  Note that the text will be centered when `chapter:` is set to `true`.
- Child pages are located at `content/<section-name>/<page-name>/index.md`

Consult the [theme documentation] for more information about content editing.

### R Markdown

Maybe you want to write in R Markdown, because its Markdown dialect brought via Pandoc and bookdown is much richer
than that provided by Hugo, and designed with academic writing in mind.
See [Pandoc's Markdown] and the [Markdown extensions by bookdown] for an overview of the markdown features..
In addition, you can include code chunks generating different kinds of output (text, tables, figures).
See the [section about format differences][format differences] in the blogdown documentation.

To use R markdown, the file extension must be .Rmarkdown or .Rmd instead of .md.
The running dev server knits R markdown files, and the output files must also be committed.
You can choose between two options via file extension.

1. .Rmarkdown files are knitted to .markdown files,
   those are rendered to HTML by Hugo like the .md files in the content folder.
   This option is recommended, because you get most R Markdown features as well as consistent HTML across the complete site.
2. .Rmd files are directly knitted to HTML, so Hugo's rendering is skipped.

## License

The content is licensed under the [CC BY-SA 4.0 license].

[tonic site]: https://gin-tonic.netlify.app
[blogdown]: https://github.com/rstudio/blogdown
[hugo]: https://gohugo.io/
[r]: https://cran.r-project.org
[rstudio]: https://www.rstudio.com/products/rstudio/download/#download
[theme documentation]: https://themes.gohugo.io//theme/hugo-theme-learn/en
[pre-commit]: https://pre-commit.com
[prettier]: http://prettier.io
[markdownlint]: https://github.com/DavidAnson/markdownlint
[vscode]: https://code.visualstudio.com
[pandoc's markdown]: https://pandoc.org/MANUAL.html#pandocs-markdown
[markdown extensions by bookdown]: https://bookdown.org/yihui/bookdown/markdown-extensions-by-bookdown.html
[format differences]: https://bookdown.org/yihui/blogdown/output-format.html
[cc by-sa 4.0 license]: https://creativecommons.org/licenses/by-sa/4.0/
