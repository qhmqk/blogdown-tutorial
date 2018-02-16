---
title: "navlistPanel"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "navlistpanel"
weight: 3
description: "ナビゲーションリストのパネルを生成"
---

{{< highlight r >}}
navlistPanel(..., id = NULL, selected = NULL, well = TRUE, fluid = TRUE, widths = c(4, 8))
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|`navlist`に含まれる`tabPanel`要素|
|**`id`**|`NULL`以外の値を設定すると、サーバでそのときにアクティブなナビゲーションの項目を決めるために`input$id`を使えるようになります。値は`tabPanel`に渡される引数に対応します。|
|**`selected`**|デフォルトで選択されているナビゲーションリスト項目の値。値がない場合はタイトルになります。`NULL`の場合は、最初のナビゲーションが選択されます。|
|**`well`**|`TRUE`なら、ナビゲーションリストの周囲に灰色の四角の枠を置きます。|
|**`fluid`**|`TRUE`なら可変レイアウト、`FALSE`なら固定レイアウトとなります。|
|**`widths`**|2つの値をベクトルで指定。それぞれ、ナビゲーションリストの列の幅とタブの集合のコンテンツ領域に対応します。|

### 説明

左から右へ並んだタブパネルへのリンクを表示するナビゲーションリストのパネルを生成。

### 詳細

リストにプレーンテキスト要素を含めることで、`navlistPanel`にヘッダ記述が可能です。Shinyのバージョン0.11までは`"------"`のセパレータをサポートしていましたが、0.11以降はサポートしていません。これはバージョン0.11からBootstrap 3に移行して、セパレータをサポートしなくなったからです。

### 使用例

{{< highlight r >}}
fluidPage(

  titlePanel("Application Title"),

  navlistPanel(
    "Header",
    tabPanel("First"),
    tabPanel("Second"),
    tabPanel("Third")
  )
)
{{< /highlight >}}

{{< highlight html >}}
<div class="container-fluid">
  <h2>Application Title</h2>
  <div class="row">
    <div class="col-sm-4 well">
      <ul class="nav nav-pills nav-stacked" data-tabsetid="4392">
        <li class="navbar-brand">Header</li>
        <li class="active">
          <a href="#tab-4392-2" data-toggle="tab" data-value="First">First</a>
        </li>
        <li>
          <a href="#tab-4392-3" data-toggle="tab" data-value="Second">Second</a>
        </li>
        <li>
          <a href="#tab-4392-4" data-toggle="tab" data-value="Third">Third</a>
        </li>
      </ul>
    </div>
    <div class="col-sm-8">
      <div class="tab-content" data-tabsetid="4392">
        <div class="tab-pane active" data-value="First" id="tab-4392-2"></div>
        <div class="tab-pane" data-value="Second" id="tab-4392-3"></div>
        <div class="tab-pane" data-value="Third" id="tab-4392-4"></div>
      </div>
    </div>
  </div>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/navlistPanel.html
