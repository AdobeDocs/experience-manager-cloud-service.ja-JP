---
title: OpenAPI 機能を使用したDynamic Mediaによるアセットの配信制限
description: OpenAPI 機能を使用してアセットの配信を制限する方法を説明します。
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 2%

---

# OpenAPI 機能を使用したDynamic Mediaによるアセットの配信制限 {#restrict-access-to-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Managerのアセットガバナンスの一元化により、DAM 管理者またはブランド管理者は、OpenAPI 機能を使用して、Dynamic Mediaを通じて使用可能なアセットへのアクセスを管理できます。 AEM as a Cloud Service オーサーサービスでアセットに特定のメタデータを設定することで ](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy) 選択した [AdobeのIdentity Management System （IMS）ユーザーまたはグループに（個々のアセットに対して）承認済みアセットの配信を制限できます。

OpenAPI を使用したDynamic Mediaによってアセットが制限されると、そのアセットへのアクセスを許可された（Adobe IMSがオンボーディングされた）ユーザーにのみアクセスが許可されます。 アセットにアクセスするには、OpenAPI でDynamic Mediaの [ 検索 ](search-assets-api.md) 機能と [ 配信 ](deliver-assets-apis.md) 機能を活用する必要があります。

![ アセットへの制限付きアクセス ](/help/assets/assets/restricted-access.png)

Experience Manager Assetsでは、IMS を介した配信制限には、次の 2 つの重要な段階が含まれます。

* オーサリング
* 配信

## オーサリング {#authoring}

### IMS ベアラートークンを使用した制限付き配信 {#restrict-delivery-ims-token}

IMS ユーザーおよびグループ ID に基づいて、[!DNL Experience Manager] 内のアセットの配信を制限できます。

>[!NOTE]
>
この機能は、現在、セルフサービスではありません。 IMS[ ユーザー ](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html) および [ グループ ](https://helpx.adobe.com/in/enterprise/using/user-groups.html) にアセット配信を制限するには、[Adobe Admin Console](https://adminconsole.adobe.com/) ポータルからアクセス制限に必要な情報を取得する方法と、AEM as a Cloud Service オーサーサービスでアクセスを設定する方法について、エンタープライズサポートチームにお問い合わせください。

### オンおよびオフの日時を使用したアセットの配信制限 {#restrict-delivery-assets-date-time}

DAM 作成者は、アセットプロパティで使用できるアクティベーションのオンタイムまたはオフタイムを定義して、アセットの配信を制限することもできます。

アセットのアクティベーションに「オンタイム」を定義すると、定義した時間にアセットの配信 URL が生成されます。 アセットは、定義された時間が経過するまでは非アクティブのままとなります。 同様に、アセットに「オフタイム」を定義した場合、アセットは定義された時間に非アクティブ化され、アセットの配信 URL はアセットの表示を停止します。

次の手順を実行して、アセットのオンタイムとオフタイムを設定します。

1. アセットを選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 予定（非スケジュール）アクティベーション]**」セクションで、要件に基づいて「オンタイム」または「オフタイム」を定義します。

同様に、Assets ビューでも、アセットを選択して **[!UICONTROL 詳細]** をクリックすると、アセットのプロパティが表示され、「オンタイム」と「オフタイム」を定義できます。

このフィールドは、デフォルトのメタデータフォームで使用できます。 アセットがデフォルトのメタデータスキーマに基づいておらず、アセットプロパティで「オンタイム」フィールドと「オフタイム」フィールドを使用できない場合は、管理表示で次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. メタデータスキーマを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. フォームのメタデータセクションの右側にある **[!UICONTROL フォームを作成]** セクションから **[!UICONTROL 日付]** フィールドを追加します。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]** パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]** を **オンタイム** または **オフタイム** に変更します。
   1. **[!UICONTROL プロパティにマッピング]** を _に更新します。「/On Time_」フィールドと _の&#x200B;**jcr:content/onTime**。「オフタイム_ フィールドの場合は **jcr:content/offTime** です。
1. 「**[!UICONTROL 保存]**」をクリックします。

同様に、Assets ビューで、アセットがデフォルトのメタデータスキーマに基づいておらず、アセットのプロパティで「オンタイム」フィールドと「オフタイム」フィールドを使用できない場合は、次の手順を実行します。

