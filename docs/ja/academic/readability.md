# 可読性

良い文章というものには様々な側面があります。簡潔な内容だけでなく、長い文と短い文がバランスよく含まれていることも必要です。さらに、複雑で難しい単語を使いすぎないようにする必要もあります。そして、段落が長くなりすぎないこと、能動態を使うこと、各段落を状況に応じて構成することも大切です。

文章というものが開発されて以来、人類の創造力により、良い文章を書くコツが生み出されてきました。Zettlrが完璧なライティング環境を提供してくれるので、文章の判別性(legibility)は非常に良いですが、可読性(readability)についても注意を向ける必要があります。幸いにも、Zettlrでは**可読性モード**が利用できます。

> 可読性スコアは読みやすさを判断するための指標の一つに過ぎないので、あまり真剣に受け止めないでください。可読性アルゴリズムにより文章が真っ赤にハイライトされたとしても、その文章を書き直す必要はありません。むしろ、アルゴリズムでは考慮されない文のコンテキストを見て、良し悪しを判断してください。**最初は可読性モードをオフにして文章を書くことを推奨します。後から、読みにくいかもしれないと思った部分を確認するときだけオンにしてください。**

## 可読性モードの機能

一言で説明するなら、可読性モードとは、各文の基本的なスコアを計算して文章の可読性を判定する手がかりを与える、CodeMirrorのシンタックスハイライトモードの一つです。可読性モードでは、各文を緑から赤の間の色でハイライトします。緑はその文が理解しやすいことを、赤はその文が理解しにくいことを表しています。

可読性モードでは4つの異なるアルゴリズムが利用できます。[Dale-Chall readability formula](https://en.wikipedia.org/wiki/Dale%E2%80%93Chall_readability_formula)、[Gunning-Fog index](https://en.wikipedia.org/wiki/Gunning_fog_index)、[Coleman-Liau index](https://en.wikipedia.org/wiki/Coleman%E2%80%93Liau_index)、[Automated Readability index](http://www.readabilityformulas.com/automated-readability-index.php)の4つです。

> Note that all of the implemented readability algorithms have been designed with English in mind. Zettlr attempts to make them work with other languages as well using newer research, but the algorithms will still be biased towards English. Non-western scripts such as Korean, Chinese, or Japanese, don't work with these scores. If you know of readability algorithms that do work with other scripts, please notify us so we can make Zettlr more universal in this regard!

## Dale-Chall Readability Formula

Dale-Challの式は、教育研究の黎明期にEdgar DaleとJeanne Challによって作られました。その目的は、学校の生徒が使うテキストの可読性を判定する指標を提供することでした。アメリカの第4学年の生徒が容易に理解できる3,000語のリストを使い、およそ0から10の間のスコアを算出します。その値は大雑把に説明すると、文章を理解するのに必要な教育年数になっています。つまり、スコア10の文章を理解するには大学卒業レベルが必要で、スコア1だと初心者でも理解できるということです。

> 幅広い読者に向けた文章を書いている場合はDale-Challを使ってください。なぜなら、このアルゴリズムは短くて簡潔な文章に高評価を与えますが、文章を不自然なほど短くするように仕向けることがないからです。

## Gunning-Fog index

Gunning-Fogはタブロイド紙の黎明期に生み出されました。1952年、Robert Gunningは自社で出版する書籍と新聞についての測定方法を探していました。そこでGunning-Fogは、対象の文章を理解するのに必要な正規教育の年数と相関するスコアとなっています。しかし、彼はビジネスマンであるため出版物を幅広い層に読んでもらうことを意図していました。Gunningのアルゴリズムは比較的簡単に理解できる文章に対しても高い難易度を示します。他のアルゴリズムと使い比べてみると、Gunning-Fogは何もかも濃い赤色で塗りつぶす傾向にあることに気づくでしょう。

> 短い宣伝用の文章(Webサイト用など)を作っている場合は、Gunning-Fogを使ってください。このような文章の場合、それを読もうとする基本的なインセンティブが存在しないと仮定すべきでしょう。

## Coleman/Liau index

コンピュータの価格の低下により、コンピュータを使った統計処理で大量のデータから意味のある測定値を取り出すことが一般的な選択肢になりました。Coleman/Liau-indexは、このような時代に作られた、音節数や「難しい単語」のリストなどに頼らないアルゴリズムです。それゆえ、ZettlrにおけるColeman/Liau-indexの実装は非常に正確です。他のアルゴリズムと同様に、スコアの値は文章を理解するために必要な正規教育の年数とおよそ等しくなります。加えて、Coleman/Liauは妥当な結果を算出し、必ずしも短い文を書くことを強制しません。

> あらゆる文章で正確な可読性の指標を必要としている場合はColeman/Liauを使ってください。一単語だけの文ではうまく機能しませんが、理解するのが難しいテキストに対しても妥当なスコアを与えてくれます。

## Automated Readability Index (ARI)

Automated Readability Indexは、Coleman/Liauの流れを汲み、シンプルな統計解析に基づいて可読性スコアを算出する式です。これが最も「緩い」アルゴリズムであり、赤いハイライトで大半のテキストを書き直すように促すようなことはありません。

> 学術論文のような要求の厳しいテキストを書いている場合はAutomated Readability Indexを使ってください。なぜなら、このアルゴリズムは難しい文に対しても比較的良いスコアをあたえるからです。

## 「難しい単語」について

Zettlrの実装では、Dale-Challで必要となるような、理解しやすい単語のリストを使っていません。その代わりに別のアプローチをとっています。理解しやすい単語というのは時と共に変化し、そして当然言語によって異なるものです。Zettlrでは、単語の難しさを測るために他の指標を取り入れました。それは、単語長の分散です。

Zettlrでは、単語の長さが平均値よりも標準偏差の2倍以上長いものを難しい単語と定義しました。ColemanとLiauが1975年に『A Computer Readability Formula Designed for Machine Scoring』で指摘したように、単語の音節数よりも長さの方が難しさを表すのにより適した指標です。これで、このアルゴリズムは英語以外の西洋の言語でも使うことができます。アルゴリズムに関する説明は、[可読性機能の説明ページ](https://zettlr.com/readability)をご覧ください。

さらに、Zettlrではアルゴリズムにもう一つ変更を加えています。4つのアルゴリズムはいずれも、テキスト全体に対して適用するものとして考案されていますが、可読性モードでは1文ごとに適用します。それゆえ、元の文脈とは離れたものになってしまいます。大まかに言えば、文の難しさを近似した値となりますが、明らかに文脈中で理解しにくい文が緑色になったり、文脈に沿った文が赤くなったりすることがあります。
