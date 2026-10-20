# この翻訳版について

## 目的

[The Clojure Style Guide][1] の日本語翻訳は Toshiki Takeuchi 氏により[Clojureスタイルガイド][2]として作成されており、正式にローカライズ版として紹介されています。
しかしながら更新は 2020 年で止まっており、以降はプルリクエストの対応もされていないようです。
一方で原文は 2026 年現在でも更新されていて、翻訳版と比べると事例が多く追加されているほか、ごく一部ですが良い/悪いといった評価基準が変更されています。

最新の原文に追従することを目的とし、翻訳版を更新しました。

## ゴール

主な目標は下記の 2 点です。

- ガイドラインは原文の最新版を反映した内容に更新
- CI/CD 環境の再整備 (CircleCI 連携から GitHub Actions に変更)

## 作業結果

主目標は完了しています。

なお、今回の翻訳版について今後の維持については未定です。
Clojure に詳しい方／情熱を持っている方に引き取っていただき、改善・維持していただければ幸いです。

## 成果物

### スタイルガイド

- README.adoc （日本語翻訳版、AsciiDoc 形式）
- README-docinfo.html（AsciiDoctor による HTML 変換時の CSS 追加設定）

### CI/CD環境

- .github/workflows/deploy.yml （GitHub Pages 公開用ワークフロー）
- Gemfile (上記ワークフローにて環境構築に使用)

ただし名前とは裏腹に、ワークフローは手動実行にしてあります。continuous (継続的)ではありません。

### リポジトリ

GitHub 上でフォークせず手元にクローンして変更しました。
参照用に[原文リポジトリ][1]をサブモジュールとして登録するとともに、原文リポジトリのコミット ID をコミットログ並びに本文に記載して翻訳状況を明確にしました。

## 翻訳内容

今回の翻訳者は[プログラミングClojure 第2版][3]はおろか、日本語・英語を問わず Clojure 関連の書籍を一切所有していません。Clojure についても初心者と同然です。
更新元とした[日本語翻訳][2]の内容を引き継いだ箇所はともかく、あらたに記述した範囲についての翻訳品質はかなり怪しいと考えてください。
そのため元の翻訳版の前置きで記載されていた翻訳版の扱いなどについては大幅に変更しています。

### 既存の翻訳版との関係

大部分を流用しましたが、以下のような場合は変更を加えました。

- [原本][1]の記述が変化した箇所
- 訳を変更した方が適切だと判断した箇所
- 外来語の長音表記

また、意図せず変更してしまった箇所があるかもしれません。

ライセンスに従って改変したものなので、今回の翻訳版の内容については[元の日本語翻訳][2]には問い合わせないようお願いします。

### 文体について

ガイドラインの規則や TIP として助言している箇所は、一部を除き常体（だ・である調）で記述しています。
一方で、NOTE として注意事項を説明している箇所、脚注、スタイルガイドそのものについて言及している箇所は敬体（です・ます調）にしました。

本文中に挿入される NOTE は周囲と文体が異なりますが、偉そうに注意するのは肌に合わないため敬体にしています。

### 事例の評価

スタイルガイドで事例として挙げられている内容の多くに、良い・悪いといった評価が添えられています。
英語表現との対応は以下のようにしており、後ろに行くほど悪い評価です。

- best: 最も良い
- much better: ずっと良い
- better: より良い
- good: 良い
- ok: 大丈夫
- okay: まあ大丈夫
- okish, ok-ish: まあまあ
- not as good: あまり良くない
- bad: 悪い
- very bad: 非常に悪い

### コメンタリー

AsciiDoc で footnote の種類分けが難しそうなので、こちらに記述します。
主に[翻訳版][2]からの変更についての言及です。

#### はじめに (Introduction)

3 つのセクションが新規追加されている。

 - 基本理念(Guiding Principles)
 - 一貫性に関する注意事項(A Note About Consistency)
 - 翻訳版(Translations)

翻訳版セクションは既存のリストをセクション化しただけで中身はほとんど変わりません。

元の翻訳版で「規約」という用語がガイドラインが示す個々のルールや規則を表す表現として使われていましたが、
「規約」で思い浮かぶのはサービスの利用規約とか組織の規約、学会とかで定めた命名規約など規則の集まりであり、
どうにもしっくりと来なかったためルールや規則などの用語に置き換えました。

#### ソースコードのレイアウトと構造 (Source Code Layout & Organization)

セマンティック・インデントに関する話題が追加されている。適切な訳語が浮かばないので、そのままカタカナに。

セマンティック・インデントについては、Lisp、それもマクロに馴染みがないと何を主張しているのか理解が難しいかもしれません。
Common Lisp における `defmacro` の `&rest` と `&body` の両キーワードについて、`&body` の使用目的と言えばわかりやすいでしょうか。
要するに、マクロ定義の引数に `& body` などを使うことでマクロがボディフォームを持っていると推測できたり、
それ用に追加されたメタデータがあれば、通常の関数とは別のルールでインデントするというだけの話です。
原著者の[記事][4]ではもう少し詳しく書かれています。

