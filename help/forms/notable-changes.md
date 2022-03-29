---
title: AEM 6.5 Forms と AEM Cloud Services の間での変更点
description: 'Experience Manager Forms のユーザーで、Adobe Experience Manager Forms as aCloud Service にアップグレードする予定ですか？Cloud Service にアップグレードまたは移行する前に、最も重要な変更点を説明します。  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 100%

---

# 既存の Adobe Experience Manager Forms ユーザーの主な変更点  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service は、Adobe Experience Manager Forms オンプレミスおよび [!DNL Adobe-Managed Service] 環境と比較して、既存の機能にいくつかの顕著な変更を加えました。主な違いを以下に示します。

* このサービスは、ローカルおよびクラウドネイティブの開発環境を提供します。[ローカル開発環境](setup-local-development-environment.md)を使用して、カスタムコード、コンポーネント、テンプレート、テーマ、アダプティブフォーム、その他のアセットを開発およびテストしてから、これらのアセットをクラウド環境にデプロイできます。開発プロセスの迅速化に役立ちます。
* [!DNL AEM] as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。
* クラウドネイティブの環境には、web コンソール（Configuration Manager）がありません。[[!DNL AEM Forms] as a Cloud Service SDK を使用して設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)するための CI／CD パイプラインを生成できます。

