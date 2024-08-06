[TOC]

![Image 3: GitHub issues by-label](https://img.shields.io/github/issues/apache/kyuubi/kind:documentation?color=green&logo=gfi&logoColor=red&style=for-the-badge)

Trivial Fixes
--------------------------------------------------------------------------------------------------------------------------------

For typos, layout, grammar, spelling, punctuation errors and other similar issues or changes that occur within a single file, it is acceptable to make edits directly on the page being viewed. When viewing a source file on kyuubi’s [\`Github repository\`\_](https://kyuubi.readthedocs.io/en/v1.9.1/contributing/doc/get_started.html#id6), a simple click on the `edit icon` or keyboard shortcut `e` will activate the editor. Similarly, when viewing files on [\`Read The Docs\`\_](https://kyuubi.readthedocs.io/en/v1.9.1/contributing/doc/get_started.html#id8) platform, clicking on the `suggest edit` button will lead you to the editor. These methods do not require any local development environment setup and are convenient for making quick fixes.

Upon completion of the editing process, opt the `commit changes` option, adhere to the provided instructions to submit a pull request, and await feedback from the designated reviewer.

Major Fixes
----------------------------------------------------------------------------------------------------------------------------

For significant modifications that affect multiple files, it is advisable to clone the repository to a local development environment, implement the necessary changes, and conduct thorough testing prior to submitting a pull request.

### [Fork](https://github.com/apache/kyuubi/fork) The Repository

### Clone The Forked Repository

> Clone the repository

```bash
$ git clone https://github.com/your_username/kyuubi.git
```

Replace “your_username” with your GitHub username. This will create a local copy of your forked repository on your machine. You will see the `master` branch if you run `git branch` in the `kyuubi` folder.

### Create A New Branch

> Create a new branch

```bash
$ git checkout -b guide
Switched to a new branch 'guide'
```

### Editing And Testing

Make the necessary changes to the documentation files using a text editor. [Build and verify](https://kyuubi.readthedocs.io/en/v1.9.1/contributing/doc/build.html) the changes you have made to see if they look fine.

### Create A Pull Request

Once you have made the changes,

*   Commit them with a descriptive commit message using the command:

    > commit the changes
    
    ```bash
    $ git commit -m "Description of changes made"
    ```

*   Push the changes to your forked repository using the command

    > push the changes
    
    ```bash
    $ git push origin guide
    ```

*   [Create A Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) with a descriptive PR title and description.
*   Polishing the PR with comments of reviews addressed

Report Only
----------------------------------------------------------------------------------------------------------------------------

If you don’t have time to fix the doc issue and submit a pull request on your own, [reporting a document issue](https://github.com/apache/kyuubi/issues/new/choose) also helps. Please follow some basic rules:

*   Use the title field to clearly describe the issue
*   Choose the documentation report template
*   Fill out the required field in the documentation report
