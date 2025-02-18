---
title: コンポーネントの国際化
description: コンポーネントとダイアログを国際化して、UI 文字列を様々な言語で表示できるようにします
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 401685af02c720994d72cd95d36f0cfcdf15d198
workflow-type: ht
source-wordcount: '355'
ht-degree: 100%

---

# コンポーネントの国際化{#internationalizing-components}

コンポーネントとダイアログを国際化して、UI 文字列を様々な言語で表示できるようにします。国際化を想定して設計されたコンポーネントでは、UI 文字列を外部化し、翻訳して、リポジトリに読み込むことができます。実行時に、ユーザーの言語の環境設定またはページのロケールによって、UI に表示される言語が決まります。

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

次のプロセスを使用して、コンポーネントを国際化し、様々な言語で UI を提供します。

1. [文字列を国際化するコードを使用してコンポーネントを実装します。](/help/implementing/developing/extending/i18n/dev.md) コードは翻訳対象の文字列を識別し、実行時に表示する言語を選択します。
1. [辞書を作成します](/help/implementing/developing/extending/i18n/translator.md#creating-a-dictionary)。
1. 辞書を XLIFF 形式で[書き出し](/help/implementing/developing/extending/i18n/translator.md#exporting-a-dictionary)、文字列を翻訳して、その XLIFF ファイルを AEM に読み込みます。
1. 辞書をアプリケーションのリリース管理プロセスに組み込みます。

>[!NOTE]
>
>ここで説明するコンポーネントの国際化の方法は、静的文字列の翻訳を対象としています。コンポーネントの文字列が変化する可能性がある場合は、従来の翻訳ワークフローを使用する必要があります。例えば、作成者がコンポーネントの編集ダイアログ内のプロパティを使用して UI 文字列を編集できる場合は、文字列の国際化に言語の辞書を使用しないでください。

## 言語の辞書 {#language-dictionaries}

AEM 国際化フレームワークでは、リポジトリ内の辞書を使用して英語の文字列と他の言語での翻訳を格納します。このフレームワークは、デフォルトの言語として英語を使用します。文字列は英語版を使用して識別されます。国際化フレームワークは通常、UI 文字列に英数字の ID を使用します。ID として文字列の英語版を使用することには、いくつかの利点があります。

* コードが読みやすい。
* デフォルトの言語を常に利用できる。

また、[トランスレーターツール](/help/implementing/developing/extending/i18n/translator.md)を使用すると、すべての辞書を 1 つの場所で一元的に管理できます。

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)

AEM as a Cloud Service では、翻訳の変更は [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を通じて Git から取得する必要があります。

### システム辞書内の文字列のオーバーレイ {#overlaying-strings-in-system-dictionaries}

AEM システム辞書に含まれる文字列をコンポーネントが使用している場合、独自の辞書にその文字列が複製されます。すべてのコンポーネントは独自の辞書の文字列を使用します。

`/apps` ノード下にある辞書の文字列が重複する場合、どの翻訳が使用されるかを予測することはできません。
