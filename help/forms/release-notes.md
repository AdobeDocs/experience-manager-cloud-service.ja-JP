---
title: '"[!DNL AEM Forms] as a Cloud Service リリースノート"'
description: '"[!DNL AEM Forms] as a Cloud Service リリースノート"'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 100%

---


# [!DNL Experience Manager Forms] as a Cloud Service リリースノート {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service は継続的に改善を受け取ります。最新の開発状況を確認するには、このページに定期的にアクセスしてください。このページでは、次の情報が確認できます。

- 新機能
- 機能強化
- プレリリース機能
- ベータ版機能
- バグの修正
- 非推奨の機能
- 特別な手順
- 将来の変更プラン

>[!NOTE]
>
>他のすべての AEM as a Cloud Service リリースコンポーネントのリリースノートについては、[最新のリリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)を参照してください。

## 2021.10.0 {#sep-2021-10-0}

### [!DNL Forms] の新機能 {#what-is-new-forms-oct-2021}

- **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics を使用して、ログイン済みとログインしていない（匿名）状態の両方の動作を取得および追跡して、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms-oct-2021}

- **AEM ワークフローデータを外部化して処理を保護**：顧客が管理するリポジトリーに、機密の個人データ（SPD）要素を含むプロセス内の AEM ワークフローデータ（AEM ワークフロー変数データ）を保存して、安全に処理できます。データ要素とワークフロー変数は、AEM リポジトリに格納されず、ワークフローの処理中に顧客が管理するリポジトリからオンデマンドで取得されます。

### [!DNL Forms] のベータ版機能 {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   - テンプレートファイル（PDF および XDP）に XML データを格納することで、最終形式のドキュメントを生成します。
   - 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

## 2021.9.0 {#sep-2021-09-0}

### [!DNL Forms] の新機能 {#what-is-new-forms-sep-2021}

- **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](working-with-adobe-sign.md#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

- **アダプティブフォーム用の Analytics**：[アダプティブフォーム用の Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

- **AEM Forms と Microsoft Dynamics および Salesforce との簡単な接続**：Microsoft Dynamics と Salesforce のデータソース設定およびデータモデルが標準で提供されるので、[開発者が Microsoft Dynamics と Salesforce をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できる](configure-msdynamics-salesforce.md)ようになりました。

- **DocuSign を使用したアダプティブフォームへの電子サイン**：[DocuSign を使用してアダプティブフォームに電子サインすることができます](integrate-docusign-adaptive-forms.md)。このサービスでは、アダプティブフォームで DocuSign を使用するためのカスタム送信アクションを提供します。

### [!DNL Forms] のベータ版機能 {#sep-what-is-new-forms-prerelease}

- **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリー内の処理中のデータを外部化することができます。例えば、個人の機密情報（SPD）を含んだ処理中の AEM ワークフローデータ（AEM ワークフロー変数データ）を顧客側で管理されるリポジトリーに格納できます。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   - テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   - 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   - XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

### 制限事項 {#limitations}

- Adobe Analytics では、認証済みユーザーの場合にのみフォーム指標を追跡できます。

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### [!DNL Forms] の新機能 {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- Forms as a Cloud Service の AEM アーキタイププロジェクトに、[Microsoft Dynamics および Salesforce のフォームデータモデル](setup-local-development-environment.md)が含まれるようになりました。

- **AcroForm ベースのレコードのドキュメント**：AEM Forms as a Cloud Service では、XFA ベースのフォームテンプレート以外に、[Adobe Acrobat フォーム PDF（AcroForm PDF）](generate-document-of-record-for-non-xfa-based-adaptive-forms.md)をレコードのドキュメントのテンプレートとして使用できます。

- **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続できるようになりました](configure-azure-storage.md)。アダプティブフォームデータを取得し、BLOB として Microsoft Azure Storage に保存することができます。

### [!DNL Forms] のベータ版機能 {#aug-what-is-new-forms-prerelease}

- **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリー内の処理中のデータを外部化することができます。例えば、次のことができます。

   - Forms ポータルの保存および再開機能を有効にし、顧客側で管理されるデータリポジトリにアダプティブフォームのドラフトを格納する
   - 個人の機密情報（SPD）を含んだ処理中の AEM ワークフローデータ（AEM ワークフロー変数データ）を、顧客側で管理されるリポジトリに格納する

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   - テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   - 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   - XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms-aug-2021}

