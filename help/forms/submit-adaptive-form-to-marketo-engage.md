---
title: フォームに対してMarketo Engageに送信アクションを設定するには？
description: アダプティブフォームの送信アクションを設定して、Marketo Engageにデータを送信する方法を説明します。
keywords: Marketo engageにデータを送信し、送信アクションをMarketo Engageに送信として設定します
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: 08fe79147c81c0a5b319fef3ef7733b6053b399a
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 21%

---

# 既存のフォーム用の Marketo Engage に対する送信アクションの設定

![ワークフロー](/help/forms/assets/workflow-marketo-3.png)

アダプティブ Forms エディターには、アダプティブ Forms データをAdobe Marketo Engageに送信して処理するための&#x200B;**Marketo Engageに送信**&#x200B;送信アクションが用意されています。 送信時に[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)にデータを送信するように、既存のアダプティブフォームを設定できます。

フォーム送信を処理するための、すぐに使用できる様々な送信アクションを利用できます。 これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事を参照してください。

## フォームに対するMarketo Engageへの送信アクションの設定時の考慮事項

* アダプティブフォームが、フォーム送信時にMarketo Engageにデータを送信するようにMarketo Engage データソースで設定されていることを確認します。 ただし、フォームがMarketo Engage データスキーマで設定されている場合でも、「**OneDriveに送信**」や「**SharePointに送信**」などの代替手段に送信アクションを変更できます。

## 既存のフォームに対してMarketo Engageに送信アクションを設定するための前提条件

Marketo Engageに送信アクションを設定するための前提条件：

* アダプティブフォーム [&#128279;](/help/forms/use-marketo-engage-data-source-in-form.md)のMarketo Engage データソースを設定し、フォーム要素をMarketo Engage フィールドにバインドします。

## 既存のフォームに対してMarketo Engageへの送信アクションを設定するには？

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

<span>このビデオは、コアコンポーネントのみに適用されます。 UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>


>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づいてアダプティブフォームの送信アクションを設定し、Adobe Marketo Engageにデータを送信できます。 Marketo Engageに送信アクションを設定するには、次の手順を実行します。

1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。
1. アダプティブフォームを開いて編集し、アダプティブフォームコンテナプロパティの&#x200B;**[!UICONTROL 送信]** セクションに移動し、送信アクションを&#x200B;**Marketo Engageに送信**&#x200B;として選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![Marketo送信アクション &#x200B;](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

アダプティブフォームの送信アクションを&#x200B;**Marketo Engageに送信**&#x200B;として設定した後、データをAdobe Marketo Engageに送信して処理できます。 それらのデータは、マーケティング施策の分析と最適化、フォローアップメールの自動化、フォームへの入力にもとづくトリガーワークフローの実行に活用できます。

>[!TAB コアコンポーネント]

コアコンポーネントに基づいてアダプティブフォームの送信アクションを設定し、Adobe Marketo Engageにデータを送信できます。 Marketo Engageに送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。 送信アクションを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開き、「**Marketo Engageに送信**」として送信アクションを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![Marketo送信アクション &#x200B;](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

アダプティブフォームの送信アクションを&#x200B;**Marketo Engageに送信**&#x200B;として設定した後、データをAdobe Marketo Engageに送信して処理できます。 それらのデータは、マーケティング施策の分析と最適化、フォローアップメールの自動化、フォームへの入力にもとづくトリガーワークフローの実行に活用できます。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成したアダプティブフォームの送信アクションを設定して、データをAdobe Marketo Engageに送信できます。 Marketo Engageに送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. エディターで&#x200B;**フォームプロパティを編集**&#x200B;拡張機能をクリックします。
**フォームプロパティ**&#x200B;ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Manager で&#x200B;**フォームプロパティを編集**&#x200B;拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については、[Extension Manager 機能のハイライト](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL Marketo Engageに送信]**」送信アクションを選択します。

   ![Marketo送信アクション &#x200B;](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

アダプティブフォームの送信アクションを&#x200B;**Marketo Engageに送信**&#x200B;として設定した後、データをAdobe Marketo Engageに送信して処理できます。 それらのデータは、マーケティング施策の分析と最適化、フォローアップメールの自動化、フォームへの入力にもとづくトリガーワークフローの実行に活用できます。

>[!ENDTABS]

## よくある質問（FAQ）

**Q: Marketo Engage スキーマに接続するように設定されたフォームの送信アクションを変更できますか？**
**A:** デフォルトでは、フォームがMarketo Engage スキーマに接続するように設定されている場合、**Marketoに送信** アクションが選択されます。 ただし、必要に応じて、フォームの送信アクションを変更できます。

## 次の手順

アダプティブフォームを[Munchkin ライブラリ &#x200B;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)と接続して、訪問回数、クリック数、フォーム送信数を追跡することもできます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
