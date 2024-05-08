[TOC]

### 关于 GitHub CLI 扩展

GitHub CLI 扩展 有关如何使用 GitHub CLI 扩展的更多信息，请参阅 [AUTOTITLE]($Using-GitHub-CLI-Extensions)。

您创建的每个扩展都需要一个存储库。存储库名称必须以 `gh-` 开头。存储库名称的其余部分是扩展的名称。存储库的根目录必须有一个与存储库同名的可执行文件或附加到版本的一组预编译的二进制可执行文件。

> 当依赖可执行脚本时，我们建议使用 bash 脚本，因为 bash 是一种广泛使用的解释器。您可以使用非 bash 脚本，但用户必须安装必要的解释器才能使用扩展。如果您不想依赖安装了解释器的用户，请考虑预编译扩展。

### 使用 `gh extension create` 创建扩展

> 运行不带参数的 `gh extension create` 将启动交互式向导。

您可以使用 `gh extension create` 命令为您的扩展创建一个项目，其中包括一个包含一些起始代码的 bash 脚本。

1. 使用 `gh extension create` 子命令设置新扩展。将 `EXTENSION-NAME` 替换为您的扩展名。

    ```shell
    gh extension create EXTENSION-NAME
    ```

1. 按照打印的说明完成并可选择发布您的扩展。

### 使用 `gh extension create` 在 Go 中创建预编译扩展

您可以使用 `--precompiled=go` 参数为您的扩展创建基于 Go 的项目，包括 Go 脚手架、工作流脚手架和起始代码。

1. 使用 `gh extension create` 子命令设置新扩展。将 `EXTENSION-NAME` 替换为您的扩展名，并指定 `--precompiled=go`。

    ```shell
    gh extension create --precompiled=go EXTENSION-NAME
    ```

1. 按照打印的说明完成并可选择发布您的扩展。

### 使用 `gh extension create` 创建非 Go 预编译扩展

您可以使用 `--precompiled=other` 参数为非 Go 预编译扩展创建项目，包括工作流脚手架。

1. 使用 `gh extension create` 子命令设置新扩展。将 `EXTENSION-NAME` 替换为您的扩展名，并指定 `--precompiled=other`。

    ```shell
    gh extension create --precompiled=other EXTENSION-NAME
    ```

1. 使用您选择的编译语言为您的扩展添加一些初始代码。

1. 在 `script/build.sh` 中填写构建扩展的代码，以确保您的扩展可以自动构建。

1. 按照打印的说明完成并可选择发布您的扩展。

### 手动创建扩展

1. 为您的扩展创建一个名为 `gh-EXTENSION-NAME` 的本地目录。将 `EXTENSION-NAME` 替换为您的扩展名。例如，`gh-whoami`。

1. 在您创建的目录中，添加与该目录同名的可执行文件。

   > 确保您的文件是可执行的。在 Unix 上，您可以在命令行中执行 `chmod +x file_name` 以使 `file_name` 可执行。在 Windows 上，您可以运行 `git init -b main`、`git add file_name`，然后运行 `git update-index --chmod=+x file_name`。

1. 将脚本写入可执行文件中。例如：

   ```bash
   #!/usr/bin/env bash
   set -e
   exec gh api user --jq '"You are @\(.login) (\(.name))."'
   ```

1. 从您的目录中，将扩展安装为本地扩展。

   ```shell
   gh extension install .
   ```

1. 验证您的扩展是否有效。将 `EXTENSION-NAME` 替换为您的扩展名。例如，`whoami`。

   ```shell
   gh EXTENSION-NAME
   ```

1. 从您的目录中创建一个存储库来发布您的扩展。将 `EXTENSION-NAME` 替换为您的扩展名。

   ```shell
   git init -b main
   git add . && git commit -m "initial commit"
   gh repo create gh-EXTENSION-NAME --source=. --public --push
   ```

