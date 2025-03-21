---
title: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
description: ' [!DNL Workfront for Experience Manager enhanced connector] の設定'
role: Admin
feature: Workfront Integrations and Apps
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 98%

---

# [!DNL Workfront for Experience Manager enhanced connector] の設定 {#assets-integration-overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] で管理者アクセス権を持つユーザーが、インストール後に拡張コネクタを設定します。インストール手順については、 [コネクタのインストール](/help/assets/workfront-integrations.md) を参照してください。

>[!IMPORTANT]
>
> 2022年6月に、アドビは Workfront と Adobe Experience Manager Assets as a Cloud Service を接続するための新しいネイティブ統合をリリースしました。この統合は、これら 2 つのソリューションを接続するために必須の方法となりました。Workfront と AEM Assets as a Cloud Service を接続する拡張コネクタ（1.9.8 以降）の今後の新しい実装は、ブロックされます。

>[!IMPORTANT]
>
>* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[拡張コネクタのインストール手順](workfront-connector-install.md)の手順 5(a) を参照してください。
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。

## イベント購読の設定 {#event-subscriptions}

イベント購読は、[!DNL Adobe Workfront] で発生するイベントを AEM に通知するために使用されます。動作するためにイベント購読を必要とする [!DNL Workfront for Experience Manager enhanced connector] 機能は次の 3 つです。

* プロジェクトにリンクされたフォルダーの自動作成。
* Workfront ドキュメントのカスタムフォーム値の変更を AEM アセットメタデータに同期します。
* プロジェクトの完了時に Brand Portal にアセットを自動的に公開します。

これらの機能を使用するには、イベント購読を有効にします。

* 手順 5 で作成した [!UICONTROL Workfront ツール]クラウドサービスの設定を編集し、「[!UICONTROL イベント購読]」タブを選択します。
* セクション 6 で作成した [!UICONTROL Workfront カスタム統合]を選択します。
* 「[!UICONTROL Workfront イベント購読の有効化]」をクリック します。

  ![イベント購読](/help/assets/assets/event-subs.png)

## リンクされたフォルダーの設定 {#linked-folders}

イベントを購読するには、次の手順に従います。

1. クラウドサービスで「**[!UICONTROL イベント購読]** 」タブに移動します。
1. [!DNL Workfront] で作成したカスタム統合を選択します。
1. 「**[!UICONTROL Workfront イベント購読の有効化]**」をクリック します。

### リンクされたフォルダー構造の設定 {#linked-folder-structure}

1. クラウドサービスの「プロジェクトにリンクされたフォルダー」タブに移動します。
1. リンクされたフォルダーの親パス：DAM 内で、リンクされたフォルダーを作成するフォルダーを選択します。空のままにすると、デフォルトで /content/dam に設定されます。Workfront ツールのメタデータスキーマと Workfront リンクフォルダーのメタデータスキーマが、選択したフォルダーに適用されていることを確認します。
1. リンクされたフォルダー構造：コンマ区切り値を入力します。各値は `DE:<some-project-custom-form-field>`、Portfolio、プログラム、年、名前または「リテラル文字列値」（最後の 1 つには引用符がいります）のいずれかです。現在は、Portfolio、プログラム、年、DE:プロジェクトの種類、名前に設定されています。
1. 権限の設定：`wf-workfront-users` グループに、`/conf/workfront-tools/settings/cloudconfigs` に対する `jcr:all permissions` 権限を追加します。
1. Workfront のフォルダーのタイトルに構造内のすべてのフォルダーを含める必要がある場合は、「フォルダー構造名を使用して Workfront でリンクされたフォルダーのタイトルを作成」チェックボックスをオンにする必要があります。それ以外の場合は、最後のフォルダーのタイトルになります。
1. サブフォルダーのマルチフィールドでは、リンクされたフォルダーの子フォルダーとして作成するフォルダーのリストを指定できます。
1. プロジェクトのステータス：プロジェクトを設定する必要があるステータスを選択して、リンクされたフォルダーを作成します。
1. ポートフォリオを使用してプロジェクトにリンクされたフォルダーを作成する：プロジェクトが属する必要のあるポートフォリオのリストで、リンクされたフォルダーを作成できます。この一覧を空のままにして、すべてのプロジェクトポートフォリオのリンクフォルダーを作成します。
1. カスタムフォームフィールドを使用してプロジェクトにリンクされたフォルダーを作成する：プロジェクトに必要なカスタムフォームフィールドおよびそれに対応する値で、リンクされたフォルダーを作成できます。この設定は、空である場合は無視されます。フィールドに `CUSTOM FORMS: Create DAM Linked Folder` を選択して、値に `Yes` を入力します。
1. 権限の設定：`wf-workfront-users group` に、`jcr:all permissions for /conf/workfront-tools/settings/cloudconfigs` の権限を設定します。
1. 「リンクされたフォルダーの自動作成を有効にする」をクリックします。「イベントの購読」タブに戻ると、作成イベントが 1 つ表示されます。

![リンクされたフォルダー設定](/help/assets/assets/wf-linked-folder-config.png)

## メタデータスキーマのマッピング {#metadata-schema-mapping}

