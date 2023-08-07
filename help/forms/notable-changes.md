---
title: AEM 6.5 Forms と AEM Cloud Services の違い
description: Experience Manager Forms のユーザーで、Adobe Experience Manager Forms as aCloud Service にアップグレードする予定ですか？AEM 6.5 Forms と AEM Cloud Services を比較し、アップグレードまたは Cloud Service への移行前に、最も重要な変更点を確認します。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 57acac078805bc195cb10c1e94462d5aa077b1af
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 97%

---

# 既存の Adobe Experience Manager 6.5 Forms ユーザー向けの主な変更点  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service では、Adobe Experience Manager Forms オンプレミスおよび [!DNL Adobe-Managed Service] 環境と比較して、既存の機能にいくつかの注目すべき変更点があります。主な違いを以下に示します。

## クラウドネイティブ機能

* このサービスは、アップグレードのダウンタイムなしに、新機能やアップデートの頻繁なロールアウト後に読み込まれ、回復と効率を最大化するために最適化されたトポロジーに基づく自動スケーリングを可能にするクラウドネイティブアーキテクチャです。

* このサービスには、Adobe Experience Manager Cloud Service インスタンスにデータを保存する送信アクションが含まれていないので、非常に安全です。フォームから取り込まれたデータは、設定済みのデータストアに直接送信されます。

* より迅速にフォームを配信およびレンダリングするのに役立つ無料の CDN（コンテンツ配信ネットワーク）も含まれています。


## 開発フローのアップデート

* このサービスは、コードを Cloud Service にデプロイする前に、ローカル環境（ローカルマシン）でカスタムコードを開発およびテストする SDK を提供します。開発者は、ローカルマシン上の SDK を使用して、カスタムコンポーネント、テーマ、ワークフローアプリケーション、設定、テンプレートなどを開発およびテストします。カスタムコードをローカル開発環境でテストした後、カスタムコードを [Forms CS 環境の開発またはステージング環境](/help/implementing/cloud-manager/deploy-code.md)にデプロイして、実稼働環境に昇格する前にさらにテストします。