#### 名前空間の宣言 (Namespace Declaration)

declaration なので、「定義」から「宣言」に変更しました。

「包括的な ns フォーム」の説明については、ns マクロのドキュメント文字列を参照する方がわかりやすいと思われる。

名前空間エイリアスについての記述が追加されている。
「慣用的な名前空間エイリアスを使う」の TIP に「`clojure.core.str`を隠蔽しているように」とあるが、正しくは「`clojure.core/str`」ではないだろうか。
また、コミュニティライブラリのエイリアスについては、やむなく訳注を入れました。判断は読む人にお任せします。

#### 命名規則 (Naming)

例の追加がほとんどで、大きな変更はなし。

「Dynamic な Var」で var の定義に :dynamic メタデータを付けて再束縛可能にしているが、システムがあらかじめ用意した再束縛可能な var には :dynamic メタデータが付いていないものがある。つまり :dynamic メタデータの有無で再束縛可能か否かは判断できない。そのような var でも名前は earmuffs 付きなので、使う分には特に問題はない。

#### 関数 (Functions)

ほとんど変更はなし。

「1行の関数」を複数アリティの説明の後に持ってきた方が、説明の流れが良い気がする。

#### 慣用的な構文 (Idioms)

翻訳版では "Idioms" の訳語が「構文」になっていましたが、構文だけでは意味がわからないので「慣用的な構文」に変更しました。カタカナで「イディオム」の方が良かったかもしれません。

一箇所を除いて少しの追加程度で大きな変更はなし。

問題の箇所は「無名関数 vs complement, comp, partial」で、[原文][1]は[このコミット][5]でスタイルの評価を変更した。
その結果、従来とは評価がひっくり返り、元の[翻訳版][2]は今ではやや不適切とされているスタイルを推奨している。
今回、既存の翻訳版に手を入れようと思ったきっかけの一つです。

「プライベートな var へのアクセス」で @#'some.ns/var と例示しているが、これは @ (deref) と #' (var-quote) の組み合わせ。

#### データ構造 (Data Structures)

例や記述の追加がほとんどで、大きな変更はなし。

「マップから値を取得する関数としてのキーワード」はマップのキーがキーワードの場合の話をしている。
キーが非キーワードの場合、`("key" m)` のような書き方はできないので実行時例外を避けて安全側に倒すとしたら `(get m "key")` の一択か。

```clojure
user=> (def directions-keyword {:north 0, :east 1, :south 2, :west 3})
#'user/directions-keyword
user=>
user=> (directions-keyword :north)
0
user=> (:north directions-keyword)
0
user=> (directions-keyword :foo)
nil
```

```clojure
user=> (def directions-str {"north" 0, "east" 1, "south" 2, "west" 3})
#'user/directions-str
user=>
user=> (directions-str "north")
0
user=> ("north" directions-str)
Execution error (ClassCastException) at user/eval13 (REPL:1).
class java.lang.String cannot be cast to class clojure.lang.IFn (java.lang.String is in module java.base of loader 'bootstrap'; clojure.lang.IFn is in unnamed module of loader 'app')
user=> (directions-str "foo")
nil
```

```clojure
user=> (def bad-lookup-map nil)
#'user/bad-lookup-map
user=>
user=> (bad-lookup-map :key)
Execution error (NullPointerException) at user/eval15 (REPL:1).
Cannot invoke "clojure.lang.IFn.invoke(Object)" because the return value of "clojure.lang.Var.getRawRoot()" is null
user=> (:key bad-lookup-map)
nil
user=>
user=> (bad-lookup-map "key")
Execution error (NullPointerException) at user/eval19 (REPL:1).
Cannot invoke "clojure.lang.IFn.invoke(Object)" because the return value of "clojure.lang.Var.getRawRoot()" is null
user=> ("key" bad-lookup-map)
Execution error (ClassCastException) at user/eval21 (REPL:1).
class java.lang.String cannot be cast to class clojure.lang.IFn (java.lang.String is in module java.base of loader 'bootstrap'; clojure.lang.IFn is in unnamed module of loader 'app')
user=>
user=> (get bad-lookup-map :key)
nil
user=> (get bad-lookup-map "key")
nil
```

#### タイプとレコード (Types & Records)

ほとんど変化がなかったと思う。

#### 状態の変更 (Mutation)

"Mutation" の訳語が「状態」になっていましたが、状態だけでは意味がわからないので「状態の変更」としました。

記述と例の追加がいくつか。大きな変更はなし。

