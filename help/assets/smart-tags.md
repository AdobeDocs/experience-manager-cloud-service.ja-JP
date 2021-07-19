---
title: ' [!DNL Adobe Sensei] スマートサービスを使用したアセットの自動タグ付け'
description: コンテキストタグと説明的なビジネスタグを適用する人工知能サービスを使用したアセットのタグ付け。
contentOwner: AG
feature: スマートタグ、タグ付け
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '2346'
ht-degree: 97%

---


# 検索体験を改善するためのアセットへのスマートタグ付けの追加 {#smart-tag-assets-for-faster-search}

デジタルアセットを扱う組織では、アセットメタデータで分類に基づく統制語彙を使用することがますます多くなっています。これには、基本的に、従業員、パートナーおよび顧客がデジタルアセットを参照したり、検索したりする場合によく使用するキーワードのリストが含まれます。分類に基づく統制語彙を使用してアセットをタグ付けすると、検索でアセットを特定し、取得することが容易になります。

自然言語語彙と比較して、ビジネス上の分類に基づいたタグ付けでは、デジタルアセットを会社のビジネスと容易に連携させることができ、関連性の最も高いアセットが検索で表示されるようになります。例えば、自動車メーカーでは、プロモーションキャンペーンを計画するために様々なモデルの画像を検索する際、関連性の高い画像のみが表示されるように、モデル名を使用して車の画像をタグ付けすることができます。

そのバックグラウンドで、機能は [Adobe Sensei](https://www.adobe.com/jp/sensei/experience-cloud-artificial-intelligence.html) の人工知能フレームワークを使用して、タグ構造とビジネス上の分類に基づいて画像認識アルゴリズムのトレーニングをおこないます。その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。[!DNL Experience Manager Assets] デプロイメントは、デフォルトで [!DNL Adobe Developer Console] と統合されます。

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## サポートされているアセットタイプ {#smart-tags-supported-file-formats}

次のタイプのアセットにタグを付けることができます。

* **画像**：多くの形式の画像が、Adobe Sensei のスマートコンテンツサービスを使用してタグ付けされます。[トレーニングモデルを作成](#train-model)した後、アップロードされた画像が自動的にタグ付けされられます。スマートタグは、JPG および PNG 形式のレンディションを生成する、サポートされるファイル形式に適用されます。
* **テキストベースのアセット**： [!DNL Experience Manager Assets] は、アップロード時に、サポートされているテキストベースのアセットに自動タグ付けをおこないます。
* **ビデオアセット**：ビデオタグ付けは、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] ではデフォルトで有効になっています。新しいビデオをアップロードする場合や、既存のビデオを再処理する場合、[ビデオは自動的にタグ付けされます](/help/assets/smart-tags-video-assets.md)。

| 画像（MIME タイプ） | テキストベースのアセット（ファイル形式） | ビデオアセット（ファイル形式とコーデック） |
|----|-----|------|
| image/jpeg | CSV | MP4（H264／AVC） |
| image/tiff | DOC | MKV（H264／AVC） |
| image/png | DOCX | MOV（H264／AVC、Motion JPEG） |
| image/bmp | HTML | AVI（indeo 4） |
| image/gif | PDF | FLV（H264／AVC、vp6f） |
| image/pjpeg | PPT | WMV（WMV2） |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] ではデフォルトで、スマートタグがテキストベースのアセットとビデオに自動的に追加されます。画像にスマートタグを自動追加するには、次のタスクを実行します。

