[TOC]

To generate a Word document from R Markdown, you can use the output format `word_document`. If you want to include cross-references in the document, you may consider the output format `bookdown::word_document2`, as mentioned in Section [4.7]($Cross-referencing-Within-Documents).

    ---
    output:
      word_document: default
      bookdown::word_document2: default  # for cross-references
    ---

From our experience, the most frequently asked questions about Word output are:

1.  How can I apply a custom Word template to the document?

2.  How can I incorporate changes made in Word in the original R Markdown document?

3.  How can I style individual document elements?


We will address these questions in this chapter.
