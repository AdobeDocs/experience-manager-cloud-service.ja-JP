---
title: Image Server 用のDynamic Media公開設定の指定
description: Dynamic Mediaで公開を設定する方法を説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: b0891095-e4a9-4dd5-8dfd-a576bc47d082
source-git-commit: 446edfd83affb062585dca81052575b73c2e796f
workflow-type: tm+mt
source-wordcount: '3448'
ht-degree: 5%

---

# Image Server 用のDynamic Media公開設定の指定

<!-- hide: yes
hidefromtoc: yes -->

Dynamic Media公開設定の指定は、次の場合にのみ使用できます。

* 次のアカウントがある *既存* **[!UICONTROL Dynamic Media Configuration]** ( **[!UICONTROL Cloud Services]**) をAdobe Experience Manager as a Cloud Serviceでクリックします。 詳しくは、 [Cloud ServicesでのDynamic Media設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* 管理者権限を持つExperience Manager・システム管理者です。

Dynamic Media公開設定は、経験豊富な Web サイト開発者およびプログラマーが使用することを目的としています。 AdobeDynamic Mediaでは、これらの公開設定を変更するユーザーに、AdobeDynamic Media、HTTP プロトコルの標準と規則、基本的な画像技術に精通していることをお勧めします。

Dynamic Mediaの公開設定ページでは、AdobeDynamic Mediaサーバーから Web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。 設定が指定されていない場合、AdobeDynamic Mediaサーバーは、Dynamic Media公開設定ページで設定されたデフォルト設定に従ってアセットを配信します。

関連トピック [オプション — Dynamic Media設定のセットアップと設定](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) を参照してください。

>[!NOTE]
>
>Dynamic Media ClassicからAdobe Experience Manager as a Cloud Service上のDynamic Mediaにアップグレードする場合 この [一般設定](/help/assets/dynamic-media/dm-general-settings.md) ページおよび公開設定ページが、Dynamic Mediaアカウントから取得した値で事前設定されています。 例外は、 **[!UICONTROL デフォルトのアップロードオプション]** 」領域に表示されます。 これらの値は既にExperience Manager中です。 したがって、以下で行う変更 **[!UICONTROL デフォルトのアップロードオプション]**&#x200B;では、5 つのタブのいずれかにまたがって、Experience Managerユーザーインターフェイスを介して、Dynamic Media ClassicではなくDynamic Mediaに反映されます。 その他の設定と値は、 [一般設定](/help/assets/dynamic-media/dm-general-settings.md) ページと公開設定ページは、Experience Manager時にDynamic Media ClassicとDynamic Mediaの間で維持されます。

**Dynamic Media Publish Setup Image Server を設定するには：**

1. Experience Manager作成モードで、Experience Managerロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 左側のレールでツールアイコンを選択し、に移動します。 **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. Image Server ページで、Image Server — 公開コンテキストを設定し、5 つのタブを使用してデフォルトの公開設定を指定します。

   * [画像サーバー](#image-server)
      * [「Security」タブ](#security-tab)
      * [カタログ管理](#catalog-management-tab) タブ
      * [要求属性](#request-attributes-tab) タブ
      * [共通のサムネール属性](#common-thumbnail-attributes-tab) タブ
      * [カラーマネジメント属性](#color-management-attributes-tab) タブ

   ![Dynamic Media Publish Setup ページ](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media公開設定ページ、**[!UICONTROL 要求属性]**」タブが選択されています。*<br><br>

1. 作業が完了したら、ページの右上隅付近にある「 」を選択します。 **[!UICONTROL 保存]**.

## 画像サーバー {#image-server}

Image Server ページでは、Image Server から画像を配信するためのデフォルト設定を指定します。 設定は 5 つのカテゴリで使用できます

| 公開コンテキスト | 説明 |
| --- | --- |
| 画像サービング | パブリッシュ設定のコンテキストを指定します。 |
| テスト画像サービング | 公開設定をテストするコンテキストを指定します。<br>新しいDynamic Mediaアカウントのみの場合、デフォルト **[!UICONTROL クライアントアドレス]** フィールドが `127.0.0.1` 自動的に。<br>詳しくは、 [アセットを公開する前にテストする](#test-assets-before-making-public). |

### 「Security」タブ {#security-tab}

**[!UICONTROL クライアントアドレス]** - 1 つ以上の IP アドレスまたは IP アドレスの範囲を指定できます。 指定した場合、登録されていない IP アドレスのクライアントからのこの画像カタログへの要求は拒否されます。 このルールは、画像とレンダリングされた画像の両方の配信に適用されます。

### 「カタログ管理」タブ {#catalog-management-tab}

**[!UICONTROL ルールセット定義ファイルのパス]**  — 画像カタログのルールセット定義を含むファイルを指定します。

関連トピック [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。

>[!NOTE]
>
>Dynamic Media Classicアカウントに既に **[!UICONTROL ルールセット定義ファイルのパス]** 選択済み（以下に設定済み） **[!UICONTROL 設定]** > **[!UICONTROL アプリ]** > **[!UICONTROL 公開設定]**&#x200B;の下 **[!UICONTROL カタログ管理]** グループ )、Experience ManagerのDynamic MediaアカウントがDynamic Media Classicからファイルを取得します。 その後、ファイルが保存され、このフィールドで使用可能になります ( を開く際に **[!UICONTROL Dynamic Media Publish Setup]** ページを初めて表示します。

### 「要求属性」タブ {#request-attributes-tab}

これらの設定は、画像のデフォルトの表示に関係します。

| 設定 | 説明 |
| --- | --- |
| **[!UICONTROL 返信画像のサイズ制限]** | 必須。<br>新しいDynamic Mediaアカウントのみの場合、デフォルトのサイズ制限は自動的に「幅」に設定されます。 `3000` 高さ： `3000` 両方 **[!UICONTROL 画像サービング]** および **[!UICONTROL 画像サービングをテスト]**.<br>クライアントに返される返信画像の最大の幅と高さを指定します。 要求によって返信画像の幅または高さ（またはその両方）がこの設定よりも大きい場合、サーバーはエラーを返します。<br>関連トピック [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL リクエスト暗号化モード]** | 有効な要求に base64 エンコーディングを適用する場合は、有効にします。<br>関連トピック [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL リクエストロックモード]** | リクエストに単純なハッシュロックを含める場合は、有効にします。<br>関連トピック [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのリクエスト属性]** |  |
| **[!UICONTROL デフォルトの画像ファイルサフィックス]** | 必須。<br>パスにファイルサフィックスが含まれていない場合に、カタログの [ パス ] および [ マスクパス ] フィールドの値に追加される既定のデータファイル拡張子。<br>関連トピック [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのフォント書体名]** | テキストレイヤー要求でフォントが提供されない場合に使用するフォントを指定します。 指定する場合は、この画像カタログのフォントマップまたはデフォルトカタログのフォントマップで有効なフォント名の値を指定する必要があります。<br>関連トピック [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルト画像]** | リクエストされた画像が見つからない場合にリクエストに応じて返すデフォルトの画像を提供します。<br>関連トピック [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。<br>**注意**:Dynamic Media Classicアカウントに既に **[!UICONTROL デフォルトの画像]** 選択済み（以下に設定済み） **[!UICONTROL 設定]** > **[!UICONTROL アプリ]** > **[!UICONTROL 公開設定]**&#x200B;の下 **[!UICONTROL デフォルトの要求属性]** グループ )、Experience ManagerのDynamic MediaアカウントがDynamic Media Classicからファイルを取得します。 その後、ファイルが保存され、このフィールドで **[!UICONTROL Dynamic Media Publish Setup]** ページを初めて表示します。 |
| **[!UICONTROL デフォルトの画像モード]** | スライダボックスが有効な場合（右側のスライダ）、 **[!UICONTROL デフォルトの画像]** ソースイメージ内の見つからない各レイヤをデフォルトのイメージで置き換え、通常どおり合成を返します。 スライダボックスが無効の場合（左側のスライダ）、見つからないイメージが複数のレイヤの 1 つに過ぎない場合でも、デフォルトのイメージが合成イメージ全体を置き換えます。<br>関連トピック [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトの表示サイズ]** | 必須。<br>新しいDynamic Mediaアカウントの場合のみ、デフォルトの表示サイズが自動的に「幅」に設定されます。 `1280` 高さ： `1280` 両方 **[!UICONTROL 画像サービング]** および **[!UICONTROL 画像サービングをテスト]**.<br>要求で `wid=`, `hei=`または `scl=`.<br>関連トピック [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのサムネールサイズ]** | 必須。<br>属性の代わりに使用 **[!UICONTROL デフォルトの表示サイズ]** (`req=tmb`) をクリックします。 サムネール要求 (`req=tmb`) は、 `wid=`, `hei=`または `scl=`.<br>関連トピック [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトの背景色]** | 実際のRGBデータを含まない返信画像の任意の領域を埋めるのに使用する画像値を指定します。<br>関連トピック [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL JPEG エンコード属性]** |  |
| **[!UICONTROL 品質]** | <br>JPEG 返信画像のデフォルト属性を指定します。<br>新しいDynamic Mediaアカウントの場合のみ、 **[!UICONTROL 品質]** デフォルト値は自動的ににに設定されます。 `80` 両方 **[!UICONTROL 画像サービング]** および **[!UICONTROL 画像サービングをテスト]**.<br>このフィールドは 1 ～ 100 の範囲で定義されます。<br>関連トピック [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL 色度のダウンサンプリング]** | JPEGエンコーダーで使用される色分けダウンサンプリングを有効または無効にします。 |
| **[!UICONTROL デフォルトの再サンプリングモード]** | 画像データの拡大/縮小に使用する初期設定の再サンプリングおよび補間属性を指定します。 使用条件 `resMode` がリクエストで指定されていません。<br>新しいDynamic Mediaアカウントのみの場合、デフォルトの再サンプリングモードは自動的ににに設定されます。 `Sharp2` 両方 **[!UICONTROL 画像サービング]** および **[!UICONTROL 画像サービングをテスト]**.<br>関連トピック [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |

### 「共通のサムネール属性」タブ {#common-thumbnail-attributes-tab}

これらの設定は、サムネール画像のデフォルトの外観と配置に関係します。

| 設定 | 説明 |
| --- | --- |
| **[!UICONTROL サムネールのデフォルトの背景色]** | 実際のRGBデータを含まない出力サムネール画像の領域を埋めるための画像値を指定します。 サムネール要求 (`req=tmb`) および **[!UICONTROL 初期設定のサムネールの種類]** 設定が **[!UICONTROL フィット]** または **[!UICONTROL テクスチャ]**.<br>関連トピック [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL 水平方向揃え]** | 返信画像の長方形で、サムネール画像の水平方向の配置を指定します ( `wid=` および `hei=` 値。<br>サムネール要求 (`req=tmb`) および **[!UICONTROL 初期設定のサムネールの種類]** 設定が **[!UICONTROL フィット]**.<br>次の 3 つの水平線形から選択できます。 **[!UICONTROL 中央揃え]**, **[!UICONTROL 左揃え]**、および **[!UICONTROL 右揃え]**.<br>関連トピック [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL 垂直方向揃え]** | 返信画像の長方形で、サムネール画像の垂直方向の配置を指定します ( `wid=` および `hei=` 値。 サムネール要求 (`req=tmb`) および **[!UICONTROL 初期設定のサムネールの種類]** 設定が **[!UICONTROL フィット]**.<br>次の 3 つの垂直線形から選択できます。 **[!UICONTROL 上揃え]**, **[!UICONTROL 中央揃え]**、および **[!UICONTROL 下揃え]**.<br>関連トピック [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのクライアントキャッシュの有効期限]** | 特定のカタログレコードに有効なカタログ有効期限の値が含まれていない場合のデフォルトの有効期限間隔（時間単位）を指定します。に設定 `-1` 期限切れにならないとマークする <br>関連トピック [有効期限](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのサムネールの種類]** | 特定のカタログレコードに有効なカタログの ThumbType 値が含まれていない場合のサムネールの種類の初期設定を指定します。 サムネール要求 (`req=tmb`) をクリックします。<br>選択できるサムネールの種類は次の 3 つです。 **[!UICONTROL 切り抜き]**, **[!UICONTROL フィット]**、および **[!UICONTROL テクスチャ]**.<br>関連トピック [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL デフォルトのサムネール解像度]** | 特定のカタログレコードに有効な catalog ThumbRes 値が含まれていない場合の、サムネールオブジェクトの解像度の初期設定を指定します。 サムネール要求 (`req=tmb`) および **[!UICONTROL デフォルトのサムネールの種類]** 設定が **[!UICONTROL テクスチャ]**.<br>関連トピック [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |

### 「カラーマネジメント属性」タブ {#color-management-attributes-tab}

これらの設定は、画像に使用する ICC カラープロファイルを決定します。

**カラー変換レンダリングの方法**
色変換レンダリングインテントを使用すると、作業プロファイルのデフォルトのレンダリングインテントを上書きして、ソースカラーの調整方法を決定できます。 次の場合に使用されます。

1. デフォルトの ICC プロファイルの 1 つは、色変換のターゲットカラースペースです。
1. 出力デバイス（プリンタまたはモニタ）は、このプロファイルによって特徴付けられます。
1. また、指定したレンダリングインテントはこのプロファイルに対して有効です。

レンダリングの目的が異なると、ソースカラーの調整方法を決定する際に異なる規則が使用されます。

関連トピック [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。

>[!NOTE]
>
>一般に、選択したカラー設定に対しては、業界標準に準拠するためにAdobeがテストしたデフォルトのレンダリング方法を使用することをお勧めします。 例えば、北米またはヨーロッパのカラー設定を選択した場合、デフォルトのカラー変換レンダリング方法は次のようになります。 **[!UICONTROL 相対的な色域を維持]**. 日本のカラー設定を選択した場合のデフォルトのカラー変換レンダリング方法は次のとおりです。 **[!UICONTROL 知覚的]**.

| 設定 | 特徴 |
| --- | --- |
| **[!UICONTROL CMYK のデフォルトカラースペース]** | CMYK データの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。 If **[!UICONTROL 指定なし]** が選択されている場合、CMYK ソース画像が関係しているときは、この画像カタログのカラーマネジメントが無効になります。 すべての CMYK 作業用スペースはデバイスに依存します。つまり、実際のインクと紙の組み合わせに基づいています。 CMYK 作業用スペースAdobeの供給は、標準的な商業印刷条件に基づいています。<br> 関連トピック [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL グレースケールのデフォルトカラースペース]** | グレースケールデータの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。 If **[!UICONTROL 指定なし]** を選択した場合、グレースケールのソース画像が関係する場合、この画像カタログのカラーマネジメントは無効になります。<br>関連トピック [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL RGB のデフォルトカラースペース]** | RGBデータの作業プロファイルとして使用する ICC カラープロファイルの名前を指定します。 If **[!UICONTROL 指定なし]** が選択されている場合、RGBソース画像が関係すると、この画像カタログのカラーマネジメントは無効になります。 一般に、選択するのが最善です **[!UICONTROL Adobe RGB]** または **[!UICONTROL sRGB]**&#x200B;特定のデバイス（モニタープロファイルなど）のプロファイルではなく。 **[!UICONTROL sRGB]** は、web またはモバイルデバイス用の画像を準備する際に推奨されます。これは、web 上の画像の表示に使用される標準モニタのカラースペースを定義するからです。 **[!UICONTROL sRGB]** また、消費者レベルのデジタルカメラの画像を操作する場合にも適しています。これらのカメラのほとんどは sRGB をデフォルトのカラースペースとして使用するからです。<br>関連トピック [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) パラメーターに関する情報をDynamic Mediaビューアリファレンスガイドで参照してください。 |
| **[!UICONTROL カラー変換レンダリングの方法]** | **[!UICONTROL 知覚的]**  — 色の値自体が変化する場合でも、人間の目に自然と感じられるように、色間の視覚的な関係を保つことを目的としています。 この目的は、色域外の色が多い写真画像に適しています。 この設定は、日本の印刷業界にとっての標準的なレンダリング意図です。 |
|  | **[!UICONTROL 相対的な色域を維持]**  — ソースカラースペースの極端なハイライトを、目的のカラースペースのハイライトと比較し、それに応じてすべての色をシフトします。 色域外の色は、出力先のカラースペースで最も近く再現可能な色にシフトします。 「相対的な色域を維持」では、「知覚的」よりも多くの元の色が画像に保持されます。 この設定は、北米およびヨーロッパでの印刷の標準的なレンダリング方法です。 |
|  | **[!UICONTROL 彩度]**  — 画像内で色の精度を犠牲にして鮮やかな色を生成しようとします。 このレンダリング方法は、グラフやグラフなどのビジネスグラフィックに適しています。色間の正確な関係よりも明るい飽和色が重要です。 |
|  | **[!UICONTROL 絶対的な色域を維持]**  — 対象の色域内に含まれる色は変更されません。 色域外の色は切り取られます。 目的の白点に対する色の拡大・縮小は行われません。 この目的は、色間の関係を保つことを犠牲にして色の精度を維持することを目的とし、特定のデバイスの出力をシミュレートするための校正に適しています。 この方法は、用紙の色が印刷色に与える影響をプレビューする場合に便利です。 |

## アセットを公開する前にテストする {#test-assets-before-making-public}

セキュアテストを使用すると、セキュアテスト環境を定義し、IP アドレスと範囲の設定可能なセットに基づいて、堅牢な B2B ソリューションを構築できます。 この機能を使用すると、AdobeのDynamic Mediaの導入と、コンテンツ管理およびビジネスシステムのアーキテクチャを一致させることができます。

セキュアテストを使用すると、非公開のコンテンツを含む Web サイトのステージングバージョンをプレビューできます。

必要に応じて、以下の理由でアセットを公開する代わりに、ステージング環境を作成します。

* 公開前に Web サイトをプレビューする（ステージング用 Web サイト）。
* B2B Web アプリケーションで価格を表示する eCatalog など、制限付きアクセスを必要とするアセットを提供する。
* 製品情報管理システム、顧客サービスアプリケーション、トレーニングサイトなどの一部として、ファイアウォールの内側にあるアセットを使用する。

>[!NOTE]
>
>セキュアテストは、Adobe Dynamic Media Classicへのアクセスに影響しません。 Adobe Dynamic Media Classicのセキュリティは一貫しており、Adobe Dynamic Media Classicおよび関連する Web サービスにアクセスするための通常の資格情報が必要です。

### セキュアテストの仕組み {#how-test-assets-works}

ほとんどの企業は、ファイアウォールの内側でインターネットを実行します。 インターネットへのアクセスは、特定のルートを通じて可能で、通常は限られた範囲のパブリック IP アドレスを通じて可能です。

企業ネットワークから、 [https://www.whatismyip.com](https://www.whatismyip.com/) または、企業の IT 組織にこの情報を要求します。

セキュアテストを使用すると、AdobeDynamic Mediaは、ステージング環境または内部アプリケーション用に専用の画像サーバーを確立します。 このサーバーへのリクエストはすべて、発信元 IP アドレスをチェックします。受信リクエストが IP アドレスの承認済みリストに含まれていない場合は、失敗のレスポンスが返されます。
AdobeDynamic Mediaの会社管理者が、自社のセキュアテスト環境で使用する承認済み IP アドレスリストを設定します。

元のリクエストの場所を確認する必要があるので、セキュアテストサービスのトラフィックは、パブリックDynamic Media Image Server トラフィックのようなコンテンツ配布ネットワークを通じてルーティングされません。 セキュアテストサービスへのリクエストの待ち時間は、パブリックなDynamic Media Image Server に比べて若干長くなります。

非公開のアセットは、セキュアテストサービスから直ちに使用できます。公開する必要はありません。 この方法では、公開されている Image Server にアセットを公開する前にプレビューを実行できます。

>[!NOTE]
>
>セキュアテストサービスは、内部公開コンテキストで設定されたカタログサーバを使用します。 したがって、セキュアテストに公開するように会社が設定されている場合、AdobeDynamic Media内にアップロードされたアセットは、セキュアテストサービスですぐに使用できるようになります。 この機能は、アセットがアップロード時に公開用にマークされているかどうかに関係なく当てはまります。

セキュアテストサービスは、現在、次のアセットのタイプと機能をサポートしています。

* 画像.
* ビネット（Render Server 要求）。
* Render Server リクエスト（サポート対象、ただしお客様が明示的にリクエストする必要あり）。
* 画像セット、eCatalog、レンダリングセット、メディアセットなどのセット。
* 標準AdobeのDynamic Mediaリッチメディアビューア。
* AdobeDynamic Media OnDemand JSP ページ。
* 静的コンテンツ (PDFファイルやプログレッシブにビデオを提供するなど )。
* HTTP ビデオストリーミング。
* プログレッシブビデオストリーミング。

次のアセットタイプと機能は、現在、サポートされていません。

* Adobe Dynamic Media Classic Info または eCatalog 検索
* RTMP ビデオストリーミング
* Web-to-print
* UGC（ユーザー生成コンテンツ）サービス

>[!IMPORTANT]
>
>AdobeDynamic Mediaでの新規または既存の UGC ベクトル画像アセットのサポートは、2021 年 9 月 30 日に終了しました。

### セキュアテストサービスのテスト {#test-secure-testing-service}

セキュアテストサービスが期待どおりに動作することを確認するには、次の手順を実行します。

#### アカウントの準備

1. Adobeカスタマーケアに問い合わせ、お使いのアカウントでセキュアテストを有効にするよう依頼します。
1. Adobe Experience Managerで、 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. Image Server ページの **[!UICONTROL 公開コンテキスト]** ドロップダウンリストで、「 **[!UICONTROL 画像サービングをテスト]**.
1. を選択します。 **[!UICONTROL セキュリティ]** タブをクリックします。
1. の **[!UICONTROL クライアントアドレス]** フィルター、選択 **[!UICONTROL 追加]**.
1. 内 **[!UICONTROL IP アドレス]** 「 」フィールドに、IP アドレスを入力します。
1. 内 **[!UICONTROL マスク]** 「 」フィールドに、ネットマスクを入力します。

   >[!NOTE]
   >
   >複数の IP アドレスとネットマスクを追加する場合は、有効に許可されます *すべて* アセット呼び出しをおこなう IP アドレス。すべて表示されます。

1. 次のいずれかの操作を行います。

   * さらに IP アドレスを追加するには、前の 3 つの手順を繰り返します。
   * 次の手順に進みます。

1. Image Server ページの右上隅で、 **[!UICONTROL 保存]**.
1. 目的の画像をAdobeDynamic Mediaアカウントにアップロードします。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 一部の画像が公開用にマークされ、他の画像がマークされていないことを確認してから、公開ジョブを送信します。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. セキュアテストサービスの名前を決定するには、 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Setting]**.
1. の **[!UICONTROL サーバー]** 」ページで、右側のサーバー名を探します。 **[!UICONTROL 公開先サーバー名]**.

Adobeケアに問い合わせて、サーバー名が見つからないか、サーバーの URL が機能しない場合。

#### Web サイトのバリエーションを準備する

公開済みアセットと非公開アセットをリンクする Web サイトには、次の 2 つのバリエーションが必要です。

* 公開バージョン — 従来のAdobeDynamic Media URL 構文を使用してアセットをリンクします。
* ステージングバージョン — 同じ構文を使用し、セキュアテストサイト名を使用してアセットをリンクします。

#### テストの実行

次のテストを実行します。

1. 会社のネットワーク内からアセットが表示されるかどうかを確認します。

   以前に定義した IP アドレス範囲で識別される企業ネットワーク内から、Web サイトのステージングバージョンには、公開用にマークされているかどうかに関わらず、すべての画像が表示されます。 したがって、プレビューの承認や製品の起動の前に、誤って画像を使用可能にすることなくテストできます。

   サイトの公開バージョンに、AdobeDynamic Mediaで以前に経験した公開済みアセットが表示されていることを確認します。

1. 企業のネットワーク外から、非公開のアセット（公開用にマークされていない）がサードパーティのアクセスから保護されていることを確認します。

   外部（自宅のコンピューターや 4G/5G 接続など）からネットワークにアクセスし、サイトの公開バージョンに公開済みのアセットがすべて表示され、非公開のコンテンツは表示されないことを確認します。

   未承認の IP アドレスからセキュアテストサービスにアクセスしているので、ステージングバージョンでアセットが表示されないことを確認します。
