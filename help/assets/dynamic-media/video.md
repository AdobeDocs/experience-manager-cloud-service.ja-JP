---
title: Dynamic Media のビデオ
description: Dynamic Media でビデオを使用する方法について説明します。ビデオのエンコード、YouTube へのビデオの公開、ビデオレポートの表示、クローズドキャプション、字幕、チャプターマーカーのビデオへの追加に関するベストプラクティスをレビューします。
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 96d11aad425ba7c78a685b3509cd96749d938229
workflow-type: tm+mt
source-wordcount: '5887'
ht-degree: 98%

---

# ビデオ {#video}

ここでは、Dynamic Media でのビデオの操作について説明します。

## クイックスタート：ビデオ {#quick-start-videos}

次のワークフローの手順説明は、Dynamic Media でアダプティブビデオセットをすぐに使い始めることを目的としたものです。各手順に続いて、詳しい説明のあるトピックの見出しへのリンクが記載されています。

>[!NOTE]
>
>Dynamic Media のビデオを操作する前に、Adobe Experience Manager の管理者が既に Dynamic Media Cloud Services を有効にして設定を完了していることを確認してください。
>
>* Dynamic Media 設定の [Dynamic Media Cloud Services の設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)、および [Dynamic Media のトラブルシューティング](/help/assets/dynamic-media/troubleshoot-dm.md)を参照してください。
>


