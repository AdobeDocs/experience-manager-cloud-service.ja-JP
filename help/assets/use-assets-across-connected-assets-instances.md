---
title: 接続されたアセットを使用して、[!DNL Adobe Experience Manager Sites]オーサリングワークフローでDAMアセットを共有します。
description: 別の[!DNL Adobe Experience Manager Sites]展開でWebページを作成する場合、リモートの[!DNL Adobe Experience Manager Assets]展開で使用できるアセットを使用します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5e89a44cb727547af9db783662e035c4e2102a4e

---


# Connected Assets を使用した での DAM アセットの共有 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大規模企業では、Web サイトの作成に必要なインフラストラクチャが分散していることがあります。Web サイト作成機能と、それらの Web サイトの作成に使用されたデジタルアセットが、別のデプロイメントに格納されている場合もあります。1つの理由は、連携して動作する必要がある既存の配置を地理的に分散させることができます。 もう1つの理由は、親会社が一緒に使用したい異種インフラストラクチャを導く買収です。

ユーザーは、でWebページを作成でき [!DNL Experience Manager Sites]ます。 [!DNL Experience Manager Assets] は、webサイトに必要なアセットを提供するDigital Asset Management(DAM)システムです。 [!DNL Experience Manager] とを統合して、上記の使用例をサポートするよう [!DNL Sites] になり [!DNL Assets]ました。

## Connected Assets の概要 {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. 管理者は、の別の（リモートの）デプロイメントとの、のデプロイメントの1回限り [!DNL Sites] の統合を作成 [!DNL Assets]します。

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. この機能は、一度に少数のリモートアセットをシームレスに検索および使用できるようサポートします。To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk.

### 前提条件とサポートされているデプロイメント {#prerequisites}

この機能を使用または設定する前に、以下を確認してください。

* ユーザーがそれぞれのデプロイメント上で適切なユーザーグループに属している。
* For [!DNL Adobe Experience Manager] deployment types, one of the supported criteria is met. 6.5について詳し [!DNL Experience Manager] くは、Experience Manager 6.5 Assetsの [接続されたアセット機能を参照してください](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Sites] クラウドサービス | [!DNL Experience Manager] 6.5 AMS [!DNL Sites] 上 | [!DNL Experience Manager] 6.5 [!DNL Sites] オンプレミス |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]クラウドサービス&#x200B;** | サポート対象 | サポート対象 | サポート対象 |
   | **[!DNL Experience Manager]6.5 AMS[!DNL Assets]上&#x200B;** | サポート対象 | サポート対象 | サポート対象 |
   | **[!DNL Experience Manager]6.5[!DNL Assets]オンプレミス&#x200B;** | サポートなし | サポートなし | サポートなし |

### サポートされているファイル形式 {#mimetypes}

作成者は、コンテンツファインダーで画像や次のタイプのドキュメントを検索し、検索したアセットをページエディターで使用できます。`Download` コンポーネントにドキュメントを追加したり、`Image` コンポーネントに画像を追加できます。Authors can also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. 次の形式がサポートされています。