* [タグモデルとガイドラインの理解](#understand-tag-models-guidelines)。
* [モデルのトレーニング](#train-model)。
* [デジタルアセットのタグ付け](#tag-assets)。
* [タグと検索の管理](#manage-smart-tags-and-searches)。

## タグモデルとガイドラインの理解 {#understand-tag-models-guidelines}

タグモデルは、タグ付けされる画像の様々な視覚要素に関連付けられた、関連タグのグループです。タグは、画像の明確に異なる視覚的要素と関連付けられるので、タグを適用すると、特定のタイプの画像を検索するのに役立ちます。例えば、靴のコレクションは異なるタグを持つことができますが、すべてのタグは靴に関連し、同じタグモデルに属します。タグを適用すると、デザインや使用法など、様々なタイプの靴を見つけるのに役立ちます。 [!DNL Experience Manager] でトレーニングモデルのコンテンツ表現を理解するには、各タグに対して手動で追加されたタグと例として用いる画像のグループから構成されるトップレベルのエンティティとして、トレーニングモデルを視覚化します。各タグは、画像にのみ適用できます。

タグモデルを作成してサービスをトレーニングする前に、自社ビジネスのコンテキストでイメージ内のオブジェクトを最もよく説明する一意のタグのセットを特定します。キュレーション後のセット内のアセットが、[トレーニングガイドライン](#training-guidelines)に従っていることを確認してください。

### トレーニングガイドライン {#training-guidelines}

トレーニングセット内の画像が次のガイドラインに従っていることを確認します。

**数量とサイズ：**&#x200B;タグ 1 つにつき画像は最小 10 個、最大 50 個。

**コヒーレンス**：タグの画像の見た目が似ていることを確認します。同じ視覚的要素（画像内の同じタイプのオブジェクトなど）に関するタグを 1 つのタグモデルにまとめるのが最適です。例えば、以下の画像は似ていないので、これらの画像すべてを `my-party`（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coherence.png)

**対象範囲**：トレーニングの画像には十分な多様性が必要です。[!DNL Experience Manager] が適切に焦点を当てることを学習できるよう、数は少なくても多様性の高い例を提供します。見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。例えば、*model-down-pose* というタグの場合、タグ付け時、類似する画像をより正確に識別できるよう、以下のハイライト表示された画像に似たトレーニング画像を増やします。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coverage_1.png)

**妨害物と障害物**：サービスのトレーニングには、障害物（目立つ背景、メインとなる対象と一緒に含まれる物や人物などの関連性のない付随物）が少ない画像のほうが効果的です。例えば、*casual-shoe* というタグの場合、2 つ目の画像はトレーニングの候補として適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/distraction.png)

**完全性**：画像が複数のタグの対象となる場合は、適用可能なすべてのタグを追加してから、画像をトレーニングに含めます。例えば、*raincoat* と *model-side-view* などのタグの場合、対象となるアセットに両方のタグを追加してから、そのアセットをトレーニングに含めます。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/completeness.png)

**タグ数**：各タグに少なくとも 2 つの個別タグと、少なくとも 10 の異なる画像を使用して、モデルのトレーニングをおこなうことをお勧めします。単一のタグモデルでは、50 個を超えるタグを追加しないでください。

**例の数**：各タグに対して、少なくとも 10 個の例を追加します。ただし、アドビでは約 30 個の例を使用することをお勧めしています。1 つのタグにつき最大 50 個の例がサポートされます。

**偽陽性や競合を回避**：単一の視覚的要素に対応した単一のタグモデルを作成することをお勧めします。モデル間でタグが重なり合うのを避けるように、タグモデルを構築します。例えば、`shoes` と `footwear` の 2 つの異なるタグモデル名で、`sneakers` のような共通タグは使用しないでください。トレーニングプロセスは、共通のキーワードに関して、トレーニングを受けた 1 つのタグモデルをもう 1 つで上書きします。

**例**：ガイダンスのさらなる例を以下に示します。

* 次のみを含むタグモデルを作成する

   * 車種に関連するタグ。
   * 女性と男性のジャケットに関連するタグ。

* 次のようなタグモデルは作成しません。

   * 2019年と2020年にリリースされた車種を含むタグモデル。
   * 同じ車種を含む複数のタグモデル。

**トレーニングに使用する画像**：同じ画像を使用して、異なるタグモデルをトレーニングできます。ただし、画像をタグモデル内の複数のタグに関連付けることはできません。異なるタグモデルに属する異なるタグを、同じ画像にタグ付けすることができます。

トレーニングを取り消すことはできません。上記のガイドラインは、トレーニングに適した画像を選択する際に役立ちます。

## カスタムタグに合わせたモデルのトレーニング {#train-model}

ビジネス固有のタグに合わせてモデルを作成してトレーニングするには、次の手順に従います。

1. 必要なタグと適切なタグ構造を作成します。DAM リポジトリーに関連する画像をアップロードします。
1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL Assets]**／**[!UICONTROL スマートタグトレーニング]**&#x200B;にアクセスします。
1. 「**[!UICONTROL 作成]**」をクリックします。「**[!UICONTROL タイトル]**」、「**[!UICONTROL 説明]**」を入力します。
1. モデルをトレーニングする既存のタグを `cq:tags` から参照して選択します。「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL アセットを選択]**&#x200B;ダイアログで、各タグに対して「**[!UICONTROL アセットを追加]**」をクリックします。DAM リポジトリー内を検索するか、リポジトリーを参照して、画像を 10 個以上、最大で 50 個選択します。フォルダーではなくアセットを選択します。画像を選択したら、「**[!UICONTROL 選択]**」をクリックします。

   ![トレーニング状況を表示](assets/smart-tags-training-status.png)

