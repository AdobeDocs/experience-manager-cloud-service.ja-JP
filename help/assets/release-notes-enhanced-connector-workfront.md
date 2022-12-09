---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f98704357c38f61e8e7d36b33ad32e9154c611e6
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 46%

---

# [!DNL Workfront for Experience Manager enhanced connector] のリリースノート {#release-notes-enhanced-connector-workfront}

以下の節では、[!DNL Workfront for Experience Manager enhanced connector] の一般リリースノートの概要を説明します。

## リリース日 {#release-date}

の最新バージョン 1.9.6 のリリース日 [!DNL Workfront for Experience Manager enhanced connector] は 2022 年 12 月 09 日です。

## リリースのハイライト {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] の最新バージョンには、次の機能強化とバグ修正が含まれています。

**機能強化**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront enhanced connector で、アセットおよびフォルダーに対する全文検索の実行がサポートされるようになりました。

**バグ修正**

* ドキュメントバージョンのメタデータは、WorkfrontとExperience Managerの間で適切に同期されません。
* WorkfrontでExperience Managerにリンクされたフォルダーを作成する際に、グローバル設定で定義されていないスキーマをフォルダーで使用しているときに問題が発生します。
* 読み込み時間が予想より長いので、任意のフィールドをクリックすると、メタデータスキーマエディターフォームが応答を停止します。 この問題を解決するために、カスタムフォーム用の特定の OSGi 設定を追加しました。 メタデータスキーマエディターに追加するカスタムフォームの名前は、ログで確認できます。

>[!IMPORTANT]
>
>アドビは [ の](../assets/update-workfront-enhanced-connector.md)最新バージョン 1.9.6 へのアップグレード[!DNL Workfront for Experience Manager enhanced connector]を推奨します。

## 既知の問題 {#known-issues}

* AEM 6.4 でプロジェクトにリンクしたフォルダーを設定する際に、Experience Manager は「**[!UICONTROL sub-folders]**」フィールドと「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値を保存しません。設定を保存すると、「**[!UICONTROL sub-folders]**」フィールドの値が **[!UICONTROL undefined]** に、「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値が **[!UICONTROL Default Portfolio]** に、それぞれ自動的に更新されます。

* 従来の Workfront エクスペリエンスを使用している場合、「**[!UICONTROL 詳細]**」ドロップダウンリストで選択できる「**[!UICONTROL 送信先]**」オプションでは、Experience Manager 内のターゲット宛先を選択できません。「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストを使用する場合、「**[!UICONTROL 送信先]**」オプションは正常に機能します。新しい Workfront エクスペリエンスの「**[!UICONTROL 詳細]**」ドロップダウンリストと「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストでは、「**[!UICONTROL 送信先]**」オプションは正常に機能します。

## 以前のリリース {#previous-releases}

### 2022 年 11 月リリース {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 11 月 11 日にリリースされたバージョン 1.9.5 には、次の更新が含まれています。

* Workfrontで複数値のフィールドに値を 1 つだけ定義した場合、そのフィールド値はExperience Managerに適切にマッピングされません。

* Experience Managerに `SERVER_ERROR` の **[!UICONTROL 外部ファイルとフォルダのリンク]** の無効な権限が原因で、アセットフォルダーにアクセス中に画面が表示されました `/content/dam/collections`.