1. 次の手順を実行して、**Dynamic Media ビデオをアップロード**&#x200B;します。

   * 独自のビデオエンコーディングプロファイルを作成します。または、Dynamic Media に付属している事前定義済みの&#x200B;_アダプティブビデオエンコーディング_（AVE）プロファイルを使用してもかまいません。

      * [ビデオエンコーディングプロファイルを作成します](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 詳しくは、[ビデオエンコーディングのベストプラクティス](#best-practices-for-encoding-videos)を参照してください。
   * ビデオ処理プロファイルを、プライマリソースビデオのアップロード先となる 1 つ以上のフォルダーに関連付けます。

      * [ビデオプロファイルをフォルダーに適用します](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
      * 詳しくは、[デジタルアセットの整理](/help/assets/organize-assets.md)を参照してください。
   * フォルダーにプライマリソースビデオをアップロードします。フォルダーにビデオを追加すると、そのフォルダーに割り当てたビデオ処理プロファイルに従ってビデオがエンコードされます。

      * Dynamic Media では、最大長 30 分、最小解像度が 25 x 25 を超える短い形式のビデオが主にサポートされています。
      * 15 GB までのビデオファイルをアップロードできます。
      * [ビデオをアップロードします](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
      * 詳しくは、[サポートされる入力ファイル形式](/help/assets/file-format-support.md)を参照してください。
   * アセットビューまたはワークフロービューから[ビデオエンコーディングの進捗](#monitoring-video-encoding-and-youtube-publishing-progress)を監視します。




1. 次のいずれかの操作を行って、**Dynamic Media ビデオを管理します**。

   * ビデオアセットの整理、参照、検索

      * [デジタルアセットの整理](/help/assets/organize-assets.md)
      * [ビデオアセットを検索](/help/assets/search-assets.md#custompredicates)するか[アセットを検索](/help/assets/manage-digital-assets.md#search-assets)します。
   * ビデオアセットをプレビューして公開します。

      * ソースビデオとビデオのエンコードされたレンディションを、関連するサムネールと共に表示します。
         [ビデオをプレビュー](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)するか[アセットをプレビュー](/help/assets/dynamic-media/previewing-assets.md)します。
         [ビデオレンディションを管理します](/help/assets/manage-digital-assets.md#managing-renditions)。

      * [ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * ビデオのメタデータを操作します。

      * タイトル、説明、タグ、カスタムメタデータフィールドなど、ビデオのプロパティを編集：
         [ビデオのプロパティの編集](/help/assets/manage-digital-assets.md#editing-properties)

      * [デジタルアセット用のメタデータの管理](/help/assets/manage-metadata.md)
      * [メタデータスキーマ](/help/assets/metadata-schemas.md)
   * ビデオをレビューおよび承認し、注釈を付け、完全なバージョン管理を維持します。

      * [ビデオへの注釈](/help/assets/manage-video-assets.md#annotate-video-assets)または[アセットへの注釈](/help/assets/manage-digital-assets.md#annotating)

      * [バージョンの作成](/help/assets/manage-digital-assets.md#asset-versioning)
      * [アセットでのワークフローの開始](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [フォルダーのアセットのレビュー](/help/assets/bulk-approval.md)
      * [プロジェクト](/help/sites-cloud/authoring/projects/overview.md)




1. 次のいずれかの操作を行って、**Dynamic Media ビデオを公開します**。

   * Adobe Experience Manager を WCM（web コンテンツ管理）システムとして使用する場合、web ページにビデオを直接追加できます。

      * [Web ページにビデオを追加します](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。
   * サードパーティの web コンテンツ管理システムを使用している場合、web ページにビデオをリンクするか、ビデオを埋め込むことができます。

      * URL を使用したビデオの統合：
         [Web アプリケーションに URL をリンクします](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。

      * Web ページの埋め込みコードを使用したビデオの統合：
         [Web ページにビデオビューアを埋め込みます](/help/assets/dynamic-media/embed-code.md)。
   * [ビデオレポートを生成します](#viewing-video-reports)。

   * [ビデオにキャプションを追加します](#adding-captions-to-video)。



## Dynamic Media でのビデオの操作 {#working-with-video-in-dynamic-media}

Dynamic Media のビデオは、高品質のアダプティブビデオを簡単に公開して、デスクトップ、タブレット、モバイルデバイスを含む複数の画面にストリーミングするためのエンドツーエンドのソリューションです。アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップコンピューターまたはモバイルデバイスが、使用可能な帯域幅を検出します。

例えば、iOS モバイルデバイスでは、3G、4G、Wi-Fi などの帯域幅が検出されます。次に、アダプティブビデオセット内の様々なビデオビットレートの中から、適切なエンコード済みビデオが自動的に選択されます。ビデオはデスクトップ、モバイルデバイスまたはタブレットにストリーミングされます。

また、デスクトップまたはモバイルデバイスでネットワークの状態が変化した場合は、ビデオ画質が自動的に動的に切り替わります。また、顧客がデスクトップで全画面表示モードに入ると、アダプティブビデオセットはより高い解像度を使用して顧客の視聴エクスペリエンスを向上させるよう対応します。アダプティブビデオセットを使用すると、Dynamic Media ビデオを複数の画面やデバイスで再生する顧客に最適な再生を提供できます。

どのエンコードされたビデオを再生するか、または再生中に選択するかを決定するためにビデオプレーヤーが使用するロジックは、次のアルゴリズムに基づいています。

1. ビデオプレーヤーは、プレーヤー自体の「初期ビットレート」に設定されている値に最も近いビットレートに基づいて、初期ビデオフラグメントを読み込みます。
1. 次の条件を使用して、帯域幅の速度の変化に応じてビデオプレーヤーが切り替わります。

   1. プレーヤーは、推定帯域幅を越えない範囲で最大帯域幅のストリームを選択します。
   1. プレーヤーは、使用可能な帯域幅の 80％ほどを見積もります。ただし、使用可能な帯域幅が上昇した場合は、帯域幅を大きく見積もりすぎてすぐに元の帯域幅に戻ることを防ぐために、より控えめな 70％ほどの見積もりとなります。

アルゴリズムの技術情報について詳しくは、[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp) を参照してください。

単一のビデオとアダプティブビデオセットの管理では、次の機能がサポートされています。

* 多数のサポートされているビデオ形式およびオーディオ形式からビデオをアップロードし、複数の画面で再生できるようにビデオを MP4 H.264 形式にエンコーディングします。事前定義済みのアダプティブビデオプリセット、または単一のビデオエンコーディングプリセットを使用するか、独自のエンコーディングをカスタマイズしてビデオの品質とサイズを制御することができます。

   * 生成されるアダプティブビデオセットには、MP4 ビデオが含まれます。
   * **注意**：プライマリ／ソースビデオはアダプティブビデオセットには追加されません。

* すべての HTML5 ビデオビューアーでビデオキャプションを追加します。
* ビデオアセットを効率的に管理するための完全なメタデータサポートを使用して、ビデオを整理、参照および検索します。
* アダプティブビデオセットを web およびデスクトップ、タブレット、モバイルデバイスに配信します。

アダプティブビデオのストリーミングは、各種 iOS プラットフォームでサポートされています。詳しくは、[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html?lang=ja)を参照してください。

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* 以下を含む Dynamic Media ビデオビューアープリセットを使用して、ビデオを再生します。

   * 単一のビデオビューアー
   * ビデオコンテンツと画像コンテンツの両方を組み合わせた混在メディアビューアー

* ブランド要件を満たすようにビデオプレーヤーを設定します。
* 単純な URL か埋め込みコードを使用して、ビデオを web サイト、モバイルサイトまたはモバイルアプリケーションに統合します。

詳しくは、[動的なビデオ再生](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480)の例を参照してください。

[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=ja)の [Experience Manager Assets および Dynamic Media Classic のビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html?lang=ja#viewers-aem-assets-dmc)および [Experience Manager Assets 専用のビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html?lang=ja#viewers-for-aem-assets-only)も参照してください。

## ベストプラクティス：HTML5 ビデオビューアの使用 {#best-practice-using-the-html-video-viewer}

Dynamic Media の HTML5 ビデオビューアプリセットは堅牢なビデオプレーヤーです。このプリセットを使用すれば、HTML5 ビデオ再生でよくある問題や、モバイルデバイスに関する問題の多くを回避することができます。例えば、アダプティブビットレートストリーミング配信機能がなかったり、デスクトップブラウザーの範囲が限定されていたりすることなどです。

プレーヤーの設計面では、標準の web 開発ツールを使用してビデオプレーヤーの機能を設計できます。例えば、HTML5 と CSS を使用して、ボタン、コントロールおよびカスタムのポスター画像背景をデザインすることにより、カスタマイズした表示で顧客にリーチすることができます。

ビューアの再生側では、ブラウザーのビデオ機能を自動的に検出します。その後、HLS または DASH（アダプティブビデオストリーミングとも呼ばれる）を使用してビデオを配信します。または、これらの配信方法が使用できない場合は、HTML5 プログレッシブが代わりに使用されます。

>[!NOTE]
>
>ビデオに DASH を使用するには、まず Adobe テクニカルサポートがアカウントで DASH を有効にする必要があります。詳しくは、「[アカウントでの DASH の有効化](#enable-dash)」を参照してください。

HTML5 と CSS を使用して再生コンポーネントを設計できる機能を 1 つのプレーヤーに統合できます。埋め込み再生が可能で、ブラウザーの機能に応じてアダプティブストリーミングやプログレッシブストリーミングを使用できます。これらの結果、リッチメディアコンテンツの配信範囲をデスクトップユーザーとモバイルユーザーの両方に拡大し、ビデオエクスペリエンスを確実に効率化することができます。

[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=ja)の [Experience Manager Assets 専用のビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html?lang=ja#viewers-for-aem-assets-only)も参照してください。


### HTML5 ビデオビューアを使用した、デスクトップコンピューターおよびモバイルデバイス上でのビデオ再生 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

デスクトップおよびモバイルへのアダプティブビデオストリーミングの場合、ビットレートの切り替えに使用されるビデオは、アダプティブビデオセット内のすべての MP4 ビデオに基づいています。

ビデオの再生は、HLS または DASH、またはプログレッシブビデオダウンロードのいずれかを使用して行われます。6.0、6.1、6.2 など以前の Experience Manager バージョンでは、ビデオは HTTP 上でストリーミングされました。

一方、Experience Manager 6.3 以降では、DM ゲートウェイサービスの URL も常に HTTPS を使用するため、ビデオは HTTPS（つまり、HLS または DASH）でストリーミングされるようになりました。このデフォルトの動作はユーザーに影響しません。つまり、ブラウザーでサポートされていない場合を除き、ビデオストリーミングは常に HTTPS 上で行われます（以下の表を参照してください）。

したがって、

* HTTPS web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しています。
* HTTP web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しており、web ブラウザーから混合コンテンツに関する問題は発生しません。

DASH は国際標準であり、HLS は Apple の標準です。どちらもアダプティブビデオストリーミングに使用されます。どちらのテクノロジーも、ネットワーク帯域幅の容量に基づいて再生を自動的に調整します。また、HLS では、ビデオの残りがダウンロードされるまで待たなくても、ビデオ内の任意のポイントを「シーク」できます。

プログレッシブビデオは、ユーザーのデスクトップシステムやモバイルデバイスにダウンロードしてローカルに保存することで配信されます。

デバイス、ブラウザー、およびデスクトップコンピューターやモバイルデバイスでの [Dynamic Media HTML5 ビデオビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html?lang=ja#interactive-video)によるビデオの再生方法を次の表に示します。

<table>
 <tbody>
  <tr>
   <td><strong>デバイス</strong></td>
   <td><strong>ブラウザー</strong></td>
   <td><strong>ビデオ再生モード</strong></td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Internet Explorer 9 および 10</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Internet Explorer 11+</td>
   <td>Windows® 8 および Windows® 10 では、DASH または HLS が要求されるたびに HTTPS を強制的に使用します。既知の制約事項：DASH または HLS の HTTP は、このブラウザーとオペレーティング システムの組み合わせでは機能しません<br /> <br /> Windows® 7 の場合 - プログレッシブダウンロード。HTTP プロトコルと HTTPS プロトコルの選択に標準のロジックを使用します。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Firefox 23～44</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Firefox 45 以降</td>
   <td>HLS または DASH* アダプティブビットレートストリーミング</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Chrome</td>
   <td>HLS または DASH* アダプティブビットレートストリーミング</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Safari（Mac）</td>
   <td>HLS アダプティブビットレートストリーミング</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（Android™ 6 以前）</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（Android™ 7 以降）</td>
   <td>HLS または DASH* アダプティブビットレートストリーミング/td&gt;
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Android™（デフォルトブラウザー）</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Safari（iOS）</td>
   <td>HLS アダプティブビットレートストリーミング</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（iOS）</td>
   <td>HLS アダプティブビットレートストリーミング</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*ビデオに DASH を使用するには、まずアカウントの Adobe テクニカルサポートが DASH を有効にする必要があります。詳しくは、「[アカウントでの DASH の有効化](#enable-dash)」を参照してください。

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media ビデオソリューションのアーキテクチャ {#architecture-of-dynamic-media-video-solution}

次の図に、アップロード後、（Dynamic Media Hybrid モードの）DMGateway によってエンコードされ、公開されるビデオのオーサリングワークフローの全体像を示します。

![chlimage_1-427](assets/chlimage_1-427.png)

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## ビデオエンコーディングのベストプラクティス {#best-practices-for-encoding-videos}

Dynamic Media を有効にし、ビデオ Cloud Services を設定済みの場合、**Dynamic Media エンコードビデオ**&#x200B;ワークフローがビデオをエンコードします。このワークフローは、ワークフローの処理履歴とエラー情報を取り込みます。Dynamic Media を有効にし、ビデオ Cloud Services を設定してある場合は、ビデオをアップロードすると、**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローが自動的に有効になります（Dynamic Media を使用していない場合は、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローが有効になります）。

ここでは、ソースビデオファイルのエンコードにおけるベストプラクティスのヒントを説明します。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### ソースビデオファイル {#source-video-files}

ビデオファイルをエンコードする場合は、可能な限り高品質のソースビデオファイルを使用します。 以前にエンコードされたビデオファイルは使用しないでください。これらのファイルは既に圧縮されており、さらにエンコーディングすると標準を下回る品質のビデオが作成されます。

* Dynamic Media では、最大長 30 分、最小解像度が 25 x 25 を超える短い形式のビデオが主にサポートされています。
* 15 GB までのプライマリソースビデオファイルをアップロードできます。

次の表に、ソースビデオファイルのエンコード前の推奨サイズ、縦横比および最小ビットレートを示します。

| サイズ | 縦横比 | 最低ビットレート |
|--- |--- |--- |
| 1024 x 768 | 4:3 | ほとんどのビデオで 4500 kbps |
| 1280 x 720 | 16:9 | ビデオ内のモーションの量に応じて 3,000～6,000 kbps。 |
| 1920 x 1080 | 16:9 | ビデオ内のモーションの量に応じて 6,000～8,000 kbps |

### ファイルのメタデータの取得 {#obtaining-a-file-s-metadata}

ファイルのメタデータは、ビデオ編集ツールを使用してメタデータを表示するか、メタデータを取得するために設計されたアプリケーションを使用して取得できます。以下は、サードパーティアプリケーションの MediaInfo を使用してビデオファイルのメタデータを取得する手順です。

1. [MediaInfo のダウンロードページ](https://mediaarea.net/ja/MediaInfo/Download)に移動します。
1. GUI バージョンのインストーラーを選択してダウンロードし、インストール手順に従って操作します。
1. インストールの完了後、ビデオファイルを右クリックして（Windows® のみ）MediaInfo を選択するか、MediaInfo を開いてビデオファイルをアプリケーションにドラッグします。ビデオの幅、高さ、fps など、ビデオファイルに関連するすべてのメタデータが表示されます。

### 縦横比 {#aspect-ratio}

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択または作成するときには、プライマリソースビデオファイルと同じ縦横比をプリセットに使用してください。縦横比とは、ビデオの高さに対する幅の比率のことです。

ビデオファイルのアスペクト比を求めるには、ファイルのメタデータを取得し、そのファイルの幅と高さを記録します（前述の「ファイルのメタデータの取得」を参照してください）。さらに、次の式を使用してアスペクト比を計算します。

幅/高さ = 縦横比

次の表に、数式の結果が一般的なアスペクト比に変換される方法を示します。

| 数式の結果 | 縦横比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例えば、幅 1,440、高さ 1,080 のビデオの縦横比は 1,440/1,080、つまり 1.33 になります。このビデオファイルをエンコードするには、縦横比 4:3 のビデオエンコーディングプリセットを選択します。

### ビットレート {#bitrate}

ビットレートとは、1 秒間のビデオ再生を構成するエンコードされたデータの量です。ビットレートは、キロビット/秒（Kbps）単位で測定されます。

>[!NOTE]
>
>すべてのコーデックは非可逆圧縮を使用するので、ビットレートはビデオ画質の最も重要な要素となります。非可逆圧縮では、ビデオファイルを圧縮するほど画質が低下します。このため、他のすべての特性（解像度、フレームレートおよびコーデック）が等しいと、ビットレートが低いほど圧縮ファイルの品質が低下します。

ビットレートエンコーディングは、次の 2 つのタイプから選択できます。

* **[!UICONTROL 固定ビットレートエンコーディング]**（CBR）- CBR エンコーディングでは、ビットレートまたは 1 秒あたりのビット数が、エンコーディングプロセス全体で同じ数値に維持されます。CBR エンコーディングでは、設定されているデータレートが、ビデオ全体での設定値として使用されます。また、CBR エンコーディングでは、メディアファイルの品質は最適化されませんが、その分、空き容量の節約になります。ビデオ全体に同じようなモーションレベルが含まれている場合は、CBR を使用します。CBR は、ビデオコンテンツのストリーミングに最も一般的に使用されています。[カスタムで追加するビデオエンコーディングパラメーターの使用](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters)も参照してください。

* **[!UICONTROL 可変ビットレートエンコーディング]**（VBR）- VBR エンコーディングでは、コンプレッサーで必要となるデータに基づいて、設定したデータレートが下限から上限の範囲内で調整されます。つまり、VBR エンコーディングプロセスでは、メディアファイルのビットレートが、そのニーズに応じて動的に増減します。VBR は、CBR よりエンコードに時間がかかりますが、生成されるメディアファイルは最高品質となります。VBR は、ビデオコンテンツの HTTP プログレッシブ配信に最も一般的に使用されます。

VBR と CRB のどちらを使用するべきかVBR と CBR のどちらを選択すべきかと言えば、ほとんどの場合、メディアファイルには VBR を使用することをお勧めします。VBR は、優位性のあるビットレートで CBR より高品質のファイルを生成します。VBR を使用するときは、2 パスエンコーディングを使用し、最大ビットレートをターゲットビデオのビットレートの 1.5 倍に設定してください。

ビデオエンコーディングプリセットを選択するときは、ターゲットエンドユーザーの接続速度を考慮してください。データレートがその速度の 80％となるプリセットを選択してください。例えば、ターゲットエンドユーザーの接続速度が 1,000 Kbps の場合、ビデオデータレートが 800 kbps のプリセットが最適です。

次の表に、一般的な接続速度のデータレートを示します。

| 速度（kbps） | 接続タイプ |
|--- |--- |
| 256 | ダイヤルアップ接続。 |
| 800 | 一般的なモバイル接続。 この接続では、3G エクスペリエンスに対して、400～最大 800 の範囲のデータレートをターゲットにします。 |
| 2,000 | 一般的なブロードバンドデスクトップ接続。この接続では、800～2,000 Kbps の範囲のデータレートがターゲットとなります。大部分のターゲットは、平均 1,200～1,500 Kbps です。 |
| 5,000 | 一般的な高ブロードバンド接続。この速度ではほとんどの消費者にビデオを配信できないので、これを範囲の上限としてエンコーディングすることはお勧めしません。 |

### 解像度 {#resolution}

**解像度**&#x200B;は、ビデオファイルの高さと幅をピクセル単位で表したものです。ほとんどのソースビデオは、1920 x 1080 などの高解像度で保存されます。ストリーミング用のソースビデオは、比較的低い解像度（640 x 480 以下）に圧縮されます。

解像度とデータレートは、ビデオ画質を決定する統合的な 2 つの要素です。同じビデオ画質を維持するには、ビデオファイルのピクセル数が多いほど（解像度が高いほど）、データレートを高くする必要があります。例えば、320 x 240 の解像度と 640 x 480 の解像度のビデオファイルで、フレームあたりのピクセル数を考えてみましょう。

| 解像度 | フレームあたりのピクセル数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480 ファイルのピクセル数は、フレームあたり 4 倍になります。この 2 つの解像度の例でデータレートを同じにするには、640 x 480 ファイルを 4 倍に圧縮します。これにより、ビデオの画質が低下する可能性があります。そのため、250 kbps のビデオデータレートの場合、320 x 240 の解像度では高画質になりますが、640 x 480 の解像度では高画質になりません。

一般に、高いデータレートを使用するほど、ビデオの画質は良くなり、高い解像度を使用するほど、その画質を維持するために必要になるデータレートも（解像度が低い場合と比較して）増加します。

解像度とデータレートには関連があるので、ビデオをエンコードする際には次の 2 つの方法から選択できます。

* データレートを選択してから、選択したデータレートできれいに表示される最高の解像度でエンコードします。
* 解像度を選択してから、選択した解像度で高品質のビデオを配信するために必要になるデータレートでエンコードします。

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択（または作成）する場合は、次の表を使用して正しい解像度をターゲットにします。

| 解像度 | 高さ（ピクセル） | 画面サイズ |
|--- |--- |--- |
| 240p | 240 | 小さい画面 |
| 300p | 300 | 小さい画面（通常はモバイルデバイス用） |
| 360p | 360 | 小さい画面 |
| 480p | 480 | 中程度の画面 |
| 720p | 720 | 大きな画面 |
| 1080p | 1080 | 高解像度の大画面 |

### Fps（1 秒あたりのフレーム数） {#fps-frames-per-second}

米国と日本では、ほとんどのビデオが 29.97 フレーム/秒（fps）で撮影されます。ヨーロッパでは、ほとんどのビデオが 25 fps で撮影されます。映画は 24 fps で撮影されます。

プライマリソースビデオファイルの fps レートに一致するビデオエンコーディングプリセットを選択します。例えば、プライマリソースビデオが 25 fps の場合は、25 fps のエンコーディングプリセットを選択します。デフォルトでは、すべてのカスタムエンコーディングでプライマリソースビデオファイルの fps が使用されます。そのため、ビデオエンコーディングプリセットを作成するときに、fps 設定を明示的に指定する必要はありません。

### ビデオエンコーディングのサイズ {#video-encoding-dimensions}

最適な結果を得るには、ソースビデオがすべてのエンコードされたビデオの整数倍になるようにエンコーディングのサイズを選択します。

この比率を計算するには、ソースの幅をエンコードされた幅で割って、幅の比率を求めます。次に、エンコードされた高さでソースの高さを割って、高さの比率を求めます。

結果の比率が整数の場合、ビデオは最適に縮小されています。結果の比率が整数でない場合は、余ったピクセルのアーティファクトがディスプレイに残るので、ビデオの画質に影響します。この影響は、ビデオにテキストが含まれている場合に顕著に現れます。

例えば、ソースビデオが 1920 x 1080 だとします。次の表では、エンコードされた 3 つのビデオで使用する、最適なエンコード設定を示しています。

| ビデオタイプ | 幅 x 高さ | 幅の比率 | 高さの比率 |
|--- |--- |--- |--- |
| ソース | 1920 x 1080 | 1 | 1 |
| エンコード済み | 960 x 540 | 2 | 2 |
| エンコード済み | 640 x 360 | 3 | 3 |
| エンコード済み | 480 x 270 | 4 | 4 |

### エンコードされたビデオのファイル形式 {#encoded-video-file-format}

Dynamic Media では、MP4 H.264 ビデオエンコーディングプリセットの使用をお勧めします。MP4 ファイルは H.264 ビデオコーデックを使用するので、ビデオは高品質になるものの圧縮されたファイルサイズです。

### アカウントでの DASH の有効化 {#enable-dash}

DASH（HTTP での動的アダプティブストリーミング）はビデオストリーミングの国際標準であり、様々なビデオビューアーで広く採用されています。アカウントで DASH が有効になっている場合は、アダプティブビデオストリーミング用に DASH または HLS のいずれかを選択できます。ビューアのプリセットで再生タイプとして「**[!UICONTROL 自動]**」が選択されていると、プレーヤー間の自動切り替えで両方を選択できます。

アカウントで DASH を有効にする場合の主なメリットには、次のようなものがあります。

* アダプティブビットレートストリーミング用に DASH ストリームビデオをパッケージ化できます。この方法では配信の効率が向上します。アダプティブストリーミングにより、顧客に最適な視聴エクスペリエンスが提供されます。
* Dynamic Media プレイヤーでブラウザーに最適化されたストリーミングにより、HLS と DASH のストリーミングを切り替え、最高のサービス品質を確保できます。Safari ブラウザーを使用すると、ビデオプレーヤーが HLS に自動的に切り替わります。
* ビデオビューアプリセットを編集して、優先ストリーミング方式（HLS または DASH）を設定できます。
* 最適化されたビデオエンコーディングにより、DASH 機能を有効にしながら、追加のストレージを使用しなくて済みます。HLS と DASH の両方に対して 1 つのビデオエンコードセットが作成され、ビデオの保存コストが最適化されます。
* 顧客がビデオ配信をアクセスしやすくなります。
* API を使用してストリーミング URL を取得することもできます。

   >[!IMPORTANT]
   >
   >現在、アカウントで DASH を有効にするのは、アジア太平洋および北米でのみ利用できます。ヨーロッパ中東アフリカで間もなく登場する

DASH を使用するリクエストを開始します。お使いのアカウントで自動的には有効になりません。

お使いのアカウントで DASH を有効にするには、以下に示すようにカスタマーサポートケースを作成します。サポートケースで、Dynamic Media アカウントと Experience Manager で DASH を有効にするように指定します。

**アカウントで DASH を有効にするには：**

1. [Admin Console を使用して、新しいサポートケースの作成を開始します](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
1. 手順に従って、次の情報を入力し、サポートケースを作成します。

   * 主要連絡先の氏名、メールアドレス、電話番号。
   * Dynamic Media アカウントの名前。
   * Dynamic Media アカウントと Experience Manager で DASH を有効にするように指定します。

1. アドビカスタマーサポートでは、リクエストが送信された順番に、DASH カスタマー待機リストに追加します。
1. リクエストを処理する準備が整った時点で、カスタマーサポートから連絡を差し上げ、DASH を有効にする日付の調整と設定を行います。
1. 完了後、カスタマーサポートから通知があります。
1. 通常通り、[ビデオビューアープリセット](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)を作成します。

## ビデオレポートの表示 {#viewing-video-reports}

>[!NOTE]
>
>ビデオレポートを使用できるのは、Dynamic Media - ハイブリッドモードを実行している場合のみです。

ビデオレポートには、指定した期間にわたるいくつかの集計指標が表示されます。ユーザーはビデオレポートを使用して、*公開済み*&#x200B;の個々のビデオやビデオの集合が期待どおりに動作しているかどうかを監視できます。次の上位指標データは、web サイト全体で公開されているすべてのビデオについて集計されます。

* ビデオ開始
* 完了率
* ビデオの平均視聴時間
* ビデオの合計視聴時間
* 訪問あたりのビデオ数

すべての&#x200B;*公開済み*&#x200B;ビデオの表も表示されるので、ビデオ開始数の合計に基づいて、web サイトで視聴された上位のビデオを追跡できます。

リストのビデオ名を選択すると、ビデオのオーディエンス保持（ドロップオフ）レポートが折れ線グラフの形式で表示されます。グラフには、ビデオの再生中の任意の時間のビュー数が表示されます。 ビデオを再生すると、縦棒はプレーヤーの時間インジケーターと同期して追跡されます。 折れ線グラフのデータの下落は、オーディエンスが興味のない場所から離脱した場所を示します。

ビデオが Adobe Experience Manager Dynamic Media 以外でエンコードされた場合、オーディエンス保持（ドロップオフ）グラフおよび表内の再生率データは利用できません。

>[!NOTE]
>
>トラッキングとレポートのデータは、Dynamic Media 独自のビデオプレーヤーと、関連するビデオプレーヤープリセットの使用にのみ基づいています。そのため、他のビデオプレーヤーを介して再生されたビデオをトラッキングしてレポートすることはできません。

デフォルトでは、ビデオレポートを最初に開いたときに、今月初めから今月の今日の日付までのビデオデータが表示されます。ただし、このデフォルトの日付範囲を上書きして、独自の日付範囲を指定することができます。次回ビデオレポートを開くと、指定した日付範囲が使用されます。

ビデオレポートの正常動作のために、Dynamic Media Cloud Services の設定時に、レポートスイート ID が自動的に作成されます。そのときに、そのレポートスイート ID がパブリッシュサーバーにプッシュされ、アセットのプレビューの際に URL のコピー機能で使用できるようになります。ただし、そのためにはパブリッシュサーバーを事前にセットアップしておく必要があります。パブリッシュサーバーがセットアップされていない場合でも、公開してビデオレポートを確認することはできます。ただし、その際には Dynamic Media クラウド設定に戻って「**[!UICONTROL OK]**」を選択する必要があります。

**ビデオレポートを表示するには：**

1. Experience Manager の左上隅にある Experience Manager ロゴを選択し、左パネルで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL ビデオレポート]**&#x200B;に移動します。
1. ビデオレポートページで、次のいずれかの操作を行います。

   * 右上隅付近にある&#x200B;**[!UICONTROL ビデオレポートを更新]**&#x200B;アイコンを選択します。「更新」を使用するのは、レポートの最終日が今日の日付である場合のみです。この機能によって、前回のレポート実行以降に発生したビデオトラッキングを確認できます。

   * 右上隅付近にある&#x200B;**[!UICONTROL 日付選択]**&#x200B;アイコンを選択します。ビデオデータを表示する開始日と終了日の範囲を指定し、「**[!UICONTROL レポートを実行]**」を選択します。

   「トップの指標」グループボックスに、サイト全体にわたるすべての公開済みビデオに関する様々な集計値が表示されます&#x200B;*。*

1. 上位の公開済みビデオを示した表で、ビデオ名を選択してビデオを再生し、そのビデオのオーディエンス保持（ドロップオフ）レポートを表示します。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## ビデオへのキャプションまたはサブタイトルの追加 {#adding-captions-to-video}

クローズドキャプションを 1 つのビデオまたはアダプティブビデオセットに追加することにより、ビデオの配信先をグローバルマーケットまで拡大できます。クローズドキャプションを追加すると、音声をダビングする必要も、異なる言語ごとにネイティブスピーカーの音声を使って再録音する必要もなくなります。ビデオは、録画された言語で再生されます。様々な言語を使う人々が音声を理解できるように、外国語の字幕が表示されます。

クローズドキャプションを使用すると、耳が聞こえない人や聞こえにくい人に対して、より高いアクセシビリティを提供できます。

>[!NOTE]
>
>使用するビデオプレーヤーがクローズドキャプションの表示に対応する必要があります。

詳しくは、[Dynamic Media のアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)を参照してください。

Dynamic Media では、キャプションファイルを JSON（JavaScript Object Notation）形式に変換できます。このように変換できるので、JSON テキストを、ビデオの完全なトランスクリプトとして表示せずに web ページに埋め込むことができます。この後、検索エンジンがコンテンツをクロールまたはインデックス作成できます。これにより、ビデオを検索しやすくなり、ビデオコンテンツの詳細がユーザーに提供されます。

URL での JSON 機能の使用について詳しくは、[静的な（画像以外の）コンテンツの提供](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html?lang=ja#image-serving-api)を参照してください。

**ビデオにキャプションまたはサブタイトルを追加するには:**

1. サードパーティのアプリケーションまたはサービスを使用して、ビデオのキャプションやサブタイトルのファイルを作成します。

   WebVTT（Web Video Text Tracks）標準に従ってファイルを作成してください。キャプションファイルの拡張子は .VTT です。WebVTT キャプション標準をよく確認してください。

   [WebVTT：Web Video Text Tracks 形式（英語）](https://w3c.github.io/webvtt/)を参照してください。

   Dynamic Media 以外でキャプションやサブタイトルのファイルの作成に使用できる、無料と有料のツールやサービスが用意されています。例えば、スタイル設定のない単純なビデオキャプションファイルを作成するには、以下の無料のオンラインキャプションオーサリング編集ツールを使用できます。

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   良い結果を得るためには、このツールを Explorer 9 以上、Google Chrome、または Safari で使用してください。

   ツールの「**[!UICONTROL ビデオファイルの URL を入力]**」フィールドにビデオファイルの URL をコピーして貼り付け、「**[!UICONTROL 読み込み]**」を選択します。[アセットの URL の取得](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照して、ビデオファイルそのものの URL を取得し、それを「**[!UICONTROL ビデオファイルの URL を入力]**」フィールドに貼り付けてください。その後、Internet Explorer、Chrome、または Safari で、ビデオを再生できます。

   ここで、サイトの画面に表示される指示に従って、WebVTT ファイルを作成して保存します。終了したら、キャプションファイルの内容をコピーし、空のテキストエディターに貼り付けて、ファイル拡張子 VTT を付けて保存します。

   >[!NOTE]
   >
   >複数言語のビデオサブタイトルを用意してグローバル対応する場合、WebVTT 標準の規定により、サポート対象の言語ごとに個別の .vtt ファイルを作成して呼び出す必要があります。

   一般に、VTT キャプションファイルの名前には、ビデオファイルと同じ名前を付けて、名前の末尾に言語ロケール（-EN、-FR、-DE など）を追加します。そうしておくと、既存の web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。

1. Experience Manager で、WebVTT キャプションファイルを DAM にアップロードします。
1. アップロードしたキャプションファイルを関連付ける、*公開済み*&#x200B;ビデオアセットに移動します。

   URL をコピーするには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。

   [アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. 次のいずれかの操作を行います。

   * ポップアップビデオビューアエクスペリエンスの場合は、「**[!UICONTROL URL]**」を選択します。URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。コピーしたビデオの URL を次の構文で追加します。

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      キャプションパスの末尾にある `,1` に注意します。パスの VTT ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それぞれ、`,1` または `,0` を設定します。

   * 埋め込みビデオビューアエクスペリエンスの場合は、「**[!UICONTROL 埋め込みコード]**」を選択します。埋め込みコードダイアログボックスで、埋め込みコードを選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。コピーした埋め込みコードを次の構文で追加します。

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      キャプションパスの末尾にある `,1` に注意します。パスの VTT ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それぞれ、`,1` または `,0` を設定します。

## ビデオへのチャプターマーカーの追加 {#adding-chapter-markers-to-video}

1 つのビデオまたはアダプティブビデオセットにチャプターマーカーを追加すると、長編ビデオの視聴と操作が簡単になります。ビデオの再生中に、ビデオタイムライン（ビデオスクラバーとも呼ばれる）のチャプターマーカーを選択することができます。これにより、ユーザーは、関心があるポイントや、新しいコンテンツ、トレーニング、デモンストレーションなどにすぐに移動できます。

>[!NOTE]
>
>ビデオプレーヤーが、チャプターマーカーの使用をサポートしている必要があります。Dynamic Media ビデオプレーヤーは、チャプターマーカーをサポートしていますが、サードパーティのビデオプレーヤーは、チャプターマーカーをサポートしているとは限りません。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

ビデオのチャプターリストを作成する方法は、キャプションを作成する方法とほとんど同じです。つまり、WebVTT ファイルを作成します。ただし、この WebVTT ファイルは、WebVTT キャプションファイルと分けておく必要があります。キャプションとチャプターを 1 つの WebVTT ファイルにまとめることはできません。

チャプターナビゲーション機能を備えた WebVTT ファイルを作成する際に使用するフォーマットの例として、次のサンプルを使用できます。

### ビデオチャプターナビゲーション機能を備えた WebVTT ファイル {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

上記の例では、`Chapter 1` はキュー識別子で、オプションです。`00:00:000 --> 01:04:364` のキュー時間は、チャプターの開始時間と終了時間を、`00:00:000` という形式で指定しています。最後の 3 桁はミリ秒で、`000` のまま残しておくこともできます。チャプタータイトルの `The bicycle store behind it all` は、チャプターの内容を示す実際の説明です。ユーザーが、タイムラインのビジュアルキューポイントにマウスポインターを置くと、キュー識別子、開始キュー時間およびチャプタータイトルが、ビデオプレーヤー内にポップアップ表示されます。

HTML5 ビデオビューアを使用するので、作成するチャプターファイルが WebVTT（Web Video Text Tracks）標準に準拠していることを確認してください。チャプターファイルの拡張子は .VTT です。WebVTT キャプション標準をよく確認してください。

[WebVTT：Web Video Text Tracks 形式（英語）](https://w3c.github.io/webvtt/)を参照してください。

**ビデオにチャプターマーカーを追加するには：**

1. この VTT ファイルを UTF8 エンコーディングで保存して、チャプタータイトルテキストの文字レンディションに関する問題を回避します。

   一般に、チャプター VTT ファイルの名前には、ビデオファイルと同じ名前を付けて、名前の末尾にチャプターを追加します。そうしておくと、既存の web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。
1. Experience Manager で、WebVTT チャプターファイルをアップロードします。

   [アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。

1. 次のいずれかの操作を行います。

   <table>
     <tbody>
      <tr>
       <td>ポップアップビデオビューアエクスペリエンスの場合</td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルを関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」を選択します。</li>
       <li>左パネルで、ビデオビューアプリセット名を選択します。ビデオのプレビューが別のページで開きます。</li>
       <li>左パネルの下部にある「<strong>URL</strong>」を選択します。</li>
       <li>URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。</li>
       <li>ビデオのコピー済み URL を次の構文で追加すると、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>埋め込みビデオビューアエクスペリエンスの場合<br /> </td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルを関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」を選択します。</li>
       <li>左パネルで、ビデオビューアプリセット名を選択します。ビデオのプレビューが別のページで開きます。</li>
       <li>左パネルの下部にある「<strong>埋め込み</strong>」を選択します。</li>
       <li>埋め込みコードダイアログボックスで、コード全体を選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。</li>
       <li>ビデオの埋め込みコードを次の構文で追加して、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to select the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, select the video asset.
1. On the toolbar, select the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Frame from video]**.
        * Select the Play button, then select the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Thumbnail from Assets]**.
        * Select **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then select **[!UICONTROL Select]**.

1. On the Change Thumbnail page, select **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, select **[!UICONTROL Save & Close]**.

-->

<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## Dynamic Media アセットの Dynamic Media URL の変更

Dynamic Media で処理されるビデオは、標準ビューアで使用できます。また、マニフェスト URL に直接アクセスし、独自のカスタムビューアを使用して再生することもできます。ビデオのマニフェスト URL を取得する API を次に示します。

### getVideoManifestURI API について

`getVideoManifestURI`API は c`q-scene7-api:com.day.cq.dam.scene7.api` を通じて公開され、次のマニフェスト URL を生成するために使用できます。

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API パラメーター

この API では、次の 3 つのパラメーターを取り込みます。

| パラメーター | 説明 |
| --- | --- |
| `resource` | Dynamic Media が取り込んだビデオに対応するリソース。 |
| `manifestType` | `ManifestType.DASH` または `ManifestType.HLS` のいずれか |
| `onlyIfPublished` | マニフェスト URI が公開され、配信層で使用できる場合にのみ生成される場合に、True に設定します。 |

上記のメソッドを使用してビデオのマニフェスト URL を取得するには、[ビデオエンコーディングプロファイル](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)を「ビデオのアップロード」フォルダーに追加します。Dynamic Media は、フォルダーに割り当てられたビデオエンコーディングファイルで見つかったエンコーディングに基づいて、これらのビデオを処理します。これで、上記の API を呼び出して、アップロードされたビデオのマニフェスト URL を取得できます。

### エラーシナリオ

エラーがある場合、API は null を返します。例外は、Experience Manager エラーログに記録されます。ログに記録されるこれらのエラーは、すべて `Could not generate Video Manifest URI` で始まります。次のシナリオでは、このようなエラーが発生する可能性があります。

* `IllegalArgumentException` は、次のいずれかに関してログに記録されます。

   * 渡された `resource` パラメーターが null である。
   * 渡された `resource` パラメーターがビデオではない。
   * 渡された `manifestType` パラメーターが null である。
   * `onlyIfPublished` パラメーターは true として渡されたものの、ビデオが公開されていない。
   * Dynamic Media のアダプティブビデオセットを使用してビデオが取り込まれていない。

* `IOException` は、Dynamic Media への接続で問題が発生した場合にログに記録されます。
* 渡された `manifestType` パラメーターが `ManifestType.DASH` であるにもかかわらず、ビデオが DASH 形式で処理されていない場合、`UnsupportedOperationException` はログに記録されます。

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->