1. （可选）为了帮助其他用户发现您的扩展，请添加存储库主题 `gh-extension`。这将使扩展出现在 [`gh-extension` 主题页面](https://github.com/topics/gh-extension)。有关如何添加存储库主题的更多信息，请参阅 [AUTOTITLE](/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics)。

## 编写解释型 GitHub CLI 扩展的技巧

### 处理参数和标志

`gh my-extension-name` 命令后面的所有命令行参数都将传递到扩展脚本。在 bash 脚本中，您可以使用 `$1`、`$2`等引用参数。您可以使用参数来获取用户输入或修改脚本的行为。

例如，此脚本处理多个标志。当使用 `-h` 或 `--help` 标志调用脚本时，脚本将打印帮助文本而不是继续执行。当使用 `--name` 标志调用脚本时，脚本将该标志后的下一个值设置为 `name_arg`。当使用 `--verbose` 标志调用脚本时，脚本会打印不同的问候语。

```bash
#!/usr/bin/env bash
set -e

verbose=""
name_arg=""
while [ $# -gt 0 ]; do
  case "$1" in
  --verbose)
    verbose=1
    ;;
  --name)
    name_arg="$2"
    shift
    ;;
  -h|--help)
    echo "Add help text here."
    exit 0
    ;;
  esac
  shift
done

if [ -z "$name_arg" ]
then
  echo "You haven't told us your name."
elif [ -z "$verbose" ]
then
  echo "Hi $name_arg"
else
  echo "Hello and welcome, $name_arg"
fi
```

### 非交互方式调用核心命令

一些 GitHub CLI 核心命令将提示用户输入。使用这些命令编写脚本时，通常不需要出现提示。为了避免提示，请通过参数显式提供必要的信息。

例如，要以编程方式创建问题，请指定标题和正文：

```shell
gh issue create --title "My Title" --body "Issue description"
```

### 以编程方式获取数据

许多核心命令支持 `--json` 标志以编程方式获取数据。例如，要返回一个 JSON 对象，列出拉取请求的数量、标题和可合并性状态：

```shell
gh pr list --json number,title,mergeStateStatus
```

如果没有从 GitHub 获取特定数据的核心命令，您可以使用 [`gh api`](https://cli.github.com/manual/gh_api) 命令访问 GitHub API。例如，要获取有关当前用户的信息：

```shell
gh api user
```

所有输出 JSON 数据的命令还可以选择将该数据过滤为更可供脚本立即使用的内容。例如，获取当前用户的名称：

```shell
gh api user --jq '.name'
```

有关更多信息，请参阅 [`gh help formatting`](https://cli.github.com/manual/gh_help_formatting).

## 手动创建预编译扩展

1. 为您的扩展创建一个名为 `gh-EXTENSION-NAME` 的本地目录。将 `EXTENSION-NAME` 替换为您的扩展名。例如，`gh-whoami`。

1. 在您创建的目录中，添加一些源代码。例如：

    ```golang
    package main
    import (
      "github.com/cli/go-gh"
      "fmt"
    )

    func main() {
      args := []string{"api", "user", "--jq", `"You are @\(.login) (\(.name))"` }
      stdOut, _, err := gh.Exec(args...)
      if err != nil {
        fmt.Println(err)
        return
      }
      fmt.Println(stdOut.String())
    }
    ```

1. 从您的目录中，将扩展安装为本地扩展。

    ```shell
    gh extension install .
    ```

1. 构建您的代码。例如，使用 Go，将 `YOUR-USERNAME` 替换为您的 GitHub 用户名：

    ```shell
    go mod init github.com/YOUR-USERNAME/gh-whoami
    go mod tidy
    go build
    ```

1. 验证您的扩展是否有效。将 `EXTENSION-NAME` 替换为您的扩展名。例如，`whoami`。

    ```shell
    gh EXTENSION-NAME
    ```

1. 从您的目录中创建一个存储库来发布您的扩展。将 `EXTENSION-NAME` 替换为您的扩展名。

   > 请小心，不要将编译步骤生成的二进制文件提交给版本控制。

   ```shell
    git init -b main
   echo "gh-EXTENSION-NAME" >> .gitignore
   git add main.go go.* .gitignore && git commit -m 'Initial commit'
   gh repo create "gh-EXTENSION-NAME"
   ```

1. 创建一个版本以与其他人共享您的预编译扩展。针对您想要支持的每个平台进行编译，将每个二进制文件作为资产附加到版本中。附加到版本的二进制可执行文件必须遵循命名约定并具有 OS-ARCHITECTURE\[EXTENSION\] 后缀。

   例如，为 Windows 64 位编译的名为 `whoami` 的扩展将具有名称 `gh-whoami-windows-amd64.exe`，而为 Linux 32 位编译的相同扩展将具有名称 `gh-whoami-linux-386`。要查看 `gh` 识别的操作系统和架构组合的详尽列表，请参阅[此源代码](https://github.com/cli/cli/blob/14f704fd0da58cc01413ee4ba16f13f27e33d15e/pkg/cmd/extension/manager.go#L696 ）。
   
   > 为了使您的扩展能够在 Windows 上正常运行，其资产文件必须具有 `.exe` 扩展名。其他操作系统无需扩展。

   可以从命令行创建版本。例如：

   ```shell
   git tag v1.0.0
   git push origin v1.0.0
   GOOS=windows GOARCH=amd64 go build -o gh-EXTENSION-NAME-windows-amd64.exe
   GOOS=linux GOARCH=amd64 go build -o gh-EXTENSION-NAME-linux-amd64
   GOOS=darwin GOARCH=amd64 go build -o gh-EXTENSION-NAME-darwin-amd64
   gh release create v1.0.0 ./*amd64*
   ```

1. （可选）为了帮助其他用户发现您的扩展，请添加存储库主题“gh-extension”。这将使扩展出现在 [`gh-extension` 主题页面](https://github.com/topics/gh-extension)。有关如何添加存储库主题的更多信息，请参阅“[使用主题对存储库进行分类](/github/administering-a-repository/managing-repository-settings/classifying-your-repository-with-topics)”。

## 编写预编译 GitHub CLI 扩展的技巧

### 自动化发布

考虑将 [gh-extension-precompile](https://github.com/cli/gh-extension-precompile) 操作添加到项目中的工作流程中。此操作将自动为您的扩展生成交叉编译的 Go 二进制文件，并为非 Go 预编译扩展提供构建脚手架。

### 使用基于 Go 的扩展中的 GitHub CLI 功能

考虑使用 [go-gh](https://github.com/cli/go-gh)，这是一个 Go 库，它公开了一些 `gh` 功能以供在扩展中使用。

## 下一步

要查看 GitHub CLI 扩展的更多示例，请查看[具有 `gh-extension` 主题的存储库](https://github.com/topics/gh-extension)。
