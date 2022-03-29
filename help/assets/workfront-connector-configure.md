---
title: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
description: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
role: Admin
feature: Integrations
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 0d3262a3182063e69f764339e7937e2f83ad7bbb
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 100%

---

# [!DNL Workfront for Experience Manager enhanced connector] の設定 {#assets-integration-overview}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] で管理者アクセス権を持つユーザーが、インストール後に拡張コネクタを設定します。インストール手順については、 [コネクタのインストール](/help/assets/workfront-integrations.md) を参照してください。

>[!IMPORTANT]
>
>アドビは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーまたは [!DNL Adobe Professional Services] 以外がデプロイと設定を行った場合は、アドビのサポート対象外となります。
>
>アドビは、このコネクタを冗長にする [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクタの使用から移行する必要が生じることがあります。

## イベント購読の設定 {#event-subscriptions}

イベント購読は、[!DNL Adobe Workfront] で発生するイベントを AEM に通知するために使用されます。動作するためにイベント購読を必要とする [!DNL Workfront for Experience Manager enhanced connector] 機能は次の 3 つです。

* プロジェクトにリンクされたフォルダーの自動作成。
* Workfront ドキュメントのカスタムフォーム値における変更の AEM アセットメタデータへの同期。
* プロジェクト完了時での Brand Portal へのアセットの自動公開。

これらの機能を使用するには、イベント購読を有効にします。

* 手順 5 で作成した [!UICONTROL Workfront ツール] クラウドサービス設定を編集し、「[!UICONTROL イベント購読]」タブを選択します。
* セクション ６ で作成した [!UICONTROL Workfront カスタム統合] を選択します。
* 「[!UICONTROL Workfront イベント購読を有効にする]」をクリックします。

   ![イベント購読](/help/assets/assets/event-subs.png)

## リンクされたフォルダーの設定 {#linked-folders}

イベントを購読するには、次の手順に従います。

1. クラウドサービスの「**[!UICONTROL イベント購読]** 」タブに移動します。
1. [!DNL Workfront] で作成したカスタム統合を選択します。
1. 「**[!UICONTROL Workfront イベント購読を有効にする]**」をクリックします。

### リンクされたフォルダー構造の設定 {#linked-folder-structure}

1. クラウドサービスの「プロジェクトにリンクされたフォルダー」タブに移動します。
1. リンクされたフォルダーの親パス：リンクされたフォルダーを作成する DAM 内のフォルダーを選択します。空のままにすると、デフォルトで /content/dam になります。Workfront ツールのメタデータスキーマと Workfront リンクフォルダーのフォルダーメタデータスキーマが、選択したフォルダーに適用されていることを確認します。
1. リンクされたフォルダー構造：コンマ区切り値を入力します。各値は、`DE:<some-project-custom-form-field>`、Portfolio、Program、Year、Name または何からの &quot;リテラル文字列値&quot; である必要があります（この最後の値には引用符が付いています）。現在は、Portfolio,Program,Year,DE:Project Type,Name に設定されています。
1. Workfront のフォルダーのタイトルに構造内のすべてのフォルダーを含める必要がある場合は、「フォルダー構造名を使用して Workfront でリンクされたフォルダーのタイトルを作成」チェックボックスをオンにしてください。それ以外の場合は、最後のフォルダーのタイトルになります。
1. サブフォルダーのマルチフィールドでは、リンクされたフォルダーの子フォルダーとして作成するフォルダーのリストを指定できます。
1. プロジェクトのステータス：リンクされたフォルダーを作成するためにプロジェクトに設定する必要があるステータスを選択します。
1. ポートフォリオを使用してプロジェクトにリンクフォルダーを作成：リンクされたフォルダーを作成するためにプロジェクトが属する必要のあるポートフォリオのリスト。リンクされたフォルダーをすべてのプロジェクトポートフォリオに作成する場合は、このリストを空のままにします。
1. カスタムフォームフィールドを使用してプロジェクトにリンクフォルダーを作成：カスタムフォームフィールドとそれに対応する値（リンクされたフォルダーを作成するためにプロジェクトに必要な値）。この設定は、空のままにした場合は無視されます。フィールドに `CUSTOM FORMS: Create DAM Linked Folder` を選択し、値として `Yes` を入力します。
1. 「リンクされたフォルダーの自動作成を有効にする」をクリックします。「イベント購読」タブに戻ると、作成イベントが 1 つになっていることがわかります。

![リンクされたフォルダーの設定](/help/assets/assets/wf-linked-folder-config.png)

## メタデータスキーマのマッピング {#metadata-schema-mapping}

### フォルダーメタデータマッピングの設定 {#folder-metadata-mapping}

Workfront プロジェクトと AEM フォルダー間のメタデータマッピングは、AEM フォルダーメタデータスキーマ内で定義されます。フォルダーメタデータスキーマは、AEM で通常どおりに作成および設定してください。Workfront ツールにより、各フォルダーメタデータスキーマフォームフィールドの「設定」タブにオートコンプリートドロップダウンが追加されます。 このオートコンプリートドロップダウンメニューを使用すると、各 AEM フォルダープロパティのマッピング先の Workfront フィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL フォルダーメタデータスキーマ]** に移動します。
1. 編集するフォルダーメタデータスキーマフォームを選択し、「編集」をクリックします。
1. 編集するフォルダーメタデータスキーマフォームフィールドを選択し、右側のパネルの「設定」タブを選択します。
1. 「[!UICONTROL Workfront フィールドからマッピング済み]」フィールドで、選択した AEM フォルダープロパティにマッピングする Workfront フィールドの名前を選択します。次のオプションを使用できます。

   * プロジェクトのカスタムフォームフィールド
   * プロジェクト概要のフィールド（ID、名前、説明、参照番号、計画完了日、プロジェクト所有者、プロジェクトスポンサー、ポートフォリオ、プログラム）

