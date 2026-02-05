# Ramile

[English Version](#english-version)

_Ramile 是一个方便的工具，用于自动从给定的项目/文件夹中提取 3000 行源代码，以满足中国软件著作权申请流程的要求。Ramile 的目标是为您在每次软件著作权提交中准备 60 页源代码时节省 0.5~1 小时的时间。_

目前 Ramile 具有以下功能：

- 自动提取源代码并生成包含 3000 行代码的 docx 文件。（不过您必须手动删除 docx 的最后几页，使其正好为 60 页）
- 支持大多数常见的前端项目：Android/iOS/Web/微信小程序等
- 可配置。只需在项目根文件夹下放置一个 `.ramileconfig.json` 文件。（详情请参阅“配置”部分）

在 python 3.6.1 下测试通过。

## 安装

目前我们只能从源代码运行 Ramile。将来可能会上传到 pypi。

要运行 Ramile 源代码，请克隆存储库并安装依赖项：`pip install -r requirements.txt`。如果在国内，可以使用镜像：`pip install -i https://pypi.mirrors.ustc.edu.cn/simple/ -r requirements.txt`

## 基本用法

使用 [uv](https://docs.astral.sh/uv/) 运行（推荐）：

```
uv run ramile-cli.py extract <您的项目根路径>
```

或者直接使用 python：

```
python ramile-cli.py extract <您的项目根路径>
```

提取完成后，将在您的项目根目录下生成一个名为 `extracted_code.docx` 的文件，其中包含 3000 行代码。您只需打开它并删除不需要的页面，使文档正好为 60 页。

如果您想严格符合[规定](./著作权法.md#第十条-软件的鉴别材料包括程序和文档的鉴别材料)，可以通过在命令行后追加 `Inf` 来提取所有行：

使用 uv（推荐）：

```
uv run ramile-cli.py extract <您的项目根路径> Inf
```

或者直接使用 python：

```
python ramile-cli.py extract <您的项目根路径> Inf
```

然后您只需打开它并保留前 30 页和后 30 页，并删除所有中间页面。

## 配置

如果存在，Ramile 会自动从项目根目录加载配置文件 `.ramileconfig.json`。该文件应为 json 格式。可能的配置项如下：

| Key              | Description                                                                                                                                 | Default | Example          |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------ | :------ | :--------------- |
| ignore           | 设置 Ramile 要忽略的目录/文件。"ignore" 路径应该是 source_root 下的子目录/文件。以任何 "ignore" 项开头的目录/文件都将被忽略。不支持通配符。 | []      | ['Pods', 'libs'] |
| source_root      | 覆盖源代码的根目录，以避免 Ramile 从项目根目录开始处理。                                                                                    | ''      | 'app'            |
| filters          | 设置文件扩展名的排他过滤器（这意味着所有其他扩展名将**不**被处理）。默认情况下，将处理所有文件。                                            | []      | ['.js', '.vue']  |
| lines_to_extract | 设置要提取的总行数                                                                                                                          | 3000    | 3000             |

## 支持的语言

| Language    | Extensions            |
| :---------- | :-------------------- |
| JavaScript  | .js, .jsx, .vue, .wpy |
| Java        | .java                 |
| C#          | .cs                   |
| C++         | .cpp, .hpp, .c, .h    |
| Dart        | .dart                 |
| PHP         | .php                  |
| HTML        | .html, .htm           |
| CSS         | .css, .less, .sass    |
| Swift       | .swift                |
| Objective-C | .m                    |

## 测试:

```shell
cd tests
pytest
```

---

<a name="english-version"></a>

# Ramile

_Ramile a handy tool used to automatically extract 3000 lines of source codes from given project/folder, as a requirement of China Software Copyright application process. The goal of Ramile is to save 0.5~1 hour of your time spent on preparing the 60 pages of source code for each Software Copyright submission._
Currently Ramile has below features:

- Automatically extracting the source code and generating a docx file containing 3000 lines. (You have to manually remove the last few pages of the docx to make it exactly 60 pages, though)
- Supporting most of the commmon front-end projects: android/ios/web/Wechat mini program, etc
- Configurable. Just place a `.ramileconfig.json` under the project root folder. (See "Config" section for details)

Tested under python 3.6.1.

## Installation

Right now we can only run Ramile from source code. In the future it may be uploaded to pypi.

To run Ramile source code, clone the repository and install dependencies: `pip install -r requirements.txt`. Or if in China, mirros could be used `pip install -i https://pypi.mirrors.ustc.edu.cn/simple/ -r requirements.txt`

## Basic Usage

Running with [uv](https://docs.astral.sh/uv/) (Recommended):

```
uv run ramile-cli.py extract <path to your project root>
```

Or just python:

```
python ramile-cli.py extract <path to your project root>
```

When the extraction is completed, a file named `extracted_code.docx` will be generated under your project root directory, with 3000 lines of code. You just have to open it and remove unnecessary pages to make the document exact 60 pages.

If you want to strictly meet the [regulation](./著作权法.md#第十条-软件的鉴别材料包括程序和文档的鉴别材料), you can extract all the lines by append `Inf` to the command line:

Using uv (Recommended):

```
uv run ramile-cli.py extract <path to your project root> Inf
```

Or just python:

```
python ramile-cli.py extract <path to your project root> Inf
```

And then you just have to open it and keep the first 30 pages and the last 30 pages, and remove all the intermediate pages.

## Config

Ramile automatically loads the config file `.ramileconfig.json` from the project root, if it exits. The file should be in json format. Possible config items as below:

| Key              | Description                                                                                                                                                                                                                          | Default | Example          |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------ | :--------------- |
| ignore           | Sets the directories/files to be ignored by Ramile. "ignore" paths should be sub directories/files under source_root. Any directories/files starting with any one of the "ignore" items will be ignored. Wildcars are not supported. | []      | ['Pods', 'libs'] |
| source_root      | Overwrites the root directory of source codes to avoid Ramile process from the project root.                                                                                                                                         | ''      | 'app'            |
| filters          | Sets the exclusive filters (which means, all other extensions will NOT be processed) for file extensions. By default all files will be processed.                                                                                    | []      | ['.js', '.vue']  |
| lines_to_extract | Sets the total lines to extract                                                                                                                                                                                                      | 3000    | 3000             |

## Supported Languages

| Language    | Extensions            |
| :---------- | :-------------------- |
| JavaScript  | .js, .jsx, .vue, .wpy |
| Java        | .java                 |
| C#          | .cs                   |
| C++         | .cpp, .hpp, .c, .h    |
| Dart        | .dart                 |
| PHP         | .php                  |
| HTML        | .html, .htm           |
| CSS         | .css, .less, .sass    |
| Swift       | .swift                |
| Objective-C | .m                    |

## Test:

```shell
cd tests
pytest
```
