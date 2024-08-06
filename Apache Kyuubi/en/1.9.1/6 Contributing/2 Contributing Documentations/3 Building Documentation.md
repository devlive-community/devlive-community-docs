[TOC]

Follow the steps below and learn how to build the Kyuubi documentation as the one you are watching now.

Setup Environment
----------------------------------------------------------------------------------------------------------------------------------

*   Firstly, install `virtualenv`, this is optional but recommended as it is useful to create an independent environment to resolve dependency issues for building the documentation.

```bash
$ pip install virtualenv
```

*   Switch to the `docs` root directory.

```bash
$ cd $KYUUBI_SOURCE_PATH/docs
```

*   Create a virtual environment named ‘kyuubi’ or anything you like using `virtualenv` if it’s not existing.

```bash
$ virtualenv kyuubi
```

*   Activate the virtual environment,

```bash
$ source ./kyuubi/bin/activate
```

Install All Dependencies
------------------------------------------------------------------------------------------------------------------------------------------------

Install all dependencies enumerated in the `requirements.txt`.

```bash
$ pip install -r requirements.txt
```

Create Documentation
----------------------------------------------------------------------------------------------------------------------------------------

Make sure you are in the `$KYUUBI_SOURCE_PATH/docs` directory.

### Linux & MacOS

```bash
$ make html
```

### Windows

```bash
$ make.bat html
```

If the build process succeed, the HTML pages are in `$KYUUBI_SOURCE_PATH/docs/_build/html`.

View Locally
------------------------------------------------------------------------------------------------------------------------

Open the $KYUUBI_SOURCE_PATH/docs/_build/html/index.html file in your favorite web browser.
