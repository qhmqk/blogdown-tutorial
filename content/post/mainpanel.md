---
title: "mainPanel"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "mainpanel"
weight: 3
description: "`sidebarLayout`に渡される出力要素を持つメインパネルを生成"
---

{{< highlight r >}}
mainPanel(..., width = 8)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|メインパネルに含まれるUI要素|
|**`width`**|メインパネルの幅。可変レイアウトでは、合計で12となる広さの単位があります(例えば8を指定すると、残りの4がサイドバーの幅となり、1:2の比率で表示されます)。固定レイアウトでは、メインパネルの幅をどのように設定しても、親の列の幅となります。|

### 値

`sidebarLayout`に渡されるメインパネル

### 説明

`sidebarLayout`に渡される出力要素を持つメインパネルを生成

{{< highlight r >}}
# Show the caption and plot of the requested variable against mpg
mainPanel(
   h3(textOutput("caption")),
   plotOutput("mpgPlot")
)
{{< /highlight >}}

{{< highlight html >}}
<div class="col-sm-8">
  <h3>
    <div id="caption" class="shiny-text-output"></div>
  </h3>
  <div id="mpgPlot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/mainPanel.html
