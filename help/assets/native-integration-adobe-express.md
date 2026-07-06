---
title: Content AdvisorからAdobe ExpressのAEM Assetsにアクセスする
description: Content Advisorを使用すれば、Adobe Expressとのネイティブな連携の中で、AEM Assetsを直接検索してアクセスできます。
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '4378'
ht-degree: 12%

---

# Content AdvisorからAdobe ExpressのAEM Assetsにアクセスする {#native-integration-adobe-express-using-content-advisor}

Adobe Experience Manager（AEM）Assetsは、Adobe Expressとネイティブに統合されているため、コンテンツアドバイザーを使用して、AEM AssetsからアセットをExpress インターフェイス内で直接検索、アクセス、使用できます。

Content Advisorは、コンテキストに即したインテリジェントなアセット検出をクリエイティブワークフローに直接提供することで、Adobe Expressでのアセットの検出および使用方法を変革します。 キーワードを入力してアセットを検索する代わりに、コンテンツアドバイザーは、キャンバスのコンテンツ、キャンペーンの概要、意図にもとづいて、関連性の高い承認済みアセットを表示するため、適切なアセットをすばやく見つけることができます。

Content Advisorを利用すれば、スマートな提案、ダイナミックメディアのレンディション、アセットのメタデータへの完全な可視性などにより、Adobe Expressから直接、AEM Assetsのアセットを効率的に検索、評価、利用できます。 これにより、コンテンツの制作を高速化し、アセットの再利用を促進して、承認済みのブランドに即したアセットを一貫して使用できます。

![Content Advisor バナー画像](assets/content-advisor-banner-image.png)

また、アセットをExpress キャンバスに配置し、新しいコンテンツや編集したコンテンツをAEM Assetsに保存して、アセット管理とガバナンスを一元化することもできます。 Adobe Expressとのネイティブ統合には、次のような主な利点があります。

* コンテキストに応じたアセットの発見とレコメンデーションにより、コンテンツ制作を加速。

* 既存のアセットを編集し、新しいアセットをAEM Assetsに保存することで、コンテンツの再利用を促進。

* チャネルに合わせて最適化された承認済みのDynamic Media レンディションへの迅速なアクセス。

* ブランドの一貫性を維持しながら、新しいアセットやバージョンの作成にかかる時間と労力を削減。

## 前提条件 {#prerequisites}

AEM Assets 内の Adobe Express と 1 つ以上の環境にアクセスする権限。 Assets as a Cloud Service リポジトリのいずれかを使用できます。

## Adobe Express エディターでの AEM Assets の使用 {#use-aem-assets-in-express}

Adobe Express エディターで AEM Assets の使用を開始するには、次の手順を実行します。

1. Adobe Express web アプリケーションを開きます。

2. 新しいテンプレートまたはプロジェクトを読み込むか、アセットを作成して、新しい空のキャンバスを開きます。