- **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](working-with-adobe-sign.md#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

- **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーに関するインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

- **AEM Forms と Microsoft Dynamics および Salesforce との簡単な接続**：Microsoft Dynamics と Salesforce のデータソース設定およびデータモデルが標準で提供されるので、[開発者が Microsoft Dynamics と Salesforce をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できる](configure-msdynamics-salesforce.md)ようになりました。

## 2021.7.0 {#july-2021-07-0}

### [!DNL Forms] の新機能 {#july-what-is-new-forms}

- 自動フォーム変換サービスを使用して、[フランス語、ドイツ語、スペイン語の PDF フォームをアダプティブフォームに変換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=ja#language-specific-meta-model)できるようになりました。
- テンプレートエディターに、アダプティブフォームのコンポーネントに関連するエラーを表示するためのパネルを別途追加しました。これにより、すべてのアダプティブフォームのエラーが 1 か所に集約されるので、解決に要する時間を短縮できます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#july-prerelease-features-forms}

- **Acroform べースのレコードのドキュメント**：XFA ベースのフォームテンプレート以外にも、[Adobe Acrobat Form PDF（Acroform PDF）](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=ja) を、レコードドキュメントのテンプレートとして使用することもできます。

- **Microsoft Azure データストアコネクタ**：[フォームデータモデルを Microsoft Azure Storage に接続できるようになりました](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=ja)。アダプティブフォームデータを取得し、BLOB として Microsoft Azure Storage に保存することができます。

- **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

### [!DNL Forms] のベータ版機能 {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](aem-forms-cloud-service-communications.md) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   - テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   - 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   - XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

## 2021.6.0 {#july-2021-06-0}

### [!DNL Forms] の新機能 {#june-what-is-new-forms}

- AEM インボックスのカスタム列をフィルタリングする機能を追加しました。
- アダプティブフォームエディターのテーマエディターとスタイルレイヤーを使用して Captcha コンポーネントのスタイルを設定する機能を追加しました。
- ソース PDF フォーム内の論理セクションを自動的に検出し、対応するアダプティブフォームパネルに変換する際の速度と精度が向上しました。
- PDF または XDP ファイルをフォルダー間で移動する移動アクションが追加されました。

### [!DNL Forms] のベータ版機能 {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**：通信 API を使用すると、XDP テンプレートと XML データを組み合わせて様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   - テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
   - 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   - XFA フォーム PDF および Adobe Acrobat フォーム（AcroForms）から印刷用 PDF を生成する。

- **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

### [!DNL Forms] で修正されたバグ  {#june-forms-bugs-fixed}

- フォームデータモデル（FDM）を使用してデータをバックエンドサービスに送信する前にフィールドの検証が完了すると、検証は成功しますが、フォームデータモデルサービスで事後検証が呼び出されません。
- 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 では、この問題を修正しています。

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#may-what-is-new-forms}

- **コンテキストヘルプ**：アダプティブフォームエディター、テンプレートエディター、テーマエディターのコンテキストヘルプが追加され、作成者がエディターの様々な機能をより深く理解できるようになりました。
- **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

### [!DNL Forms] の今後のベータ版機能 {#may-what-is-new-forms-prerelease}

Output as a Cloud service：出力サービスを使用すると、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および非同期の一括モードでドキュメントを生成できます。出力サービスにより、以下のような機能を備えたアプリケーションを作成することができます。

- テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
- 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
- XFA フォームの PDF ファイルから印刷用 PDF を生成する。

ベータ版プログラムに新規登録する場合は、 formscsbeta@adobe.com までお問い合わせください。

### [!DNL Forms] で修正されたバグ  {#may-forms-bugs-fixed}

- AEM Forms ワークフローの「タスクの割り当て」手順で、アクションボタンのデフォルトのアイコンを Coral アイコンに置き換えると、ワークフローは動作を停止し、例外がログに記録されます。デフォルトのアイコンが使用されている場合、ワークフローは期待どおりに実行されます。
- レイアウトレイヤーで、列数を変更し、編集レイヤーを開いてパネル内の一部のコンポーネントをドラッグすると、青い四角いボックスがアダプティブフォームエディターのコンテンツ領域に表示され、エディターが応答しなくなります。
- アダプティブアセットまたは外部アセットの URL の指定に関連するルールエディターオプションのエラーメッセージが長すぎて、使いやすくありません。

## 2021.4.0 {#april-2021-04-0}

### [!DNL Forms] の新機能 {#april-what-is-new-forms}

- **Adobe Sign 対応アダプティブフォームでの Government ID 認証方法の使用**

   高度な機械学習アルゴリズムを活用した Adobe Sign の Government ID プロセスにより、世界中の企業がその受信者の ID を高品質に認証できるように支援します。Adobe Sign 対応のアダプティブフォームで、Government ID 認証方法を使用できるようになりました。

   Government ID は、政府発行の ID 文書[（運転免許証、国民 ID、パスポート）の画像をアップロード](https://helpx.adobe.com/jp/sign/using/adobesign-authentication-government-id.html)するように受信者に指示し、その文書を評価して信頼性を確認するプレミアム ID 認証方法です。

- **非同期のアダプティブフォーム送信に対するフォーム内署名機能の使用をサポート**

   非同期のアダプティブフォーム送信に対して、フォーム内署名機能を使用できるようになりました。アダプティブフォームを [!DNL Experience Manager Sites] ページに埋め込み、アダプティブフォーム送信時にフォーム内署名機能を使用することもできます。

- **変数を使用して添付ファイルを指定し、アダプティブフォームにタスクの割り当て手順を事前入力する際のサポート**

   アダプティブフォームをタスクの割り当て手順用に事前入力する際に、ドキュメントタイプ変数を使用してアダプティブフォームの入力添付ファイルを選択できるようになりました。

- **リテラルオプションを使用して JSON タイプの変数の値を設定する機能をサポート**

   リテラルオプションを使用して、AEM ワークフローの変数設定手順で JSON タイプの変数の値を設定できます。リテラルオプションを使用すると、文字列の形式で JSON を指定できます。

- **ローカル開発環境を使用したレコードのドキュメント（DoR）の作成**

   Cloud Service インスタンスおよび AEM Forms as a Cloud Service SDK（ローカル開発環境）のレコードのドキュメントテンプレートとして XDP を使用できます。以前は、Cloud Service インスタンスのみサポートされていました。

### [!DNL Forms] のバグ修正  {#april-bug-fixes-forms}

- レコードのドキュメントを生成しないように設定されたアダプティブフォームが、レコードのドキュメントを生成するように設定された AEM ワークフローに送信された場合、エラーメッセージは表示されず、タスクの送信に失敗します。
