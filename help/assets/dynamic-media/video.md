---
title: Dynamic Media のビデオ
description: Dynamic Media でビデオを使用する方法について説明します。ビデオのエンコード、YouTube へのビデオの公開、ビデオレポートの表示、クローズドキャプション、チャプターマーカーのビデオへの追加に関するベストプラクティスをレビューします。
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '10063'
ht-degree: 99%

---

# ビデオ {#video}

この節では、Dynamic Media でのビデオの操作について説明します。

## クイックスタート：ビデオ {#quick-start-videos}

次のワークフローの手順説明は、Dynamic Media でアダプティブビデオセットをすぐに使い始めることを目的としたものです。各手順に続いて、詳しい説明のあるトピックの見出しへのリンクが記載されています。

>[!NOTE]
>
>Dynamic Media のビデオを操作する前に、Adobe Experience Manager の管理者が既に Dynamic Media Cloud Services を有効にして設定を完了していることを確認してください。
>
>* Dynamic Media 設定の [Dynamic Media Cloud Services の設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)、および [Dynamic Media のトラブルシューティング](/help/assets/dynamic-media/troubleshoot-dm.md)を参照してください。
>

1. 次の手順を実行して、**Dynamic Media ビデオをアップロード**&#x200B;します。

   * 独自のビデオエンコーディングプロファイルを作成します。または、ダイナミックメディアに付属する、事前定義済みの「_アダプティブビデオエンコーディング_」プロファイルを使用します。

      * [ビデオエンコーディングプロファイルを作成します](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 出力ビデオエンコーディングの最大解像度は、8,192 × 4,320 または 4,320 × 8,192.md です。
      * 詳しくは、[ビデオエンコーディングのベストプラクティス](#best-practices-for-encoding-videos)を参照してください。

   * ビデオ処理プロファイルを、プライマリソースビデオのアップロード先となる 1 つ以上のフォルダーに関連付けます。

      * [ビデオプロファイルをフォルダーに適用します](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。
      * 詳しくは、[デジタルアセットの整理](/help/assets/organize-assets.md)を参照してください。

   * 指定フォルダーにプライマリソースビデオをアップロードします。追加したビデオは、そのフォルダーに割り当てたビデオ処理プロファイルに従ってエンコードされます。

      * Dynamic Media は主に、最大 30 分、最小解像度が 25 x 25 を超える短時間のビデオをサポートします。
      * サポートされる入力ビデオの最大解像度は 16,384 × 16,384 です。
      * 15 GB までのビデオファイルをアップロードできます。
      * [ビデオをアップロードします](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。
      * 詳しくは、[サポートされる入力ファイル形式](/help/assets/file-format-support.md)を参照してください。

   * アセットまたはワークフロー表示から、[ビデオエンコードの進行状況](#monitoring-video-encoding-and-youtube-publishing-progress)を監視します。

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

      * タイトル、説明、タグ、カスタムメタデータフィールドなど、ビデオのプロパティを編集します。
        [ビデオのプロパティを編集します](/help/assets/manage-digital-assets.md#editing-properties)。

      * [デジタルアセットのメタデータの管理](/help/assets/manage-metadata.md)
      * [メタデータスキーマ](/help/assets/metadata-schemas.md)

   * ビデオをレビューおよび承認し、注釈を付け、完全なバージョン管理を維持します。

      * [ビデオの注釈](/help/assets/manage-video-assets.md#annotate-video-assets)または[アセットの注釈](/help/assets/manage-digital-assets.md#annotating)

      * [バージョンを作成](/help/assets/manage-digital-assets.md#asset-versioning)
      * [アセットでのワークフローの開始](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [フォルダーのアセットのレビュー](/help/assets/bulk-approval.md)
      * [プロジェクト](/help/sites-cloud/authoring/projects/overview.md)

1. 次のいずれかの操作を行って、**Dynamic Media ビデオを公開します**。

   * Adobe Experience Manager を WCM（web コンテンツ管理）システムとして使用する場合、web ページにビデオを直接追加できます。

      * [Web ページにビデオを追加します](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

   * サードパーティの WCM システムを使用している場合、web ページにビデオをリンクするか、ビデオを埋め込むことができます。

      * URL を使用したビデオの統合：
        [Web アプリケーションに URL をリンクします](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)。

      * Web ページの埋め込みコードを使用したビデオの統合：
        [Web ページにビデオビューアを埋め込みます](/help/assets/dynamic-media/embed-code.md)。

   * [ビデオレポートを生成します](#viewing-video-reports)。

   * [ビデオに複数のキャプションとオーディオトラックを追加します](#about-msma)。

## Dynamic Media でのビデオの操作 {#working-with-video-in-dynamic-media}

Dynamic Media のビデオは、高品質のアダプティブビデオを簡単に公開して、デスクトップ、タブレット、モバイルデバイスを含む複数の画面にストリーミングするエンドツーエンドのソリューションです。アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップコンピューターまたはモバイルデバイスが、使用可能な帯域幅を検出します。

例えば、iOS モバイルデバイスでは、3G、4G、Wi-Fi などの帯域幅が検出されます。次に、アダプティブビデオセット内の様々なビデオビットレートの中から、適切なエンコード済みビデオが自動的に選択されます。ビデオはデスクトップ、モバイルデバイスまたはタブレットにストリーミングされます。

また、デスクトップまたはモバイルデバイスでネットワークの状態が変化した場合は、ビデオ画質が自動的に動的に切り替わります。また、顧客がデスクトップで全画面表示モードに入ると、アダプティブビデオセットはより高い解像度を使用して顧客の視聴エクスペリエンスを向上させるよう対応します。アダプティブビデオセットを使用すると、Dynamic Media ビデオを複数の画面とデバイスで再生する顧客にとって最適な視聴エクスペリエンスが提供されます。

再生または再生時に選択するエンコード済みビデオの決定に、ビデオプレーヤーが使用するロジックは、次のアルゴリズムに基づきます。

1. ビデオプレーヤーは、プレーヤー自体の「初期ビットレート」に設定されている値に最も近いビットレートで、初期ビデオフラグメントを読み込みます。
1. ビデオプレーヤーは、帯域幅の速度の変化に応じて、次の条件に従って切り替わります。

   1. プレーヤーは、見積もり帯域幅を超えない範囲内で、最も高い帯域幅でのストリームを選択します。
   1. プレーヤーは、使用可能な帯域幅の 80％ほどを見積もります。ただし、使用可能な帯域幅が上昇した場合は、帯域幅を大きく見積もりすぎてすぐに元の帯域幅に戻ることを防ぐために、より控えめな 70％ほどの見積もりとなります。

アルゴリズムの技術情報について詳しくは、[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp) を参照してください。

単一のビデオとアダプティブビデオセットを管理する際、次の機能がサポートされています。

* 多数のサポートされているビデオ形式およびオーディオ形式からビデオをアップロードする。複数の画面で再生できるようにビデオを MP4 H.264 形式にエンコーディングする。事前定義済みのアダプティブビデオセット、1 つのビデオのエンコーディングプリセットを使用するか、独自のエンコーディングをカスタマイズしてビデオの品質とサイズを制御できます。

   * 生成されるアダプティブビデオセットには、MP4 ビデオが含まれます。
   * **注意**：プライマリ／ソースビデオはアダプティブビデオセットには追加されません。

* すべての HTML5 ビデオビューアでのビデオキャプション。
* ビデオアセットを効率的に管理するための完全なメタデータサポートを使用して、ビデオを整理、参照および検索します。
* アダプティブビデオセットを web およびデスクトップ、タブレット、モバイルデバイスに配信します。

アダプティブビデオのストリーミングは、各種 iOS プラットフォームでサポートされています。詳しくは、[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference)を参照してください。

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Dynamic Media ビデオビューアプリセットを使用してビデオを再生します。このビューアプリセットには、次のビューアが含まれます。

   * 単一のビデオビューア。
   * ビデオコンテンツと画像コンテンツの両方を組み合わせた混在メディアビューア。

* 自社ブランドのニーズに合わせてビデオプレーヤーを設定します。
* 単純な URL か埋め込みコードを使用して、ビデオを web サイト、モバイルサイトまたはモバイルアプリケーションに統合します。

<!-- GIVES a 404 See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources)の [Experience Manager Assets および Dynamic Media Classic のビューア](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc)および [Experience Manager Assets 専用のビューア](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only)も参照してください。

## ベストプラクティス：HTML5 ビデオビューアの使用 {#best-practice-using-the-html-video-viewer}

Dynamic Media の HTML5 ビデオビューアプリセットは堅牢なビデオプレーヤーです。このプリセットを使用すれば、HTML5 ビデオ再生でよくある問題や、モバイルデバイスに関する問題の多くを回避できます。例えば、アダプティブビットレートストリーミング配信機能がなかったり、デスクトップブラウザーの範囲が限定されていたりすることなどです。

プレーヤーの設計面では、標準の web 開発ツールを使用してビデオプレーヤーの機能を設計できます。例えば、HTML5 と CSS を使用して、ボタン、コントロールおよびカスタムのポスター画像背景をデザインすることにより、カスタマイズした表示で顧客にリーチすることができます。

ビューアの再生側では、ブラウザーのビデオ機能を自動的に検出します。その後、HLS または DASH（アダプティブビデオストリーミングとも呼ばれる）を使用してビデオを配信します。または、これらの配信方法が使用できない場合は、HTML5 プログレッシブが代わりに使用されます。

HTML5 と CSS を使用して再生コンポーネントを設計できる機能を 1 つのプレーヤーに統合できます。埋め込み再生が可能で、ブラウザーの機能に応じてアダプティブストリーミングやプログレッシブストリーミングを使用できます。すべてのこの機能により、リッチメディアコンテンツの配信範囲をデスクトップユーザーとモバイルユーザーの両方に拡大し、ビデオエクスペリエンスを確実に効率化できます。

[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources)の [Experience Manager Assets 専用のビューア](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only)も参照してください。


### HTML5 ビデオビューアを使用した、デスクトップコンピューターおよびモバイルデバイス上でのビデオ再生 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

デスクトップおよびモバイルへのアダプティブビデオストリーミングの場合、ビットレートの切り替えに使用されるビデオは、アダプティブビデオセット内のすべての MP4 ビデオに基づいています。

ビデオの再生は、HLS または DASH、またはプログレッシブビデオダウンロードのいずれかを使用して行われます。6.0、6.1、6.2 など以前の Experience Manager バージョンでは、ビデオは HTTP 上でストリーミングされました。

一方、Experience Manager 6.3 以降では、DM ゲートウェイサービスの URL も常に HTTPS を使用するため、ビデオは HTTPS（つまり、HLS または DASH）でストリーミングされるようになりました。このデフォルトの動作はユーザーに影響しません。ブラウザーでサポートしている場合、ビデオストリーミングは常に HTTPS 上で行われます。次の表を参照してください。

したがって、次のようになります。

* HTTPS web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しています。
* HTTP web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しており、web ブラウザーから混合コンテンツに関する問題は発生しません。

DASH は国際標準であり、HLS は Apple の標準です。どちらもアダプティブビデオストリーミングに使用されます。どちらのテクノロジーも、ネットワーク帯域幅の容量に基づいて再生を自動的に調整します。また、HLS では、ビデオの残りがダウンロードされるまで待たなくても、ビデオ内の任意のポイントを「シーク」できます。

プログレッシブビデオは、ユーザーのデスクトップシステムやモバイルデバイスにダウンロードしてローカルに保存することで配信されます。

デバイス、ブラウザー、およびデスクトップコンピューターやモバイルデバイスでの [Dynamic Media HTML5 ビデオビューア](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video#interactive-video)によるビデオの再生方法を次の表に示します。

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
   <td>Windows® 8 および Windows® 10 では、DASH または HLS が要求されるたびに HTTPS を強制的に使用します。既知の制約事項：DASH または HLS の HTTP は、このブラウザーとオペレーティング システムの組み合わせでは機能しません<br /> <br /> Windows® 7 の場合 - プログレッシブダウンロード。HTTP プロトコルと HTTPS プロトコルに標準のロジックを使用します。</td>
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

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Dynamic Media ビデオソリューションのアーキテクチャ {#architecture-of-dynamic-media-video-solution}

次の図に、アップロード後、（Dynamic Media ハイブリッドモードの）DMGateway によってエンコードされ、公開されるビデオのオーサリングワークフローの全体像を示します。

![chlimage_1-427](assets/chlimage_1-427.png)

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## ビデオエンコーディングのベストプラクティス {#best-practices-for-encoding-videos}

Dynamic Media を有効にし、ビデオクラウドサービスを設定済みの場合、**Dynamic Media エンコードビデオ**&#x200B;ワークフローがビデオをエンコードします。このワークフローは、ワークフローの処理履歴とエラー情報を取り込みます。Dynamic Media を有効にし、ビデオクラウドサービスを設定済みの場合、ビデオをアップロードすると、**[!UICONTROL Dynamic Media エンコードビデオ]**&#x200B;ワークフローが自動的に有効になります。（Dynamic Media を使用していない場合は、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローが有効になります）。

ここでは、ソースビデオファイルのエンコードにおけるベストプラクティスのヒントを説明します。

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_jp).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_jp). -->

### ソースビデオファイル {#source-video-files}

ビデオファイルをエンコードする場合は、可能な限り高品質のソースビデオファイルを使用します。以前にエンコードされたビデオファイルの使用は避けてください。そのようなファイルは既に圧縮済みで、さらにエンコードすると標準を下回る品質のビデオが作成されるからです。

* Dynamic Media は主に、最大 30 分、最小解像度が 25 x 25 を超える短時間のビデオをサポートします。
* 15 GB までのプライマリソースビデオファイルをアップロードできます。

次の表に、ソースビデオファイルのエンコード前の推奨サイズ、縦横比および最小ビットレートを示します。

| サイズ | 縦横比 | 最小ビットレート |
|--- |--- |--- |
| 1,024 x 768 | 4:3 | 4,500 kbps（ほとんどのビデオ） |
| 1,280 x 720 | 16:9 | 3,000～6,000 kbps（ビデオ内のモーションの量に応じて調整） |
| 1,920 x 1,080 | 16:9 | 6,000～8,000 kbps（ビデオ内のモーションの量に応じて調整） |

### ファイルのメタデータの取得 {#obtaining-a-file-s-metadata}

ファイルのメタデータは、ビデオ編集ツールを使用してメタデータを表示するか、メタデータを取得するために設計されたアプリケーションを使用して取得できます。以下は、サードパーティアプリケーションの MediaInfo を使用してビデオファイルのメタデータを取得する手順です。

1. [MediaInfo のダウンロードページ](https://mediaarea.net/ja/MediaInfo/Download)に移動します。
1. GUI バージョンのインストーラーを選択してダウンロードし、インストール手順に従って操作します。
1. インストールの完了後、ビデオファイルを右クリックして（Windows® のみ）MediaInfo を選択するか、MediaInfo を開いてビデオファイルをアプリケーションにドラッグします。ビデオの幅、高さ、fps など、ビデオファイルに関連するすべてのメタデータが表示されます。

### 縦横比 {#aspect-ratio}

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択または作成するときには、同じ縦横比をプリセットに使用してください。このアプローチにより、プライマリソースビデオファイルとの一貫性が確保されます。縦横比とは、ビデオの高さに対する幅の比率のことです。

ビデオファイルの縦横比を求めるには、ファイルのメタデータを取得します。ファイルの幅と高さを記録します（前述のファイルのメタデータの取得を参照）。その後、次の式を使用して縦横比を計算します。

幅/高さ = 縦横比

次の表に、この式の解を一般的な縦横比に変換した結果を示します。

| 数式の結果 | 縦横比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例えば、幅 1,440、高さ 1,080×ビデオの縦横比は 1,440/1,080 （1.33）になります。この場合、縦横比が 4 :3 のビデオエンコーディングプリセットを選択して、ビデオファイルをエンコードします。

### ビットレート {#bitrate}

ビットレートとは、1 秒間のビデオ再生を構成するエンコードされたデータの量です。ビットレートは、1 秒あたりのキロビット数（Kbps）の単位で測定します。

>[!NOTE]
>
>すべてのコーデックは非可逆圧縮を使用するので、ビットレートはビデオ画質の最も重要な要素となります。非可逆圧縮では、ビデオファイルを圧縮するほど画質が低下します。したがって、他の特性（解像度、フレームレートおよびコーデック）がすべて等しい場合は、ビットレートが低いほど、圧縮ファイルの品質は低下します。

ビットレートエンコーディングは 2 種類あり、そのどちらかを選択できます。

* **[!UICONTROL 固定ビットレートエンコーディング]**（CBR）- CBR エンコーディングでは、ビットレートまたは 1 秒あたりのビット数が、エンコーディングプロセス全体で同じ数値に維持されます。CBR エンコーディングでは、設定されているデータレートが、ビデオ全体での設定値として使用されます。また、CBR エンコーディングでは、メディアファイルの品質は最適化されませんが、その分、空き容量の節約になります。ビデオ全体に同じようなモーションレベルが含まれている場合は、CBR を使用します。CBR は、ビデオコンテンツのストリーミングに最も一般的に使用されています。[カスタムで追加するビデオエンコーディングパラメーターの使用](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters)も参照してください。

* **[!UICONTROL 可変ビットレートエンコーディング]**（VBR）- VBR エンコーディングでは、コンプレッサーで必要となるデータに基づいて、設定したデータレートが下限から上限の範囲内で調整されます。つまり、VBR エンコーディングプロセスでは、メディアファイルのビットレートが、そのニーズに応じて動的に増減します。
VBR は、CBR よりエンコードに時間がかかりますが、生成されるメディアファイルは最高品質となります。VBR は、ビデオコンテンツの HTTP プログレッシブ配信に最も一般的に使用されます。

VBR と CRB のどちらを使用するべきかVBR と CBR のどちらを選択すべきかと言えば、ほとんどの場合、メディアファイルには VBR を使用することをお勧めします。VBR は、優位性のあるビットレートで CBR より高品質のファイルを生成します。VBR を使用するときは、2 パスエンコーディングを使用し、最大ビットレートをターゲットビデオのビットレートの 1.5 倍に設定してください。

ビデオエンコーディングプリセットを選択するときは、ターゲットユーザーの接続速度を考慮してください。その速度の 80%のデータレートを持つプリセットを選択します。例えば、ターゲットユーザーの接続速度が 1,000 Kbps の場合、ビデオデータレートが 800 Kbps のプリセットが最適です。

次の表に、一般的な接続速度のデータレートを示します。

| 速度（Kbps） | 接続タイプ |
|--- |--- |
| 256 | ダイヤルアップ接続。 |
| 800 | 一般的なモバイル接続。この接続では、3G エクスペリエンス向けに 400～800 の範囲のデータレートがターゲットとなります。 |
| 2,000 | 一般的なブロードバンドデスクトップ接続。この接続では、800～2,000 Kbps の範囲のデータレートがターゲットとなります。大部分のターゲットは、平均 1,200～1,500 Kbps です。 |
| 5,000 | 一般的な高ブロードバンド接続。ほとんどの消費者は、この速度でのビデオ配信を使用できないので、この上限範囲でのエンコーディングはお勧めしません。 |

### 解像度 {#resolution}

**解像度**&#x200B;は、ビデオファイルの高さと幅をピクセル単位で表します。ほとんどのソースビデオは、高解像度（例：1,920 × 1,080）で保存されます。ストリーミング目的では、ソースビデオはより低い解像度（640 × 480 以下）に圧縮されます。

解像度とデータレートは、ビデオ画質を決定する統合的な 2 つの要素です。同じビデオ画質を維持するには、ビデオファイルのピクセル数が多いほど（解像度が高いほど）、データレートを高くする必要があります。例えば、解像度 320 x 240 と 640 x 480 のビデオファイルで、フレームあたりのピクセル数を考えてみましょう。

| 解像度 | フレームあたりピクセル数 |
|--- |--- |
| 320 × 240 | 76,800 |
| 640 × 480 | 307,200 |

640 x 480 ファイルのピクセル数は、フレームあたり 4 倍になります。この 2 つの解像度の例でデータレートを同じにするには、640 x 480 ファイルを 4 倍に圧縮します。これにより、ビデオの画質が低下する可能性があります。そのため、250 kbps のビデオデータレートの場合、320 x 240 の解像度では高画質になりますが、640 x 480 の解像度では高画質になりません。

一般に、高いデータレートを使用するほど、ビデオの画質は良くなり、高い解像度を使用するほど、その画質を維持するために必要になるデータレートも（解像度が低い場合と比較して）増加します。

解像度とデータレートには関連があるので、ビデオをエンコードする際には次の 2 つの方法から選択できます。

* データレートを選択してから、選択したデータレートできれいに表示される最高の解像度でエンコードします。
* 解像度を選択してから、選択した解像度で高品質のビデオを配信するために必要になるデータレートでエンコードします。

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択（または作成）する場合は、次の表を使用して正しい解像度をターゲットにします。

| 解像度 | 高さ（ピクセル） | 画面サイズ |
|--- |--- |--- |
| 240p | 240 | ごく小さな画面 |
| 300p | 300 | 小型の画面（一般にモバイルデバイス用） |
| 360p | 360 | 小型の画面 |
| 480p | 480 | 中型の画面 |
| 720p | 720 | 大型の画面 |
| 1080p | 1080 | 高画質の大型の画面 |

サポートされる入力ビデオの最大解像度は 16,384 × 16,384 です。出力ビデオエンコーディングの最大解像度は、8,192 × 4,320 または 4,320 × 8,192 です。

### fps（1 秒あたりのフレーム数） {#fps-frames-per-second}

米国と日本では、ほとんどのビデオが 29.97 fps で撮影されます。ヨーロッパでは、ほとんどのビデオが 25 fps で撮影されます。映画は 24 fps で撮影されます。

プライマリソースビデオファイルの fps レートに一致するビデオエンコーディングプリセットを選択します。例えば、プライマリソースビデオが 25 fps の場合は、25 fps のエンコーディングプリセットを選択します。デフォルトでは、すべてのカスタムエンコーディングでプライマリソースビデオファイルの fps が使用されます。そのため、ビデオエンコーディングプリセットを作成するときに、fps 設定を明示的に指定する必要はありません。

### ビデオエンコーディングのサイズ {#video-encoding-dimensions}

最適な結果を得るには、ソースビデオがエンコードされたすべてのビデオの整数倍になるようにエンコーディングのサイズを選択します。

この比率を計算するには、ソースの幅をエンコードされた幅で割って、幅の比率を求めます。次に、ソースの高さをエンコードの高さで割って高さの比率を求めます。

結果の比率が整数の場合、ビデオは最適に拡大／縮小されます。結果の比率が整数でない場合は、余ったピクセルのアーティファクトがディスプレイに残るので、ビデオの画質に影響します。この影響は、ビデオにテキストが含まれる場合に特に目立ちます。

例えば、ソースビデオが 1,920 x 1,080 だとします。次の表では、エンコードされた 3 つのビデオで使用する、最適なエンコード設定を示しています。

| ビデオタイプ | 幅 × 高さ | 幅の比率 | 高さの比率 |
|--- |--- |--- |--- |
| ソース | 1,920 x 1,080 | 1 | 1 |
| エンコード済み | 960 × 540 | 2 | 2 |
| エンコード済み | 640 × 360 | 3 | 3 |
| エンコード済み | 480 × 270 | 4 | 4 |

### エンコードされたビデオのファイル形式 {#encoded-video-file-format}

Dynamic Media では、MP4 H.264 ビデオエンコーディングプリセットの使用をお勧めします。MP4 ファイルでは H.264 ビデオコーデックが使用されるので、高品質のビデオを圧縮されたファイルサイズで作成できます。

## ビデオレポートの表示 {#viewing-video-reports}

>[!NOTE]
>
>ビデオレポートを使用できるのは、Dynamic Media - ハイブリッドモードを実行している場合のみです。

ビデオレポートには、指定した期間にわたるいくつかの集計指標が表示されます。ユーザーはビデオレポートを使用して、*公開済み*&#x200B;の個々のビデオやビデオの集合が期待どおりに動作しているかどうかを監視できます。次の上位指標データは、web サイト全体で公開されているすべてのビデオについて集計されます。

* ビデオ開始
* 完了率
* ビデオの平均視聴時間
* ビデオの合計視聴時間
* 訪問別ビデオ数

すべての&#x200B;*公開済み*&#x200B;ビデオの表も表示されるので、ビデオ開始数の合計に基づいて、web サイトで視聴された上位のビデオを追跡できます。

リストのビデオ名を選択すると、ビデオのオーディエンス保持（ドロップオフ）レポートが折れ線グラフの形式で表示されます。グラフには、ビデオの再生中の任意の時間のビュー数が表示されます。ビデオを再生すると、プレーヤーの時間インジケーターと同期して縦棒が表示されます。この折れ線グラフのデータが急激に下降するところは、オーディエンスが関心をなくして再生を終了したところです。

ビデオが Adobe Experience Manager Dynamic Media 以外でエンコードされた場合、オーディエンス保持（ドロップオフ）グラフおよび表内の再生率データは利用できません。

>[!NOTE]
>
>トラッキングとレポートのデータは、Dynamic Media 独自のビデオプレーヤーと、関連するビデオプレーヤープリセットの使用にのみ基づいています。そのため、他のビデオプレーヤーで再生されたビデオをトラッキングしてレポートすることはできません。

デフォルトでは、ビデオレポートを最初に開いたときに、今月初めから今月の今日の日付までのビデオデータが表示されます。ただし、独自の日付範囲を指定して、デフォルトの日付範囲を上書きすることができます。次回ビデオレポートを開くと、指定した日付範囲が使用されます。

ビデオレポートの正常動作のために、Dynamic Media クラウドサービスの設定時に、レポートスイート ID が自動的に作成されます。そのときに、そのレポートスイート ID がパブリッシュサーバーにプッシュされ、アセットのプレビューの際に URL のコピー機能で使用できるようになります。ただし、そのためにはパブリッシュサーバーを事前にセットアップしておく必要があります。パブリッシュサーバーがセットアップされていない場合でも、公開してビデオレポートを確認することはできます。ただし、その際には Dynamic Media クラウド設定に戻って「**[!UICONTROL OK]**」を選択する必要があります。

**ビデオレポートを表示するには：**

1. Experience Manager の左上隅にある Experience Manager ロゴを選択します。左パネルで、![ハンマーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg)／**[!UICONTROL アセット]**／**[!UICONTROL ビデオレポート]**&#x200B;をクリックします。
1. ビデオレポートページで、次のいずれかの操作を行います。

   * 右上隅付近にある&#x200B;**[!UICONTROL ビデオレポートを更新]**&#x200B;アイコンを選択します。「更新」を使用するのは、レポートの終了日が今日の日付である場合のみです。この機能によって、前回のレポート実行以降に発生したビデオトラッキングを確認できます。

   * 右上隅付近にある&#x200B;**[!UICONTROL 日付選択]**&#x200B;アイコンを選択します。ビデオデータを表示する開始日と終了日の範囲を指定し、「**[!UICONTROL レポートを実行]**」を選択します。

   「トップの指標」グループボックスに、サイト全体にわたるすべての公開済みビデオに関する様々な集計値が表示されます&#x200B;*。*

1. 上位の公開済みビデオを示した表で、ビデオ名を選択してビデオを再生し、そのビデオのオーディエンス保持（ドロップオフ）レポートを表示します。

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html?lang=ja).

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

## Dynamic Media におけるビデオの複数のキャプションとオーディオトラックのサポートについて{#about-msma}

Dynamic Media で複数のキャプションとオーディオトラック機能を使用すると、複数のオーディオトラックを簡単に追加できます。また、独自の `.vtt`（ビデオテキストトラック）ファイルまたは AI 生成のキャプションファイルを使用して、複数のキャプションファイルを追加することもできます。Dynamic Media の AI 生成キャプションは、正確で同期された字幕を自動的に生成し、ビデオのアクセシビリティとエンゲージメントを向上させるように設計されています。このテクノロジーは、高度な AI アルゴリズムを使用して、音声コンテンツをテキストに文字起こしして、ビデオにキャプションとして表示します。このテクノロジーの主な機能には、次のものが含まれます。

* **自動トランスクリプション：** AI システムは、音声の単語をリアルタイムでテキストに文字起こしするので、キャプションを迅速かつ正確に生成できます。
* **多言語サポート：**&#x200B;キャプションは、60 以上の言語で自動的に配信できるので、世界中のオーディエンスに簡単に到達できます。
* **アクセシビリティの向上：**&#x200B;キャプションを提供すると、聴覚障害のある視聴者や、サウンドをオフにしてビデオを視聴したい人びとにとって、ビデオへのアクセスが向上します。
* **エンゲージメントの向上：**&#x200B;キャプションは、特にノイズの多い環境や、視聴者の母国語がビデオの言語と異なる場合に、視聴者の注意を引き、理解を向上させるのに役立ちます。

これらの機能があることで、AI を活用したキャプションは、ビデオコンテンツのアクセシビリティとエンゲージメントの向上を目指すコンテンツクリエーターにとって価値のあるツールになります。

![Dynamic Media の「キャプションとオーディオトラック」タブと、アップロードされた .VTT キャプションファイルおよびビデオ用にアップロードされた .MP3 オーディオトラックファイルを示すテーブル。](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)

プライマリビデオに複数のキャプションとオーディオトラックを追加する際に考慮するユースケースとしては、次のようなものがあります。

| タイプ | ユースケース |
|--- |--- |
| **キャプション** | 複数言語のサポート |
|  | アクセシビリティ用代替テキスト |
| **オーディオトラック** | 複数言語のサポート |
|  | 解説トラック |
|  | 説明オーディオ |

[Dynamic Media でサポートされているすべてのビデオ形式](/help/assets/file-format-support.md)とすべての Dynamic Media ビデオビューア（Dynamic Media *Video_360* ビューアを除く）は、複数のキャプションとオーディオトラックでの使用がサポートされています。

### ビデオに複数のキャプションとオーディオトラックを追加 {#add-msma}

ビデオに複数のキャプションとオーディオトラックを追加する前に、次を確認しておく必要があります。

* Dynamic Media が AEM 環境で設定されている。
* [Dynamic Media ビデオプロファイルが、ビデオが取り込まれるフォルダーに適用されている](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

追加されたキャプションでサポートされる形式は、WebVTT および AdobeVTT 形式です。また、追加されたオーディオトラックファイルでサポートされる形式は、MP3 形式です。

>[!IMPORTANT]
>
>Dynamic Media アカウントで複数のキャプション／オーディオトラックのサポートまたは AI 生成キャプションを有効にする&#x200B;*前*&#x200B;にアップロードしたビデオについては、[再処理する必要があります](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)。この再処理の手順により、これらのビデオで複数のキャプション／オーディオトラックと AI 生成キャプション機能を使用できます。再処理後も、ビデオ URL は引き続き通常どおり機能し、再生されます。

**ビデオに複数のキャプションとオーディオトラックを追加するには：**

1. 既にビデオプロファイルが割り当てられている[フォルダーにプライマリビデオをアップロード](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)します。
1. 複数のキャプションおよびオーディオトラックを追加する、アップロード済みビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
   ![ビデオのサムネール画像の上にチェックマークが付いている、選択したビデオアセットと、ツールバーでハイライト表示されている「プロパティを表示」。](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*カード表示で選択したビデオアセット。*
1. ビデオのプロパティページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。

   >[!TIP]
   >「**[!UICONTROL キャプションとオーディオトラック]**」タブが表示されない場合、次の 2 つのいずれかを意味します。
   >
   >* 選択したビデオが存在するフォルダーには、ビデオプロファイルが割り当てられていません。その場合は、[フォルダーへのビデオプロファイルの適用](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)を参照してください。
   >* または、Dynamic Media でビデオを再処理する必要があります。その場合は、[フォルダー内の Dynamic Media アセットの再処理](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)を参照してください。
   >
   >上記のいずれかのタスクを完了したら、次の手順に戻ります。

   ![プロパティページの「キャプションとオーディオトラック」タブ。](/help/assets/dynamic-media/assets/msma-audiotracks.png)
   *ビデオのプロパティページの「キャプションとオーディオトラック」タブ。*

1. ビデオに 1 つまたは複数のオーディオトラックを追加するには、次の手順を実行します。
   1. 「**[!UICONTROL オーディオトラックをアップロード]**」を選択します。
   1. 1 つまたは複数の .mp3 ファイルに移動して選択し、開きます。
   1. メディアプレーヤーの&#x200B;**[!UICONTROL オーディオまたはキャプションを選択]**&#x200B;ポップアップリストでオーディオトラックを表示するには、各オーディオトラックファイルに関する必要な詳細を追加することが必要です。これにより、すべてのオーディオトラックが適切にリストされ、アクセスできます。オーディオトラックのファイル名の右側にある ![描画アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) をクリックします。**オーディオトラックを編集**&#x200B;ダイアログボックスで、次の必要な詳細情報を入力します。

      | オーディオトラックメタデータ | 説明 |
      |--- |--- |
      | ファイル名 | デフォルトのファイル名は、元のファイル名から派生します。ファイル名はアップロード時にのみ変更でき、後で変更することはできません。ファイル名の文字数の要件は、AEM Assets と同じです。<br>追加のオーディオトラックファイルやキャプションファイルに同じファイル名を使用することはできません。 |
      | 言語 | オーディオトラックの正しい言語を選択します。 |
      | タイプ | 使用するオーディオトラックのタイプを選択します。<br>**オリジナル** - 元々ビデオに添付されていたオーディオトラック。ラベルには `[Original]` と表示され、デフォルトで `English` 言語が選択されています。**[!UICONTROL オーディオトラックを編集]**&#x200B;ダイアログボックスで&#x200B;**[!UICONTROL ラベル]**&#x200B;と&#x200B;**[!UICONTROL 言語]**&#x200B;は変更できますが、プライマリビデオが再処理されていると、デフォルトは元の値になります。<br>**標準** - 元の言語以外の言語のアドオンオーディオトラック。<br>**オーディオの説明** - ビデオ内の非言語的動作やジェスチャーの記述的ナレーションも含まれるオーディオトラック。視覚障害のあるユーザー向けのコンテンツアクセシビリティを高めます。 |
      | ラベル | オーディオトラックの名前として、メディアプレーヤーの&#x200B;**[!UICONTROL オーディオまたはキャプションを選択]**&#x200B;ポップアップリストに表示されるテキスト。ラベルは、オーディオトラックに対応する顧客に表示される内容です。例えば、`English [Original]` などです。ビデオに添付されるオーディオのラベルは、デフォルトでは `[Original]` に設定されます。 |

      必要に応じて、後でこのオーディオトラックメタデータを変更または編集できます。 ビデオが公開されると、これらの詳細は、公開中のビデオの公開 URL に反映されます。

   1. ページの右上隅付近にある&#x200B;**[!UICONTROL 保存して閉じる]**&#x200B;ドロップダウンで、「**[!UICONTROL 保存]**」をクリックします。
   1. 次のいずれかの操作を行います。
      * アップロードした各オーディオトラックファイルに対して、この手順を繰り返します。
      * 次の手順に進み、ビデオにキャプションを追加します。

1. ビデオに 1 つ以上のキャプションファイルを追加するには、シナリオに最も適した次のユースケースのいずれかを選択します。

   |  | ユースケース | 使用する「キャプションを作成」オプション |
   | --- | --- | --- |
   | **オプション 1** | 独自の既存キャプションファイル（自分が使用する言語のもの）がある場合。<br>以下の&#x200B;**オプション 1** を参照してください。 | **[!UICONTROL ファイルをアップロード]** |
   | **オプション 2** | AI で、複数の言語でキャプションファイルを生成したい場合。<br>以下の&#x200B;**オプション 2** を参照してください。 | **[!UICONTROL オーディオトラックを変換]** |
   | **オプション 3** | キャプションファイル（`.vtt`）内のテキストを修正し、再度アップロードして古い `.vtt` ファイルを置き換えてから、修正したファイルを AI で翻訳する場合。<br>以下の&#x200B;**オプション 3** を参照してください。 | **[!UICONTROL キャプションを翻訳]** |

   ![「キャプションを作成」オプション。](/help/assets/dynamic-media/assets/msma-createcaption.png)
   *キャプションを作成ドロップダウンメニューには、「ファイルをアップロード」、「オーディオトラックを変換」、「キャプションを翻訳」の 3 つのオプションがあります。*

   +++**オプション 1：***使用する言語の既存の独自のキャプションファイルを自分で用意します*（「**[!UICONTROL ファイルをアップロード]**」オプション）

   1. ページの右上付近で、**[!UICONTROL キャプションを作成]**／**[!UICONTROL ファイルをアップロード]**&#x200B;をクリックします。
   1. 1 つまたは複数の既存の `.vtt` ファイルに移動して選択し、開きます。
   1. キャプションをメディアプレーヤーに表示するには、アップロードした&#x200B;*各*&#x200B;キャプションファイルに関する必要な詳細を追加することが&#x200B;*必要*&#x200B;です。キャプションファイル名の右側にある ![描画アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) をクリックします。**キャプションを編集**&#x200B;ダイアログボックスで、次の必要なファイルの詳細情報を入力します。

      | キャプションメタデータ | 説明 |
      |--- |--- |
      | ファイル名 | デフォルトのファイル名は、元のファイル名から派生します。ファイル名はアップロード時にのみ変更でき、後で変更することはできません。ファイル名の文字数の要件は、AEM Assets と同じです。<br>追加のキャプションファイルとオーディオトラックファイルに同じファイル名を使用することはできません。 |
      | 言語 | キャプションの言語を選択します。キャプションファイルを処理すると、この言語フィールドは編集できなくなります（グレー表示になる） |
      | タイプ | 使用するキャプションのタイプを選択します。<br>**サブタイトル** - ダイアログを翻訳または文字起こししたビデオと共に表示されるキャプションテキスト。<br>**キャプション** - キャプションテキストには、背景雑音、話者の識別、その他の関連する詳細、および会話の翻訳または文字起こしが含まれているので、聴覚障害のあるユーザーのアクセシビリティを向上します。 |
      | ラベル | メディアプレーヤーの&#x200B;**[!UICONTROL オーディオまたはキャプションを選択]**&#x200B;ポップアップリストのキャプションの名前に表示されるテキスト。ラベルは、サブタイトルまたはキャプショントラックに対応するユーザーに表示される内容です。例えば、`English (CC)` のように指定します。 |

      必要に応じて、後でキャプションメタデータを変更または編集できます。ビデオが公開されると、これらの詳細は、公開中のビデオの公開 URL に反映されます。

   1. ページの右上隅付近にある&#x200B;**[!UICONTROL 保存して閉じる]**&#x200B;ドロップダウンで、「**[!UICONTROL 保存]**」をクリックします。ファイルがアップロードされ、メタデータ処理が開始されます（インターフェイスの&#x200B;**ステータス**&#x200B;列参照）。

      >[!NOTE]
      >
      >インスタンスのキャッシュ設定に基づき、メタデータ処理がプレビューおよび公開済み URL に反映されるまでに数分かかる場合があります。

   1. 前の手順で「**[!UICONTROL 保存]**」を選択する代わりに「**[!UICONTROL 保存して閉じる]**」を選択した場合でも、アップロードしたファイルの処理ステータスを表示できます。詳しくは、[アップロードされたキャプションファイルとオーディオトラックファイルのライフサイクルステータスを表示する](#lifecycle-status-video)を参照してください。
   1. 手順 8 に進みます。

   +++

   +++**オプション 2：***AI に複数の言語でキャプションファイルを生成する場合*（「**[!UICONTROL オーディオトラックを変換]**」オプション）

   1. ページの右上隅付近で、**[!UICONTROL キャプションを作成]**／**[!UICONTROL オーディオトラックを変換]**&#x200B;をクリックします。

      ![オーディオトラックを変換ダイアログボックス。](/help/assets/dynamic-media/assets/msma-convertaudiotracks.png)
      *オーディオトラックを変換ダイアログボックスでは、AI を使用して複数の言語のキャプションファイルを生成します。*

   1. **オーディオトラックを変換**&#x200B;ダイアログボックスで、次のオプションを設定します。

      | オプション | 説明 |
      |--- |--- |
      | 変換するオーディオトラック | ![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、AI を使用してキャプションを生成する、アップロードされたオーディオトラックファイルを選択します。 |
      | 出力言語 | ![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、キャプションファイルを表示する言語を 1 つ以上選択します。<br>選択した言語を削除するには、![閉じるアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) をクリックします。<br>ビデオの再生中、ここで選択した順序でメディアプレーヤーに言語のリストが表示されます。 |

   1. 「**[!UICONTROL 完了]**」をクリックします。
   1. ページの右上隅付近にある&#x200B;**[!UICONTROL 保存して閉じる]**&#x200B;ドロップダウンで、「**[!UICONTROL 保存]**」をクリックします。
   1. 「**[!UICONTROL キャプションとオーディオトラック]**」タブをもう一度クリックします。1 つ以上のキャプションファイルが作成され、処理が開始されます（インターフェイスの&#x200B;**ステータス**&#x200B;列を参照）。また、[アップロードされたキャプションファイルとオーディオトラックファイルのライフサイクルステータスを表示する](#lifecycle-status-video)も参照してください。

      >[!NOTE]
      >
      >インスタンスのキャッシュ設定に基づき、メタデータ処理がプレビューおよび公開済み URL に反映されるまでに数分かかる場合があります。

   1. （オプション）キャプションファイル名の右側にある ![描画アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) をクリックします。**キャプションを編集**&#x200B;ダイアログボックスで、次のファイルの詳細情報を編集できます。

      | キャプションメタデータ | 説明 |
      | --- | --- |
      | タイプ | 使用するキャプションのタイプを選択します。<br>**サブタイトル** - ダイアログを翻訳または文字起こししたビデオと共に表示されるキャプションテキスト。<br>**キャプション** - キャプションテキストには、背景雑音と話者の識別が含まれます。また、会話の翻訳または文字起こしと共に、その他の関連情報も含まれます。このアプローチにより、聴覚障害のある人にとってコンテンツのアクセシビリティが向上します。 |
      | ラベル | メディアプレーヤーの&#x200B;**[!UICONTROL オーディオまたはキャプションを選択]**&#x200B;ポップアップリストのキャプションの名前に表示されるテキスト。ラベルは、サブタイトルまたはキャプショントラックに対応するユーザーに表示される内容です。例：`English (CC)` |

      必要に応じて、後で特定のキャプションメタデータを変更または編集できます。ビデオが公開されると、これらのメタデータの詳細が公開されたビデオの公開 URL に反映されます。
   1. 手順 8 に進みます。

   +++

   +++**オプション 3：***キャプションファイル（`.vtt`）内のテキストを修正し、再度アップロードして古い `.vtt` ファイルを置き換え、修正したファイルを AI に翻訳させる必要があります*（「**[!UICONTROL キャプションを翻訳]**」オプション）

   1. **[!UICONTROL キャプションを作成]**／**[!UICONTROL キャプションを翻訳]**&#x200B;をクリックします。このオプションは、1 つ以上のキャプションファイルが既に追加および処理されている場合に使用できます。

      ![キャプションを翻訳ダイアログボックス。](/help/assets/dynamic-media/assets/msma-translate-captions.png)
      *キャプションを翻訳ダイアログボックスでは、既存のキャプションファイルを使用して、AI に複数の言語の新しいキャプションファイルを生成させることができます。*

   1. **キャプションを翻訳**&#x200B;ダイアログボックスで、次のオプションを設定します。

      | オプション | 説明 |
      |--- |--- |
      | 翻訳するキャプション | ![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、AI を使用してキャプションを生成するキャプションファイルを選択します。 |
      | 出力言語 | ![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、キャプションファイルを表示する言語を 1 つ以上選択します。<br>選択した言語を削除するには、![閉じるアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) をクリックします。<br>ビデオの再生中、ここで選択した順序でメディアプレーヤーに言語のリストが表示されます。 |

   1. 「**[!UICONTROL 完了]**」をクリックします。
   1. ページの右上隅付近にある&#x200B;**[!UICONTROL 保存して閉じる]**&#x200B;ドロップダウンで、「**[!UICONTROL 保存]**」をクリックします。
   1. 「**[!UICONTROL キャプションとオーディオトラック]**」タブをもう一度クリックします。1 つ以上のキャプションファイルが作成され、処理が開始されます（インターフェイスの&#x200B;**ステータス**&#x200B;列を参照）。また、[アップロードされたキャプションファイルとオーディオトラックファイルのライフサイクルステータスを表示する](#lifecycle-status-video)も参照してください。

      >[!NOTE]
      >
      >インスタンスのキャッシュ設定に基づき、メタデータ処理がプレビューおよび公開済み URL に反映されるまでに数分かかる場合があります。

   1. （オプション）キャプションファイル名の右側にある ![描画アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) をクリックします。**キャプションを編集**&#x200B;ダイアログボックスで、次のファイルの詳細情報を編集できます。

      | キャプションメタデータ | 説明 |
      | --- | --- |
      | タイプ | 使用するキャプションのタイプを選択します。<br>**サブタイトル** - ダイアログを翻訳または文字起こししたビデオと共に表示されるキャプションテキスト。<br>**キャプション** - キャプションテキストには、背景雑音、話者の識別も含まれます。また、会話の翻訳または文字起こしと共に、その他の関連情報も含まれます。このアプローチにより、聴覚障害のある人にとってコンテンツのアクセシビリティが向上します。 |
      | ラベル | メディアプレーヤーの&#x200B;**[!UICONTROL オーディオまたはキャプションを選択]**&#x200B;ポップアップリストのキャプションの名前に表示されるテキスト。ラベルは、サブタイトルまたはキャプショントラックに対応するユーザーに表示される内容です。例：`English (CC)` |

      必要に応じて、後で特定のキャプションメタデータを変更または編集できます。ビデオが公開されると、これらのメタデータの詳細が公開されたビデオの公開 URL に反映されます。

   1. 手順 8 に進みます。

   +++

1. （オプション）公開する前にビデオをプレビューして、キャプションとオーディオが期待どおりに動作することを確認します。[複数のキャプションとオーディオトラックがあるビデオのプレビュー](#preview-video-audio-subtitle)を参照してください。
1. ビデオを公開します。詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

#### 既に公開されているビデオへのキャプションとオーディオトラックのファイルの追加について

公開されているビデオに追加のキャプションファイルまたはオーディオトラックファイルをアップロードした後に、準備が整うと、これらのファイルは `Processed` ステータスになります。そうすると、Dynamic Media でビデオをプレビューして、新しいファイルをを見たり、聞いたりできます。

ただし、プレビュー後、新しく追加されたキャプションまたはオーディオトラックファイルも公開されるようにするには、ビデオを再度&#x200B;*公開*&#x200B;する必要があります。公開後、キャプションやオーディオは、Dynamic Media のパブリック URL で使用できるようになります。

>[!NOTE]
>
>インスタンスのキャッシュ設定に基づき、メタデータの更新がプレビューおよび公開済み URL に反映されるまでに、数分かかる場合があります。

即時公開されるように Dynamic Media を設定したシナリオでは、追加のキャプションまたはオーディオのファイルをアップロードすると、キャプションまたはオーディオのファイルのアップロード後にビデオの公開が直ちにトリガーされます。

>[!CAUTION]
>
>公開または非公開のビデオにキャプションファイルまたはオーディオファイルをアップロードした場合、ビデオを&#x200B;[*再処理*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)&#x200B;するとファイルは削除されます。ビデオの元のオーディオのみがそのままの状態で残ります。このような場合は、キャプションファイルとオーディオトラックファイルをビデオに再度アップロードする必要があります。

#### キャプション修飾子が付いた既存の URL があるビデオへの複数のキャプションの追加

Dynamic Media では、URL 修飾子を使用して、ビデオにキャプションを 1 つ追加できます。詳しくは、[ビデオへのキャプションの追加](#adding-captions-to-video)を参照してください。

公開済みビデオでは、URL 修飾子を使用して追加されたキャプションよりも、複数のキャプションの変更が優先されます。

**キャプション修飾子が付いた既存の URL があるビデオに複数のキャプションを追加するには：**

1. 既に修飾子として追加されているキャプションファイルをビデオにアップロードして、ファイルを明示的に管理できます。
1. 必要に応じて、その他のキャプションファイルをアップロードします。
1. 通常どおりにビデオを公開します。
キャプション修飾子を持つ既存の URL で、複数のキャプションを読み込めるようになりました。


### ビデオのサブタイトルの編集

ビデオアセットのサブタイトル（キャプション）は、Dynamic Media ユーザーインターフェイス内で直接編集できます。この機能を使用すると、`.vtt` サブタイトルファイルの編集、更新のプレビュー、変更の公開をシームレスに行うことができます。

* サブタイトルを公開すると、変更内容は自動的に同期および公開されます。
* 編集エラーが発生し、サブタイトルを再生成する必要がある場合：
   * 既存のサブタイトルファイルを削除します。
   * [ビデオに複数のキャプションとオーディオトラックを追加](#add-msma)の手順 7 でオプション 2（オーディオトラックを変換）を使用します。
   * 「**保存**」または「**保存して閉じる**」をクリックして、新しいサブタイトルファイルを生成します。
* エディター内のサブタイトルプレビューは編集専用で、最終的なビデオ再生ユーザーインターフェイスでのサブタイトルの表示方法を反映していません。

**ビデオのサブタイトルを編集するには：**

1. サブタイトルを編集するビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. プロパティページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。
1. **キャプション**&#x200B;見出しの下で、キャプションファイル名の右側にある ![アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ProjectEdit_18_N.svg) をクリックします。

   ![「キャプション」見出しの下にある「サブタイトルを編集」アイコン](/help/assets/dynamic-media/assets/msma-editcaption.png)

1. **サブタイトルを編集**&#x200B;ダイアログボックスで、必要に応じて WebVTT ファイルのテキストを編集します。

   ![サブタイトルを編集ダイアログボックス](/help/assets/dynamic-media/assets/msma-editsubtitle-dialogbox.png)

1. ダイアログボックスの右下隅にある「**保存**」をクリックします。


### アップロードされたキャプションファイルとオーディオトラックファイルのライフサイクルステータスを表示する {#lifecycle-status-video}

プライマリビデオにアップロードされたキャプションやオーディオトラックのファイルのライフサイクルステータスを確認できます。これは、**プロパティ**&#x200B;の「**キャプションとオーディオトラック**」タブから行うことができます。

**ビデオのライフサイクルステータスを表示するには：**

1. ライフサイクルステータスを表示するビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. **プロパティ**&#x200B;ページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。
1. **[!UICONTROL ステータス]**&#x200B;列で、各キャプションファイルまたはオーディオファイルのステートをメモします。

| キャプションとオーディオトラックのステータス | 説明 |
| --- | --- |
| 処理 | 新しいキャプションまたはオーディオトラックのファイルを追加して保存すると、「処理中」の状態になります。Dynamic Media は、ストリーミングマニフェストをプライマリビデオに添付することで、ファイルを処理します。 |
| 処理済み | 処理が完了すると、キャプションやオーディオトラックのファイル、またはプライマリビデオに関連付けられていたオリジナルのオーディオトラックが「処理済み」ステータスで表示されます。ビデオを公開する&#x200B;*前*&#x200B;に、「処理済み」として表示されるキャプションおよびオーディオトラックのファイルをプレビューできます。 |
| 公開済み | 「公開済み」状態は、プライマリビデオの「公開済み」と同じ状態を表します。アセットは、プライマリビデオが公開されると公開されます。また、公開 Dynamic Media URL で使用できます。 |
| 失敗 | 「失敗」状態は、キャプションまたはオーディオトラックのファイルの処理が完了しなかったことを意味します。キャプションまたはオーディオトラックのファイルを削除して、再度アップロードします。 |
| 非公開 | 公開済みのプライマリビデオを明示的に非公開にすると、ビデオに追加したキャプションまたはオーディオトラックのファイルも非公開になります。 |


### 複数のオーディオトラックがあるビデオでのデフォルトオーディオの設定

デフォルトでは、ビデオの元々のオーディオが、再生されるオーディオとしてデフォルトで設定されます。

ただし、アップロードしたオーディオトラックファイルは、ビデオをビューアーに読み込んだ後に再生されるデフォルトのオーディオとして設定できます。プロパティのユーザインターフェイスの「**キャプションとオーディオトラック**」タブでは、`Default` ラベルは、ビデオ再生用のオーディオトラックファイルの右側に適用されます。

>[!NOTE]
>
>デフォルトのオーディオの再生は、次のブラウザーで設定されている内容によっても異なります。
>
>* Chrome - ビデオに設定されているデフォルトのオーディオが再生されます。
>* Safari - Safari でデフォルト言語が設定されている場合、オーディオは設定されたデフォルト言語で再生されます（ビデオのマニフェストで使用できる場合）。それ以外の場合は、ビデオのプロパティの一部として設定されたデフォルトのオーディオが再生されます。

**複数のオーディオトラックがあるビデオのデフォルトオーディオを設定するには：**

1. デフォルトのオーディオトラックを設定するビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. プロパティページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。
1. **オーディオトラック**&#x200B;の見出しで、ビデオのデフォルトとして設定するオーディオトラックファイルを選択します。
1. ![オーディオアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Audio_18_N.svg)「**[!UICONTROL デフォルトとして設定]**」をクリックします。
1. **デフォルトとして設定**&#x200B;ダイアログボックスで、「**[!UICONTROL 置換]**」をクリックします。

   ![選択したオーディオトラックファイル名と、ハイライトされた「デフォルトとして設定」ボタンが表示されたオーディオトラックの見出し。](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*ビデオのデフォルトオーディオトラックの設定*

1. 右上隅で「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. ビデオを公開します。詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

### 複数のキャプションとオーディオトラックがあるビデオのプレビュー {#preview-video-audio-subtitle}

キャプションファイルとオーディオトラックファイルをビデオにアップロードして処理した後、Dynamic Media ビデオビューアーを使用して、様々なトラックをプレビューできます。これにより、ビデオが顧客に対してどのように表示され、聞こえるかを確認し、ビデオが期待どおりに動作していることを確認できます。

このビデオに満足したら、次の操作を実行できます。 [公開する](publishing-dynamicmedia-assets.md) 次のいずれかの方法を使用します。

[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。[ページへの Dynamic Media アセットの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

>[!NOTE]
>
>Experience Manager のデフォルトの「プレビュー」タブには、複数のキャプションとオーディオトラックは表示されません。これは、これらのトラックが Dynamic Media に関連付けられており、Dynamic Media ビューアーのプレビューでのみ表示できるからです。

**複数のキャプションとオーディオトラックを持つビデオをプレビューするには：**

1. **[!UICONTROL アセット]**&#x200B;で、複数のキャプションとオーディオトラックを追加した既存のビデオに移動します。
1. ビデオアセットをクリックして、プレビューモードで開きます。
1. プレビューページで、ページの左上隅付近にある ![左パネルアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、「**[!UICONTROL ビューア]**」を選択します。

   ![「ビューアー」オプションを表示するドロップダウンリスト。](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. ページの左上隅付近にある ![左パネルアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg)「ビューア」![山形下向きアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) をクリックし、ビデオプレビューに使用するビューアを選択します。

1. ページの右下隅付近にある吹き出しアイコンをクリックし、聞きたい、見たい、またはその両方を行いたいオーディオまたはサブタイトル／キャプションを選択します。

   ![ビデオビューアーのオーディオとキャプションのポップアップリスト。](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*ビデオ再生用のオーディオとキャプションを選択するユーザーのシミュレーション。*

1. 再生を開始するには、![再生アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg) をクリックします。
必要に応じて、![最大化アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Maximize_22_N.svg) をクリックして、表示ウィンドウを最大化します。
ページの左下隅付近にある「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL 埋め込み]**」ボタンをクリックします。これらのボタンはそれぞれ、[web アプリケーションにビデオの URL をリンクする](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)ため、[web ページにビデオを埋め込む](/help/assets/dynamic-media/embed-code.md)ために使用します。
1. プレビューページの右上隅付近にある「**[!UICONTROL 閉じる]**」をクリックします。

### ビデオからのキャプションまたはオーディオトラックファイルの削除

ビデオからキャプションファイルやオーディオトラックファイルを削除できます。公開済みのキャプションまたはオーディオトラックのファイルを削除すると、そのビデオの公開済み URL に自動的に反映されます。

プライマリビデオから抽出されたオリジナルのオーディオトラックは削除できません。

**ビデオからキャプションファイルまたはオーディオトラックファイルを削除するには：**

1. デフォルトのオーディオトラックを設定するビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. プロパティページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。
1. 次のいずれかの操作を行います。

   * キャプション - **キャプション**&#x200B;の見出しで、ビデオから削除する 1 つまたは複数のキャプションファイルを選択し、![削除アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg)「**[!UICONTROL 削除]**」をクリックします。
   * オーディオトラック - **オーディオトラック**&#x200B;の見出しで、ビデオから削除する 1 つまたは複数のオーディオトラックファイルを選択し、![削除アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg)「**[!UICONTROL 削除]**」をクリックします。

1. 削除ダイアログボックスで、「**[!UICONTROL OK]**」をクリックします。
1. ビデオを公開します。

### ビデオにアップロードされたキャプションまたはオーディオトラックファイルをダウンロード

ビデオにアップロードしたキャプションまたはオーディオトラックファイルをダウンロードできます。選択したすべてのファイルを `.zip` としてダウンロードするか、ファイルごとに個別のダウンロードフォルダーを作成するかを選択できます。

プライマリビデオファイルから抽出された、元のオーディオトラックはダウンロードできません。

**ユースケース：**`.vtt` ファイルにエラーが見つかった場合は、キャプションファイルのダウンロードが必要になる場合があります。間違った `.vtt` ファイルをダウンロードし、プレーンテキストエディターで開いて、修正するだけです。`.vtt` ファイルを保存したら、もう一度アップロードします。次に、「**[!UICONTROL キャプションを翻訳]**」オプションを使用して、修正した `.vtt` ファイルを再翻訳します。

**ビデオにアップロードされたキャプションまたはオーディオトラックファイルをダウンロードするには：**

1. デフォルトのオーディオトラックを設定するビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. **プロパティ**&#x200B;ページで、「**[!UICONTROL キャプションとオーディオトラック]**」タブを選択します。
1. 次のいずれかの操作を行います。

   * キャプション - **キャプション**&#x200B;見出しで、ビデオからダウンロードする 1 つ以上のキャプションファイルを選択し、![ダウンロードアイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg)「**[!UICONTROL ダウンロード]**」をクリックします。
   * オーディオトラック - **オーディオトラック**&#x200B;見出しで、ビデオからダウンロードする 1 つ以上のオーディオトラックファイルを選択し、![ダウンロードアイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg)「**[!UICONTROL ダウンロード]**」をクリックします。

1. ダウンロードダイアログボックスで、以下のオプションを設定します。

   | ダウンロードオプション | 説明 |
   |--- |--- |
   | 名前を付けて保存 | 「名前を付けて保存」テキストフィールドに指定されたデフォルトのファイル名を使用するか、独自の名前を指定します。 |
   | アセットごとに個別のフォルダーを作成 | ダウンロード用に選択したキャプションファイルまたはオーディオトラックファイルごとにフォルダーを作成します。 |
   | メール | デフォルトのメールプログラムを使用して、.zip ファイルを指定したメールアドレスに送信します。 |
   | アセット | ダウンロードするファイルの数と、選択したすべてのファイルの合計サイズを指定します。このオプションの選択を解除すると、「**[!UICONTROL ダウンロード]**」ボタンが暗くなり（オフになり）、ファイルをダウンロードできなくなります。 |
   | レンディション | レンディションとは、元のファイルの代替バージョンまたはプレビューを指し、通常は小さいまたは低い解像度のバージョンです。0 B と表示される場合は、代替バージョンが使用できないか、サイズを登録するには小さすぎる可能性があります。 |

1. 「**[!UICONTROL ダウンロード]**」を選択します。
1. ビデオを公開します。詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

<!-- ## About AI-generated captions for videos in Dynamic Media

AI-powered captions in Dynamic Media are designed to enhance video accessibility and engagement by automatically generating accurate and synchronized subtitles. This technology uses advanced AI algorithms to transcribe spoken content into text, which is then displayed as captions on the video. Here are some key features.

* **Automatic Transcription:** The AI system transcribes spoken words from an existing audio file into text in real-time, ensuring that captions are generated quickly and accurately.
* **Multilingual Support:** It supports more than 60 languages, making it easier to reach a global audience. You can even translate your existing captions to different languages.
* **Enhanced Accessibility:** By providing captions, videos become more accessible to viewers who are deaf or hard of hearing, as well as those who prefer to watch videos with the sound off.
* **Improved Engagement:** Captions can help retain viewer attention and improve comprehension, especially in noisy environments or when the viewer's native language is different from the video's language.

These features in Dynamic Media make AI-powered video aptions a valuable tool for content creators looking to enhance their video content's accessibility and engagement. -->

## ビデオにクローズドキャプションを追加 {#adding-captions-to-video}

1 つのビデオまたはアダプティブビデオセットにクローズドキャプションを追加すると、ビデオの配信先をグローバルマーケットまで拡大できます。クローズドキャプションを追加すると、音声をダビングする必要も、異なる言語ごとにネイティブスピーカーの音声を使って再録音する必要もなくなります。ビデオは、録画された言語で再生されます。外国語のキャプションが表示されるので、異なる言語を使用する視聴者もオーディオ部分を理解できます。

クローズドキャプションを使用すると、耳が聞こえない人や聞こえにくい人に対して、より高いアクセシビリティを提供できます。

>[!NOTE]
>
>使用するビデオプレーヤーがクローズドキャプションの表示に対応する必要があります。

詳しくは、[Dynamic Media のアクセシビリティ](/help/assets/dynamic-media/accessibility-dm.md)を参照してください。

Dynamic Media では、キャプションファイルを JSON（JavaScript Object Notation）形式に変換できます。このように変換できるので、JSON テキストを、ビデオの完全なトランスクリプトとして表示せずに web ページに埋め込むことができます。この後、検索エンジンがコンテンツをクロールまたはインデックス作成できます。これにより、ビデオを検索しやすくなり、ビデオコンテンツの詳細がユーザーに提供されます。

URL での JSON 機能の使用について詳しくは、[静的な（画像以外の）コンテンツの提供](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api)を参照してください。

**ビデオにキャプションを追加するには：**

1. サードパーティのアプリケーションまたはサービスを使用して、ビデオのキャプションファイルを作成します。

   作成するファイルは、WebVTT（Web ビデオテキストトラック）標準に従っている必要があります。キャプションファイル名の拡張子は `.vtt` です。WebVTT キャプション標準をよく確認してください。

   [WebVTT：Web Video Text Tracks 形式（英語）](https://w3c.github.io/webvtt/)を参照してください。

   Dynamic Media 以外で WebVTT キャプションファイルの作成に使用できる、無料と有料のツールやサービスを提供している web サイトが多数あります。

サイトの画面に表示される指示に従って、WebVTT ファイルを作成して保存します。終了したら、キャプションファイルの内容をコピーし、空のテキストエディターに貼り付けて、ファイル拡張子 VTT を付けて保存します。

>[!NOTE]
>
>複数言語のビデオキャプションを用意してグローバル対応する場合、WebVTT 標準では、サポート対象の言語ごとに個別の `.vtt` ファイルと呼び出しを作成する必要があります。

一般に、キャプションの `.vtt` ファイルにはビデオファイルと同じ名前を付け、名前の末尾に言語ロケール（-EN、-FR、-DE、-JA など）を追加します。このようにすると、既存の WCM システムを使用してビデオの URL を自動的に生成する際に役立ちます。

1. Experience Manager で、WebVTT キャプションファイルを DAM にアップロードします。
1. アップロードしたキャプションファイルに関連付ける、*公開済み*&#x200B;ビデオアセットに移動します。

   URL をコピーするには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。

   [アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

1. 次のいずれかの操作を行います。

   * ポップアップビデオビューアエクスペリエンスの場合、「**[!UICONTROL URL]**」ボタンをクリックします。URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。コピーしたビデオの URL を次の構文で追加します。

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     キャプションパスの末尾にある `,1` に注意します。パスの VTT ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それぞれ、`,1` または `,0` を設定します。

   * 埋め込みビデオビューアエクスペリエンスの場合は、「**[!UICONTROL 埋め込みコード]**」をクリックします。埋め込みコードダイアログボックスで、埋め込みコードを選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。コピーした埋め込みコードを次の構文で追加します。

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     キャプションパスの末尾にある `,1` に注意します。パスの VTT ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それぞれ、`,1` または `,0` を設定します。

## ビデオにチャプターマーカーを追加 {#adding-chapter-markers-to-video}

1 つのビデオまたはアダプティブビデオセットにチャプターマーカーを追加すると、長編ビデオの視聴と操作が簡単になります。ビデオの再生中に、ビデオタイムライン（ビデオスクラバーとも呼ばれる）のチャプターマーカーを選択することができます。これにより、ユーザーは、関心があるポイントや、新しいコンテンツ、トレーニング、デモンストレーションなどにすぐに移動できます。

>[!NOTE]
>
>使用するビデオプレーヤーが、チャプターマーカーの使用をサポートしている必要があります。Dynamic Media ビデオプレーヤーは、チャプターマーカーをサポートしていますが、サードパーティのビデオプレーヤーは、チャプターマーカーをサポートしていない場合があります。

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

HTML5 ビデオビューアを使用するので、作成するチャプターファイルが WebVTT（Web Video Text Tracks）標準に準拠していることを確認してください。チャプターファイルの拡張子は `.vtt` です。WebVTT キャプション標準をよく確認してください。

[WebVTT：Web Video Text Tracks 形式（英語）](https://w3c.github.io/webvtt/)を参照してください。

**ビデオにチャプターマーカーを追加するには：**

1. この `.vtt` ファイルを UTF8 エンコーディングで保存して、チャプタータイトルテキストの文字レンディションに関する問題を回避します。

   一般に、チャプター VTT ファイルの名前には、ビデオファイルと同じ名前を付けて、名前の末尾にチャプターを追加します。このようにすると、既存の WCM システムを使用してビデオの URL を自動的に生成する際に役立ちます。
1. Experience Manager で、WebVTT チャプターファイルをアップロードします。

   [アセットのアップロード](/help/assets/manage-digital-assets.md#uploading-assets)を参照してください。

1. 次のいずれかの操作を行います。

   <table>
     <tbody>
      <tr>
       <td>ポップアップビデオビューアエクスペリエンスの場合、</td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルに関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」を選択します。</li>
       <li>左パネルで、ビデオビューアプリセット名を選択します。ビデオのプレビューが別のページで開きます。</li>
       <li>左パネルの下部にある「<strong>URL</strong>」ボタンをクリックします。</li>
       <li>URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。</li>
       <li>ビデオのコピー済み URL を次の構文で追加すると、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>埋め込みビデオビューアエクスペリエンスの場合、<br /> </td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルに関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」を選択します。</li>
       <li>左パネルで、ビデオビューアプリセット名を選択します。ビデオのプレビューが別のページで開きます。</li>
       <li>左パネルの下部にある「<strong>埋め込み</strong>」を選択します。</li>
       <li>埋め込みコードダイアログボックスで、コード全体を選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。</li>
       <li>ビデオの埋め込みコードを次の構文で追加して、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>


## ビデオサムネールについて {#about-video-thumbnails}

ビデオサムネールとは、ビデオフレームまたは画像アセットの縮小バージョンで、顧客向けのビデオを表すものです。サムネールは、顧客にビデオの選択を促すものにします。

Experience Manager 内のすべてのビデオには、サムネールを関連付ける必要があります。デフォルトでは、Experience Manager にビデオをアップロードすると、最初のフレームがサムネールとして使用されます。ただし、ブランド設定やビジュアル検索用にサムネールをカスタマイズできます。ビデオのサムネールをカスタマイズするには、ビデオを再生して、使用するフレームで一時停止します。あるいは、Digital Asset Manager に既にアップロードして、*公開済み*&#x200B;の画像アセットを選択することもできます。

ビデオのサムネールを変更すると、ビデオの再処理時に Asset compute サービスを介したサムネールの生成がスキップされます。

ビデオのサムネールをカスタマイズする機能は、ビデオが保存されているフォルダーにビデオプロファイルを適用した後でのみ使用できます。

### カスタムビデオサムネールの追加 {#adding-a-custom-video-thumbnail}

1. 次の作業が完了していることを確認してください。

   * ビデオアセット用のフォルダーの作成。
   * [ビデオプロファイルをフォルダーに適用しました](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders)。

   * [フォルダーへのビデオのアップロード](/help/assets/manage-video-assets.md#upload-and-preview-video-assets)。


1. サムネイル画像を変更するアップロード済みビデオアセットに移動します。
1. アセット選択モードで、![カードを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg)（カード表示）または ![リストを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg)（リスト表示）からビデオアセットを選択します。
1. ツールバーで、![情報アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) プロパティをクリックします。
1. ビデオのプロパティページで、「**[!UICONTROL サムネールを変更]**」をクリックします。
1. サムネールを変更ダイアログボックスで、次のいずれかの操作を行います。

   * ビデオのフレームを新しいサムネイルとして使用するには：

      * ツールバーで「**[!UICONTROL ビデオからフレームを選択]**」タブをクリックします。
      * ![再生アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg) をクリックします。
      * ビデオの新しいサムネールとしてキャプチャするフレームの ![一時停止アイコン](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PauseCircle_22_N.svg) をクリックします。

   * 画像アセットを新しいサムネールとして使用するには、次の手順を行います。

      * ツールバーで「**[!UICONTROL アセットからサムネールを選択]**」タブをクリックします。
      * 「**[!UICONTROL サムネールを選択]**」ボタンをクリックします。
      * 使用を希望する、以前にアップロードおよび公開された画像アセットに移動します。アセットは、ビデオのサムネール画像として機能するように自動的にサイズ変更されます。
      * 画像アセットを選択し、「**[!UICONTROL 選択]**」をクリックします。

1. サムネールを変更ダイアログボックスで、「**[!UICONTROL 変更を保存]**」をクリックします。
1. ビデオのプロパティページで、右上隅にある「**[!UICONTROL 保存して閉じる]**」または「**[!UICONTROL 保存]**」をクリックします。



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 &times; 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

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

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

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

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
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

標準ビューアでは、Dynamic Media で処理されたビデオを再生できます。また、マニフェスト URL に直接アクセスし、独自のカスタムビューアを使用して再生することもできます。次に、ビデオのマニフェスト URL を取得する API を示します。

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

上記のメソッドを使用してビデオのマニフェスト URL を取得するには、[ビデオエンコーディングプロファイル](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)を「ビデオのアップロード」フォルダーに追加します。Dynamic Media は、フォルダーに割り当てられたビデオエンコーディングファイルで見つかったエンコーディングに基づいて、これらのビデオを処理します。これで、上記の API を呼び出して、アップロードされたビデオのマニフェスト URL を取得できるようになりました。

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


<!-- REMOVED THE FOLLOWING TOPIC AS PER EMAIL FROM RIYA MIDHA, WEDNESDAY, MARCH 5, 2025; TOPIC IS OBSOLETE/NO LONGER NEEDED BECAUSE THE FEATURES IT DESCRIBES ARE NOW GA WITHIN THE SOFTWARE

## Enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account {#enable-dash}

You can enable support in Dynamic Media for:

* DASH
* Multi-captions and audio tracks
* AI-generated captions (Limited Availability)

By creating and submitting an Adobe Customer Support case. 

Enabling any of the above three capabilities, enables all of them. So, if you only want DASH enabled, you are actually enabling all three capabilities listed above.  

| Capability | Description |
| --- | --- |
| DASH | DASH (Digital Adaptive Streaming over HTTP) is the international standard for video streaming and is widely adopted across different video viewers. When DASH is enabled on your account, you get the option to choose from either DASH or HLS for adaptive video streaming. Or, you can opt for both with automatic switching between players when **[!UICONTROL auto]** is selected as the playback type in the Viewer preset.<br>Some key benefits from enabling DASH on your account include the following:<ul><li>Package DASH stream video for adaptive bitrate streaming. This method leads to higher efficiency of delivery. Adaptive streaming ensures the best viewing experience for your customers.</li><li>Browser optimized streaming with Dynamic Media players switches between HLS and DASH streaming to ensure the best quality of service. The video player auto-switches to HLS when a Safari browser is used.</li><li>You can configure your preferred streaming method (HLS or DASH) by editing the video viewer preset.</li><li>Optimized video encoding ensures that no additional storage is used while enabling DASH capability. A single set of video encodings is created for both HLS and DASH to optimize video storage costs.</li><li>Helps make video delivery more accessible for your customers.</li><li>Get the streaming URL by way of APIs, too.</li></ul>|
| Multi-captions and audio tracks | You can benefit from having multiple caption and audio track support automatically enabled. After enablement, all subsequent videos that you upload are processed with a new backend architecture that includes support for adding multiple caption and audio tracks to your videos. |
| AI-generated captions (Limited Availability) | Create captions for your videos powered by AI. Using AI, it creates the transcript of the video and converts it into captions. Even the timeline is defined, too. |

>[!IMPORTANT]
>
>Any videos that you uploaded *before* enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account:** 

1. [Use the Admin Console to start the creation of a new support case](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html).
1. To create a support case, follow the instructions while ensuring you provide the following information:

    * Primary contact name, email, phone.
    * Your Cloud Services environment (program ID and environment ID).
    * Your Dynamic Media company account name.
    * Your Dynamic Media region: North America (NA), Asia-Pacific (APAC), or Europe-Middle East-Asia (EMEA).
    * Specify that you want DASH, multi-captions and multi-audio tracks, and AI-generated captions (Limited Availability) support enabled on your Dynamic Media account, on AEM as a Cloud Service.
   
1. Adobe Customer Support adds you to the Customer Wait List based on the order in which requests are submitted.
1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate and set a target date for enablement.
1. Adobe Customer Support notifies you after completion.
1. Now, do one or more of the following:

    * Create your [video viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) as usual.
    * Create your [video profile](/help/assets/dynamic-media/video-profiles.md) as usual.
    * [Add multiple captions and audio tracks](#add-msma) to your video. -->


<!-- 
## About multiple caption and audio track support for videos in Dynamic Media{#about-msma}

With multiple caption and audio track capability in Dynamic Media, you can easily add multiple captions and audio tracks to a primary video. This capability means that your videos are accessible to a global audience. You can customize a single, published primary video to a global audience in multiple languages and adhere with accessibility guidelines for different geographical regions. Authors can also manage the captions and audio tracks from a single tab in the user interface.

   ![Captions and audio tracks tab in Dynamic Media along with a table showing uploaded .VTT caption files and uploaded .MP3 audio track files for a video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)


Some of the use cases to consider for adding multiple captions and audio tracks to your primary video include the following:

| Type | Use case |
| --- | --- |
| Captions | Multiple language support<br>Descriptive text for accessibility |
| Audio tracks | Multiple language support<br>Commentary tracks<br>Descriptive audio |


All [video formats supported in Dynamic Media](/help/assets/file-format-support.md) and all Dynamic Media video viewers-except the Dynamic Media Video_360 viewer-are supported for use with multiple captions and audio tracks.

Multi-caption and multi-audio track capability is available for your Dynamic Media account by way of a feature toggle that must be enabled (turned on) by Adobe Customer Support.

### Add multiple captions and audio tracks to your video {#add-msma}

Before you add multiple caption and audio tracks to your video, be sure you already have the following in-place:

* Dynamic Media is set up in an AEM environment.
* A [Dynamic Media Video profile is applied to the folder where your videos are ingested](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Multi-caption, and multi-audio track is enabled on your Dynamic Media account](/help/assets/dynamic-media/video.md#enable-dash).

Added captions and captions are supported with WebVTT and Adobe VTT formats. And, added audio track files are supported with MP3 format.

>[!IMPORTANT]
>
>Any videos that you uploaded before enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To add multiple captions and audio tracks to your video:**

1. [Upload your primary video to a folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) that already has a video profile assigned to it.
1. Navigate to the uploaded video asset that you want to add multiple caption and audio tracks.
1. In asset selection mode, either from the List View or the Card View, select the video asset.
1. On the toolbar, select the Properties icon (a circle with an "i" in it). 

   ![Asset properties button.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Selected video asset in Card View.*

1. On the video's Properties page, select the **[!UICONTROL Captions & Audio tracks]** tab.


   >[!TIP]
   >If you do not see the [!UICONTROL Captions & Audio tracks] tab, it means either one of two things:
   >* The folder in which the selected video resides does not have a video profile assigned to it. In which case, see [Apply a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Or, Dynamic Media must reprocess the video. In which case, see [Reprocess Dynamic Media assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

    When you have completed either one of the above tasks, return to these steps.

   ![Asset properties](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Captions and audio tracks tab on the video's Properties page.*

1. (Optional) To add one or more caption files to a video, do the following:

    * Select **[!UICONTROL Upload Captions]**.
    * Navigate to, and select, one or more `.vtt` (Video Text Tracks) files and open them.
    * For captions to be visible on the media player, you must add required details (metadata) about each caption file that you uploaded. Select the pencil icon to the right of a caption file name. In the Edit Caption dialog box, enter the following required details about the file, then select **[!UICONTROL Save]**. Repeat this process for each caption file that you uploaded:


    | Caption metadata | Description | 
    | --- | --- | 
    Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional caption files and audio track files. |
    | Language | Select the language of the caption. |
    | Type | Select the type of caption that you are using.<br>**Subtitle** - The caption text displayed with the video that translates or transcribes the dialogue.<br>**Caption** - The caption text includes background noises and speaker identification. It also includes other relevant details alongside the translation or transcription of dialogue. This functionality makes the content more accessible to individuals who are deaf or hard of hearing. |
    | Label | The text that is displayed for the caption's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to a subtitle or caption track. For example, English (CC). |

    You can change or edit caption metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. (Optional) To add one or more audio tracks to a video, do the following:

    * Select **[!UICONTROL Upload Audio Tracks]**.
    * Navigate to, and select, one or more .mp3 files and open them.
    * To make audio tracks visible in the **[!UICONTROL Select audio or caption]** pop-up list on the media player, add the required details for each audio track file. Ensure you include all necessary information for proper display. Select the pencil icon to the right of an audio track file name. In the Edit Audio Track dialog box, enter the following required details, then select **[!UICONTROL Save]**. Repeat this process for each audio track file that you uploaded.

    | Audio Track metadata | Description |
    | --- | --- |
    | Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional audio track files or caption files.| 
    | Language | Select the language of the audio track. |
    | Type | Select the type of audio track that you are using.<br>**Original** - The audio track originally attached to the video and represented as `[Original]` in the label with English language selected by default. While **[!UICONTROL Label]** and **[!UICONTROL Language]** can be changed in the **[!UICONTROL Edit Audio Track]** dialog box, it defaults to the original values if the primary video is reprocessed.<br>**Standard** - An add-on audio track for a language other than the original.<br>**Audio description** - An audio track that also includes a descriptive narration of non-verbal actions and gestures in the video, making content more accessible for individuals who are visually impaired. |
    | Label | The text that is displayed as the audio track's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to an audio track. For example, `English [Original]`. The label of audio attached to a video is set to `[Original]` by default. |

    You can change or edit this audio track metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. In the upper-right corner of the page, from the **[!UICONTROL Save & Close]** drop-down list, select **[!UICONTROL Save]**. The files are uploaded and metadata processing begins, as seen in the Status column of the interface.

    >[!NOTE]
    >
    >Based on the caching settings of your instance, the metadata processing can take several minutes before it is reflected in preview and in published URLs.

1. (Optional) If you selected **[!UICONTROL Save & Close]** in the previous step, instead of selecting **[!UICONTROL Save]**, you can still view the processing status of the uploaded files. See [View the lifecycle status of uploaded caption and audio track files](/help/assets/dynamic-media/video.md#lifecycle-status-video).

1. (Optional) Preview the video before publishing to ensure the captions and audio work as expected. See [Preview a video that has multiple captions and audio tracks](/help/assets/dynamic-media/video.md#preview-video-audio-subtitle).

1. Publish the video. See [Publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md). -->






