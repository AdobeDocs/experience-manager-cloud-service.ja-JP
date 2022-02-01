---
title: Dynamic Media Cloud Service の設定
description: Adobe Experience Manager as a Cloud Service で Dynamic Media を設定する方法を説明します。
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 446edfd83affb062585dca81052575b73c2e796f
workflow-type: tm+mt
source-wordcount: '3420'
ht-degree: 90%

---

# Dynamic Media Cloud Service の設定について {#configuring-dynamic-media}

開発、ステージング、実稼動など、様々な環境で Adobe Experience Manager を使用する場合は、環境ごとに Dynamic Media Cloud Services を設定します。

## Dynamic Media のアーキテクチャ図 {#architecture-diagram-of-dynamic-media}

以下のアーキテクチャ図に Dynamic Media の仕組みを示します。

新しいアーキテクチャでは、Experience Manager は、プライマリソースアセットを扱い、Dynamic Media と同期してアセットの処理や公開を行います。

1. プライマリソースアセットが Adobe Experience Manager as a Cloud Service にアップロードされると、Dynamic Media にレプリケートされます。その時点で、Dynamic Media は、ビデオエンコーディングおよび画像の動的バリアントなど、すべてのアセットの処理とレンディションの生成を扱います。
1. レンディションが生成されると、Experience Manager as a Cloud Service から、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager as a Cloud Service インスタンスに送り返されることはありません）。
1. コンテンツを公開および承認する準備ができると、Dynamic Media サービスがトリガーされて、コンテンツが配信サーバーにプッシュされ、CDN（コンテンツ配信ネットワーク）のコンテンツがキャッシュされます。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>次の機能では、Adobe Experience Manager - Dynamic Media に組み込まれている標準搭載の CDN を使用する必要があります。他のカスタム CDN は、これらの機能ではサポートされません。
>
>* [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)
>* [キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [ホットリンクの保護](/help/assets/dynamic-media/hotlink-protection.md)
>* [コンテンツの HTTP/2 配信](/help/assets/dynamic-media/http2faq.md)
>* CDN レベルでの URL リダイレクト
>* Akamai ChinaCDN（中国での最適な配信用）


<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Cloud Services での Dynamic Media 設定の作成 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. Experience Manager as a Cloud Service で、Experience Manager as a Cloud Service ロゴを選択し、グローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側にあるツールアイコンを選択したあと、**[!UICONTROL Cloud Services／Dynamic Media 設定]**&#x200B;に移動します。
1. Dynamic Media 設定ブラウザーページの左側のパネルで、「**[!UICONTROL グローバル]**」を選択します（「**[!UICONTROL グローバル]**」の左側にあるフォルダーアイコンを選択しないでください）。次に、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページで、タイトル、Dynamic Media アカウントの電子メールアドレス、パスワードを入力し、地域を選択します。この情報は、プロビジョニングの電子メールでアドビから提供されます。この電子メールを受け取っていない場合は、アドビカスタマーサポートにお問い合せください。
1. 「**[!UICONTROL Dynamic Media に接続]**」をクリックします。
1. **[!UICONTROL パスワードを変更]**&#x200B;ダイアログボックスの「**[!UICONTROL 新しいパスワード]**」フィールドに、8～25 文字の新しいパスワードを入力します。パスワードには、次のうち少なくとも 1 つを含める必要があります。

   * 大文字
   * 小文字
   * 数値
   * 特殊文字：`# $ & . - _ : { }`

   「**[!UICONTROL 現在のパスワード]**」フィールドは意図的に事前入力されており、操作時には非表示になっています。

   必要に応じて、パスワードの目のアイコンを選択してパスワードを表示し、入力または再入力したパスワードのスペルを確認できます。アイコンをもう一度選択すると、パスワードが非表示になります。

1. 「**[!UICONTROL パスワードを繰り返す]**」フィールドに新しいパスワードを再入力し、「**[!UICONTROL 完了]**」を選択します。

   新しいパスワードは、**[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」を選択したときに保存されます。

   **[!UICONTROL パスワードを変更]**&#x200B;ダイアログボックスで「**[!UICONTROL キャンセル]**」を選択した場合でも、新規作成の Dynamic Media 設定を保存する際に、新しいパスワードを入力する必要があります。

   [Dynamic Media のパスワードの変更](#change-dm-password)も参照してください。

1. 接続に成功したら、次のように設定できます。

   | プロパティ | 説明 |
   |---|---|
   | 会社 | Dynamic Media アカウントの名前です。異なるサブブランドや部門、またはステージングや実稼動環境のために、複数の Dynamic Media アカウントを持っている場合があります。 |
   | 会社のルートフォルダーのパス | 会社のルートフォルダーパスです。 |
   | アセットの公開 | 次の 3 つのオプションから選択できます。<br>**[!UICONTROL 即時&#x200B;]**：アセットがアップロードされると、システムによってアセットが取り込まれ、URL／埋め込みがすぐに提供されます。アセットを公開するためにユーザーが操作する必要はありません。<br>**[!UICONTROL アクティベーション時]**：URL／埋め込みリンクの提供の前に、最初にアセットを明示的に公開する必要があります。<br>**[!UICONTROL 選択的公開&#x200B;]**：アセットは、セキュリティで保護されたプレビューのみを目的として自動公開されます。また、パブリックドメインでの配信用に DMS7 に公開することなく、Experience Manager as a Cloud Service に明示的に公開することもできます。将来的には、このオプションでアセットを相互排他的に Experience Manager as a Cloud Service に公開したり、Dynamic Media に公開したりするようになります。つまり、アセットを DMS7 に公開して、スマート切り抜きや動的レンディションなどの機能を使用できます。または、アセットを、プレビュー用に Experience Manager as a Cloud Service でのみ公開し、パブリックドメイン配信用の DMS7 で公開しないようにすることもできます。 |
   | プレビューサーバーを保護 | セキュアなレンディションプレビューサーバーへの URL パスを指定できます。つまり、レンディションが生成されると、Experience Manager as a Cloud Service は、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager as a Cloud Service インスタンスに送り返されることはありません）。<br>自社のサーバーまたは特別なサーバーを使用する特別な取り決めがない限り、アドビでは、この設定を指定されたとおりにしておくことをお勧めします。 |
   | すべてのコンテンツを同期 | デフォルトで選択されています。Dynamic Media との同期で、アセットを選択して含めるまたは除外する場合は、このオプションの選択を解除します。このオプションの選択を解除すると、次の 2 つの Dynamic Media 同期モードから選択できるようになります。<br>**[!UICONTROL Dynamic Media 同期モード]**<br>**[!UICONTROL デフォルトで有効&#x200B;]**- フォルダーを特別に除外するようにマークしない限り、設定はすべてのフォルダーにデフォルトで適用されます。<!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL デフォルトで無効]** - 選択したフォルダーを Dynamic Media と同期するように明示的にマークしない限り、設定はどのフォルダーにも適用されません。 <br>選択したフォルダーを Dynamic Media と同期するようにマークするには、アセットフォルダーを選択した後、ツールバーで「**[!UICONTROL プロパティ]**」を選択します。「**[!UICONTROL 詳細]**」タブの **[!UICONTROL Dynamic Media 同期モード]**&#x200B;ドロップダウンリストで、次の 3 つのオプションから選択します。完了したら、「**[!UICONTROL 保存]**」を選択します。*注意：以前に「**すべてのコンテンツを同期**」を選択した場合、これら 3 つのオプションは使用できません。*[Dynamic Media のフォルダーレベルでの選択的公開の設定](/help/assets/dynamic-media/selective-publishing.md)も参照してください。<br>**[!UICONTROL 継承&#x200B;]**- フォルダーに明示的な同期値はなく、代わりに、上位フォルダーの 1 つまたはクラウド設定のデフォルトモードから同期値を継承します。継承された詳細なステータスは、ツールチップで表示されます。<br>**[!UICONTROL サブフォルダーで有効にする]** - このサブツリー内のすべての項目を Dynamic Media との同期に含めます。フォルダー固有の設定は、クラウド設定内のデフォルトモードよりも優先されます。<br>**[!UICONTROL サブフォルダーで無効にする&#x200B;]**- このサブツリー内のすべての項目を Dynamic Media との同期から除外します。 |

   >[!NOTE]
   >
   >Dynamic Media ではバージョン管理はサポートされていません。また、遅延アクティベーションは、Dynamic Media 設定の編集ページの「**[!UICONTROL アセットを公開]**」が「**[!UICONTROL アクティベーション時]**」に設定されている場合にのみ、アセットが最初にアクティベートされるまでの間に限って適用されます。
   >
   >
   >アセットがアクティベートされるとすぐに、すべての更新が S7 配信にライブ公開されます。

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 「**[!UICONTROL 保存]**」を選択します。Dynamic Media の新しいパスワードと設定が保存されます。「**[!UICONTROL キャンセル]**」を選択した場合、パスワードは更新されません。
1. **[!UICONTROL Dynamic Media の設定]**&#x200B;ダイアログボックスで、「**[!UICONTROL OK]**」を選択して設定を開始します。

   >[!IMPORTANT]
   >
   >新しい Dynamic Media 設定が完了すると、Experience Manager as a Cloud Service のインボックス内にステータス通知が届きます。
   >
   >このインボックス通知は、設定が成功したかどうかを知らせるものです。
   > 詳しくは、[新しい Dynamic Media 設定のトラブルシューティング](#troubleshoot-dm-config)と[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)を参照してください。

1. 公開前にDynamic Mediaコンテンツを安全にプレビューするには、Experience Manageras a Cloud Serviceではトークンベースの検証が使用されるので、Experience Manager作成者は、Dynamic Mediaコンテンツをデフォルトでプレビューできます。 ただし、次の操作は可能です。 *許可リスト* コンテンツを安全にプレビューするためのアクセスをユーザーに提供する IP の数が増えました。 このアクションをas a Cloud ServiceのExperience Managerで設定するには [Image Server 用のDynamic Media公開設定の指定 — 「セキュリティ」タブ](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

これで基本設定は完了です。Dynamic Media を使用する準備が整いました。

設定をさらにカスタマイズする場合は、[Dynamic Media での詳細設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)で示す任意のタスクをオプションで実行できます。

### 新しい Dynamic Media 設定のトラブルシューティング {#troubleshoot-dm-config}

新しい Dynamic Media 設定が完了すると、Experience Manager as a Cloud Service のインボックスにステータス通知が届きます。この通知は、以下の各インボックス画像に示すように、設定が成功したかどうかを知らせるものです。

![Experience Manager インボックス成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager インボックス失敗](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)も参照してください。

**新しい Dynamic Media 設定のトラブルシューティングを行うには：**

1. Experience Manager as a Cloud Service ページの右上隅にあるベルアイコンを選択し、「**[!UICONTROL すべて表示]**」を選択します。
1. インボックスページで成功通知を選択して、設定のステータスとログの概要を読み取ります。

   設定に失敗した場合は、次のスクリーンショットに示すような失敗通知を選択します。

   ![Dynamic Media のセットアップの失敗](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. **[!UICONTROL DMSETUP]** ページで、失敗を説明する設定詳細を確認します。特に、エラーメッセージやエラーコードは控えておいてください。この情報については、アドビカスタマーサポートにお問い合わせください。

   ![Dynamic Media 設定ページ](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Dynamic Media のパスワードの変更 {#change-dm-password}

Dynamic Media でのパスワードの有効期限は、現在のシステム日付から 100 年間に設定されています。

パスワードには、次のうち少なくとも 1 つを含める必要があります。

* 大文字
* 小文字
* 数値
* 特殊文字：`# $ & . - _ : { }`

必要に応じて、パスワードの目のアイコンを選択してパスワードを表示し、入力または再入力したパスワードのスペルを確認できます。アイコンをもう一度選択すると、パスワードが非表示になります。

変更したパスワードは、**[!UICONTROL Dynamic Media 設定を編集]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」を選択したときに保存されます。

1. Experience Manager as a Cloud Service で、Experience Manager as a Cloud Service ロゴを選択し、グローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側にあるツールアイコンを選択したあと、**[!UICONTROL Cloud Services／Dynamic Media 設定]**&#x200B;に移動します。
1. Dynamic Media 設定ブラウザーページの左側のペインで「**[!UICONTROL global]**」を選択します。**[!UICONTROL global]** の左側にあるフォルダーアイコンを選択しないでください。次に、「**[!UICONTROL 編集]**」を選択します。
1. **[!UICONTROL Dynamic Media 設定を編集]**&#x200B;ページで「**[!UICONTROL パスワード]**」フィールドのすぐ下の「**[!UICONTROL パスワードを変更]**」を選択します。
1. **[!UICONTROL パスワードを変更]**&#x200B;ダイアログボックスで以下を行います。

   * 「**[!UICONTROL 新しいパスワード]**」フィールドに、新しいパスワードを入力します。

      「**[!UICONTROL 現在のパスワード]**」フィールドは意図的に事前入力されており、操作時には非表示になっています。

   * 「**[!UICONTROL パスワードを繰り返す]**」フィールドに新しいパスワードを再入力し、「**[!UICONTROL 完了]**」を選択します。

1. **[!UICONTROL Dynamic Media 設定を編集]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」を選択したあと、「**[!UICONTROL OK]**」を選択します。

## （オプション）Dynamic Media での詳細設定{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Media のセットアップと設定をさらにカスタマイズしたり、パフォーマンスを最適化したりする場合は、次の&#x200B;*オプション*&#x200B;タスクを 1 つまたは複数実行できます。

* [（オプション）Dynamic Media 設定のセットアップと設定 ](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（オプション）Dynamic Media のパフォーマンスの調整](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （オプション）Dynamic Media 設定のセットアップと設定  {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Dynamic Media Classic のユーザーインターフェイスを使用し、Dynamic Media の設定を変更します。

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

セットアップおよび設定タスクには、次のものが含まれます。

* [Image Server 用のDynamic Media公開設定の指定](#publishing-setup-for-image-server)
* [Dynamic Mediaの一般設定](#configuring-application-general-settings)
* [カラーマネジメントの設定](#configuring-color-management)
* [サポートされている形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)
* [サポートされていない形式の MIME タイプの追加](#adding-mime-types-for-unsupported-formats)

<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Image Server 用のDynamic Media公開設定の指定 {#publishing-setup-for-image-server}

Dynamic Mediaの公開設定ページでは、AdobeDynamic Mediaサーバーから Web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。

詳しくは、 [Image Server 用のDynamic Media公開設定の指定](/help/assets/dynamic-media/dm-publish-settings.md).

#### Dynamic Mediaの一般設定 {#configuring-application-general-settings}

Dynamic Mediaの設定 **[!UICONTROL 公開サーバ名]** URL と **[!UICONTROL オリジンサーバー名]** URL。 また、 **[!UICONTROL アプリケーションにアップロード]** 設定と **[!UICONTROL デフォルトのアップロードオプション]** すべて、特定の使用例に基づいておこないます。

詳しくは、 [Dynamic Mediaの一般設定](/help/assets/dynamic-media/dm-general-settings.md).

#### カラーマネジメントの設定 {#configuring-color-management}

Dynamic Media カラーマネジメントを使用すると、アセットをカラー補正できます。カラー補正により、取り込まれたアセットは、カラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、CMYK、RGB またはグレー出力を使用するターゲットのカラースペースに補正されます。

[画像プリセットの設定](/help/assets/dynamic-media/managing-image-presets.md)を参照してください。

画像を要求する際にカラー補正を有効にするためのデフォルトのカラープロパティを設定するには：

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、プロビジョニング時に提供された資格情報を使用してアカウントにログインします。
1. **[!UICONTROL 設定／アプリケーション設定]**&#x200B;に移動します。
1. 「**[!UICONTROL 公開設定]**」領域を展開して、「**[!UICONTROL Image Server]**」を選択します。パブリッシュインスタンスのデフォルトを設定する際に、「**[!UICONTROL 公開コンテキスト]**」を「**[!UICONTROL 画像サービング]**」に設定します。
1. 例えば「**[!UICONTROL カラーマネジメント属性]**」領域のプロパティなど、変更が必要なプロパティにスクロールします。
次のカラー補正プロパティを設定できます。

   | プロパティ | 説明 |
   |---|---|
   | CMYK の初期設定カラースペース | 初期設定の CMYK カラープロファイルの名前。 |
   | グレースケールのデフォルトのカラースペース | 初期設定のグレーカラープロファイルの名前。 |
   | RGB の初期設定カラースペース | 初期設定の RGB カラープロファイルの名前。 |
   | カラー変換レンダリングインテント | レンダリングインテントを指定します。指定できる値は、**[!UICONTROL 知覚的]**、**[!UICONTROL 相対的な色域を維持]**、**[!UICONTROL 彩度]**、**[!UICONTROL 絶対的な色域を維持]**&#x200B;です。アドビでは、デフォルトとして&#x200B;**[!UICONTROL 相対的]**&#x200B;をお勧めします。 |

1. 「**[!UICONTROL 保存]**」を選択します。

例えば、**[!UICONTROL RGB の初期設定カラースペース]**&#x200B;を *sRGB* に、**[!UICONTROL CMYK の初期設定カラースペース]**&#x200B;を *WebCoated* に設定できます。

それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルを持たない RGB 画像は、*sRGB* カラースペースにあると見なされます。
* カラープロファイルを持たない CMYK 画像は、*WebCoated* カラースペースにあると見なされます。
* RGB 出力を返す動的レンディションは、RGB 出力を *sRGB* カラースペース内で返します。
* CMYK 出力を返す動的レンディションは、CMYK 出力を *WebCoated* カラースペース内で返します。

#### サポートされている形式の MIME タイプの編集 {#editing-mime-types-for-supported-formats}

Dynamic Media によって処理されるアセットタイプを定義して、高度なアセット処理パラメーターをカスタマイズできます。例えば、アセット処理パラメーターを指定して次のことができます。

* Adobe PDF を eCatalog アセットに変換する。
* Adobe Photoshop ドキュメント（.PSD）をパーソナライズ用のバナーテンプレートアセットに変換する。
* Adobe Illustrator ファイル（.AI）または Adobe Photoshop Encapsulated PostScript® ファイル（.EPS）をラスタライズする。
* [ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)および[イメージングプロファイル](/help/assets/dynamic-media/image-profiles.md)は、それぞれ、ビデオおよび画像の処理を定義するのに使用できます。

[アセットのアップロード](/help/assets/add-assets.md)を参照してください。

**サポートされている形式の MIME タイプを編集するには：**

1. Experience Manager as a Cloud Service で、Experience Manager as a Cloud Service ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL 一般／CRXDE Lite]** に移動します。
1. 左側のパネルで、次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME タイプ](assets/mimetypes.png)

1. MIME タイプフォルダーで、MIME タイプを選択します。
1. CRXDE Lite ページの右側の下部で、次の操作を行います。

   * 「**[!UICONTROL 有効]**」フィールドをダブルタップします。デフォルトでは、すべてのアセットの MIME タイプが有効になって（**[!UICONTROL true]** に設定されて）います。これは、処理に関してアセットが Dynamic Media に同期されることを意味します。このアセットの MIME タイプを処理から除外する場合、この設定を **[!UICONTROL false]** に変更します。

   * **[!UICONTROL jobParam]** をダブルタップして、関連するテキストフィールドを開きます。特定の MIME タイプに使用可能な、許容される処理パラメーター値のリストについては、[サポートされる MIME タイプ](/help/assets/file-format-support.md)を参照してください。

1. 次のいずれかの操作を行います。
   * 手順 3～4 を繰り返して、その他の MIME タイプを編集します。
   * CRXDE Lite ページのメニューバーで、「**[!UICONTROL すべて保存]**」を選択します。

1. ページの左上隅にある「**[!UICONTROL CRXDE Lite]**」を選択して、Experience Manager as a Cloud Service に戻ります。

#### サポートされていない形式の MIME タイプの追加 {#adding-mime-types-for-unsupported-formats}

Experience Manager Assets でサポートされていない形式のカスタム MIME タイプを追加できます。CRXDE Lite に追加した新しいノードが Experience Manager によって削除されないようにするには、MIME タイプを `image_` の前に移動します。また、有効な値が **[!UICONTROL false]** に設定されていることを確認します。

**サポートされていない形式のカスタム MIME タイプを追加するには:**

1. Experience Manager as a Cloud Service で、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動します。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新しいブラウザータブが開き、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;ページが表示されます。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. ページ上で、*Adobe CQ Scene7 Asset MIME type Service* という名前まで下にスクロールします。次のスクリーンショットを参照してください。名前の右側にある&#x200B;**[!UICONTROL 設定値を編集]**（鉛筆アイコン）をタップします。

   ![設定値の編集](assets/2019-08-02_16-44-56.png)

1. **Adobe CQ Scene7 Asset MIME type Service** ページで、任意のプラス記号アイコン「+」を選択します。新しい MIME タイプを追加する場合に、テーブルで選択するプラス記号の場所はすぐわかります。

   ![Adobe CQ Scene7 Asset Mime Type Service](assets/2019-08-02_16-27-27.png)

1. 空のテキストフィールドに追加した `DWG=image/vnd.dwg` を入力します。

   `DWG=image/vnd.dwg` MIME タイプはサンプル用です。ここで追加する MIME タイプは、その他のサポートされていない形式でもかまいません。

   ![DWG MIME タイプの追加](assets/2019-08-02_16-36-36.png)

1. ページの右下隅にある「**[!UICONTROL 保存]**」を選択します。

   この時点で、Adobe Experience Manager Web コンソール設定ページが開いているブラウザータブを閉じることができます。

1. Experience Manager as a Cloud Service のコンソールを開いているブラウザータブに戻ります。
1. Experience Manager as a Cloud Service で、**[!UICONTROL ツール／一般／CRXDE Lite]** に移動します。

   ![ツール/一般/CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. 左側のパネルで、次の場所に移動します。

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. `image_vnd.dwg` MIME タイプをドラッグし、次のスクリーンショットに示すように、ツリー内の `image_` の上にドロップします。

   ![DWG ファイルをCRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. MIME `image_vnd.dwg` を選択したまま、「**[!UICONTROL プロパティ]**」タブの&#x200B;**[!UICONTROL 有効]**&#x200B;行の&#x200B;**[!UICONTROL 値]**&#x200B;列見出しの値をダブルタップします。**[!UICONTROL 値]**&#x200B;ドロップダウンリストが開きます。
1. フィールドに `false` と入力します（または、ドロップダウンリストから「**[!UICONTROL false]**」を選択します）。

   ![CRXDE Liteでの MIME タイプの編集](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。

### （オプション）Dynamic Media のパフォーマンスの調整 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> のスムーズな実行を維持するために、アドビでは、次の同期パフォーマンス／拡張性の微調整のヒントをお勧めします。

* [様々なファイル形式の処理に対応する定義済みジョブパラメーターの更新](#update-job-para).
* [事前定義済みの Granite Workflow Queue（ビデオアセット）ワーカースレッドを更新する](#update-granite-workflow-queue-worker-threads-video)
* [事前定義済みの Granite の一時的なワークフローキュー（画像および非ビデオアセット）ワーカースレッドを更新する](#update-granite-transient-workflow-queue-worker-threads-images).
* [Dynamic Media Classic(Scene7) サーバーへの最大アップロード接続数を更新する](#update-max-s7-upload-connections).

#### 様々なファイル形式の処理に対応する定義済みジョブパラメーターの更新 {#update-job-para}

ジョブパラメーターを調整して、ファイルアップロード時の処理を高速化できます。例えば、PSD ファイルをアップロードしても、テンプレートとして処理しない場合は、レイヤー抽出を false（オフ）に設定できます。この場合、調整されたジョブパラメーターは次のように表示されます。`process=None&createTemplate=false`

テンプレートの作成を有効にする場合は、次のパラメーターを使用します。`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

PDF ファイル、PostScript® ファイル、PSD ファイルには、以下の「調整済み」ジョブパラメーターを使用することをお勧めします。

| ファイルタイプ | 推奨されるジョブパラメーター |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

これらのパラメーターをアップデートするには、「[サポートされている形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)」を参照してください。

「[サポートされていない形式のカスタム MIME タイプの追加](#adding-mime-types-for-unsupported-formats)」も参照してください。

#### 事前定義済みの Granite Workflow Queue（ビデオアセット）ワーカースレッドを更新する {#update-granite-workflow-queue-worker-threads-video}

Granite のワークフローキューは、一時的でないワークフローに使用されます。Dynamic Media では、**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローでビデオを処理するために使用されます。

**事前定義済みの Granite Workflow Queue（ビデオアセット）ワーカースレッドを更新するには：**

1. `https://<server>/system/console/configMgr` に移動して、**Queue: Granite Workflow Queue** を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   デフォルトでは、並列ジョブの最大数は、使用可能な CPU コア数によって異なります。例えば、4 コアサーバーでは、2 つの作業スレッドが割り当てられます。（0.0～1.0 の値は比率ベースです。1 より大きい場合は作業スレッドが割り当てられます）。

   ほとんどの事例では、デフォルト設定の 0.5 で十分です。

   ![ジョブ処理キューの設定](assets/chlimage_1-1.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

#### 事前定義済みの Granite 一時的なワークフローキューワーカースレッドを更新する {#update-granite-transient-workflow-queue-worker-threads-images}

Granite の一時的なワークフローキューは、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローに使用されます。Dynamic Mediaでは、画像および非ビデオアセットの取り込みと処理に使用されます。

**事前定義済みの Granite 一時的なワークフローキューワーカースレッドを更新するには：**

1. **Adobe Experience Manager Web Console Configuration**（`http://<host>:<port>/system/console/configMgr`）に移動します。
1. **キュー：Granite 一時的なワークフローキュー**&#x200B;を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   **[!UICONTROL 並列ジョブの最大数]**&#x200B;を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初回移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

#### Dynamic Media Classic(Scene7) サーバーへの最大アップロード接続数を更新する {#update-max-s7-upload-connections}

「 Dynamic Media Classic(Scene7) 接続をアップロード」設定は、Experience ManagerアセットをDynamic Media Classicサーバーに同期します。

**Dynamic Media Classic(Scene7) サーバーへの最大アップロード接続数を更新するには：**

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl` に移動します。
1. 「**[!UICONTROL 接続数]**」フィールドおよび「**[!UICONTROL アクティブなジョブのタイムアウト]**」フィールド、またはその両方で、必要に応じて数値を変更します。

   「**[!UICONTROL 接続数]**」設定は、Experience Manager が Dynamic Media へのアップロードに使用できる HTTP 接続の最大数を制御します。通常は、事前定義の 10 個で十分です。

   「**[!UICONTROL Active job timeout]**」設定は、アップロードされた Dynamic Media アセットが配信サーバーで公開されるまでの待機時間を決定します。デフォルトでは、この値は 2100 秒または 35 分です。

   ほとんどの事例では、2100 の設定で十分です。

   ![Adobe Scene7 Upload Service](assets/chlimage_1-2.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
