---
title: 画像に、人工的にインテリジェントなサービスでタグ付けする。
description: Adobe Senseiサービスを使用して、状況依存や説明的なビジネスタグを適用する、人工的にインテリジェントなサービスで画像にタグ付けします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cc24b16cf17f146e773e7974c649adae1bd10ddf
workflow-type: tm+mt
source-wordcount: '2401'
ht-degree: 35%

---


# スマートタグサービスをトレーニングし、画像にタグを付ける {#train-service-tag-assets}

デジタルアセットを扱う組織では、アセットメタデータで分類に基づく統制語彙を使用することがますます多くなっています。基本的に、従業員、パートナーおよび顧客がデジタルアセットを参照し、検索する際によく使用するキーワードのリストが含まれます。 タクソノミ制御のボキャブラリでアセットをタグ付けすると、タグベースの検索でアセットを簡単に識別および取得できます。

自然言語の語彙と比較して、ビジネスタクソノミに基づくタグ付けは、アセットを会社のビジネスと連携させ、最も関連のあるアセットを検索に表示するのに役立ちます。 例えば、車の製造元は車の画像にモデル名を付けて、プロモーションキャンペーンを設計するために検索した場合に関連する画像のみが表示されるようにすることができます。

In the background, the Smart Tags uses an artificial intelligence framework of [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) to train its image recognition algorithm on your tag structure and business taxonomy. その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。

<!-- TBD: Create a similar flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

スマートタグを使用するには、次のタスクを実行します。

