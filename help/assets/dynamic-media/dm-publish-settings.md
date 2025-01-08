---
title: Image Server 用の Dynamic Media の公開設定
description: Image Server 用のDynamic Media公開設定を設定する方法、特にカラーマネジメント、セキュリティ、サムネール画像を設定する方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: b0891095-e4a9-4dd5-8dfd-a576bc47d082
source-git-commit: 73a1f8fcfb38e433392a15730d239bb2b7062f75
workflow-type: tm+mt
source-wordcount: '3356'
ht-degree: 76%

---

# Image Server 用の Dynamic Media の公開設定

<!-- hide: yes
hidefromtoc: yes -->

{{work-with-dynamic-media}}

Dynamic Media Publishの設定オプションは、次の場合にのみ使用できます。

* Adobe Experience Manager as a Cloud Service に&#x200B;*既存*&#x200B;の **[!UICONTROL Dynamic Media 設定]**（**[!UICONTROL Cloud Services]** 内）がある。[Cloud Services での Dynamic Media 設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)を参照してください。
* 自身が管理者権限を持つ Experience Manager システム管理者である。

経験豊富な web サイト開発者およびプログラマーがDynamic Media Publish設定を使用します。 AdobeDynamic Mediaでは、AdobeDynamic Media、HTTP プロトコルの標準と規則、基本的な画像技術に精通しているユーザーが、公開設定を変更することをお勧めします。

Dynamic Media の公開設定ページでは、Adobe Dynamic Media サーバーから web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。設定が指定されていない場合、Adobe Dynamic Media サーバーは、Dynamic Media 公開設定ページで設定されたデフォルト設定に従ってアセットを配信します。

その他のオプションの設定タスクについては、[オプション - Dynamic Media 設定のセットアップと設定](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)も参照してください。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service 上で Dynamic Media Classic から Dynamic Media にアップグレードしますか？Dynamic Media の[一般設定](/help/assets/dynamic-media/dm-general-settings.md)ページと公開設定ページには、Dynamic Media Classic アカウントから取得した値が事前に入力されています。ただし、一般設定ページの&#x200B;**[!UICONTROL デフォルトアップロードオプション]**&#x200B;領域に表示されるすべての値は例外です。これらの値はすでに Experience Manager に存在します。そのため、**[!UICONTROL デフォルトのアップロードオプション]**&#x200B;で行った変更は、5 つのタブのいずれかで、Experience Manager ユーザーインターフェイスを介して Dynamic Media に反映されます（Dynamic Media Classic ではありません）。[一般設定](/help/assets/dynamic-media/dm-general-settings.md)ページと公開設定ページのその他の設定と値は、Experience Manager の Dynamic Media Classic と Dynamic Media の間で維持されます。

**Dynamic Media 公開設定の Image Server を設定するには：**

1. Experience Manager 作成者モードで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 左側のパネルで「ツール」アイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL Dynamic Media 公開設定]**&#x200B;に移動します。
1. Image Server ページのドロップダウンリストで公開コンテキストを選択して、Image Server から画像を配信するためのデフォルト設定を確立します。

| Publish コンテキスト | 説明 |
| --- | --- |
| 画像サービング | 公開設定のコンテキストを指定します。 |
| テスト画像サービング | 公開設定をテストするコンテキストを指定します。<br>新しい Dynamic Media アカウントの場合のみ、**[!UICONTROL クライアントアドレス]**&#x200B;フィールドがデフォルトで自動的に `127.0.0.1` に設定されます。<br>[アセットを公開する前にテストする](#test-assets-before-making-public)を参照してください。 |

