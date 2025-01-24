---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: ht
source-wordcount: '877'
ht-degree: 100%

---


# フォームのオーサリング

Adobe Experience Manager では、フォームを作成する複数のエディターを提供およびサポートします。 以下を使用できます。
* ユニバーサルエディター（WYSIWYG オーサリング用）
* Microsoft Excel または Google Sheets（ドキュメントベースのオーサリングと呼ばれます）
* アダプティブフォームエディター（コアコンポーネント用または基盤コンポーネントベースのオーサリング用）

**[追加する画像]**

## ユニバーサルエディター（WYSIWYG オーサリング用）

ユニバーサルエディターは、WYSIWYG（見たままが得られる）機能を備えた多用途なビジュアルエディターであり、直感的なフォーム作成エクスペリエンスを実現します。 新しいフォームを作成する際は、最新の使いやすいデザインと便利なドラッグ＆ドロップインターフェイスを備えたユニバーサルエディターを使用することをお勧めします。

ユニバーサルエディターを使用してフォームを作成するには、AEM 環境で使用可能な Edge Delivery Services テンプレートを使用します。 これらのフォームは、Edge Delivery Services GitHub リポジトリの設定からルックアンドフィールを継承します。 Edge Delivery Services でこれらのフォームを公開できるようにするために、[AEM 環境と Edge Delivery Services GitHub リポジトリの間で接続](/help/edge/docs/forms/publishing-forms.md)が確立されます。

ユニバーサルエディターを使用したオーサリング方法の詳細な手順については、[ユニバーサルエディターを使用したコンテンツのオーサリング](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)の記事を参照してください。

## Microsoft Excel または Google Sheets（ドキュメントベースのオーサリングと呼ばれます）

Microsoft Excel または Google Sheets ファイルでドキュメントベースのオーサリングを使用してフォームを作成できるので、Google Sheets、Microsoft Excel、Microsoft SharePoint の堅牢なエコシステムと API を活用できます。 このアプローチは、高度な送信サービスを使用せずに単純なフォームを作成する場合に特に役立ちます。

Microsoft Excel または Google Sheets を使用してフォームの作成を開始するには、[AEM Forms ボイラープレートを使用して AEM プロジェクトを設定](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)し、ローカルマシンに対応する GitHub リポジトリのクローンを作成します。 AEM Forms Edge Delivery には、データのキャプチャと保存のためのフォーム作成プロセスを簡素化する、アダプティブフォームブロックと呼ばれる機能が用意されています。 Edge Delivery Services でアダプティブフォームブロックを使用してフォームを作成および公開する方法について詳しくは、[フォームの作成](/help/edge/docs/forms/create-forms.md)を参照してください。

## アダプティブフォームエディター（コアコンポーネント用または基盤コンポーネントベースのオーサリング用）

魅力的でレスポンシブ、かつ動的なフォームを作成できます。 アダプティブフォームエディターには、アダプティブフォームをすばやく作成できる、使いやすいウィザードが用意されています。 フォームウィザードには簡単なタブナビゲーション機能があり、基盤コンポーネントまたはコアコンポーネント、テーマ、データモデル、送信オプションなどに事前設定済みのテンプレートを選択して、効率的にフォームを作成できます。

[コアコンポーネントを含むフォームのオーサリング](/help/forms/creating-adaptive-form-core-components.md)を使用すると、カスタマイズ可能な標準化されたデータキャプチャコンポーネントを活用できるので、開発時間が短くなり、デジタル登録エクスペリエンスのメンテナンスコストが削減されます。 これらのフォームは、Edge Delivery Services でアダプティブフォームブロックを使用するか、AEM パブリッシュインスタンスを通じて公開できます。

[基盤コンポーネントを含むフォームのオーサリング](/help/forms/create-an-adaptive-form.md)では、従来のデータキャプチャコンポーネントを使用します。 これらのフォームは、AEM パブリッシュインスタンスを使用してのみ公開できます。

