---
title: "navbarPage"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "navbarpage"
weight: 3
description: "上部にナビゲーションバーのあるページを生成"
---

{{< highlight r >}}
navbarPage(title, ..., id = NULL, selected = NULL,
  position = c("static-top", "fixed-top", "fixed-bottom"), header = NULL,
  footer = NULL, inverse = FALSE, collapsible = FALSE, collapsable,
  fluid = TRUE, responsive = NULL, theme = NULL, windowTitle = title)
{{< /highlight >}}

{{< highlight r >}}
navbarMenu(title, ..., menuName = title, icon = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`title`**|ナビゲーションバーの中に表示するタイトル|
|**`...`**|ページに含まれる`tabPanel`要素。`navbarMenu`関数はメニューセクションのヘッダとして用いられる文字列も受け付けます。文字列が`"----"`のようなダッシュの集合の場合、メニューに水平のセパレータが表示されます。|
|**`id`**|指定すると、サーバでどのタブが有効かどうかを決定するために`input$id`を使用できるようになります。`tabPanel`に渡される値の引数に対応します。|
|**`selected`**|デフォルトで選択されているタブの値。指定しない場合はタイトルになります。NULLの場合は最初のタブが選択されます。|
|**`position`**|標準のスクロール("static-top")または上部に固定("fixed-top")、下側に固定("fixed-bottom")のいずれかでページの上部にナビゲーションバーが表示を決定。"fixed-top"と"fixed-bottom"は、ナビゲーションバーがコンテンツ本体に重なる場合があることに注意してください。スペースを挿入するためのpaddingを指定する場合、例えば`tags$style(type="text/css", "body {padding-top: 70px;}")`のような記述を追加します。|
|**`header`**|すべてのタブパネル上の共通のヘッダとして表示するタグまたはタグのリスト|
|**`footer`**|すべてのタブパネル下の共通のフッタとして表示するタグまたはタグのリスト|
|**`inverse`**|`TRUE`ならナビゲーションバーに暗い背景と明るいテキストを表示します。|
|**`collapsible`**|`TRUE`ならブラウザの幅が940ピクセル以下のときにナビゲーション要素をメニューに畳み込みます。スマホなどのより小さいタッチスクリーンのデバイスで見るときに有用です。|
|**`collapsable`**|使用は推奨されません。代わりに`collapsible`を使用します。|
|**`fluid`**|`TRUE`なら可変レイアウト、`FALSE`なら固定レイアウトとなります。|
|**`responsive`**|このオプションは推奨されません。Bootstrap 3ではオプションにないからです。|
|**`theme`**|Bootstrapのスタイルシートを指定します。通常CSSファイルはwwwディレクトリ内に置きます。例えば、www/bootstrap.cssのテーマを使用するには、`theme = "bootstrap.css"`を記述します。|
|**`windowTitle`**|ブラウザウィンドウに表示されるタイトル。タイトルが文字列でない場合に有用です。|
|**`menuName`**|`navbarMenu`を指定する名前。`navbarMenu`を挿入・削除または表示・非表示切り替えしたい場合に必要となります。|
|**`icon`**|`navbarMenu`のタブ上に現れるオプションのアイコン|

### 値

`shinyUI`関数に渡されるUI定義

### 説明

上部に`tabPanel`要素の集合を切り替えるためのナビゲーションバーを持つページを生成

### 詳細

`navbarMenu`関数は、以下の例のように、追加の`tabPanel`を含むナビゲーションバー内に組み込んだメニューを生成することに用いられます。

### 使用例

{{< highlight r >}}
navbarPage("App Title",
  tabPanel("Plot"),
  tabPanel("Summary"),
  tabPanel("Table")
)
{{< /highlight >}}

{{< highlight html >}}
<nav class="navbar navbar-default navbar-static-top" role="navigation">
  <div class="container-fluid">
    <div class="navbar-header">
      <span class="navbar-brand">App Title</span>
    </div>
    <ul class="nav navbar-nav" data-tabsetid="8029">
      <li class="active">
        <a href="#tab-8029-1" data-toggle="tab" data-value="Plot">Plot</a>
      </li>
      <li>
        <a href="#tab-8029-2" data-toggle="tab" data-value="Summary">Summary</a>
      </li>
      <li>
        <a href="#tab-8029-3" data-toggle="tab" data-value="Table">Table</a>
      </li>
    </ul>
  </div>
</nav>
<div class="container-fluid">
  <div class="tab-content" data-tabsetid="8029">
    <div class="tab-pane active" data-value="Plot" id="tab-8029-1"></div>
    <div class="tab-pane" data-value="Summary" id="tab-8029-2"></div>
    <div class="tab-pane" data-value="Table" id="tab-8029-3"></div>
  </div>
</div>
{{< /highlight >}}

{{< highlight r >}}
navbarPage("App Title",
  tabPanel("Plot"),
  navbarMenu("More",
    tabPanel("Summary"),
    "----",
    "Section header",
    tabPanel("Table")
  )
)
{{< /highlight >}}

{{< highlight html >}}
<nav class="navbar navbar-default navbar-static-top" role="navigation">
  <div class="container-fluid">
    <div class="navbar-header">
      <span class="navbar-brand">App Title</span>
    </div>
    <ul class="nav navbar-nav" data-tabsetid="7742">
      <li class="active">
        <a href="#tab-7742-1" data-toggle="tab" data-value="Plot">Plot</a>
      </li>
      <li class="dropdown">
        <a href="#" class="dropdown-toggle" data-toggle="dropdown" data-value="More">
          More
          <b class="caret"></b>
        </a>
        <ul class="dropdown-menu" data-tabsetid="8562">
          <li>
            <a href="#tab-8562-1" data-toggle="tab" data-value="Summary">Summary</a>
          </li>
          <li class="divider"></li>
          <li class="dropdown-header">Section header</li>
          <li>
            <a href="#tab-8562-4" data-toggle="tab" data-value="Table">Table</a>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</nav>
<div class="container-fluid">
  <div class="tab-content" data-tabsetid="7742">
    <div class="tab-pane active" data-value="Plot" id="tab-7742-1"></div>
    <div class="tab-pane" data-value="Summary" id="tab-8562-1"></div>
    <div class="tab-pane" data-value="Table" id="tab-8562-4"></div>
  </div>
</div>
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/navbarPage.html