1. 5 つのタブを使用して、デフォルトの公開コンテキスト設定を指定します。

   * [「Security」タブ](#security-tab)
   * 「[カタログ管理](#catalog-management-tab)」タブ
   * 「[リクエスト属性](#request-attributes-tab) 」タブ
   * 「[共通のサムネール属性](#common-thumbnail-attributes-tab) 」タブ
   * 「[カラーマネジメント属性](#color-management-attributes-tab) 」タブ

   ![Dynamic Media 公開設定ページ](/help/assets/assets-dm/dm-publish-setup.png)
   *「**[!UICONTROL リクエスト属性]**」タブが選択されている Dynamic Media 公開設定ページ*<br><br>

1. 作業が完了したら、ページの右上隅のほうにある「**[!UICONTROL 保存]**」を選択します。

## 「Security」タブ {#security-tab}

>[!NOTE]
>
>*画像サービング* 公開コンテキストのセキュリティ設定はサポートされていません。

*画像サービングをテスト* が公開コンテキストとして設定されている場合、次のセキュリティ設定を指定できます。

**[!UICONTROL クライアントアドレス]** - 1 つ以上の IP アドレスまたは IP アドレスの範囲を指定できます。指定した場合、登録されていない IP アドレスのクライアントからは、この画像カタログへの要求が拒否されます。このルールは、画像の配信とレンダリングされた画像の両方に適用されます。

![ 「セキュリティ」タブ ](/help/assets/assets-dm/dm-ipallowlist.png)<br>*IP 「許可」フィールドを表示する「セキュリティ」タブ*


## 「カタログ管理」タブ {#catalog-management-tab}

**[!UICONTROL ルールセット定義ファイルのパス]** - 画像カタログのルールセット定義を含むファイルを指定します。

Dynamic Media ビューアリファレンスガイドの [RuleSetFile](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile) パラメーターも参照してください。

>[!NOTE]
>
>Dynamic Media Classic アカウントで既に **[!UICONTROL ルールセット定義ファイルパス]** が選択されている場合は、**[!UICONTROL カタログ管理]** グループの **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション]** > **[!UICONTROL Publish設定]** で設定されます。 Experience ManagerのDynamic Media アカウントで、この選択が認識されます。 その後、Dynamic Media Classicからファイルを取得します。 初めて **[!UICONTROL Dynamic Media 公開設定]**&#x200B;ページを開いたときに、ファイルが保存され、このフィールドで使用できるようになります。

## 要求属性タブ {#request-attributes-tab}

これらの設定は、画像のデフォルトの表示に関係します。

| 設定 | 説明 |
| --- | --- |
| **[!UICONTROL 返信画像のサイズ制限]** | 必須。<br> 新しいDynamic Media アカウントの場合のみ、デフォルトのサイズ制限は、**[!UICONTROL 画像サービング]** と **[!UICONTROL テスト画像サービング]** の両方で、幅：`3000` と高さ：`3000` に自動的に設定されます。<br>クライアントに返される返信画像の最大の幅と高さを指定します。要求によって返信画像の幅、高さ、またはその両方がこの設定よりも大きくなる場合、サーバーはエラーを返します。<br>Dynamic Media ビューアリファレンスガイドの [MaxPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix) パラメーターも参照してください。 |
| **[!UICONTROL リクエスト暗号化モード]** | 有効な要求に base64 エンコーディングを適用する場合は、有効にします。<br>Dynamic Media ビューアリファレンスガイドの [RequestObfuscation](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation) パラメーターも参照してください。 |
| **[!UICONTROL リクエストロックモード]** | 要求に単純なハッシュロックを含める場合は、有効にします。<br>Dynamic Media ビューアリファレンスガイドの [RequestLock](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのリクエスト属性]** | |
| **[!UICONTROL デフォルトの画像ファイルサフィックス]** | 必須。<br>パスにファイルのサフィックスが含まれていない場合に、カタログの「パス」フィールドと「MaskPath」フィールドの値に追加するデフォルトのデータファイル拡張子です。<br>Dynamic Media ビューアリファレンスガイドの [DefaultExt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのフォント書体名]** | テキストレイヤー要求でフォントが提供されない場合に使用するフォントを指定します。指定する場合は、この画像カタログのフォントマップまたはデフォルトのカタログのフォントマップで有効なフォント名を指定する必要があります。<br>Dynamic Media ビューアリファレンスガイドの [DefaultFont](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont) パラメーターも参照してください。 |
| **[!UICONTROL デフォルト画像]** | デフォルトの画像は、リクエストされた画像が見つからない場合、リクエストに応答してを返します。<br>Dynamic Media ビューアリファレンスガイドの [DefaultImage](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage) パラメーターも参照してください。<br>**注意**:Dynamic Media Classic アカウントの **[!UICONTROL デフォルトのリクエスト属性**[!UICONTROL  グループの ]**設定]**/**[!UICONTROL アプリケーション]**/**[!UICONTROL Publish設定]** で選択された **[!UICONTROL デフォルトの画像]** がある場合、Experience Managerは画像を取得します。 その後、ファイルは保存され、**[!UICONTROL Dynamic Media 公開設定]**&#x200B;ページを初めて開いたときにこのフィールドで使用できるようになります。 |
| **[!UICONTROL デフォルトの画像モード]** | スライダーボックスが有効な場合（右側のスライダー）、**[!UICONTROL デフォルトの画像]**&#x200B;はソースの画像の欠落している各レイヤーをデフォルトの画像に置き換え、通常どおり合成を返します。スライダーボックスが無効な場合（左側のスライダー）、欠落している画像がいくつかのレイヤーの 1 つにすぎない場合でも、デフォルトの画像が合成画像全体に置き換わります。<br>Dynamic Media ビューアリファレンスガイドの [DefaultImageMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトの表示サイズ]** | 必須。<br> 新しいDynamic Media アカウントの場合のみ、デフォルトのサイズ制限は、**[!UICONTROL 画像サービング]** と **[!UICONTROL テスト画像サービング]** の両方で、幅：`1280` と高さ：`1280` に自動的に設定されます。<br>リクエストで `wid=`、`hei=`、`scl=` のいずれかを使用して表示サイズを明示的に指定していない場合、サーバーによって、返信画像がこの幅と高さを超えないように制限されます。<br>Dynamic Media ビューアリファレンスガイドの [DefaultPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのサムネールサイズ]** | 必須。<br>サムネールリクエスト（`req=tmb`）の属性である&#x200B;**[!UICONTROL デフォルトの表示サイズ]**&#x200B;の代わりに使用されます。サムネールリクエスト（`req=tmb`）で `wid=`、`hei=`、または `scl=` を使用してサイズが明示的に指定されていない場合、サーバーによって、返信画像がこの幅と高さを超えないように制限されます。<br>Dynamic Media ビューアリファレンスガイドの [DefaultThumbPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトの背景色]** | 返信画像内で実際の画像データが含まれない領域を埋めるために使用する RGB 値を指定します。<br>Dynamic Media ビューアリファレンスガイドの [BkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor) パラメーターも参照。 |
| **[!UICONTROL JPEG エンコード属性]** |  |
| **[!UICONTROL 品質]** | <br>JPEG 返信画像のデフォルト属性を指定します。<br> 新しいDynamic Media アカウントの場合のみ、**[!UICONTROL 画像サービング]** と **[!UICONTROL テスト画像サービング**[!UICONTROL  の両方で ]**画質]** のデフォルト値が自動的に `80` に設定されます。<br>このフィールドは 1 ～ 100 の範囲で定義されます。<br>Dynamic Media ビューアリファレンスガイドの [JpegQuality](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality) パラメーターも参照してください。 |
| **[!UICONTROL 色度のダウンサンプリング]** | JPEGエンコーダが使用する色度のダウンサンプリングを有効または無効にします。 |
| **[!UICONTROL デフォルトの再サンプリングモード]** | 画像データの拡大縮小に使用するデフォルトの再サンプリングおよび補間属性を指定します。`resMode` がリクエスト内で指定されていない場合に使用します。<br> 新しいDynamic Media アカウントの場合のみ、**[!UICONTROL 画像サービング]** と **[!UICONTROL テスト画像サービング]** の両方で、デフォルトの再サンプリングモードが自動的に `Sharp2` に設定されます。<br>Dynamic Media ビューアリファレンスガイドの [ResMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode) パラメーターも参照してください。 |

## 共通のサムネール属性タブ {#common-thumbnail-attributes-tab}

これらの設定は、サムネール画像のデフォルトの外観と配置に関係します。

| 設定 | 説明 |
| --- | --- |
| **[!UICONTROL サムネールのデフォルトの背景色]** | 出力サムネール画像内で実際の画像データが含まれない領域を埋めるために使用する RGB 値を指定します。サムネールリクエスト（`req=tmb`）にのみ使用され、**[!UICONTROL デフォルトのサムネールの種類]**&#x200B;設定が「**[!UICONTROL フィット]**」または「**[!UICONTROL テクスチャ]**」に設定されている場合に使用されます。<br>Dynamic Media ビューアリファレンスガイドの [ThumbBkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor) パラメーターも参照してください。 |
| **[!UICONTROL 水平方向揃え]** | `wid=` および `hei=` の値で指定された返信画像の長方形におけるサムネール画像の水平方向揃えを指定します。<br>サムネールリクエスト（`req=tmb`）にのみ使用され、**[!UICONTROL デフォルトのサムネールの種類]**&#x200B;設定が「**[!UICONTROL フィット]**」に設定されている場合に使用されます。<br>水平方向揃えは、**[!UICONTROL 中央揃え]**、**[!UICONTROL 左揃え]**、**[!UICONTROL 右揃え]**&#x200B;の 3 つから選択できます。<br>Dynamic Media ビューアリファレンスガイドの [ThumbHorizAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign) パラメーターも参照してください。 |
| **[!UICONTROL 垂直方向揃え]** | `wid=` および `hei=` の値で指定された返信画像の長方形内のサムネール画像の垂直方向揃えを指定します。サムネールリクエスト（`req=tmb`）にのみ使用され、**[!UICONTROL デフォルトのサムネールの種類]**&#x200B;設定が「**[!UICONTROL フィット]**」に設定されている場合に使用されます。<br>垂直方向揃えは、**[!UICONTROL 上揃え]**、**[!UICONTROL 中央揃え]**、**[!UICONTROL 下揃え]**&#x200B;の 3 つから選択できます。<br>Dynamic Media ビューアリファレンスガイドの [ThumbVertAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのクライアントキャッシュの有効期限]** | 特定のカタログレコードに有効なカタログ有効期限の値が含まれていない場合は、デフォルトの有効期限間隔（時間単位）が指定されます。 `-1` に設定すると、有効期限切れになりません。<br>Dynamic Media ビューアリファレンスガイドの [Expiration](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのサムネールの種類]** | 特定のカタログレコードに有効なカタログの ThumbType の値が含まれていない場合に使用する、サムネールの種類のデフォルトが指定されています。 サムネイルリクエスト（`req=tmb`）にのみ使用されます。<br>サムネールの種類は、**[!UICONTROL 切り抜き]**、「**[!UICONTROL フィット]**」、「**[!UICONTROL テクスチャ]**」の 3 つから選択できます。<br>Dynamic Media ビューアリファレンスガイドの [ThumbType](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype) パラメーターも参照してください。 |
| **[!UICONTROL デフォルトのサムネール解像度]** | 特定のカタログレコードに有効なカタログの ThumbRes の値が含まれていない場合に使用する、サムネールオブジェクト解像度のデフォルトが指定されます。 サムネールリクエスト（`req=tmb`）にのみ使用され、**[!UICONTROL デフォルトのサムネールの種類]**&#x200B;設定が「**[!UICONTROL テクスチャ]**」に設定されている場合に使用されます。<br>Dynamic Media ビューアリファレンスガイドの [ThumbRes](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres) パラメーターも参照してください。 |

## 「カラーマネジメント属性」タブ {#color-management-attributes-tab}

これらの設定は、画像に使用する ICC カラープロファイルを決定します。

**カラー変換レンダリングインテント**
カラー変換レンダリングインテントを使用すると、作業プロファイルのデフォルトのレンダリングインテントを上書きして、ソースカラーの調整方法を決定できます。次の場合に使用されます。

1. デフォルトの ICC プロファイルの 1 つは、カラー変換のターゲットカラースペースです。
1. このプロファイルは、プリンターやモニターなどの出力デバイスを特徴付けます。
1. また、指定したレンダリングインテントはこのプロファイルに対して有効です。

レンダリングインテントが異なると、ソースカラーの調整方法を決定するために異なるルールが使用されます。

Dynamic Media ビューアリファレンスガイドの [IccRenderIntent](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent) パラメーターも参照してください。

>[!NOTE]
>
>一般に、選択したカラー設定には、業界標準に準拠するためにAdobeがテストしたデフォルトのレンダリングインテントを使用します。 例えば、北米またはヨーロッパのカラー設定を選択した場合、デフォルトのカラー変換レンダリングインテントは、**[!UICONTROL 相対的な色域を維持]**&#x200B;です。日本のカラー設定を選択した場合、デフォルトのカラー変換レンダリングインテントは、**[!UICONTROL 知覚的]**&#x200B;です。

| 設定 | 特徴 |
| --- | --- |
| **[!UICONTROL CMYK のデフォルトカラースペース]** | CMYK データの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。**[!UICONTROL 指定なし]**&#x200B;が選択されている場合、CMYK ソース画像が関係しているときは、この画像カタログのカラーマネジメントが無効になります。すべての CMYK 作業用スペースはデバイスに依存します。つまり、実際のインクと紙の組み合わせに基づいています。アドビが提供する CMYK 作業用スペースは、標準的な商業印刷条件に基づいています。<br> Dynamic Media ビューアリファレンスガイドの [IccProfileCMYK](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk) パラメーターも参照してください。 |
| **[!UICONTROL グレースケールのデフォルトカラースペース]** | グレースケールデータの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。「**[!UICONTROL 指定なし]**」が選択されている場合、グレースケールのソース画像が関係しているときは、この画像カタログのカラーマネジメントが無効になります。<br>Dynamic Media ビューアリファレンスガイドの [IccProfileGray](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray) パラメーターも参照してください。 |
| **[!UICONTROL RGB のデフォルトカラースペース]** | RGB データの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。**[!UICONTROL 指定なし]**&#x200B;が選択されている場合、RGBソース画像が関係しているときは、この画像カタログのカラーマネジメントが無効になります。一般に、特定のデバイスのプロファイル（モニタープロファイルなど）ではなく、**[!UICONTROL Adobe RGB]** または **[!UICONTROL sRGB]** を選択するのが最適です。**[!UICONTROL sRGB]** は、web またはモバイルデバイス用の画像を準備する際に推奨されます。これは、web 上の画像の表示に使用される標準モニターのカラースペースを定義するからです。**[!UICONTROL sRGB]** は、消費者レベルのデジタルカメラからの画像を操作する場合にも適しています。これらのカメラのほとんどは、デフォルトのカラースペースとして sRGB を使用しているためです。<br>Dynamic Media ビューアリファレンスガイドの [IccProfileRBG](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb) パラメーターも参照してください。 |
| **[!UICONTROL カラー変換レンダリングの方法]** | **[!UICONTROL 知覚的]** - カラーの値自体が変化する場合でも、人間の目に自然と感じられるように、カラー間の視覚的な関係を保つことを目的としています。このインテントは、色域外の色が多い写真画像に適しています。この設定は、日本の印刷業界にとっての標準的なレンダリングインテントです。 |
|  | **[!UICONTROL 相対的な色域を維持]** - ソースカラースペースの極端なハイライトを目的のカラースペースのハイライトと比較し、それに応じてすべての色をシフトします。色域外の色は、出力先のカラースペースで最も近く再現可能な色にシフトします。「相対的な色域を維持」では、「知覚的」よりも多くの元の色が画像に保持されます。この設定は、北米およびヨーロッパでの印刷の標準的なレンダリングインテントです。 |
|  | **[!UICONTROL 彩度]** - 画像内で色の精度を犠牲にして鮮やかな色を生成しようとします。このレンダリングインテントは、グラフやチャートなどのビジネスグラフィックに適しています。色間の正確な関係よりも明るい彩度の色が重要です。 |
|  | **[!UICONTROL 絶対的な色域を維持]** - 対象の色域内に含まれる色は変更されません。色域外の色は切り取られます。目的の白点に対する色の拡大・縮小は行われません。このインテントは、色間の関係を保つことを犠牲にして色の精度を維持することを目的とし、特定のデバイスの出力をシミュレートするための校正に適しています。このインテントは、用紙の色が印刷色に与える影響をプレビューする場合に便利です。 |

## アセットを公開する前にテストする {#test-assets-before-making-public}

セキュアテストを使用すると、設定可能な一連の IP アドレスと範囲に基づいて、セキュアテスト環境を定義して堅牢な B2B ソリューションを作成できます。この機能を使用すると、Adobe Dynamic Media の導入と、コンテンツ管理およびビジネスシステムのアーキテクチャを一致させることができます。

セキュアテストを使用すると、非公開のコンテンツを含む web サイトのステージングバージョンをプレビューできます。

必要に応じて、以下の理由でアセットを公開する代わりに、ステージング環境を作成します。

* 公開前に web サイトをプレビューする（ステージング用 web サイト）。
* B2B web アプリケーションで価格を表示する eCatalog など、制限付きアクセスを必要とするアセットを提供する。
* 製品情報管理システム、顧客サービスアプリケーション、トレーニングサイトなどの一部として、ファイアウォールの内側にあるアセットを使用する。

>[!NOTE]
>
>セキュアテストは、Adobe Dynamic Media Classic へのアクセスに影響しません。Adobe Dynamic Media Classic のセキュリティは一貫しており、Adobe Dynamic Media Classic および関連する web サービスにアクセスするための通常の資格情報が必要です。

### セキュアテストの仕組み {#how-test-assets-works}

ほとんどの企業は、ファイアウォールの内側でインターネットを実行します。インターネットへのアクセスは、特定のルートを通じて可能で、通常は限られた範囲のパブリック IP アドレスを通じて可能です。

企業ネットワークから、 [https://www.whatismyip.com](https://www.whatismyip.com/)などの web サイトを使用してパブリック IP アドレスを把握するか、企業の IT 組織にこの情報をリクエストします。

セキュアテストを使用すると、Adobe Dynamic Media は、ステージング環境または内部アプリケーション用に専用の Image Server を確立します。このサーバーへのリクエストはすべて、発信元 IP アドレスをチェックします。受信リクエストが IP アドレスの承認済みリストに含まれていない場合は、失敗のレスポンスが返されます。
Adobe Dynamic Media の会社管理者が、自社のセキュアテスト環境で使用する承認済み IP アドレスリストを設定します。

元のリクエストの場所を確認する必要があるので、セキュアテストサービスのトラフィックは、パブリック Dynamic Media Image Server トラフィックのようにコンテンツ配布ネットワークを通じてルーティングされません。セキュアテストサービスへのリクエストの待ち時間は、パブリックな Dynamic Media Image Server に比べて若干長くなります。

非公開のアセットは、セキュアテストサービスから直ちに使用できます。公開する必要はありません。この方法では、公開されている Image Server にアセットを公開する前にプレビューを実行できます。

>[!NOTE]
>
>セキュアテストサービスは、内部公開コンテキストで設定されたカタログサーバーを使用します。したがって、セキュアテストに公開するように会社が設定されている場合、Adobe Dynamic Media にアップロードされたアセットは、セキュアテストサービスですぐに使用できるようになります。この機能は、アセットがアップロード時に公開用にマークされているかどうかに関係なく当てはまります。

セキュアテストサービスは、現在、次のアセットのタイプと機能をサポートしています。

* 画像.
* ビネット（Render Server リクエスト）。
* ユーザーは、Render Server のサポートを明示的にリクエストする必要があります（を使用できます）。
* 画像セット、eCatalog、レンダリングセット、メディアセットを含む複数のセット。
* 標準の Adobe Dynamic Media リッチメディアビューア。
* Adobe Dynamic Media OnDemand JSP ページ。
* 静的コンテンツ（PDF ファイルやプログレッシブに提供するビデオなど）。
* HTTP ビデオストリーミング。
* プログレッシブビデオストリーミング。

次のアセットタイプと機能は、現在、サポートされていません。

* Adobe Dynamic Media Classic Info または eCatalog 検索
* RTMP ビデオストリーミング
* Web-to-print
* UGC（ユーザー生成コンテンツ）サービス

  >[!IMPORTANT]
  >
  >2023年5月1日（PT）以降、Dynamic Media の UGC アセットは、アップロード日から最大 60 日間使用できます。60 日後にアセットは削除されます。

  >[!NOTE]
  >
  >Adobe Dynamic Media での新規または既存の UGC ベクター画像アセットのサポートは、2021年9月30日（PT）に終了しました。

### セキュアテストサービスのテスト {#test-secure-testing-service}

セキュアテストサービスが期待どおりに動作することを確認するには、次の手順を実行します。

#### アカウントの準備

1. アドビカスタマーケアに問い合わせ、お使いのアカウントでセキュアテストを有効にするようリクエストしてください。
1. Adobe Experience Manager で、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL Dynamic Media 公開設定]**&#x200B;を選択します。
1. Image Server ページの「**[!UICONTROL 公開コンテキスト]**」ドロップダウンリストで、「**[!UICONTROL 画像サービングをテスト]**」を選択します。
1. **[!UICONTROL セキュリティ]**&#x200B;タブを選択します。
1. **[!UICONTROL クライアントアドレス]**&#x200B;フィルターで、「**[!UICONTROL 追加]**」を選択します。
1. 「**[!UICONTROL IP アドレス]**」フィールドに、IP アドレスを入力します。
1. 「**[!UICONTROL マスク]**」フィールドに、ネットマスクを入力します。

   >[!NOTE]
   >
   >複数の IP アドレスとネットマスクを追加すると、実質的に&#x200B;*すべての* IP アドレスにアセット呼び出しを行うことが許可され、それらがすべて表示されます。

1. 次のいずれかの操作を行います。

   * さらに IP アドレスを追加するには、前の 3 つの手順を繰り返します。
   * 次の手順に進みます。

1. Image Server ページの右上隅で、「**[!UICONTROL 保存]**」を選択します。
1. 目的の画像を Adobe Dynamic Media アカウントにアップロードします。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 一部の画像が公開用にマークされており、他の画像がマークされていないことを確認し、公開ジョブを送信します。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL Dynamic Media の一般設定]**&#x200B;に移動して、セキュアテストサービスの名前を決定します。
1. **[!UICONTROL サーバー]**&#x200B;ページで、**[!UICONTROL 公開サーバー名]**&#x200B;の右側にあるサーバー名を見つけます。

サーバー名が見つからないかサーバーへの URL が機能しない場合は、アドビケアに問い合わせてください。

#### Web サイトのバリエーションの準備

公開済みアセットと非公開アセットをリンクする、2 つのバリエーションの web サイトが必要です。

* 公開バージョン - 従来の Adobe Dynamic Media URL 構文を使用してアセットをリンクします。
* ステージングバージョン - 同じ構文でアセットをリンクしますが、セキュアテストサイト名を使用します。

#### テストの実行

次のテストを実行します。

1. 企業ネットワーク内からアセットが表示されているかどうかを確認します。

   事前に定義した IP アドレス範囲によって識別される企業ネットワーク内からであれば、ステージングバージョンの web サイトは、公開用にマークされているかどうかにかかわらずすべての画像を表示します。そのため、プレビューの承認や製品の発売前に、誤って画像を公開することなくテストできます。

   Adobe Dynamic Media で以前に確認したように、公開バージョンのサイトに公開済みアセットが表示されていることを確認します。

1. 企業ネットワークの外部から、非公開のアセット（つまり、公開のマークが付いていないアセット）がサードパーティのアクセスから保護されていることを確認します。

   外部（自宅のコンピューターや 4G／5G 接続など）からネットワークにアクセスし、公開バージョンのサイトに公開済みのアセットがすべて表示され、非公開のコンテンツは表示されないことを確認します。

   ステージングバージョンでは、未承認の IP アドレスからセキュアテストサービスにアクセスしているので、アセットはどれも表示されないことを確認します。
