---
title: AEM 6.5 Formsと AEM Cloud Services の違い
description: Experience Manager Forms のユーザーで、Adobe Experience Manager Forms as aCloud Service にアップグレードする予定ですか？AEM 6.5 Formsと AEM Cloud Services を比較し、アップグレードまたはCloud Serviceへの移行前に、最も重要な変更点を確認します。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 14%

---

# 既存のAdobe Experience Manager 6.5 Formsユーザーの主な変更点  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Serviceは、Adobe Experience Manager Formsオンプレミスおよび [!DNL Adobe-Managed Service] 環境。 主な違いを以下に示します。

## クラウドネイティブ機能

* このサービスは、負荷、アップグレードのダウンタイムなし、新機能や更新の頻繁なロールアウト後、および耐障害性と効率性を最大限に高めるために最適化されたトポロジーに基づく自動スケーリングを可能にするクラウドネイティブアーキテクチャです。

* このサービスには、Adobe Experience ManagerCloud Serviceインスタンスにデータを保存する送信アクションが含まれていないので、非常に安全です。 フォームから取り込まれたデータは、設定済みのデータストアに直接送信されます。

* より迅速にフォームを配信およびレンダリングするのに役立つ無料の CDN（コンテンツ配信ネットワーク）も含まれています。


## 開発フローの更新

* このサービスは、コードをCloud Serviceにデプロイする前に、ローカル環境（ローカルマシン）でカスタムコードを開発およびテストする SDK を提供します。 開発者は、ローカルマシン上の SDK を使用して、カスタムコンポーネント、テーマ、ワークフローアプリケーション、設定、テンプレートなどを開発およびテストします。 カスタムコードをローカル開発環境でテストした後、カスタムコードをにデプロイします。 [Forms CS 環境の開発またはステージ環境](/help/implementing/cloud-manager/deploy-code.md) を参照してください。

* 開発者は、共通のCloud Serviceおよびローカル開発環境のコードを維持する [git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). AEMアーキタイプに基づく Git リポジトリは、AEM as a Cloud Serviceプログラムの作成時に自動的に作成されます。

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Serviceの開発フローは、AEM Cloud ServiceのAEMアーキタイプに従っています。 ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEM は可変コンテンツと不変コンテンツの分割を考慮してコンテンツとコードを個別のサブパッケージに分離する必要があります。[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=ja)Repository Modernizer ツールを使用して、Adobe Experience Manager as a Cloud Service 向けに定義されているプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再構築します。

* Forms as a Cloud Serviceで顧客バンドルを使用する前に、最新バージョンの adobe-aemfd-docmanager でカスタムコードを再コンパイルします。

