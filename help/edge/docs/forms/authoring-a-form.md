---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 2%

---


# フォームのオーサリング

Adobe Experience Managerでは、フォームを作成するために複数のエディターを提供およびサポートしています。 以下を使用できます。
* ユニバーサルエディター（WYSIWYG オーサリング用）
* Microsoft Excel シートまたはGoogle シート （ドキュメントベースのオーサリングと呼ばれます）
* アダプティブ Forms エディター（コアコンポーネント用または基盤コンポーネントベースのオーサリング用）

**[追加する画像]**

## ユニバーサルエディター（WYSIWYG オーサリング用）

ユニバーサルエディターは汎用性の高いビジュアルエディターで、WYSIWYG（What-You-See-Is-What-You-Get）機能を提供し、直感的なフォーム作成エクスペリエンスを実現します。 新しいフォームを作成する際は、ユニバーサルエディターを使用することをお勧めします。最新の使いやすいデザインと、便利なドラッグ&amp;ドロップインターフェイスが用意されているからです。

ユニバーサルエディターを使用してフォームを作成するには、AEM環境で使用可能なEdge Delivery Servicesテンプレートを使用します。 これらのフォームは、Edge Delivery Services GitHub リポジトリの設定からルックアンドフィールを継承しています。 [AEM環境とEdge Delivery Services GitHub リポジトリの間の接続 ](/help/edge/docs/forms/publishing-forms.md) が確立され、これらのフォームをEdge Delivery Servicesに公開できるようになります。

ユニバーサルエディターを使用したコンテンツのオーサリング手順について詳しくは、[ ユニバーサルエディターを使用したコンテンツのオーサリング ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring) を参照してください。

## Microsoft Excel シートまたはGoogle シート （ドキュメントベースのオーサリングと呼ばれます）

Microsoft Excel ファイルまたはMicrosoft Sheets ファイルを使用したドキュメントベースのオーサリングを使用してフォームを作成すると、Google Sheets、Microsoft Excel およびGoogle SharePointの堅牢なエコシステムと API を活用できます。 このアプローチは、高度な送信サービスを使用せずに単純なフォームを作成する場合に特に役立ちます。

Microsoft Excel またはGoogle Sheets を使用してフォームの作成を開始するには、[AEM Forms ボイラープレートを使用してAEM プロジェクトを設定 ](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) し、対応する GitHub リポジトリをローカルマシンにクローンします。 AEM Forms Edge Deliveryには、アダプティブ Forms ブロックと呼ばれる機能が用意されています。この機能により、データのキャプチャと保存を行うフォームを簡単に作成できます。 Edge Delivery Servicesでアダプティブ Forms ブロックを使用してフォームを作成および公開する方法については、[ フォームの作成 ](/help/edge/docs/forms/create-forms.md) を参照してください。

## アダプティブ Forms エディター（コアコンポーネント用または基盤コンポーネントベースのオーサリング用）

魅力的でレスポンシブ、かつ動的なフォームを作成できます。 アダプティブフォームエディターは、アダプティブFormsをすばやく作成できる、使いやすいウィザードを備えています。 フォームウィザードでは、タブ操作が容易で、基盤コンポーネントまたはコアコンポーネント、テーマ、データモデル、送信オプション用の事前設定済みテンプレートを選択して、フォームを効率的に作成できます。

[ コアコンポーネントを含むフォームのオーサリング ](/help/forms/creating-adaptive-form-core-components.md) を使用すると、標準化されたデータキャプチャコンポーネントを活用してカスタマイズできるため、開発時間が短縮され、デジタル登録エクスペリエンスのメンテナンスコストが削減されます。 これらのフォームは、Edge Delivery ServicesのアダプティブFormsブロックを使用して、またはAEM Publish インスタンスを通じて公開できます。

[ 基盤コンポーネントを使用したフォームのオーサリング ](/help/forms/create-an-adaptive-form.md) は、従来のデータキャプチャコンポーネントを使用します。 これらのフォームは、AEM Publish インスタンスを使用してのみ公開できます。

