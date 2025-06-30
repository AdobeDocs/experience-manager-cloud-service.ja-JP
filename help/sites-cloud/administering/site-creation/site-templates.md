---
title: サイトテンプレート
description: AEM サイトテンプレートを使用して、サイト構造と初期コンテンツを事前に定義し、サイトをすばやく作成する方法を説明します。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '556'
ht-degree: 100%

---

# サイトテンプレート {#site-templates}

{{traditional-aem}}

AEM サイトテンプレートを使用して、サイト構造と初期コンテンツを事前に定義し、サイトをすばやく作成する方法を説明します。

## 概要 {#overview}

一連の既存の標準に基づいて新しいサイトをすばやくデプロイするために、事前定義された構造を利用できると便利です。サイトテンプレートを使用すると、基本的なサイトコンテンツを組み合わせて、便利で再利用可能なパッケージを作成できます。

サイトテンプレートには通常、新しいサイトをすばやく開始するために、ベースサイトのコンテンツと構造、および[サイトテーマ](site-themes.md)と呼ばれるサイトスタイル設定情報が含まれています。管理者は、[サイト作成プロセス中に](create-site.md)サイトのベースとなるサイトテンプレートを選択します。

テンプレートは再利用かつカスタマイズ可能なので、強力です。また、AEM インストールで複数のテンプレートを使用できるため、様々なビジネスニーズを満たすために異なるサイトを柔軟に作成できます。

>[!NOTE]
>
>AEM サイトテンプレートを[ページテンプレート](/help/sites-cloud/authoring/page-editor/templates.md)と混同しないでください。サイトテンプレートは、サイトの全体的な構造を定義します。ページテンプレートは、個々のページの構造と初期コンテンツを定義します。
>
>AEM サイトテンプレートを [AEM サイトテーマ](site-themes.md)と混同しないでください。AEM サイトテーマには、AEM サイトのスタイル設定情報のみが含まれています。AEM サイトテンプレートは、サイト構造と初期コンテンツを定義し、[クイックサイト作成](create-site.md)を可能にする AEM サイトテーマを含んでいます。

## サイトテンプレートの AEM への追加 {#adding}

複数のテンプレートを AEM に追加して、[サイトの作成](create-site.md)に使用できます。

1. AEM オーサリング環境にサインインし、サイトコンソールに移動します

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 画面の右上にある「**作成**」を選択し、ドロップダウンメニューから「**テンプレートからのサイト**」を選択します。

   ![テンプレートからのサイトの作成](../assets/create-site-from-template.png)

1. サイトの作成ウィザードで、左側の列の上部にある「**読み込み**」を選択します。

   ![サイトの作成ウィザード](../assets/site-creation-wizard.png)

1. ファイルブラウザーで、使用するテンプレートを見つけて、「**アップロード**」を選択します。

1. アップロードが完了すると、使用可能なテンプレートのリストに表示されます。

テンプレートがアップロードされ、[新しいサイトの作成](create-site.md)に使用できます。

既存のテンプレートを選択すると、右側の列にテンプレートに関する情報が表示されます。

![テンプレートを選択](../assets/select-site-template.png)

## サイトテンプレート構造 {#structure}

サイトテンプレートは、パッケージコンテンツの目的を明確に反映する論理構造を持つ単なるパッケージです。サイトテンプレートの構造は次のとおりです。

* `files`：UI キット、XD ファイル、およびその他のファイルを含むフォルダー
* `previews`：サイトテンプレートのスクリーンショットを含むフォルダー
* `site`：ページテンプレート、ページなど、このテンプレートから作成したサイトごとにコピーされるコンテンツのコンテンツパッケージ。
* `theme`：CSS、JavaScript など、サイトの外観を変更するための[サイトテーマ](site-themes.md)のソース。

## Standard Site Template {#standard-site-template}

アドビは、独自のテンプレートを作成するための基礎として使用できるベストプラクティスの参照テンプレートを提供しています。[Standard Site Template は GitHub で入手できます](https://github.com/adobe/aem-site-template-standard)。

[標準サイトテンプレートの最新リリース](https://github.com/adobe/aem-site-template-standard/releases)をダウンロードすると、[新しいサイトの作成](create-site.md)に直接使用できます。

## サイトテンプレートの開発 {#developing-templates}

アドビは、新しいサイトテンプレートを作成するための一連のスクリプトとして AEM サイトテンプレートビルダーを提供しています。

[AEM サイトテンプレートビルダーは、GitHub の使用方法に関するドキュメントと共に利用できます](https://github.com/adobe/aem-site-template-builder)。[サイトテーマ](site-themes.md) をカスタマイズするにはフロントエンドの開発者の経験が必要であり、サイト構造とコンテンツをカスタマイズするには AEM 開発者の知識が必要です。
