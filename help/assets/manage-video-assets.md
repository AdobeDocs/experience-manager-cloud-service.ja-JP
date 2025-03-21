---
title: ビデオアセットの管理
description: ' [!DNL Adobe Experience Manager] でビデオアセットをアップロード、プレビュー、注釈、公開します。'
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '5029'
ht-degree: 99%

---

# ビデオアセットの管理 {#manage-video-assets}

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
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

ビデオ形式は、組織のデジタルアセットの重要な部分です。[!DNL Adobe Experience Manager] は、ビデオアセットの作成後に、ビデオアセットのライフサイクル全体を管理するための充実した機能を提供しています。

[!DNL Adobe Experience Manager Assets] でビデオアセットを管理および編集する方法について説明します。ビデオのエンコーディングとトランスコーディング、例えば、FFmpeg トランスコーディングは、処理プロファイルを使用し、[!DNL Dynamic Media] 統合を使用して行うことができます。[!DNL Experience Manager] は、[!DNL Dynamic Media] ライセンスを使用せずにビデオの基本的なサポートを提供します。例えば、FFmpeg によるトランスコード、サポートされているファイル形式のプレビューサムネールの抽出、ブラウザーでの直接の再生に対応した形式のプレビューなどが可能です。

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

サポートされている形式のビデオアセットを [!DNL Experience Manager Assets] にアップロードしてプレビューできます。
<!-- It generates previews for video assets with the extension MP4. -->

### ビデオアセットをアップロードする

ビデオアセットをアップロードするには、次の手順に従います。

