---
title: コンテンツハブの新機能
description: 最近ローンチされたコンテンツハブの機能の一部について詳しく説明します
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: a7e847b70b02f8c7da880ac530792d56999035a6
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 58%

---

# コンテンツハブの新機能 {#whats-new-content-hub}

コンテンツハブは、Experience Manager Assets as a Cloud Service の一部として使用でき、組織とそのビジネスパートナーがオンブランドのコンテンツに簡単にアクセスできます。 これは、大規模なアクティベーション用のアセットの配布と、マーケティングの俊敏性を向上させるオンブランドのコンテンツバリアントの作成に焦点を当てています。

次のビデオでは、コンテンツハブの主な機能について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) および Assets as a Cloud Service には、250 人のコンテンツハブ制限付きユーザーが含まれます。 [Assets Prime](/help/assets/assets-prime.md) には、50 人のコンテンツハブ制限付きユーザーが含まれます。

## リリース日 {#release-date}

Content Hub機能リリース（2026.05.0）のリリース日は2026年5月28日（AEM as a Cloud Service リリースと同じ）です。 次回の機能リリース（2026.06.0）は2026年6月25日（PT）に予定されています。

## 2026年5月リリースの機能 {#may-2026-release-features}

**AI 検索**

AEM Assets Content Hubには、高度な検索機能であるAI 検索が搭載されました。これにより、キーワードマッチのみに依存することなく、ユーザークエリの背後にある意味と意図を理解できます。 AI 検索によって、単語、概念、ユーザーの意図の間の関係を把握することで、より正確でコンテキストに即した結果を得ることができます。 多言語クエリのサポート、誤字やタイプミスの処理、類義語の理解など、正確なメタデータ用語を使用しない場合でも適切なアセットを表示できます。

例えば、`Woman drinking coffee`を検索すると、`Lady`、`Girl`、`Latte`、`Cappuccino`などの関連用語でタグ付けされたアセットを返すこともできます。

管理者は、AI 検索検索または従来のキーワード検索のいずれかを選択して、「設定」メニューを使用して、Content HubのAI 検索を有効または無効にできます。


**カスタム並べ替えオプション**

Content Hubでは、管理者がContent Hub ホームページでカスタムメタデータフィールドをソートオプションとして有効にできるようになりました。 管理者は、デフォルトの並べ替えオプション（サイズ、変更、名前、関連性）に加えて、チャネル、地域、SKU、Campaignなどのビジネス固有のメタデータフィールドを設定して、ユーザーがより効果的に検索結果を整理できるようにすることができます。

**配信APIのアセット検索とダウンロードイベントのサポート**

AEM Assets Delivery APIは、アセット検索とアセットのダウンロードイベントをサポートするようになり、接続されたアプリケーションやエクスペリエンスをまたいでアセットが検出および使用される方法を追跡し、対応できるようになりました。 これらのイベントは、アセットの使用パターンの可視性を向上し、分析とレポートのワークフローをサポートします。また、外部システムや自動化プロセスとの統合を簡素化します。

イベント駆動型のインサイトにより、コンテンツエンゲージメントをより深く理解し、より連続性のあるデジタルアセットワークフローを構築することができます。 詳しくは、[API ドキュメント &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/asset_downloaded)を参照してください。

>[!IMPORTANT]
>
>これらの機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

## 2026年2月リリースの機能 {#february-2026-release-features}

**AEM Governance Agentを使用したContent Hubでの権限管理**

Content Hubでは、AEM Governance Agentにより、適切なユーザーのみが適切なアセットにタイミングよくアクセスできるようになります。 きめ細かい属性ベースの制御と使用権限を適用することで、機密コンテンツを保護しながら、安全なコラボレーションを可能にします。 これにより、コンプライアンスリスクの低減、ブランドの一貫性の強化、ワークフローの高速化を実現し、不正アクセスや悪用を心配することなく、自信を持ってアセットを共有し、再利用することができます。 こうしたセキュリティと柔軟性のバランスにより、組織全体の業務効率と信頼性が向上します。

![権限管理の概要](/help/ai-in-aem/agents/governance/assets/permission-management.png)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview#permission-and-digital-rights-management"}


## 2025年10月リリースの機能 {#october-2025-release-features}

**Content Hubのダウンロードエクスペリエンスの機能強化**

Content Hubでは、複数のアセットレンディションをフラット階層でダウンロードできるようになり、複数のフォルダーを移動する必要がなくなりました。 ダウンロード動作に関するユーザー設定が、セッション間で一貫したエクスペリエンスのために保持されるようになりました。 新しいアセットのダウンロード体験は、ダウンロードしたファイルの検索と整理が容易になるため、アセット管理を合理化し、効率性を向上させます。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

## 2025年9月リリースの機能 {#september-2025-release-features}

**コレクションをお気に入りにマーク**

Content Hubでコレクションをお気に入りとしてマークできるようになり、コレクションの整理と取得が簡単になりました。 お気に入りのコレクションを追加すると、Content Hubのホームページの「**[!UICONTROL お気に入り]**」タブから便利に利用できるようになります。

**クイックアクセス用にコレクションをピン留めする**

