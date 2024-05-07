[TOC]

The basic R session information when compiling this book is as follows:

```r
xfun::session_info(c(
  'bookdown', 'knitr', 'rmarkdown', 'xfun'
), dependencies = FALSE)
```

We do not add prompts (`>` and `+`) to R source code in this book, and we comment out the text output with two hashes `##` by default, as you can see from the R session information above. This is for your convenience when you want to copy and run the code (the text output will be ignored since it is commented out). Package names are in bold text (e.g., **rmarkdown**), and inline code and filenames are formatted in a typewriter font (e.g., `knitr::knit('foo.Rmd')`). Function names are followed by parentheses (e.g., `blogdown::serve_site()`). The double-colon operator `::` means accessing an object from a package.

"Rmd" is the filename extension of R Markdown files, and also an abbreviation of R Markdown in this book.
