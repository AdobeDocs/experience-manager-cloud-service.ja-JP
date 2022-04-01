---
title: 転写サービスの設定
seo-title: Configure transcription service
description: Adobe Experience Manager Assets は、 [!DNL Azure Media Services] WebVTT(Vtt) 形式のサポートされているオーディオまたはビデオファイル内の音声言語のテキストトランスクリプトを自動的に生成します。
seo-description: When an audio or video asset is processed in Experience Manager Assets, the AI-based transcription service automatically generates the text transcript rendition of the audio or video asset and stores it at the same location within your Assets repository where the original asset resides. The Experience Manager Assets transcription service allows marketers to effectively manage their audio and video content with added discoverability of the text content as well as increase the ROI of these assets by supporting accessibility and localization.
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
source-git-commit: feef8159a01393baebe11c014ae6093b79df72d1
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 3%

---


# での転写の設定 [!DNL Experience Manager Assets] {#configure-transcription-service}

転写とは、音声認識技術を使用して、音声またはビデオファイルから音声をテキスト（音声からテキスト）に変換するプロセスです。
[!DNL Adobe Experience Manager Assets] 次を使用して設定 [!DNL Azure Media Services] WebVTT(.vtt) 形式のサポートされているオーディオまたはビデオファイルで、音声言語のテキストトランスクリプトを自動的に生成します。 オーディオまたはビデオアセットがで処理されたとき [!DNL Experience Manager Assets]を使用すると、トランスクリプションサービスはオーディオまたはビデオアセットのテキストトランスクリプトレンディションを自動的に生成し、元のアセットが存在する Assets リポジトリ内の同じ場所に保存します。 この [!DNL Experience Manager Assets] 転写サービスを使用すると、マーケターは、アクセシビリティとローカライゼーションをサポートすることで、テキストコンテンツの発見性を高め、オーディオとビデオのコンテンツを効果的に管理できるほか、アセットの ROI を向上できます。

トランスクリプトは、音声コンテンツのテキストバージョンです。例えば、OTT プラットフォームで視聴している映画です。多くの場合、アクセシビリティに役立つキャプションやサブタイトルを含めたり、他の言語でのコンテンツの使用に役立ちます。 または、マーケティング、学習、エンターテイメントの目的で使用される任意のオーディオまたはビデオファイル。 これらのエクスペリエンスは、最初に転写を使用し、必要に応じて書式設定または翻訳します。 オーディオやビデオの書き起こしは、手動で行う場合に時間がかかり、エラーが発生しやすいプロセスです。 また、オーディオビデオコンテンツのニーズが増え続ける中で、手動プロセスを拡大するのも課題です。 [!DNL Experience Manager Assets] は Azure の AI ベースの転写を使用し、オーディオおよびビデオアセットの高度な処理を可能にし、タイムスタンプの詳細と共にテキストの転写（.vtt ファイル）を生成します。 転写機能は、Assets と共にDynamic Mediaでもサポートされています。

