---
title: 複数ステップのフォームシーケンスの作成方法
description: ' [!DNL Experience Manager Forms] を使用すると、アダプティブフォームのナビゲーションや記入を行う一連のフォームパネルを定義できます。'
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 93%

---

# 複数ステップのフォームシーケンスの概要 {#introduction-to-multi-step-form-sequence}

>[!NOTE]
>
> Adobeでは、（新しいアダプティブFormsの作成 [ または ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)[ AEM SitesページへのアダプティブFormsの追加 [ に、最新の拡張可能なデータキャプチャ ](/help/forms/creating-adaptive-form-core-components.md) コアコンポーネント ](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) を使用することをお勧めします。 これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古いアプローチを説明します。

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/introduction-form-sequence.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

フォーム作成者は、アダプティブフォームを使用すると非常に簡単に複数ステップのデータ取得エクスペリエンスを作成できます。複数パネルの作成や、各パネルと別の移動パターンとの関連付けに対する組み込みサポートが付属しています。フォーム作成者は、フォームフィールドを論理セクションでグループ化し、グループをパネルとして表示できます。パネル間の移動はすべてパネルレイアウトを使用して制御されます。作成者は、様々なレイアウトでパネルをアレンジできます。例えば、ウィザードレイアウトで順番に配置することも、タブ付きレイアウトを使って即興で配置することもできます。パネルレイアウトについては、「[アダプティブフォームのレイアウトの機能](layout-capabilities-adaptive-forms.md)」を参照してください。

一般的なフォームの記入では、データを取得する以上に、関連する多くのステップがあります。完全なフォーム送信ステップには、フォームへの電子署名、フォームに入力した情報の検証、支払い処理など、その他のステップが含まれる場合があります。これは、場合によって異なります。

データ取得に一連のステップを必要とするケースや、規則により特定の手順を踏む必要があるケースでは、[!DNL Experience Manager Forms] はフォーム全体でその共通の構造を適用する方法を提供します。フォーム構造の実装を事前に計画して、フォームのステップのシーケンスを定義します。![複数ステップのフォームシーケンスの例](assets/formpipeline.png)

複数ステップのフォームシーケンスの例

フォームの入力、検証、署名、確認のシーケンスを作成する必要がある場合の使用例を考えてみます。このようなシーケンスを作成する手順は次のとおりです。

1. フォームテンプレートを定義し、それに必要なパネルを追加します。シーケンスの各段階につき 1 つのパネルが必要です。ただし、パネル内にサブパネルを含めることができます。

   この例では、次のパネルを追加できます。

   * **[!UICONTROL 入力]**：データを取得するためのフォームフィールドが含まれます。ここではネストされたサブパネルを追加して、様々な種類の情報（個人、家族、財務など）のセクションを作成できます。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子サイン]**：XFA ベースのアダプティブフォームで使用できる&#x200B;**[!UICONTROL 署名]**&#x200B;コンポーネントが含まれます。電子サインには、次の署名サービスが含まれます。

      * Adobe Document Cloud 電子サインサービス
      * 手書き署名

   * **[!UICONTROL 確認]**：ユーザーがフォームに署名してシーケンスの確認（概要）段階に到達したときにフォーム送信の確認メッセージを表示する&#x200B;**[!UICONTROL 概要]**&#x200B;コンポーネントが含まれます。作成者は[!UICONTROL 概要]コンポーネントのテキストの構成、お礼のメッセージの表示、生成された PDF へのリンクの表示などを設定できます。

1. root パネルのレイアウトを **[!UICONTROL ウィザード]** として選択します。
1. 残りの手順を実行して、フォームテンプレートを作成します。<!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

フォームテンプレートでフォームのシーケンスを定義したら、そのテンプレートを使用して、適切なシーケンスで定義した基本構造を持つフォームを作成できます。フォームはいつでも要件に合わせてカスタマイズできます。


## 関連トピック {#see-also}

{{see-also}}