1. **[!UICONTROL 設定]** セクションの **[!UICONTROL メタデータForms]** をクリックします。
1. メタデータフォームを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. 左側のペインの **[!UICONTROL コンポーネント]** セクションから **[!UICONTROL 日付]** フィールドをフォームに追加します。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL ラベル]** を **オンタイム** または **オフタイム** に変更します。
1. **[!UICONTROL メタデータプロパティ]** を _に更新します。「/On Time_」フィールドと _の&#x200B;**jcr:content/onTime**。「オフタイム_ フィールドの場合は **jcr:content/offTime** です。
1. 「**[!UICONTROL 保存]**」をクリックします。



## 制限付きアセットの配信 {#delivery-restricted-assets}

制限付きアセットの配信は、アセットへのアクセスが正常に許可されるかどうかに基づいて行われます。 認証は、[IMS ベアラートークン ](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/) （[AEM アセットセレクター ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector) から開始されたリクエストの申請）またはセキュア cookie を使用して行います（AEM Publish/プレビューサービスでカスタム ID プロバイダーを設定しており、ページで cookie の作成と包含を設定している場合）。

### AEM オーサーリクエストまたはアセットセレクターリクエストの配信 {#delivery-aem-author-asset-selector}

AEM オーサーサービスまたはAEM アセットセレクターからリクエストが送信された場合に制限付きアセットの配信を有効にするには、有効な IMS ベアラートークンが必要です。\
AEM Cloud Service オーサーサービスおよびアセットセレクターでは、IMS ベアラートークンが自動的に生成され、ログイン成功後のリクエストに使用されます。

>[!NOTE]
>
AEM Asset Selector ベースの統合で IMS 認証を有効にする方法について詳しくは、エンタープライズサポートにお問い合わせください

1. アセットセレクターベース以外のエクスペリエンスの場合、OpenAPI 機能を備えたAEM as a Cloud ServiceおよびDynamic Mediaは現在、サーバーサイド API 統合をサポートし、IMS ベアラートークンを生成できます。
   * [2](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow)AEM as a Cloud Service Developer Consoleを介して IMS ベアラートークンを取得できるサービス間 API 統合を実行するには、](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) こちら } の手順に従います。[
   * 期間限定で、（実稼動のユースケース向けではなく）ローカル開発者アクセス、[AEM as a Cloud Service Developer Consoleで認証されたユーザーの短時間のみ有効な IMS ベアラートークンを ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) 手順に従って生成できます。[ こちら ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)

1. [Search](search-assets-api.md) および [Delivery](deliver-assets-apis.md) API リクエストを行う際に、取得した IMS ベアラートークンを HTTP リクエストの **[!UICONTROL Authorization]** ヘッダーに追加します（その値に **[!UICONTROL Bearer]** というプレフィックスが付いていることを確認します）。

1. アクセス制限を検証するには、**[!UICONTROL Authorization]** ヘッダーを含める場合と含めない場合の配信 API リクエストを開始します。
   * IMS ベアラートークンがない場合や、指定された IMS ベアラートークンがアセットへのアクセス権を付与されたユーザーに属していない場合（直接またはグループメンバーシップを通じて）、応答は `404` しいエラーステータスコードを生成します。
   * IMS ベアラートークンがアセットへのアクセスを許可されたユーザーまたはグループの 1 つである場合、応答はアセットのバイナリコンテンツを含んだ `200` 成功ステータスコードを生成します。

### Publish サービスでのカスタム ID プロバイダーの配信 {#delivery-custom-identity-provider}

OpenAPI ライセンスを持つAEM Sites、AEM Assets、Dynamic Mediaを一緒に使用できるので、AEM Publishまたはプレビューサービスでホストされている web サイトで、アセットの配信制限を設定できます。 セキュア配信フローでは、ブラウザー Cookie を利用してユーザーのアクセスを確立します。このユースケースを実装するには、配信層用のカスタムドメインがパブリッシュドメインのサブドメインになっている必要があります。 AEM SitesのPublishおよびプレビューサービスが [ カスタム ID プロバイダー（IdP） ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) を使用するように設定されている場合、ユーザーのグループメンバーシップをカプセル化す `delivery-token` と呼ばれる新しい Cookie を、公開ドメインの投稿ユーザーの認証で設定する必要があります。 配信層は、セキュア cookie から認証内容を抽出し、アクセスを検証します。 詳しくは、[ エンタープライズサポートチケット ](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities) をログに記録してください。
