# Contributing to the Tonic site

Thank you for taking the time to contribute to the Tonic site.
Contributions are welcome and this document is intended to help them to find their way into the project.

## What can be contributed?

There are several ways to contribute:

- Ideas, suggestions, issue reports
- smaller fixes on existing pages
- Content: new pages or larger additions to existing pages

If you are missing something or have discovered incorrect informations,
you can use the project's [issue tracker] to briefly describe what you'd like to see on the site.
Fixes or content can be submitted via fork and pull request on Github.

## Content file structure

The content on this site is authored in Markdown, a lightweight markup language that is rendered to HTML.
Page files are written in markdown or R markdown and organized in the content folder.
The folder names represent the URL segments, and the menu is built from the folder structure.

- Chapter pages are located at `content/<chapter-name>/_index.md`.
  The underscore is important, and the metadata block should contain `chapter: true`.
  Note that the text will be centered when `chapter:` is set to `true`.
- Child pages are located either at `content/<chapter-name>/<page-name>/index.md` or at `content/<chapter-name>/<page-name>.md`.
  If the former variant is used (page bundles), static assets can put directly into the page directory.
  This can be very useful when assets exclusively belong to a given page.

- If you put a file named `figure5.png` next to a chapter page, that Markdown file can reference the image file with `![Figure 5](figure5.png)`.
- If more Markdown files are located next to the chapter page file without their own child directory,
  they have to reference the image with a `../` prefix, e.g. `![figure 5](../figure5.png)`,
  as if the Markdown files were located in their own subdirectories.
- If you put each Markdown file in its own subdirectory, the `../` makes sense,
  because the image is located one level up in relation to the Markdown file.
- If you put the image in a directory with a non-chapter Markdown file (a leaf bundle),
  the link becomes `![Figure 5](figure5.png)` again.

The `static` directory is an alternative place where you can put more global static assets.
It contains files that are directly made available according to their folder structure
The file `static/images/logo.svg` can e.g. referenced in Markdown or HTML files as `/images/logo.svg`.

Consult the [theme documentation] for more information about content editing.

## Minor improvements via browser

It is possible and absolutely fine to provide fixes and suggestions in a pure browser-based workflow.
If you hit the _edit this page_ button on a website page, you will be redirected to the respective edit page on Github,
where you can improve the Markdown source, create a commit and submit it as a pull request.
If you don't have write access to the repo and if you are a first-time contributor, you will be asked to create a fork before you can edit the page file.

In this project, we strive to maintain a clean and consistent code style.
the files in the PR are formatted by [prettier], a code formatting tool which understands many languages,
but you can use the [prettier playground] to preformat your markdown Before you commit and submit the PR:

1. Make your changes
2. Paste the full document into the input field of the playground (left side)
3. Replace document with Prettier's result from the output field (right side).
4. Commit and submit

Some quality checks will run on the PR before it is ready for review.
This takes a moment, and you will probably be informed per email if your PR introduces an issue.
You can fix the reported issues by adding more commits to the PR.
It's relatively unlikely to introduce an error in a small change, but not impossible.
The Markdown files are checked using [markdownlint], a tool which helps to discaver errors and inconsistencies in Markdown files..
You can use its browser-based [online demo][markdownlint-demo] to inspect the file you have edited and figure out what went wrong.

## Contributions via local setup

The browser-based workflow might be sufficient for smaller improvements, but for larger contributions,
especially if you want to add new pages or intend to contribute for multiple times,
the recommended way is cloning the forked project to your machine and preparing your changes locally in a suited text editor.
This makes it easier to write clean files and to preview the result in the local development server before any PR is submitted.

### Workflow overview

This actually applies to the browser-based workflow, except that some steps in the browser are shortened a bit.
And of course both can be combined, e.g., one can open a PR in the browser but finish it locally.

1. Setup
   - Make sure you have [git] installed
   - If you want to preview the site in a local development server, install [hugo].
   - If you want to edit R Markdown files, you'll also need [R] and the [blogdown] package.
   - If you don't have write access to the project repo, fork it.
   - Clone the repo you want to write to
   - Create a new local branch from the main branch, name it after your contribution
2. Uploading your Changes (iterative)
   - Make your improvements
   - Please try to write one sentence or clause per line, as far as it makes sense. This improves `git diff`(previews of differences) and file reviews.
   - Try to format your edited files with [Prettier] and lint Markdown with [markdownlint].
   - commit to the new branch.
   - Push the new branch to your remote
3. Requesting the improvements to be merged
   - On Github, create a pull request to merge the new branch into the main branch
   - If the title is not sufficient, you can provide a PR description.
   - Please leave the “allow edits” checkbox enabled
4. Checking, cleaning (iterative)
   - When a PR is created, Prettier runs on the PR branch.
     If it detects unformatted files, a commit that applies formatting changes is added to the branch.
     if you want to add more commits to the PR, you will have to pull these changes into your local branch.
   - After prettifying is done, the Markdown files are checked for issues that relate to ambiguity, accessibility, consistency, and alike by [markdownlint].
     If this check doesn't pass, you have to add commits to your branch which fix the detected issues.
   - The checks rerun and the cycle repeats, until the checks succeed.
5. Reviewing and improving content (iterative)
   - Now your PR is ready for review, and you can request review from one or more collaborators.
   - If a reviewer rejects your PR and provides feedback, you will have to discuss or integrate the feedback
     by adding fixup commits to your PR branch until it gets approved.
     This also triggers the checking and cleaning cycle.
   - Meanwhile, if the main branch receives new commits and your PR can't be merged anymore due to merge conflicts,
     please don't merge main into your branch, but rebase your branch on main and force-push your branch.
     This keeps the commit history linear.
     - Finally, a reviewer might approve your PR