1. 選択した画像のサムネールをプレビューするには、タグの前にあるアコーディオンをクリックします。「**[!UICONTROL アセットを追加]**」をクリックして、選択内容を変更できます。選択が完了したら、「**[!UICONTROL 送信]**」をクリックします。ユーザーインターフェイスに、トレーニングが開始されたことを示す通知がページの下部に表示されます。
1. 各タグモデルの「**[!UICONTROL ステータス]**」列で、トレーニングのステータスを確認します。可能なステータスは、「[!UICONTROL 保留]」、「[!UICONTROL トレーニング済み]」、「[!UICONTROL 失敗]」です。

![スマートタグ用のタグ付けモデルをトレーニングするワークフロー](assets/smart-tag-model-training-flow.png)

*図：タグ付けモデルをトレーニングするトレーニングワークフロー手順。*

### トレーニングのステータスとレポートの表示 {#training-status}

アセットのトレーニングセット内のタグに関するスマートタグサービスのトレーニングが実施されたかどうかを確認するには、レポートコンソールでトレーニングワークフローレポートを調べます。

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;に移動します。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、「**[!UICONTROL 作成]**」をクリックします。
1. 「**[!UICONTROL スマートタグトレーニング]**」レポートを選択し、ツールバーで「**[!UICONTROL 次へ]**」をクリックします。
1. レポートのタイトルと説明を指定します。「**[!UICONTROL レポートをスケジュール]**」で、「**[!UICONTROL 今すぐ]**」オプションを選択したままにします。レポートを後で生成するようにスケジュールするには、「**[!UICONTROL 後で]**」を選択し、日時を指定します。次に、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、生成したレポートを選択します。レポートを表示するには、ツールバーの「**[!UICONTROL 表示]**」アイコンをクリックします。
1. レポートの詳細をレビューします。レポートには、トレーニングしたタグのトレーニングステータスが表示されます。「**[!UICONTROL トレーニングステータス]**」列の緑色は、そのタグについてスマートタグサービスのトレーニングが実施されたことを示します。黄色は、特定のタグに関するサービスのトレーニングが完全には実施されていないことを示します。この場合、特定のタグを含む画像をさらに追加し、トレーニングワークフローを実行して、そのタグに関するサービスのトレーニングを完全に実施します。このレポートにタグが表示されない場合は、それらのタグに関するトレーニングワークフローを再度実行してください。
1. レポートをダウンロードするには、リストから対象のレポートを選択し、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。レポートは [!DNL Microsoft Excel] スプレッドシートとしてダウンロードされます。

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## スマートタグ付きアセットのタグ付け {#tag-assets}

サポートされているすべてのタイプのアセットは、アップロード時に [!DNL Experience Manager Assets] によって自動的にタグ付けされます。タグ付けはデフォルトで有効になっています。[!DNL Experience Manager] は適切なタグをほぼリアルタイムで適用します。 <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

画像およびビデオの場合、スマートタグは視覚的な観点に基づいて生成されます。

テキストベースのアセットの場合、スマートタグの有効性は、アセット内のテキストの量に依存するのではなく、アセットのテキスト内に存在する関連キーワードまたは関連エンティティに依存します。テキストベースのアセットの場合、スマートタグはテキストに表示されるキーワードですが、アセットを説明するのに最適なキーワードです。サポートされているアセットの場合、[!DNL Experience Manager] は既にテキストを抽出しており、インデックス化してアセットの検索に使用しています。しかし、テキスト内のキーワードに基づくスマートタグは、フル検索インデックスに比べて、アセット検出を改善するために使用される専用の、構造化された、より優先度の高い検索ファセットを提供します。

## スマートタグとアセット検索の管理 {#manage-smart-tags-and-searches}

関連性の高いタグのみが表示されるようにするために、スマートタグを整理し、ブランドアセットに割り当てられた可能性のある不正確なタグを削除することができます。