![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### アセットメタデータマッピングの設定 {#asset-metadata-mapping}

Adobe Workfront ドキュメントとアセット間のメタデータマッピングは、AEM メタデータスキーマ内で定義されます。メタデータスキーマは、AEM で通常どおりに作成および設定してください。Workfront ツールは、各メタデータスキーマフォームフィールドの「設定」設定タブに設定オプションを追加します。これらのオプションを使用すると、各 AEM プロパティのマッピング先となる Workfront フィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. **ツール**／**Assets**／**メタデータスキーマ** に移動します。
1. 編集するメタデータスキーマフォームを選択し、「**編集**」をクリックするか、新しいメタデータスキーマを最初から作成します。
1. 編集するメタデータスキーマフォームフィールドを選択し、右側のパネルの「**設定**」タブを選択します。
1. [!DNL Workfront] カスタムフォームフィールドで、選択した AEM プロパティにマッピングする [!DNL Workfront] フィールドの名前を選択します。次のオプションを使用できます。

   * ドキュメントのカスタムフォームフィールド
   * プロジェクトのカスタムフォームフィールド
   * 発行のカスタムフォームフィールド
   * タスクのカスタムフォームフィールド
   * プロジェクトの概要フィールド（ID、名前、説明、参照番号）

1. [!UICONTROL Workfront カスタムフォームフィールド] で選択した [!DNL Workfront] フィールドが Workfront ユーザー先行入力フィールドの場合、マッピングする Workfront ユーザーフィールドを指定する必要があります。これを行うには、「Workfront の参照オブジェクトから値を取得」フィールドをオンにしてから、マッピングする値を取得する [!UICONTROL Workfront ユーザーカスタムフォームフィールド] の名前を指定します。

   ![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## プロパティのマッピング {#map-property}

このワークフローステップでは、プロジェクト、タスク、発行またはドキュメントの [!DNL Workfront] カスタムフォームにプロパティをマッピングできます。このステップが影響する [!DNL Workfront] アーティファクトは、ペイロードからの相対パスを使用して検索されます。マッピングするプロパティは、ステップダイアログ設定内で制御します。

**タイプ**：このフィールドでは、プロパティのマッピング先の Workfront オブジェクトタイプを選択できます。

**ID プロパティ**：このフィールドでは、プロパティのマッピング先の Workfront オブジェクト ID へのパスを指定できます。このフィールドで指定するパスは、ワークフローペイロードを基準にする必要があります。

**プロパティの割り当て**：このマルチフィールドを使用すると、AEM プロパティと Workfront フィールド間のマッピングを指定できます。マルチフィールドの各項目は、1 つのマッピングを指定します。各マッピングの形式は、`<workfront-field>=<aem-mapped-property>` である必要があります。

* `workfront-field` は以下のようになります。

   * プレフィックス `DE:` で識別されるカスタムフォームフィールド。
   * 名前で識別される編集可能なフィールド。フィールド名は、[[!DNL Workfront]  API エクスプローラーにあります](https://experience.workfront.com/s/api-explorer)。

* `aem-mapped-property` は以下のようになります。

   * リテラル値。これらは引用符で囲む必要があります。
   * AEM プロパティ。この参照は、ワークフローペイロードに関連している必要があります。
   * 名前付きの値。これらは角括弧で囲む必要があります。
   * 上記の 3 つの項目を連結したもの。`{+}` を使用して指定します。
   * 値を `{replace(<value>,”old-char”,”new-char”)}` で囲むことによる上記の 3 つの項目の変更。

* 次に例を示します。

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![プロパティをマッピングするための設定](/help/assets/assets/wf-map-property-config.png)

## ステータスを設定 {#set-status}

ワークフローエディターで、「**[!UICONTROL 引数]**」タブの **[!UICONTROL Workfront - ステータスの設定]** のプロパティを編集します。

![ワークフローを編集してステータスを設定](/help/assets/assets/wf-set-status.png)

## コメントの同期 {#comments-sync}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Workfront ツールの設定]** にアクセスし、設定を選択して、「**[!UICONTROL プロパティ]**」を選択します。

   ![コメント同期](/help/assets/assets/comments-sync1.png)

1. 「**[!UICONTROL イベント購読]**」タブを選択し、「**[!UICONTROL Workfront で作成されたコメントを AEM に送信]**」オプションで「**[!UICONTROL コメント同期を有効にする]**」をクリックします。

   ![同期が有効になっています](/help/assets/assets/wf-comment-sync-enabled.png)

Workfront から AEM へのコメントの同期をテストするには、以下の手順に従います。

1. Workfront でリンクされたドキュメントに移動し、「更新」タブでコメントを追加します。

   ![Workfront にコメントを残す](/help/assets/assets/comments-sync2.png)

1. AEM で同じリンク先ドキュメントに移動し、そのドキュメントを選択して、左側のナビゲーションで「[!UICONTROL タイムライン]」オプションを開き、「[!UICONTROL コメント]」を選択します。左側のサイドバーには、[!DNL Workfront] から同期元のコメントが表示されます。

## アセットのバージョン {#asset-versions}

AEM でアセットのバージョン履歴を管理するには、AEM でアセットのバージョン管理を設定します。

1. Experience Manager で、 **[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Workfront ツールの設定]** にアクセスし、「**[!UICONTROL 詳細]**」タブを開きます。

1. 「**[!UICONTROL 既存のアセットのバージョンと同じ名前のアセットを保存]**」オプションを選択します。オンにすると、既存のアセットのバージョンと同じ名前で同じ場所にアップロードされたアセットを保存できます。オフのままにすると、別の名前（例： `asset-name.pdf` および `asset-name-1.pdf`）で新しいアセットが作成されます。

1. 「**[!UICONTROL 新しいバージョンの作成時にアセットメタデータを更新]**」オプションを選択します。オンにすると、アセットの新しいバージョンが作成されるたびに、アセットのメタデータが更新されます。オフにすると、アセットは新しいバージョンの作成前に持っていたメタデータを保持します。

![アセットのバージョン管理の設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>バージョン管理は、リンクされたフォルダーではサポートされていません。リンクされたフォルダー内のドキュメントを使用して [!DNL Workfront] 配達確認を作成すると、以前のバージョンに対するアセットのコメントと注釈が削除されます。

## カスタムフォームを添付 {#attach-custom-forms}

このワークフローステップでは、ユーザーはカスタムフォームを [!DNL Workfront] アーティファクトに添付できます。このワークフローステップは、任意のワークフローモデルに追加できます。このステップが影響を与える [!DNL Workfront] アーティファクトは、ペイロードからの相対パスを使用して検索されます。

Experience Manager のワークフローエディターで、 [!UICONTROL Workfront - カスタムフォームを添付] ワークフローステップのプロパティを編集します。

![カスタムフォーム](/help/assets/assets/wf-custom-forms.png)。

## アセットの自動公開 {#auto-publish-assets}

1. Experience Manager で、 **[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Workfront ツールの設定]** にアクセスし、 **[!UICONTROL 詳細]** タブを開きます。

1. **[!UICONTROL Workfront から送信されたときにアセットを自動的に公開する]** を選択します。このオプションを使用すると、Workfront から AEM にアセットが送信される際に、自動公開を有効にできます。この機能は、Workfront カスタムフォームフィールドと、そのフィールドを設定する値を指定することで、条件付きで有効にできます。ドキュメントが AEM に送信されるたびに、条件を満たした場合、アセットは自動的に公開されます。

1. **[!UICONTROL プロジェクトの完了時に、すべてのプロジェクトアセットを Brand Portal に公開する]** を選択します。このオプションを使用すると、アセットが属する Workfront プロジェクトのステータスが `Complete` に変更されたときに、アセットを [!DNL Brand Portal] に自動的に公開できます。

![自動公開を設定](/help/assets/assets/wf-auto-publish-config.png)

## Workfront ドキュメントのカスタムフォームの更新 {#subscribe-workfront-doc-custom-form-updates}

[!DNL Workfront] ドキュメントのカスタムフォームの変更を購読するには、 **[!UICONTROL 詳細]** タブで関連するオプションを選択します。これらの更新情報を購読すると、[!DNL Workfront] ドキュメントカスタムフォームの対応するフィールドが変更されたときに、マッピングされた [!DNL Experience Manager] メタデータフィールドが更新されます。

![Workfront ドキュメントのカスタムフォームは [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png) で設定を更新
