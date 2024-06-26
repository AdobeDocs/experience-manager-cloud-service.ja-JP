---
title: Experience Managerでのアセットの承認
description: でアセットを承認する方法を説明します [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 2%

---

# でのアセットの承認 [!DNL Experience Manager]

ブランドマネージャーとマーケターは、ブランドアセットを厳格に管理しています。 アセットの承認済みの最新バージョンのみを使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性を確保できます。

AEM Assetsでアセットを承認してアセット管理を効率化し、アセットを処理するための制御された効率的なプロセスを確保できます。

## 事前準備 {#pre-requisites}

を編集するには、AEM Assetsのas a Cloud Serviceへのアクセス権と権限が必要です **[!UICONTROL レビューステータス]** アセットのプロパティ。

## 設定

アセットを承認するには、管理表示で該当するメタデータスキーマを 1 回更新する必要があります。 Assets ビューの場合は、この設定をスキップできます。 メタデータスキーマを設定するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. 該当するメタデータスキーマを選択し、 **[!UICONTROL 編集]**. <br>この **[!UICONTROL メタデータスキーマフォームエディター]** が次で開く **[!UICONTROL 基本]** タブがハイライト表示されました。
1. 下にスクロールして、 **[!UICONTROL レビューステータス]**.
1. 「」をクリックします **[!UICONTROL ルール]** 右側のパネルの「」タブ。
1. Uncheck **[!UICONTROL 編集を無効にする]** をクリックして、 **[!UICONTROL 保存]**.
プロパティを表示する必要がある場合、 **[!UICONTROL レビューステータス]** フィールドのマッピング先、次に移動 **[!UICONTROL 設定]** tab キーを押してを表示します `./jcr:content/metadata/dam:status` の値 **[!UICONTROL プロパティにマッピング]** フィールド。

>[!NOTE]
>
>アセットまたはフォルダーのデフォルトのスキーマが異なる場合は、その特定のスキーマでこの更新を行ってください。

## アセットの承認 {#approve-assets}

アセットは両方で承認できます [!DNL Experience Manager] および [!DNL Experience Manager Assets]. でアセットを承認するには [!DNL Experience Manager]は、次の手順に従います。

1. アセットを選択し、 **[!UICONTROL プロパティ]** 上部のウィンドウで確認します。
1. が含まれる **[!UICONTROL 基本]** タブ、下にスクロール **[!UICONTROL レビューステータス]**.
1. レビューステータスをに変更します。 **[!UICONTROL 承認済み]**.
   ![画像](/help/assets/assets/approve-old-ui.png)
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同様に、を使用してアセットを承認できます [新しいAssets ビュー](/help/assets/manage-organize-assets-view.md).

## アセットの一括承認 {#bulk-approve-assets}

複数のアセットを一度にすばやく承認することで、ワークフローを効率化します。 アセットを一括承認して、承認プロセスを迅速化し、時間を節約し、生産性を向上させることができます。
<br>で一括アセットを承認するには、次の手順に従います [!DNL Experience Manager]:

1. オーサー環境でフォルダーを作成します（https://author-pXXX-eYYY.adobeaemcloud.com）。 置換 _XXX_ （プログラム ID を使用） _YYYY_ と、Experience Managerの環境 ID を使用します。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL メタデータプロファイル]**.
1. クリック **[!UICONTROL 作成]** ページの右上に表示されます。
1. プロファイルのタイトルを追加して、をクリックします **[!UICONTROL 作成]**. メタデータプロファイルが正常に作成されました。
1. 新しく作成したメタデータプロファイルを選択し、 **[!UICONTROL 編集 _ホ_]**. <br>この&#x200B;**[!UICONTROL メタデータプロファイルを編集]**フォームが次の情報で開く&#x200B;**[!UICONTROL 基本]**タブがハイライト表示されました。
1. をドラッグ&amp;ドロップ **[!UICONTROL 1 行のテキストフィールド]** から **[!UICONTROL フォームを作成]** フォームの「メタデータ」セクションの右側のセクションです。
1. 新しく追加されたフィールドをクリックし、で次の更新を行います **[!UICONTROL 設定]** パネル：
   1. 変更： **[!UICONTROL フィールドラベル]** 対象： _承認済みAssets_.
   1. を更新 **[!UICONTROL プロパティにマッピング]** 対象： _./jcr:content/metadata/dam:status_.
   1. デフォルト値をに変更します。 _承認済み_.

1. 「**[!UICONTROL 保存]**」をクリックします。
1. が含まれる **[!UICONTROL メタデータプロファイル]** ページで、新しく作成したメタデータプロファイルを選択します。
1. クリック **[!UICONTROL フォルダーへのメタデータプロファイルの適用]** 上部のアクションバーから。
1. 承認する必要があるフォルダーを選択し、 **[!UICONTROL 適用]**.
   <br> フォルダー全体に対する権限が承認用に設定され、このフォルダーにアップロードされたアセットが自動的に承認されます。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>この方法では、フォルダー内に新しく作成されたアセットが承認されます。 フォルダー内の既存のアセットの場合、手動で選択して承認する必要があります。 <br> または、を使用することもできます。 **[!UICONTROL 再処理]** メタデータプロファイルから古いアセットに変更を適用するオプション。

同様に、Assets ビューでフォルダー内のアセットを一括承認するには、次の手順を実行します。

1. アセットを選択し、 **[!UICONTROL メタデータの一括編集]**.

1. を選択 **[!UICONTROL 承認済み]** が含まれる **[!UICONTROL ステータス]** で使用できるフィールド [!UICONTROL プロパティ] 右側のペインの「」セクション。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 承認済みアセットの配信 URL をコピー {#copy-delivery-url-approved-assets}

リポジトリ内のすべての承認済みアセットの配信 URL は、次のいずれかの場合に使用できます [!UICONTROL OpenAPI 機能を備えたDynamic Media] お使いのAEM as a Cloud Service インスタンスで有効にします。

リポジトリ内の承認済みアセットの配信 URL をコピーするには：

1. アセットを選択し、 **[!UICONTROL 詳細]**.

1. 右側のパネルに表示されている「レンディション」アイコンをクリックします。

1. を選択 **[!UICONTROL OpenAPI のDynamic Media]** で利用可能 **[!UICONTROL 動的]** セクション。

1. クリック **[!UICONTROL URL をコピー]** でアセットの配信 URL をコピーします。
   ![配信 URL をコピー](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >承認済みアセットの配信 URL をコピーするオプションは、Assets ビューでのみ使用できます。