「トランザクショナル参照(Ref)」は原文では「Refs」だが io! マクロの話も扱っており、
表題は「トランザクション」もしくは「トランザクションと参照」の方がセクションの内容に沿っている気がする。

「同一Refに対する長短期トランザクションの混在を避ける」の話題は、おそらく Clojure が
Multiversion Concurrency Control (MVCC) なトランザクション処理をしているからだと思われる（裏はとっていません）。

#### 数学 (Math)

新規追加。`clojure.math` を使え、以上。

説明で触れていない点として、これらのラッパー関数は可能ならインライン展開されるが、高階関数へのパラメーターとして使われるなどインライン展開できない場合は通常の関数定義が使われる。

#### 文字列 (Strings)

注意書きの追加のみ。

#### 例外 (Exceptions)

例が追加されている他に、Throwable クラスのキャッチについて説明が追加されている。

#### マクロ (Macros)

説明の詳細化と例の追加。新規の項目はなし。

#### 一般的なメタデータ (Common Metadata)

まるごと新規追加。つまり翻訳品質が一番疑わしい箇所なので、眉に唾をつけて読んでください。

「:superseded-by」の例は、あまり良くない気がする。Clojure は Lisp-1 なので変数名と関数名は同じ名前空間で管理されるが、ここでの例は `def` と `defn` の両方で同じ `foo` が使われている。単に例が並んでいるだけと読み取れれば良いが、他の名前を参照するメタデータの例だけに、異なる名前にしておいた方が余計な誤解を招かずにすむと思う。

#### コメント (Comments)

例の追加がほとんど。大きな変更はなし。

#### ドキュメント (Documentation)

ここは変更がなかったと思う。

#### テスト (Testing)

大幅に項目が追加されている。翻訳眉唾案件その2。

間違ってはいないが、混乱しそうなのがマップ型データに対するテストとして挙げられている `match?`。
ここで示されている例は [malli][6] による型バリデーションを組み合わせているようで、[matcher-combinators][7] だけ見ても理解が難しいと思われる。

#### ライブラリの構成 (Library Organization)

ここは変更がなかったと思う。

#### 実際のコードでは (Existential)

同じく変更がなかったと思う。

#### ツール (Tools)

コードフォーマッターについて追加されている。

#### 残りの部分

歴史とか編集チームなど、スタイルガイドについての説明が拡充されている。翻訳眉唾案件その3。


## その他

Clojure の話題からは逸れますが、記録しておきたい事項についての備忘録。

### セクション ID

AsciiDoctor による HTML 変換時、各セクションには ID が振られて目次からのリンクに使われています。
この ID は特に指定しない限りはセクションのタイトルから自動生成されます。

[原文][1]では明示的な指定があったりなかったりしていますが、これをこのまま翻訳版に持ってくると ID に英語と日本語が入り混じります。
HTML5 の仕様として日本語でも全く問題はないのですが、混在は URL の見た目が少々悪いので原文の HTML 版から ID を拾ってきて明示的に指定しています。
手作業が入っているので、ID の文言がタイトルの内容と一致していない箇所が混入している可能性があります。

### 見た目の改善

突き詰めると大変な労力が必要なので、手軽にできる範囲に限定しました。

#### テーブル

[原文][1]では column 数の指定だけで、その結果、見た目がのっぺりとして 1990 年代半ばに素人が HTML 直打ちして作ったようなテーブルになっていました。
そこで AsciiDoctor の機能でヘッダー行の分離ならびにカラム幅を調整しました。

#### 表意文字と非表意文字の間のスペース

AsciiDoctor はデフォルトの CSS を用意していて、生成した HTML はそれなりの見た目で表示できます。
最近、CSS のプロパティ `text-autospace` に設定可能な値として `normal` が[主要なブラウザでサポート][8]され、
和欧混植のテキスト文書の表示において従来より見た目を良くできます。

そこで AsciiDoc 文書からフォーマット用マークの検出のために入っていた半角スペースを削除しました。
前述のプロパティ設定と併せることで、HTML 表示時に読みやすさがだいぶ向上したと思います。

なお、マークに関しては手間が増えますが必要な箇所は unconstrained formatting pair へ変更しました。

#### 注記号

別名、合印。
文末に付ける際に英語の場合はピリオドの後ろと決まっているのですが、日本語だと句点の前に付ける流派と後ろに付ける流派があります。
元の[翻訳版][2]もそうでしたが、英語から日本語に翻訳した文書だと英語方式で句点の後ろになっていたりします。
本翻訳では W3C の[日本語組版処理の要件][9]やモリサワの[Note記事][10]にあるように、
日本語の組版では一般的と思われる句点の前に付けるようにしました。

### 外来語の末尾における長音表記

#### 長音をつけた単語

- エディター
- オーダー
- トランスデューサー
- パラメーター
- フォーマッター
- プログラマー
- ベクター
- ヘルパー
- メンバー
- ユーザー
- リーダー (reader macro の訳語で使用)