また、スマートタグをモデレートすると、アセットが最も関連性の高いタグの検索結果に表示されるようになるので、アセットのタグベース検索の精度が向上します。実質的には、検索結果に関連性のないアセットが表示されないようにすることができます。

また、タグに上位のランクを割り当てて、タグのアセットに対する関連性を高めることもできます。アセットのタグのランクを高くすることで、特定のタグに基づいて検索が実行されたときに、そのアセットが検索結果に表示される可能性が高くなります。

アセットのスマートタグをモデレートするには、以下をおこないます。

1. 検索フィールドで、タグに基づいてアセットを検索します。

1. 検索結果を調査し、検索に関連性のないアセットを特定します。

1. アセットを選択し、ツールバーの![タグを管理アイコン](assets/do-not-localize/manage-tags-icon.png)をクリックします。

1. **[!UICONTROL タグを管理]**&#x200B;ページで、タグを調査します。特定のタグに基づいてアセットを検索しない場合は、タグを選択し、ツールバーから![削除アイコン](assets/do-not-localize/delete-icon.png)を選択します。または、ラベルの横の `X` 記号を選択します。

1. タグに高いランクを割り当てるには、タグを選択し、ツールバーの![昇格アイコン](assets/do-not-localize/promote-icon.png)をクリックします。昇格したタグは「**[!UICONTROL タグ]**」セクションに移動されます。

1. 「**[!UICONTROL 保存]**」、「**[!UICONTROL OK]**」の順に選択して、[!UICONTROL 成功]ダイアログを閉じます。

1. アセットの[!UICONTROL プロパティ]ページに移動します。昇格したタグに高い関連性が割り当てられていること、その結果として検索結果の上位に表示されることを確認します。

### スマートタグ付き [!DNL Experience Manager] 検索結果について {#understand-search}

デフォルトでは、検索用語同士を `AND` 句で組み合わせて [!DNL Experience Manager] 検索がおこなわれます。スマートタグを使用しても、このデフォルトの動作は変わりません。スマートタグを使用すると、適用されたスマートタグ内にある検索用語のいずれかを探すための `OR` 句が追加されます。例えば、「`woman running`」を検索する場合を考えます。デフォルトでは、「`woman`」のみ、または「`running`」のみがメタデータに含まれているアセットは、検索結果に表示されません。しかし、スマートタグを使って「`woman`」または「`running`」のどちらかがタグ付けされているアセットは、そうした検索クエリに表示されます。つまり、検索結果は、以下を組み合わせたものになります。

* 「`woman`」と「`running`」の両方のキーワードがメタデータ内にあるアセット。

* 上記どちらかのキーワードがメタデータ内にあるアセット。

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. 各種メタデータフィールド内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman`」または「`running`」に一致するもの。

## タグ付けの制限とベストプラクティス {#limitations}

拡張スマートタグは、画像とそのタグの学習モデルに基づいています。これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。スマートタグの現行バージョンには次の制限事項があります。

* 画像内の細かい違いを認識することはできません。例えば、シャツのサイズが細身か標準かなどです。
* 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、シャツのロゴなどです。
* タグ付けは、[!DNL Experience Manager] がサポートする言語でサポートされています。言語の一覧については、[スマートコンテンツサービスのリリースノート](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html?lang=ja#languages)を参照してください。
* 実際には処理されないタグは、次のものに関連しています。

   * 視覚的でない、抽象的な側面。製品のリリースの年や季節、画像によって誘発されるムードや感情、ビデオの主観的な意味など、非視覚的で抽象的な要素。
   * シャツの襟の有無や、製品に埋め込まれた小さな製品ロゴなど、製品の視覚的な細かい違い。

<!-- TBD: Add limitations related to text-based assets. -->

スマートタグ（通常または拡張）付きのアセットを検索するには、[!DNL Assets] 検索（全文検索）を使用します。スマートタグには個別の検索用述語はありません。

>[!NOTE]
>
>スマートタグでタグのトレーニングを実施し、それらのタグを他の画像に適用できるかどうかは、トレーニングで使用する画像の質によって決まります。
>最適な結果を得るには、視覚的に似ている画像を使用し、それぞれのタグについてサービスのトレーニングを実施することをお勧めします。

>[!MORELIKETHIS]
>
>* [スマートタグによるアセット管理の仕組み](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [ビデオアセットのスマートタグ](smart-tags-video-assets.md)