* の有効化 **[!UICONTROL Brand Portalへのアセットの公開]** 「 Workfront拡張コネクタ設定」ページの「 」オプションを選択すると、間違ったイベントが作成されていました。 このオプションを無効にした後も、イベントは削除されません。

   この問題を解決するには、以下の手順を実行する必要があります。

   1. 拡張コネクタのバージョン 1.9.5 にアップグレードします。

   1. を無効にします。 **[!UICONTROL Brand Portalへのアセットの公開]** オプションが追加されました。

   1. を有効にします。 **[!UICONTROL Brand Portalへのアセットの公開]** オプション。

   1. 間違ったイベント購読を削除します。

      1. に対するGET呼び出しの実行 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         ページ番号ごとに 1 回の API 呼び出しを実行します。

      1. 次のテキストを検索して、次の URL に一致し、 `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         次の間のコンテンツを必ず `"objId": "",` および `"url"` は JSON 応答に一致します。 これをおこなうための推奨される方法は、 `objId` 数字を削除します。

      1. イベント購読 ID をメモしておきます。

      1. 間違ったイベントサブスクリプションを削除します。 への削除 API 呼び出しを実行する `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` は、応答コードが誤ったイベントサブスクリプションを正常に削除したことを示しているので、
   >[!NOTE]
   >
   >この手順を実行する前に誤ったイベント購読を削除した場合は、この手順の最後の手順をスキップできます。

### 2022 年 10 月リリース {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 2007 年 10 月 7 日にリリースされたバージョン 1.9.4 には、次の更新が含まれています。

* 多数のイベントがあるので、拡張コネクタ設定ページの「イベント購読」タブを表示できません。

* Workfrontは、プロジェクト内の既存のフォルダーのリストを取得できないので、フォルダーが重複して作成されます。

### 2022 年 9 月リリース {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 9 月 17 日にリリースされたバージョン 1.9.3 には、次の更新が含まれています。

* サイズが 8 GB を超えるファイルをアップロードできません。
* WorkfrontからAEMに送信されたアセットを自動公開する際に発生する問題を修正しました。
* デフォルトのメタデータスキーマフォームの編集中、「ルートパス」フィールドを「タグ」フィールドで使用できません。
* AEMワークフローを使用してWorkfrontで新しいバージョンを追加する際に発生する問題を修正しました。
* Workfrontで使用可能なアセットに対してAEM検索を実行すると、AEMにエラーメッセージが表示されます。
* アセットからタスク作成用のAEMワークフローを作成し、親タスク名を定義しない場合、Workfrontではタスクは作成されません。

### 2022 年 8 月リリース {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 8 月 3 日にリリースされたバージョン 1.9.2 には、次の更新が含まれています。

* **[!UICONTROL ドキュメントをアップロード]**&#x200B;ワークフローの手順で、ドキュメントを Workfront に添付できない。

* **[!UICONTROL ドキュメントをアップロード]**&#x200B;ワークフローの手順で、Workfront のタスクと問題にドキュメントを添付できない。ワークフローの手順で、プロジェクトにはドキュメントを正常に添付できる。

### 2022年7月リリース {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.1 には、次の更新が含まれています。

* Adobe IMS に移行されたインスタンス用の Workfront API キーを使用した、Experience Manager と Workfront アプリケーション間の認証のサポートが追加されました。

* 外部のファイルまたはフォルダーにリンクすると、Workfront アプリケーションに `SERVER_ERROR` エラーメッセージが表示されます。このエラーメッセージは、API キーの不一致による未認証の例外を示しています。

* アセットに対してタスクの作成ワークフローを実行すると、ログメッセージに Null ポインター例外が表示されます。

* Experience Manager の詳細設定にある「`Replace Spaces with DASH` 設定」オプションを有効にすると、Workfront でフォルダーが重複して作成されます。

### 2022年6月リリース {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* Experience Manager as a Cloud Service へアセットをアップロードする際、リンクされたフォルダーを使用したり、Workfront の `Send To` アクションを使用したりすると、アセットが破損し、Adobe Photoshop で開くことができなくなります。

### 2022年3月リリース {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* プロジェクトにリンクしているフォルダー設定が複数ある場合でも、Adobe Workfront と AEM Assets as a Cloud Service の間でリンクされたフォルダーを作成できるようになりました。

* イベント購読のページネーションがサポートされるようになりました。

* AEM 6.4.x がサポートされるようになりました。

* プロキシ環境がサポートされるようになりました。

* パートナーやお客様のご意見に基づいて、いくつかのバグを修正しました。

>[!MORELIKETHIS]
>
>* [ [!DNL Workfront for Experience Manager enhanced connector]  と Experience Manager 6.5 の統合](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=ja)
>* [ [!DNL Workfront for Experience Manager enhanced connector]  と Experience Manager 6.4 の統合](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=ja)