### フォルダーメタデータマッピングの設定 {#folder-metadata-mapping}

Workfront プロジェクトと AEM フォルダー間のメタデータマッピングは、AEM フォルダーメタデータスキーマ内で定義されます。フォルダーメタデータスキーマは、AEM で通常どおりに作成および設定する必要があります。Workfront ツールにより、各フォルダーメタデータスキーマフォームフィールドの「設定」タブにオートコンプリートドロップダウンが追加されます。このオートコンプリートドロップダウンメニューを使用すると、各 AEM フォルダープロパティのマッピング先の Workfront フィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. `wf-workfront-users` グループについて、`jcr:read` 権限を `/conf/global/settings/dam/adminui-extension/foldermetadataschema` に追加します。
1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL フォルダーメタデータスキーマ]**&#x200B;に移動します。
1. 編集するフォルダーメタデータスキーマフォームを選択し、「編集」をクリックします。
1. 編集するフォルダーメタデータスキーマフォームフィールドを選択し、右側のパネルの「設定」タブを選択します。
1. 「[!UICONTROL Workfront フィールドからマッピング済み]」フィールドで、選択した AEM フォルダープロパティにマッピングする Workfront フィールドの名前を選択します。次のオプションを使用できます。

   * プロジェクトのカスタムフォームフィールド
   * 「プロジェクト概要」フィールド (ID、名前、説明、参照番号、計画完了日、プロジェクト所有者、プロジェクトスポンサー、ポートフォリオ、プログラム )

