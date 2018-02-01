---
title: "htmlOutput"
author: "qhmqk"
date: 2018-02-01
categories: ["Shiny"]
tags: ["UI Outputs"]
slug: "htmloutput"
weight: 3
description: "HTMLを出力"
---

{{< highlight r >}}
htmlOutput(outputId, inline = FALSE, container = if (inline) span else div, ...)
{{< /highlight >}}


### 引数

|名前|説明|
|:--|:--|
|**`outputId`**|値を読み込む出力変数|
|**`container`**|テキストを含むHTML要素を生成するための関数|
|**`inline`**|インライン(`span()`)またはブロックコンテナ(`div()`)を出力で使用するかどうかを論理値で指定|
|**`...`**|`container`のタグ関数に渡す引数。タグで追加のクラスを使うときに有用です。|

### 値

パネル内に含まれるHTML出力要素

### 説明

アプリケーションのページ内に、HTMLとしてリアクティブな出力変数をレンダリングします。テキストは、HTMLのdivタグ内に含まれ、エスケープされないHTMLコンテンツを含むことを仮定しています。

### 詳細

`uiOutput`はサーバ側の`renderUI`での使用を目的としています。現在は`htmlOutput`のエイリアスです。

### 使用例

{{< highlight r >}}
htmlOutput("summary")

<div id="summary" class="shiny-html-output"></div>


# Using a custom container and class
tags$ul(
  htmlOutput("summary", container = tags$li, class = "custom-li-output")
)

<ul>
  <li class="shiny-html-output custom-li-output" id="summary"></li>
</ul>
{{< /highlight >}}