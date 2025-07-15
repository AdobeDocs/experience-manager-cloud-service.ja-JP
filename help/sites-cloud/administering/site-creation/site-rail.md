---
title: サイトパネルを使用したサイトテーマの管理
description: 公開配信を使用した従来のAEM オーサリングプロジェクト用にサイトテーマを簡単にカスタマイズおよび管理するのに役立つ、サイトパネルの強力な機能について説明します。
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
source-git-commit: 076005e1ed1ca3303ed5843a3f27e0d707df5022
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 82%

---


# サイトパネルを使用したサイトテーマの管理 {#site-panel}

{{traditional-aem}}

公開配信を使用した従来のAEM オーサリングプロジェクト用にサイトテーマを簡単にカスタマイズおよび管理するのに役立つ、サイトパネルの強力な機能について説明します。

## 概要 {#overview}

サイトパネルを使用すると、[ パブリッシュ配信を使用した従来のAEM オーサリングプロジェクト用に、サイトのテーマとテンプレートのリソースを管理できます。コンテンツツリーパネル、参照パネル、タイムラインパネルなどの ](/help/sites-cloud/authoring/author-publish.md) [ 他のパネルと同様 ](/help/sites-cloud/authoring/sites-console/console-side-panel.md)、サイトパネルは、Sites コンソールの左端のパネルとして表示され、選択した項目に関する情報が表示されます。 他のパネルとは異なり、サイトパネルはサイトルートにのみ適用されます。

サイトパネルは、次のように、サイトのテーマおよびテンプレートに関連する情報の管理に使用します。

* [テーマソースのダウンロード](#downloading-theme-sources)
* [ワイヤーフレームなどのテンプレートリソースのダウンロード](#downloading-template-resources)
* [テーマのバージョンの表示と変更](#theme-vrsions)
* [フロントエンドパイプラインの有効化](#enabling-the-front-end-pipeline)

>[!TIP]
>
>クイックサイト作成ツールや、サイトテーマを容易にカスタマイズするためのフロントエンドパイプラインに習熟するには、[クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を確認します。

## テーマソースのダウンロード {#downloading-theme-sources}

AEMで[サイトテンプレート](site-templates.md)に基づいてサイトを作成する場合は、サイトパネルを使用して[サイトテーマ](site-themes.md)をダウンロードできます。

Sites コンソールにサイトパネルが表示された状態で、サイトのルートを選択すると、そのサイトに関するテーマ情報が表示されます。

![テーマソースのダウンロード](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

「**テーマソースをダウンロード**」を選択して、カスタマイズ目的でサイトテーマのローカルコピーを `.zip` ファイルとしてダウンロードします。

## テンプレートリソースのダウンロード {#downloading-template-resources}

[サイトテンプレート](site-templates.md)には、サイトコンテンツ構造や[サイトテーマ](site-themes.md)に加えて、ワイヤフレーム設計やその他のサイト関連ファイルなどの情報を含めることができます。

サイトテンプレートをベースにしたサイトの場合は、Sites コンソールにサイトパネルが表示された状態で、サイトのルートを選択すると、追加のサイトリソースなど、そのサイトに関するテーマ情報が表示されます。

![テーマソースのダウンロード](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

**その他のテンプレートリソースをダウンロード**&#x200B;の見出しの下にあるボタンを選択すると、使用可能なファイルのローカルコピーをダウンロードできます。

## テーマのバージョンの表示と変更 {#them-versions}

サイトテンプレートをベースにしたサイトの場合は、そのテンプレートのテーマをフロントエンド開発者が既にカスタマイズしている可能性があります。サイトパネルを使用すると、現在デプロイされているサイトテーマのバージョンを表示し、以前のバージョンに切り替えることができます。

Sites コンソールにサイトパネルが表示された状態で、サイトのルートを選択すると、そのサイトに関するテーマ情報が表示されます。

![パネルに表示されるサイトのバージョン](/help/sites-cloud/administering/assets/theme-versions.png)

テーマの現在のバージョンは、コミットハッシュと、前回の更新のタイムスタンプと共に表示されます。

「**バージョンを選択**」を選択すると、テーマの以前のバージョンを表示します。

![テーマのバージョンを選択](/help/sites-cloud/administering/assets/select-theme-versions.png)

変更するバージョンを選択してから「**適用**」を選択し、変更を加えます。

テーマの新しいバージョンがフロントエンドパイプラインを通じてデプロイされたが、サイトには適用されていないことを AEM が検出した場合は、通知アイコンが表示されます。

![テーマの新しいバージョンを示すインジケーター](/help/sites-cloud/administering/assets/new-theme-version.png)

「**バージョンを選択**」ボタンを使用して、新しいテーマバージョンに更新できます。

## フロントエンドパイプラインの有効化 {#enabling-front-end-pipeline}

サイトテンプレートを使用してサイトを作成しなかった場合は、フロントエンドパイプラインを使用してテーマをカスタマイズおよびデプロイすることはできません。

ただし、サイトパネルを使用して、サイトのフロントエンドパイプラインを有効にすることができます。

Sites コンソールにサイトパネルが表示された状態で、サイトのルートを選択すると、そのサイトに関するテーマ情報が表示されます。次に、「**フロントエンドパイプラインを有効化**」を選択します。

![フロントエンドパイプラインの有効化](/help/sites-cloud/administering/assets/enable-fep.png)

詳しくは、[フロントエンドパイプラインの有効化](enable-front-end-pipeline.md)のドキュメントを参照してください。
