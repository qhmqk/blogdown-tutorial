---
title: "textOutput"
author: "qhmqk"
date: 2018-02-01
categories: ["Shiny"]
tags: ["UI Outputs"]
slug: "textoutput"
weight: 3
description: "テキストを出力"
---


{{< highlight r >}}
textOutput(outputId, container = if (inline) span else div, inline = FALSE)
{{< /highlight >}}


### 引数

|名前|説明|
|:--|:--|
|**`outputId`**|表を読み込む出力変数|
|**`container`**|テキストを含むHTML要素を生成するための関数|
|**`inline`**|インライン(`span()`)またはブロックコンテナ(`div()`)を出力で使用するかどうかを論理値で指定|

### 値

パネル内に含まれるテキスト出力要素

### 説明

アプリケーション内でテキストとしてリアクティブな出力変数をレンダリングします。テキストは、デフォルトで、HTMLのdivタグ内に含まれます。

### 詳細

テキストは、レンダリングに優先してHTMLをエスケープします。この要素は`renderText`出力変数で使用されます。

### 使用例

{{< highlight r >}}
h3(textOutput("caption"))

<h3>
  <div id="caption" class="shiny-text-output"></div>
</h3>
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/textOutput.html