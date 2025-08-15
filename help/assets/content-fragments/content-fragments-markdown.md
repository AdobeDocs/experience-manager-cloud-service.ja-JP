---
title: マークダウン（アセット - コンテンツフラグメント）
description: コンテンツフラグメントエディターでマークダウン構文を使用してヘッドレスコンテンツを簡単に作成する方法を説明します。
feature: Content Fragments
role: User
exl-id: 7a6d4a63-faf8-4e1c-95da-90db2027a2dd
solution: Experience Manager Sites
source-git-commit: ea85381d63954af3093c34f612babd953c466e1e
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 98%

---

# マークダウン {#markdown}

コンテンツフラグメントの編集者は、[オーサリング](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content)の際、ヘッドレス配信またはページオーサリングのいずれかで、*マークダウン*&#x200B;構文を使用してコンテンツを簡単に記述できます。

>[!NOTE]
>
>コンテンツフラグメントは Sites 機能ですが、**Assets** として保存されます。
>
>コンテンツフラグメントをオーサリングするエディターは 2 つあります。基本機能は同じですが、いくつか違いがあります。この節では、**Assets** コンソールから主にアクセスされるエディターを説明します。（主に&#x200B;**コンテンツフラグメント**&#x200B;コンソールからアクセスされる）新しいエディターについて詳しくは、Sites のドキュメントの[コンテンツフラグメント - オーサリング](/help/sites-cloud/administering/content-fragments/authoring.md)を参照してください。

![Markdown エディター](/help/assets/content-fragments/assets/cfm-markdown-01.png)

以下を定義できます。

* [見出し表記](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落と改行](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [リンク](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [画像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [ブロック引用](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [リスト](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [コードブロック](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [バックスラッシュエスケープ](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 見出し表記 {#heading-notation}

ハッシュタグ（#）を前に付けてヘッダーを作成します。H1 にはハッシュタグを 1 つ（#）、H2 にはハッシュタグを 2 つ（##）使用します。最大で 6 個のハッシュタグを使用できます。例：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

オプションで、テキストに等号で下線を付けて H1、マイナス符号で下線を付けて H2 を作成することもできます。例：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落と改行 {#paragraphs-and-line-breaks}

段落とは、1 つ以上の空白行によって区切られている、1 つ以上の連続したテキスト行です。空白行とは、スペースまたはタブしか含まれていない行です。通常の段落はスペースまたはタブでインデントされません。

改行するには、行の末尾に 2 つ以上のスペースを付けてからリターンします。

## リンク {#links}

インラインリンクと参照リンクを作成できます。

どちらのスタイルでも、リンクテキストはブラケット `[]` で囲みます。

インラインリンクの例を次に示します。

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

参照リンクの構文は次のとおりです。

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 画像 {#images}

画像の構文はリンクと似ています。インライン画像と参照画像を作成できます。

例えば、インライン画像の構文は次のようになります。

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

構文の内容は次のとおりです。

* 感嘆符：! 。
* 1 組のブラケットが後に続き、その中に画像の alt 属性テキストが含まれています。
* 1 組の丸括弧が後に続き、その中に画像の URL またはパスが含まれています。さらに、title 属性を二重引用符または一重引用符で囲んで指定することもできます。

参照スタイルの画像の構文は次のとおりです。

    `![Alt text][id]`

「id」は、定義された画像参照の名前です。画像参照は、次のようにリンク参照と同じ構文を使用して定義されます。

    `[id]: url/to/image "Optional title attribute"`

## ブロック引用 {#block-quotes}

テキストを引用するときは、テキストの先頭に > 記号を付けます。例：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

ブロック引用はネストできます。例：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## リスト {#lists}

順序付きと順序なし両方のリストを作成できます。

順序なしリストを作成するには、* 記号をリストの項目の前に付けます。例：

    `* item in list`

    `* item in list`

    `* item in list`

順序付きリストを作成するには、数字の後にピリオドを付けて、リストの項目の前に付けます。例：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

斜体または太字のスタイルをテキストに追加できます。

次のように斜体を追加できます。

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

次のようにテキストを太字にすることができます。

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

コードの範囲を示すには、バッククォート（`` ` ``）で囲みます。 事前に書式設定されたコードブロックとは異なり、コード範囲は通常の段落内のコードを示します。

例：

    ``Use the `printf()` function.``

## コードブロック {#code-blocks}

コードブロックは通常はソースコードを示すために使用されます。コードブロックを作成するには、1 個のタブまたは少なくとも 4 個分のスペースを使用してコードをインデントします。例：

    `This is a normal paragraph.`

        `This is a code block.`

## バックスラッシュエスケープ {#backslash-escapes}

書式設定構文で特殊な意味を持つリテラル文字を表示するには、バックスラッシュエスケープを使用します。例えば、ある単語を（HTML の &lt;em> タグではなく）リテラルアスタリスクで囲みたい場合は、次のようにアスタリスクの前にバックスラッシュを使用します。

    `\\*literal asterisks\\*`

バックスラッシュエスケープは次の文字に使用できます。

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
