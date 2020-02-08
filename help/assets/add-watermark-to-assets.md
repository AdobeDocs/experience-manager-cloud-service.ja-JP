---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 透かし処理 {#watermarking}

Adobe Experience Manager (AEM) Assetsの透かし機能を使用すると、アセットに電子透かしを追加でき、ユーザーはアセットの信頼性と著作権の所有を確認できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用するには、DAMアセットの更新ワークフローで透かしステップを追加します。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. From the Workflow Models page, select the **[!UICONTROL DAM Update Asset]** workflow and click **[!UICONTROL Edit]**.

1. From the Side Panel, drag the **[!UICONTROL Add Watermark]** step to the DAM Update Asset workflow.

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>「透かしを追加」ステップを、「サムネールを処理」ステップより前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するために、完了アイコンをタップまたはクリックします。

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the Watermark step.
1. アセットユーザーインターフェイスから、サンプルアセットをアップロードします。 透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。