6. Merge
   - The PR is clean, approved, and thus ready for merge.
   - A maintainer will merge it.

### Content editing and clean files

In fact, any text editor can be used to edit Markdown files,
but you should consider using a more powerful text editor which is suited for editing different kinds of code and prose.
The project wiki contains a [step-by-step guide for Visual Studio Code][vscode-guide],
but e.g. Sublime Text or Atom could be good choices as well.
These editors can directly integrate with [Prettier] and [Markdownlint],
and thus let you catch and fix many errors before they are commited.

If you want to use Prettier and Markdownlint on the command line, you can install [node] and use the project's npm scripts.

```bash
# cd to project root
cd tonic.site
# Install npm dependencies and husky pre-commit hooks
# The pre-commit hook formats and lints staged files
npm i
# Format project
npm run format
# Format and lint project
npm run lint
# Get rid of the git hook, if it prevents you from working productively
npx husky uninstall
```

### Live preview

Hugo comes with a local development server where you can preview the result of your changes live in your browser.
When a file is added or changed, it rebuilds the site and reloads in the browser.
If you want the live preview while your working, you have some options:

```bash
# Run hugo server on the command line
hugo server --watch --navigateToChanged --enableGitInfo
# If you work with node, use the shortcut npm script
npm run watch
```

### Using Blogdown

Maybe you are used to R and RStudio or simply want to write in R Markdown.
Then you can use R and the [blogdown] package for content editing and previewing.
If you're not using RStudio, you will need to install [pandoc].
The Markdown dialect brought via Pandoc and bookdown is much richer than that provided by Hugo, and designed with academic writing in mind.
See [Pandoc's Markdown] and the [Markdown extensions by bookdown] for an overview of the markdown features..
In addition, you can include code chunks generating different kinds of output (text, tables, figures).
See the [section about format differences][format differences] in the blogdown documentation.

To write in R markdown, the file extension must be .Rmarkdown (preferred) or .Rmd instead of .md.
R Markdown files must be knitted and the resulting output files must be committed to take effect.
You can use the preview server via [blogdown] package to knit them automatically.

```r
# Install blogdown package in R (if not already done) and restart R in the project root
install.packages("blogdown")
# Run the development server or use the RStudio addin “Serve Site”
blogdown::serve_site()
# Quit R or stop the server when you're done
blogdown::server_stop()
```

[blogdown]: https://github.com/rstudio/blogdown
[git]: https://git-scm.com
[hugo]: https://gohugo.io/
[issue tracker]: https://github.com/tonic-team/tonic.site/issues
[markdownlint]: https://github.com/DavidAnson/markdownlint
[markdownlint-demo]: https://dlaa.me/markdownlint/
[node]: https://nodejs.org
[pandoc's markdown]: https://pandoc.org/MANUAL.html#pandocs-markdown
[prettier]: https://prettier.io
[prettier playground]: https://prettier.io/playground/#N4Igxg9gdgLgprEAuEAJOBDAJnATgHSgF4TTDCB9AGQggGsAaCgAkh2YCMAbCMOgZ2YZccZgDMIuALYYY8LMwBUMWgEJF5KAAMdzAFb9CYgK5QwMAJbRmFnLAswAngAoAHgEpmwZiJjHcUMyuzAC+hDpamgAKFjwwAD4Agha4AA6SCagQ-oZQALR58UgFSPElhABSEAAWgQAiEHDxAMoA0gDi8QCMAMw9AByVGFCiAEqN8RUAYq3xPV0ALJp5zCtrqxvrW5ubmgDUzFQW-DCEzAcA7g7VQswA2lwWUHQAuszOAPQqH-wQUnAXap4ODuQgHYYKO7DCAwIG4ZjQOAvTRne7Q2F4BEjF5IZjMapyVJID4fOCuDBSVJcOAAOkgUmYAHIAKLkynU5iWGDUxmaGgiBkWVL8YwMrAQHjw-gOIT-GAMVjQfhwcxwPzw7BC45gJ4Ac2YcEeMBphAAwv4MBwHP5FVBlar1cwZK4LFJjIJcMd3QrlQpna73ZzDVxA5YzLZTDADcaQAwQBBUpYlchQMJcBALlFhAh+MgQBguBcMI5c3GOLgMHw1c1UpW9cgYLhjHA43ApBw4FgcFgqMNdcYMLq4FNJDI5PWUBhjCpYyACVIuAB1aoOOD8WtgODNHMOCwANwcjjzYH4pZAT2VuBgUQrupkyDEBeVcYMrgAQhWqzBmhS4EcRg+T4tiAr7NHq1IAIrGDCcCAVwz4gLWuCXnmMi4HQ4oXFAs6pJ6sCLrYsLIP0AAMca4RAyqLhWqR5rha54HusFxgAjtB8A3gmuaTvweQjJ2naziIbEpHAN6DveSCPvBwHKlIFgNk2sngXAUEwXBCEwJaBFYERSAAExxo2GCxHqpp-JJIBrgArLO7pwAAKpa3HSQhe7NgAklAdjfmAnqJok3nNE41IaXAIQhEAA
[r]: https://cran.r-project.org
[rstudio]: https://www.rstudio.com/products/rstudio/download/#download
[theme documentation]: https://themes.gohugo.io//theme/hugo-theme-learn/en
[vscode]: https://code.visualstudio.com
[vscode-guide]: https://github.com/tonic-team/tonic.site/wiki/How-to-edit-Markdown-files-using-Visual-Studio-Code
