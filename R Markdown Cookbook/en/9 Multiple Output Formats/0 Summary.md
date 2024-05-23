[TOC]

One main advantage of R Markdown is that it can create multiple output formats from a single source, which could be one or multiple Rmd documents. For example, this book was written in R Markdown, and compiled to two formats: PDF for printing, and HTML for the online version.

Sometimes it can be challenging to make an output element of a code chunk work for all output formats. For example, it is extremely simple to create a rounded and circular image in HTML output with a single CSS rule (`img { border-radius: 50%; }`), but not so straightforward in LaTeX output (typically it will involve TikZ graphics).

Sometimes it is just impossible for an output element to work for all output formats. For example, you can easily create a GIF animation with the **gifski** package ([Ooms, Kornel Lesiński, and Authors of the dependency Rust crates 2023](#ref-R-gifski)) (see Section [4.14]($Create-An-Animation-From-Multiple-R-Plots)), and it will work perfectly for HTML output, but embedding such an animation in LaTeX output is not possible without extra steps of processing the GIF file and using extra LaTeX packages.

This chapter provides a few examples that can work for multiple formats. If a certain feature is only available to a specific output format, we will show you how to conditionally enable or disable it based on the output format.

### References[]

Ooms, Jeroen, Kornel Lesiński, and Authors of the dependency Rust crates. 2023. _Gifski: Highest Quality GIF Encoder_. [https://r-rust.r-universe.dev/gifski](https://r-rust.r-universe.dev/gifski).