* 開発者は、Cloud Service のコードとローカル開発環境を共通の [Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html?lang=ja)で管理します。AEM アーキタイプに基づく Git リポジトリは、AEM as a Cloud Service プログラムの作成時に自動的に作成されます。

  ![AEM as a cloud service プログラムでの git リポジトリの自動作成](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Forms as a Cloud Service の開発フローは、AEM Cloud Service の AEM アーキタイプに従っています。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEM は可変コンテンツと不変コンテンツの分割を考慮してコンテンツとコードを個別のサブパッケージに分離する必要があります。[Repository Modernizer ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=ja)を使用して、Adobe Experience Manager as a Cloud Service 向けに定義されているプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再構築します。

* Forms as a Cloud Service でカスタマーバンドルを使用する前に、最新バージョンの adobe-aemfd-docmanager でカスタムコードを再コンパイルします。

* [AEM Forms as a Cloud Service 移行ユーティリティ](/help/forms/migrate-to-forms-as-a-cloud-service.md)を使用して、<!-- AEM 6.3 Forms-->OSGi 上の AEM 6.4 Forms および OSGi 上の AEM 6.5 Forms から [!DNL AEM] as a Cloud Serviceにアダプティブフォーム、テーマ、テンプレート、クラウド設定を準備し移行します。[プログラムの Git リポジトリ](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)を使用して、既存のアダプティブフォームテンプレートを読み込みます。

* メールは、デフォルトで HTTP と HTTPs プロトコルのみをサポートしています。[サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)、メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。

## ローカライゼーション

* ローカライズされたアダプティブフォームの URL 規則で、URL でのロケールの指定がサポートされるようになりました。新しい URL 規則により、ローカライズされたフォームを Dispatcher または CDN にキャッシュできます。Cloud Service 環境では、`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` の代わりに `http://host:port/content/forms/af/<afName>.<locale>.html` の URL 形式を使用して、アダプティブフォームのローカライズ版をリクエストします。

* アドビでは、Dispatcher または CDN キャッシュを使用することをお勧めします。これにより、事前入力されたフォームのレンダリング速度を向上できます。


## アダプティブフォーム

* **ルールエディター：** AEM Forms as a Cloud Service は、強化された[ルールエディター](rule-editor.md#visual-rule-editor)を提供します。Forms as a Cloud Service では、コードエディターは使用できません。

  [移行ユーティリティ](/help/forms/migrate-to-forms-as-a-cloud-service.md)は、（コードエディターで作成した）カスタムルールを持つフォームを移行するのに役立ちます。ユーティリティは、このようなルールを Forms as a Cloud Service でサポートされるカスタム関数に変換します。再利用可能な関数をビジュアルルールエディターで使用することにより、引き続き、ルールスクリプトで取得した結果を利用できるようになります。`onSubmitError` または `onSubmitSuccess` 関数は、ルールエディターでアクションとして使用できるようになりました。

* **事前入力サービス：**&#x200B;デフォルトでは、事前入力サービスは、AEM 6.5 Forms のサーバー上でデータを結合するのではなく、クライアントでアダプティブフォームとデータを結合します。この機能により、アダプティブフォームの事前入力に必要な時間を短縮できます。Adobe Experience Manager Forms Server で結合アクションを実行するように常に設定できます。

* **メールの送信アクション**：添付ファイルを送信し、**メール**&#x200B;にレコードのドキュメント（DoR）を添付するオプションが提供されます。AEM 6.5 Forms で利用できる、**PDF としてメールで送信**&#x200B;アクションの代わりに使用できます。

* **自動フォーム変換サービス**：このサービスは、自動フォーム変換サービスのメタモデルを提供しません。メタモデルは、[フォームの自動変換サービスドキュメントからダウンロード](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#default-meta-model)できます。

* **XSD ベースのアダプティブフォーム：** XDP テンプレートを使用して、レコードのドキュメント用のテンプレートをデザインできます。このサービスは、XFA ベースのアダプティブフォームをサポートしていません

* **コンポーネント**：[アダプティブフォームコアコンポーネント](/help/forms/creating-adaptive-form-core-components.md)を使用してフォームをデザインできます。これらのコンポーネントは、WCM コアコンポーネントに基づき、BEM 標準に従っており、容易にカスタマイズできます。このサービスはフォーム内の署名エクスペリエンスをサポートしておらず、アダプティブフォームの概要コンポーネントと検証コンポーネントは含まれていません。

## Forms ポータル

* フォームポータルの検索とリスター、ドラフトと送信、リンクコンポーネントを使用して、ログインしているユーザーのフォームを一覧表示できます。フォームポータルの匿名での使用は、標準（OOTB）ではサポートされていません。フォームポータルをカスタマイズして、ログインしていないユーザー向けのフォームの表示を有効にすることができます。

* このサービスは、ドラフトと送信されたアダプティブフォームのメタデータを保持しません。

## ドキュメントサービス：

Forms as a Cloud Service には、ドキュメント生成とドキュメント操作の RESTful API が用意されています。これらの API を使用して、必要に応じて、ドキュメントをオンデマンドまたはバッチで生成および操作できます。

* **ドキュメントサービス：ドキュメント生成 API（出力サービス）**：1 回の API 呼び出しまたはバッチで、複数の DATA XML ファイルで使用できるテンプレートは 1 つだけです。1 回の API 呼び出しで、複数のデータファイルで複数のテンプレートを使用することはできません。

* **ドキュメント操作 API（Assembler サービス）**：

   * ドキュメントサービスまたはアプリケーションに依存する操作は使用できません。例えば、Microsoft Word から PDF、Microsoft Excel から PDF、HTML から PDF、PostScript（PS）から PDF、XDP から PDF forms への変換はサポートされていません。これらの操作は、それぞれ Microsoft Office、Adobe Acrobat、Adobe Distiller、Forms ドキュメントサービスに依存します。

   * コミュニケーションドキュメント操作 API でドキュメントを使用する前に、PDF 以外の形式のドキュメントを PDF 形式に変換してください。例えば、ドキュメントが Microsoft Office、HTML、PostScript（PS）、XDP 形式である場合、PDF でこれらのドキュメントを使用する前に、PDF 形式に変換します。このような変換には、[ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html?lang=ja) サービスを使用できます。

* AEM 6.5 Forms 環境を使用して、電子署名、暗号化、Reader Extension、プリンターに送信、PDF に変換および Barcoded Forms サービスを実行できます。


## データ統合（フォームデータモデル）

* また、JDBC コネクタ、Microsoft Dynamics、SalesForce、SOAP ベースの web サービス、OData をサポートするサービスもサポートしています。

* AEM ユーザープロファイルに接続して、ユーザー情報を取得および更新することもできます。

* フォームデータモデルでは、データを送信する際に HTTP および HTTPs エンドポイントのみをサポートしています。このサービスでは、REST コネクターの相互 SSL および SOAP データソースの x509 証明書ベースの認証をサポートしていません。

* Forms as a Cloud Service では、Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive、および一般的な CRUD（作成、読み取り、更新、削除）操作をサポートするサービスを、データストアとして使用できます。Open API Specification 2.0 と Open API Specification 3.0 の両方をサポートしています。


## 電子サイン

* このサービスは、Adobe Sign との OOTB 統合を提供し、電子サイン用の DocuSign をサポートします。

* また、このサービスは Adobe Sign の役割もサポートします。ビジネスユーザーが署名ワークフローを簡単に設定できるように、アダプティブフォームエディターで役割を設定できます。


## HTML5 Forms

* AEM 6.5 Forms 環境を使用して、次のことができます。

   * XDP ベースのフォームを HTML5 Forms としてレンダリングします。このサービスでは、HTML5 Forms（モバイルフォーム）をサポートしていません。

   * [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html?lang=ja) アプリを使用して、オフラインでデータをキャプチャし、次回オンラインに戻る際に同期します。

## インタラクティブコミュニケーション

* 通信 API を使用して、パーソナライズされたドキュメントを Forms as a Cloud Service 上でオンデマンドまたはバッチで生成できます。AEM 6.5 Forms 環境は、インタラクティブ通信とエージェント UI のユースケースに使用できます。

## 次へを参照

* [AEM Forms（オンプレミスおよび AMS 環境）からAEM Formsas a Cloud Service環境への移行](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [AEM SitesページへのアダプティブFormsの追加または作成](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [アダプティブフォーム（コアコンポーネント）の作成](/help/forms/creating-adaptive-form-core-components.md)

## 追加情報

* [AEM Forms as a Cloud Service の概要](/help/forms/home.md)
* [ローカル開発環境と初期開発プロジェクトの設定](/help/forms/setup-local-development-environment.md)