* **画像形式**: [画像コンポーネントがサポートする形式](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/image.html) 。 [!DNL Dynamic Media] 画像はサポートされていません。
* **ドキュメント形式**：詳しくは、[Connected Assets でサポートされるドキュメント形式](file-format-support.md#document-formats)を参照してください。

### 関連するユーザーとグループ {#users-and-groups-involved}

この機能の設定や使用に関係する様々な役割と対応するユーザーグループについて、以下で説明します。ローカルスコープは、作成者がWebページを作成する場合に使用します。 リモートスコープは、必要なアセットをホストしている DAM デプロイメントで使用されます。The [!DNL Sites] author fetches these remote assets.

| 役割 | 対象範囲 | ユーザーグループ | 手順のユーザーネーム | 要件 |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Sites] administrator | ローカル | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| DAM ユーザー | ローカル | `Authors` | `ksaner` | `/content/DAM/connectedassets/` の取得済みアセットを表示／複製するために使用されます。 |
| [!DNL Sites] 各手順で | ローカル | `Authors` (リモートDAMでの読み取りアクセスと、ローカルでの作成者アクセスを使用 [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. `ksaner` DAM ユーザーの資格情報が使用されます。 |
| [!DNL Assets] administrator | リモート | [!DNL Experience Manager] `administrators` | `admin` リモートで [!DNL Experience Manager] | クロスオリジンリソース共有（CORS）を設定します。 |
| DAM ユーザー | リモート | `Authors` | `ksaner` リモートで [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| DAM ディストリビューター（テクニカルユーザー） | リモート | [!DNL Sites] `Authors` | `ksaner` リモートで [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. この役割は、上の 2 つの `ksaner` の役割とは異なり、別のユーザーグループに属しています。 |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL Connected Assets 設定]**&#x200B;をクリックし、次の値を入力します。

   1. [!DNL Assets] 場所は `https://[assets_servername_ams]:[port]`です。
   1. DAM ディストリビューターの資格情報（テクニカルユーザー）。
   1. 「**[!UICONTROL マウントポイント]**」フィールドに、 が取得したアセットの格納先となるローカル パスを入力します。[!DNL Experience Manager][!DNL Experience Manager]例：`remoteassets` フォルダー。

   1. 「**[!UICONTROL オリジナルバイナリ転送の最適化しきい値]**」の値をネットワークに応じて調整します。このしきい値より大きいサイズのアセットレンディションは、非同期で転送されます。
   1. データストアを使用してアセットを保存し、データストアが両方の デプロイメント間に共通のストレージである場合は、「**[!UICONTROL Connected Assets と共有されるデータストア]**」を選択します。この場合、実際のアセットバイナリはデータストアに存在し、転送されないため、しきい値の制限は重要ではありません。
      ![Connected Assets の典型的な設定](assets/connected-assets-typical-config.png)

      *図：Connected Assets の典型的な設定.*

1. アセットは既に処理され、レンディションが取得されたので、ワークフローランチャーを無効にします。Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. **[!UICONTROL DAM アセットの更新]**&#x200B;および **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ワークフローを含むランチャーを検索します。

   1. ワークフローランチャーを選択し、アクションバーの「**[!UICONTROL プロパティ]**」をクリックします。

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | 前 | 後 |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作成者がアセットを取得する際、リモート デプロイメントで使用可能なすべてのレンディションが取得されます。取得したアセットのレンディションをさらに作成したい場合は、この設定手順をスキップしてください。The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. 管理者の資格情報を使用してログインします。 Search for `Cross-Origin`. **[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;にアクセスします。

   1. To create a CORS configuration for [!DNL Sites] instance, click ![aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. 設定を保存します。

## リモートアセットの使用 {#use-remote-assets}

Web サイト作成者は、コンテンツファインダーを使用して DAM インスタンスに接続します。Web サイト作成者は、コンポーネント内のリモートアセットを参照、検索、ドラッグできます。リモート DAM への認証をおこなえるよう、管理者から提供された DAM ユーザーの資格情報を手元に用意してください。

作成者は、ローカルDAMおよびリモートDAMインスタンスで使用可能なアセットを、単一のWebページで使用できます。 コンテンツファインダーを使用すれば、ローカル DAM の検索とリモート DAM の検索を切り替えることができます。

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. その他のタグは破棄されます。Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### 使用手順 {#walk-through-of-usage}

上記のセットアップを使用してオーサリングエクスペリエンスを試し、機能を理解してください。リモート DAM デプロイメントで、選択したドキュメントまたは画像を使用します。

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. または、ブラウザーで `https://[assets_servername_ams]:[port]/assets.html/content/dam` にアクセスします。選択したアセットをアップロードします。
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. ユーザー名として `ksaner` を入力し、提供されたオプションを選択し、「**[!UICONTROL OK]**」をクリックします。
1. **[!UICONTROL サイト]**／**[!UICONTROL We.Retail]**／**[!UICONTROL us]**／**[!UICONTROL en]** で、We.Retail Web サイトページを開きます。ページを編集します。または、ブラウザーで `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` にアクセスしてページを編集します。

   ページの左上隅にある「**[!UICONTROL サイドパネルを切り替え]**」をクリックします。

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. 資格情報（ユーザー名：`ksaner`、パスワード：`password`）を入力します。This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. DAM に追加したアセットを検索します。リモートアセットは左側のパネルに表示されます。画像またはドキュメントでフィルタリングしてから、サポートされているドキュメントのタイプでさらにフィルタリングします。`Image` コンポーネント上の画像と `Download` コンポーネント上のドキュメントをドラッグします。

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. コンポーネントによる編集は非破壊的です。

   ![リモート DAM でアセットを検索するときにドキュメントタイプと画像をフィルタリングするオプション](assets/filetypes_filter_connected_assets.png)

   *図：リモート DAM でアセットを検索するときにドキュメントタイプと画像をフィルタリングするオプション.*

1. アセットが非同期で取得され、取得タスクが失敗した場合、サイト作成者に通知されます。オーサリング中またはオーサリング後でも、作成者は[非同期ジョブ](/help/assets/asynchronous-jobs.md)ユーザーインターフェースで取得タスクやエラーについての詳細情報を確認できます。

   ![バックグラウンドで発生するアセットの非同期取得に関する通知。](assets/assets_async_transfer_fails.png)

   *図：バックグラウンドで発生するアセットの非同期取得に関する通知。*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. 公開時にリモートアセットが正常に取得されることを確認します。取得した各アセットのステータスを確認するには、[非同期ジョブ](/help/assets/asynchronous-jobs.md)ユーザーインターフェースをご覧ください。

   >[!NOTE]
   >
   >1 つ以上のリモートアセットが取得されない場合でも、ページは公開されます。リモートアセットを使用するコンポーネントは空で公開されます。The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Web ページで使用された、取得済みのリモートアセットは、その格納先となるローカルフォルダー（上の手順の場合は `connectedassets`）へのアクセス権限を持つすべてのユーザーから検索や使用が可能となります。これらのアセットは、ローカルリポジトリでも[!UICONTROL コンテンツファインダー]経由で検索および表示できます。

取得されたアセットは他のローカルアセットと同じように使用できます。ただし、関連するメタデータは編集できません。

## 制限事項 {#limitations}

### 権限とアセット管理 {#permissions-and-managing-assets}

* ローカルアセットは、リモートデプロイメントの元のアセットと同期されません。DAM デプロイメント上での編集、削除または権限の失効は、ローカル側には一切伝播されません。
* ローカルアセットは読み取り専用のコピーです。[!DNL Experience Manager] コンポーネントは、アセットに対して非破壊編集をおこないます。その他のいかなる編集もできません。
* ローカルで取得されたアセットは、オーサリング用途でのみ使用できます。アセット更新ワークフローの適用やメタデータの編集はおこなえません。
* 画像とリストに表示されるドキュメント形式のみがサポートされます。[!DNL Dynamic Media]、アセット、コンテンツフラグメントおよびエクスペリエンスフラグメントはサポートされません。
* メタデータスキーマは取得されません。
* All [!DNL Sites] authors have read permissions on the fetched copies, even if authors do not have access to the remote DAM deployment.
* 統合をカスタマイズするための API サポートはありません。
* この機能は、リモートアセットのシームレスな検索および使用をサポートします。多くのリモートアセットをローカルデプロイメントで一度に利用できるようにするには、リモートアセットの移行を検討します。
* リモートアセットを [!UICONTROL ページプロパティ] ユーザーインターフェイスのページサムネールとして使用することはできません。 Webページのサムネールは、 [!UICONTROL ページのプロパティ] ( [!UICONTROL Thumbnail] )ユーザインターフェイスで「画像を [!UICONTROL 選択]」をクリックして設定できます。

### セットアップとライセンス {#setup-licensing}

* [!DNL Assets] の展開 [!DNL Adobe Managed Services] はサポートされています。
* [!DNL Sites] は、一度に1つの [!DNL Assets] リポジトリに接続できます。
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### 使用方法 {#usage}

* リモートアセットを検索し、ローカルページ上のリモートアセットをドラッグしてコンテンツを作成する機能のみがサポートされています。
* 取得操作は 5 秒でタイムアウトします。アセット取得時、問題が発生する場合があります（ネットワークに問題がある場合など）。Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* 取得されたアセットに対しては、単純な非破壊編集と、 `Image` コンポーネント経由でサポートされている編集をおこなえます。アセットは読み取り専用です。

## 問題のトラブルシューティング {#troubleshoot}

一般的なエラーシナリオのトラブルシューティングをおこなうには、次の手順に従います。

* If you cannot search for remote assets from the [!UICONTROL Content Finder], recheck and ensure that the required roles and permissions are in place.
* リモート DAM から取得したアセットは、リモートに存在しない、それを取得するための適切な権限が不足している、ネットワーク障害などの理由で Web ページに公開されない場合があります。アセットがリモートDAMから削除されていないか、権限が変更されていないことを確認します。 適切な前提条件が満たされていることを確認します。 アセットをページに追加し直して、再公開してください。 アセット取得時のエラーについては、[非同期ジョブのリスト](/help/assets/asynchronous-jobs.md)を確認してください。