* 用途 [AEM Formsas a Cloud Service移行ユーティリティ](/help/forms/migrate-to-forms-as-a-cloud-service.md) アダプティブForms、テーマ、テンプレート、クラウド設定を次のように準備して移行する <!-- AEM 6.3 Forms--> OSGi 上のAEM 6.4 Formsと OSGi 上のAEM 6.5 Formsを [!DNL AEM] as a Cloud Service。 用途 [プログラムの Git リポジトリ](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 既存のアダプティブフォームテンプレートを読み込むには、次の手順を実行します。

* 電子メールは、デフォルトで HTTP および HTTPs プロトコルのみをサポートしています。 [サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)、メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。

## ローカライゼーション

* ローカライズされたアダプティブフォームの URL 規則で、URL でのロケールの指定がサポートされるようになりました。新しい URL 規則により、ローカライズされたフォームを Dispatcher または CDN にキャッシュできます。Cloud Service環境では、URL 形式を使用します。 `http://host:port/content/forms/af/<afName>.<locale>.html` アダプティブフォームのローカライズ版をリクエストするには `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* アドビでは、Dispatcher または CDN キャッシュを使用することをお勧めします。これにより、事前入力されたフォームのレンダリング速度を向上できます。


## アダプティブフォーム

* **ルールエディター：** AEM Formsas a Cloud Service家は、堅固な [ルールエディター](rule-editor.md#visual-rule-editor). コードエディターは、Forms as a Cloud Serviceでは使用できません。

   この [移行ユーティリティ](/help/forms/migrate-to-forms-as-a-cloud-service.md) は、（コードエディターで作成された）カスタムルールを持つフォームを移行する際に役立ちます。 ユーティリティは、これらのルールを、Forms as a Cloud Serviceでサポートされるカスタム関数に変換します。 ルールエディターで再利用可能な関数を使用して、ルールスクリプトで取得した結果を引き続き取得できます。 この `onSubmitError` または `onSubmitSuccess` 関数は、ルールエディターでアクションとして使用できるようになりました。

* **事前入力サービス：** デフォルトでは、事前入力サービスは、AEM 6.5 Formsでのサーバー上のデータの結合とは異なり、クライアント側でデータをアダプティブフォームに結合します。 この機能により、アダプティブフォームの事前入力に要する時間が短縮されます。 Adobe Experience Manager Forms Server で結合アクションを実行するようにをいつでも設定できます。

* **送信アクション：** この **電子メール** 送信アクションには、添付ファイルを送信し、電子メールにレコードのドキュメント (DoR) を添付するオプションが用意されています。 これを **メールをPDF** AEM 6.5 Formsで使用可能なアクション。

* **automated forms conversionサービス**:このサービスは、Automated forms conversionサービスのメタモデルを提供しません。 以下が可能です。 [automated forms conversionサービスドキュメントからダウンロード](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **XSD ベースのアダプティブForms:** XDP-template を使用して、レコード用のドキュメントのテンプレートをデザインできます。 このサービスは、XFA ベースのアダプティブFormsをサポートしていません

* **コンポーネント**:以下を使用できます。 [アダプティブFormsコアコンポーネント](/help/forms/creating-adaptive-form-core-components.md) フォームをデザインする場合。 これらのコンポーネントは、WCM コアコンポーネントに基づいており、BEM 標準に従っており、容易にカスタマイズできます。 このサービスは、フォーム内署名機能をサポートしておらず、アダプティブフォームの概要コンポーネントと検証コンポーネントが含まれていません

## Forms ポータル

* Forms Portal の Search &amp; Lister、ドラフトと送信およびリンクコンポーネントを使用して、ログインしているユーザーのフォームを一覧表示できます。 Forms Portal の匿名での使用は、標準ではサポートされていません (OOTB)。 Forms Portal をカスタマイズして、ログインしていないユーザー向けのフォームの表示を有効にすることができます。

* このサービスは、ドラフトおよび送信されたアダプティブFormsのメタデータを保持しません。

## ドキュメントサービス:

Forms as a Cloud Serviceには、ドキュメント生成とドキュメント操作の RESTful API が用意されています。 これらの API を使用して、必要に応じて、ドキュメントをオンデマンドで、またはバッチで生成または操作できます。

* **ドキュメントサービス：ドキュメント生成 API（Output サービス）**:1 回の API 呼び出しまたはバッチで、複数の DATA XML ファイルで使用できるテンプレートは 1 つだけです。 1 回の API 呼び出しで複数のデータファイルで複数のテンプレートを使用することはできません。

* **ドキュメント操作 API（Assembler サービス）**:

   * Document Services またはアプリケーションに依存する操作は使用できません。 例えば、Microsoft Word からPDFへ、Microsoft Excel からPDFへ、およびPDFへのHTML、PostScript(PS) からPDFへの、XDP からPDF formsへの変換はサポートされていません。 これらの操作は、それぞれMicrosoft Office、Adobe Acrobat、AdobeDistiller、Forms Document Service に依存します。

   * Communications Document Manipulation API でドキュメントを使用する前に、PDF以外の形式のドキュメントをPDF形式に変換してください。 例えば、ドキュメントがMicrosoft Office、HTML、PostScript(PS)、XDP 形式の場合、PDFドキュメントで使用する前に、これらのドキュメントをPDF形式に変換します。 以下を使用して、 [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) このようなコンバージョンに対するサービス。

* デジタル署名、暗号化、Reader拡張、プリンターに送信、PDFの変換、および Barcoded FormsサービスにAEM 6.5 Forms環境を使用できます。


## データ統合（フォームデータモデル）

* また、JDBC コネクタ、Microsoft Dynamics、SalesForce、SOAP ベースの Web サービス、OData をサポートするサービスもサポートしています。

* また、AEMユーザープロファイルに接続して、ユーザー情報を取得および更新することもできます。

* Formsデータモデルでは、データの送信に HTTP および HTTPS エンドポイントのみをサポートしています。 このサービスは、REST コネクタの相互 SSL および SOAP データソースの x509 証明書ベースの認証をサポートしていません。

* Formsas a Cloud Serviceでは、Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive および一般的な CRUD（作成、読み取り、更新、削除）操作をサポートするサービスをデータストアとして使用できます。Open API 仕様 2.0 と Open API 3.0 の両方の仕様がサポートされています。


## E 署名

* このサービスは、Adobe Signとの OOTB 統合を提供し、電子署名用の DocuSign をサポートします。

* また、このサービスはAdobe Signの役割もサポートします。 ビジネスユーザーが署名ワークフローを簡単に設定できるよう、アダプティブFormsエディターで役割を設定することができます。


## HTML5 のフォーム

* AEM 6.5 Forms環境を使用して、次のことができます。

   * XDP ベースのフォームをHTML5 Formsとしてレンダリングします。 このサービスは、HTML5 Forms (Mobile Forms) をサポートしていません。

   * 次回オンラインに戻る際にオフラインでデータをキャプチャし、同期する [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) アプリを使用します。

## インタラクティブコミュニケーション

* 通信 API を使用して、パーソナライズされたドキュメントをオンデマンドで、またはForms as a Cloud Service上でバッチで生成できます。 AEM 6.5 Forms環境は、インタラクティブ通信とエージェント UI のユースケースに使用できます。


