---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
feature: Release Information
role: Admin
source-git-commit: cb06380e4d3977f4f70a6444923cda2b0566d173
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 98%

---

# [!DNL Workfront for Experience Manager enhanced connector] のリリースノート {#release-notes-enhanced-connector-workfront}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
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

以下の節では、[!DNL Workfront for Experience Manager enhanced connector] の一般リリースノートの概要を説明します。

[!DNL Workfront for Experience Manager enhanced connector] の最新バージョン 1.9.21 のリリース日は 2025年6月25日（PT）です。

## リリースのハイライト {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] の最新バージョンには、次の機能強化とバグ修正が含まれています。

* API リクエストのログ機能を改善して、認証エラーの偽陽性ログを回避しました。

* Workfront API 呼び出しでの接続リークを修正しました。

* Java 17 および Java 21 バージョンの 6.5 LTS でWorkfront拡張コネクタをサポート。

>[!NOTE]
>
>AEM 6.4 は、拡張サポートの終了に達しました。詳しくは、[技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)を参照してください。サポートされているバージョンについては、[ここ](https://experienceleague.adobe.com/docs/?lang=ja)をご覧ください。

>[!IMPORTANT]
>
>アドビでは [!DNL Workfront for Experience Manager enhanced connector] の[最新バージョン 1.9.20 へのアップグレード](/help/assets/workfront-connector-install.md)をお勧めします。

## 既知の問題 {#known-issues}

* AEM 6.4 でプロジェクトにリンクしたフォルダーを設定する際に、Experience Manager は「**[!UICONTROL sub-folders]**」フィールドと「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値を保存しません。設定を保存すると、「**[!UICONTROL sub-folders]**」フィールドの値が **[!UICONTROL undefined]** に、「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値が **[!UICONTROL Default Portfolio]** に、それぞれ自動的に更新されます。

* 従来の Workfront エクスペリエンスを使用している場合、**[!UICONTROL 詳細]**&#x200B;ドロップダウンリストで選択できる「**[!UICONTROL 送信先]**」オプションでは、Experience Manager 内のターゲット宛先を選択できません。「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストを使用する場合、「**[!UICONTROL 送信先]**」オプションは正常に機能します。新しい Workfront エクスペリエンスの「**[!UICONTROL 詳細]**」ドロップダウンリストと「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストでは、「**[!UICONTROL 送信先]**」オプションは正常に機能します。

## 以前のリリース {#previous-releases}

### 2024年9月リリース {#september-2024-release}

* 既存のアセットの新しいバージョンをアップロードして作成する際に、MIME タイプが失われます。

### 2024年4月リリース {#april-2024-release}

* HTTP クライアントを閉じることに失敗すると、メモリ不足の問題が発生する。


### 2024年3月リリース {#march-2024-release}

* Workfront からの複数アセットのアップロードを処理すると問題が発生する。
* Workfront を使用して Experience Manager でフォルダーを検索する際に終了引用符を追加しないと、`SERVER_ERROR` が発生する。

### 2024年2月リリース {#february-2024-release}

* 切替スイッチ機能を有効にすると、AEM Cloud のお客様がコネクタを設定およびセットアップできるようになる。

* 基になるセッションを明示的に閉じずに `resourceResolver` を閉じると、AEM インスタンスでセッションリークが発生する。リソースリゾルバーを自動終了してもセッションは暗黙的に閉じられないので、セッションを明示的に閉じることが重要です。

### 2024年1月リリース {#january-2024-release}

* 現在、[!DNL CRX DE] の [!DNL Workfront] 設定には `project ID` が保存されていないので、読み取り専用権限を適用する際にエラーが発生します。方法について詳しくは、[権限の設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=ja#linked-folders)を参照してください。

* カスタムプロパティを標準インデックス定義に追加する方法に関する公開ドキュメントはありません。詳しくは、[カスタムプロパティの追加](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=ja#metadata-schema-mapping)を参照してください。

* 拡張コネクタの接続設定を削除すると、イベント購読やその他の保存された設定に大きな影響を与え、古い URL を指すようになります。

* Forms アドオンパッケージをインストールしても&#x200B;**[!UICONTROL ルーターの切り替え機能]**&#x200B;がインストールされないので、[!DNL WFEC AMS environment Toggle] 機能にエラーが発生します。

* EWC 設定でイベント購読を有効にすると、[!DNL Workfront] 拡張コネクタを初めて設定する際に、API 呼び出しが繰り返し失敗し、`HTTP 400` エラーが発生します。

* Workfront でリンクされたフォルダーアセットのコメントを削除すると、AEM でリンクされたフォルダーのパスが見つかりません。

* AEM での大きなファイルアセットのサポートが不十分な場合、4 バイトサイズの問題が発生します。

* リンクされたフォルダー内の重要なフロー、ドキュメントの更新およびメモの更新に対するリクエスト時間の処理はありません。

### 2023年11月リリース {#nov-2023-release}

* AEM フォルダーのリストを表示している間、ダイアログの読み込みに 1 分以上かかります。
* 承認済み [!DNL Workfront] ユーザーは、常に認証失敗エラーログを受信しています。

### 2023年10月リリース {#october-2023-release}

* 詳細設定でイベント購読が無効になっている場合、「**ドキュメント更新イベントに購読して AEM のアセットメタデータを更新**」、「**プロジェクト完了時にすべてのプロジェクトアセットを Brand Portal に公開**」および「**コメント同期を有効にする**」からオプションを選択できます。

* Workfront でプレビューする際に、Experience Manager に保存されたアセットの一部が適切にレンダリングされません。

* Workfront との Experience Manager 接続を再設定する際に、コメント同期の更新、削除、ドキュメントの更新などのイベント購読は正常に作成されません。

* リンクされたフォルダーの作成、更新、リンクされたフォルダーの有効化、コメントの同期の有効化と無効化、コネクタでの設定の保存に関する API の大幅なパフォーマンス向上。

### 2023年9月リリース {#september-2023-release}

* Experience Manager 拡張コネクタは、プロジェクトのイベント購読を削除する際に Workfront からすべてのイベント購読を取得します。これにより、アプリケーションのパフォーマンスに影響を与えます。

* アセットが Workfront から Experience Manager に送信される場合、Experience Manager 内でそのアセットの MIME タイプは `dc:format` 属性に設定されません。

* Experience Manager 強化コネクタに保存された Workfront プロジェクト ID には、重複が含まれます。

### 2023年8月リリース {#august-2023-release}

* リンクされたフォルダーに関連付けられたユーザーアカウントが存在しないので、Experience Manager でリンクされたフォルダーを作成できません。

* Experience Manager のアセットのメタデータ更新中の競合状態。

### 2023年6月リリース {#june-2023-release}

* 高度なネットワークを設定している場合、Adobe Workfront から AEM as a Cloud Service にコンテンツを送信する際に問題が発生します。


### 2023年5月リリース {#may-2023-release}

* Workfront は、Experience Manager から Workfront への REST 呼び出しに基づいて、重複するイベント購読に対して 409 HTTP 応答を返します。これにより、null ポインター例外が発生します。

### 2023年4月リリース {#april-2023-release}

2023年4月10日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.9 には、次のアップデートが含まれています。

* リンクされたフォルダーの作成中に Workfront から最終変更日を受け取ると、Experience Manager で `DateTimeParseException` 例外が表示されます。

* 短期間で複数のリンクされたプロジェクトフォルダーを作成する際に発生する問題。

* 新しいプロジェクトリンクフォルダーのセット数のしきい値制限を設定できません。

### 2023年3月リリース {#march-2023-release}

2023年3月3日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.8 には、次のアップデートが含まれています。

* Workfront でプロジェクトにリンクしたフォルダーを作成する際の Experience Manager のパフォーマンス改善。

* Workfront のコメントの削除が Experience Manager に反映されるようになりました。

* コネクタの設定から、Experience Manager as a Cloud Service で純新規顧客のブロッキングを管理できる機能。

### 2023年1月リリース {#january-2022-release}

2023年2月2日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.7 には、次のアップデートが含まれています。

* 1.9.6 リリースをインストールした後、メタデータエディターに Workfront カスタムフォームのプロパティが表示されない。

* Workfront の拡張コネクタをインストールして Assets のホームページを開くと、開発コンソールに `/content/dam/jcr:content/metadata/wfProjectURL not found` というエラーメッセージが表示される。

### 2022年12月リリース {#december-2022-release}

12月9日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.6 には、次のアップデートが含まれています。

**機能強化**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront 拡張コネクタで、アセットおよびフォルダーに対する全文検索の実行がサポートされるようになりました。

**バグ修正**

* ドキュメントバージョンのメタデータが、Workfront と Experience Manager の間で適切に同期されません。
* Workfront で Experience Manager にリンクされたフォルダーを作成する際に、グローバル設定で定義されていないスキーマをフォルダーで使用すると問題が発生します。
* 予想より読み込み時間が長いので、任意のフィールドをクリックすると、メタデータスキーマエディターフォームが応答しません。 この問題を解決するために、カスタムフォーム用の特定の OSGi 設定を追加しました。 メタデータスキーマエディターに追加するカスタムフォームの名前は、ログで確認できます。

### 2022年11月リリース {#november-2022-release}

11月11日（PT）にリリースされた [!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.5 では、次の問題が修正されています。

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

* 8 GB を超えるファイルをアップロードできません。
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

* Experience Manager as a Cloud Service にアセットをアップロードする際、リンクされたフォルダーを使用したり、Workfront の `Send To` アクションを使用したりすると、アセットが破損し、Adobe Photoshop で開くことができなくなります。

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