転写機能は、 [!DNL Experience Manager Assets]. ただし、管理者には、でトランスクリプションサービスを設定するためにユーザーの Azure 資格情報が必要です [!DNL Experience Manager Assets]. また、 [体験版資格情報を取得する](https://azure.microsoft.com/en-us/pricing/details/media-services/) Microsoft®から直接アセットでオーディオまたはビデオの転写機能を体験できます。

## 転写の前提条件 {#prerequisites}

1. 起動および実行 [!DNL Experience Manager Assets as a Cloud Service] インスタンス。
1. での設定には、次の Azure 資格情報が必要です。 [!DNL Experience Manager Assets]:

   * クライアント ID（API キー）
   * クライアント秘密鍵
   * テナントエンドポイント（ドメイン）
   * メディアアカウント
   * リソースグループ
   * 購読 ID

   詳しくは、 [Azure ドキュメント](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal) Azure Media Services API にアクセスするための資格情報を取得するには、以下を実行します。

1. 新しい要求を処理するのに十分なクレジットが Azure アカウントにあることを確認します。

## での転写の設定 [!DNL Experience Manager Assets] {#configure-transcription}

の転写機能を有効にするために必要な設定を次に示します。 [!DNL Experience Manager Assets]:

1. [Azure Media Services の設定](#configure-azure-media-service)
1. [オーディオ/ビデオの転写の処理プロファイルの設定](#configure-processing-profile-for-transcription)


### Azure Media Services の設定 {#configure-azure-media-services}

[!DNL Experience Manager Assets] は [!DNL Azure Media Services] これは、 [サポートされているオーディオまたはビデオファイル](#supported-file-formats-for-transcription) を WebVTT(.vtt) 形式で設定します。 管理者は [!DNL Azure Media Services] in [!DNL Experience Manager Assets] Azure の資格情報を使用します。 この [転写前提条件](#transcription-prerequisites) リスト [!DNL Azure] 設定に必要な資格情報。 次の条件を満たしていない場合、 [!DNL Azure] アカウントと資格情報： [Azure Media Services ドキュメント](https://azure.microsoft.com/en-us/pricing/details/media-services/) をクリックして体験版の資格情報を取得します。

![configure-transcription-service](assets/configure-transcription-service.png)

に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Media Services の設定]**. 左側のレールからフォルダー（ロケーション）を選択し、 [!UICONTROL 作成] ボタンをクリックして、 [!DNL Azure] アカウント このフォルダーは、 [!DNL Azure] クラウド設定は、Experience Manager Assetsに保存されます。 次を入力します。 [!DNL Azure] 認証情報をクリックします。 **[!UICONTROL 保存して閉じる]**.

### 転記の処理プロファイルを設定 {#configure-processing-profile}

一度 [!DNL Azure Media Services] はExperience Manager Assetsで設定され、次の手順では、オーディオおよびビデオアセットの AI ベースの転写を生成するためのアセット処理プロファイルを作成します。 AI ベースの処理プロファイルは、 [サポートされているオーディオまたはビデオアセット](#supported-file-formats-for-transcription) をExperience Manager Assetsでレンディションとして使用し、元のアセットが存在する同じフォルダーにトランスクリプト（.vtt ファイル）を保存します。 したがって、ユーザーがアセットとそのトランスクリプトレンディションを簡単に検索して見つけることができます。

に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL 処理プロファイル]** をクリックし、 **[!UICONTROL 作成]** ボタンをクリックして、オーディオおよびビデオファイルの転写を生成する AI ベースの処理プロファイルを作成します。 デフォルトでは、処理プロファイルページに表示されるタブは 3 つ（「画像」、「ビデオ」、「カスタム」）のみです。 ただし、 **[!UICONTROL コンテンツ AI]** 設定済みの場合は、「 」タブが表示されます。 [!DNL Azure Media Services] の [!DNL Experience Manager Assets] インスタンス。 確認する [!DNL Azure] 資格情報が表示されない場合 **[!UICONTROL コンテンツ AI]** 」タブをクリックします。

内 **[!UICONTROL コンテンツ AI]** タブで、 **[!UICONTROL 新規追加]** ボタンをクリックして、転写を設定します。 ここでは、ドロップダウンリストからファイルタイプを選択して、トランスクリプトを生成するためのファイル形式（MIME タイプ）を含めたり除外したりすることができます。 次の図では、サポートされているすべてのオーディオおよびビデオファイルが含まれ、テキストファイルは除外されています。

を有効にします。 **[!UICONTROL 同じディレクトリに VTT トランスクリプトを作成]** トランスクリプトレンディション（.vtt ファイル）を作成し、元のアセットが存在する同じフォルダーに保存することを切り替えます。 他のレンディションも、この設定に関係なく、デフォルトの DAM アセット処理ワークフローで生成されます。

![configure-transcription-service](assets/configure-transcription-profile.png)

次の図は、Experience Manager Assetsで作成されたカスタムビデオプロファイルの詳細を示しています。

![configure-transcription-service](assets/video-processing-profile.png)

ビデオプロファイルには、次のカスタム設定も含まれています。 詳しくは、 [処理プロファイルドキュメント](/help/assets/asset-microservices-configure-and-use.md) を参照してください。

![configure-transcription-service](assets/video-processing-profile2.png)

次に、このビデオプロファイルで転写を設定しましょう。 次に移動： **[!UICONTROL コンテンツ AI]** 」タブで、 **[!UICONTROL 新規追加]** 」ボタンをクリックします。 すべてのオーディオおよびビデオファイルを含め、画像およびアプリケーションファイルを除外します。 を有効にします。 **[!UICONTROL 同じディレクトリに VTT トランスクリプトを作成]** 設定を切り替えて保存します。

![configure-transcription-service](assets/video-processing-profile1.png)

オーディオおよびビデオファイルの書き起こし用に処理プロファイルを設定したら、次のいずれかの方法を使用して、この処理プロファイルをフォルダーに適用できます。

* で処理プロファイルの定義を選択 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL 処理プロファイル]**、およびを使用します。 **[!UICONTROL プロファイルをフォルダーに適用]** アクション。 コンテンツブラウザーを使用すると、特定のフォルダーに移動し、フォルダーを選択して、プロファイルの適用を確定できます。
* Assets ユーザーインターフェイスでフォルダーを選択し、 **[!UICONTROL プロパティ]** アクションを使用して、フォルダーのプロパティを開きます。 次をクリック： **[!UICONTROL アセット処理]** 」タブをクリックし、そのフォルダーに適した処理プロファイルを「 **[!UICONTROL 処理プロファイル]** リスト。 変更を保存するには、「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![configure-transcription-service](assets/video-processing-profile3.png)

* ユーザーは、Assets ユーザーインターフェイスでフォルダーまたは特定のアセットを選択して処理プロファイルを適用し、「 」を選択できます **[!UICONTROL アセットを再処理]** 」オプションを使用して、上部にあるオプションから選択します。

>[!TIP]
>1 つのフォルダーに適用できる処理プロファイルは 1 つだけです。
>
>処理プロファイルをフォルダーに適用すると、このフォルダーまたはそのサブフォルダー内の新しいアセットがすべて、設定された追加の処理プロファイルを使用して処理されます（または更新）。 この処理は、標準のデフォルトプロファイルによる処理に加えて行われます。

>[!NOTE]
>
>フォルダーに適用された処理プロファイルはツリー全体で機能しますが、サブフォルダーに適用された別のプロファイルでオーバーライドすることもできます。
>
>アセットがフォルダーにアップロードされると、Experience Managerは、そのフォルダーのプロパティと通信して、処理プロファイルを識別します。 何も適用されない場合は、適用する処理プロファイルが階層内の親フォルダーで確認されます。


## オーディオまたはビデオアセットの転写を生成する {#generate-transcription}

ビデオアセットを処理する際に、 [AI ベースの処理プロファイル](#configure-processing-profile-for-transcription) は、同じフォルダー内の元のアセットと共に、トランスクリプト（.vtt ファイル）をレンディションとして自動的に生成します。

![configure-transcription-service](assets/transcript1.png)

また、元のビデオアセットのレンディションにアクセスして、トランスクリプトレンディションを表示することもできます。 次の手順で **[!UICONTROL レンディション]** パネルで、元のビデオアセットを選択し、左側のパネルを開きます。 トランスクリプトレンディション（.vtt ファイル）が **[!UICONTROL TRANSCRIPTVTT]** 頭

![configure-transcription-service](assets/transcript.png)

トランスクリプト（.vtt テキストファイル）を別のアセットレンディションとしてフォルダーから、または **[!UICONTROL レンディション]** 元のアセットのパネル（アセットのすべてのレンディションをダウンロードする）

現在、Experience Managerは VTT ファイルの全文プレビューや編集をネイティブではサポートしていません。 ただし、トランスクリプトのレンディションをダウンロードし、任意のテキストエディターを使用して、トランスクリプトを編集または検証できます。 トランスクリプトは、ビデオ内の指定されたタイムスタンプのテキストとしての話し言語を、転写の信頼性スコア（精度）と共に反映します。

![configure-transcription-service](assets/transcript-text.png)

## Dynamic Mediaでの転写の使用 {#using-transcription-in-dynamic-media}

次の場合： [設定済みのDynamic Media](/help/assets/dynamic-media/config-dm.md) Experience Manager Assetsインスタンスで、アセット（オーディオまたはビデオファイル）とそのトランスクリプト（.vtt ファイル）をDynamic Mediaに公開できます。 これにより、元のアセット（オーディオまたはビデオファイル）とその転写レンディション（.vtt ファイル）が、同じフォルダー内のDynamic Mediaに公開されます。 Dynamic Media管理者が実行できる操作 [CC クローズドキャプションエクスペリエンスを有効にする](/help/assets/dynamic-media/video.md#adding-captions-to-video) トランスクリプトレンディション（.vtt ファイル）を使用するオーディオまたはビデオファイルの場合。

関連トピック：

* [CC クローズドキャプションをDynamic Mediaに追加する方法に関するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html#add-cc-closed-captioning-to-dynamic-media-video)
* [YouTubeへのDynamic Mediaビデオの公開](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

次の図では、URL は、トランスクリプト（.vtt ファイル）を参照するキャプション部分を反映しています。 このビデオは、読み上げ言語（テキストの転写）を **[!UICONTROL クローズドキャプション]** ビデオ内の指定されたタイムスタンプ。 ユーザーは、 **[!UICONTROL CC]** 」ボタンをクリックします。

![configure-transcription-service](assets/transcript-example.png)

## 転記でサポートされているファイル形式 {#supported-file-format}

次のオーディオおよびビデオファイル形式が転写でサポートされています。

| サポートされるオーディオ/ビデオ形式 | 拡張 |
|----|----|
| FLV （H.264 および AAC コーデックを使用） | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS、MPEG2-TS、3GP | (.ts, .ps, .3gp, .3gpp, .mpg) |
| Windows Media ビデオ (WMV)/ASF | (.wmv, .asf) |
| AVI（非圧縮 8 ビット/10 ビット） | (.avi) |
| MP4 | （.mp4、.m4a、.m4v） |
| Microsoft®デジタルビデオ録画 (DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| QuickTime | (.mov) |


>[!NOTE]
>
>アプリケーションタイプのアセット（オーディオまたはビデオファイル）は、転写に対してサポートされていません。

## 既知の制限事項 {#known-limitations}

* 転写機能は、最長 10 分のビデオに対してサポートされます。
* ビデオタイトルは 80 文字未満にする必要があります。
* サポートされるファイルサイズは最大 15 GB です。
* サポートされる最大処理時間は 60 分です。
* 有料 [!DNL Azure] アカウントに保存する場合、1 分あたり最大 50 本のムービーをアップロードできます。 ただし、体験版アカウントでは、1 分あたり最大 5 本のムービーをアップロードできます。

## トラブルシューティングのヒント {#troubleshooting}

にログインします。 [!DNL Azure Media Services] 同じ資格情報（設定に使用済み）を持つアカウントを使用して、リクエストのステータスを検証します。 連絡先 [!DNL Azure] リクエストが正常に処理されなかった場合に対応します。



