---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 1244bafe1263c52a584b587845c1a12b9ddfd333
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 57%

---


# Edge Delivery ServicesForms

Adobe Edge 配信サービス Formsは、フォームの作成、実行、処理の方法を変えます。 Edge Delivery Servicesを活用すると、高速で安全な、可用性の高いデジタルフォームを作成でき、迅速な開発環境でユーザーエクスペリエンスと運用効率を向上させることができます。 Edge Delivery Services Formsを使用すると、コンバージョンを促進し、コストを削減し、コンテンツ配信を高速化できます。

## Edge Delivery Services Formsの利点

* **より高速なフォーム作成**：完璧な Lighthouse スコアで高性能のフォームを作成し、リアルタイムユーザーモニタリング（RUM）を使用して実世界のパフォーマンスを継続的に監視します。

* **効率化されたオーサリングプロセス**：複数のソースからコンテンツを容易に管理し、柔軟性を高めます。 すぐに使用でき、WYSIWYGとドキュメントベースのオーサリングの両方を使用してフォームを作成できるので、様々なコンテンツ形式をシームレスに統合できます。

* **技術者以外のユーザーでも使用しやすい**: Edge Delivery Servicesを使用すると、プログラマーでなくても、プログラミングに関する豊富な知識を必要とせずにフォームを簡単に管理および公開できます。

* **ユーザーエクスペリエンスの向上**：迅速な読み込み時間とスムーズなインタラクションを実現し、最小限の待ち時間と直感的なフォーム入力エクスペリエンスをユーザーに提供します。

* **サーバーレス実行**:Edge Delivery Servicesを使用すると、フォームロジックのサーバーレス実行が可能になります。 変更してはいけないものの一例は、次のとおりです。

   * **クライアントサイドの検証**：フォームフィールドの検証はクライアントサイドで行われるので、ラウンドトリップの遅延が減ります。

   * **事前入力およびPersonalization**：フォームデータの事前入力は、シームレスなユーザーエクスペリエンスを実現するためにクライアントサイドで処理されます。

   * **送信処理**：中央のサーバーを使用せずに、フォーム送信を検証し、安全に転送します

## Edge Delivery Services Formsの仕組み

ユーザーは、Edge Delivery Services Drive、SharePoint、ユニバーサルエディター（Google オーサリング）などのドキュメントベースのオーサリングツールを使用して、WYSIWYG Formsを作成しながら、GitHub リポジトリで使用できる基本的なスタイル、動作、コンポーネントを活用できます。 オーサリングが完了すると、Edge Delivery Services Formsは、Forms Submission Service を使用して任意のプラットフォームにデータを送信できます。

![Edge Delivery Services Formsの仕組み ](/help/edge/docs/forms/assets/eds-forms-working.png)

### Edge Delivery Services Formsの主要コンポーネント

Edge Delivery サービス Formsの主なコンポーネントは次のとおりです。

* **GitHub リポジトリ**:GitHub リポジトリは、Edge Delivery Services Formsを作成するためのボイラープレートとして機能します。 フォームは、リポジトリの基本的なスタイル設定と機能を活用し、ユーザーがEdge Delivery Services Formsにカスタマイズとカスタムコンポーネントを追加できるようにします。

* **フォームオーサリング**:Edge Delivery Services Formsでは、WYSIWYGとドキュメントベースの 2 種類のオーサリングをサポートしています。 ドキュメントベースのオーサリングでは、Google DocsやMicrosoft Office などの使い慣れたツールを使用してフォームを作成できます。 WYSIWYGのオーサリング機能を使用すると、ユニバーサルエディターを使用してフォームを視覚的にデザインできます。また、技術に詳しくないユーザーでも、フォームを簡単に作成および管理できます。 ユニバーサルエディターを使用すると、直感的なフォーム作成操作が可能になり、多数のフォーム機能にアクセスできます。

* **Forms送信サービス**: Forms送信サービスを使用すると、OneDrive、SharePoint、Google シートなど、任意のプラットフォームでフォーム送信データを保存でき、好みのシステム内でフォームデータに簡単にアクセスして管理できます。

## フォームのオーサリング

