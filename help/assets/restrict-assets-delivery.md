---
title: OpenAPI 機能を備えた Dynamic Media を使用したアセットの配信の制限
description: OpenAPI 機能を使用したアセットの配信の制限方法について説明します。
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 97%

---

# OpenAPI 機能を備えた Dynamic Media を使用したアセットの配信の制限 {#restrict-access-to-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager のアセットガバナンスを一元化すると、DAM 管理者またはブランドマネージャーは、OpenAPI 機能を備えた Dynamic Media を通じて使用可能なアセットへのアクセスを管理できます。AEM as a Cloud Service オーサーサービスでアセットの特定のメタデータを設定して、承認済みアセット（個別のアセットに至るまで）の配信を、選択した [Adobe Identity Management System（IMS）ユーザーまたはグループ](https://helpx.adobe.com/jp/enterprise/using/users.html#user-mgt-strategy)に制限できます。

OpenAPI を備えた Dynamic Media を通じてアセットを制限すると、該当するアセットへのアクセスが許可された（Adobe IMS オンボードの）ユーザーにのみアクセス権が付与されます。アセットにアクセスするには、ユーザーは OpenAPI を備えた Dynamic Media の[検索](search-assets-api.md)および[配信](deliver-assets-apis.md)の機能を活用する必要があります。

![アセットへの制限付きアクセス](/help/assets/assets/restricted-access.png)

Experience Manager Assets では、IMS 経由の制限付き配信には、次の 2 つの主要なステージが含まれます。

* オーサリング
* 配信

## オーサリング {#authoring}

### IMS ベアラートークンを使用した制限付き配信 {#restrict-delivery-ims-token}

IMS ユーザーおよびグループ ID に基づいて、[!DNL Experience Manager] 内でのアセットの配信を制限できます。

>[!NOTE]
>
この機能は現在セルフサービスではありません。IMS [ユーザー](https://helpx.adobe.com/jp/enterprise/using/manage-directory-users.html)および[グループ](https://helpx.adobe.com/jp/enterprise/using/user-groups.html)に対するアセット配信を制限するには、エンタープライズサポートチームにお問い合わせください。[Adobe Admin Console](https://adminconsole.adobe.com/) ポータルからアクセスを制限するために必要な情報を取得する方法と、AEM as a Cloud Service オーサーサービスでアクセスを設定する方法を紹介します。

### オン／オフの日時を使用したアセットの配信の制限 {#restrict-delivery-assets-date-time}

DAM 作成者は、アセットプロパティで使用可能なアクティベーションのオンタイムまたはオフタイムを定義して、アセットの配信を制限することもできます。

アセットのアクティベーションのオンタイムを定義すると、定義した時間にアセットの配信 URL が生成されます。アセットは、定義した時間まで非アクティブなままになります。同様に、アセットのオフタイムを定義すると、アセットは定義した時間にアクティベート解除され、アセットの配信 URL でアセットの表示が停止します。

アセットのオンタイムとオフタイムを設定するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 予定されているアクティベーション（アクティベート解除）]**」セクションで、要件に基づいてオンタイムまたはオフタイムを定義します。

同様に、アセットビューでアセットを選択し、「**[!UICONTROL 詳細]**」をクリックして、アセットのプロパティを表示し、オンタイムとオフタイムを定義できます。

このフィールドは、デフォルトのメタデータフォームで使用できます。アセットがデフォルトのメタデータスキーマに基づいておらず、アセットプロパティで「オンタイム」フィールドと「オフタイム」フィールドが使用できない場合は、管理ビューで次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. メタデータスキーマを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. 右側の「**[!UICONTROL フォームを作成]**」セクションからフォームの「メタデータ」セクションに「**[!UICONTROL 日付]**」フィールドを追加します。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]**&#x200B;パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]**&#x200B;を「**オンタイム**」または「**オフタイム**」に変更します。
   1. 「**[!UICONTROL プロパティにマッピング]**」を _../jcr:content/onTime_（「**オンタイム**」フィールドの場合）および _./jcr:content/offTime_（「**オフタイム**」フィールドの場合）に更新します。
1. 「**[!UICONTROL 保存]**」をクリックします。

同様に、アセットビューでは、アセットがデフォルトのメタデータスキーマに基づいておらず、アセットプロパティで「オンタイム」フィールドと「オフタイム」フィールドが使用できない場合は、次の手順を実行します。

