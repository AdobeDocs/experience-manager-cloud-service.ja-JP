---
title: AEM 6.5 Forms と AEM 6.4 Forms から  [!DNL AEM Forms] as a Cloud Service 環境に移行する方法
description: ' [!DNL AEM Forms] オンプレミス環境から [!DNL AEM Forms] as a Cloud Service 環境への移行'
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: b11979acc23efe5f1af690443180a6b456d589ed
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 74%

---

# [!DNL AEM Forms] as a Cloud Service への移行  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

アダプティブフォーム、テーマ、テンプレート、クラウドの設定情報は、OSGi 上の <!-- AEM 6.3 Forms--> AEM 6.4 Forms および OSGi の AEM 6.5 Forms から [!DNL AEM] as a Cloud Service に移行できます。これらのアセットを移行する前に、移行ユーティリティを使用して、以前のバージョンで使用されていた形式を [!DNL AEM] as a Cloud Service で使用されていた形式に変換します。移行ユーティリティを実行すると、以下の項目が更新されます。

* アダプティブフォームのカスタムコンポーネント
* アダプティブフォームのテンプレートとテーマ
* クラウドの設定情報
* コードエディターのスクリプトは再利用可能な関数に変換され、ビジュアルルールに適用されます。

## 考慮事項 {#consideration}

* このサービスは、OSGi 環境上の [!DNL AEM Forms] のみからコンテンツを移行するのに役立ちます。JEE 上の [!DNL AEM Forms] からクラウドサービス環境へのコンテンツの移行はサポートされていません。

* （AEM 6.3 Forms、または AEM 6.4 Forms または AEM 6.5 Forms にアップグレードした旧バージョンの環境のみ）AEM 6.3 Forms または以前のバージョンで使用可能な、初期設定のテンプレートおよびテーマに基づくアダプティブフォームは、[!DNL AEM Forms] as a Cloud Service ではサポートされていません。

* 検証ステップは使用できません。こうしたフォームを Cloud Service 環境に移動する前に、既存のアダプティブフォームから検証ステップを削除します。

* アダプティブFormsの署名ステップは使用できません。 既存のアダプティブフォームから署名ステップを削除します。ブラウザー内署名エクスペリエンスを使用するようにアダプティブフォームを設定します。アダプティブフォームの送信時に、ブラウザー内で契約書に署名するための Adobe Sign 契約書が表示されます。ブラウザー内署名エクスペリエンスにより、署名をより迅速に行えるようになり、署名者にとって時間の節約になります。

## AEM 6.5 Formsとの違い

