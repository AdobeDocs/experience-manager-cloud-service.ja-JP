---
title: 複数ステップのフォームシーケンスの作成方法
description: ' [!DNL Experience Manager Forms] を使用すると、アダプティブフォームのナビゲーションや記入を行う一連のフォームパネルを定義できます。複数ステップのフォームシーケンスを作成する例として、使用例のアプローチを使用し、詳しく調べます。 '
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 100%

---

# 複数ステップのフォームシーケンスの概要 {#introduction-to-multi-step-form-sequence}

フォーム作成者は、アダプティブフォームを使用すると非常に簡単に複数ステップのデータ取得エクスペリエンスを作成できます。複数パネルの作成や、各パネルと別の移動パターンとの関連付けに対する組み込みサポートが付属しています。フォーム作成者は、フォームフィールドを複数の論理的なセクションにグループ分けし、グループをパネルとして表示できます。パネル間の移動はすべてパネルレイアウトを使用して制御されます。作成者は、様々なレイアウトでパネルを配置することができます。例えば、ウィザードレイアウトで順番に配置したり、タブ付きレイアウトでアドホックな方法で配置したりできます。パネルレイアウトについては、「[アダプティブフォームのレイアウトの機能](layout-capabilities-adaptive-forms.md)」を参照してください。

一般的なフォームの記入では、データを取得する以上に、関連する多くのステップがあります。完全なフォーム送信ステップには、フォームへの電子署名、フォームに入力した情報の検証、支払い処理など、その他のステップが含まれる場合があります。これらの手順は、個々の場合によって異なります。

データ取得に一連のステップを必要とするケースや、規則により特定の手順を踏む必要があるケースでは、[!DNL Experience Manager Forms] はフォーム全体でその共通の構造を適用する方法を提供します。フォーム構造の実装を事前に計画して、フォームのステップのシーケンスを定義します。![複数ステップのフォームシーケンスの例](assets/formpipeline.png)

複数ステップのフォームシーケンスの例

フォームの入力、検証、署名、確認のシーケンスを作成する必要がある場合の使用例を考えてみます。このようなシーケンスを作成する手順は次のとおりです。

1. フォームテンプレートを定義して、それに必要なパネルを追加します。シーケンスの各段階につき 1 つのパネルが必要です。ただし、パネル内にサブパネルを含めることができます。

   この例では、次のパネルを追加できます。

   * **[!UICONTROL 入力]**：データを取得するためのフォームフィールドが含まれます。ここではネストされたサブパネルを追加して、様々な種類の情報（個人、家族、財務など）のセクションを作成できます。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子サイン]**：XFA ベースのアダプティブフォームで使用できる&#x200B;**[!UICONTROL 署名]**&#x200B;コンポーネントが含まれます。電子サインには、次の署名サービスが含まれます。

      * Adobe Document Cloud 電子サインサービス
      * 手書き署名
   * **[!UICONTROL 確認]**：ユーザーがフォームに署名してシーケンスの確認（概要）段階に到達したときにフォーム送信の確認メッセージを表示する&#x200B;**[!UICONTROL 概要]**&#x200B;コンポーネントが含まれます。作成者は[!UICONTROL 概要]コンポーネントのテキストの構成、お礼のメッセージの表示、生成された PDF へのリンクの表示などを設定できます。



1. root パネルのレイアウトを&#x200B;**[!UICONTROL ウィザード]**&#x200B;として選択します。
1. 残りの手順を完了して、フォームテンプレートを作成します。<!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

フォームテンプレートでフォームのシーケンスを定義したら、適切なシーケンスで定義された基本構造を持つフォームを作成するためにそのテンプレートを使用できます。ただし、フォームはいつでも要件に合わせてカスタマイズできます。
