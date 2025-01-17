[TOC]

## Update Project Version

```bash

build/mvn versions:set -DgenerateBackupPoms=false
```

## Update Dependency List

Kyuubi uses the `dev/dependencyList` file to indicate what upstream dependencies will actually go to the server-side classpath.

For Pull requests, a linter for dependency check will be automatically executed in GitHub Actions.

You can run `build/dependency.sh` locally first to detect the potential dependency change first.

If the changes look expected, run `build/dependency.sh --replace` to update `dev/dependencyList` in your Pull request.

## Format All Code

Kyuubi uses [Spotless](https://github.com/diffplug/spotless/tree/main/plugin-maven)
with [google-java-format](https://github.com/google/google-java-format) and [Scalafmt](https://scalameta.org/scalafmt/)
to format the Java and Scala code.

You can run `dev/reformat` to format all Java and Scala code.

## Append descriptions of new configurations to settings.md

Kyuubi uses settings.md to explain available configurations.

You can run `dev/gen/gen_all_config_docs.sh` to append and update descriptions of new configurations to `settings.md`.

## Generative Tooling Usage

In general, the ASF allows contributions co-authored using generative AI tools. However, there are several considerations when you submit a patch containing generated content.

Foremost, you are required to disclose usage of such tool. Furthermore, you are responsible for ensuring that the terms and conditions of the tool in question are
compatible with usage in an Open Source project and inclusion of the generated content doesn't pose a risk of copyright violation.

Please refer to [The ASF Generative Tooling Guidance](https://www.apache.org/legal/generative-tooling.html) for more detailed information.

