---
title: "tabPanel"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "tabpanel"
weight: 3
description: "タブパネルを生成"
---

{{< highlight r >}}
tabPanel(title, ..., value = title, icon = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`title`**|タブに表示するタイトル|
|**`...`**|タブ内に含まれるUI要素|
|**`value`**|`tabsetPanel`でこのタブが選択されたときに送られる値。`value`の設定なしで、`tabsetPane`が`id`を保つ場合、`title`が使用されます。|
|**`icon`**|タブ上にオプションで表示するアイコン。この属性は、`navbarPage`内で`tabPanel`を用いているときのみ有効です。|

### 値

`tabsetPanel`に渡されるタブ。

### 説明

`tabsetPanel`内に含まれるタブパネルを生成。

### 使用例

{{< highlight r >}}
# Show a tabset that includes a plot, summary, and
# table view of the generated distribution
mainPanel(
  tabsetPanel(
    tabPanel("Plot", plotOutput("plot")),
    tabPanel("Summary", verbatimTextOutput("summary")),
    tabPanel("Table", tableOutput("table"))
  )
)
{{< /highlight >}}

{{< highlight html >}}
<div class="col-sm-8">
  <div class="tabbable">
    <ul class="nav nav-tabs" data-tabsetid="8523">
      <li class="active">
        <a href="#tab-8523-1" data-toggle="tab" data-value="Plot">Plot</a>
      </li>
      <li>
        <a href="#tab-8523-2" data-toggle="tab" data-value="Summary">Summary</a>
      </li>
      <li>
        <a href="#tab-8523-3" data-toggle="tab" data-value="Table">Table</a>
      </li>
    </ul>
    <div class="tab-content" data-tabsetid="8523">
      <div class="tab-pane active" data-value="Plot" id="tab-8523-1">
        <div id="plot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
      </div>
      <div class="tab-pane" data-value="Summary" id="tab-8523-2">
        <pre id="summary" class="shiny-text-output noplaceholder"></pre>
      </div>
      <div class="tab-pane" data-value="Table" id="tab-8523-3">
        <div id="table" class="shiny-html-output"></div>
      </div>
    </div>
  </div>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/tabPanel.html
