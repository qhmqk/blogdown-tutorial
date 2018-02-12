---
title: "sidebarPanel"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "sidebarpanel"
weight: 3
description: "`sidebarLayout`に渡される入力コントロールを含むサイドバーのパネルを生成"
---

{{< highlight r >}}
sidebarPanel(..., width = 4)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|サイドバーに含まれるUI要素|
|**`width`**|サイドバーの幅。可変レイアウトでは、合計で12となる広さの単位があります(例えば4を指定すると、残りの8がメインパネルの幅となり、1:2の比率で表示されます)。固定レイアウトでは、サイドバーの幅をどのように設定しても、親の列の幅となります。|

### 値

`sidebarLayout`に渡されるサイドバー。

### 説明

`sidebarLayout`に渡される入力コントロールを含むサイドバーのパネルを生成

### 使用例

{{< highlight r >}}
# Sidebar with controls to select a dataset and specify
# the number of observations to view
sidebarPanel(
  selectInput("dataset", "Choose a dataset:",
              choices = c("rock", "pressure", "cars")),

  numericInput("obs", "Observations:", 10)
)
{{< /highlight >}}

{{< highlight html >}}
<div class="col-sm-4">
  <form class="well">
    <div class="form-group shiny-input-container">
      <label class="control-label" for="dataset">Choose a dataset:</label>
      <div>
        <select id="dataset"><option value="rock" selected>rock</option>
<option value="pressure">pressure</option>
<option value="cars">cars</option></select>
        <script type="application/json" data-for="dataset" data-nonempty="">{}</script>
      </div>
    </div>
    <div class="form-group shiny-input-container">
      <label for="obs">Observations:</label>
      <input id="obs" type="number" class="form-control" value="10"/>
    </div>
  </form>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/sidebarPanel.html
