---
title: Experience Managerでのアセットの配信を制限
description: ' [!DNL Experience Manager] でアセット配信を制限する方法を説明します。'
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 2%

---

# [!DNL Experience Manager] のアセットへのアクセス制限 {#restrict-access-to-assets}

| [ 検索のベストプラクティス ](/help/assets/search-best-practices.md) | [ メタデータのベストプラクティス ](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えたDynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開発者向けドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Managerの中央アセットガバナンスを使用すると、DAM 管理者またはブランド管理者がアセットへのアクセスを管理できます。 オーサリング側、特にAEM as a Cloud Service オーサーインスタンスで承認済みアセットの役割を設定することで、アクセスを制限できます。

ユーザー [ 検索 ](search-assets-api.md) または [ 配信 URL](deliver-assets-apis.md) の利用は、認証プロセスを正常に渡すと、制限付きアセットにアクセスできます。

![ アセットへの制限付きアクセス ](/help/assets/assets/restricted-access.png)

## IMS トークンを使用した制限付き配信 {#restrict-delivery-ims-token}

Experience Manager Assetsでは、IMS を介した配信制限には、次の 2 つの重要な段階が含まれます。

* オーサリング
* 配信

### オーサリング {#authoring}

[!DNL Experience Manager] 内のアセットの配信を役割に基づいて制限できます。 役割を設定するには、次の手順を実行します。

1. DAM 管理者として [!DNL Experience Manager] に移動します。
1. 役割を設定する必要があるアセットを選択します。
1. **[!UICONTROL プロパティ]**/**[!UICONTROL 詳細]** に移動し、「**[!UICONTROL 詳細メタデータ]**」タブに [!UICONTROL  役割 ] フィールドが存在することを確認します。

   ![ 役割メタデータ ](/help/assets/assets/roles_metadata.jpg)
フィールドが使用できない場合は、次の手順を使用してフィールドを追加します。

   1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
   1. メタデータスキーマを選択し、「**[!UICONTROL 編集 _（e）_]**」をクリックします。
   1. フォームのメタデータセクションの右側にある **[!UICONTROL フォームを作成]** セクションから **[!UICONTROL 複数値テキスト]** フィールドを追加します。
   1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]** パネルで次の更新を行います。
      1. **[!UICONTROL フィールドラベル]** を _役割_ に変更します。
      1. **[!UICONTROL プロパティにマッピング]** を _に更新します。/jcr:content/metadata/dam:roles_ です。

1. アセットの役割メタデータに追加する IMS グループを取得します。 IMS グループを取得するには、次の手順に従います。
   1. `https://adminconsole.adobe.com/.` でログイン
   1. それぞれの組織に移動し、**[!UICONTROL ユーザーグループ]** に移動します。
   1. 追加する **[!UICONTROL ユーザーグループ]** を選択し、URL から **[!UICONTROL orgID]** と **[!UICONTROL userGroupID]** を抽出するか、`{orgID}@AdobeOrg:{usergroupID}` などの組織 ID を使用します。

1. グループ ID をアセットプロパティの **[!UICONTROL 役割]** フィールドに追加します。 <br>
「**[!UICONTROL 役割]**」フィールドで定義されたグループ ID は、アセットにアクセスできる唯一のユーザーです。 IMS グループ ID 以外にも、「**[!UICONTROL 役割]**」フィールドに IMS ユーザー ID と IMS プロファイル ID を追加できます。 例えば、`{orgId}@AdobeOrg:{profileId}` のように指定します。

   >[!NOTE]
   >
   >新しいAssets ビューでは、個々のユーザーではなく、フォルダーレベルまで、そしてグループにのみアクセス権を付与できます。 詳しくは、[Experience Manager Assets内での権限の管理 ](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions) を参照してください。

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### オンおよびオフの日時を使用したアセットの配信制限 {#restrict-delivery-assets-date-time}

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



### 制限付きアセットの配信 {#delivery-restricted-assets}

制限付きアセットの配信は、アセットへのアクセスが正常に許可されるかどうかに基づいて行われます。 認証は、AEM オーサーインスタンスまたはアセットセレクターからリクエストが送信された場合は IMS トークンに基づき、Publishまたはプレビューインスタンスにカスタム ID プロバイダーが設定されている場合は特別な Cookie に基づいています。

#### AEM オーサーリクエストまたはアセットセレクターリクエストの配信 {#delivery-aem-author-asset-selector}

AEM オーサーインスタンスやアセットセレクターからリクエストが送信された場合に制限付きアセットの配信を有効にするには、有効な IMS トークンが必要です。 次の手順に従います。

1. [ アクセストークンの生成 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)。
   * AEM as a Cloud Service環境の開発コンソールにログインします。

   * **[!UICONTROL Environment]**/**[!UICONTROL Integrations]**/**[!UICONTROL ローカルトークン]**/**[!UICONTROL ローカル開発トークンの取得]**/**[!UICONTROL accessToken 値をコピー]** に移動します。 [ トークンへのアクセス方法と関連する側面 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) について説明します。

1. 取得したアクセストークンを **[!UICONTROL Authorization]** ヘッダーに統合し、その値に **[!UICONTROL Bearer]** というプレフィックスが付いていることを確認します。

1. リクエストを開始して、アクセストークンの機能を検証します。 IMS アクセストークンがない場合や、提供されたアクセストークンにアセットのメタデータに追加されたものと同じプリンシパルまたはグループがない場合は、404 エラーが発生します。

#### Publish インスタンスのカスタム ID プロバイダーの配信 {#delivery-custom-identity-provider}

Publishまたはプレビューインスタンスで設定されたカスタム ID プロバイダーの場合、セットアッププロセス中に、属性内の保護されたアセットへのアクセス権を持つ必要があ `groupMembership` グループを指定できます。 [SAML 統合 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) を介してカスタム ID プロバイダーにログオンすると、`groupMembership` 属性が読み取られ、Cookie が作成するために使用されます。この Cookie は、認証用のすべてのリクエストで送信されます。AEM オーサーまたはアセットセレクターからのリクエストの場合は IMS トークンと同様です。

セキュリティで保護されたアセットがページで使用可能で、アセットをレンダリングするためのリクエストが配信 URL に対して行われると、AEMは cookie または IMS トークンに存在するロールを確認し、アセットのオーサリング中に適用される `dam:roles property` と照合します。 一致する場合は、アセットが表示されます。

>[!NOTE]
>
> [OpenAPI 機能を使用してDynamic Mediaをアクティブ化するためのサポートチケット ](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities) で、ユースケースに制限付き配信を指定します。 Adobeエンジニアリングは、必要な説明や、制限付き配信のプロセスの設定を支援します。
