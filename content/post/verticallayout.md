---
title: "verticalLayout"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "verticallayout"
weight: 3
description: "UI要素を縦にレイアウト。"
---

{{< highlight r >}}
verticalLayout(..., fluid = TRUE)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|コンテナ内に含まれる要素|
|**`fluid`**|`TRUE`なら可変レイアウト、`FALSE`なら固定レイアウトとなります。|

### 説明

１つ以上コンテンツの行を含むコンテナを生成します。コンテナに渡されるそれぞれの要素はUI中の自身の列上に現れます。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  verticalLayout(
    a(href="http://example.com/link1", "Link One"),
    a(href="http://example.com/link2", "Link Two"),
    a(href="http://example.com/link3", "Link Three")
  )
)
shinyApp(ui, server = function(input, output) { })
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/verticalLayout.html