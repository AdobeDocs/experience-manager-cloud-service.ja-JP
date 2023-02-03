---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 56fe4fde38fd6662c30b313a887f9740e919e0dc
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 82%

---

# [!DNL Workfront for Experience Manager enhanced connector] のリリースノート {#release-notes-enhanced-connector-workfront}

以下の節では、[!DNL Workfront for Experience Manager enhanced connector] の一般リリースノートの概要を説明します。

## リリース日 {#release-date}

の最新バージョン 1.9.7 のリリース日 [!DNL Workfront for Experience Manager enhanced connector] は 2023 年 2 月 2 日です。

## リリースのハイライト {#release-highlights}

の最新バージョン [!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* 1.9.6 リリースをインストールした後、メタデータエディターにWorkfrontカスタムフォームのプロパティが表示されない。

* 開発コンソールが表示されます `/content/dam/jcr:content/metadata/wfProjectURL not found` Workfront enhanced connector をインストールして Assets のホームページを開いた後のエラーメッセージ


>[!IMPORTANT]
>
>アドビでは [ の](../assets/update-workfront-enhanced-connector.md)最新バージョン 1.9.7 へのアップグレード[!DNL Workfront for Experience Manager enhanced connector]をお勧めします。

## 既知の問題 {#known-issues}

* AEM 6.4 でプロジェクトにリンクしたフォルダーを設定する際に、Experience Manager は「**[!UICONTROL sub-folders]**」フィールドと「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値を保存しません。設定を保存すると、「**[!UICONTROL sub-folders]**」フィールドの値が **[!UICONTROL undefined]** に、「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値が **[!UICONTROL Default Portfolio]** に、それぞれ自動的に更新されます。

* 従来の Workfront エクスペリエンスを使用している場合、「**[!UICONTROL 詳細]**」ドロップダウンリストで選択できる「**[!UICONTROL 送信先]**」オプションでは、Experience Manager 内のターゲット宛先を選択できません。「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストを使用する場合、「**[!UICONTROL 送信先]**」オプションは正常に機能します。新しい Workfront エクスペリエンスの「**[!UICONTROL 詳細]**」ドロップダウンリストと「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストでは、「**[!UICONTROL 送信先]**」オプションは正常に機能します。

## 以前のリリース {#previous-releases}

### 2022 年 12 月リリース {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 12 月 09 日にリリースされたバージョン 1.9.6 には、次の更新が含まれています。

**機能強化**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront enhanced connector で、アセットおよびフォルダーに対する全文検索の実行がサポートされるようになりました。

**バグ修正**

* ドキュメントバージョンのメタデータは、WorkfrontとExperience Managerの間で適切に同期されません。
* WorkfrontでExperience Managerにリンクされたフォルダーを作成する際に、グローバル設定で定義されていないスキーマをフォルダーで使用しているときに問題が発生します。
* 読み込み時間が予想より長いので、任意のフィールドをクリックすると、メタデータスキーマエディターフォームが応答を停止します。 この問題を解決するために、カスタムフォーム用の特定の OSGi 設定を追加しました。 メタデータスキーマエディターに追加するカスタムフォームの名前は、ログで確認できます。

### 2022 年 11 月リリース {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 11 月 11 日にリリースされたバージョン 1.9.5 には、次の更新が含まれています。

* Workfront で複数値のフィールドに値を 1 つだけ定義した場合、そのフィールド値は Experience Manager に適切にマッピングされません。

* Experience Manager では、`/content/dam/collections` に対する無効な権限が原因でアセットフォルダーにアクセスしている場合、**[!UICONTROL Link External Files and Folders]** 画面に `SERVER_ERROR` を表示します。

* Workfront 拡張コネクタ設定ページで 「**[!UICONTROL アセットを Brand Portal に公開]**」オプションを有効にすると、不正確なイベントが作成されます。このオプションを無効にした後も、このイベントは削除されません。

   この問題を解決するには、以下の手順を実行する必要があります。

   1. 拡張コネクタのバージョン 1.9.5 へのアップグレード。

   1. 詳細設定の「**[!UICONTROL アセットを Brand Portal に公開]**」オプションを無効にします。

   1. 「**[!UICONTROL アセットを Brand Portal に公開]**」オプションを有効にします。

   1. 間違ったイベント購読を削除します。

      1. `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>` に対する GET 呼び出しを実行します。

         ページ番号ごとに 1 回の API 呼び出しを実行します。

      1. 次のテキストを検索して、次の URL に一致し `objId` を含まないイベント購読を見つけます。

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         `"objId": "",` と `"url"` の間のコンテンツが JSON 応答と一致することを確認します。これを行うための推奨される方法は、 `objId` を持つ任意のイベント購読からコピーし、番号を削除することです。

      1. イベント購読 ID をメモしておきます。

      1. 間違ったイベント購読を削除します。 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>` に対する DELETE 呼び出しを行います。

         応答コード `200` は、間違ったイベント購読が正常に削除されたことを示します。
   >[!NOTE]
   >
   >ここで示している手順を実行する前に間違ったイベント購読を既に削除している場合は、最後の手順を省略することができます。

### 2022年10月リリース {#october-2022-release}

10月7日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.4 では、次の問題が修正されています。

* 多数のイベントがある場合、拡張コネクタ設定ページに「イベント購読」タブが表示されません。

* Workfront でプロジェクト内の既存フォルダーのリストを取得できず、その結果、フォルダーが重複して作成されます。

### 2022年9月リリース {#september-2022-release}

9月16日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.3 では、次の問題が修正されています。

* サイズが 8 GB を超えるファイルをアップロードできません。
* Workfront から AEM に送信されるアセットを自動公開する際の問題。
* デフォルトのメタデータスキーマフォームの編集中は、「ルートパス」フィールドを「タグ」フィールドで使用することができません。
* AEM ワークフローを使用して Workfront に新しいバージョンを追加する際の問題。
* Workfront で使用可能なアセットの AEM 検索を実行すると、AEM がエラーメッセージを表示します。
* アセットからタスク作成の AEM ワークフローを作成し、親タスク名を定義しない場合、タスクは Workfront で作成されません。

### 2022年8月リリース {#august-2022-release}

8月3日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.2 では、次の問題が修正されています。

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