| 機能 | AEM 6.5 Formsとの違い |
|--------------|-----------|
| HTML5 Forms (Mobile Forms) | このサービスは、HTML5 Forms (Mobile Forms) をサポートしていません。 XDP ベースのフォームをHTML5 Formsとしてレンダリングする場合、AEM 6.5 Forms上で引き続きこの機能を使用できます。 |
| アダプティブフォーム | <li><b>XSD ベースのアダプティブForms:</b> このサービスは、HTML5 Forms (Mobile Forms) をサポートしていません。 XDP ベースのフォームをHTML5 Formsとしてレンダリングする場合、AEM 6.5 Forms上で引き続きこの機能を使用できます。 </li> <li><b> アダプティブフォームテンプレート：</b> ビルドパイプラインと、プログラムの対応する Git リポジトリを使用して、既存のアダプティブフォームテンプレートを読み込みます。 </li><li><b>ルールエディター：</b> AEM Formsas a Cloud Service家は、堅固な [ルールエディター](rule-editor.md#visual-rule-editor). コードエディターは、Forms as a Cloud Serviceでは使用できません。 移行ユーティリティは、カスタムルール（コードエディターで作成）を持つフォームを移行する場合に役立ちます。 ユーティリティは、これらのルールを、Forms as a Cloud Serviceでサポートされるカスタム関数に変換します。 ルールエディタで再利用可能な関数を使用して、ルールスクリプトで取得した結果を引き続き取得できます。 `onSubmitError` または `onSubmitSuccess` 関数は、ルールエディターのアクションとして使用できるようになりました。 </li> <li><b>ドラフトと送信：</b> このサービスは、ドラフトおよび送信されたアダプティブFormsのメタデータを保持しません。 </li> <li><b> 事前入力サービス：</b> デフォルトでは、事前入力サービスは、AEM 6.5 Formsでのサーバー上のデータの結合とは異なり、クライアント側でデータをアダプティブフォームに結合します。 この機能により、アダプティブフォームの事前入力に要する時間が短縮されます。 Adobe Experience Manager Forms Server で結合アクションを実行するようにをいつでも設定できます。 </li><li><b>送信アクション：</b> この **メールをPDF** アクションは使用できません。 **メール**&#x200B;の送信アクションでは、添付ファイルを送信し、メールにレコードのドキュメント（DoR）を添付するオプションが提供されます。 </li> |
| フォームデータモデル | <li>Formsデータモデルでは、データの送信に HTTP および HTTPs エンドポイントのみをサポートしています。 </li><li>Forms as a Cloud Serviceでは、Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive および一般的な CRUD（作成、読み取り、更新、削除）操作をサポートするサービスをデータストアとして使用できます。 このサービスは、JDBC コネクタ、Rest コネクタの相互 SSL、SOAP データソースの x509 証明書ベースの認証をサポートしていません。 </li> |
| 自動フォーム変換サービス | このサービスは、Automated forms conversionサービスのメタモデルを提供しません。 以下が可能です。 [automated forms conversionサービスドキュメントからダウンロード](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model). |
| 設定 | <li>メールは、デフォルトでは HTTP プロトコルおよび HTTPs プロトコルのみをサポートします。[サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)、メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。 </li> <li>カスタムバンドルを使用する場合は、Forms as a Cloud Serviceでこれらのバンドルを使用する前に、最新バージョンの adobe-aemfd-docmanager でコードを再コンパイルします。</li> |
| ドキュメント操作 API（Assembler サービス） | このサービスは、他のサービスやアプリケーションに依存する操作をサポートしていません。 <li>ドキュメント形式以外のドキュメントをPDF形式に変換することはできません。 例えば、Microsoft Word からPDFへ、Microsoft Excel からPDFへ、PDFへのHTMLはサポートされていません</li><li>AdobeDistillerベースの変換はサポートされていません。 例えば、PostScript(PS) からPDF</li><li>Forms Service-based Conversions はサポートされていません。 例えば、XDP からPDF forms。</li><li>署名付きPDFまたは透明PDFを別の形式に変換することはサポートされていません。</li> |

## 前提条件 {#prerequisites}

* お使いの Forms Cloud Service プログラムで[「Forms - デジタル登録」オプションを有効に](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=ja#editing-program)し、[パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja)します。

   ![ドライランの結果](assets/enable-add-on.png)

* クラウドサービス環境では、移行ユーティリティはユーザーマッピングツールおよびコンテンツ転送ツールと連携して機能します。移行ユーティリティは、[!DNL AEM Forms] アセットをクラウドサービスと互換性のあるものにし、コンテンツ転送ツールは、コンテンツを [!DNL AEM Forms] 環境から[!DNL AEM] as a Cloud Service 環境に移行します。移行ユーティリティを使用する前に、[AEM as a Cloud Service に移行する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=ja)プロセスを学習します。このプロセスには次の 2 つのツールがあります。
   * [ユーザーマッピングツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#cloud-migration)：ユーザーマッピングツールは、対応するアドビの IMS ユーザーアカウントでユーザーをマッピングするのに役立ちます。
   * [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#cloud-migration)：コンテンツ転送ツールは、コンテンツを準備して、既存の環境からクラウドサービス環境に転送するのに役立ちます。
* [!DNL AEM Forms] as a Cloud Service およびローカル [!DNL AEM Forms] 環境の管理者権限を持つアカウント。
* [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) からベストプラクティスアナライザー、コンテンツ転送ツール、[!DNL AEM Forms] 移行ユーティリティをダウンロードしてインストールする

* [ベストプラクティスアナライザー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja#cloud-migration) ツールを実行し、報告された問題を修正します。

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## [!DNL AEM Forms] アセットを移行  {#use-the-migration-utility}

次の手順を実行して、[!DNL AEM Forms] アセットをクラウドサービスと互換性を持たせ、[!DNL AEM] as a Cloud Service 環境に転送します。

1. 既存の [!DNL AEM Forms] 環境の[クローン](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/td-p/363487?profile.language=ja)を作成します。

   コンテンツ転送ツールと移行ユーティリティを実行するには、必ずクローン環境を使用してください。コンテンツ転送ツールと移行ユーティリティで、コンテンツとアセットに変更をいくつか加えます。したがって、実稼働環境上でコンテンツ転送ツールと移行ユーティリティを実行しないでください。

1. 管理者権限を使ってクローン環境にログインします。

1. [ユーザーマッピングツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#cloud-migration)を実行して、ユーザーを対応するアドビの IMS ユーザーアカウントにマッピングします。[!DNL AEM Forms] as a Cloud Service インスタンスにログインするには、アドビの IMS ユーザーアカウントが必要です。

1. クローン環境の[ソフトウェア配布ポータル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#cloud-migration)から、[!DNL AEM Forms]コンテンツ転送ツール[と ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) as a Cloud Service 移行ユーティリティをダウンロードしてインストールします。AEM パッケージマネージャーを使用して、ツールとユーティリティをインストールできます。

1. **[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL コンテンツの移行]**&#x200B;に移動します。

1. **[!UICONTROL 移行用フォームの準備]**&#x200B;カードを開きます。ブラウザーに、以下に示す 5 つのオプションが表示されます。
   * **[!UICONTROL AEM Forms アセットの移行]**
   * **[!UICONTROL アダプティブフォームカスタムコンポーネントの移行]**
   * **[!UICONTROL アダプティブフォームテンプレートの移行]**
   * **[!UICONTROL AEM Forms クラウド設定の移行]**
   * **[!UICONTROL コードエディタースクリプトの移行]**

1. オプションを次々に使用して、[!DNL AEM Forms] アセットに [!DNL AEM] as a Cloud Service との互換性を持たせます。

   1. 「**[!UICONTROL AEM Forms アセットの移行]**」をタップし、次の画面で「**[!UICONTROL 移行を開始]**」をタップします。これにより、[!DNL AEM Forms] 環境のアダプティブフォームとテーマは [!DNL AEM] as a Cloud Service と互換性を持つようになります。

   1. 「**[!UICONTROL アダプティブフォームカスタムコンポーネントの移行]**」をタップし、カスタムコンポーネントの移行ページで「**[!UICONTROL 移行の開始]**」をタップします。これは、アダプティブフォーム用に開発されたカスタムコンポーネントと、[!DNL AEM Forms] 環境上のコンポーネントオーバーレイを、[!DNL AEM] as a Cloud Service と互換性を持たせます。

   1. 「**[!UICONTROL アダプティブフォームテンプレートの移行]**」をタップし、カスタムコンポーネントの移行ページで、「**[!UICONTROL 移行の開始]**」をタップします。/apps または /conf で AEM テンプレートをエディターを使用して、[!DNL AEM] as a Cloud Service と互換性のあるアダプティブフォームテンプレートを作成します。

   1. 「**[!UICONTROL AEM Forms クラウド設定の移行]**」をタップし、設定の移行ページで「**[!UICONTROL 移行の開始]**」をタップします。次のクラウドサービスを更新して新しい場所に移動します。

      * Form Data Model Cloud Service
      * Google reCAPTCHA Cloud Service
      * [!DNL Adobe Sign] Cloud Service
      * Adobe Fonts Cloud Service
   1. 「**[!UICONTROL コードエディタースクリプトの移行]**」をタップし、再利用可能な関数を保存する場所を指定して、「**[!UICONTROL 移行の開始]」をタップします。

   Cloud Service は、ルールエディタースクリプトをサポートしていません。**[!UICONTROL コードエディタースクリプトの移行]**&#x200B;ツールは、環境上のすべてのルールスクリプトを再利用可能な関数に変換し、再利用可能な関数を適切な場所のビジュアルエディターに適用します。これらの再利用可能な関数は、クライアントライブラリの形式で保存され、既存の機能をそのまま維持するのに役立ちます。ツールは、生成された再利用可能な関数を、対応するアダプティブフォームに自動的に適用します。

   [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja#contentmanagement)を使用して、再利用可能な関数（クライアントライブラリ）をパッケージに書き出します。

1. 再利用可能な関数（クライアントライブラリ）パッケージ、[カスタムコード、コンポーネント、設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=ja#cloud-manager)、カスタムロケール固有のライブラリを、[!DNL AEM] as a Cloud Service 環境に[デプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#deploying-content-packages-via-cloud-manager-and-package-manager)します。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#cloud-migration)を実行します。「**[!UICONTROL 移行セットの作成]**」画面でパラメーターを指定するときに、アダプティブフォーム、テーマ、テンプレート、フォームデータモデル、クラウドサービス、カスタムコンポーネント、その他の AEM Forms 固有のアセットのパスを「**[!UICONTROL 含めるパス]**」オプションに指定します。指定した [!DNL AEM Forms] アセットを移行セットに追加します。

## 様々な AEM Forms 固有のアセットのパス

* **アダプティブフォーム**：アダプティブフォームは、`/content/dam/formsanddocuments/` および /content/forms/af にあります。例えば、WKND 登録という名前のアダプティブフォームの場合、`/content/dam/formsanddocuments/wknd-registration`と`/content/forms/af/wknd-registration`のパスを追加します。
* **フォームデータモデル**：すべてのフォームデータモデルは、`/content/dam/formsanddocuments-fdm`にあります。例：`/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

* **クライアントライブラリ**：クライアントライブラリのデフォルトパスは `/etc/clientlibs/fd/theme` です。

* **アダプティブフォームテンプレート**：テンプレートのデフォルトパスは`/conf/<template folder>`です。例えば、基本追加パス`/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`という名前のテンプレートの場合。

* **アダプティブフォームテーマとクライアントライブラリ**：テーマのデフォルトパスは` /content/dam/formsanddocuments-themes/`で、クライアントライブラリのデフォルトパスは`/etc/clientlibs/fd/theme`です。例えば、WKND テーマという名前のテンプレートの場合、パス` /content/dam/formsanddocuments-themes/wkndtheme`とテーマのクライアントライブラリを`/etc/clientlibs/reference-themes/wkndtheme-3-0`に追加します。他のカスタムパスにテーマとクライアントライブラリを配置することもできます。

* **クラウドの設定情報**：クラウドの設定情報は、`/conf/`で確認できます。例えば、フォームデータモデルのクラウドの設定情報は`/conf/global/settings/cloudconfigs/fdm`にあります。

* **ワークフローモデル**：AEM ワークフローモデルは、`/conf/global/settings/workflow/models/`で参照できます。例えば、WKND 登録という名前のワークフローモデルの場合、パス`/conf/global/settings/workflow/models/wknd-registration`を追加します

以下に示すトップレベルのフォルダーパスまたは以下に示す特定のフォルダーパスを追加できます。これにより、特定のアセットとすべてのアセットおよびフォームを一度に移行できます。

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

AEM ワークフローモデルを移行するには、次のパスを指定します。

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
