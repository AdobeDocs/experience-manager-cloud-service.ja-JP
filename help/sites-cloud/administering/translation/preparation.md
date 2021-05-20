---
title: 翻訳するコンテンツの準備
description: 翻訳するコンテンツを準備する方法について説明します。
feature: 言語コピー
role: Administrator
exl-id: afc577a2-2791-481a-ac77-468011e4302e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 37%

---

# 翻訳するコンテンツの準備 {#preparing-content-for-translation}

通常、多言語の Web サイトは、ある程度の量のコンテンツを複数の言語で提供します。サイトは 1 つの言語でオーサリングされてから、他の言語に翻訳されます。通常、多言語サイトはページのブランチで構成されます。各ブランチには、異なる言語のサイトのページが含まれています。

[WKNDチュートリアルサイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)には、複数の言語ブランチが含まれ、次の構造を使用します。

```text
/content
    |- wknd
        |- language-masters
            |- en
            |- de
            |- es
            |- fr
            |- it
        |- us
            |- en
            |- es
        |- ca
            |- en
            |- fr
        |- ch
            |- de
            |- fr
            |- it
        |- de
            |- de
        |- fr
            |- fr
        |- es
            |- es
        |- it
            |- it
```

サイトのコンテンツを最初にオーサリングするための言語コピーが言語マスターです。言語マスターは、他の言語に翻訳されるソースです。

サイトの各言語ブランチは言語コピーと呼ばれます。言語コピーのルートページ（言語ルート）では、言語コピー内のコンテンツの言語を識別します。例えば、`/content/wknd/fr`はフランス語の言語コピーの言語ルートです。 ソースサイトの翻訳の実行時に正しい言語がターゲットになるように、言語コピーは、[正しく設定された言語ルート](preparation.md#creating-a-language-root)を使用する必要があります。

翻訳するサイトを準備するには、次の手順を使用します。

1. 言語マスターの言語ルートを作成します。例えば、英語のWKNDデモサイトの言語ルートは`/content/wknd/language-masters/en`です。 [言語ルートの作成](preparation.md#creating-a-language-root)の情報に従って言語ルートが正しく設定されていることを確認してください。
1. 言語マスターのコンテンツをオーサリングします。
1. サイトの各言語コピーの言語ルートを作成します。例えば、WKNDサンプルサイトのフランス語の言語コピーは`/content/wknd/language-masters/fr`です。

翻訳するコンテンツを準備したら、言語コピーおよび関連する翻訳プロジェクトに、見つからないページを自動的に作成できます。（[翻訳プロジェクトの作成](managing-projects.md)を参照） AEMのコンテンツ翻訳プロセスの概要については、[多言語Webサイトのコンテンツの翻訳](overview.md)を参照してください。

## 言語ルートの作成 {#creating-a-language-root}

コンテンツの言語を識別する言語コピーのルートページとして言語ルートを作成します。言語ルートを作成したら、言語コピーを含む翻訳プロジェクトを作成できます。

言語ルートを作成するには、ページを作成し、**Name**&#x200B;プロパティの値としてISO言語コードを使用します。言語コードは、次のいずれかの形式にする必要があります。

* `<language-code>`  — サポートされている言語コードは、ISO-639-1で定義されている2文字のコードです(例： `en`)。
* `<language-code>_<country-code>` また `<language-code>-<country-code>` は — ISO 3166で定義されている小文字または大文字の2文字コード(例： `en_US`、 `en_us`、 `en_GB`、 `en-gb`)がサポートされています。

グローバルサイト用に選択した構造に従って、どちらかの形式を使用できます。例えば、WKNDサイトのフランス語の言語コピーのルートページの`fr`は、**Name**&#x200B;プロパティとして表示されます。 **Name**&#x200B;プロパティは、リポジトリ内のページノードの名前として使用され、ページのパス(`http://<host>:<4502>/content/wknd/language-masters/fr.html`)を決定します。

1. サイトに移動します。
1. 言語コピーを作成するサイトをクリックまたはタップします。
1. 「**作成**」をクリックまたはタップし、「**ページ**」をクリックまたはタップします。

   ![ページを作成](../assets/create-page.png)

1. ページテンプレートを選択し、「**次へ**」をクリックまたはタップします。
1. 「**名前**」フィールドに、国コードを`<language-code>`または`<language-code>_<country-code>`の形式で入力します（例：`en`、`en_US`、`en_us`、`en_GB`、`en_gb`）。 ページのタイトルを入力します。

   ![言語ルートページの作成](../assets/create-language-root.png)

1. 「**作成**」をクリックまたはタップします。確認のダイアログボックスで、「**完了**」をクリックまたはタップしてサイトコンソールに戻ります。または「**開く**」をクリックまたはタップして言語コピーを開きます。

## 言語ルートのステータスの確認  {#seeing-the-status-of-language-roots}

AEMには、作成された言語ルートのリストを表示する&#x200B;**参照**&#x200B;レールが用意されています。

![言語ルート](../assets/language-roots.png)

[パネルセレクターを使用して、ページの言語コピーを表示する手順は次のとおりです。](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

1. サイトコンソールで、サイトのページを選択し、「**参照**」をクリックまたはタップします。

   ![参照レールを開く](../assets/opening-references-rail.png)

1. 参照レールで、「**言語コピー**」をクリックまたはタップします。 レールには、Webサイトの言語コピーが表示されます。

## 複数のレベルの言語コピー {#multiple-levels}

言語ルートは、例えば地域別にノードの下にグループ化することもできますが、言語コピーのルートとして認識され続けます。

```text
/content
    |- wknd
        |- language-masters
            |- europe
                |- de
                |- fr
                |- it
                |- es
                ]- pt
            |- americas
                |- en
                |- es
                |- fr
                |- pt
            |- asia
                |- ...
            |- africa
                |- ...
            |- oceania
                |- ...
        |- europe
        |- americas
        |- asia
        |- africa
        |- oceania            
```

>[!NOTE]
>
>1 レベルのみ許可されます。例えば、次の例では、`es`ページを言語コピーに解決できません。
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`

>
> 
この`es`言語コピーは、`en`ノードから2レベル(`americas/central-america`)離れているので、検出されません。

>[!TIP]
>
>このような設定では、言語ルートは、言語のISOコードだけでなく、任意のページ名を持つことができます。 AEMは常に最初にパスと名前を確認しますが、ページ名が言語を識別しない場合、AEMはページの`cq:language`プロパティで言語の識別を確認します。
