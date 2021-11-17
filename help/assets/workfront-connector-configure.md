---
title: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
description: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
role: Admin
feature: Integrations
source-git-commit: 6923f3d63bf9b1c24f70e50548b4fb0c13f0cd88
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 0%

---


# [!DNL Workfront for Experience Manager enhanced connector] の設定 {#assets-integration-overview}

で管理者アクセス権を持つユーザー [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 拡張コネクタをインストール後に設定します。 のインストール手順については、 [コネクタのインストール](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>Adobeには、 [!DNL Adobe Workfront for Experience Manager enhanced connector] 認定パートナーまたは [!DNL Adobe Professional Services]. 認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobeではサポートされません。
>
>Adobeが次の更新をリリースする可能性がある： [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] このコネクタを冗長にするこの場合、お客様はこのコネクタの使用から移行する必要が生じる場合があります。

## イベント購読の設定 {#event-subscriptions}

イベント購読は、AEMに対して、 [!DNL Adobe Workfront]. 三つある [!DNL Workfront for Experience Manager enhanced connector] 機能を動作させるには、イベントサブスクリプションが必要な機能を次に示します。

* プロジェクトにリンクされたフォルダーの自動作成。
* Workfrontドキュメントのカスタムフォーム値の変更をAEMアセットメタデータに同期します。
* プロジェクトの完了時にBrand Portalにアセットを自動的に公開する。

これらの機能を使用するには、イベント購読を有効にします。

* 編集 [!UICONTROL Workfront Tools] Cloud Servicesの設定は手順 5 で作成し、 [!UICONTROL イベント購読] タブをクリックします。
* を選択します。 [!UICONTROL Workfront Custom Integration] セクション 6 で作成した手順です。
* クリック [!UICONTROL Workfrontイベント購読の有効化].

   ![イベント購読](/help/assets/assets/event-subs.png)

## リンクされたフォルダーの設定 {#linked-folders}

イベントを購読するには、次の手順に従います。

1. 次に移動： **[!UICONTROL イベント購読]** 」タブをクリックします。
1. で作成したカスタム統合を選択 [!DNL Workfront].
1. クリック **[!UICONTROL Workfrontイベント購読の有効化]**.

### リンクされたフォルダー構造の設定 {#linked-folder-structure}

1. クラウドサービスの「プロジェクトにリンクされたフォルダー」タブに移動します。
1. リンクされたフォルダーの親パス：DAM 内で、リンクされたフォルダーを作成するフォルダーを選択します。 空のままにすると、デフォルトで/content/dam に設定されます。 WorkfrontツールのメタデータスキーマとWorkfrontリンクフォルダーのメタデータスキーマが、選択したフォルダーに適用されていることを確認します。
1. リンクされたフォルダー構造：コンマ区切り値を入力します。 各値は `DE:<some-project-custom-form-field>`、Portfolio、プログラム、年、名前、または「リテラル文字列値」（最後の 1 つは引用符） 現在は、Portfolio、プログラム、年、DE：プロジェクトの種類、名前に設定されています。
1. Workfrontのフォルダーのタイトルに構造内のすべてのフォルダーを含める必要がある場合は、「フォルダー構造名を使用してWorkfrontでリンクされたフォルダーのタイトルを作成」チェックボックスをオンにする必要があります。 それ以外の場合は、最後のフォルダーのタイトルになります。
1. 「サブフォルダー」マルチフィールドでは、リンクされたフォルダーの子フォルダーとして作成するフォルダーのリストを指定できます。
1. プロジェクトのステータス：リンクされたフォルダーを作成するためにプロジェクトを設定する必要があるステータスを選択します。
1. ポートフォリオを含むプロジェクトで、リンクされたフォルダーを作成します。リンクされたPortfolioーを作成するためにプロジェクトが属する必要があるフォルダーのリスト。 この一覧を空のままにして、すべてのプロジェクトポートフォリオのリンクフォルダを作成します。
1. カスタムフォームフィールドを含む、プロジェクト内にリンクされたフォルダーを作成します。リンクされたフォルダーを作成するためにプロジェクトで必要となるカスタムフォームフィールドと、それに対応する値。 この設定は、空のままにした場合は無視されます。 選択 `CUSTOM FORMS: Create DAM Linked Folder` フィールドと入力 `Yes` 値の
1. 「リンクされたフォルダーの自動作成を有効にする」をクリックします。 「イベントの購読」タブに戻ると、作成イベントが 1 つ表示されます。

![リンクされたフォルダー設定](/help/assets/assets/wf-linked-folder-config.png)

## メタデータスキーマのマッピング {#metadata-schema-mapping}

### フォルダーメタデータマッピングの設定 {#folder-metadata-mapping}

WorkfrontプロジェクトとAEMフォルダー間のメタデータマッピングは、AEMフォルダーメタデータスキーマ内で定義されます。 フォルダーメタデータスキーマは、AEMで通常どおりに作成および設定する必要があります。 Workfrontツールにより、各フォルダーメタデータスキーマフォームフィールドの「設定」設定タブにオートコンプリートドロップダウンが追加されます。 このオートコンプリートドロップダウンメニューを使用すると、各AEMフォルダープロパティのマッピング先のWorkfrontフィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL フォルダーメタデータスキーマ]**.
1. 編集するフォルダーメタデータスキーマフォームを選択し、「編集」をクリックします。
1. 編集するフォルダーメタデータスキーマフォームフィールドを選択し、右側のパネルの「設定」タブを選択します。
1. In [!UICONTROL Workfrontフィールドからマッピング済み] 「 」フィールドで、選択したAEMフォルダープロパティにマッピングするWorkfrontフィールドの名前を選択します。 次のオプションを使用できます。

   * プロジェクトのカスタムフォームフィールド
   * 「プロジェクト概要」フィールド (ID、名前、説明、参照番号、計画完了日、プロジェクト所有者、プロジェクトスポンサー、Portfolio、プログラム )

![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### アセットメタデータマッピングの設定 {#asset-metadata-mapping}

Adobe Workfrontドキュメントとアセット間のメタデータマッピングは、AEMメタデータスキーマ内で定義されます。 メタデータスキーマは、AEMで通常どおりに作成および設定する必要があります。 Workfrontツールは、各メタデータスキーマフォームフィールドの「設定」設定タブに設定オプションを追加します。 これらのオプションを使用すると、各AEMプロパティのマッピング先となるWorkfrontフィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. に移動します。 **ツール** > **Assets** > **メタデータスキーマ**.
1. 編集するメタデータスキーマフォームを選択し、 **編集** または、新しいメタデータスキーマを最初から作成します。
1. 編集するメタデータスキーマフォームフィールドを選択し、「 」を選択します。 **設定** 」タブをクリックします。
1. In [!DNL Workfront] カスタムフォームフィールド： [!DNL Workfront] 選択したAEMプロパティにマッピングするフィールド。 次のオプションを使用できます。

   * ドキュメントのカスタムフォームフィールド
   * プロジェクトのカスタムフォームフィールド
   * カスタムフォームフィールドの発行
   * タスクのカスタムフォームフィールド
   * プロジェクトの概要フィールド（ID、名前、説明、参照番号）

1. 例えば、 [!DNL Workfront] 選択されたフィールド [!UICONTROL Workfrontカスタムフォームフィールド] はWorkfront User type-ahead フィールドです。マッピングするWorkfrontユーザーフィールドを指定する必要があります。 これをおこなうには、「 Workfrontの参照オブジェクトから値を取得」フィールドにチェックを入れ、 [!UICONTROL Workfrontユーザーカスタムフォームフィールド] マッピングする値の取得元。

   ![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## Map プロパティ {#map-property}

このワークフローステップでは、ユーザーがプロパティを [!DNL Workfront] プロジェクト、タスク、タスク、イシュー、またはドキュメントのカスタムフォーム。 この [!DNL Workfront] アーティファクトこの手順の影響は、ペイロードからの相対パスを使用して検索されます。 マッピングするプロパティは、ステップダイアログ設定内で制御します。

**タイプ**:このフィールドでは、プロパティのマッピング先のWorkfrontオブジェクトタイプを選択できます。

**ID プロパティ**:このフィールドでは、プロパティのマッピング先のWorkfrontオブジェクト ID へのパスを指定できます。 このフィールドで指定するパスは、ワークフローペイロードを基準とした相対パスにする必要があります。

**プロパティの割り当て**:このマルチフィールドを使用すると、AEMプロパティとWorkfrontフィールド間のマッピングを指定できます。 複数フィールドの各項目は、1 つのマッピングを指定します。 各マッピングは、 `<workfront-field>=<aem-mapped-property>`.

* この `workfront-field` は

   * プレフィックスで識別されるカスタムフォームフィールド `DE:`.
   * 名前で識別される編集可能なフィールド。 フィールド名は、 [[!DNL Workfront] API エクスプローラー](https://experience.workfront.com/s/api-explorer).

* この `aem-mapped-property` は次のいずれかになります。

   * リテラル値。 これらは引用符で囲む必要があります。
   * AEMプロパティ。 この参照は、ワークフローペイロードに対する相対参照にする必要があります。
   * 名前付きの値。 これらは角括弧で囲む必要があります。
   * 上記の 3 つの項目を連結したもの。 次を使用して指定 `{+}`.
   * 上記 3 項目の変更は、値を `{replace(<value>,”old-char”,”new-char”)}`.

* 次に例を示します。

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![プロパティをマッピングするための設定](/help/assets/assets/wf-map-property-config.png)

## ステータスを設定 {#set-status}

ワークフローエディターで、 **[!UICONTROL Workfront — ステータスの設定]** 内 **[!UICONTROL 引数]** タブをクリックします。

![ワークフローを編集してステータスを設定](/help/assets/assets/wf-set-status.png)

## コメントの同期 {#comments-sync}

1. In [!DNL Experience Manager]，アクセス **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**、設定を選択し、「 」を選択します。 **[!UICONTROL プロパティ]**.

   ![コメント同期](/help/assets/assets/comments-sync1.png)

1. 選択 **[!UICONTROL イベント購読]** タブ、クリック **[!UICONTROL コメント同期の有効化]** オン **[!UICONTROL WorkfrontでおこなったコメントをAEMに送信]** オプション。

   ![同期が有効になっています](/help/assets/assets/wf-comment-sync-enabled.png)

WorkfrontからAEMへのコメントの同期をテストするには、次の手順に従います。

1. Workfrontでリンクされたドキュメントに移動し、「更新」タブでコメントを追加します。

   ![Workfrontにコメントを残す](/help/assets/assets/comments-sync2.png)

1. AEM内の同じリンク先ドキュメントに移動し、そのドキュメントを選択して、 [!UICONTROL タイムライン] オプションを選択し、 [!UICONTROL コメント]. 左側のサイドバーには、同期元のコメントが表示されます。 [!DNL Workfront].

## アセットのバージョン {#asset-versions}

AEMでアセットのバージョン履歴を管理するには、AEMでアセットのバージョン管理を設定します。

1. Experience Managerで、 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**&#x200B;をクリックし、 **[!UICONTROL 詳細]** タブをクリックします。

1. オプションを選択 **[!UICONTROL 既存のアセットのバージョンと同じ名前のアセットを保存]**. オンにすると、既存のアセットのバージョンと同じ名前で同じ場所にアップロードされたアセットを保存できます。 オフのままにすると、別の名前 ( 例： `asset-name.pdf` および `asset-name-1.pdf`) をクリックします。

1. オプションを選択 **[!UICONTROL 新しいバージョンの作成時にアセットメタデータを更新する]**. オンにすると、アセットの新しいバージョンが作成されるたびに、アセットのメタデータが更新されます。 オフにすると、アセットは新しいバージョンの作成前に保持していたメタデータを保持します。

![アセットのバージョン管理の設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>バージョン管理は、リンクされたフォルダーではサポートされていません。 を作成する際に [!DNL Workfront] リンクされたフォルダー内のドキュメントを含む配達確認では、以前のバージョンのアセットに対するコメントと注釈が削除されます。

## カスタムフォームを添付 {#attach-custom-forms}

ユーザーが [!DNL Workfront] アーティファクト。 このワークフローステップは、任意のワークフローモデルに追加できます。 この [!DNL Workfront] アーティファクトこの手順の影響は、ペイロードからの相対パスを使用して検索されます。

Experience Managerのワークフローエディターで、 [!UICONTROL Workfront — カスタムフォームを添付] ワークフローステップ。

![カスタムフォーム](/help/assets/assets/wf-custom-forms.png).

## アセットの自動公開 {#auto-publish-assets}

1. Experience Managerで、 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**&#x200B;をクリックし、 **[!UICONTROL 詳細]** タブをクリックします。

1. 選択 **[!UICONTROL Workfrontから送信されたときにアセットを自動的に公開する]**. このオプションを使用すると、WorkfrontからAEMにアセットが送信される際に、自動公開を有効にできます。 この機能は、Workfrontカスタムフォームフィールドと、そのフィールドを設定する値を指定することで、条件付きで有効にできます。 ドキュメントがAEMに送信されるたびに、条件を満たした場合、アセットは自動的に公開されます。

1. 選択 **[!UICONTROL プロジェクトの完了時に、すべてのプロジェクトアセットをBrand Portalに公開する]**. このオプションを使用すると、にアセットを自動的に公開できます。 [!DNL Brand Portal] そのユーザーが属するWorkfrontプロジェクトのステータスが「 `Complete`.

![自動公開を設定](/help/assets/assets/wf-auto-publish-config.png)

## Workfrontドキュメントのカスタムフォームの更新 {#subscribe-workfront-doc-custom-form-updates}

変更を購読するには、以下を実行します。 [!DNL Workfront] カスタムフォームのドキュメントを作成するには、 **[!UICONTROL 詳細]** タブをクリックします。 これらの更新情報を購読すると、マッピングされた更新情報が更新されます [!DNL Experience Manager] メタデータフィールド ( [!DNL Workfront] ドキュメントのカスタムフォームが変更されました。

![Workfront Document カスタムフォームの更新設定 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