Content Hub管理者は、Content Hubでコレクションをピン留めして、すばやくアクセスできるようになりました。 ピン留めされたコレクションは、コレクションホームページの専用の&#x200B;**[!UICONTROL ピン留め]** セクションに表示され、重要なコレクションを手の届くところに保つことが簡単になります。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#pin-unpin-collection"}

## 2025年8月リリースの機能 {#august-release-features}

**フィルタープロパティ経由の一括検索**

コンテンツハブでは、必要なアセットをすばやく見つけることができるようになりました。 新しい一括検索機能を使用すると、任意のフィルタープロパティに複数の値（区切り文字で区切られた値、例えば、複数の SKU ID）を入力し、1 回の検索で一致するすべてのアセットを即座に取得できます。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#bulk-search"}

## 2025年7月リリースの機能 {#july-2025-release-features}

**コンテンツハブでのブランディングの柔軟性の強化**

既存のパーソナライゼーション機能を基に、コンテンツハブでは、管理者がカスタムロゴ画像を追加して、デプロイメントをさらにカスタマイズできるようになりました。 また、バナー画像とロゴ画像の両方で TIFF ファイル形式のサポートが追加され、より柔軟なデザインが可能になります。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

**タイトル付きリンクでよりスマートな共有**

共有リンクを生成する際に、アセットの詳細ビューからでも、1 つ以上のアセットを選択した後でも、タイトルを追加できるようになりました。 これにより、受信者は、特に複数の共有アセットを受け取った場合に、各リンクの目的を簡単に識別できます。

![プライベートリンクとパブリックリンク](/help/assets/assets/shared-link-for-assets.png)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

**フィルターナビゲーションの改善**

コンテンツハブのフィルター内に「**すべて表示**」オプションが含まれるようになりました。これにより、ユーザーは、最大 10 個のファセットのみの現在の表示制限から使用可能なすべてのファセットとアセット数を表示できます。 各フィルター内の検索機能と並べ替え機能が強化され、アセットをより効率的に検出および管理するのがより簡単になります。

## 2025年6月リリースの機能 {#june-2025-release-features}

### コレクションに関するガバナンス {#collections-governance}

コンテンツハブでは、作成中のコレクションへのアクセスを制御し、許可されたユーザーのみがグループ化されたアセットを表示または管理できるようになりました。 これにより、セキュリティの強化、共同作業の向上、組織的なアセット管理、ガバナンスの簡素化が実現します。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## 2025年5月リリースの機能 {#may-2025-release-features}

コンテンツハブの 5月リリースには、次の機能が含まれます。

* [属性ベースのアクセス制御](#attribute-based-access-control)

* [UI ブランディング](#ui-branding)

* [公開リンク共有](#public-link-sharing)

* [複数のアセットを ZIP としてダウンロードする](#download-multiple-assets-as-zip)

* [コンテンツハブにおける Dynamic Media のレンディション](#dynamic-media-renditions)

### 属性ベースのアクセス制御（ABAC） {#attribute-based-access-control}

コンテンツハブで、アセットへのアクセスについてルールベースの制限を適用できるようになりました。 アセット権限を使用すると、ガバナンスが確保され、ユーザーは関連するアセットにのみアクセスできるようになります。

アセット制限ルールはメタデータに基づいており、ルールで定義された条件がアセットメタデータに一致する場合、アセットはユーザーグループに表示されます。

属性ベースのアクセス制御の主なメリットには、次のようなものがあります。

* 権限に対するフォルダー構造への依存が排除される

* 管理者がアセットをアップロードし、遡及的に権限構造を決定できる

* 重複の数を減らす – アセットの整合性を向上させます。 同じアセットが異なるグループと共有される場合は、フォルダーベースの権限で重複が必要になります。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/attribute-based-access-control"}

### UI ブランディング {#ui-branding}

コンテンツハブでは、管理者がプライマリカラーとセカンダリカラーに加え、バナー画像、バナータイトル、本文などのブランド固有の要素を使用してユーザーインターフェイスをカスタマイズできます。 これらの機能強化により、ブランドの一貫性の確保、ユーザーのオンボーディングの簡素化、信頼の構築が可能になります。

![UI ブランディング](/help/assets/assets/content-hub-ui-branding.png)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

### 公開リンク共有 {#public-link-sharing}

コンテンツハブでは、外部のユーザーがアプリケーションにアクセスすることなくアセットのメタデータを表示したり、アセットをダウンロードしたりできるように共有可能なリンクを生成できるようになりました。

![UI ブランディング](/help/assets/assets/public-and-private-link.png)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

### 複数のアセットを ZIP としてダウンロードする {#download-multiple-assets-as-zip}

また、コンテンツハブではファイル管理を簡単にする個別のファイルとしてではなく、選択したアセットとそのレンディションを ZIP ファイルでダウンロードできるようになりました。

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

### コンテンツハブにおける Dynamic Media のレンディション {#dynamic-media-renditions}

すべての Dynamic Media プリセットレンディションおよびダウンロード用のスマート切り抜きには、コンテンツハブのユーザーインターフェイス内から直接アクセスできます。

![Dynamic Media レンディション](/help/assets/assets/dm-renditions-content-hub.png)

[!BADGE この機能の詳細情報]{type=Informative url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}