3. 左側のナビゲーションパネルで「**[!UICONTROL アセット]**」をクリックします。 Adobe Expressには[Content Advisor](#intelligent-asset-discovery-content-advisor)が表示され、アクセス権限のあるリポジトリと、ルートレベルで使用可能なアセットとフォルダーのリストが一覧表示されます。

4. [Content Advisor](#intelligent-asset-discovery-content-advisor)を使用してリポジトリ内のアセットを参照または検索し、キャンバスにドラッグ&amp;ドロップします。 または、アセットをクリックしてカンバスに配置します。 また、承認ステータス、ファイルタイプ、MIME タイプ、ディメンションなど、様々な条件で![ フィルター](assets/do-not-localize/filter.svg) アセットをフィルタリングすることもできます。

   >[!NOTE]
   >
   >ディメンションによるフィルターは、ビデオには適用されません。

   ![Assets アドオンのアセットを含める](assets/native-express-content-advisor-home.png)

## Content Advisorによるインテリジェントなアセット発見 {#intelligent-asset-discovery-content-advisor}

Content Advisorは、キャンバスのコンテンツやキャンペーン概要にもとづいて、コンテキストに即したインテリジェントなレコメンデーションを使用して、適切なアセットを見つけるのに役立ちます。 また、ユースケースに最適化された、チャネル対応のDynamic Media レンディションを選択することもできます。


コンテンツアドバイザーは、リストビューとグリッドビューにファイル、フォルダー、コレクションのリストを表示します。 PNG、JPEG、PSD、MP4、SVGおよびPDF形式のアセットをExpress キャンバスに追加できます。 また、アセットカードにある![情報アイコン ](assets/info-icon.svg) アイコンをクリックすると、スクロール可能なPDF ファイルやその他の種類のフォーマットをプレビューできます。

![情報アイコン ](assets/info-icon.svg) アイコンをクリックして、**[!UICONTROL 基本]** タブで利用可能なアセットメタデータを表示するか、[Dynamic Media](#dynamic-media-renditions-content-advisor) タブで利用可能なDynamic Media レンディションを表示します。 提案されたコンテンツをキャンバスにドラッグ&amp;ドロップします。 または、アセットをクリックして、自動的にカンバスに配置します。

![Adobe Expressのアセットメタデータ ](assets/express-native-integration-metadata.png)


>[!IMPORTANT]
> 
>**リポジトリ** ドロップダウンリストから&#x200B;**作成者** リポジトリを選択してください。 **配信** リポジトリにContent Advisor機能が表示されません。
>
> また、**配信** リポジトリには、フォルダーとコレクションで整理されたアセットがありません。 すべてのアセットは、ルートレベルでフラットな構造で表示されます。

Content Advisorには、次の主な機能が用意されています。

* [AI 検索を活用し、よりスマートなアセットの発見を実現](#content-advisor-ai-search)

* [コンテキストと意図にもとづくスマートな提案](#smart-suggestions-content-advisor)

* [適切なアセットを見つけるためのキャンペーン概要](#campaign-briefs-content-advisor)

* [使用できるDynamic Media アセットのレンディション](#dynamic-media-renditions-content-advisor)

* [Assetsのビューと一致したアセットのメタデータへのアクセス](#asset-metadata-content-advisor)

* [Assets ビューと一致したフィルターへのアクセス](#filters-content-advisor)

* [最近の検索と保存した検索にアクセスして再利用](#saved-searches-content-advisor)

* [コレクション間およびコレクション内のアセットの検索](#search-collections-content-advisor)

### AI 検索を活用し、よりスマートなアセットの発見を実現 {#content-advisor-ai-search}

Content Advisorは、正確なキーワード一致に依存するのではなく、ユーザーのクエリの背後にある意味と意図を理解する高度な検索機能を使用します。 AI （人工知能）とマシンラーニング（機械学習）を利用して、より正確でコンテキストに即した結果を提供します。

従来のキーワードベースの検索では、正確な用語を検索しますが、AI 検索は、単語、概念、ユーザーの意図の間の関係を解釈します。 これにより、クエリの表現が異なる場合や、入力ミスが含まれる場合、別の言語である場合でも、ユーザーが探しているものを確実に見つけることができます。

![Adobe ExpressのアセットのAI 検索](assets/express-native-integration-ai-search.png)

主なメリットには、次のようなものがあります。

* 多言語サポート：正確な翻訳を必要とせずに、複数の言語を検索できます。 ユーザーは、クエリ言語に関係なく、関連するコンテンツを見つけることができます。

* 誤字の処理：タイプミスやスペルミスを解釈して、入力に不備がある場合でも正確な結果を得ることができます。

* 類義語の理解：関連する用語やフレーズに対して結果を提供するため、ユーザーは適切なキーワードを推測する必要がありません。

* コンテキストに応じた検索：正確な単語だけでなく、クエリの背後にある意図を認識します。

>[!IMPORTANT]
> 
>* Content Advisor内のAI 検索にアクセスするために必要なAEM リリースの最小バージョンは`21994`です。


### コンテキストと意図にもとづくスマートな提案 {#smart-suggestions-content-advisor}

Content Advisorは、Express キャンバス内のコンテンツのコンテキストと意図に基づいてスマート提案を表示します。 これにより、時間のかかる手作業での検索をおこなうことなく、コンテンツニーズに即したアセットをすばやく見つけ出して使用できます。

![Adobe ExpressでContent Advisorの推奨コンテンツ ](assets/express-native-integration-suggested-content.png)

>[!IMPORTANT]
> 
>* コンテンツアドバイザーは、テキストレイヤーまたはExpress キャンバスのタイトルで使用可能なコンテンツのコンテキストと意図に基づいて、スマート提案を表示します。 カンバスで使用可能な画像に基づく結果は表示されません。
>* Content Advisor内でこの機能にアクセスするには、GenAI ライダーに署名する必要があります。 GenAI ライダーに署名するには、Adobe担当者にお問い合わせください。
>* この機能にアクセスするために必要なAEM リリースの最小バージョンは`21994`です。
>* スマート提案は、キャンバスを更新しても自動的には更新されません。 **おすすめコンテンツ** パネルの更新アイコンをクリックすると、更新された候補のリストが表示されます。

### 適切なアセットを見つけるためのキャンペーン概要 {#campaign-briefs-content-advisor}

Content Advisorを使用すると、検索キーワードを手動で入力しなくても、キャンペーン概要ドキュメントをアップロードして関連アセットを見つけることができます。 Content Advisorは、施策概要の情報を分析し、施策の意図を把握して、AEM Assetsで利用可能な関連アセットを提案します。

![Assets アドオンのアセットを含める](assets/upload-brief-native-express.png)

>[!IMPORTANT]
>
>* コンテンツアドバイザーは、キャンペーン概要のテキストとして利用できる情報を分析し、関連するアセットを提案します。 キャンペーン概要で画像として利用できる情報は分析されません。
>* キャンペーン概要としてアップロードできるサポートされているファイルタイプには、PDF、DOCX、TXT ドキュメントがあります。
>* Content Advisor内でこの機能にアクセスするには、GenAI ライダーに署名する必要があります。 GenAI ライダーに署名するには、Adobe担当者にお問い合わせください。
>* この機能にアクセスするために必要なAEM リリースの最小バージョンは`21994`です。

### 使用できるDynamic Media アセットのレンディション {#dynamic-media-renditions-content-advisor}

Dynamic Mediaのレンディションは、[画像プリセット ](/help/assets/dynamic-media/managing-image-presets.md)、[ スマート切り抜き](/help/assets/dynamic-media/image-profiles.md)、形式タイプ、カラープロファイルなど、チャネルに合わせて最適化された、すぐに使用できるバージョンのアセットを提供します。 これらのレンディションにより、選択したアセットが手作業による編集やアセットの複製を必要とせずに、チャネルやデザイン要件を満たしていることを確認できます。

また、レンディションをExpress キャンバスに配置する前に、Dynamic Media修飾子をリアルタイムでプレビューして、アセットの一貫性と品質を維持しながら、最も適切なレンディションをより迅速に選択できます。

アセットカードの![情報アイコン ](assets/info-icon.svg) アイコンをクリックし、**[!UICONTROL Dynamic Media]** タブを選択して、アセットで使用可能なレンディションを表示します。 [Dynamic Media Scene7](/help/assets/dynamic-media/dynamic-media.md) レンディションまたは[Dynamic Media with OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) レンディションを表示するように選択できます。 アセットに&#x200B;**[!UICONTROL OpenAPI]**&#x200B;を選択すると、使用可能なレンディションは、アセットが承認され、OpenAPIを使用してDynamic Mediaで使用可能な場合にのみ表示されます。

Dynamic Media タブを表示するには、有効なAEM Dynamic Media ライセンスが必要です。

![Dynamic Media レンディションを表示](assets/native-express-dynamic-media.png)

![ プレビューアイコン ](assets/do-not-localize/preview-icon.svg) アイコンをクリックしてレンディションをプレビューするか、レンディション名をクリックして自動的にカンバスに配置します。 レンディションをプレビューしてからドラッグ&amp;ドロップして、画像をカンバスに配置することもできます。

![Dynamic Media レンディションのプレビュー](assets/native-express-dynamic-media-preview.png)

「**[!UICONTROL 修飾子を追加]**」をクリックし、テキストボックスに修飾子を指定してEnter キーを押し、変換をリアルタイムでレンディションに適用します。 同様に、レンディションに複数の修飾子を追加し、それらの変換をプレビューすることもできます。 プレビューからキャンバスにアセットをドラッグ&amp;ドロップします。 これらの修飾子を適用した後のレンディションは保存されません。 [Dynamic Media Scene7](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference)および[Dynamic Media with OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat)でサポートされている修飾子の一覧を参照してください。

>[!IMPORTANT]
> 
>Dynamic Mediaは、大きなアセットの最適化されたレンディションを提供することで、Adobe Express（web）の80 MB アップロードファイルサイズの制限を克服するのに役立ちます。 Dynamic Mediaのレンディションは、ビジュアル品質を保ちながらファイルサイズを大幅に削減します。 例えば、300 MBのTIFF アセットは、品質を損なうことなく2.5 MB レンディションとして配信でき、Adobe Expressで高解像度アセットを効率的に使用できます。

### Assetsのビューと一致したアセットのメタデータへのアクセス {#asset-metadata-content-advisor}

Content Advisorでは、Assets ビューで使用可能なメタデータを含む、AEM Assetsで定義されたアセットプロパティにアクセスできます。 Content Advisorは、Assets ビューと同じメタデータ設定を使用し、Assets ビューアセットの詳細ページのメタデータタブとコンテンツのリストをレプリケートします。 これにより、アセットを選択する前に、タイトル、説明、形式、サイズ、その他のメタデータなどの主要なアセットの詳細を確認できます。 アセットのプロパティにアクセスすることで、コンテンツに適した承認済みアセットを選択できます。

![Content Advisor](assets/native-express-asset-metadata.png)のAssets ビューメタデータ

アセットカードの![情報アイコン ](assets/info-icon.svg) アイコンをクリックし、**[!UICONTROL 基本]** タブを選択して、アセットのメタデータを表示します。 Assets ビューに存在するアセットメタデータと一致して、他のアセットメタデータタブ（製品、キャンペーン、タグなど）を表示することもできます。

Content Advisorは、ファイルのプロパティ（メタデータ）を読み取り専用ビューで表示します。 コレクションとフォルダーのプロパティは表示されません。

### Assets ビューと一致したフィルターへのアクセス {#filters-content-advisor}

Content Advisorには、Assets ビューで利用できるExpressと同じフィルタリング機能が用意されており、定義済みのフィルターを使用してアセットを絞り込むことができます。 Assets ビューと同じフィルタリング機能が、ファイル、フォルダー、コレクションなど、コンテンツタイプに固有のフィルターにも適用されます。 これにより、アセットを一貫して検索し、Adobe Express内で適切なアセットを効率的に見つけることができます。

フィルタースキーマを使用してAssets ビューでフィルターを設定していない場合、Content Advisorには、ファイルタイプ、ファイル形式、アセットステータス、ファイルサイズ、画像サイズ、画像の高さ、変更日、作成日など、すぐに使用できるフィルターが表示されます。

### 最近の検索と保存した検索にアクセスして再利用 {#saved-searches-content-advisor}

Assets ビューで作成された保存済みの検索も使用できるので、定義済みの検索条件を再利用できます。 保存済み検索は、ブラウザー間でAssets ビューとContent Advisorの間で一貫して機能します。 これにより、AEM AssetsとAdobe Express全体で一貫した検索パターンを使用して、アセットを効率的に見つけることができます。

コンテンツアドバイザーを使用して頻繁に使用する検索を保存するには：

1. 検索語（オプション）を指定し、フィルターアイコンをクリックし、要件に基づいてオプションを選択して検索クエリを作成します。

1. **[!UICONTROL 適用]**&#x200B;をクリックして結果を表示します。

1. フィルターアイコン/**保存済み検索を管理**/**新しい保存済み検索を作成**&#x200B;をクリックします。

1. 検索の名前を指定し、![情報アイコン ](assets/do-not-localize/checkmark-icon.svg)をクリックして保存します。 検索が項目のリストに表示されます。

   ![保存された検索コンテンツ アドバイザー](assets/native-express-saved-searches.png)

保存した検索項目のいずれかを適用するには、フィルターアイコンをクリックし、**[!UICONTROL 保存済み検索項目]** ドロップダウンリストから検索項目を選択して、**[!UICONTROL 適用]**&#x200B;をクリックします。

Content Advisorは、最近検索した項目を保存し、頻繁に使用する項目を保存して、後ですばやくアクセスできるようにします。 Assets ビューとContent Advisorの間で、最近検索した内容のリストが一致しません。 同じユーザーが、Assets ビューとContent Advisorで異なる最近検索セットを持つことができます。 シークレットモードを使用してContent Advisorにアクセスする場合、最近検索した項目のリストは使用できません。 また、最近検索した内容は、同じユーザーに対して異なるブラウザー間で共有されず、AEM環境に固有です。



Assets ビューで使用できるデフォルトの保存済み検索機能は、コンテンツアドバイザーではまだ使用できません。

### コレクション間およびコレクション内のアセットの検索 {#search-collections-content-advisor}

Content Advisorを使用すると、すべてのコレクション間でアセットまたはコレクションを検索したり、特定のコレクションに検索を制限したりできます。 これにより、組織のコンテキストを維持しながら、厳選されたコレクションからアセットをすばやく見つけ出して使用することができます。

## AEM アップロードを使用した画像の置き換え {#replace-image-using-aem-upload}

さらに、**[!UICONTROL AEM アップロード]**&#x200B;を使用して、追加した画像を置き換えることができます。 これを行うには、次の手順を実行します。

1. アセットを参照または検索し、キャンバスにドラッグ&amp;ドロップします。

1. 置き換える画像を選択します。 **[!UICONTROL 置換]**&#x200B;をクリックし、その他の様々なオプションの中から&#x200B;**[!UICONTROL AEM Assets]**&#x200B;を選択します。

   ![AEM Replace](assets/aem-replace.png)

1. 左側のナビゲーションペインで[ コンテンツアドバイザー](#intelligent-asset-discovery-content-advisor)が開きます。 Adobe Express には、アクセス権が付与されたリポジトリのリストとルートレベルで使用可能なアセットおよびフォルダーのリストが表示されます。 そこからアセットを選択してキャンバス上で置換をプレビューし、**[!UICONTROL 置換]**&#x200B;をクリックして確定します。

   >[!NOTE]
   >
   > SVGのファイル形式はサポートされていません。

## AEM Assets での Adobe Express プロジェクトの保存 {#save-express-projects-in-assets}

Express キャンバスに適切な修正を組み込んだ後、AEM Assetsに保存できます。

1. 「**[!UICONTROL 共有]**」をクリックして、**[!UICONTROL 共有]**&#x200B;ダイアログを開きます。

   ![AEM でのアセットの保存](assets/adobe-express-share.png)

2. **AEM Assets**&#x200B;を選択します。 Adobe Express にアップロードダイアログが表示されます。

3. 「**現在のページ**」または「**すべてのページ**」を選択します。 書き出すアセットの名前と形式を指定します。 キャンバスのコンテンツは、PNG、JPEG、PDF、MP4、MP4+PNG、または MP4+JPEG 形式で書き出すことができます。 形式は、キャンバスページのアセットに基づいて自動的に調整されます。「**現在のページ**」を選択すると、現在のページのアセットが宛先フォルダーに保存されます。 「**すべてのページ**」を選択し、書き出す形式が PDF でない場合、すべてのキャンバスページは、宛先フォルダー内の新しいフォルダーに個別のファイルとして保存されます。 書き出す形式が PDF の場合、すべてのキャンバスページが 1 つの PDF ファイルとして宛先フォルダーに保存されます。

4. **宛先フォルダー**&#x200B;の下にあるフォルダーアイコンをクリックして場所を選択し、アセットを保存します。

   ![AEM でのアセットの保存](/help/assets/assets/page-selection-and-destination-folder.png)

5. オプション：「**プロジェクトまたはキャンペーン名**」フィールドを使用して、アップロード用のキャンペーンメタデータを追加できます。 既存の名前を使用するか、新しい名前を作成できます。 アップロードには、複数のプロジェクト名またはキャンペーン名を定義できます。 名前を登録するには、名前を入力して Enter キーを押すだけです。ベストプラクティスとして、アドビでは、アップロードしたアセットの検索エクスペリエンスを強化すると共に、残りのフィールドに値を指定することをお勧めします。

6. 同様に、「**[!UICONTROL キーワード]**」フィールドと「**[!UICONTROL チャネル]**」フィールドの値を定義します。

7. 「**[!UICONTROL アップロード]**」をクリックして、AEM Assets にアセットをアップロードします。

   >[!NOTE]
   >
   > アセットをContent Hub配信リポジトリに保存する場合、プロジェクト名またはキャンペーン名は必須フィールドです。 また、この場合はメタデータから自動的に派生するので、宛先フォルダーを選択する必要はありません。

## サポートされているファイル形式 {#supported-file-formats-import-assets}

Adobe Expressは、[最小必要な画像の確認](https://helpx.adobe.com/express/web/image-creation-and-editing/change-file-formats/image-requirements.html)で使用できる形式をネイティブでサポートしています。 ただし、AEM Assetsでは次のフォーマットの種類をサポートしています。

| サポートされる形式 | 最大ディメンション/解像度 | 最大ファイルサイズ |
|------------------|---------------------------------------------|---------------|
| JPEG | 65 MP （8K × 8Kまたは16K × 4Kなど） | 80 MB デスクトップ、40 MB モバイル |
| PNG | 65 MP （8K × 8Kまたは16K × 4Kなど） | 80 MB デスクトップ、40 MB モバイル |
| SVG | — | 250 KB |
| MP4 | 3840 × 3840 ピクセル | 200 MB |
| PSD | 65 MP （8K × 8Kまたは16K × 4Kなど） | 80 MB デスクトップ、40 MB モバイル |
| PDF | — | — |


## 制限事項 {#limitations}

1. 読み込みと書き出しの場合、サポートされるビデオファイルのタイプは MP4 です。

2. **MP4 ビデオの読み込み**&#x200B;の場合、背景が透明なビデオ（アルファチャンネル）はサポートされません。
   <!--
   1. The maximum file size supported is 200 MB. If this limit exceeds, an alert message displays.
   2. The maximum supported resolution is 3840 X 3840 pixels.
   3. Videos with transparent backgrounds (alpha channel) are not supported.
   -->

3. **MP4 ビデオの書き出し**&#x200B;の場合、サポートされる最大ファイルサイズは 200 MB です。 この制限を超えると、ビデオを 200 MB 以下にトリミングするか、ダウンロード後に AEM Assets の宛先フォルダーに手動でアップロードすることを提案するアラートが表示されます。

<!--
## Content Advisor Properties {#content-advisor-props}

You can configure following properties for the content advisor:

* `featureSet` : This property enables the Content Advisor MFE.

    ```
    featureSet: [
        ...defaultFeatures, /* to include all default features */
        'advisor', /* enables Content Advisor features */
        'content-fragments', /* enables Content Fragments */
    ],
    ```

* `rail:true/false` : If marked true, Content Advisor is rendered in a left rail view. If it is marked false, the Content Advisor is rendered in modal view.

## Browse assets using Content Advisor {#browse-assets-content-advisor}

<!--In the Modal View of Content Advisor, you can access both [Assets](#using-assets-tab) and [Content Fragments](#using-content-fragments) within a unified interface.

### Assets tab{#assets-tab}

The **[!UICONTROL Assets]** tab allows you to browse or filter available assets, preview them before selection, and choose appropriate **[!UICONTROL Dynamic Media]** [renditions](renditions.md) or [smart crops](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles) as needed. Assets, folders, and collections are presented together in a single, streamlined experience. The interface also provides contextual recommendations based on the integrated application context, helping you quickly identify relevant content.

Within assets tab, you can access content by browsing [Files and folders](#content-advisor-files-and-folders) or viewing [Collections](#content-advisor-collections).

### Files and Folders tab{#content-advisor-files-and-folders}

Browsing content using Files and Folders allows you navigate your assets in a familiar hierarchical structure, making it easy to locate assets within the repository. To browse assets within files and folders, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Files & Folders]**. A hierarchical structure is then displayed, allowing you to easily locate and select the desired assets.

![Browse assets using files and folder](assets/browse-assets-content-advisor.png)

### Collections tab{#content-advisor-collections}

Browsing content using Collections allows you to access curated groups of assets within Collections. To browse assets within Collections, navigate to the **[!UICONTROL Assets]** tab and select **[!UICONTROL Collections]**. The interface then displays curated groups of assets, enabling you to browse the content you need.

![Browse assets using Collections](assets/browse-assets-collections.png)

<!--
### Content Fragments tab{#content-fragments}

The [Content Fragments](/help/assets/content-fragments/content-fragments.md) tab displays structured assets, allowing you to browse, search, and filter fragments efficiently within the same interface. To browse assets using Content Fragments, navigate to the **[!UICONTROL Content Fragments]** tab to access and explore the fragments available in the repository.

![Browse assets using Content Fragments](assets/browse-assets-content-fragment.png)
-->

## よくある質問 {#frequently-asked-questions-content-advisor}

### AEM AssetsとAdobe Expressの連携におけるContent Advisorとは何ですか？ {#content-advisor-overview}

Content Advisorは、Adobe Express内のAEM Assetsとのネイティブな連携に組み込まれた、コンテキストに応じたインテリジェントなアセット発見機能です。 Adobe Expressのキャンバスのコンテンツ、キャンペーンの概要、クリエイティブの意図にもとづいて、関連性の高い承認済みアセットを表示します。手作業でキーワードを検索する必要はありません。 また、Content Advisorでは、Dynamic Mediaのレンディション、アセットのメタデータ、フィルター、保存された検索、コレクションにアクセスできるため、デザイナーはツールを切り替えることなく、Adobe Expressのインターフェイス内で直接AEM Assetsを検索、評価、使用できます。

### Adobe ExpressでAEM Assetsを使用するための前提条件は何ですか？ {#aem-assets-express-prerequisites}

Adobe ExpressでAEM Assetsを使用するには、Adobe Expressと1つ以上のAEM Assets環境にアクセスするための使用権限が必要です。 任意のAdobe Experience Manager Assets as a Cloud Service リポジトリを使用できます。 コネクタやプラグインの追加インストールは必要ありません。この統合はAdobe Expressネイティブです。

### Adobe Express エディターでAEM Assetsを使用するには、どうすればよいですか？ {#access-aem-assets-in-express}

Adobe ExpressでAEM Assetsの使用を開始するには、Adobe Express web アプリケーションを開き、新しい空白のカンバス、テンプレート、またはプロジェクトを開きます。 左側のナビゲーションパネルで「Assets」をクリックしてコンテンツアドバイザーを開きます。これにより、利用可能なリポジトリと、ルートレベルのアセットとフォルダーが表示されます。 アセットを参照または検索し、キャンバスにドラッグ&amp;ドロップするか、アセットをクリックして自動的に配置します。 Assetsは、承認ステータス、ファイルタイプ、MIME タイプ、ディメンションでフィルタリングすることもできます。 ディメンションによるフィルターは、ビデオアセットには適用されないことに注意してください。

### すべての機能にアクセスするには、コンテンツアドバイザーでどのリポジトリタイプを選択する必要がありますか？ {#content-advisor-repository-selection}

AI 検索、スマートサジェスト、キャンペーンブリーフ、Dynamic Mediaのレンディションなど、コンテンツアドバイザーのすべての機能にアクセスするには、オーサーリポジトリをコンテンツアドバイザーのリポジトリドロップダウンから選択する必要があります。 配信リポジトリにコンテンツアドバイザー機能が表示されない。 配信リポジトリ内のAssetsは、ルートレベルでのみフラット構造で表示されます。フォルダーやコレクションには整理されません。

### Content Advisorを使用して、Adobe Express キャンバスに追加できるファイル形式は何ですか？ {#content-advisor-supported-formats}

Content Advisorでは、PNG、JPEG、PSD、MP4、SVGおよびPDF形式のアセットをAdobe Express キャンバスに追加できます。 PDF ファイルをカンバスに配置する前に、アセットカードの情報アイコンをクリックすることで、スクロール可能なドキュメントとしてプレビューできます。 アセットのメタデータとDynamic Mediaのレンディションには、リストビューとグリッドビューの両方で、各アセットの情報アイコンからアクセスすることもできます。

### Content AdvisorのAI 検索の仕組み？ {#content-advisor-ai-search-faq}

Content AdvisorのAI 検索では、AI （人工知能）とマシンラーニング（機械学習）を利用して、キーワードを正確に一致させるのではなく、検索クエリの背後にある意味と意図を解釈します。 多言語のクエリをサポートし、誤字やタイプミスを処理し、類義語や関連する用語を理解し、ユーザーの意図に基づいてコンテキストに応じた結果を提供します。これにより、クエリが異なるフレーズや異なる言語で入力された場合でも、関連するアセットを見つけることができます。 Content Advisor内のAI 検索にアクセスするために必要な最小AEM リリースバージョンは21994です。

### Content Advisorのスマートな提案とは何ですか？また、どのようなコンテンツを分析しますか？ {#content-advisor-smart-suggestions-overview}

コンテンツアドバイザーのスマート提案は、テキストレイヤーのコンテキストと意図、またはAdobe Express キャンバスに存在するタイトルに基づいて、関連するアセットを自動的に表示します。 スマート提案は、キャンバス上のテキストコンテンツのみを分析します。キャンバスで使用可能な画像は分析しません。 スマート提案は、キャンバスが変更されても自動的に更新されません。提案されたコンテンツパネルの更新アイコンをクリックして、更新された提案のリストを表示します。 スマート提案にアクセスするために必要なAEM リリースバージョンの最小値は21994です。

### コンテンツアドバイザーのスマート提案にアクセスするには、追加の契約書が必要ですか？ {#content-advisor-smart-suggestions-genai-rider}

コンテンツアドバイザーでスマート提案にアクセスするには、GenAI ライダーに署名する必要があります。 Adobeの担当者に連絡して、GenAI ライダーに登録し、組織にスマートサジェストを有効にします。 GenAI Riderに署名すると、Adobe Expressのコンテンツアドバイザー内で、Adobe AEMの最小リリースバージョン要件である21994を満たす組織内のすべてのユーザーがスマート提案を利用できるようになります。

### キャンペーン概要を使用してContent Advisorでアセットを見つけるにはどうすればよいですか？ {#content-advisor-campaign-briefs}

Content Advisorは、検索キーワードを手動で入力することなく、キャンペーン概要ドキュメントをアップロードして関連アセットを発見することをサポートしています。 キャンペーン概要をPDF、DOCX、TXT形式でアップロードすると、コンテンツアドバイザーがテキストコンテンツを分析してキャンペーンの意図を理解し、AEM Assetsから関連アセットをレコメンドします。 キャンペーンブリーフは、テキストコンテンツにもとづいて分析されます。ブリーフ文書内の画像は分析されません。 キャンペーン概要を確認するには、GenAI担当者にサインする必要があります。有効にするには、Adobeの担当者にお問い合わせください。 必要なAEM リリースバージョンの最小値は21994です。

### Content AdvisorのアセットのDynamic Media レンディションにアクセスするにはどうすればよいですか？ {#content-advisor-dynamic-media-renditions}

Content AdvisorでDynamic Media レンディションにアクセスするには、アセットカードの情報アイコンをクリックし、「Dynamic Media」タブを選択します。 利用できるレンディションには、画像プリセット、スマート切り抜き、フォーマットタイプ、特定のチャネルに最適化されたカラープロファイルなどがあります。 Dynamic Media Scene7またはOpenAPI レンディション付きDynamic Mediaのいずれかを選択します。 OpenAPI レンディションの場合、利用可能なレンディションは、アセットが承認され、OpenAPIを使用するDynamic Mediaで利用可能な場合にのみ表示されます。 Dynamic Media タブを表示するには、有効なAEM Dynamic Media ライセンスが必要です。

### カンバスに配置する前に、Dynamic Media レンディションをプレビューして適用できますか？ {#content-advisor-dynamic-media-modifiers}

Content AdvisorのDynamic Media レンディションは、Adobe Express キャンバスに配置する前にプレビューおよび変更できます。 レンディションのプレビューアイコンをクリックしてプレビューするか、レンディション名をクリックしてカンバスに直接配置します。 「修飾子を追加」をクリックし、テキストボックスで修飾子を指定し、Enter キーを押してリアルタイム変換を適用します。 複数の修飾子を同時に適用してプレビューできます。 プレビューしたレンディションをカンバスにドラッグ&amp;ドロップして配置します。プレビュー中に適用された修飾子は、AEM Assetsのアセットには保存されません。

### Dynamic Mediaは、Adobe Expressのファイルサイズ制限にどのように役立ちますか？ {#content-advisor-dynamic-media-file-size}

Content AdvisorのDynamic Mediaは、AEM Assetsから直接、大規模なアセットの最適化されたレンディションを配信することで、Adobe Expressの80 MB アップロードファイルサイズの制限を克服します。 例えば、300 MBのTIFF アセットは、視覚的な画質を損なうことなく、2.5 MBのレンディションとして配信できます。 これにより、Adobe Expressで高解像度アセットを効率的に使用できます。ファイルをインポートする前に、ファイルサイズを手動で縮小したり重複したりする必要はありません。

### 保存された検索条件は、Content Advisorでどのように機能し、Assets ビューと共有されますか？ {#content-advisor-saved-searches}

Assets ビューで作成された保存済みの検索条件は、Content Advisorで使用でき、ブラウザー間で一貫して動作するので、両方のインターフェイスで事前に定義された検索条件を再利用できます。 コンテンツアドバイザーで検索を保存するには、目的のフィルターを適用し、フィルターアイコンをクリックして「保存済み検索を管理」を選択し、「新しい保存済み検索を作成」をクリックして、名前を指定します。 ただし、最近の検索は、Assets ビューとContent Advisorの間で一貫性がありません。同じユーザーが各インターフェイスで異なる最近検索を行う場合があります。 最近の検索は、異なるブラウザー間で共有されず、シークレットモードでは使用できず、AEM環境に固有です。 Assets ビューで使用できるデフォルトの保存済み検索機能は、Content Advisorでは使用できません。

### Content Advisorを使用して、特定のコレクション内のアセットを検索できますか？ {#content-advisor-collection-search}

Content Advisorは、すべてのコレクションでのアセットの検索や、特定のコレクションへの検索の制限をサポートしています。 これにより、収集したコレクションからアセットに素早くアクセスし、意図した組織のコンテキストを維持することができます。 Assetsのビューで利用できるフィルタリング機能は、Content Advisorのコレクション内の検索にも適用され、AEM AssetsとAdobe Express全体で一貫性のあるアセット発見体験を実現します。

### Express キャンバスの画像をAEM Assetsのアセットに置き換えるにはどうすればよいですか？ {#replace-image-aem-assets-express}

Adobe Expressのカンバス上の画像をAEM Assetsのアセットに置き換えるには、カンバス上の画像を選択し、「置換」をクリックして、使用可能なオプションから「AEM Assets」を選択します。 左側のナビゲーションパネルにコンテンツアドバイザーが開き、使用可能なリポジトリとアセットが表示されます。 置き換えアセットを選択してキャンバス上でプレビューし、「置換」をクリックして確定します。 SVGのファイルタイプは、このワークフローを使用した画像の置き換えではサポートされていません。

### Adobe Express プロジェクトをAEM Assets リポジトリに戻すにはどうすればよいですか？ {#save-express-project-aem-assets}

Adobe Express プロジェクトをAEM Assetsに保存するには、Express カンバスで「共有」をクリックして共有ダイアログを開き、「AEM Assets」を選択します。 アップロードダイアログで、「現在のページ」または「すべてのページ」を選択し、名前と書き出し形式を指定して、「宛先フォルダー」の下にあるフォルダーアイコンをクリックして保存場所を選択します。 サポートされている書き出し形式には、PNG、JPEG、PDF、MP4、MP4+PNG、およびMP4+JPEGがあります。 必要に応じて、「アップロード」をクリックする前に、「プロジェクト」フィールドまたは「キャンペーン名」、「キーワード」フィールドおよび「チャネル」フィールドを使用してキャンペーンメタデータを追加します。 Content Hub配信リポジトリに保存する場合、「プロジェクト」フィールドまたは「キャンペーン名」フィールドは必須であり、宛先フォルダーはメタデータから自動的に派生されます。

### AEM AssetsからAdobe Expressに読み込むアセットのファイルサイズとディメンションの制限は何ですか？ {#aem-assets-express-file-size-limits}

AEM Assets経由のAdobe Expressでは、次のファイルサイズとサイズの制限がサポートされています。JPEGおよびPNG アセットは、最大65 メガピクセル（8K×8Kまたは16K×4Kなど）をサポートし、最大ファイルサイズはデスクトップで80 MB、モバイルで40 MBです。 SVG ファイルは、最大ファイルサイズ 250 KBをサポートします。 MP4 ビデオは、最大ファイルサイズが200 MBの最大3840×3840 ピクセルをサポートします。 PSD ファイルは、最大65 メガピクセルをサポートし、最大ファイルサイズはデスクトップで80 MB、モバイルで40 MBです。 PDF ファイルには、定義済みの最大ディメンションまたはファイルサイズの制限がありません。

### AEM AssetsとAdobe Expressの統合におけるビデオの制限は何ですか？ {#aem-assets-express-video-limitations}

AEM AssetsとAdobe Expressの統合では、MP4が唯一のビデオファイルタイプとしてサポートされ、インポートとエクスポートの両方が可能です。 MP4 ビデオの読み込みでは、透明な背景（アルファチャンネル）を持つビデオはサポートされていません。 MP4 ビデオの書き出しの場合、サポートされる最大ファイルサイズは200 MBです。 書き出しファイルサイズが200 MBを超える場合は、ビデオを200 MB以下にトリミングするか、ローカルにダウンロードした後にビデオを手動でAEM Assetsの保存先フォルダーにアップロードすることをお勧めします。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
