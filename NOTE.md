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

### CI/CD環境

- .github/workflows/deploy.yml （GitHub Pages 公開用ワークフロー）

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
- good: 良い、適切な
- ok, okay: 大丈夫
- okish, ok-ish: まあまあ
- not as good: あまり良くない
- bad: 悪い、不適切な
- very bad: 非常に悪い

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
最近、CSS のプロパティ `text-autospace` に設定可能な値として `normal` が[主要なブラウザでサポート][4]され、
和欧混植のテキスト文書の表示において従来より見た目を良くできます。

そこで AsciiDoc 文書からフォーマット用マークの検出のために入っていた半角スペースを削除しました。
前述のプロパティ設定と併せることで、HTML 表示時に読みやすさがだいぶ向上したと思います。

なお、マークに関しては手間が増えますが必要な箇所は unconstrained formatting pair へ変更しました。

#### 注記号

別名、合印。
文末に付ける際に英語の場合はピリオドの後ろと決まっているのですが、日本語だと句点の前に付ける流派と後ろに付ける流派があります。
元の[翻訳版][2]もそうでしたが、英語から日本語に翻訳した文書だと英語方式で句点の後ろになっていたりします。
本翻訳では W3C の[日本語組版処理の要件][5]やモリサワの[Note記事][6]にあるように、
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
なお、必要となるソフトウェアは既に導入されているものとします。私は全部入りの[Docker イメージ][7]を使いました。

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

日本語用のフォントを用意します。今回は [IBM Plex Sans JP][8] から `.ttf` ファイルを抜粋して `./fonts/` フォルダに展開。

```
$ ls ./fonts
IBMPlexSansJP-Bold.ttf
IBMPlexSansJP-Medium.ttf
IBMPlexSansJP-Regular.ttf
IBMPlexSansJP-SemiBold.ttf
```

つづいて標準テーマ修正のため、[元ネタ][9]を改変して下記のテーマファイルを作成。
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
Lisp を触ったことがあるか、[Webサイト][10]のドキュメントを流し読みしておかないと厳しいのではないかと思います。


[1]: https://github.com/bbatsov/clojure-style-guide
[2]: https://github.com/totakke/clojure-style-guide
[3]: https://www.ohmsha.co.jp/book/9784274069130.html
[4]: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-autospace#browser_compatibility
[5]: https://www.w3.org/TR/jlreq/ "Requirements for Japanese Text Layout 日本語組版処理の要件（日本語版）"
[6]: https://note.morisawa.co.jp/n/n6a1ca4c1a85d "縁の下の力持ち「注」の使いどころ"
[7]: https://hub.docker.com/r/asciidoctor/docker-asciidoctor/
[8]: https://fonts.google.com/specimen/IBM+Plex+Sans+JP
[9]: https://github.com/asciidoctor/asciidoctor-pdf/blob/main/data/themes/default-with-font-fallbacks-theme.yml
[10]: https://clojure.org/
