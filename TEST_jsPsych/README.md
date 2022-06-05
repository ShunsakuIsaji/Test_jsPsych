# README

jsPsychをテストするためのフォルダです

## 参考文献

- <https://kunisatolab.github.io/main/code_tips.html> 
- <https://ando-roid.hatenablog.com/entry/intro_psyexp_R>

## 手順

### 1.jsPsychを下記リンク先からダウンロードする
<https://github.com/jspsych/jsPsych/releases>
直でGitに入らんだろうか。。。

### 2.Rmarkdownで記述
#### YAMLヘッダー
```r
---
title: "TEST"
author: "ShunsakuIsaji"
date: '2022-06-05'
output:
 html_document:
   mathjax: null
   highlight: null
   theme: null
   css: ./jspsych/dist/jspsych.css
---
```
- インデント忘れがち（特に:の後）。注意。

#### {r}チャンク部分
```r
###```{r setup, include=FALSE}###
knitr::opts_chunk$set(echo = FALSE,message = FALSE, warning = FALSE)
###```###

###```{r}###
library(htmltools)
tagList(
  tags$script(src = './jspsych/dist/jspsych.js'),
  tags$script(src = './jspsych/dist/plugin-html-keyboard-response.js'),
)
###```###
```
- グローバルオプションはメッセージや警告をHTMLに載せない措置。
- `{r}`内は`htmltools::tags`を使ってscriptタグを設定。パス注意。

#### {js}チャンク部分
```js
/*```{js}*/
/*最初のおまじない*/
const jsPsych = initJsPsych();
/*提示する文字*/
var text = "Hello World";
/*提示する内容設定*/
const stimuli = {
 type: jsPsychHtmlKeyboardResponse,
 stimulus: text
}
/*実験開始*/
jsPsych.run([stimuli]);
/*```*/
```
- バージョンの違いによりここに苦戦。
-- `const jsPsych = initJsPsych`での初期化と、typeの指定方法が主。
- varとconstの使い分け。だいじ。