1. 「**[!UICONTROL 設定]**」セクションで「**[!UICONTROL メタデータフォーム]**」をクリックします。
1. メタデータフォームを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. 左側のパネルの「**[!UICONTROL コンポーネント]**」セクションから「**[!UICONTROL 日付]**」フィールドをフォームに追加します。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL ラベル]**&#x200B;を「**オンタイム**」または「**オフタイム**」に変更します。
1. **[!UICONTROL メタデータプロパティ]**&#x200B;を _../jcr:content/onTime_（「**オンタイム**」フィールドの場合）および _./jcr:content/offTime_（「**オフタイム**」フィールドの場合）に更新します。
1. 「**[!UICONTROL 保存]**」をクリックします。



## 制限付きアセットの配信 {#delivery-restricted-assets}

制限付きアセットの配信は、アセットへのアクセスに対する正常な認証に基づいています。認証は、[IMS ベアラートークン](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/)（[AEM アセットセレクター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)から開始されたリクエストの申請）またはセキュア Cookie（AEM パブリッシュ／プレビューサービスにカスタム ID プロバイダーが設定され、ページでの Cookie の作成と組み込みが設定されている場合）を通じて行われます。

### AEM オーサーリクエストまたはアセットセレクターリクエストの配信 {#delivery-aem-author-asset-selector}

AEM オーサーサービスまたは AEM アセットセレクターからリクエストが送信された場合に制限付きアセットの配信を有効にするには、有効な IMS ベアラートークンが不可欠です。\
AEM Cloud Service オーサーサービスとアセットセレクターでは、ログインが成功すると、IMS ベアラートークンが自動的に生成され、リクエストに使用されます。

>[!NOTE]
>
AEM アセットセレクターベースの統合で IMS 認証を有効にする方法について詳しくは、エンタープライズサポートにお問い合わせください

1. アセットセレクターベース以外のエクスペリエンスの場合、AEM as a Cloud Service および OpenAPI 機能を備えた Dynamic Media では現在、サーバーサイド API 統合をサポートし、IMS ベアラートークンを生成できます。
   * [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) を通じて IMS ベアラートークンを取得できるサービスとサーバー間の API 統合を実行するには、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow)の手順に従ってください。
   * 期間限定のローカル開発者アクセス（実稼動ユースケースを意図したものではない）の場合、[AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) で認証されたユーザー用の短時間のみ有効な IMS ベアラートークンは、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)の手順に従って生成できます。

1. [検索](search-assets-api.md)および[配信](deliver-assets-apis.md)の API リクエストを行う際に、取得した IMS ベアラートークンを HTTP リクエストの&#x200B;**[!UICONTROL 認証]**&#x200B;ヘッダーに追加します（その値の先頭に&#x200B;**[!UICONTROL ベアラー]**&#x200B;が付いていることを確認します）。

1. アクセス制限を検証するには、**[!UICONTROL 認証]**&#x200B;ヘッダーの有無にかかわらず、配信の API リクエストを開始します。
   * IMS ベアラートークンが存在しない場合や、指定した IMS ベアラートークンがアセットへのアクセス権を付与されたユーザー（直接またはグループメンバーシップを通じて）に属していない場合、応答では `404` エラーステータスコードが生成されます。
   * IMS ベアラートークンがアセットへのアクセス権を付与されたユーザーまたはグループの 1 つである場合、応答ではアセットのバイナリコンテンツを含む `200` 成功ステータスコードが生成されます。

### パブリッシュサービスでのカスタム ID プロバイダーの配信 {#delivery-custom-identity-provider}

AEM Sites、AEM Assets、および OpenAPI ライセンスを備えた Dynamic Media を一緒に使用すると、AEM パブリッシュまたはプレビューサービスでホストされている web サイトでアセットの制限付き配信を設定できます。セキュリティ保護された配信フローでは、ブラウザーの Cookie を活用してユーザーのアクセスを確立します。このユースケースを実装するには、パブリッシュドメインのサブドメインである配信層のカスタムドメインを持つことが前提条件となります。AEM Sites のパブリッシュおよびプレビューサービスが[カスタム ID プロバイダー（IdP）](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)を使用するように設定されている場合、ユーザーの認証後にユーザーのグループメンバーシップをカプセル化する、`delivery-token` と呼ばれる新しい Cookie をパブリッシュドメインに設定する必要があります。配信層では、セキュリティ保護された Cookie から認証マテリアルを抽出し、アクセスを検証します。詳しくは、[エンタープライズサポートチケット](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)のログを参照してください。
