---
title: Experience Managerでのアセットの配信を制限
description: でのアセット配信を制限する方法を説明します [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 1%

---

# でのアセットへのアクセス制限 [!DNL Experience Manager] {#restrict-access-to-assets}

Experience Managerの中央アセットガバナンスを使用すると、DAM 管理者またはブランド管理者がアセットへのアクセスを管理できます。 オーサリング側、特にAEM as a Cloud Service オーサーインスタンスで承認済みアセットの役割を設定することで、アクセスを制限できます。

ユーザー [検索](search-assets-api.md) または利用する [配信 URL](deliver-assets-apis.md) は、認証プロセスを正常に渡した際に、制限付きアセットにアクセスできます。

![アセットへの制限付きアクセス](/help/assets/assets/restricted-access.png)

## IMS トークンを使用した制限付き配信 {#restrict-delivery-ims-token}

Experience Managerとして、IMS による配信制限には、次の 2 つの重要な段階が含まれます。

* オーサリング
* 配信

### オーサリング {#authoring}

内でのアセットの配信を制限できます [!DNL Experience Manager] の役割に基づいています。 役割を設定するには、次の手順を実行します。

1. に移動します [!DNL Experience Manager] dam 管理者です。
1. 役割を設定する必要があるアセットを選択します。
1. に移動します。 **[!UICONTROL プロパティ]** > **[!UICONTROL 詳細]**&#x200B;を選択し、以下を行います **[!UICONTROL 役割]** フィールドがに存在する [!UICONTROL 詳細メタデータ] タブ。

   ![役割メタデータ](/help/assets/assets/roles_metadata.jpg)
フィールドが使用できない場合は、次の手順を使用してフィールドを追加します。

   1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
   1. メタデータスキーマを選択し、 **[!UICONTROL 編集 _ホ_]**.
   1. を追加 **[!UICONTROL 複数値テキスト]** からのフィールド **[!UICONTROL フォームを作成]** フォームの「メタデータ」セクションの右側のセクションです。
   1. 新しく追加されたフィールドをクリックし、で次の更新を行います  **[!UICONTROL 設定]** パネル：
      1. 変更： **[!UICONTROL フィールドラベル]** 対象： _役割_.
      1. を更新 **[!UICONTROL プロパティにマッピング]** 対象： _./jcr:content/metadata/dam:roles_.

1. アセットの役割メタデータに追加する IMS グループを取得します。 IMS グループを取得するには、次の手順に従います。
   1. https://adminconsole.adobe.com/でログインします。
   1. 各組織に移動して、次に移動します **[!UICONTROL ユーザーグループ]**.
   1. 「」を選択します **[!UICONTROL ユーザーグループ]** を追加し、抽出する必要があります **[!UICONTROL orgID]** および **[!UICONTROL userGroupID]** url から、または次のような組織 ID を使用します `{orgID}@AdobeOrg:{usergroupID}`.

1. グループ ID をに追加します **[!UICONTROL 役割]** アセットプロパティのフィールド。 <br>
で定義されたグループ ID **[!UICONTROL 役割]** フィールドは、アセットにアクセスできる唯一のユーザーです。 では、IMS クライアント ID および IMS プロファイル ID も追加できます。 **[!UICONTROL 役割]** フィールド。 例えば、`{orgId}@AdobeOrg:{profileId}` のように指定します。

   >[!NOTE]
   >
   >新しいAssets ビューでは、個々のユーザーではなく、フォルダーレベルまで、そしてグループにのみアクセス権を付与できます。 の詳細情報 [Experience Manager Assets内での権限の管理](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### オンおよびオフの日時を使用したアセットの配信制限 {#restrict-delivery-assets-date-time}

DAM 作成者は、アセットプロパティで使用できるアクティベーションのオンタイムまたはオフタイムを定義して、アセットの配信を制限することもできます。

アセットのアクティベーションに「オンタイム」を定義すると、定義した時間にアセットの配信 URL が生成されます。 アセットは、定義された時間が経過するまでは非アクティブのままとなります。 同様に、アセットに「オフタイム」を定義した場合、アセットは定義された時間に非アクティブ化され、アセットの配信 URL はアセットの表示を停止します。

次の手順を実行して、アセットのオンタイムとオフタイムを設定します。

1. アセットを選択し、 **[!UICONTROL プロパティ]**.

1. が含まれる **[!UICONTROL スケジュールされた（非）アクティブ化]** の節 **[!UICONTROL 基本]** タブで、要件に基づいて「オンタイム」または「オフタイム」を定義します。

同様に、Assets ビューで、アセットを選択し、 **[!UICONTROL 詳細]** アセットのプロパティを表示し、オンタイムとオフタイムを定義します。

このフィールドは、デフォルトのメタデータフォームで使用できます。 アセットがデフォルトのメタデータスキーマに基づいておらず、アセットプロパティで「オンタイム」フィールドと「オフタイム」フィールドを使用できない場合は、管理表示で次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. メタデータスキーマを選択し、 **[!UICONTROL 編集]**.
1. を追加 **[!UICONTROL 日付]** からのフィールド **[!UICONTROL フォームを作成]** フォームの「メタデータ」セクションの右側のセクションです。
1. 新しく追加されたフィールドをクリックし、で次の更新を行います  **[!UICONTROL 設定]** パネル：
   1. 変更： **[!UICONTROL フィールドラベル]** 対象： **オンタイム** または **オフタイム**.
   1. を更新 **[!UICONTROL プロパティにマッピング]** 対象： _./jcr:content/onTime_ （用） **オンタイム** フィールドと _./jcr:content/offTime_ （用） **オフタイム** フィールド。
1. 「**[!UICONTROL 保存]**」をクリックします。

同様に、Assets ビューで、アセットがデフォルトのメタデータスキーマに基づいておらず、アセットのプロパティで「オンタイム」フィールドと「オフタイム」フィールドを使用できない場合は、次の手順を実行します。

1. クリック **[!UICONTROL メタデータForms]** が含まれる **[!UICONTROL 設定]** セクション。
1. メタデータフォームを選択し、 **[!UICONTROL 編集]**.
1. を追加 **[!UICONTROL 日付]** からのフィールド **[!UICONTROL Components]** 左側のウィンドウのセクションからフォームへ。
1. 新しく追加されたフィールドをクリックし、 **[!UICONTROL ラベル]** 対象： **オンタイム** または **オフタイム**.
1. を更新 **[!UICONTROL メタデータプロパティ]** 対象： _./jcr:content/onTime_ （用） **オンタイム** フィールドと _./jcr:content/offTime_ （用） **オフタイム** フィールド。
1. 「**[!UICONTROL 保存]**」をクリックします。



### 制限付きアセットの配信 {#delivery-restricted-assets}

制限付きアセットの配信は、アセットへのアクセスが正常に許可されるかどうかに基づいて行われます。 認証は、AEM オーサーインスタンスまたはアセットセレクターからリクエストが送信された場合は IMS トークンに基づき、Publishまたはプレビューインスタンスにカスタム ID プロバイダーが設定されている場合は特別な Cookie に基づいています。

#### AEM オーサーリクエストまたはアセットセレクターリクエストの配信 {#delivery-aem-author-asset-selector}

AEM オーサーインスタンスやアセットセレクターからリクエストが送信された場合に制限付きアセットの配信を有効にするには、有効な IMS トークンが必要です。 次の手順に従います。

1. [アクセストークンの生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * AEM as a Cloud Service環境の開発コンソールにログインします。

   * に移動します。 **[!UICONTROL 0.5511122]** > **[!UICONTROL 統合]** > **[!UICONTROL ローカルトークン]** > **[!UICONTROL ローカル開発トークンを取得]** > **[!UICONTROL accessToken 値をコピー]**. の詳細情報 [トークンと関連する側面へのアクセス方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. 取得したアクセストークンをに統合 **[!UICONTROL 認証]** ヘッダー、その値の先頭にが付いていることを確認する **[!UICONTROL ベアラー]**.

1. リクエストを開始して、アクセストークンの機能を検証します。 IMS アクセストークンがない場合や、提供されたアクセストークンにアセットのメタデータに追加されたものと同じプリンシパルまたはグループがない場合は、404 エラーが発生します。

#### Publish インスタンスのカスタム ID プロバイダーの配信 {#delivery-custom-identity-provider}

Publishまたはプレビューインスタンスで設定されたカスタム ID プロバイダーの場合、セキュリティで保護されたアセットにアクセスできる必要があるグループを指定できます `groupMembership` セットアッププロセス中の属性。 次を経由してカスタム ID プロバイダーにログオンしたとき [SAML 統合](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), `groupMembership` 属性は読み取られて cookie を作成するために使用されます。これは、AEM オーサーまたはアセットセレクターからのリクエストの場合に IMS トークンと同様に、認証のすべてのリクエストで送信されます。

セキュリティで保護されたアセットがページで使用可能で、アセットをレンダリングするためのリクエストが配信 URL に対して行われると、AEMは cookie または IMS トークンに存在するロールを確認し、それに対して照合します `dam:roles property` アセットのオーサリング中に適用されます。 一致する場合は、アセットが表示されます。

>[!NOTE]
>
> が含まれる [openapi 機能を使用してDynamic Mediaをアクティブ化するためのサポートチケット](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities)ユースケースでは、制限付き配信に言及してください。 Adobeエンジニアリングは、必要な説明や、制限付き配信のプロセスの設定を支援します。
