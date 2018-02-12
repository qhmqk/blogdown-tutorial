---
title: "flowLayout"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "flowlayout"
weight: 3
description: "左から右へ、上から下へ要素を配置するレイアウトです。"
---

{{< highlight r >}}
flowLayout(..., cellArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|名前無しの引数はレイアウトの子の要素になります。名前ありの引数はもっとも外側のタグのHTML属性となります。|
|**`cellArgs`**|レイアウトの各セルで用いられる追加の属性|

### 説明

左から右へ、上から下へ要素を配置するレイアウトです。要素はそれぞれ行の上側になります。このレイアウトは、パーセンテージで指定した幅を持つ要素(例えば、`plotOutput`でデフォルトの設定で`width = 100%`となっている場合)ではうまく動作しません。

### 使用例

{{< highlight r >}}
Examples
## Only run examples in interactive R sessions
if (interactive()) {

ui <- flowLayout(
  numericInput("rows", "How many rows?", 5),
  selectInput("letter", "Which letter?", LETTERS),
  sliderInput("value", "What value?", 0, 100, 50)
)
shinyApp(ui, server = function(input, output) { })
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/flowLayout.html