1. デジタルアセットフォルダー（またはサブフォルダー）で、アセットを追加する必要がある場所に移動します。
1. ツールバーから「**[!UICONTROL 作成]**」をクリックし、「**[!UICONTROL ファイル]**」を選択します。<br>または、ユーザーインターフェイス上でファイルをドラッグします。
詳しくは、[!DNL Experience Manager Assets] の [アセットのアップロード](manage-digital-assets.md#uploading-assets)を参照してください。

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### ビデオアセットをプレビューする

[!DNL Assets] ユーザーインターフェイスでは、サポートされているレンディションでビデオをプレビューすることができます。ビデオアセットをプレビューするには、次の手順に従います。

1. サポートされている形式のビデオアセットを [!DNL Experience Manager Assets] にアップロードします。詳しくは、[サポートされるビデオ形式](file-format-support.md#video-formats)を参照してください。<br>アップロードすると、ビデオアセットが処理され、プレビューレンディションが生成されます。
1. アセットをクリックし、上部のツールバーから ![ 詳細オプション](assets/do-not-localize/details_icon.svg) **[!UICONTROL 詳細]** を選択します。ビデオアセットがビデオビューアで開きます。
1. 動画サムネイルの ![ 再生オプション ](assets/do-not-localize/play.png) アイコンをクリックします。<br>再生、一時停止、音量の制御、およびビデオの全画面表示を行うことができます。

[!DNL Experience Manager Assets] の既存の動画アセットの場合、動画プレビュー機能を有効にするには、[!DNL Experience Manager] のアセットを&#x200B;**[!UICONTROL 再処理]**&#x200B;する必要があります。[!DNL Experience Manager] で[デジタルアセットを再処理](reprocessing.md)する方法を説明します。

### ビデオプレビューの制限事項

* MXF ファイルでは、レンディションが生成されても、ビデオのプレビューが表示されません。
* WebM ファイルは web ブラウザーでネイティブに再生できるので、プレビューレンディションは生成されません。

## ビデオアセットを公開する {#publish-video-assets}

公開後、ビデオアセットを URL として Web ページに含めたり、アセットを直接埋め込んだりできます。詳しくは、[ [!DNL Dynamic Media]  アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## YouTube へのビデオの公開 {#publishing-videos-to-youtube}

Experience Manager Assets で管理されているビデオアセットは、以前に作成した YouTube チャンネルに直接投稿できます。

ビデオアセットを YouTube に公開するには、Experience Manager Assets のビデオアセットにタグを付けます。これらのタグを YouTube チャンネルに関連付けます。ビデオアセットのタグが YouTube チャンネルのタグと一致する場合、ビデオが YouTube に公開されます。YouTube への公開は、関連するタグが使用されている限り、ビデオの通常公開と一緒に行われます。

YouTube は独自のエンコーディングを行います。そのため、Dynamic Media のエンコーディングで作成した版のビデオではなく、Experience Manager にアップロードされた元のビデオファイルが YouTube に公開されます。Dynamic Media を使用してビデオを処理する必要はありませんが、再生にビューアプリセットが必要な場合は、それが行われます。

ビデオ処理プロファイルをスキップして YouTube に直接公開すると、Experience Manager Assets のビデオアセットに対して、表示可能なサムネールが作成されません。また、エンコードされていないビデオは、Dynamic Media のアセットタイプのいずれでも動作しないことを意味します。

ビデオアセットの YouTube サーバーへの公開において、YouTube との安全でセキュアなサーバー間検証を行うには、次のタスクを実行する必要があります。

1. [Google Cloud の設定](#configuring-google-cloud-settings)
1. [YouTube チャンネルの作成](#creating-a-youtube-channel)
1. [公開用タグの追加](#adding-tags-for-publishing)
1. [Experience Manager での YouTube のセットアップ](#setting-up-youtube-in-aem)
1. [（オプション）アップロードしたビデオのデフォルト YouTube プロパティ設定の自動化](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [YouTube チャンネルへのビデオの公開](#publishing-videos-to-your-youtube-channel)
1. [（オプション）YouTube での公開済みビデオの確認](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Web アプリケーションへの YouTube URL のリンク](#linking-youtube-urls-to-your-web-application)

また、[ビデオを非公開にして YouTube から削除する](#unpublishing-videos-to-remove-them-from-youtube)こともできます。

### Google Cloud の設定 {#configuring-google-cloud-settings}

YouTube に公開するには、Google アカウントが必要です。GMAIL のアカウントを持っている場合は、既に Google アカウントも所有しています。Google アカウントがない場合も、簡単に作成できます。ビデオアセットを YouTube に公開するには資格情報が必要なので、アカウントが必要です。<!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Google Cloud で使用するアカウントと YouTube に使用する Google アカウントは、必ずしも同じである必要はありません。

Google ではユーザーインターフェイスが定期的に変更されます。そのため、YouTube にビデオを公開する手順は、以下の手順とは少し異なる場合があります。これは、ビデオが YouTube にアップロードされるかどうかを確認する場合にも当てはまります。

>[!NOTE]
>
>以下の手順は、ドキュメントを執筆している時点で正確なものです。ただし、Google では、Cloud web ページを予告なく定期的に更新します。そのため、一部の設定オプションの名前は、Google ユーザーインターフェイスでは手順で使用した名前とは少し異なる場合があります。

**Google Cloud を設定するには：**

1. Google アカウントを作成します。

   既に Google アカウントを持っている場合は、次の手順に進んでください。

1. [https://cloud.google.com/](https://cloud.google.com/) にアクセスします。
1. **[!UICONTROL Google Cloud]** ページの右上隅付近にある、「**[!UICONTROL コンソール]**」を選択します。

   必要に応じて、Google アカウントの資格情報を使用して&#x200B;**[!UICONTROL ログイン]**&#x200B;し、「**[!UICONTROL コンソール]**」オプションを確認します。

1. **[!UICONTROL ダッシュボード]**&#x200B;ページで、**[!UICONTROL Google Cloud Platform]** の右側にある「**[!UICONTROL プロジェクト]**」ドロップダウンリストを選択して、**[!UICONTROL プロジェクトの選択]**&#x200B;ダイアログボックスを開きます。
1. **[!UICONTROL プロジェクトの選択]**&#x200B;ダイアログボックスで、「**[!UICONTROL 新しいプロジェクト]**」を選択します。
1. **[!UICONTROL 新しいプロジェクト]**&#x200B;ダイアログボックスで、「**[!UICONTROL プロジェクト名]**」フィールドに新しいプロジェクトの名前を入力します。

   プロジェクト ID は、プロジェクト名に基づいて付けられます。そのため、プロジェクト名は慎重に選んでください。プロジェクト名を後で変更することはできません。また、このプロジェクト ID は、後で Experience Manager で YouTube をセットアップする際にも入力する必要があります。そのため、ID を書き留めておくとよいでしょう。

1. 「**[!UICONTROL 作成]**」を選択します。

1. 次のいずれかの操作を行います。

   * プロジェクトのダッシュボードの「**[!UICONTROL スタートガイド]**」カードで、「**[!UICONTROL API を確認して有効化]**」を選択します。
   * プロジェクトのダッシュボードの「**[!UICONTROL API]**」カードで「**[!UICONTROL API の概要に移動]**」を選択します。

1. **[!UICONTROL API とサービス]**&#x200B;ページの上部にある「**[!UICONTROL API とサービスを有効にする]**」を選択します。<!-- NEXT STEP BELOW IS STEP 10 -->
1. **[!UICONTROL API ライブラリ]**&#x200B;ページの左側の「**[!UICONTROL カテゴリ]**」で、「**[!UICONTROL YouTube]**」を選択します。ページの右側で、「**[!UICONTROL YouTube]**」を選択します。
1. **[!UICONTROL YouTube]** ページで、「**[!UICONTROL YouTube Data API v3]**」を選択します。
1. **[!UICONTROL YouTube Data API v3]** ページで、「**[!UICONTROL 管理]**」を選択します。

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. この API を使用するには、資格情報が必要です。必要に応じて、**[!UICONTROL API とサービス]**&#x200B;ページの左側で、「**[!UICONTROL 資格情報]**」を選択します。
1. **[!UICONTROL 資格情報]**&#x200B;ページの上部付近で、「**[!UICONTROL 資格情報を作成]**」を選択し、「**[!UICONTROL OAuth クライアント ID]**」を選択します。
1. **[!UICONTROL OAuth クライアント ID を作成]**&#x200B;ページの「**[!UICONTROL アプリケーションタイプ]**」ドロップダウンリストで、「**[!UICONTROL Web アプリケーション]**」を選択します。

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. 次のいずれかの操作を行います。

   * 「**[!UICONTROL 名前]**」フィールドに、OAuth 2.0 クライアントの一意の名前を入力します。
   * Google が既に「**[!UICONTROL 名前]**」フィールドに提供しているデフォルトの名前を使用します。

1. 「**[!UICONTROL 許可された JavaScript オリジン]**」見出しで、「**[!UICONTROL URI を追加]**」を選択します。

   ![6_5_googleaccount-apis-nameauthorizations](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. 「**[!UICONTROL URI]**」テキストフィールドに、次のように、実際に使用するドメインとポート番号を入力します。入力が終わったら、**[!UICONTROL Enter]** キーを押して、パスをリストに追加します。

   `https://<servername.domain>:<port_number>`

   例：`https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >上記の URI パスの例は、仮定的で、説明の目的でのみ使用します。

1. 「**[!UICONTROL 承認済みのリダイレクト URI]**」見出しで、「URI を追加」を選択します。
1. 「**[!UICONTROL URI]**」テキストフィールドに、次のように、実際に使用するドメインとポート番号を入力します。入力が終わったら、**[!UICONTROL Enter]** キーを押して、パスをリストに追加します。

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例：`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >上記の URI パスの例は、仮定的で、説明の目的でのみ使用します。

1. **[!UICONTROL OAuth クライアント ID を作成]**&#x200B;ページの下部付近で、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL OAuth クライアントが作成されました]**&#x200B;ダイアログボックスで、次の操作を行います。

   * （オプション）「**[!UICONTROL クライアント ID]**」および「**[!UICONTROL クライアント秘密鍵]**」フィールドに値を入力し、保存します。
   * 「**[!UICONTROL JSON をダウンロード]**」選択し、JSON ファイルを保存します。

   ダウンロードした JSON ファイルは、後で Adobe Experience Manager で YouTube をセットアップするときに必要になります。

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. **[!UICONTROL OAuth クライアントが作成されました]**&#x200B;ダイアログボックスで、「**[!UICONTROL OK]**」を選択します。
1. Google アカウントからログアウトします。次に、YouTube チャンネルを作成します。

### YouTube チャンネルの作成 {#creating-a-youtube-channel}

YouTube にビデオを公開するには、1 つ以上のチャンネルが必要です。既に YouTube チャンネルを作成している場合は、このタスクをスキップして、次の「[公開用タグの追加](/help/assets/dynamic-media/video.md#adding-tags-for-publishing)」タスクに進んでください。

>[!CAUTION]
>
>*Experience Manager* の「YouTube 設定」にチャンネルを追加する前に、YouTube のチャンネルを 1 つ以上セットアップ済みであることを確認してください（以下の [Experience Manager での YouTube のセットアップ](#setting-up-youtube-in-aem)を参照してください）。チャンネルのセットアップに失敗した場合でも、既存のチャンネルがないことを知らせる警告は表示されません。ただし、それでも、チャンネルを追加する際に Google 検証が行われますが、ビデオの送信先となるチャンネルを選択するオプションがありません。

**YouTube チャンネルを作成するには：**

1. [https://www.youtube.com](https://www.youtube.com/) にアクセスし、Google アカウントの資格情報を使用してログインします。
1. YouTube ページの右上隅にあるプロフィール写真（内側に文字が表示された、べた塗りの円が表示されている場合はその円）を選択したあと、「**[!UICONTROL 設定]**」（丸い歯車アイコン）を選択します。
1. 概要ページの「その他の機能」で、「**[!UICONTROL チャンネルをすべて表示するか、新しいチャンネルを作成する]**」を選択します。
1. チャンネルページで、「**[!UICONTROL 新しいチャンネルを作成]**」を選択します。
1. ブランドアカウントページで、「ブランドアカウント名」フィールドに、会社名や、ビデオアセットの公開先となる他のチャンネル名を入力し、「**[!UICONTROL 作成]**」を選択します。

   ここで入力する名前は、Experience Manager で YouTube をセットアップするときに再度入力する必要があるので、覚えておいてください。

1. （オプション）必要に応じて、さらにチャンネルを追加します。

   次は、公開用タグを追加します。

### 公開用タグの追加 {#adding-tags-for-publishing}

Experience Manager で、YouTube にビデオを公開するには、1 つ以上の YouTube チャンネルにタグを関連付けます。公開用タグの追加については、[タグの管理](/help/sites-cloud/authoring/sites-console/tags.md)を参照してください。

また、Experience Manager のデフォルトのタグを使用する場合は、このタスクをスキップして、次の [Experience Manager での YouTube のセットアップ](#setting-up-youtube-in-aem)に進んでください。

>[!NOTE]
>
>Cloud Service の設定後は、この時点で YouTube への公開レプリケーションエージェントを有効にするために他の設定は必要ありません。このエージェントは、Cloud Service 設定が保存されたときに有効になっているからです。

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Experience Manager での YouTube のセットアップ {#setting-up-youtube-in-aem}

Experience Manager 6.4 以降では、Experience Manager で YouTube への公開をセットアップするための新しいタッチ対応ユーザーインターフェイスが導入されました。使用している Experience Manager のインストール済みインスタンスに応じて、次のいずれかを行います。

* 6.4 以前の Experience Manager で YouTube を設定するには、[6.4 以前の Experience Manager での YouTube のセットアップ](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before)を参照してください。
* Experience Manager 6.4 以降で YouTube を設定するには、[Experience Manager 6.4 以降での YouTube のセットアップ](#setting-up-youtube-in-aem-and-later)を参照してください。

#### Experience Manager 6.4 以降での YouTube のセットアップ {#setting-up-youtube-in-aem-and-later}

1. Dynamic Media のインスタンスに管理者としてログインしてください。
1. Experience Manager の左上隅にある Experience Manager ロゴを選択し、左パネルで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL クラウドサービス]**／**[!UICONTROL YouTube 公開設定]**&#x200B;に移動します。
1. 「**[!UICONTROL グローバル]**」を選択します。

1. グローバルページの右上隅にある「**[!UICONTROL 作成]**」を選択します。
1. YouTube 設定を作成ページの「Google Cloud Platform 設定」で、「**[!UICONTROL アプリケーション名]**」フィールドに Google プロジェクト ID を入力します。

   このプロジェクト ID は、先ほど Google Cloud 設定を行ったときに指定したものです。YouTube 設定を作成ページを開いたままにしておきます。このページには後ですぐ戻ります。

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 任意のテキストエディターを使用して、「[Google Cloud 設定](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)」のタスクでダウンロードして保存しておいた JSON ファイルを開きます。
1. この JSON テキスト全体を選択してコピーします。
1. YouTube アカウント設定ダイアログボックスに戻ります。「**[!UICONTROL JSON 設定]**」フィールドに JSON テキストを貼り付けます。
1. ページの右上隅にある「**[!UICONTROL 保存]**」を選択します。

   次に、Experience Manager で YouTube チャンネルをセットアップします。

1. 「**[!UICONTROL チャンネルを追加]**」を選択します。
1. 「チャネル名」フィールドに、前に「**[!UICONTROL YouTube への 1 つ以上のチャネルの追加]**」タスクで作成したチャネルの名前を入力します。

   オプションで、必要に応じて説明を追加できます。

1. 「**[!UICONTROL 追加]**」を選択します。
1. YouTube／Google 検証が表示されます。まだ Google Cloud アカウントにログインしていない場合は、この手順をスキップします。

   * 前述の Google プロジェクト ID と JSON テキストに関連付けられた Google のユーザー名とパスワードを入力します。
   * アカウントのチャネル数に応じて、2 つ以上の項目が表示されます。チャネルを選択します。メールアドレスはチャネルではないので、選択しないでください。
   * 次のページで、「**[!UICONTROL 確定]**」を選択して、このチャネルへのアクセスを許可します。

1. 「**[!UICONTROL 許可]**」を選択します。

   次に、タグを公開用にセットアップします。

1. **[!UICONTROL 公開用タグの設定]** - クラウドサービス／YouTube ページで、鉛筆アイコンを選択して、使用するタグのリストを編集します。
1. Experience Manager で使用可能なタグのリストを表示するには、ドロップダウンリストアイコン（上下逆のキャレット）を選択します。
1. タグを追加するには、1 つ以上のタグを選択します。

   追加したタグを削除するには、そのタグを選択して、**[!UICONTROL X]** を選択します。

1. 使用するタグの追加が終了したら、「**[!UICONTROL 保存]**」を選択します。

   次は、YouTube チャンネルにビデオを公開します。

#### 6.4 以前の Experience Manager での YouTube のセットアップ {#setting-up-youtube-in-aem-before}

1. Dynamic Media のインスタンスに管理者としてログインしてください。

1. Experience Manager の左上隅にある Experience Manager ロゴを選択し、左パネルで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL デプロイメント]**／**[!UICONTROL クラウドサービス]**&#x200B;に移動します。
1. 「サードパーティのサービス」ヘッダーの下の「YouTube」で、「**[!UICONTROL 今すぐ設定]**」を選択します。
1. 設定を作成ダイアログボックスで、タイトル（必須）と名前（オプション）をそれぞれのフィールドに入力します。
1. 「**[!UICONTROL 作成]**」を選択します。
1. YouTube アカウント設定ダイアログボックスで、「**[!UICONTROL アプリケーション名]**」フィールドに Google プロジェクト ID を入力します。

   このプロジェクト ID は、先ほど [Google Cloud 設定を行った](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings)ときに指定したものです。YouTube アカウント設定ダイアログボックスを開いたままにしておきます。このダイアログボックスには後ですぐ戻ります。

1. 任意のテキストエディターを使用して、「Google Cloud 設定」のタスクでダウンロードして保存しておいた JSON ファイルを開きます。
1. この JSON テキスト全体を選択してコピーします。
1. YouTube アカウント設定ダイアログボックスに戻ります。「**[!UICONTROL JSON 設定]**」フィールドに JSON テキストを貼り付けます。
1. 「**[!UICONTROL OK]**」を選択します。

   次に、Experience Manager で YouTube チャンネルをセットアップします。

1. 「**[!UICONTROL 利用可能なチャネル]**」の右にある「**+**」（プラス記号のアイコン）を選択します。
1. YouTube チャンネル設定ダイアログボックスの「タイトル」フィールドに、前の「**[!UICONTROL YouTube への 1 つ以上のチャネルの追加]**」タスクで作成したチャネルの名前を入力します。

   オプションで、必要に応じて説明を追加できます。

1. 「**[!UICONTROL OK]**」を選択します。
1. YouTube／Google 検証が表示されます。まだ Google Cloud アカウントにログインしていない場合は、この手順をスキップします。

   * 前述の Google プロジェクト ID と JSON テキストに関連付けられた Google のユーザー名とパスワードを入力します。
   * アカウントのチャネル数に応じて、2 つ以上の項目が表示されます。チャネルを選択します。メールアドレスはチャネルではないので、選択しないでください。
   * 次のページで、「**[!UICONTROL 確定]**」を選択して、このチャネルへのアクセスを許可します。

1. 「**[!UICONTROL 許可]**」を選択します。

   次に、タグを公開用にセットアップします。

1. **[!UICONTROL 公開用タグの設定]** - クラウドサービス／YouTube ページで、鉛筆アイコンを選択して、使用するタグのリストを編集します。
1. Experience Manager で使用可能なタグのリストを表示するには、ドロップダウンリストアイコン（上下逆のキャレット）を選択します。
1. タグを追加するには、1 つ以上のタグを選択します。

   追加したタグを削除するには、そのタグを選択して、**X** を選択します。

1. 使用するタグの追加が終了したら、「**[!UICONTROL OK]**」を選択します。

   次は、YouTube チャンネルにビデオを公開します。

### （オプション）アップロードしたビデオのデフォルト YouTube プロパティ設定の自動化 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

ビデオをアップロードする際に YouTube プロパティの設定を自動化することもできます。Experience Manager でメタデータ処理プロファイルを作成します。

メタデータ処理プロファイルを作成するには、まず「**[!UICONTROL フィールドラベル]**」、「**[!UICONTROL プロパティにマッピング]**」、「**[!UICONTROL 選択肢]**」の各フィールドの値をコピーします。これらはすべてビデオのメタデータスキーマで見つかります。次に、これらの値を追加して、YouTube ビデオメタデータ処理プロファイルを作成します。

**アップロードしたビデオのデフォルト YouTube プロパティの設定を自動化するには：**

1. Experience Manager の左上隅にある Experience Manager ロゴを選択し、左パネルで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. 「**[!UICONTROL デフォルト値]**」を選択します（「デフォルト値」の左側にある選択ボックスにチェックマークを追加しないでください）。
1. **[!UICONTROL デフォルト値]**&#x200B;ページで、「**[!UICONTROL ビデオ]**」の左側にあるボックスをオンにし、「**[!UICONTROL 編集]**」を選択します。
1. メタデータスキーマエディターページで、「**[!UICONTROL 詳細]**」タブを選択します。
1. 「YouTube への公開」の下で、「**[!UICONTROL YouTube カテゴリ]**」を選択します。
1. ページの右側の「**[!UICONTROL 設定]**」タブで次の手順を実行します。

   * 「**[!UICONTROL プロパティにマッピング]**」テキストフィールドで、値を選択してコピーします。コピーした値を、開いているテキストエディターに貼り付けます。この値は、後でメタデータ処理プロファイルを作成する際に必要になります。テキストエディターは開いたままにしておきます。

   * 「**[!UICONTROL 選択肢]**」の下で、使用するデフォルト値（「人とブログ」または「科学と技術」など）を選択してコピーします。コピーした値を、開いているテキストエディターに貼り付けます。この値は、後でメタデータ処理プロファイルを作成する際に必要になります。テキストエディターは開いたままにしておきます。

1. 「YouTube への公開」の下で、「**[!UICONTROL YouTube のプライバシー]**」を選択します。
1. ページの右側の「**[!UICONTROL 設定]**」タブで次の手順を実行します。

   * 「**[!UICONTROL プロパティにマッピング]**」テキストフィールドで、値を選択してコピーします。コピーした値を、開いているテキストエディターに貼り付けます。この値は、後でメタデータ処理プロファイルを作成する際に必要になります。テキストエディターは開いたままにしておきます。

   * **[!UICONTROL 選択肢]**&#x200B;で、使用するデフォルト値を選択してコピーします。選択肢は 2 つが 1 組になっています。1 組の下のフィールドは、コピーするデフォルト値（公開、非公開またはプライベート）です。コピーした値を、開いているテキストエディターに貼り付けます。この値は、後でメタデータ処理プロファイルを作成する際に必要になります。テキストエディターは開いたままにしておきます。

1. メタデータスキーマエディターページの右上隅付近にある「**[!UICONTROL キャンセル]**」を選択します。
1. Experience Manager の左上隅にある Experience Manager ロゴを選択し、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL メタデータプロファイル]**&#x200B;を選択します。

1. メタデータプロファイルページの右上隅付近にある「**[!UICONTROL 作成]**」を選択します。
1. メタデータプロファイルを追加ダイアログボックスの「**[!UICONTROL プロファイルのタイトル]**」テキストフィールドに、「`YouTube Video`」と入力した後、「**[!UICONTROL 作成]**」を選択します。
1. メタデータプロファイルエディターページで、「**[!UICONTROL 詳細]**」タブを選択します。
1. 次の手順を実行して、コピーした「YouTube への公開」の値を、プロファイルに追加します。

   * ページの右側にある「**[!UICONTROL フォームを作成]**」タブを選択します。
   * （オプション）**[!UICONTROL セクションヘッダー]**&#x200B;というラベルのコンポーネントを左にドラッグして、フォーム領域にドロップします。
   * （オプション）「**[!UICONTROL フィールドラベル]**」を選択して、コンポーネントを選択します。
   * （オプション）ページの右側にある「設定」タブで、「フィールドラベル」テキストフィールドに「`YouTube Publishing`」と入力します。
   * 「**[!UICONTROL フォームを作成]**」タブを選択し、「**[!UICONTROL 複数値テキスト]**」というラベルのコンポーネントをドラッグして、作成した「**[!UICONTROL YouTube への公開]**」の下にドロップします。

   * コンポーネントを選択するには、「**[!UICONTROL フィールドラベル]**」を選択します。
   * ページの右側にある「設定」タブで、先ほどコピーした「YouTube への公開」の値（フィールドラベル値と、プロパティにマッピング値）をフォームのそれぞれのフィールドに貼り付けます。選択肢値を「デフォルト値」フィールドに貼り付けます。

1. コピーした「YouTube プライバシー」の値を、次の手順どおりにプロファイルに追加します。

   * ページの右側にある「**[!UICONTROL フォームを作成]**」タブを選択します。
   * （オプション）**[!UICONTROL セクションヘッダー]**&#x200B;というラベルのコンポーネントを左にドラッグして、フォーム領域にドロップします。
   * （オプション）「**[!UICONTROL フィールドラベル]**」を選択して、コンポーネントを選択します。
   * （オプション）ページの右側にある「設定」タブで、「フィールドラベル」テキストフィールドに「`YouTube Privacy`」と入力します。
   * 「**[!UICONTROL フォームを作成]**」タブを選択し、「**[!UICONTROL 複数値テキスト]**」というラベルのコンポーネントをドラッグして、作成した「**[!UICONTROL YouTube のプライバシー]**」の下にドロップします。

   * コンポーネントを選択するには、「**[!UICONTROL フィールドラベル]**」を選択します。
   * ページの右側にある「設定」タブで、先ほどコピーした「YouTube への公開」の値（フィールドラベル値と、プロパティにマッピング値）をフォームのそれぞれのフィールドに貼り付けます。選択肢値を「デフォルト値」フィールドに貼り付けます。

1. ページの右上隅にある「**[!UICONTROL 保存]**」を選択します。
1. YouTube への公開メタデータプロファイルを、ビデオのアップロード先フォルダーに適用します。メタデータプロファイルとビデオプロファイルの両方を設定する必要があります。

   詳しくは、[メタデータプロファイル](/help/assets/metadata-profiles.md)と[ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)を参照してください。

### YouTube チャンネルへのビデオの公開 {#publishing-videos-to-your-youtube-channel}

次は、前の手順で追加したタグを、ビデオアセットに関連付けます。このプロセスによって、Experience Manager が YouTube チャンネルに公開するアセットを把握できるようになります。

>[!NOTE]
>
>即時公開しても、YouTube には自動的には公開されません。Dynamic Media が設定されている場合は、**[!UICONTROL 即時]**&#x200B;と&#x200B;**[!UICONTROL アクティベーション時]**&#x200B;の 2 つの公開オプションがあります。
>
>**[!UICONTROL 即時公開する]**&#x200B;の場合、アップロードされたアセットは、IPS と同期された後、配信システムに自動的に公開されます。これは Dynamic Media には当てはまりますが、YouTube には当てはまりません。YouTube に公開するには、Experience Manager オーサーを介して公開する必要があります。

>[!NOTE]
>
>Experience Manager では、YouTube からのコンテンツの公開に **[!UICONTROL YouTube に公開]**&#x200B;ワークフローを使用します。このワークフローでは、進行状況を監視して、エラー情報を表示できます。
>
>詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。
>
>詳細な進行状況については、レプリケーション下の YouTube ログを監視できます。ただし、このような監視には管理者アクセスが必要です。

**YouTube チャンネルにビデオを公開するには：**

1. Experience Manager で、YouTube チャンネルに公開するビデオアセットの場所に移動します。
1. ビデオアセット（アダプティブビデオセット）を選択します。
1. ツールバーの「**[!UICONTROL プロパティ]**」を選択します。
1. 「基本」タブの「メタデータ」で、「タグ」フィールドの右側にある「**[!UICONTROL 選択ダイアログを開く]**」を選択します。
1. タグを選択ページで、使用するタグに移動し、1 つ以上のタグを選択します。

   タグは YouTube チャネルに関連付ける必要があります。

1. ページの右上隅にある「**[!UICONTROL 選択]**」を選択します。
1. ビデオのプロパティページの右上隅にある「**[!UICONTROL 保存して閉じる]**」を選択します。
1. ツールバーの「**[!UICONTROL クイック公開]**」を選択します。

   [Experience Manager Sites での公開管理の使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html?lang=ja#page-authoring)も参照してください。

   オプションで、YouTube チャンネルで公開済みビデオを確認できます。

### （オプション）YouTube での公開済みビデオの確認 {#optional-verifying-the-published-video-on-youtube}

オプションで、YouTube への公開（または非公開）の進行状況を監視できます。

詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。

公開にかかる時間は、プライマリソースビデオの形式、ファイルサイズ、アップロードトラフィックなどの多数の要因により左右されます。公開プロセスにかかる時間は、数分から数時間までの幅があります。また、高解像度の形式の方が、レンダリングの時間が長くなります。例えば、720p や 1080p の場合、表示されるまでの時間が 480p よりも長くなります。

8 時間経っても「**[!UICONTROL アップロード済み（処理しています、お待ちください）]**」というステータスメッセージが表示される場合は、サイトからビデオを削除して再度アップロードしてみてください。

### Web アプリケーションへの YouTube URL のリンク {#linking-youtube-urls-to-your-web-application}

ビデオの公開後、Dynamic Media によって生成された YouTube URL 文字列を取得できます。YouTube URL をコピーしたらクリップボードに配置されるので、必要に応じて web サイトのページまたはアプリケーションに貼り付けることができます。

>[!NOTE]
>
>YouTube URL は、ビデオアセットを YouTube に公開するまではコピーできません。

Web アプリケーションに YouTube URL をリンクするには：

1. URL をコピーする、*YouTube への公開済み*&#x200B;ビデオアセットの場所に移動して選択します。

   YouTube URL をコピーするには、*その前に*&#x200B;ビデオアセットを YouTube に&#x200B;*公開しておく*&#x200B;必要があります。

1. ツールバーの「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL 詳細]**」タブを選択します。
1. 「YouTube への公開」の「YouTube URL リスト」で、URL テキストを選択し、web ブラウザーにコピーしてアセットをプレビューするか、web コンテンツページに追加します。

### ビデオの非公開による YouTube からの削除 {#unpublishing-videos-to-remove-them-from-youtube}

Experience Manager のビデオアセットを非公開にすると、そのビデオは YouTube から削除されます。

>[!CAUTION]
>
>YouTube 内からビデオを直接削除すると、Experience Manager はそのことを認識できないので、そのビデオがまだ YouTube に公開されているかのように動作を続けます。ビデオアセットを YouTube で非公開にするときは、必ず Experience Manager から行ってください。

>[!NOTE]
>
>Experience Manager では、YouTube からのコンテンツの削除に **[!UICONTROL YouTube で非公開]**&#x200B;ワークフローを使用します。このワークフローでは、進行状況を監視して、エラー情報を表示できます。
>
>詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。

**ビデオを非公開にして YouTube から削除するには：**

1. YouTube チャネルで非公開にするビデオアセットの場所に移動します。
1. アセット選択モードで、1 つ以上の公開済みビデオアセットを選択します。
1. ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。必要に応じて、ツールバーの 3 ドットアイコン（`. . .`）を選択して、**[!UICONTROL 公開を管理]**&#x200B;を表示します。
1. 公開を管理ページで、「**[!UICONTROL 非公開]**」を選択します。
1. ページの右上隅にある「**[!UICONTROL 次へ]**」を選択します。
1. ページの右上隅にある「**[!UICONTROL 非公開]**」を選択します。

## ビデオエンコーディングと YouTube への公開の進行状況の監視 {#monitoring-video-encoding-and-youtube-publishing-progress}

ビデオエンコーディングが適用されたフォルダーに新しいビデオをアップロードしたり、YouTube にビデオを公開したりする場合は、ビデオエンコーディング／YouTube への公開の進行状況（エラー状況）を監視します。YouTube への公開の実際の進行状況は、ログでのみ確認できます。しかし、失敗したか成功したかは、以下の手順に従って他の方法で示されます。さらに、YouTube の公開ワークフローやビデオエンコーディングが完了するか中断されると、そのことを知らせるメール通知も受け取ります。

### 進行状況の監視 {#monitoring-progress}

進行状況（エンコーディング／YouTube の公開の失敗を含む）を監視できます。

1. アセットフォルダー内のビデオエンコーディングの進行状況を表示します。

   * カードビューでは、ビデオエンコーディングの進行状況がパーセント単位でアセットに表示されます。エラーがある場合、エラー情報はアセットにも表示されます。

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * リスト表示では、ビデオエンコーディングの進行状況は、「**[!UICONTROL 処理ステータス]**」列に表示されます。エラーがある場合は、そのメッセージも同じ列に表示されます。

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   この列は、デフォルトでは表示されません。この列を有効にするには、ビュードロップダウンメニューから「**[!UICONTROL 設定を表示]**」を選択し、「**[!UICONTROL 処理ステータス]**」列を追加して、「**[!UICONTROL 更新]**」を選択します。

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. アセット詳細の進行状況を表示します。アセットを選択したら、ドロップダウンメニューを開き、「**[!UICONTROL タイムライン]**」を選択します。タイムラインを、エンコーディングや YouTube への公開などのワークフローアクティビティに絞り込むには、「**[!UICONTROL ワークフロー]**」を選択します。

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   エンコーディングなどのワークフロー情報がタイムラインに表示されます。YouTube で公開する場合、ワークフロータイムラインには YouTube チャネルの名前と YouTube 動画の URL も含まれます。さらに、公開が完了すると、ワークフロータイムラインにエラー通知も表示されます。

   >[!NOTE]
   >
   >[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) からの&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**&#x200B;および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;に関する複数のワークフロー設定があるので、失敗／エラーメッセージが最終的に記録されるまでには時間がかかる可能性があります。例えば、次の設定です。
   >
   >* Apache Sling ジョブキューの設定
   >* Adobe Granite ワークフロー外部プロセスジョブハンドラー
   >* Granite ワークフロータイムアウトキュー
   >
   >これらの設定の&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**&#x200B;および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;プロパティは調整できます。

1. 進行中のワークフローについては、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL インスタンス]**&#x200B;からワークフローインスタンスを表示します。

   >[!NOTE]
   >
   >**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要です。

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   インスタンスを選択し、「**[!UICONTROL 履歴を開く]**」を選択します。

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   ワークフローインスタンス領域から、ワークフローを休止、終了または名前変更できます。詳しくは、[ワークフローの管理](/help/sites-cloud/authoring/workflows/overview.md)を参照してください。

1. エラーが発生したジョブについては、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL エラー]**&#x200B;からワークフローエラーを表示します。**[!UICONTROL ワークフローエラー]**&#x200B;に、エラーが発生したすべてのワークフローアクティビティが表示されます。

   >[!NOTE]
   >
   >**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要です。

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) からの&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**、および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;に関する複数のワークフロー設定があるので、エラーメッセージが最終的に記録されるまでには時間がかかる可能性があります。例えば、次の設定です。
   >
   >* Apache Sling ジョブキューの設定
   >* Adobe Granite ワークフロー外部プロセスジョブハンドラー
   >* Granite ワークフロータイムアウトキュー
   >
   >これらの設定の&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**&#x200B;および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;プロパティは調整できます。

1. 完了したワークフローについては、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL アーカイブ]**&#x200B;からワークフローアーカイブを表示します。**[!UICONTROL ワークフローアーカイブ]**&#x200B;に、完了したすべてのワークフローアクティビティが表示されます。

   >[!NOTE]
   >
   >**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要です。

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. 中止またはエラーが発生したワークフロージョブに関するメール通知を受け取ります。これらのメール通知は、管理者が設定できます。詳しくは、[メール通知の設定](#configuring-e-mail-notifications)を参照してください。

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## 処理プロファイルを使用したトランスコード {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] では、処理プロファイルを使用して MP4 ビデオファイルの基本的なトランスコードを実行できます。この機能により、アップロードだけでなく、MP4 ビデオファイルのプレビューやスケールの操作も実行できます。

![ でのビデオトランスコードの処理プロファイルの作成[!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*図：[!DNL Experience Manager] でのビデオトランスコードの処理プロファイル。*

幅または高さのみを指定して、その他のフィールドを空白にした場合、レンディションは縦横比を維持します。H.264 ビデオコーデックはトランスコードに使用できます。

処理プロファイルを使用してアセットを処理するには、プロファイルをフォルダーに追加します。詳しくは、[処理プロファイルを使用したアセットの処理](/help/assets/asset-microservices-configure-and-use.md#use-profiles)を参照してください。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

ビデオアセットに注釈を追加できます。ビデオに注釈を追加する際は、ユーザーがフレームに注釈を追加できるようにプレーヤーが一時停止します。詳しくは、 [ビデオアセットの管理](manage-video-assets.md) を参照してください。

>[!NOTE]
>
>MXF ビデオ形式は、ビデオアセットの注釈では、まだサポートされていません。

1. [!DNL Assets] コンソールから、アセットカードの「**[!UICONTROL 編集]**」を選択して、アセット詳細ページを表示します。
1. ビデオを再生するには、「**[!UICONTROL プレビュー]**」をクリックします。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」をクリックします。注釈がビデオ内の特定の時点（フレーム）に追加されます。注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。
1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「20」と入力します。
1. タイムラインに表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。

## ベストプラクティスと制限事項 {#tips-limitations}

* [!DNL Dynamic Media] ライセンスがない場合、処理プロファイルを使用して処理できるのは、MP4 ファイルのみです。
* 処理プロファイルを使用して MP4 ファイルをトランスコードする場合は、次のガイドラインと制限が適用されます。

   * Apple ProRes ファイルは、最大解像度 1080p にのみトランスコードできます。
   * ソースファイルのビットレートが 200 Mbps を超える場合は、最大解像度 1080p にのみトランスコードできます。
   * ソースフレームレートが 60 fps 以上の場合、使用できるソースファイルの最大サイズは、次のとおりです。

      * 400 MB（4k トランスコードの場合）
      * 800 MB（1080p トランスコードの場合）
      * 8 GB（720p トランスコードの場合）

   * 4k 解像度にトランスコードできる最大ファイルサイズは、解像度 4k、ビットレート 12 Mbps、23 fps の MP4 ファイルで 2.55 GB です。

  **関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Dynamic Media ビデオドキュメント。](/help/assets/dynamic-media/video.md)
>* [処理プロファイルの使用、タイプ、設定について詳しく知る](/help/assets/asset-microservices-configure-and-use.md)。
