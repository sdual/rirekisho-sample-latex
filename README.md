# 履歴書（LaTeX）

従来のJIS様式を参考にした、A4縦・2ページの日本語履歴書テンプレートです。未記入の状態で印刷し、手書きすることもできます。

> 「JIS規格の履歴書」と通称されてきた様式を参考にしています。JISの履歴書様式例は2020年に削除されているため、現行JISへの適合を保証するものではありません。提出先に指定様式がある場合は、そちらを優先してください。

## ファイル

- `resume.tex`：履歴書の本体（LuaLaTeX用）
- `.latexmkrc`：`latexmk`用の設定

## PDFの作成

LuaLaTeX、LuaTeX-ja、原ノ味フォントを含むTeX環境が必要です。TeX Liveの日本語環境、またはMacTeXを利用できます。最小構成のTeX Liveでは、日本語関連の `collection-langjapanese` と `latexmk` などを追加してください。

このディレクトリで実行します。

```sh
latexmk resume.tex
```

`latexmk`を使わない場合：

```sh
lualatex -interaction=nonstopmode -halt-on-error resume.tex
```

`resume.pdf`が生成されます。Overleafではプロジェクトに `resume.tex` をアップロードし、コンパイラを **LuaLaTeX** に設定してください。

## 記入方法

### 基本情報と自由記述

`resume.tex`冒頭の `\newcommand` の最後の `{}` に内容を入力します。

```tex
\newcommand{\AsOfDate}{2026年9月22日}
\newcommand{\NameKana}{やまだ たろう}
\newcommand{\FullName}{山田 太郎}
\newcommand{\BirthDate}{2000年4月1日}
\newcommand{\Age}{26}
\newcommand{\PostalCode}{100-0001}
\newcommand{\Address}{東京都千代田区○○1-2-3}
\newcommand{\Phone}{090-1234-5678}
\newcommand{\Email}{taro@example.com}
\newcommand{\Motivation}{これまでの経験を生かし、……}
\newcommand{\Requests}{貴社規定に従います。}
```

年齢は自動計算されません。日付とともに更新してください。性別は任意記載です。連絡先欄は、現住所以外への連絡を希望する場合に記入してください。

従来様式の項目として、通勤時間・扶養家族数・配偶者・配偶者の扶養義務も設けています。これらを省略したい場合は、2ページ目の該当する `tabularx` 環境を削除できます。

### 学歴・職歴・免許・資格

該当する表の空行 `\Entry{}{}{}` を、次のように置き換えます。

```tex
\Entry{}{}{\hfill 学歴\hfill\mbox{}}
\Entry{2020}{4}{○○大学 ○○学部 ○○学科 入学}
\Entry{2024}{3}{○○大学 ○○学部 ○○学科 卒業}
\Entry{}{}{\hfill 職歴\hfill\mbox{}}
\Entry{2024}{4}{株式会社○○ 入社}
\Entry{}{}{現在に至る}
\Entry{}{}{\hfill 以上}
```

西暦・和暦は全体で統一してください。1ページ目で収まらない職歴は、2ページ目の続き欄へ記入します。

### 写真

写真ファイルを `resume.tex` と同じディレクトリに置きます。

```tex
\newcommand{\PhotoFile}{photo.jpg}
```

縦40mm・横30mmの枠内に、縦横比を維持して配置します。写真を事前に横3：縦4にトリミングすると枠に合います。空欄のままなら、印刷後の写真貼付用の枠になります。

### 改行・特殊文字・ページ数

- 自由記述欄では `\par` で段落を分けられます。
- `%`、`&`、`_`、`#` などは `\%`、`\&`、`\_`、`\#` と記入します。メールアドレスの `_` にも注意してください。
- 表の行を追加したり、長い文章を入力したりすると、2ページを超えたり枠からはみ出したりする場合があります。まず空行を置き換え、生成したPDFで改行・枠・ページ数を確認してください。
- 自由記述枠の高さは `\TextBox{46mm}` などの値で調整できます。

## 印刷

A4用紙に **実際のサイズ（100%）** で印刷してください。A3横1枚の見開きにしたい場合は、印刷設定でA3・横向き・1枚あたり2ページ・左から右の順を選択してください。
# rirekisho-sample-latex