* [Experience ManagerとAdobe Developer Consoleの統合](#integrate-aem-with-aio)。
* [タグのモデルとガイドラインを理解します](#understand-tag-models-guidelines)。
* [モデルをトレーニングします](#train-model)。
* [デジタルアセットのタグ付け](#tag-assets)。
* [タグと検索を管理します](#manage-smart-tags-and-searches)。

スマートタグは、 [!DNL Adobe Experience Manager Assets] お客様にのみ適用できます。 The Smart Tags is available for purchase as an add-on to [!DNL Experience Manager].

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? -->

## Adobe Developer Console [!DNL Experience Manager] との連携 {#integrate-aem-with-aio}

Adobe Developer Consoleを使用 [!DNL Adobe Experience Manager] して、スマートタグと統合できます。 Use this configuration to access the Smart Tags service from within [!DNL Experience Manager].

スマートタグを設定するタスク向けに、Experience Managerでアセットのスマートタグ付けを [設定する](smart-tags-configuration.md) （英語のみ）を参照してください。 At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Tags service.

## タグモデルとガイドラインの理解 {#understand-tag-models-guidelines}

タグモデルは、画像の視覚的な側面に基づく、関連するタグのグループです。 例えば、靴のコレクションは異なるタグを持つことができますが、すべてのタグは靴に関連し、同じタグモデルに属することができます。 タグは、画像の明確に異なる視覚要素にのみ関連付けることができます。 でトレーニングモデルのコンテンツ表現を理解するには、各タグに対して手動で追加されたタグのグループと例の画像から構成されるトップレベルのエンティティとして、トレーニングモデルを視覚化します。 [!DNL Experience Manager]各タグは、画像にのみ適用できます。

現実的に処理できないタグは、次のものに関連しています。

* 画像によって誘発される製品、ムード、感情の年や季節など、非視覚的で抽象的な要素。
* 製品に埋め込まれたカラーや小さな製品ロゴのあるシャツや、ないシャツなどの製品の視覚的な違いが細かく表示されます。

タグモデルを作成してサービスをトレーニングする前に、ビジネスのコンテキストでイメージ内のオブジェクトを最もよく説明する一意のタグのセットを特定します。 Ensure that the assets in your curated set conform to [the training guidelines](#training-guidelines).

### トレーニングガイドライン {#training-guidelines}

トレーニングセットの画像は、次のガイドラインに従う必要があります。

**数量とサイズ：** 画像は最小10個、タグあたり最大50個。

**一貫性**：タグの各画像は、似たような外観にする必要があります。同じ視覚的要素（画像内の同じタイプのオブジェクトなど）に関するタグを1つのタグモデルにまとめるのが最適です。 例えば、以下の画像は似ていないので、これらの画像すべてを `my-party`（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coherence.png)

**対象範囲**：トレーニングの画像には十分な多様性が必要です。AEM が適切に焦点を当てることを学習できるよう、数は少なくても多様性の高い例を提供します。見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。例えば、model-down-pose ** というタグの場合、タグ付け時、類似する画像をより正確に識別できるよう、以下のハイライト表示された画像に似たトレーニング画像を増やします。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coverage_1.png)

**妨害物と障害物**：サービスのトレーニングには、障害物（目立つ背景、メインとなる対象と一緒に含まれる物や人物などの関連性のない付随物）が少ない画像のほうが効果的です。例えば、casual-shoe ** というタグの場合、2 つ目の画像はトレーニングの候補として適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/distraction.png)

**完全性**：画像が複数のタグの対象となる場合は、適用可能なすべてのタグを追加してから、画像をトレーニングに含めます。例えば、*raincoat* と *model-side-view* などのタグの場合、対象となるアセットに両方のタグを追加してから、そのアセットをトレーニングに含めます。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/completeness.png)

**タグ数**: 各タグに少なくとも2つの異なるタグと少なくとも10の異なる画像を使用して、モデルのトレーニングを行うことをお勧めします。 単一のタグモデルでは、50個を超えるタグを追加しないでください。

**例の数**: 各タグに対して、少なくとも10個の例を追加します。 ただし、アドビでは約30例をお勧めします。 1つのタグにつき最大50個のサンプルがサポートされます。

**偽陽性や競合を回避**: 単一の視覚的側面に対応した単一のタグモデルを作成することをお勧めします。 モデル間でタグが重なり合うのを避けるように、タグモデルを構築します。 例えば、との2つの異なるタグモデル名でのよう `sneakers` な共通のタグは使用し `shoes` ないでくだ `footwear`さい。 トレーニングプロセスは、共通のキーワードに関して、トレーニングを受けた1つのタグモデルをもう1つで上書きします。

**例**: 手順説明の例を以下に示します。

* 次を含むタグモデルを作成します。
   * 車種に関連するタグのみ。
   * シャツの色に関連するタグのみ。
   * 女性と男性のジャケットに関するタグのみ。
* 作成しない、
   * 2019年と2020年にリリースされた車種を含むタグモデル。
   * 同じ車種を含む複数のタグモデル。

**トレーニングに使用する画像**: 同じ画像を使用して、異なるタグモデルをトレーニングできます。 ただし、イメージをタグモデル内の複数のタグに関連付けることはできません。 したがって、同じ画像に異なるタグモデルに属する異なるタグをタグ付けすることが可能です。

トレーニングを取り消すことはできません。 上記のガイドラインは、トレーニングに適した画像を選択する際に役立ちます。

## カスタムタグに合わせてモデルをトレーニングする {#train-model}

ビジネス固有のタグに合わせてモデルを作成し、トレーニングするには、次の手順に従います。

1. 必要なタグと適切なタグ構造を作成します。 DAMリポジトリに関連する画像をアップロードします。
1. ユーザーインターフェイスで、 [!DNL Experience Manager] アセット **[!UICONTROL /]** スマートタグトレーニングにアクセスします ****。
1. 「**[!UICONTROL 作成]**」をクリックします。「 **[!UICONTROL タイトル]**」、「 **[!UICONTROL 説明]**」を入力します。
1. モデルをトレーニングする既存のタグを参照して選択 `cq:tags` します。 「**[!UICONTROL 次へ]**」をクリックします。
1. アセットを **[!UICONTROL 選択ダイアログで]** 、各タグに対して「アセット **** 」をクリックします。 DAMリポジトリ内を検索するか、リポジトリを参照して、少なくとも10個の画像と最大50個の画像を選択します。 フォルダーではなくアセットを選択します。 画像を選択したら、「 **[!UICONTROL 選択]**」をクリックします。
1. 選択した画像のサムネールをプレビューするには、タグの前にあるアコーディオンをクリックします。 「 **[!UICONTROL 追加アセット]**」をクリックして、選択内容を変更できます。 選択が完了したら、「 **[!UICONTROL 送信]**」をクリックします。 ユーザーインターフェイスに、トレーニングが開始されたことを示す通知がページの下部に表示されます。
1. 各タグモデルの「 **[!UICONTROL Status]** 」列で、トレーニングのステータスを確認します。 可能なステータスは、 [!UICONTROL 「]Pending [!UICONTROL 」、「]Trained [!UICONTROL 」、「]Failed」です。

![スマートタグ付け用のタグ付けモデルをトレーニングするワークフロー](assets/smart-tag-model-training-flow.png)

*図： タグ付けモデルをトレーニングするためのトレーニングワークフローの手順です。*

### 表示トレーニングのステータスとレポート {#training-status}

Smart Tagsサービスがアセットのトレーニングセット内のタグに関するトレーニングを受けているかどうかを確認するには、レポートコンソールからトレーニングワークフローレポートを確認します。

1. インター [!DNL Experience Manager] フェイスで、 **[!UICONTROL ツール/アセット/レポートに移動します]**。
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. レポートのタイトルと説明を指定します。「**[!UICONTROL レポートをスケジュール]**」で、「**[!UICONTROL 今すぐ]**」オプションを選択したままにします。レポートを後で生成するようにスケジュールするには、「**[!UICONTROL 後で]**」を選択し、日時を指定します。Then, click **[!UICONTROL Create]** from the toolbar.
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、生成したレポートを選択します。To view the report, click **[!UICONTROL View]** from the toolbar.
1. レポートの詳細をレビューします。レポートには、トレーニングしたタグのトレーニングステータスが表示されます。The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Tags service is trained for the tag. 黄色は、特定のタグに関するサービスのトレーニングが完全には実施されていないことを示します。この場合、特定のタグを含む画像をさらに追加し、トレーニングワークフローを実行して、そのタグに関するサービスのトレーニングを完全に実施します。このレポートにタグが表示されない場合は、これらのタグに対して、トレーニングワークフローを再実行します。タグ
1. To download the report, select it from the list, and click **[!UICONTROL Download]** from the toolbar. レポートはMicrosoft Excelスプレッドシートとしてダウンロードされます。

## アセットのタグ付け {#tag-assets}

スマートタグサービスのトレーニングを終えたら、タグ付けワークフローをトリガーして、類似の別のアセットに適切なタグを自動的に適用できます。 タグ付けワークフローは、定期的に、または必要に応じて適用できます。 タグ付けワークフローは、アセットとフォルダの両方に適用されます。

### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. Experience Managerインターフェイスで、 **[!UICONTROL ツール/ワークフロー/モデルに移動します]**。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. ワークフローのタイトルとオプションのコメントを指定します。「**[!UICONTROL 実行]**」をクリックします。

   ![tagging_dialog](assets/tagging_dialog.png)

   アセットフォルダーに移動し、タグを確認して、アセットが適切にタグ付けされているかどうかを確認します。 For details, see [manage smart tags](#manage-smart-tags-and-searches).

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. Assets のユーザーインターフェイスで、スマートタグを適用するアセットが格納されているフォルダーまたは特定のアセットを選択します。
1. 左上隅から、 **[!UICONTROL タイムラインを開きます]**。
1. 左側のサイドバーの下部でアクションを開き、「 **[!UICONTROL 開始ワークフロー]**」をクリックします。

   ![開始_ワークフロー](assets/start_workflow.png)

1. 「**[!UICONTROL DAM スマートタグアセット]**」ワークフローを選択し、ワークフローのタイトルを指定します。
1. 「**[!UICONTROL 開始]**」をクリックします。ワークフローによってアセットにタグが適用されます。アセットフォルダーに移動し、タグを確認して、アセットが適切にタグ付けされているかどうかを確認します。 For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>後続のタグ付けサイクルでは、新しくトレーニングされたタグを使用して、変更したアセットのみが再度タグ付けされます。ただし、タグ付けワークフローの最後のタグ付けサイクルと現在のタグ付けサイクルの間のギャップが24時間を超える場合は、変更されないアセットもタグ付けされます。 定期的なタグ付けワークフローの場合、タイムギャップが6か月を超えると、変更されていないアセットにタグが付けられます。

### アップロードしたアセットのタグ付け {#tag-uploaded-assets}

Experience Managerでは、ユーザーがDAMにアップロードするアセットに自動的にタグを付けることができます。 そのためには、管理者は、の使用可能な手順をスマートタグアセットに追加するワークフローを設定します。 アップロードしたアセットのスマートタグを有効にする [方法を参照してください](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)。

## Manage smart tags and image searches {#manage-smart-tags-and-searches}

関連性の高いタグのみが表示されるようにするために、スマートタグを整理し、ブランド画像に割り当てられた可能性のある不正確なタグを削除することができます。

また、スマートタグをモデレートすると、画像が最も関連性の高いタグの検索結果に表示されるようになるので、画像のタグベース検索の精度が向上します。実質的には、検索結果に関連性のない画像が表示されないようにすることができます。

タグに高いランクを割り当てて、画像に関して関連性を高めることもできます。画像のタグのランクを高くすることで、特定のタグに基づいて検索が実行されたときに、その画像が検索結果に表示される可能性が高くなります。

1. オムニサーチボックスで、タグに基づいてアセットを検索します。
1. 検索結果を調査し、検索に関連性のない画像を特定します。
1. Select the image, and then click the **[!UICONTROL Manage Tags]** icon from the toolbar.
1. **[!UICONTROL タグを管理]**&#x200B;ページで、タグを調査します。特定のタグに基づいてイメージを検索しない場合は、タグを選択し、ツールバーの削除アイコンをクリックします。 Alternatively, click `X` symbol that appears beside the label.
1. タグに上位のランクを割り当てるには、タグを選択し、ツールバーのプロモーションアイコンをクリックします。 昇格したタグは、「**[!UICONTROL タグ]**」セクションに移動されます。
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. 画像のプロパティページに移動します。昇格したタグに高い関連性が割り当てられていること、その結果として検索結果の上位に表示されることを確認します。

### スマートタグ付き AEM 検索結果について {#understandsearch}

デフォルトでは、検索用語同士を `AND` 句で組み合わせて AEM 検索がおこなわれます。スマートタグを使用しても、このデフォルトの動作は変わりません。スマートタグを使用すると、適用されたスマートタグ内にある検索用語のいずれかを探すための `OR` 句が追加されます。例えば、「`woman running`」を検索する場合を考えます。デフォルトでは、「`woman`」のみ、または「`running`」のみがメタデータに含まれているアセットは、検索結果に表示されません。しかし、スマートタグを使って「`woman`」または「`running`」のどちらかがタグ付けされているアセットは、そうした検索結果に表示されます。つまり、検索結果は、以下を組み合わせたものになります。

* 「`woman`」と「`running`」の両方のキーワードがメタデータ内にあるアセット。

* 上記どちらかのキーワードがメタデータ内にあるアセット。

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. 各種メタデータフィールド内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman`」または「`running`」に一致するもの。

### タグの制限 {#limitations}

拡張スマートタグは、ブランド画像とそのタグの学習モデルに基づいています。これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。現在のバージョンのスマートタグには、次の制限があります。

* 画像内の細かい違いを認識することはできません。例えば、スリムとレギュラーのフィットシャツ。
* 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、T シャツのロゴなどです。
* タグ付けは、AEM がサポートされているロケールでサポートされています。For a list of languages, see [Smart Tags release notes](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

スマートタグを使用してアセットを検索（通常または拡張）するには、「アセットの検索」（フルテキスト検索）を使用します。 スマートタグには個別の検索用述語はありません。

>[!NOTE]
>
>スマートタグでタグをトレーニングして他の画像に適用する機能は、トレーニングに使用する画像の質に応じて異なります。
>最適な結果を得るには、視覚的に似ている画像を使用し、それぞれのタグについてサービスのトレーニングを実施することをお勧めします。

>[!MORELIKETHIS]
>
>* [スマートタグを使用するためのExperience Managerの設定](smart-tags-configuration.md)
>* [スマートタグによるアセット管理の仕組み](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)

