---
title: "dateInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "dateinput"
weight: 3
description: "クリックすると日付選択できるカレンダーが表示されるテキスト入力を生成"
---

{{< highlight r >}}
dateInput(inputId, label, value = NULL, min = NULL, max = NULL, format = "yyyy-mm-dd", startview = "month", weekstart = 0, language = "en", width = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`value`**|開始日。データオブジェクト、または`yyyy-mm-dd`というフォーマットの文字列。デフォルトは`NULL`で、`NULL`ならクライアントのタイムゾーンの現在の日付となります。|
|**`min`**|最も昔の日付。データオブジェクト、または`yyyy-mm-dd`というフォーマットの文字列。|
|**`max`**|最も後の日付。データオブジェクト、または`yyyy-mm-dd`というフォーマットの文字列。|
|**`format`**|ブラウザに表示する日付のフォーマット。デフォルトは`yyyy-mm-dd`。|
|**`startview`**|最初の入力オブジェクトがクリックされたときに表示される日付の範囲。"month", "year", "decade"を指定します。デフォルトは"month"。|
|**`weekstart`**|週の最初の日を0(日曜日)～6(土曜日)の整数で指定します。|
|**`language`**|月と日の名前に使用する言語を指定します。デフォルトは"en"で英語。他に指定可能な値は、"ar", "az", "bg", "bs", "ca", "cs", "cy", "da", "de", "el", "en-AU", "en-GB", "eo", "es", "et", "eu", "fa", "fi", "fo", "fr-CH", "fr", "gl", "he", "hr", "hu", "hy", "id", "is", "it-CH", "it", "ja", "ka", "kh", "kk", "ko", "kr", "lt", "lv", "me", "mk", "mn", "ms", "nb", "nl-BE", "nl", "no", "pl", "pt-BR", "pt", "ro", "rs-latin", "rs", "ru", "sk", "sl", "sq", "sr-latin", "sr", "sv", "sw", "th", "tr", "uk", "vi", "zh-CN", "zh-TW"。|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細は`validateCssUnit`を参照|

### 説明

クリックすると日付選択できるカレンダーが表示されるテキスト入力を生成。

### 詳細

日付の`format`文字列のデフォルトは`yyyy-mm-dd`ですが、以下の表の値が使用可能です。

|値(文字列)|説明|
|:--|:--|
|`yy`|世紀の部分がない西暦。2018年なら18となります。|
|`yyyy`|世紀ありの西暦。2018年ならそのまま2018となります。|
|`mm`|01から12までの2桁の月の数字を表示します。|
|`m`|1桁の場合の0なしの1から12までの2桁の月の数字を表示します。|
|`M`|月の名前の短縮を表示します。|
|`MM`|月の名前を短縮せずに表示します。|
|`dd`|2桁目のゼロを付けた日|
|`d`|2桁目のゼロなしの日|
|`D`|省略した曜日の名前|
|`DD`|曜日のフルネーム|

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {
ui <- fluidPage(
  dateInput("date1", "Date:", value = "2012-02-29"),
  # Default value is the date in client's time zone
  dateInput("date2", "Date:"),
  # value is always yyyy-mm-dd, even if the display format is different
  dateInput("date3", "Date:", value = "2012-02-29", format = "mm/dd/yy"),
  # Pass in a Date object
  dateInput("date4", "Date:", value = Sys.Date()-10),
  # Use different language and different first day of week
  dateInput("date5", "Date:",
          language = "ru",
          weekstart = 1),
  # Start with decade view instead of default month view
  dateInput("date6", "Date:",
            startview = "decade")
)
shinyApp(ui, server = function(input, output) { })
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/latest/dateInput.html



