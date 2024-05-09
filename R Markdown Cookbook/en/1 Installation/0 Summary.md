[TOC]

To use R Markdown, you have to install R [@R-base] and the R package **rmarkdown** [@R-rmarkdown].

```{r eval=FALSE}
# install the rmarkdown package from CRAN in R
install.packages('rmarkdown')

# or install from GitHub if you want to test the development version
if (!requireNamespace("remotes")) install.packages('remotes')
remotes::install_github('rstudio/rmarkdown')
```

Unless you have a favorite editor or IDE (Integrated Development Environment), we recommend that you also install the RStudio\index{RStudio} IDE (https://www.rstudio.com). RStudio is not required, but it will make it easier for an average user to work with R Markdown because of the strong editor support. If you choose not to use the RStudio IDE, you will need to install Pandoc\index{Pandoc} (see Section [1.1]($Use-A-Pandoc-Version-Not-Bundled-With-The-RStudio-IDE)), which is the tool used by **rmarkdown** to convert Markdown to other document formats.

If you need to create PDF output, you may need to install LaTeX\index{LaTeX} (Section [1.2]($Install-LaTeX-TinyTeX-For-PDF-Reports)) and certain LaTeX packages (Section [1.3]($Install-Missing-LaTeX-Packages)).