また、AEM環境とEdge Delivery Services GitHub リポジトリの間に [ 接続 ](/help/edge/docs/forms/publishing-forms.md) を確立することにより、Edge Delivery ServicesでアダプティブFormsエディターを使用して作成されたフォームを公開することもできます。

## フォームのオーサリングで様々なタイプを選択する方法

次の表に、各オーサリングエディターの機能とユースケースの概要を示します。要件とフォーム送信のニーズに基づいて適切な機能を選択するのに役立ちます。

| **フォームオーサリングエディター** | **主要アプローチ** | **機能** | **公表の方法** | **ユースケース** |
|--------|-----------|-------|-------|------------------------------------------------|
| **ドキュメントベースのオーサリング** | は、Google DocsやMicrosoft Office などの使い慣れたツールを活用してフォームを作成します。 | Formsはスプレッドシートを使用して設計され、データはGoogle シートまたはMicrosoft Excel シートに直接送信されます。</br> </br> これらのフォームは、作成とデプロイが迅速です。 これらのフォームのカスタムコンポーネントとスタイルを開発するために、AEMに関する予備知識は必要ありません。 | これらのフォームはEdge Delivery Servicesに公開され、Google Lighthouse スコアが非常に高くなっています。</br> </br> スコアが高いと、レンダリングが速くなり、SEO が向上します。 | これらのフォームは、高度な送信サービスが必要ないクイックプロトタイプや基本フォームに最適です。</br> </br> これらは、スプレッドシートへのデータストレージを必要とする調査、登録、フィードバックフォームに適しています。 これらのフォームは、Edge Delivery サービスで公開されます |
| **ユニバーサルエディター** </br> </br> 新しいフォームを作成する場合は、ユニバーサルエディターを使用してフォームを作成します。 | は、直感的なフォーム作成のためのWYSIWYG インターフェイスを提供しています。 | Formsは、直感的なドラッグ&amp;ドロップインターフェイスを使用して設計されています。</br> </br> これらのフォームは、対応するフォームの設定済みEdge Delivery Services GitHub リポジトリからルックアンドフィールを借ります。 | これらのフォームはEdge Delivery Servicesに公開され、Google Lighthouse スコアが非常に高くなっています。</br> </br> スコアが高いと、レンダリングが速くなり、SEO が向上します。 | これらのフォームは、Edge Delivery サービスのサイトやページ用のフォームを作成するのに最適です。 複雑なフォーム、複雑なワークフロー、カスタムアクション、外部システムとの統合などが含まれるフォームシナリオ |
| **アダプティブFormsエディター** | は、テンプレート、スタイル設定、定義済みフィールドを使用してフォームのオーサリングをすばやく開始するためのウィザード駆動型アプローチを提供します。 | これらのエディターを使用して、コアコンポーネントベースのフォームまたは基盤コンポーネントベースのフォームを作成します。 | これらのフォームは、Edge Delivery Services上またはAEM Publish インスタンスを介して公開できます。 | これらのエディターを使用して、コアコンポーネントベースのフォームまたは基盤コンポーネントベースのフォームを作成します。 複雑なフォーム、複雑なワークフロー、カスタムアクション、外部システムとの統合などが含まれるシナリオに最適です。 |


>[!NOTE]
>
>
> ユニバーサルエディターに見つからない機能のうち、以前にアダプティブForms エディターで使用できたものが見つかった場合は、公式メールアドレスを使用してmailto:aem-forms-ea@adobe.comにメールで送信することでリクエストできます。

## 関連記事

* [Microsoft Excel またはGoogle Sheets を使用したドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)
* [WYSIWYG オーサリング用ユニバーサルエディター ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [アダプティブフォームの作成（基盤コンポーネント）](/help/forms/creating-adaptive-form.md)
* [アダプティブフォーム（コアコンポーネント）の作成](/help/forms/create-an-adaptive-form.md)

## 関連トピック

{{see-more-forms-eds}}