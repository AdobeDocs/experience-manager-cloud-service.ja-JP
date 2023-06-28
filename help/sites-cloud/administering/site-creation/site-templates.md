---
title: サイトテンプレート
description: AEM サイトテンプレートを使用して、サイト構造と初期コンテンツを事前に定義し、サイトをすばやく作成する方法を説明します。
feature: Administering
role: Admin
exl-id: 42eec922-b02e-4f2c-8107-7336192919c7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 76%

---

# サイトテンプレート {#site-templates}

AEM サイトテンプレートを使用して、サイト構造と初期コンテンツを事前に定義し、サイトをすばやく作成する方法を説明します。

## 概要 {#overview}

一連の既存の標準に基づいて新しいサイトをすばやくデプロイするために、事前定義された構造を利用できると便利です。サイトテンプレートを使用すると、基本的なサイトコンテンツを組み合わせて、便利で再利用可能なパッケージを作成できます。

サイトテンプレートには、通常、基本的なサイトコンテンツと、構造およびサイトスタイル設定情報 ( [サイトのテーマ](site-themes.md) 新しいサイトを素早く開始する。 管理者は、 [サイト作成プロセス中に](create-site.md) サイトのベースとなるサイトテンプレートを選択します。

テンプレートは再利用可能でカスタマイズ可能なので、強力です。 また、AEM インストールで複数のテンプレートを使用できるため、様々なビジネスニーズを満たすために異なるサイトを柔軟に作成できます。

>[!NOTE]
>
>AEMのサイトテンプレートを [ページテンプレート](/help/sites-cloud/authoring/features/templates.md). サイトテンプレートは、サイトの全体的な構造を定義します。ページテンプレートは、個々のページの構造と初期コンテンツを定義します。
>
>AEMのサイトテンプレートを [AEMサイトテーマ](site-themes.md).  AEM サイトテーマには、AEM サイトのスタイル設定情報のみが含まれています。AEMのサイトテンプレートは、サイト構造と初期コンテンツを定義し、次の目的で使用できるAEMのサイトテーマを含みます。 [クイックサイト作成](create-site.md).

## サイトテンプレートの AEM への追加 {#adding}

複数のテンプレートをAEMに追加できます。これを使用して、 [サイトの作成](create-site.md).

1. AEM オーサリング環境にサインインし、サイトコンソールに移動します

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 画面の右上にある「**作成**」をタップまたはクリックし、ドロップダウンメニューから「**テンプレートのサイト**」を選択します。

   ![テンプレートからのサイトの作成](../assets/create-site-from-template.png)

1. サイトの作成ウィザードで、左側の列の上部にある「**インポート**」をタップまたはクリックします。

   ![サイトの作成ウィザード](../assets/site-creation-wizard.png)

1. ファイルブラウザーで、使用するテンプレートを見つけて、「**アップロード**」をタップまたはクリックします。

1. アップロードが完了すると、使用可能なテンプレートのリストに表示されます。

テンプレートがアップロードされ、次の場所で使用できます。 [新しいサイトを作成](create-site.md).

既存のテンプレートを選択すると、右側の列にテンプレートに関する情報が表示されます。

![テンプレートを選択](../assets/select-site-template.png)

## サイトテンプレート構造 {#structure}

サイトテンプレートは、パッケージコンテンツの目的を明確に反映する論理構造を持つ単なるパッケージです。サイトテンプレートの構造は次のとおりです。

* `files`：UI キット、XD ファイル、およびその他のファイルを含むフォルダー
* `previews`：サイトテンプレートのスクリーンショットを含むフォルダー
* `site`：ページテンプレート、ページなど、このテンプレートから作成したサイトごとにコピーされるコンテンツのコンテンツパッケージ。
* `theme`：CSS、JavaScript など、サイトの外観を変更するための[サイトテーマ](site-themes.md)のソース。

## Standard Site Template {#standard-site-template}

アドビは、独自のテンプレートを作成するための基礎として使用できるベストプラクティスの参照テンプレートを提供しています。[Standard Site Template は GitHub で入手できます。](https://github.com/adobe/aem-site-template-standard)

[標準サイトテンプレートの最新リリース](https://github.com/adobe/aem-site-template-standard/releases) は、 [新しいサイトの作成](create-site.md).

## サイトテンプレートの開発 {#developing-templates}

アドビは、新しいサイトテンプレートを作成するための一連のスクリプトとして AEM サイトテンプレートビルダーを提供しています。

[AEM Site Template Builder は、GitHub の使用方法に関するドキュメントと共に利用できます](https://github.com/adobe/aem-site-template-builder).  [サイトテーマ](site-themes.md) をカスタマイズするにはフロントエンドの開発者の経験が必要であり、サイト構造とコンテンツをカスタマイズするには AEM 開発者の知識が必要です。