#### 長音をつけなかった単語

- クロージャ
- コミュニティ
- ライブラリ
- ユーティリティ

### AsciiDoctor による変換作業

英語版に記載されている手順とは少し異なるので補足します。
なお、必要となるソフトウェアは既に導入されているものとします。私は全部入りの[Docker イメージ][11]を使いました。

#### HTML

前述したように CSS の設定を追加するため、docinfo で `<style>` タグを差し込んでいます。
README.adoc と README-docinfo.html を用意して、AsciiDoctor で HTML ファイルを生成。
GitHub Pages で公開している HTML 版は、左側に目次を付けるよう以下のコマンドで生成されています。

```
asciidoctor -a toc="left" -a toclevels=2 -a docinfo=private-head README.adoc
```

docinfo を使わなくても HTML ファイルの生成は可能です。少々、見栄えが悪くなるだけです。

#### PDF

AsciiDoctor PDF の他に、日本語フォントが必要になります。
ただし、AsciiDoctor PDF で生成される PDF 文書のレイアウト品質は悪いです。

- テーブルの全体幅を自動調整にするとカラム幅がおかしくなる場合あり
- 日本語とラテン文字の間の文字間隔が調整されていない

これは元文書に起因する話ですが、物理的なページを前提として文書が書かれておらず PDF にすると妙な箇所でページをまたいだりします。

HTML 版を眺めるのが一番良いと思いますが、念の為に作ったときの作業手順を残しておきます。

日本語用のフォントを用意します。今回は [IBM Plex Sans JP][12] から `.ttf` ファイルを抜粋して `./fonts/` フォルダに展開。

```
$ ls ./fonts
IBMPlexSansJP-Bold.ttf
IBMPlexSansJP-Medium.ttf
IBMPlexSansJP-Regular.ttf
IBMPlexSansJP-SemiBold.ttf
```

つづいて標準テーマ修正のため、[元ネタ][13]を改変して下記のテーマファイルを作成。
適当なファイル名を付けて、README.adoc と同じフォルダに置きます。
日本語フォントは特別に用意しない限りイタリック体が無いので、ウェイト違いで誤魔化しています。

```
$ cat ./my-theme.yml
extends: default
font:
  catalog:
    merge: true
    IBM Plex Sans JP:
      normal: ./fonts/IBMPlexSansJP-Regular.ttf
      bold: ./fonts/IBMPlexSansJP-SemiBold.ttf
      italic: ./fonts/IBMPlexSansJP-Medium.ttf
      bold_italic: ./fonts/IBMPlexSansJP-Bold.ttf
    M+ 1p Fallback: GEM_FONTS_DIR/mplus1p-regular-fallback.ttf
    Noto Emoji: GEM_FONTS_DIR/notoemoji-subset.ttf
  fallbacks: [M+ 1p Fallback, Noto Emoji]
base:
  font_family: IBM Plex Sans JP
  text_align: left
```

AsciiDoctor PDF で PDF ファイルを生成。
テーマの指定以外のオプションは、Creative Commons のロゴマークを読み込むための指定(allow-uri-read)と、
日本語向けの組版指定(scripts=cjk)です。

```
asciidoctor-pdf -a allow-uri-read -a scripts=cjk -a pdf-theme=my-theme.yml README.adoc
```

### 文書の難易度

スタイルガイドなので仕方がないとは思いますが、まったくの Clojure 初心者には少しハードルが高い気がします。
Lisp を触ったことがあるか、[Webサイト][14]のドキュメントを流し読みしておかないと厳しいのではないかと思います。


[1]: https://github.com/bbatsov/clojure-style-guide
[2]: https://github.com/totakke/clojure-style-guide
[3]: https://www.ohmsha.co.jp/book/9784274069130.html
[4]: https://metaredux.com/posts/2020/12/06/semantic-clojure-formatting.html "Semantic Clojure Formatting"
[5]: https://github.com/bbatsov/clojure-style-guide/commit/463c776813063417749e0a522161ef999d0678c5
[6]: https://github.com/metosin/malli
[7]: https://github.com/nubank/matcher-combinators
[8]: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-autospace#browser_compatibility
[9]: https://www.w3.org/TR/jlreq/ "Requirements for Japanese Text Layout 日本語組版処理の要件（日本語版）"
[10]: https://note.morisawa.co.jp/n/n6a1ca4c1a85d "縁の下の力持ち「注」の使いどころ"
[11]: https://hub.docker.com/r/asciidoctor/docker-asciidoctor/
[12]: https://fonts.google.com/specimen/IBM+Plex+Sans+JP
[13]: https://github.com/asciidoctor/asciidoctor-pdf/blob/main/data/themes/default-with-font-fallbacks-theme.yml
[14]: https://clojure.org/