* ローカライズされたアダプティブフォームの URL 規則で、URL でのロケールの指定がサポートされるようになりました。新しい URL 規則により、ローカライズされたフォームを Dispatcher または CDN にキャッシュできます。Cloud Service 環境では、`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` の代わりに `http://host:port/content/forms/af/<afName>.<locale>.html` の URL 形式を使用して、アダプティブフォームのローカライズ版をリクエストします。アドビでは、Dispatcher または CDN キャッシュを使用することをお勧めします。これにより、事前入力されたフォームのレンダリング速度を向上できます。
* 事前入力サービスは、データをクライアント上のアダプティブフォームに結合します。これにより、アダプティブフォームの事前入力に要する時間を短縮できます。いつでも、Adobe Experience Manager Forms サーバーで結合アクションを実行するように設定できます。
* 電子メールは、デフォルトでは HTTP プロトコルおよび HTTPs プロトコルのみをサポートします。[サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)、電子メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。
* Adobe Experience Manager Forms a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEM は可変コンテンツと不変コンテンツの分割を考慮してコンテンツとコードを個別のサブパッケージに分離する必要があります。[Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=ja) ツールを使用して、Adobe Experience Manager as a Cloud Service 向けに定義されているプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再構築します。

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* パスワード、プライベート API キー、その他の値など、シークレットの OSGi 設定値に対する環境固有の設定の使用。セキュリティ上の理由から、これらは Git に保存できません。[シークレットの環境固有の設定を使用して、ステージングや実稼働などのあらゆる Adobe Experience Manager as a Cloud Service 環境にシークレットの値を保存します](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#when-to-use-secret-environment-specific-configuration-values)。

Adobe Experience Manager as a Cloud Service の変更点の包括的なリストについては、[新機能と相違点](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja)を参照してください。

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## 主な機能強化 {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

以下の機能および機能強化は、[!DNL AEM Forms] as a Cloud Service でのみ使用できます。

**強化されたビジュアルルールエディター**
このサービスは、強化された[ビジュアルルールエディター](rule-editor.md#visual-rule-editor)を提供します。このサービスでは、有効なルールを記述するのに役立つ以下の機能をビジュアルルールエディターに追加しました。

* [新しい送信イベント](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor)：`Navigation`、`Step Completion`、`Successful Submission` および `Error`

* [新しいデータタイプ `scope`](rule-editor.md#custom-functions)。カスタム関数で `scope` データタイプを使用して、フォームのスコープ全体を渡すことができます。

* [@this を使用して、カスタム関数で JSDoc を指定する機能](rule-editor.md#custom-functions)。アクティブコンポーネントで @this を使用してカスタム関数を呼び出すことができます。

* プロパティベースのルールの条件を追加する機能。

**コアコンポーネント**
[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)は、AEM 用の標準化された Web コンテンツ管理（WCM）コンポーネントのセットで、開発時間を短縮し、メンテナンスコストを削減します。[!DNL AEM Forms] as a Cloud Service は、**[!UICONTROL AEM Forms コンテナ]**&#x200B;コアコンポーネントをサポートします。このコンポーネントを使用して、アダプティブフォームを AEM Sites ページに埋め込むことができます。

**Forms as a Cloud Service の AEM アーキタイプ**
[AEM アーキタイプ](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27)は、[!DNL AEM Forms] as a Cloud Service の開発を開始するのに役立ちます。アーキタイプバージョン 27 以降を使用して、[!DNL AEM Forms] as a Cloud Service 環境と互換性のあるプロジェクトテンプレートを作成できます。アーキタイプには、すぐに使い始めるのに役立つサンプルのテーマとテンプレートも含まれています。

**フォームと Sign の間の安全で改善された情報フロー**
Cloud Service での[アダプティブフォームと Adobe Sign の統合](working-with-adobe-sign.md)により、データの送信と署名アクティビティが同時に行われます。署名ステータスに依存せずにフォームを送信し、より高速な送信を実現します。その上、このサービスは Cloud Service インスタンスにデータを保存しないので、署名プロセスが非常に安全になります。

**ベストプラクティスアナライザーと移行ツール** 
ベストプラクティスアナライザーは、現在の AEM の実装を評価します。[Forms as a Cloud Service に移行する](migrate-to-forms-as-a-cloud-service.md)前に、ツールを実行します。既存の Adobe Experience Manager（AEM）デプロイメントから AEM as a Cloud Service に移行する準備ができているかどうかを評価します。

また、このサービスは、[改善された移行エクスペリエンス](migrate-to-forms-as-a-cloud-service.md)を提供し、[!DNL AEM 6.4 Forms] および [!DNL AEM 6.5 Forms] から [!DNL AEM Forms] as a Cloud Service に簡単に移行できるようにします。

**より高速なフォームレンディションとより高速なサーバーサイド検証**
このサービスは、CDN および Dispatcher のキャッシュを使用して、アダプティブフォームのより高速なレンディションとサーバーサイドの検証を実現します。

**CAPTCHA の改善**
アダプティブフォーム送信時またはビジネスロジック時に、[CAPTCHA を検証](captcha-adaptive-forms.md)できるようになりました。また、条件を追加して、ユーザーアクションで CAPTCHA を検証し、ルールに基づいてアダプティブフォームで CAPTCHA コンポーネントを表示または非表示にすることもできます。

CAPTCHA コンポーネントは、Google reCAPTCHA とあらかじめ統合されています。必要に応じて、コンポーネントに対してさらに CAPTCHA サービスを設定することもできます。

**レコードのドキュメント用の複数のマスターページ**
レコードのドキュメントの各ページに異なるマスターページを使用し、ページ付けオプションでレコードのオプション上のアダプティブフォームパネルの配置を制御できるようになりました。

**ヘッドレステーブルに列を追加**
ヘッダーのないテーブルに列を追加したり、削除したりできます。列の追加と削除に役立つように、非表示のヘッダーがこのようなテーブルに追加されます。これらのヘッダーは、オーサリング中には表示されますが、公開されたフォームでは非表示のままになります。ヘッダーのないテーブルは、自動フォーム変換サービスを使用して作成されたアダプティブフォームで多く見られます。

**送信アクションの向上**
[電子メールを送信](configuring-submit-actions.md#send-email#send-email)アクションを使用して、レコードのドキュメント（DoR）PDF を添付ファイルとして送信できます。

**ワークフローのグループ電子メール**
タスクを割り当てステップから、1 人のユーザーまたは 1 組のグループに[通知電子メールを送信](aem-forms-workflow-step-reference.md#assign-task-step)することを選択できます。

**強化されたフォームデータモデルの呼び出しステップ**
フォームデータモデルの呼び出しステップで、入力サービス引数の「ペイロードを基準とする」オプションのフォルダーのパスを指定できるようになりました。指定したフォルダーに存在するファイルを、正確なファイル名を指定せずに、サービス引数にマップするのに役立ちます。

**翻訳ファイルの読みやすさの向上**
Forms as a Cloud Service では、アダプティブフォームのフィールドとパネル、および対応する翻訳ファイル（.XLIFF ファイル）のメッセージキーの読み取り順序は、同じ構造になっています。これは、手動の翻訳速度の向上に役立ちます。

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
