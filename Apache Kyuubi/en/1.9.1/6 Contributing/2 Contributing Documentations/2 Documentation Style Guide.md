[TOC]

This guide contains guidelines, not rules. While guidelines are important to follow, they are not hard and fast rules. It’s important to use your own judgement and discretion when creating content, and to depart from the guidelines when necessary to improve the quality and effectiveness of your content. Ultimately, the goal is to create content that is clear, concise, and useful to your audience, and sometimes deviating from the guidelines may be necessary to achieve that goal.

Goals
----------------------------------------------------------------------------------------------------------

*   Source text files are readable and portable
*   Source diagram files are editable
*   Source files are maintainable over time and across community

License Header
----------------------------------------------------------------------------------------------------------------------------

All original documents should include the ASF license header. All reproduced or quoted content should be authorized and attributed to the source.

If you are about to quote some from commercial materials, please refer to [ASF 3RD PARTY LICENSE POLICY](https://www.apache.org/legal/resolved.html#asf-3rd-party-license-policy), or consult the Apache Kyuubi PMC to avoid legality issues.

General Style
--------------------------------------------------------------------------------------------------------------------------

*   Use [ReStructuredText](https://docutils.sourceforge.io/rst.html) or [Markdown](https://en.wikipedia.org/wiki/Markdown) format for text, avoid HTML hacks
*   Use [draw.io](https://www.diagrams.net/) for drawing or editing an image, and export it as PNG for referencing in document. A pull request should commit both of them
*   Use Kyuubi for short instead of Apache Kyuubi after the first time in the same page
*   Character line limit: 78, except unbreakable ones
*   Prefer lists to tables
*   Prefer unordered list than ordered

ReStructuredText
--------------------------------------------------------------------------------------------------------------------------------

### Headings

*   Use **Pascal Case**, every word starts with an uppercase letter, e.g., ‘Documentation Style Guide’
*   Use a max of **three levels**

> *   Split into multiple files when there comes an H4
>
> *   Prefer [\`directive rubric\`_](https://kyuubi.readthedocs.io/en/v1.9.1/contributing/doc/style.html#id6) than H4
>

*   Use underline-only adornment styles, **DO NOT** use overline

> *   The length of underline characters **SHOULD** match the title
>
> *   H1 should be underlined with ‘=’
>
> *   H2 should be underlined with ‘-’
>
> *   H3 should be underlined with ‘~’
>
> *   H4 should be underlined with ‘^’, but it’s better to avoid using H4
>

*   **DO NOT** use numbering for sections
*   **DO NOT** use “Kyuubi” in titles if possible

### Links

*   Define links with short descriptive phrases, group them at the bottom of the file

> Recommended

```java
Please refer to `Apache Kyuubi Home Page`_.

.. _Apache Kyuubi Home Page: https://kyuubi.apache.org/
```

> Not recommended

```java
Please refer to `Apache Kyuubi Home Page <https://kyuubi.apache.org/>`_.
```

Markdown
----------------------------------------------------------------------------------------------------------------

### Headings

*   Use **Pascal Case**, every word starts with an uppercase letter, e.g., ‘Documentation Style Guide’
*   Use a max of **three levels**

> *   Split into multiple files when there comes an H4
>

*   **DO NOT** use numbering for sections
*   **DO NOT** use “Kyuubi” in titles if possible

Images
------------------------------------------------------------------------------------------------------------

Use images only when they provide helpful visual explanations of information otherwise difficult to express with words

Third-party references
--------------------------------------------------------------------------------------------------------------------------------------------

If the preceding references don’t provide explicit guidance, then see these third-party references, depending on the nature of your question:

*   [Google developer documentation style](https://developers.google.com/style)
*   [Apple Style Guide](https://help.apple.com/applestyleguide/)
*   [Red Hat supplementary style guide for product documentation](https://redhat-documentation.github.io/supplementary-style-guide/)
