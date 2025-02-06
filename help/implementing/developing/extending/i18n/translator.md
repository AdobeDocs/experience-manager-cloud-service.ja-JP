---
title: UI 文字列の国際化
description: AEMには、コンポーネント UI で使用される様々なテキスト翻訳を管理するためのコンソールが用意されています。
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 14%

---


# トランスレーターを使用した辞書の管理{#using-translator-to-manage-dictionaries}

AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するためのコンソールが用意されています。このコンソールの入手先：

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

トランスレーターツールを使用して、英語の文字列とその翻訳を管理します。辞書はリポジトリ（例：`/apps/myproject/i18n`）に作成されます。

トランスレーターツールとユーザー管理辞書は、異なる言語でコンポーネント UI を表します。ページを翻訳する場合は、[ 多言語サイトのコンテンツの翻訳 ](/help/sites-cloud/administering/translation/overview.md) を参照してください。

## 辞書の作成 {#creating-a-dictionary}

開発者は、AEMで i18n 辞書を作成して、ローカライズされたコンポーネント文字列を管理できます。 辞書は、通常、`/apps` のコンポーネントコードの一部です。 以下は、すべての WKND コンポーネントで使用される 1 つのキーと値のペアを持つAEM WKND コードの例です。

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

辞書は、AEM GitHub リポジトリで作成したら、AEM [CI/CD パイプライン ](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) を使用してデプロイできます。

## 辞書の場所 {#dictionary-locations}

開発者は、`/apps` または `/content/cq:i18n` のいずれかでソース言語辞書を自由に作成できます。 AEM アーキタイプのサンプルコードから開始すると、最初の辞書は通常、`/apps` パスにあります。 対応する辞書の言語コピーを `/apps` にも保存する場合は、開発者がコンポーネントコードでこれらの言語コピーを手動で作成および管理する必要があります。

または、i18n 辞書に対する新しいAEM ランタイム翻訳プロセスにより、ソースディクショナリが `/apps` または `/content` に格納されているかどうかに関係なく、翻訳済みの辞書が `/content/cq:i18n/<projectName>` に作成されます。

i18N 辞書、ソースおよび言語コピーの場所は、次の条件を使用して決定する必要があります。

* `/apps`
   * AEM アーキタイプおよび WKND サンプルコードに従った、コンポーネント文字列の翻訳を含む辞書のデフォルトの場所
   * sling ごとの最高のレンダリング順序（[ リソースバンドル検索階層 ](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies)）
   * ただし、AEM as a Cloud Service環境では変更できないので、実行時の編集や辞書の翻訳 `/apps` できません

* `/content/cq:i18n`
   * i18n 辞書用の代替の場所（場合）
      * 辞書のランタイム翻訳が必要です
      * 実行時に辞書を編集する機能が必要です
   * ランタイム辞書の翻訳によって言語コピーが作成されるデフォルトの場所。

`/apps` は Sling のレンダリング順序で常に `/content` を置き換えるので、キーと値のペアが同じ辞書は `/apps` と `/content/cq:i18n` に同時に存在してはいけません。これは、`/content/cq:i18n` の辞書はレンダリングには使用されないからです。 辞書言語コピー（翻訳先）が `/apps` に既に存在し、実行時にAEM as a Cloud Serviceで翻訳可能にすることを目的としている場合、`/apps` 内の元の辞書言語コピーを `/content/cq:i18n` に移動するか、`/apps` で削除して、ソース辞書を翻訳することにより `/content/cq:i18n` 内で自動的に再作成する必要があります。 この翻訳プロセスにより、`/content/cq:i18n` に言語コピーが自動的に作成されます。

## 辞書の自動作成 {#automatic-creation}

AEM コアコンポーネントを含むAEM ページおよびエクスペリエンスフラグメントの場合、新しい辞書の翻訳プロセスでは、これらのページやエクスペリエンスフラグメントをスキャンして、翻訳する必要のあるコンポーネントやコンポーネント文字列を探します。 次に、対応する新しい辞書言語コピーが `/content/cq:i18n` に自動的に作成されます。 コンテンツフラグメントはAEM コアコンポーネントを使用しない純粋な構造化コンテンツなので、これは適用されません。

## 辞書の書き出し {#exporting-a-dictionary}

AEM as a Cloud Service `/apps` または `/libs` の場所にある i18n 辞書は変更できないので、実行時にそれらの場所に変換することはできませんが、それらの辞書を実行時に書き出して、AEMの外部で非同期に変換することは可能です。

辞書のソース言語文字列を XLIFF ファイルに書き出すには：

1. トランスレーターツール `http://<host>:<port>/libs/cq/i18n/gui/translator.html` を開く

   >[!NOTE]
   >
   >ツールは、この URL 経由でのみ使用でき、AEM製品の UI からアクセスすることはできません。

1. Dictionaries ドロップダウンメニューを使用して、書き出す辞書を選択します。
1. 「XLIFF 翻訳を書き出し」をクリックし、「完全な `<locale>` xliff を書き出し」をクリックします。

## 辞書の読み込み {#importing-a-dictionary}

XLIFF ファイルを辞書に読み込んで辞書のコンテンツを入力するには：

1. トランスレーターツール `http://<host>:<port>/libs/cq/i18n/gui/translator.html` を開く
1. 「インポート」をクリックし、「翻訳を XLIFF」をクリックします。
1. 読み込むファイルを選択して、「OK」をクリックします。