Adobe Experience Manager では、フォームを作成する複数のエディターを提供およびサポートします。 以下を使用できます。
* [ユニバーサルエディター（WYSIWYG オーサリング用）](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel または Google Sheets（ドキュメントベースのオーサリングと呼ばれます）](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### ユニバーサルエディター（WYSIWYG オーサリング用）

ユニバーサルエディターは、WYSIWYG（見たままが得られる）機能を備えた多用途なビジュアルエディターであり、直感的なフォーム作成エクスペリエンスを実現します。 新しいフォームを作成する際は、最新の使いやすいデザインと便利なドラッグ＆ドロップインターフェイスを備えたユニバーサルエディターを使用することをお勧めします。

ユニバーサルエディターを使用してフォームを作成するには、AEM 環境で使用可能な Edge Delivery Services テンプレートを使用します。 これらのフォームは、Edge Delivery Services GitHub リポジトリの設定からルックアンドフィールを継承します。 Edge Delivery Services でこれらのフォームを公開できるようにするために、[AEM 環境と Edge Delivery Services GitHub リポジトリの間で接続](/help/edge/docs/forms/publishing-forms.md)が確立されます。

ユニバーサルエディターを使用したオーサリング方法の詳細な手順については、[ユニバーサルエディターを使用したコンテンツのオーサリング](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)の記事を参照してください。

### Microsoft Excel または Google Sheets（ドキュメントベースのオーサリングと呼ばれます）

Microsoft Excel または Google Sheets ファイルでドキュメントベースのオーサリングを使用してフォームを作成できるので、Google Sheets、Microsoft Excel、Microsoft SharePoint の堅牢なエコシステムと API を活用できます。 このアプローチは、高度な送信サービスを使用せずに単純なフォームを作成する場合に特に役立ちます。

Microsoft Excel または Google Sheets を使用してフォームの作成を開始するには、[AEM Forms ボイラープレートを使用して AEM プロジェクトを設定](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)し、ローカルマシンに対応する GitHub リポジトリのクローンを作成します。 AEM Forms Edge Delivery には、データのキャプチャと保存のためのフォーム作成プロセスを簡素化する、アダプティブフォームブロックと呼ばれる機能が用意されています。 Edge Delivery Services でアダプティブフォームブロックを使用してフォームを作成および公開する方法について詳しくは、[フォームの作成](/help/edge/docs/forms/create-forms.md)を参照してください。

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### 様々なタイプのフォームのオーサリングの中から選択する方法

次の表に、各オーサリングエディターの機能とユースケースの概要を示します。要件とフォーム送信のニーズに基づいて適切なエディターを選択するのに役立ちます。

| **フォームオーサリングエディター** | **主なアプローチ** | **機能** | **公開方法** | **ユースケース** |
|--------|-----------|-------|-------|------------------------------------------------|
| **ドキュメントベースのオーサリング** | フォームの作成には、Google Docs や Microsoft Office などの使い慣れたツールを活用します。 | フォームはスプレッドシートを使用して設計され、データは Google Sheets または Microsoft Excel スプレッドシートに直接送信されます。 </br> </br>これらのフォームを使用すれば、作成とデプロイを素早く行うことができます。 これらのフォームのカスタムコンポーネントとスタイルを開発するために、AEM の事前知識は必要ありません。 | これらのフォームは Edge Delivery Services で公開され、Google Lighthouse スコアが非常に高くなっています。 </br> </br>スコアが高いほどレンダリングが速くなり、SEO が向上します。 | これらのフォームは、迅速なプロトタイプ作成や、高度な送信サービスが必要ない基本フォームに最適です。 </br> </br>これらは、スプレッドシートへのデータストレージを必要とする調査、登録、フィードバックフォームに適しています。 これらのフォームは、Edge Delivery Services で公開されます |
| **ユニバーサルエディター**  </br> </br>新しいフォームを作成する場合は、ユニバーサルエディターを使用してフォームを作成します。 | 直感的なフォーム作成の WYSIWYG インターフェイスを提供します。 | フォームは、直感的なドラッグ＆ドロップインターフェイスを使用して設計されます。 </br> </br>これらのフォームは、対応するフォーム用に設定された Edge Delivery Services GitHub リポジトリからルックアンドフィールを借用します。 | これらのフォームは Edge Delivery Services で公開され、Google Lighthouse スコアが非常に高くなっています。 </br> </br>スコアが高いほどレンダリングが速くなり、SEO が向上します。 | これらのフォームは、Edge Delivery Service サイトおよびページ用のフォームを作成するのに最適です。 これらのフォームシナリオには、複雑なフォーム、複雑なワークフロー、カスタムアクション、または外部システムとの統合が含まれます。 |

>[!NOTE]
>
>
> 以前はアダプティブフォームエディターで使用できた機能がユニバーサルエディターで使用できなくなった場合は、公式メールアドレスを使用して mailto:aem-forms-ea@adobe.com にメールを送信してリクエストできます。

## 関連トピック

{{see-more-forms-eds}}




