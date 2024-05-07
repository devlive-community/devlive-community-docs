[TOC]

It is recommended that readers have a basic understanding of R Markdown. [Chapter 2]($Basics) of *R Markdown: The Definitive Guide* [@rmarkdown2018] provides an overview of the basics of R Markdown and is recommended background reading for any new users of R Markdown. For example, we did not cover Markdown syntax in this book, and expect readers to learn Markdown elsewhere. In particular, we strongly recommend that you go through [the full manual of Pandoc](https://pandoc.org/MANUAL.html) at least once. The manual is quite lengthy, but it is also a gold mine. You do not have to remember everything, but it will be very helpful if you are aware of the possible features of Markdown. [For countless times, I have seen](https://yihui.org/en/2018/11/hard-markdown/) people fail to write verbatim code blocks that contain three backticks, or list items that contain child elements. Without fully reading the Markdown syntax in the manual, perhaps you will never know or understand the rule "`N + 1` outer backticks for `N` inner backticks" or "indent properly to indicate child elements."

We do not intend to provide a full technical reference for R Markdown in this cookbook. This cookbook aims to supplement, instead of replace, the existing literature. Therefore, readers may explore the following books if they want to seek further information:

- *R Markdown: The Definitive Guide* [@rmarkdown2018], the technical reference for all R Markdown output formats in the **rmarkdown** package and several other extension packages.

- Part V ("Communicate") of *R for Data Science* [@wickham2016]. This part is less technical than the above "Definitive Guide," and hence may be a gentler introduction to R Markdown.

- *Dynamic Documents with R and knitr* [@knitr2015] provides a thorough introduction to the **knitr** package [@R-knitr] (note that R Markdown is only one of the document formats that **knitr** supports). If you want to read a shorter version, you may find Karl Broman's minimal tutorial ["knitr in a knutshell"](https://kbroman.org/knitr_knutshell/) helpful.

- *bookdown: Authoring Books and Technical Documents with R Markdown* [@bookdown2016] is a short book as the official documentation of the **bookdown** package [@R-bookdown], which is designed to simplify the creation of long-format documents in R Markdown.

- *blogdown: Creating Websites with R Markdown* [@blogdown2017] introduces how to create websites in R Markdown with the **blogdown** package [@R-blogdown].

Where relevant, this book provides references to these existing resources. By the way, the official R Markdown website also contains a lot of resources that you may find helpful: https://rmarkdown.rstudio.com.

You do not need to read this book in a particular order. Later chapters are not necessarily more challenging than previous chapters. The chapters and sections that we consider to be more advanced than others are marked with an asterisk (`*`) in their titles. It may be most efficient to read this book when you have some specific tasks in mind that you want to do with R Markdown, otherwise you can thumb through the table of contents and see if you are interested in any particular parts. We have tried to make each section and example as self-contained as possible, so you do not have to go back and forth among different parts of this book. In some cases, cross-referencing is unavoidable, and we will refer you to the background knowledge required to understand a certain example.

If you want to try the examples by yourself, the full source code of this book and examples are freely provided on GitHub at https://github.com/yihui/rmarkdown-cookbook. If you are reading the electronic version of this book, you may also just copy and paste the examples from the pages and run them in your favorite editor.

### References

Wickham, Hadley, and Garrett Grolemund. 2016. R for Data Science. O’Reilly Media, Inc.
Xie, Yihui. 2015. Dynamic Documents with R and Knitr. 2nd ed. Boca Raton, Florida: Chapman; Hall/CRC. https://yihui.org/knitr/.

———. 2016. Bookdown: Authoring Books and Technical Documents with R Markdown. Boca Raton, Florida: Chapman; Hall/CRC. https://bookdown.org/yihui/bookdown.

———. 2023a. Bookdown: Authoring Books and Technical Documents with r Markdown. https://github.com/rstudio/bookdown.

———. 2023c. Knitr: A General-Purpose Package for Dynamic Report Generation in r. https://yihui.org/knitr/.

Xie, Yihui, J. J. Allaire, and Garrett Grolemund. 2018. R Markdown: The Definitive Guide. Boca Raton, Florida: Chapman; Hall/CRC. https://bookdown.org/yihui/rmarkdown.

Xie, Yihui, Christophe Dervieux, and Alison Presmanes Hill. 2024. Blogdown: Create Blogs and Websites with r Markdown. https://github.com/rstudio/blogdown.

Xie, Yihui, Alison Presmanes Hill, and Amber Thomas. 2017. Blogdown: Creating Websites with R Markdown. Boca Raton, Florida: Chapman; Hall/CRC. https://bookdown.org/yihui/blogdown/.