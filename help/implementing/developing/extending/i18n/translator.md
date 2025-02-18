---
title: UI 文字列の国際化
description: AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するコンソールが用意されています。
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4b363473-3c5e-4d8e-97d6-b7b96ccf9e58
source-git-commit: f7aeec56d2eb10cdeb7efe63ffb15ed8af6a36e0
workflow-type: ht
source-wordcount: '654'
ht-degree: 100%

---

# トランスレーターを使用した辞書の管理{#using-translator-to-manage-dictionaries}

AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するためのコンソールが用意されています。このコンソールの入手先：

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

トランスレーターツールを使用して、英語の文字列とその翻訳を管理します。辞書はリポジトリ（例：`/apps/myproject/i18n`）に作成されます。

トランスレーターツールとユーザー管理辞書は、異なる言語でコンポーネント UI を表します。ページを翻訳する場合は、[多言語サイトのコンテンツの翻訳](/help/sites-cloud/administering/translation/overview.md)を参照してください。

## 辞書の作成 {#creating-a-dictionary}

開発者は、AEM で i18n 辞書を作成して、ローカライズされたコンポーネント文字列を管理できます。辞書は通常、`/apps` のコンポーネントコードの一部です。次に、すべての WKND コンポーネントで使用される 1 つのキーと値のペアを含む AEM WKND コードの例を示します。

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

開発者は、コンポーネント文字列の言語定義を保持する新しい辞書のルートノード（`sling:Folder`）を追加することで、追加の辞書を作成できます。

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>これは [Sling i18n モジュール](https://sling.apache.org/site/internationalization-support.html)の構造です。

AEM GitHub リポジトリで作成された辞書は、AEM [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を通じてデプロイできます。

## 辞書の場所 {#dictionary-locations}

開発者は、`/apps` または `/content/cq:i18n` のいずれかでソース言語辞書を自由に作成できます。AEM アーキタイプサンプルコードから開始すると、最初の辞書は通常、`/apps` パスにあります。対応する辞書の言語コピーも `/apps` に保存することが目標である場合、これらの言語コピーは、開発者がコンポーネントコード内で手動で作成および管理する必要があります。

または、i18n 辞書の新しい AEM ランタイム翻訳プロセスでは、ソース辞書が `/apps` または `/content` に保存されているかどうかに関係なく、翻訳済み辞書が `/content/cq:i18n/<projectName>` に作成されます。

i18n 辞書、ソースおよび言語コピーを配置する場所の決定は、次の条件を使用して行う必要があります。

* `/apps`
   * AEM アーキタイプと WKND サンプルコードに従った、コンポーネント文字列の翻訳を含む辞書のデフォルトの場所
   * Sling（[リソースバンドル検索階層](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies)）ごとの最高のレンダリング順序
   * ただし、`/apps` は AEM as a Cloud Service 環境では不変であるので、辞書のランタイム編集や翻訳はできません。

* `/content/cq:i18n`
   * i18n 辞書の代替場所（次の場合）
      * 辞書のランタイム翻訳は必須です
      * ランタイムに辞書を編集する機能は必須です
   * ランタイム辞書の翻訳によって言語コピーが作成されるデフォルトの場所。

Sling のレンダリング順序では `/apps` が常に `/content` に優先するので、`/content/cq:i18n` の辞書をレンダリングに使用しない場合、同一のキーと値のペアを持つ辞書が `/apps` と `/content/cq:i18n` に同時に存在してはならないことに留意することが重要です。辞書言語コピー、つまり翻訳先が既に `/apps` に存在し、AEM as a Cloud Service でランタイムに翻訳できるようにすることを目標としている場合は、`/apps` の元の辞書言語コピーを `/content/cq:i18n` に移動するか、`/apps` で削除してソース辞書を翻訳することで `/content/cq:i18n` に自動的に再作成する必要があります。この翻訳プロセスにより、`/content/cq:i18n` に言語コピーが自動的に作成されます。

## 辞書の自動作成 {#automatic-creation}

AEM コアコンポーネントを含む AEM ページおよびエクスペリエンスフラグメントの場合、新しい辞書翻訳プロセスでは、翻訳する必要があるコンポーネントとコンポーネント文字列について、これらのページやエクスペリエンスフラグメントもスキャンします。その後、対応する新しい辞書言語コピーが `/content/cq:i18n` に自動的に作成されます。コンテンツフラグメントはAEM コアコンポーネントを使用しない純粋な構造化コンテンツなので、これは適用されません。

## 辞書の書き出し {#exporting-a-dictionary}

`/apps` または `/libs` の場所にある i18n 辞書のランタイム翻訳は、これらの場所が不変であるので AEM as a Cloud Service では実行できませんが、これらの辞書を引き続きランタイムに書き出して AEM の外部で非同期翻訳を行うことはできます。

辞書のソース言語文字列を XLIFF ファイルに書き出すには：

1. トランスレーターツール `http://<host>:<port>/libs/cq/i18n/gui/translator.html` を開く

   >[!NOTE]
   >
   >ツールは、この URL 経由でのみ使用でき、AEM 製品の UI からはアクセスできません。

1. Dictionaries ドロップダウンメニューを使用して、書き出す辞書を選択します。
1. 「XLIFF 翻訳を書き出し」をクリックし、「完全な `<locale>` xliff を書き出し」をクリックします。

## 辞書の読み込み {#importing-a-dictionary}

XLIFF ファイルを辞書に読み込んで辞書コンテンツを入力するには：

1. トランスレーターツール `http://<host>:<port>/libs/cq/i18n/gui/translator.html` を開く
1. 「読み込み」をクリックし、「XLIFF 翻訳」をクリックします。
1. 読み込むファイルを選択して、「OK」をクリックします。
