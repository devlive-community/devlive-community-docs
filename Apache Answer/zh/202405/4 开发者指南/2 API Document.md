[TOC]

Answer 使用swagger自动生成API文档。 Swagger可以以友好的方式展示API文档，也可以提供一种便捷的方式来测试API。

## API文档在哪里？

### 快速查看

如果您想快速查看API文档，可以访问以下链接：
https://meta.answer.dev/swagger/index.html

### 查看自己的API文档

如果您已有Answer实例，您可以通过以下链接查看自己实例的API文档：
`https://example.com/swagger/index.html`

如果无法访问上述链接，请检查以下配置项是否配置正确。

```yaml
swaggerui:
  show: true
  protocol: http
  host: 127.0.0.1
  address: ':9080' # leave blank to use the 80 port number
```

## 生成API文档

使用[swag](https://github.com/swaggo/swag)回答，根据代码中的注释自动生成API文档json/yaml文件。您可以按照以下步骤生成API文档。
```bash
# install swag cli
$ go install github.com/swaggo/swag/cmd/swag@latest

# enter the project root directory and execute the following command
$ cd script
$ ./gen-api.sh

# the generated documentation is in the docs/api directory
```

