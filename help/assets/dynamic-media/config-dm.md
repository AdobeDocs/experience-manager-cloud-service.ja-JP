---
title: Dynamic Media Cloud Service の設定
description: Adobe Experience ManagerのDynamic MediaをCloud Serviceとして設定する方法を説明します。
role: Administrator,Business Practitioner
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '4053'
ht-degree: 54%

---

# Dynamic Media Cloud Service の設定について {#configuring-dynamic-media}

開発、ステージング、実稼働など、様々な環境でAdobe Experience Managerを使用する場合は、それらの環境ごとにDynamic MediaCloud Servicesを設定します。

## Dynamic Media のアーキテクチャ図 {#architecture-diagram-of-dynamic-media}

以下のアーキテクチャ図に Dynamic Media の仕組みを示します。

新しいアーキテクチャでは、Experience Managerは主要なソースアセットを管理し、Dynamic Mediaと同期してアセットの処理と公開を行います。

1. 主要なソース資産がCloud ServiceとしてAdobe Experience Managerにアップロードされると、Dynamic Mediaに複製されます。 その時点で、Dynamic Media は、ビデオエンコーディングおよび画像の動的バリアントなど、すべてのアセットの処理とレンディションの生成を扱います。
1. レンディションの生成後、Cloud ServiceとしてのExperience Managerは、リモートのDynamic Mediaレンディションに安全にアクセスし、プレビューできます(バイナリがCloud ServiceインスタンスとしてExperience Managerに送り返されることはありません)。
1. コンテンツの公開と承認の準備が整ったら、Dynamic Mediaサービスは配信サーバーにコンテンツをプッシュして、CDN(コンテンツ配信ネットワーク)でコンテンツをキャッシュするようトリガーします。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>次の機能のリストでは、Adobe Experience Manager-Dynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。 これらの機能では、その他のカスタムCDNはサポートされません。
>
>* [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)
>* [キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [ホットリンクの保護](/help/assets/dynamic-media/hotlink-protection.md)
>* [コンテンツの HTTP/2 配信](/help/assets/dynamic-media/http2faq.md)
>* CDNレベルでのURLリダイレクト
>* Akamai ChinaCDN(中国での最適な配信のため)


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

## Cloud ServicesでのDynamic Media構成の作成{#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. Cloud ServiceとしてのExperience Managerで、Experience ManagerをCloud Serviceのロゴとしてタップし、グローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側で、ツールアイコンをタップし、**[!UICONTROL Cloud Services/Dynamic Media設定]**&#x200B;をタップします。
1. Dynamic Media構成ブラウザーページの左ペインで、**[!UICONTROL グローバル]**&#x200B;をタップします（**[!UICONTROL グローバル]**&#x200B;の左にあるフォルダーアイコンはタップまたは選択しないでください）。 次に、「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページで、タイトル、Dynamic Media アカウントの電子メールアドレス、パスワードを入力し、地域を選択します。この情報は、プロビジョニング用の電子メールにAdobeが提供します。 この電子メールを受信しなかった場合は、Adobeカスタマーケアにお問い合わせください。
1. 「**[!UICONTROL Dynamic Media に接続]**」をクリックします。
1. **[!UICONTROL パスワードを変更]**&#x200B;ダイアログボックスの「**[!UICONTROL 新しいパスワード]**」フィールドに、8～25 文字の新しいパスワードを入力します。パスワードには、次のうち少なくとも 1 つを含める必要があります。

   * 大文字
   * 小文字
   * 数値
   * 特殊文字：`# $ & . - _ : { }`

   「**[!UICONTROL 現在のパスワード]**」フィールドは、意図的に事前入力され、操作から隠されています。

   必要に応じて、パスワードの目のアイコンをタップしてパスワードを表示し、入力または再入力したパスワードのスペルを確認できます。アイコンをもう一度タップすると、パスワードが非表示になります。

1. 「**[!UICONTROL パスワードを繰り返す]**」フィールドに新しいパスワードを再入力し、「**[!UICONTROL 完了]**」をタップします。

   新しいパスワードは、**[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」をタップしたときに保存されます。

   **[!UICONTROL パスワードの変更]**&#x200B;ダイアログボックスで「**[!UICONTROL キャンセル]**」をタップした場合、新しく作成したDynamic Media設定を保存する際に、新しいパスワードを入力する必要があります。

   [Dynamic Media のパスワードの変更](#change-dm-password)も参照してください。

1. 接続に成功したら、次のように設定できます。

   | プロパティ | 説明 |
   |---|---|
   | 会社 | Dynamic Media アカウントの名前です。様々なサブブランド、部門、ステージング/実稼動環境用に複数のDynamic Mediaアカウントを持つ可能性があります。 |
   | 会社のルートフォルダーのパス | 会社のルートフォルダーパスです。 |
   | アセットの公開 | 次の 3 つのオプションから選択できます。<br>**[!UICONTROL 即時&#x200B;]**：アセットがアップロードされると、システムによってアセットが取り込まれ、URL／埋め込みがすぐに提供されます。アセットを公開するためにユーザーが操作する必要はありません。<br>**[!UICONTROL アクティベーション時]**:URL/埋め込みリンクを指定する前に、最初にアセットを明示的に公開する必要があります。<br>**[!UICONTROL 一部のみの発行&#x200B;]**:アセットは、セキュリティで保護されたプレビューのみを目的として自動公開されます。また、パブリックドメインでの配信用にDMS7に公開することなく、Cloud ServiceとしてExperience Managerに明示的に公開することもできます。 今後は、Cloud ServiceとしてExperience Managerにアセットを公開し、お互いに排他的にDynamic Mediaにアセットを公開する予定です。 つまり、アセットを DMS7 に公開して、スマート切り抜きや動的レンディションなどの機能を使用できます。または、プレビュー用のCloud Serviceとして、Experience Manager内のアセットのみをプレビュー用のアセットとして公開することもできます。これらの同じアセットは、パブリックドメインでの配信のために、DMS7で公開されません。 |
   | プレビューサーバーを保護 | セキュアなレンディションプレビューサーバーへの URL パスを指定できます。つまり、レンディションの生成後、Cloud ServiceとしてのExperience Managerは、リモートのDynamic Mediaレンディションに安全にアクセスし、プレビューできます(バイナリがCloud ServiceインスタンスとしてExperience Managerに送り返されることはありません)。<br>独自の会社のサーバーまたは特別なサーバーを使用する特別な設定がない限り、Adobeはこの設定を指定のままにすることをお勧めします。 |
   | すべてのコンテンツを同期 | デフォルトで選択されています。Dynamic Media との同期で、アセットを選択して含めるまたは除外する場合は、このオプションの選択を解除します。このオプションの選択を解除すると、次の 2 つの Dynamic Media 同期モードから選択できるようになります。<br>**[!UICONTROL Dynamic Media 同期モード]**<br>**[!UICONTROL デフォルトで有効&#x200B;]**：フォルダーを特別に除外するようにマークしない限り、設定はすべてのフォルダーにデフォルトで適用されます。<!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL デフォルトで無効]**：選択したフォルダーを Dynamic Media と同期するように明示的にマークしない限り、設定はどのフォルダーにも適用されません。<br>選択したフォルダーをDynamic Mediaと同期するようにマークするには、アセットフォルダーを選択し、ツールバーで「 **[!UICONTROL プロパティ]**」をタップします。「**[!UICONTROL 詳細]**」タブの **[!UICONTROL Dynamic Media 同期モード]**&#x200B;ドロップダウンリストで、次の 3 つのオプションから選択します。完了したら、「**[!UICONTROL 保存]**」をタップします。*注意：以前に「**すべてのコンテンツを同期**」を選択した場合、これら 3 つのオプションは使用できません。* Dynamic Mediaのフォルダーレベルでの一部のみの発行の [操作も参照してください](/help/assets/dynamic-media/selective-publishing.md)。<br>**[!UICONTROL 継承&#x200B;]**:フォルダーに明示的な同期値がありません。代わりに、フォルダーは、その上位フォルダーの1つ、またはクラウド設定のデフォルトモードから同期値を継承します。ツールチップを介した継承されたショーの詳細なステータス。<br>**[!UICONTROL サブフォルダーに対して有効にする]**:Dynamic Mediaと同期するために、このサブツリーの内容をすべて含めます。フォルダー固有の設定は、クラウド設定内のデフォルトモードよりも優先されます。<br>**[!UICONTROL サブフォルダーに対して無効&#x200B;]**:このサブツリーのすべてをDynamic Mediaに同期から除外します。 |

   >[!NOTE]
   >
   >Dynamic Media ではバージョン管理はサポートされていません。また、遅延アクティベーションは、Dynamic Media設定を編集ページの&#x200B;**[!UICONTROL アセットを発行]**&#x200B;が&#x200B;**[!UICONTROL アクティベーション]**&#x200B;に設定されている場合にのみ適用されます。その後、アセットが初めてアクティブ化されるまでのみ有効です。
   >
   >
   >アセットがアクティベートされるとすぐに、すべての更新が S7 配信にライブ公開されます。

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 「**[!UICONTROL 保存]**」をタップします。Dynamic Media の新しいパスワードと設定が保存されます。「**[!UICONTROL キャンセル]**」をタップした場合、パスワードは更新されません。
1. **[!UICONTROL Dynamic Media の設定]**&#x200B;ダイアログボックスで、「**[!UICONTROL OK]**」をタップして設定を開始します。

   >[!IMPORTANT]
   >
   >新しいDynamic Media構成のセットアップが完了すると、Cloud ServiceのインボックスとしてExperience Manager内にステータス通知が届きます。
   >
   >このインボックス通知は、設定が成功したかどうかを知らせるものです。
   > 詳しくは、[新しい Dynamic Media 設定のトラブルシューティング](#troubleshoot-dm-config)と[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)を参照してください。

1. Dynamic Mediaコンテンツが公開される前に安全にプレビューできるように、Cloud ServiceとしてのExperience Managerはデフォルトでトークンベースの認証を使用します。 ただし、より多くのIPを「許可リスト」して、安全なプレビューコンテンツへのアクセスをユーザーに提供することもできます。 このアクションを設定するには、次の手順を実行します。<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。資格情報とログインの詳細は、プロビジョニング時にAdobeから提供されました。 この情報がない場合は、Adobeカスタマーケアにお問い合わせください。
   * ページの右上隅近くにあるナビゲーションバーで、**[!UICONTROL 設定]**/**[!UICONTROL アプリケーション設定]**/**[!UICONTROL 公開設定]**/**[!UICONTROL Image Server]**&#x200B;をタップします。
   * Image Server公開ページの&#x200B;**[!UICONTROL 公開コンテキスト]**&#x200B;ドロップダウンリストで、「**[!UICONTROL 画像サービングをテスト]**」を選択します。
   * 「クライアントアドレスフィルター」で、**[!UICONTROL 「追加」]**&#x200B;をタップします。
   * アドレスを有効（有効）にするには、チェックボックスを選択し、Experience Manager作成者インスタンスのIPアドレスを入力します（ディスパッチャーIPではありません）。
   * 「**[!UICONTROL 保存]**」をクリックします。

これで基本設定は完了です。Dynamic Media を使用する準備が整いました。

設定をさらにカスタマイズする場合は、[Dynamic Media での詳細設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)で示す任意のタスクをオプションで実行できます。

### 新しい Dynamic Media 設定のトラブルシューティング {#troubleshoot-dm-config}

新しいDynamic Media構成のセットアップが完了すると、Cloud ServiceのインボックスとしてExperience Manager内にステータス通知が届きます。 この通知は、以下の各インボックス画像に示すように、設定が成功したかどうかを知らせるものです。

![Experience Managerインボックス成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager受信トレイエラー](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

[インボックス](/help/sites-cloud/authoring/getting-started/inbox.md)も参照してください。

**新しい Dynamic Media 設定のトラブルシューティングをおこなうには：**

1. Experience Managerの右上隅近くにあるCloud Serviceページでベルのアイコンをタップし、「**[!UICONTROL 表示」「すべて]**」をタップします。
1. インボックスページで成功通知をタップして、設定のステータスとログの概要を読み取ります。

   設定に失敗した場合は、次のスクリーンショットに示すような失敗通知をタップします。

   ![Dynamic Mediaのセットアップに失敗しました](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. **[!UICONTROL DMSETUP]** ページで、失敗を説明する設定詳細を確認します。特に、エラーメッセージやエラーコードは控えておいてください。この情報については、Adobeカスタマーケアにお問い合わせください。

   ![Dynamic Media設定ページ](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Dynamic Media のパスワードの変更 {#change-dm-password}

Dynamic Media でのパスワードの有効期限は、現在のシステム日付から 100 年間に設定されています。

パスワードには、次のうち少なくとも 1 つを含める必要があります。

* 大文字
* 小文字
* 数値
* 特殊文字：`# $ & . - _ : { }`

必要に応じて、パスワードの目のアイコンをタップしてパスワードを表示し、入力または再入力したパスワードのスペルを確認できます。アイコンをもう一度タップすると、パスワードが非表示になります。

変更したパスワードは、**[!UICONTROL Dynamic Media 設定を編集]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」をタップしたときに保存されます。

1. Cloud ServiceとしてのExperience Managerで、Experience ManagerをCloud Serviceのロゴとしてタップし、グローバルナビゲーションコンソールにアクセスします。
1. コンソールの左側で、ツールアイコンをタップし、**[!UICONTROL Cloud Services/Dynamic Media設定]**&#x200B;をタップします。
1. [Dynamic Media構成ブラウザ]ページの左ペインで、**[!UICONTROL グローバル]**&#x200B;をタップします。**[!UICONTROL グローバル]**&#x200B;の左にあるフォルダーアイコンをタップまたは選択しないでください。次に、「**[!UICONTROL 編集]**」をタップします。
1. **[!UICONTROL Dynamic Media設定]**&#x200B;を編集ページの&#x200B;**[!UICONTROL パスワード]**&#x200B;フィールドのすぐ下で、**[!UICONTROL パスワードの変更]**&#x200B;をタップします。
1. **[!UICONTROL パスワードを変更]**&#x200B;ダイアログボックスで以下をおこないます。

   * 「**[!UICONTROL 新しいパスワード]**」フィールドに、新しいパスワードを入力します。

      「**[!UICONTROL 現在のパスワード]**」フィールドは、意図的に事前入力され、操作から隠されています。

   * 「**[!UICONTROL パスワードを繰り返す]**」フィールドに新しいパスワードを再入力し、「**[!UICONTROL 完了]**」をタップします。

1. **[!UICONTROL Dynamic Media設定を編集]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」をタップし、「**[!UICONTROL OK]**」をタップします。

## （オプション）Dynamic Media での詳細設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Mediaの設定とセットアップをさらにカスタマイズしたり、パフォーマンスを最適化するには、次の&#x200B;*オプション*&#x200B;タスクを1つ以上実行します。

* [Dynamic Media 設定のセットアップと設定](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（オプション）Dynamic Media のパフォーマンスの調整](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （オプション）Dynamic Media 設定のセットアップと設定 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Dynamic Mediaクラシックユーザインターフェイスを使用して、Dynamic Media設定を変更します。

上記のタスクの一部では、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開いて、アカウントにログインする必要があります。

セットアップおよび設定タスクには、次のものが含まれます。

* [Image Server の公開設定 ](#publishing-setup-for-image-server)
* [アプリケーションの一般設定の指定](#configuring-application-general-settings)
* [カラーマネジメントの設定](#configuring-color-management)
* [サポートされる形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)
* [サポートされていない形式のカスタム MIME タイプの追加](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Image Server の公開設定           {#publishing-setup-for-image-server}

公開設定は、アセットがデフォルトで Dynamic Media からどのように配信されるかを決定します。設定が指定されていない場合、Dynamic Media は、公開設定で定義されたデフォルト設定に従ってアセットを配信します。例えば、解像度属性が含まれていない画像を配信するように要求した場合、画像は初期設定のオブジェクト解像度設定で配信されます。

公開設定を指定するには、Dynamic Media Classic で、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。

Image Server 画面では、画像を配信するためのデフォルト設定を指定します。各設定の説明については、UI 画面を参照してください。

**[!UICONTROL 要求属性]** - これらの設定は、サーバーから配信できる画像を制限します。**[!UICONTROL 初期設定の要求属性]** - これらの設定は、画像のデフォルトの表示に関係します。**[!UICONTROL 共通のサムネール属性]** - これらの設定は、サムネール画像のデフォルトの表示に関係します。**[!UICONTROL カタログフィールドの初期設定]** - これらの設定は、画像の解像度とデフォルトのサムネールの種類に関係します。**[!UICONTROL カラーマネジメント属性]** - これらの設定は、使用する ICC カラープロファイルを決定します。**[!UICONTROL 互換性の属性]** - この設定により、後方互換性の確保のためにバージョン 3.6 の場合と同様に、テキストレイヤーの先頭と末尾の段落が処理されます。**[!UICONTROL ローカリゼーションサポート]** - これらの設定によって、複数のロケール属性を管理します。また、ロケールマップ文字列を指定することもできます。これにより、ビューアのツールチップで使用する言語を指定できます。**[!UICONTROL ローカリゼーションサポート]**&#x200B;の設定について詳しくは、[アセットのローカライゼーションを設定する場合の考慮事項](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html?lang=ja#considerations-when-setting-up-localization-of-assets)を参照してください。

#### アプリケーションの一般設定の指定 {#configuring-application-general-settings}

アプリケーションの一般設定ページを開くには、Dynamic Media Classic グローバルナビゲーションバーで、**[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

**[!UICONTROL サーバー -]**アカウントのプロビジョニング時に、会社に割り当てられているサーバーが Dynamic Media によって自動的に提供されます。これらのサーバーは、WebサイトやアプリケーションのURL文字列の作成に使用されます。 これらの URL 呼び出しは、アカウントに固有です。Cloud ServiceサポートとしてExperience Managerからサーバー名を指示された場合を除き、サーバー名は一切変更しないでください。
**[!UICONTROL 画像を上書き]** - Dynamic Media は、2 つのファイルが同じ名前を持つことを許可しません。各項目の URL ID（ファイル名から拡張子を取り除いた部分）は一意である必要があります。これらのオプションは、置き換えるアセットのアップロード方法、つまり元のアセットを置き換えるか、重複させるかを指定します。重複するアセット名には「-1」が付けられます（例えば、chair.tif は chair-1.tif に変更されます）。これらのオプションは、元のアセットとは別のフォルダにアップロードされたアセット、または元のアセットとは異なるファイル拡張子を持つアセットに影響を与えます。
**[!UICONTROL 現在のフォルダーでベース名と拡張子が同じファイルを上書き]** - このオプションは最も厳格な置換規則です。置き換え画像は、元の画像と同じフォルダにアップロードし、元の画像と同じファイル拡張子を持つ必要があります。 これらの要件が満たされない場合は、重複する画像が作成されます。Cloud ServiceーとしてのExperience Managerとの一貫性を維持するには、常に「現在のフォルダーでベース名と拡張子が同じ&#x200B;**[!UICONTROL を上書き」を選択します。]****[!UICONTROL 任意のフォルダでベース名と拡張子が同じファイルを上書き]**  — 置き換え画像と元の画像のファイル拡張子が同じである必要があります。例えば、chair.jpgはchair.jpgを置き換える必要があり、chair.tifは置き換えません。 ただし、置き換え画像を、元の画像と別のフォルダーにアップロードできます。更新された画像は新しいフォルダーにあり、元の場所のファイルはなくなります.
**[!UICONTROL 任意のフォルダーでベース名が同じファイルを上書き]** - このオプションは最も包括的な置換規則です。置き換え画像を元の画像とは別のフォルダにアップロードしたり、ファイル拡張子が異なるファイルをアップロードしたり、元のファイルと置き換えたりできます。 元のファイルが別のフォルダーにある場合、置き換え画像は、アップロード先の新しいフォルダーに存在します。**[!UICONTROL 初期設定のカラープロファイル]** - 詳細については、[カラーマネジメントの設定](#configuring-color-management)を参照してください。デフォルトでは、アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択した場合 15 個のレンディションが表示され、「**[!UICONTROL ビューア]**」を選択した場合 15 個のビューアプリセットが表示されます。この制限は増やすことができます。[表示する画像プリセット数を増減する](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)または[表示するビューアプリセット数を増減する](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)を参照してください。

#### カラーマネジメントの設定 {#configuring-color-management}

Dynamic Mediaのカラーマネジメントを使用すると、正しいアセットをカラーマネジメントできます。 カラー補正により、取り込まれたアセットは、カラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、CMYK、RGB またはグレー出力を使用するターゲットのカラースペースに補正されます。[画像プリセットの設定](/help/assets/dynamic-media/managing-image-presets.md)を参照してください。

画像を要求する際にカラー補正を有効にするための初期設定のカラープロパティを設定するには：

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、プロビジョニング時に提供された資格情報を使用してアカウントにログインします。
1. **[!UICONTROL 設定／アプリケーション設定]**&#x200B;に移動します。
1. 「**[!UICONTROL 公開設定]**」領域を展開して、「**[!UICONTROL Image Server]**」を選択します。パブリッシュインスタンスのデフォルトを設定する際に、「**[!UICONTROL 公開コンテキスト]**」を「**[!UICONTROL 画像サービング]**」に設定します。
1. 変更する必要のあるプロパティまでスクロールします。例えば、**[!UICONTROL 「カラーマネジメント属性」]**領域のプロパティなどです。
次のカラー補正プロパティを設定できます。

   | プロパティ | 説明 |
   |---|---|
   | CMYK の初期設定カラースペース | 初期設定の CMYK カラープロファイルの名前。 |
   | Grayscale Default Color Space | 初期設定のグレーカラープロファイルの名前。 |
   | RGB の初期設定カラースペース | 初期設定の RGB カラープロファイルの名前。 |
   | カラー変換レンダリングインテント | レンダリングインテントを指定します。指定できる値は、**[!UICONTROL 知覚的]**、**[!UICONTROL 相対的な色域を維持]**、**[!UICONTROL 彩度]**、**[!UICONTROL 絶対的な色域を維持]**&#x200B;です。アドビでは、デフォルトとして&#x200B;**[!UICONTROL 相対]**&#x200B;をお勧めします。 |

1. 「**[!UICONTROL 保存]**」をタップします。

例えば、**[!UICONTROL RGB の初期設定カラースペース]**&#x200B;を *sRGB* に、**[!UICONTROL CMYK の初期設定カラースペース]**&#x200B;を *WebCoated* に設定できます。

それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルのないRGB画像は、*sRGB*&#x200B;カラースペースにあると見なされます。
* カラープロファイルのないCMYK画像は、*WebCoated*&#x200B;のカラースペースにあると見なされます。
* RGB出力を返すダイナミックレンディション、sRGB *カラースペースに返すレンディション。*
* CMYK出力を返すダイナミックレンディションを&#x200B;*WebCoated*&#x200B;のカラースペースに戻します。

#### サポートされる形式の MIME タイプの編集 {#editing-mime-types-for-supported-formats}

Dynamic Media によって処理されるアセットタイプを定義して、高度なアセット処理パラメーターをカスタマイズできます。例えば、アセット処理パラメーターを指定して次のことができます。

* Adobe PDF を eCatalog アセットに変換する。
* Adobe Photoshop ドキュメント（.PSD）をパーソナライズ用のバナーテンプレートアセットに変換する。
* Adobe Illustratorファイル(.AI)またはAdobe Photoshopカプセル化PostScript®ファイル(.EPS)をラスタライズします。
* [ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)および[イメージングプロファイル](/help/assets/dynamic-media/image-profiles.md)は、それぞれ、ビデオおよび画像の処理を定義するのに使用できます。

[アセットのアップロード](/help/assets/add-assets.md)を参照してください。

**サポートされる形式の MIME タイプを編集するには**

1. Cloud ServiceとしてのExperience Managerで、Experience ManagerをCloud Serviceのロゴとしてクリックしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL 一般/CRXDE Lite]**&#x200B;をクリックします。
1. 左側のパネルで、次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME タイプ](assets/mimetypes.png)

1. mimeTypesフォルダーで、MIMEタイプを選択します。
1. CRXDE Lite ページの右側の下部で、次の操作をおこないます。

   * 「**[!UICONTROL 有効]**」フィールドをダブルクリックします。デフォルトでは、すべてのアセットのMIMEタイプが有効（**[!UICONTROL true]**&#x200B;に設定）になります。これは、アセットがDynamic Mediaと同期されて処理されることを意味します。 このアセットのMIMEタイプを処理から除外する場合は、この設定を&#x200B;**[!UICONTROL false]**&#x200B;に変更します。

   * **[!UICONTROL jobParam]** をダブルクリックして、関連するテキストフィールドを開きます。特定のMIMEタイプで使用できる処理パラメーターの値のリストについては、[サポートされているMIMEタイプ](/help/assets/file-format-support.md)を参照してください。

1. 次のいずれかの操作をおこないます。
   * 手順3 ～ 4を繰り返して、さらにMIMEタイプを編集します。
   * CRXDE Lite ページのメニューバーで、「**[!UICONTROL すべて保存]**」をクリックします。

1. ページの左上隅にある&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;をタップすると、Cloud ServiceとしてExperience Managerに戻ります。

#### サポートされていない形式のカスタム MIME タイプの追加 {#adding-mime-types-for-unsupported-formats}

Experience Managerアセットで、サポートされていない形式のカスタムMIMEタイプを追加できます。 CRXDE Liteに追加した新しいノードがExperience Managerによって削除されないようにするには、MIMEタイプを`image_`の前に移動します。 また、有効な値が&#x200B;**[!UICONTROL false]**&#x200B;に設定されていることを確認します。

**サポートされていない形式のカスタム MIME タイプを追加するには**

1. Cloud ServiceとしてExperience Managerから、**[!UICONTROL ツール/操作/Webコンソール]**&#x200B;をタップします。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新しいブラウザータブが開き、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;ページが表示されます。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. ページ上で、*Adobe CQ Scene7 Asset MIME type Service* という名前まで下にスクロールします。次のスクリーンショットを参照してください。名前の右側にある&#x200B;**[!UICONTROL 設定値を編集]**（鉛筆アイコン）をタップします。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. **Adobe CQ Scene7 Asset MIME type Service** ページで、任意のプラス記号アイコン「+」をクリックします。表内でプラス記号をクリックして新しいMIMEタイプを追加する場所は簡単です。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 空のテキストフィールドに追加した `DWG=image/vnd.dwg` を入力します。

   例`DWG=image/vnd.dwg`は説明用です。 ここで追加する MIME タイプは、その他のサポートされていない形式でもかまいません。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. ページの右下隅にある「**[!UICONTROL 保存]**」をタップします。

   この時点で、Adobe Experience Manager Web コンソール設定ページが開いているブラウザータブを閉じることができます。

1. Cloud Serviceコンソールとして開いているExperience Managerを持つブラウザタブに戻ります。
1. Cloud ServiceとしてExperience Managerから、**[!UICONTROL ツール/一般/CRXDE Lite]**&#x200B;をタップします。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 左側のパネルで、次の場所に移動します。

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. MIMEタイプ`image_vnd.dwg`をドラッグし、次のスクリーンショットに示すように、ツリーの`image_`のすぐ上にドロップします。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. MIMEタイプ`image_vnd.dwg`が選択された状態で、**[!UICONTROL 「プロパティ]**」タブの&#x200B;**[!UICONTROL enabled]**&#x200B;行の&#x200B;**[!UICONTROL 値]**&#x200B;列ヘッダーの下の値を重複クリックします。 **[!UICONTROL 値]**&#x200B;ドロップダウンリストが開きます。
1. フィールドに `false` と入力します（または、ドロップダウンリストから「**[!UICONTROL false]**」を選択します）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」をクリックします。



### （オプション）Dynamic Media のパフォーマンスの調整 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> のスムーズな実行を維持するために、アドビでは、次の同期パフォーマンス／拡張性の微調整のヒントをお勧めします。

* 様々なファイル形式の処理に対応する定義済みのジョブパラメーターを更新する。
* 事前定義済みの Granite のワークフロー（ビデオアセット）キューワーカースレッドを更新する。
* Granite の事前定義済みの一時的なワークフロー（画像および非ビデオアセット）キューワーカースレッドを更新する。
* Dynamic Media Classic サーバーへの最大アップロード接続数を更新する。

#### 様々なファイル形式の処理に対応する定義済みのジョブパラメーターを更新する

ジョブパラメータを調整して、ファイルアップロード時の処理を高速化できます。例えば、PSDファイルをアップロードし、テンプレートとして処理したくない場合に、レイヤーの抽出をfalse（オフ）に設定できます。 この場合、調整されたジョブパラメーターは次のように表示されます。`process=None&createTemplate=false`.

テンプレートの作成を有効にする場合は、次のパラメーターを使用します。`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobeでは、PDF、PostScript®およびPSDファイルに対して、次の「調整済み」ジョブパラメーターを使用することをお勧めします。

| ファイルタイプ | 推奨されるジョブパラメーター |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

これらのパラメーターを更新するには、[サポートされる形式のMIMEタイプの編集](#editing-mime-types-for-supported-formats)を参照してください。

[サポートされていない形式に対するMIMEタイプの追加](#adding-mime-types-for-unsupported-formats)も参照してください。

#### Granite の一時的なワークフローキューの更新 {#updating-the-granite-transient-workflow-queue}

Granite の一時的なワークフローキューは、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローに使用されます。Dynamic Media では、画像の取り込みおよび処理に使用されます。

**Granite の一時的なワークフローキューを更新するには：**

1. [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) に移動して、**Queue: Granite Transient Workflow Queue** を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   **[!UICONTROL 並列ジョブの最大数]**&#x200B;を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェア容量によって異なります。 初回移行や1回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。 ただし、大きな値（コア数の2倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。 そのため、特定の使用事例に基づいて値をテストし、調整します。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

#### Granite のワークフローキューの更新 {#updating-the-granite-workflow-queue}

Granite のワークフローキューは、一時的でないワークフローに使用されます。Dynamic Mediaでは、**[!UICONTROL Dynamic Mediaエンコードビデオ]**&#x200B;のワークフローでビデオを処理するのに使用しました。

Granite のワークフローキューを更新するには：:

1. `https://<server>/system/console/configMgr` に移動して、**Queue: Granite Workflow Queue** を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   デフォルトでは、並列ジョブの最大数は、使用可能な CPU コア数によって異なります。例えば、4コアサーバーでは、2つのワーカースレッドが割り当てられます。 （0.0 ～ 1.0の値は比率ベース、または1より大きい任意の数値によって、ワーカースレッドの数が割り当てられます）。

   ほとんどの事例では、デフォルト設定の 0.5 で十分です。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

#### Scene7 アップロード接続の更新 {#updating-the-scene-upload-connection}

「Scene7アップロード接続」設定により、Experience ManagerアセットがDynamic Mediaクラシックサーバーに同期されます。

Scene7 アップロード接続を更新するには：:

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl` に移動します。
1. 「**[!UICONTROL 接続数]**」フィールド、または「**[!UICONTROL アクティブなジョブタイムアウト]**」フィールド、またはその両方で、必要に応じて数を変更します。

   「**[!UICONTROL 接続数]**」設定は、Dynamic MediaへのアップロードにExperience ManagerできるHTTP接続の最大数を制御します。 通常、10個の接続の定義済み値で十分です。

   「**[!UICONTROL Active job timeout]**」設定は、アップロードされた Dynamic Media アセットが配信サーバーで公開されるまでの待機時間を決定します。デフォルトでは、この値は 2100 秒または 35 分です。

   ほとんどの事例では、2100 の設定で十分です。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

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

1. In Experience Manager as a Cloud Service, tap the Experience Manager as a Cloud Service logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
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
