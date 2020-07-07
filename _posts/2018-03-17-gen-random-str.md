---
layout: post
title: コマンドでランダムな文字列生成
date: 2018-03-17 01:18:24.000000000 +00:00
type: post
categories:
- Linux
tags:
- command
permalink: "/2018/03/gen-random-str/"
---
適当なパスワードを作るときに覚えておいたら便利そうだったのでメモ。

以下のコマンドで半角英数(大文字、小文字)10桁のパスワードを5つ生成できる。

```
cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 10 | head -5
LkJMKmqJd0
pfmQndkHSU
oQd3cxojJH
QPUjH5pVzD
2dkOA4lVOQ5
```

`tr` の詳細がイマイチわかっていないのだけど、ここでは `cat /dev/urandom` の出力を指定した文字種に置き換えている。 `cat /dev/urandom | tr -dc 'a-zA-Z0-9'` だけ打つとランダムな文字列が延々と出力されて大変なことになるので、 `fold` で折り返し、 `head` で必要な行数だけ出力している感じ。</p>

**2020-07-07 追記**

↑のコマンド、macOSの `tr` ではうまく動かないので、動くやつを調べてみた。  
`tr` の代わりに `base64` に通す。なるほど、その手があったか。

でも文字の種類指定できないのがちょっと残念。まぁcoreutilsとか入れたり、RubyやらPythonやらNode.jsやら入れてるんだからそれでなんとかすれば、っていう感じでもあるけど。

```
cat /dev/urandom | base64 | fold -w 10 | head -5
+nsRhgbnQE
TpQja3/fim
x9lMosu0oP
Q8xer3NsF1
3TyUgmAemZ
```

参考

* [コマンドラインでランダムな10文字を得る方法](https://qiita.com/tt2004d/items/0212611b6eb321ee860c)
