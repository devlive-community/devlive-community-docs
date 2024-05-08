[TOC]

## 关于 GitHub CLI 扩展

> GitHub 和 GitHub CLI 之外的扩展未经 GitHub 认证，并受单独的服务条款、隐私政策和支持文档的约束。为了降低使用第三方扩展时的风险，请在安装或更新扩展之前审核扩展的源代码。

GitHub CLI 扩展 有关如何创建 GitHub CLI 扩展的更多信息，请参阅 _"[AUTOTITLE]($Creating-GitHub-CLI-Extensions)."

扩展在本地安装并且仅限于用户。因此，如果您从不同的计算机访问 GitHub CLI，或者其他用户从同一台计算机访问 GitHub CLI，则该扩展将不可用。_

## 寻找扩展

您可以通过浏览[具有 `gh-extension` 主题的存储库](https://github.com/topics/gh-extension)来查找扩展。

## 安装扩展

要安装扩展，请使用 `extensions install` 子命令。将 `repo` 参数替换为扩展的存储库。您可以使用完整的 URL，例如https://github.com/octocat/gh-whoami，也可以仅使用所有者和存储库，例如 `octocat/gh-whoami`。

如果使用所有者和存储库，`gh` 将使用 `gh` 当前经过身份验证的主机名安装扩展。从不同主机安装扩展时，完整 URL 格式非常有用。例如，GitHub Enterprise Server 上的用户应使用完整的存储库 URL 从 GitHub.com 或任何其他主机安装扩展。

要从当前目录安装开发中的扩展，请使用 `.` 作为 `repo` 参数的值。

```shell
gh extension install REPO
```

如果您已经安装了同名的扩展，该命令将失败。例如，如果您已经安装了 `octocat/gh-whoami`，则必须在安装 `hubot/gh-whoami` 之前将其卸载。

## 运行扩展

安装扩展后，您可以使用 `gh EXTENSION-NAME` 运行该扩展，就像运行本机 GitHub CLI 命令一样。 `EXTENSION-NAME` 是包含扩展的存储库的名称，减去 `gh-` 前缀。

例如，如果您从 `octocat/gh-whoami` 存储库安装了扩展，则可以使用以下命令运行该扩展。

``` shell
gh whoami
```

您通常可以在包含扩展的存储库的自述文件中找到有关如何使用扩展的具体信息。

## 查看已安装的扩展

要查看所有已安装的扩展，请使用 `extensions list` 子命令。输出还将告诉您哪些扩展有可用的更新。

```shell
gh extension list
```

## 更新扩展

要更新扩展，请使用 `extensions upgrade` 子命令。将 `extension` 参数替换为扩展名。

```shell
gh extension upgrade EXTENSION
```

要更新所有已安装的扩展，请使用 `--all` 标志。

```shell
gh extension upgrade --all
```

## 卸载扩展

要卸载扩展，请使用 `extensions remove` 子命令。将 `extension` 参数替换为扩展名。

```shell
gh extension remove EXTENSION
```
