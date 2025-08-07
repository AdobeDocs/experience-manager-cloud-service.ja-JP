---
title: コンテンツハブの新機能
description: 最近公開されたContent Hub機能の一部の詳細を説明します
role: User
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: 9f185b48405cd6924ea1483ca79b2acbf36b1be9
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 33%

---

# コンテンツハブの新機能 {#whats-new-content-hub}

コンテンツハブは、Experience Manager Assets as a Cloud Service の一部として使用でき、組織とそのビジネスパートナーがオンブランドのコンテンツに簡単にアクセスできます。これは、大規模なアクティベーション用のアセットの配布と、マーケティングの俊敏性を向上させるオンブランドのコンテンツバリアントの作成に焦点を当てています。

次のビデオでは、Content Hubの主な機能を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) および Assets as a Cloud Service には、250 人のコンテンツハブ制限付きユーザーが含まれます。[Assets Prime](/help/assets/assets-prime.md) には、50 人のコンテンツハブ制限付きユーザーが含まれます。

## リリース日 {#release-date}

Content Hub機能リリース（2025.7.0）のリリース日は 2025 年 8 月 7 日（PT）です（AEM as a Cloud Service リリースのリリースと同じ）。 次回の機能リリース（2025.8.0）は、2025年8月28日（PT）に予定されています。

## 7 月リリースの機能 {#july-release-features}

**Content Hubのブランディングの柔軟性の強化**

Content Hub既存のパーソナライゼーション機能を基に、管理者は、カスタムロゴイメージを追加することで、デプロイメントをさらにカスタマイズできるようになりました。 バナー画像とロゴ画像の両方でTIFF ファイル形式がサポートされるようになり、デザインの柔軟性が高まっています。

**タイトル付きリンクによるスマートな共有**

アセットの詳細表示から共有リンクを生成した場合や、1 つ以上のアセットを選択した後で共有リンクを生成した場合に、タイトルを追加できるようになりました。 これにより、受信者は、特に複数の共有アセットを受信する場合に、各リンクの目的を簡単に識別できます。

![プライベートリンクとパブリックリンク](/help/assets/assets/shared-link-for-assets.png)

**フィルターナビゲーションの改善**

Content Hubのフィルターに **すべて表示** オプションが含まれるようになりました。これにより、使用可能なすべてのファセットと、現在の制限の閲覧のみのアセットカウントから最大 10 個のファセットを表示できます。 各フィルター内の検索機能と並べ替え機能が強化され、アセットの検出と管理がより効率的になります。

## 6 月リリースの機能 {#june-release-features}

### コレクションガバナンス {#collections-governance}

Content Hubでは、作成時にコレクションへのアクセスを制御できるようになり、許可されたユーザーのみがグループ化されたアセットを表示または管理できるようになりました。 これにより、セキュリティの強化、共同作業の向上、アセットの組織的な管理、ガバナンスの効率化が実現します。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## の機能を 5 月リリース {#may-release-features}

Content Hubの 5 月のリリースには、次の機能が含まれています。

* [属性ベースのアクセス制御](#attribute-based-access-control)

* [UI ブランディング](#ui-branding)

* [公開リンク共有](#public-link-sharing)

* [複数のアセットを ZIP としてダウンロード](#download-multiple-assets-as-zip)

* [Content Hubの Dynamic Media レンディション](#dynamic-media-renditions)

### 属性ベースのアクセス制御（ABAC） {#attribute-based-access-control}

Content Hubでは、アセットへのアクセスにルールベースの制限を適用できるようになりました。 アセット権限によりガバナンスが確保され、関連するアセットのみがユーザーからアクセスできるようになります。

アセット制限ルールはメタデータに基づいており、ルールで定義された条件がアセットメタデータに一致する場合、アセットはユーザーグループに表示されます。

属性ベースのアクセス制御の主なメリットには、次のようなものがあります。

* 権限に対するフォルダー構造への依存が排除される

* 管理者がアセットをアップロードし、遡及的に権限構造を決定できる

* 重複の数を減らす – アセットの整合性を向上させます。同じアセットが異なるグループと共有される場合は、フォルダーベースの権限で重複が必要になります。

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/attribute-based-access-control"}

### UI ブランディング {#ui-branding}

Content Hubのプライマリカラーとセカンダリカラーに加え、バナー画像、バナータイトル、本文テキストなど、ブランド固有の要素を使用してユーザーインターフェイスをカスタマイズできるようになりました。 これらの機能強化により、ブランドの一貫性の確保、ユーザーのオンボーディングの簡素化、信頼の構築が可能になります。

![UI ブランディング](/help/assets/assets/content-hub-ui-branding.png)

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

### 公開リンク共有 {#public-link-sharing}

Content Hubで共有可能なリンクの生成がサポートされるようになりました。これにより、アプリケーションにアクセスすることなく、外部ユーザーがアセットのメタデータを表示したり、アセットをダウンロードしたりできるようになりました。

![UI ブランディング](/help/assets/assets/public-and-private-link.png)

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

### 複数のアセットを ZIP としてダウンロード {#download-multiple-assets-as-zip}

また、Content Hubでは、選択したアセットとそのレンディションを、ファイル管理を簡素化する個別のファイルとしてダウンロードするのではなく、ZIP ファイルでダウンロードできるようになりました。

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

### Content Hubの Dynamic Media レンディション {#dynamic-media-renditions}

Content Hub ユーザーインターフェイス内から直接、すべての Dynamic Media プリセットレンディションおよびダウンロード用のスマート切り抜きにアクセスします。

![Dynamic Media レンディション](/help/assets/assets/dm-renditions-content-hub.png)

[!BADGE  この機能の詳細 ]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}