また、[AEM 環境と Edge Delivery Services GitHub リポジトリの間に接続](/help/edge/docs/forms/publishing-forms.md)を確立し、アダプティブフォームエディターを使用して作成したフォームを Edge Delivery Services に公開することもできます。

## 様々なタイプのフォームのオーサリングの中から選択する方法

次の表に、各オーサリングエディターの機能とユースケースの概要を示します。要件とフォーム送信のニーズに基づいて適切なエディターを選択するのに役立ちます。

| **フォームオーサリングエディター** | **主なアプローチ** | **機能** | **公開方法** | **ユースケース** |
|--------|-----------|-------|-------|------------------------------------------------|
| **ドキュメントベースのオーサリング** | フォームの作成には、Google Docs や Microsoft Office などの使い慣れたツールを活用します。 | フォームはスプレッドシートを使用して設計され、データは Google Sheets または Microsoft Excel スプレッドシートに直接送信されます。 </br> </br>これらのフォームを使用すれば、作成とデプロイを素早く行うことができます。 これらのフォームのカスタムコンポーネントとスタイルを開発するために、AEM の事前知識は必要ありません。 | これらのフォームは Edge Delivery Services で公開され、Google Lighthouse スコアが非常に高くなっています。 </br> </br>スコアが高いほどレンダリングが速くなり、SEO が向上します。 | これらのフォームは、迅速なプロトタイプ作成や、高度な送信サービスが必要ない基本フォームに最適です。 </br> </br>これらは、スプレッドシートへのデータストレージを必要とする調査、登録、フィードバックフォームに適しています。 これらのフォームは、Edge Delivery Services で公開されます |
| **ユニバーサルエディター**  </br> </br>新しいフォームを作成する場合は、ユニバーサルエディターを使用してフォームを作成します。 | 直感的なフォーム作成の WYSIWYG インターフェイスを提供します。 | フォームは、直感的なドラッグ＆ドロップインターフェイスを使用して設計されます。 </br> </br>これらのフォームは、対応するフォーム用に設定された Edge Delivery Services GitHub リポジトリからルックアンドフィールを借用します。 | これらのフォームは Edge Delivery Services で公開され、Google Lighthouse スコアが非常に高くなっています。 </br> </br>スコアが高いほどレンダリングが速くなり、SEO が向上します。 | これらのフォームは、Edge Delivery Service サイトおよびページ用のフォームを作成するのに最適です。 これらのフォームシナリオには、複雑なフォーム、複雑なワークフロー、カスタムアクション、または外部システムとの統合が含まれます。 |
| **アダプティブフォームエディター** | テンプレート、スタイル、定義済みフィールドを使用してフォームのオーサリングをすばやく開始するウィザード駆動型アプローチを提供します。 | これらのエディターを使用して、コアコンポーネントベースのフォームまたは基盤コンポーネントベースのフォームを作成します。 | これらのフォームは、Edge Delivery Services で、または AEM パブリッシュインスタンスを通じて公開できます。 | これらのエディターを使用して、コアコンポーネントベースのフォームまたは基盤コンポーネントベースのフォームを作成します。 複雑なフォーム、複雑なワークフロー、カスタムアクション、または外部システムとの統合が含まれるシナリオに最適です。 |


>[!NOTE]
>
>
> 以前はアダプティブフォームエディターで使用できた機能がユニバーサルエディターで使用できなくなった場合は、公式メールアドレスを使用して mailto:aem-forms-ea@adobe.com にメールを送信してリクエストできます。

## 関連記事

* [Microsoft Excel またはGoogle Sheets を使用したドキュメントベースのオーサリング](/help/edge/docs/forms/create-forms.md)
* [WYSIWYG オーサリング用ユニバーサルエディター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [アダプティブフォームの作成（基盤コンポーネント）](/help/forms/creating-adaptive-form.md)
* [アダプティブフォームの作成（コアコンポーネント）](/help/forms/create-an-adaptive-form.md)

## 関連トピック

{{see-more-forms-eds}}