![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### アセットメタデータマッピングの設定 {#asset-metadata-mapping}

Adobe Workfront ドキュメントとアセット間のメタデータマッピングは、AEM メタデータスキーマ内で定義されます。メタデータスキーマは、AEM で通常どおりに作成および設定する必要があります。Workfront ツールは、各メタデータスキーマフォームフィールドの「設定」指定タブに設定オプションを追加します。これらのオプションを使用すると、各 AEM プロパティのマッピング先となる Workfront フィールドを指定できます。

マッピングを設定するには、次の手順に従います。

1. **ツール**／**Assets**／**メタデータスキーマ**&#x200B;に移動します。
1. 編集するメタデータスキーマフォームを選択し、「**編集**」をクリックするか、新しいメタデータスキーマを最初から作成します。
1. 編集するメタデータスキーマフォームフィールドを選択し、右側のパネルで「**設定**」タブを選択します。
1. [!DNL Workfront] カスタムフォームフィールドで、選択した AEM プロパティにマッピングする [!DNL Workfront] フィールドの名前を選択します。次のオプションを使用できます。

   * ドキュメントのカスタムフォームフィールド
   * プロジェクトのカスタムフォームフィールド
   * カスタムフォームフィールドの公開
   * タスクのカスタムフォームフィールド
   * プロジェクトの概要フィールド（ID、名前、説明、参照番号）

1. [!UICONTROL Workfront カスタムフォームフィールド]で選択した [!DNL Workfront] フィールドが Workfront ユーザー先行入力フィールドの場合、マッピングする Workfront ユーザーフィールドを指定する必要があります。これを行うには、「Workfront の参照オブジェクトから値を取得」フィールドをオンにしてから、マッピングする値を取得する [!UICONTROL Workfront ユーザーカスタムフォームフィールド]の名前を指定します。

   ![メタデータマッピング設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## Map プロパティ {#map-property}

このワークフローステップでは、ユーザーはプロパティをプロジェクト、タスク、イシューまたはドキュメントの [!DNL Workfront] カスタムフォームにマッピングできます。この手順が影響を与える [!DNL Workfront] アーティファクトは、ペイロードからの相対パスを使用して検索されます。マッピングするプロパティは、ステップダイアログ設定内で制御します。

**タイプ**：このフィールドでは、プロパティのマッピング先の Workfront オブジェクトタイプを選択できます。

**ID プロパティ**：このフィールドでは、プロパティのマッピング先の Workfront オブジェクト ID へのパスを指定できます。このフィールドで指定するパスは、ワークフローペイロードを基準とした相対パスにする必要があります。

**プロパティの割り当て**：このマルチフィールドを使用すると、AEM プロパティと Workfront フィールド間のマッピングを指定できます。複数フィールドの各項目は、1 つのマッピングを指定します。各マッピングは、`<workfront-field>=<aem-mapped-property>` の形式である必要があります。

* `workfront-field` は次になることができます。

   * プレフィックス `DE:` で識別されるカスタムフォームフィールド 。
   * 名前で識別される編集可能なフィールド。フィールド名は [[!DNL Workfront] API エクスプローラー](https://experience.workfront.com/s/api-explorer)にあります。

* `aem-mapped-property` は次になることができます。

   * リテラル値。これらは引用符で囲む必要があります。
   * AEM プロパティ。この参照は、ワークフローペイロードに対する相対参照にする必要があります。
   * 名前付きの値。これらは角括弧で囲む必要があります。
   * 上記の 3 つの項目を連結したもの。`{+}` を使用して指定します。
   * 値を `{replace(<value>,"old-char","new-char")}` で囲むことによる上記の 3 つの項目の変更。

* 次に例を示します。

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![プロパティをマッピングするための設定](/help/assets/assets/wf-map-property-config.png)

## ステータスを設定 {#set-status}

ワークフローエディターで、「**[!UICONTROL 引数]**」タブの「**[!UICONTROL Workfront - ステータスの設定]**」のプロパティをクリックします。

![ワークフローを編集してステータスを設定](/help/assets/assets/wf-set-status.png)

## コメントの同期 {#comments-sync}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／ **[!UICONTROL Workfront ツール設定]**&#x200B;にアクセスして、設定を選択し、「**[!UICONTROL プロパティ]** 」を選択します。

   ![コメント同期](/help/assets/assets/comments-sync1.png)

1. 「**[!UICONTROL イベント購読]**」タブを選択し、「**[!UICONTROL Workfront で作成されたコメントを AEM に送信]**」オプションの「**[!UICONTROL コメント同期を有効にする]**」をクリックします。

   ![同期を有効にする](/help/assets/assets/wf-comment-sync-enabled.png)

Workfront から AEM へのコメントの同期をテストするには、次の手順に従います。

1. Workfront でリンクされたドキュメントに移動し、「更新」タブでコメントを追加します。

   ![Workfront にコメントを残す](/help/assets/assets/comments-sync2.png)

1. AEM 内の同じリンク先ドキュメントに移動し、そのドキュメントを選択して、左ナビゲーションの「[!UICONTROL タイムライン]」オプションを開いて、「[!UICONTROL コメント]」を選択します。左側のサイドバーには、[!DNL Workfront] から同期されたコメントが表示されます。

## アセットのバージョン {#asset-versions}

AEM でアセットのバージョン履歴を管理するには、AEM でアセットのバージョン管理を設定します。

1. Experience Manager で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／ **[!UICONTROL Workfront ツール設定]**&#x200B;をクリックし、「**[!UICONTROL 詳細]**」タブを開きます。

1. 「**[!UICONTROL 既存のアセットのバージョンと同じ名前のアセットを保存]**」オプションを選択します。オプションをオンにすると、既存のアセットのバージョンとして同じ名前で同じ場所にアップロードされたアセットを保存できます。オフのままにすると、別の名前（例：`asset-name.pdf` や `asset-name-1.pdf`）で新しいアセットが作成されます。

1. 「**[!UICONTROL 新しいバージョンの作成時にアセットメタデータを更新]**」オプションを選択します。オプションをオンにすると、アセットの新しいバージョンが作成されるたびに、アセットのメタデータが更新されます。オプションをオフにすると、アセットは新しいバージョンの作成前のメタデータを保持します。

![アセットのバージョン管理の設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>バージョン管理は、リンクされたフォルダーではサポートされていません。リンクされたフォルダー内のドキュメントの [!DNL Workfront] 配達確認を作成すると、以前のバージョンのアセットのコメントと注釈が削除されます。

## カスタムフォームを添付 {#attach-custom-forms}

このワークフローステップでは、ユーザーはカスタムフォームを [!DNL Workfront] アーティファクトに添付できます。このワークフローステップは、任意のワークフローモデルに追加できます。この手順が影響を与える [!DNL Workfront] アーティファクトは、ペイロードからの相対パスを使用して検索されます。

Experience Manager のワークフローエディターで、[!UICONTROL Workfront - カスタムフォームを添付]ワークフローステップのプロパティを編集します。

![カスタムフォーム](/help/assets/assets/wf-custom-forms.png)。

## アセットの自動公開 {#auto-publish-assets}

1. Experience Manager で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／ **[!UICONTROL Workfront ツール設定]** をクリックし、「**[!UICONTROL 詳細]**」タブを開きます。

1. 「**[!UICONTROL Workfront から送信されたときにアセットを自動的に公開する]**」を選択します。このオプションを使用すると、Workfront から AEM にアセットが送信される際に、アセットの自動公開を有効にできます。この機能は、Workfront カスタムフォームフィールドと、そのフィールドを設定する値を指定することで、条件付きで有効にできます。ドキュメントが AEM に送信されるたびに、条件を満たした場合、アセットは自動的に公開されます。

1. 「**[!UICONTROL プロジェクトの完了時に、すべてのプロジェクトアセットを Brand Portal に公開する]**」を選択します。このオプションを使用すると、属する Workfront プロジェクトのステータスが `Complete` に変更された場合、[!DNL Brand Portal] にアセットを自動的に公開できます。

![自動公開を設定](/help/assets/assets/wf-auto-publish-config.png)

## Workfront ドキュメントのカスタムフォームのアップデート {#subscribe-workfront-doc-custom-form-updates}

 [!DNL Workfront] ドキュメントカスタムフォームで変更を購入するには、「**[!UICONTROL 詳細]**」タブで関連オプションを選択します。これらのアップデートを購入すると、[!DNL Workfront] ドキュメントカスタムフォームの対応するフィールドが変更されたときに、マップされた [!DNL Experience Manager] メタデータフィールドがアップデートされます。

![[!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png) での Workfront ドキュメントカスタムフォームのアップデート設定
