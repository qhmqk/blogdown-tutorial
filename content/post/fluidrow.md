---
title: "fluidRow"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "fluidrow"
weight: 3
description: "左から右へ、上から下へ要素を配置するレイアウトです。"
---

{{< highlight r >}}
fluidRow(...)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|ページ内の要素|

### 値

`shinyUI`関数に渡されるUI定義

### 説明

可変ページレイアウトを生成する関数です。可変ページレイアウトは、行と行に順番に含まれる列から構成されます。行は要素が(ブラウザに十分な幅があるなら)同じ行に現れるようにする目的で存在します。列は水平に12分割したグリッドで要素がどれだけを占めるのかを定義する目的で存在します。可変ページは利用可能なブラウザの幅すべてを埋めるためにリアルタイムで拡大縮小します。

### 詳細

可変ページの生成には、`fluidPage`関数を用いて、`fluidRow`とその中の`column`のインスタンスを同梱します。低級な行と列関数の代わりとして、`sidebarLayout`のような高級レイアウト関数を使用可能です。

### 注記

可変ページにレイアウトするときのさらなる詳細は、Shiny-Applicatin-Layout-Guideを参照してください。

### 使用例

{{< highlight r >}}
# UI demonstrating column layouts
ui <- fluidPage(
  title = "Hello Shiny!",
  fluidRow(
    column(width = 4,
      "4"
    ),
    column(width = 3, offset = 2,
      "3 offset 2"
    )
  )
)

shinyApp(ui, server = function(input, output) { })
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/fluidPage.html
