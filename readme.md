# MontFerret/ferret [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 `ferret`是一个网络抓取系统。 」

[中文](./readme.md) | [english](https://github.com/MontFerret/ferret)

---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'MontFerret/ferret' -->
<!-- commit = '88188cac2c0c603d24377cd2b321f7cf9a2991e5' -->
<!-- time = '2018-10-11' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-10-11 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/MontFerret/ferret.svg
[commit]: https://github.com/MontFerret/ferret/tree/88188cac2c0c603d24377cd2b321f7cf9a2991e5

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [ferret](#ferret)
  - [它是什么?](#%E5%AE%83%E6%98%AF%E4%BB%80%E4%B9%88)
  - [给我看一些代码](#%E7%BB%99%E6%88%91%E7%9C%8B%E4%B8%80%E4%BA%9B%E4%BB%A3%E7%A0%81)
  - [特性](#%E7%89%B9%E6%80%A7)
  - [动机](#%E5%8A%A8%E6%9C%BA)
  - [灵感](#%E7%81%B5%E6%84%9F)
  - [WIP](#wip)
  - [安装](#%E5%AE%89%E8%A3%85)
    - [先决条件](#%E5%85%88%E5%86%B3%E6%9D%A1%E4%BB%B6)
      - [生产](#%E7%94%9F%E4%BA%A7)
      - [发展](#%E5%8F%91%E5%B1%95)
  - [快速开始](#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)
    - [无浏览器模式](#%E6%97%A0%E6%B5%8F%E8%A7%88%E5%99%A8%E6%A8%A1%E5%BC%8F)
    - [浏览器模式](#%E6%B5%8F%E8%A7%88%E5%99%A8%E6%A8%A1%E5%BC%8F)
    - [嵌入模式](#%E5%B5%8C%E5%85%A5%E6%A8%A1%E5%BC%8F)
  - [可扩展性](#%E5%8F%AF%E6%89%A9%E5%B1%95%E6%80%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ferret

[![Build Status](https://travis-ci.com/MontFerret/ferret.svg?branch=master)](https://travis-ci.com/MontFerret/ferret)\
![ferret](https://raw.githubusercontent.com/MontFerret/ferret/master/assets/intro.jpg)

## 它是什么?

`ferret`是一个网络抓取系统，旨在简化网络上的数据提取，用于 UI 测试，机器学习和分析等.\
拥有自己的声明性语言，`ferret`抽象出技术细节和底层技术的复杂性，帮助关注数据本身.\
它非常便携,可扩展且快速.

## 给我看一些代码

以下示例演示了动态页面的使用.\
首先,我们加载主 Google 搜索页面,在输入框中，键入搜索条件,然后单击搜索按钮.\
点击操作会触发重定向,因此我们会等到它结束.\
页面加载后,我们迭代搜索结果中的所有元素，并将输出分配给变量.\
最后的 for 循环会过滤掉，可能因使用不准确选择器而导致的空元素.

```aql
LET google = DOCUMENT("https://www.google.com/", true)

INPUT(google, 'input[name="q"]', "ferret", 25)
CLICK(google, 'input[name="btnK"]')

WAIT_NAVIGATION(google)

FOR result IN ELEMENTS(google, '.g')
    // 过滤videos 和 'People also ask'等的额外元素
    FILTER TRIM(result.attributes.class) == 'g'
    RETURN {
        title: INNER_TEXT(result, 'h3'),
        description: INNER_TEXT(result, '.st'),
        url: INNER_TEXT(result, 'cite')
    }
```

您可以找到更多示例[这里](https://github.com/MontFerret/ferret/blob/master/examples)

## 特性

- 陈述性语言
- 支持静态和动态网页
- 嵌入式
- 可扩展

## 动机

如今数据就是一切,谁拥有数据 - 拥有世界.\
我参与了多个数据驱动的项目,其中数据是系统的重要组成部分,我意识到编写大量的刮刀(爬虫)是多么繁琐.\
经过一段时间寻找一个，让我不再编写代码的工具，仅仅给出我需要的数据,这时我决定提出我自己的解决方案.\
`ferret`项目是一项雄心勃勃的计划,旨在为通用平台，不费吹灰之力编写刮刀。

## 灵感

FQL(Ferret查询语言)受到了[AQL](https://www.arangodb.com/)(ArangoDB 查询语言)很大的启发.\
但由于域名具体,在工作方式上,存在一些差异.

## WIP

请注意,该项目正在大力发展。暂时没有文档,且最终版本中可能会有一些变化.\
对于查询语法,您可以转到[ArangoDB 网站](https://docs.arangodb.com/3.3/AQL/index.html)并，使用 AQL 文档作为 FQL 的文档 - 因为它们是相同的.

## 安装

### 先决条件

#### 生产

- Go >= 1.9
- Chrome 或 Docker

#### 发展

- GoDep
- GNU Make
- ANTLR4 >= 4.7.1

```sh
go get github.com/MontFerret/ferret
```

您可以使用 Google Chrome / Chromium 的本地副本,但为了便于使用,建议您在 Docker 容器中，运行它:

```sh
docker pull alpeware/chrome-headless-trunk
docker run -d -p=0.0.0.0:9222:9222 --name=chrome-headless -v /tmp/chromedata/:/data alpeware/chrome-headless-trunk
```

但是,如果您想查看查询执行过程中发生的情况,只需以远程调试端口启动 Chrome:

```sh
chrome.exe --remote-debugging-port=9222
```

## 快速开始

### 无浏览器模式

如果你想玩`fql`，并检查其语法,您可以使用以下命令运行 CLI:

```
ferret
```

`ferret`将以 REPL 模式运行.

```shell
Welcome to Ferret REPL
Please use `Ctrl-D` to exit this program.
>%
>LET doc = DOCUMENT('https://news.ycombinator.com/')
>FOR post IN ELEMENTS(doc, '.storylink')
>RETURN post.attributes.href
>%
```

**注意:**符号`%`用于启动，和结束多行查询。您也可以使用 heredoc 格式.

如果要执行存储在文件中的查询,只需传递文件名:

```
ferret ./docs/examples/static-page.fql
```

```
cat ./docs/examples/static-page.fql | ferret
```

```
ferret < ./docs/examples/static-page.fql
```

### 浏览器模式

默认情况下,`ferret`通过 HTTP 协议加载 HTML 页面,因为它更快.\
但是现在,有越来越多的网站使用 JavaScript 进行渲染,因此,这种"老派"方法，常常并没有真正起作用。\
对于这种情况，您可以通过 Chrome DevTools 协议(也称为 CDP)使用 Chrome 或 Chromium 获取文档页面.\
首先,您需要确保已启动 Chrome 的`remote-debugging-port=9222`参数.\
其次,您需要将地址传递给`ferret`CLI.

```
ferret --cdp http://127.0.0.1:9222
```

**注意:**默认情况下,`ferret`以这个本地地址，作为默认地址,因此在不同端口号或远程地址的情况下，才用显式传递参数.

或者,您可以告诉 CLI 为您启动 Chrome.

```shell
ferret --cdp-launch
```

**注意:**MacOS 上的启动命令，目前已被破坏.

一旦`ferret`知道如何与 Chrome 通信,您可以使用一个`DOCUMENT(url, isDynamic)`函数，用布尔值`true`表明isDynamic是否动态页面:

```shell
Welcome to Ferret REPL
Please use `exit` or `Ctrl-D` to exit this program.
>%
>LET doc = DOCUMENT('https://soundcloud.com/charts/top', true)
>WAIT_ELEMENT(doc, '.chartTrack__details', 5000)
>LET tracks = ELEMENTS(doc, '.chartTrack__details')
>FOR track IN tracks
>    LET username = ELEMENT(track, '.chartTrack__username')
>    LET title = ELEMENT(track, '.chartTrack__title')
>    RETURN {
>       artist: username.innerText,
>        track: title.innerText
>    }
>%
```

```shell
Welcome to Ferret REPL
Please use `exit` or `Ctrl-D` to exit this program.
>%
>LET doc = DOCUMENT("https://github.com/", true)
>LET btn = ELEMENT(doc, ".HeaderMenu a")

>CLICK(btn)
>WAIT_NAVIGATION(doc)
>WAIT_ELEMENT(doc, '.IconNav')

>FOR el IN ELEMENTS(doc, '.IconNav a')
>    RETURN TRIM(el.innerText)
>%
```

### 嵌入模式

`ferret`是一个注重模块化的系统,因此,可以轻松嵌入到您的 Go 应用程序中.

```go
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"github.com/MontFerret/ferret/pkg/compiler"
	"os"
)

type Topic struct {
	Name        string `json:"name"`
	Description string `json:"description"`
	Url         string `json:"url"`
}

func main() {
	topics, err := getTopTenTrendingTopics()

	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	for _, topic := range topics {
		fmt.Println(fmt.Sprintf("%s: %s %s", topic.Name, topic.Description, topic.Url))
	}
}

func getTopTenTrendingTopics() ([]*Topic, error) {
	query := `
		LET doc = DOCUMENT("https://github.com/topics")

		FOR el IN ELEMENTS(doc, ".py-4.border-bottom")
			LIMIT 10
			LET url = ELEMENT(el, "a")
			LET name = ELEMENT(el, ".f3")
			LET desc = ELEMENT(el, ".f5")

			RETURN {
				name: TRIM(name.innerText),
				description: TRIM(desc.innerText),
				url: "https://github.com" + url.attributes.href
			}
	`

	comp := compiler.New()

	program, err := comp.Compile(query)

	if err != nil {
		return nil, err
	}

	out, err := program.Run(context.Background())

	if err != nil {
		return nil, err
	}

	res := make([]*Topic, 0, 10)

	err = json.Unmarshal(out, &res)

	if err != nil {
		return nil, err
	}

	return res, nil
}
```

## 可扩展性

同样的,`ferret`更是一个注重模块化的系统,它不仅可以嵌入它,还可以扩展其标准库.

```go
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"github.com/MontFerret/ferret/pkg/compiler"
	"github.com/MontFerret/ferret/pkg/runtime/core"
	"github.com/MontFerret/ferret/pkg/runtime/values"
	"os"
)

func main() {
	strs, err := getStrings()

	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	for _, str := range strs {
		fmt.Println(str)
	}
}

func getStrings() ([]string, error) {
	// 此函数实现了一种函数类型，而ferret支持该函数作为运行时函数
	transform := func(ctx context.Context, args ...core.Value) (core.Value, error) {
		// 它只是一个辅助函数，有助于验证一些传递的args
		err := core.ValidateArgs(args, 1)

		if err != nil {
			// 建议返回内置的None类型，而不是nil
			return values.None, err
		}

		// 这是另一个允许进行类型验证的辅助函数
		err = core.ValidateType(args[0], core.StringType)

		if err != nil {
			return values.None, err
		}

		// 强制转换为内置字符串类型
		str := args[0].(values.String)

		return str.Concat(values.NewString("_ferret")).ToUpper(), nil
	}

	query := `
		FOR el IN ["foo", "bar", "qaz"]
			// 通常，所有函数都以大写形式注册
			RETURN TRANSFORM(el)
	`

	comp := compiler.New()
	comp.RegisterFunction("transform", transform)

	program, err := comp.Compile(query)

	if err != nil {
		return nil, err
	}

	out, err := program.Run(context.Background())

	if err != nil {
		return nil, err
	}

	res := make([]string, 0, 3)

	err = json.Unmarshal(out, &res)

	if err != nil {
		return nil, err
	}

	return res, nil
}
```

最重要的是,您可以绕过以下选项，完全关闭标准库:

```go
comp := compiler.New(compiler.WithoutStdlib())
```

之后,您可以轻松地从标准库中，提供自己的函数实现.

如果您不需要标准库中的特定函数集,则可以关闭整个`stdlib`函数，并注册其他单独的包:

```go
package main

import (
    "github.com/MontFerret/ferret/pkg/compiler"
    "github.com/MontFerret/ferret/pkg/stdlib/strings"
)

func main() {
    comp := compiler.New(compiler.WithoutStdlib())

    comp.RegisterFunctions(strings.NewLib())
}
```
