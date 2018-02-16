---
title: "tabsetPanel"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "tabsetpanel"
weight: 3
description: "タブの集合パネルを生成"
---

{{< highlight r >}}
tabsetPanel(..., id = NULL, selected = NULL, type = c("tabs", "pills"), position = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|タブの集合に含まれる`tabPanel`要素|
|**`id`**|`NULL`以外の値を設定すると、サーバでそのときにアクティブなタブを決めるために`input$id`を使えるようになります。値は`tabPanel`に渡される引数に対応します。|
|**`selected`**|デフォルトで選択されているタブの値。値がない場合はタイトルになります。`NULL`の場合は、最初のタブが選択されます。|
|**`type`**|"tabs"を指定数と標準的なタブになります。"pills"を指定するとタブが背景色で塗りつぶされた見た目になります。|
|**`position`**|この引数は推奨されません。Bootstrap 3で廃止された機能を使用しているからです。|

### 値

`mainPanel`に渡されるタブの集合。

### 説明

`tabPanel`要素を持つタブの集合を生成します。タブの集合は、複数の独立した閲覧可能なセクションに出力を分割するのに有用です。

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
    <ul class="nav nav-tabs" data-tabsetid="5915">
      <li class="active">
        <a href="#tab-5915-1" data-toggle="tab" data-value="Plot">Plot</a>
      </li>
      <li>
        <a href="#tab-5915-2" data-toggle="tab" data-value="Summary">Summary</a>
      </li>
      <li>
        <a href="#tab-5915-3" data-toggle="tab" data-value="Table">Table</a>
      </li>
    </ul>
    <div class="tab-content" data-tabsetid="5915">
      <div class="tab-pane active" data-value="Plot" id="tab-5915-1">
        <div id="plot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
      </div>
      <div class="tab-pane" data-value="Summary" id="tab-5915-2">
        <pre id="summary" class="shiny-text-output noplaceholder"></pre>
      </div>
      <div class="tab-pane" data-value="Table" id="tab-5915-3">
        <div id="table" class="shiny-html-output"></div>
      </div>
    </div>
  </div>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/tabsetPanel.html
