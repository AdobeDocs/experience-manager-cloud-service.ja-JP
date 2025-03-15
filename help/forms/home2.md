---
title: ' [!DNL AEM Forms]  as a Cloud Service の概要'
description: AEM Forms を検出して、ビジネスに対応するフォームを作成し、ビジネスプロセスのワークフローを作成し、ドキュメントサービスを使用してドキュメントを作成および保護します。
landing-page-description: AEM as a Cloud Service でのフォームの使用方法を理解します。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 2c41fae87821a28af1fd00701780e9fc52b5577d
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 12%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>別のバージョンのドキュメントをお探しですか？</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html">AEM 6.5 Forms ドキュメント</a></li>
    <li><strong>AEM Formsas a Cloud Service</strong> （最新）</li>
  </ul>
</div>

## AEM Forms as a Cloud Serviceとは

AEM Forms as a Cloud Serviceは、デジタルフォームとコミュニケーションを作成、管理、配信するための、Adobeのクラウドネイティブなソリューションです。 これにより、組織はカスタマージャーニー全体を通じて、複雑なトランザクションをシンプルでデジタルなエクスペリエンスに変換できます。 サービスを使用して以下のことが行えます。

* 登録／オンボーディングエクスペリエンスのデジタル化と合理化
* パーソナライズされたコミュニケーションの提供
* バックオフィスワークフローの自動化
* フォームとコミュニケーションエクスペリエンスのデータソースへの統合
* フォームのパフォーマンスの追跡と最適化

このサービスは常に最新、常に利用可能で、常に学習しています。組織はローカルインフラストラクチャがなくても、[!DNL AEM Forms] as a Cloud Service を使用することで、クラウド内のこれらすべての機能を取得できます。また、このサービスは常に最新の機能を備えているので、複雑なアップグレードサイクルから組織を解放します。

Adobe [!DNL Experience Manager Forms as a Cloud Service] は、カスタマージャーニーのあらゆる段階をサポートする、顧客中心のソリューションです。

<div class="card-container">
  <div class="card">
    <div class="card-header">
      <h3>アダプティブフォーム</h3>
    </div>
    <div class="card-body">
      <p>ユーザーの入力とデバイスタイプに適応する、レスポンシブな動的フォームを作成します。</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components"> アダプティブFormsの作成 </a> – 様々な画面サイズやユーザー入力に合わせて自動調整されるフォームを作成します。</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type"> リッチコンポーネントライブラリ </a> – 様々な入力フィールドと UI コンポーネントを使用します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components"> アダプティブFormsのスタイル設定 </a> – 一貫したブランディングとビジュアルデザインをフォームに適用します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components"> 事前定義済みのテーマとテンプレートを使用 </a> – すぐに使用できるコンポーネントを使用して開発を促進します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components"> フォームの検証 </a> - クライアントサイドおよびサーバーサイドの検証ルールを実装します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components"> 送信アクション </a> - ユーザーがフォームを送信したときの動作を設定します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components"> レコードのドキュメント </a> – 送信されたフォームデータの永続的なレコードを作成します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">AEM Sites ページへのFormsの追加 </a> - フォームを Web サイトにシームレスに統合します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page"> サードパーティの Web サイトページへのFormsの追加 </a> - フォームを Web サイトにシームレスに統合します</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>通信 API</h3>
    </div>
    <div class="card-body">
      <p>プログラムによるドキュメントの生成、操作、保護：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation"> パーソナライズされたコミュニケーションの生成 </a> - テンプレートとデータに基づいてカスタマイズされたドキュメントを作成します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">PDF のアセンブリと操作 </a> - PDF ドキュメントの結合、分割、変更</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">PDF/A ドキュメントの作成 </a> - アーカイブ品質のドキュメントの生成</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis"> 署名の適用 </a> – 署名を使用してドキュメントを保護します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">PDF の暗号化と復号化 </a> – 機密ドキュメントコンテンツを保護します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">XDP をPostScriptに変換 </a> - XDP ドキュメントをPostScript形式に変換します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">XDP を PCL に変換 </a> - XDP ドキュメントをプリンターコマンド言語に変換します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">XDP を ZPL に変換 </a> - XDP ドキュメントをゼブラプリント言語に変換します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">PDFをPDF/A 標準に変換 </a> - アーカイブに準拠したPDF ドキュメントを作成します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards"> デジタル署名の追加 </a> – 認証用のドキュメントにデジタル署名を行います</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>ヘッドレスForms</h3>
    </div>
    <div class="card-body">
      <p>任意のチャネルまたはフロントエンドフレームワークをまたいでフォームエクスペリエンスを配信します。</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview"> ヘッドレスFormsの概要 </a> - フォームに対するヘッドレスアプローチについて説明します</li>
        <li>React またはその他のフロントエンドフレームワークを使用したフォームの作成</li>
        <li>モバイルアプリ、web サイトおよびチャットアプリケーションへのフォームの統合</li>
        <li>フォーム機能で既存の UI コンポーネントを活用する</li>
        <li>フロントエンドに柔軟性を持たせながら、バックエンドフォームのロジックを維持する</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>FormsのEdge Delivery Services</h3>
    </div>
    <div class="card-body">
      <p>Edge Delivery Servicesを使用したフォームの作成と配信：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Edge Delivery Formsの概要 </a> - Edge Delivery Servicesでのフォームについて</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">Forms用ユニバーサルエディター </a> - WYSIWYG ユニバーサルエディターを使用したフォームの作成</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial"> ドキュメントベースのオーサリング </a> - Microsoft Word またはGoogle Docsを使用してフォームを作成します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">Edge Delivery Formsのスタイル設定 </a> - フォームにカスタムスタイルを適用します</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>ワークフローの自動化</h3>
    </div>
    <div class="card-body">
      <p>フォームとドキュメントに関するビジネス・プロセスを自動化：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step"> ビジネスプロセスの作成 </a> – 登録プロセスを管理するための承認またはフィードバック、送信後のワークフロー、バックエンドワークフローのフォームをルーティングします。</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">AEM ワークフローでの Adobe Sign の使用 </a> – 署名用のドキュメントを送信します </li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step"> レコードのドキュメントの生成 </a> - オンデマンドまたはフォーム送信時に生成します</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>電子サイン</h3>
    </div>
    <div class="card-body">
      <p>フォームとドキュメントに法的拘束力のある電子署名を追加する：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Adobe Sign 統合 </a> - アダプティブFormsでの電子サインの有効化</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step"> ワークフローへの電子サインの追加 </a> - ビジネスプロセスに署名ステップを含めます</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step"> 署名を含むレコードのドキュメント </a> - フォーム送信の署名済みレコードを生成します</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>分析とインサイト</h3>
    </div>
    <div class="card-body">
      <p>フォームの使用状況とパフォーマンスに関するインサイトを取得します。</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">Adobe Analyticsを有効にする </a> - フォームの使用状況とパフォーマンスを追跡します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics"> 手動の Analytics 統合 </a> – 詳細なトラッキング用に Analytics を設定する</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports"> 分析レポートの表示 </a> - フォームのパフォーマンスとユーザーの行動を分析します</li>
      </ul>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>データ統合</h3>
    </div>
    <div class="card-body">
      <p>既存のデータソースとシステムにフォームを接続する：</p>
      <h4>Adobeのエコシステム</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> - Adobe Sign で電子署名を送信します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a> - フォームとAdobe Marketo Engageの統合</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">AEM ワークフロー </a> - AEM ワークフローとフォーム送信のトリガー付け</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> - Adobe Workfront Fusion にアダプティブフォームを送信します</li>
      </ul>
      <h4>Microsoft統合</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> - Microsoft CRM との統合</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Azure Blob ストレージ </a> - フォームデータをMicrosoft クラウドストレージに保存します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">SharePoint ドキュメントライブラリ </a> - Microsoft SharePoint ドキュメントライブラリへの接続</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">SharePointリスト </a> - Microsoft SharePointに接続リスト</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a> - Microsoft OneDrive に接続します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a> - トリガー Microsoft Power Automate フロー</li>
      </ul>
      <h4>その他のデータソースとサービス</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> - Salesforce CRM との統合</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">RESTful サービス </a> – 任意の REST API エンドポイントに接続します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">RDBMS データベース </a> - リレーショナルデータベースに接続します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email"> メール </a> - フォームデータをメールで送信します。</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Forms ポータル </a> - Forms ポータルに送信してドラフトを保存します</li>
        <li><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email"> メールでPDFを送信 </a> – 送信したフォームのPDF版をメールで送信します</li>
        <li><a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model"> フォームデータモデルを使用して送信 </a> - フォームデータモデルを使用してデータを送信します。</li>
      </ul>
    </div>
  </div>
</div>

## AEM Forms as a Cloud Serviceの概要

<div class="card-container">
  <div class="card">
    <div class="card-header">
      <h3>ビジネスユーザー向け</h3>
    </div>
    <div class="card-body">
      <ol>
        <li><strong> 基本を理解する </strong>: <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components"> アダプティブForms</a> と、それらがビジネスプロセスのデジタル化にどのように役立つかについて説明します。</li>
        <li><strong> テンプレートを探索 </strong>:<a href="https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components"> 事前定義済みのテンプレートとテーマ </a> を参照して、フォームプロジェクトを素早く開始します。</li>
        <li><strong> フォームオーサリングについて </strong>:<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring"> フォームオーサリングガイド </a> に従って、最初のフォームを作成します。</li>
      </ol>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>開発者向け</h3>
    </div>
    <div class="card-body">
      <ol>
        <li><strong> 環境の設定 </strong>:AEM Formsの <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">ローカル開発環境を設定 </a> します。</li>
        <li><strong> アーキテクチャについて </strong>:<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">AEM Forms as a Cloud Serviceのアーキテクチャ </a></li>
        <li><strong>API を探索 </strong>:Formsの拡張および統合に使用でき <a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/">API の </a> と SDK について理解します。</li>
      </ol>
    </div>
  </div>

<div class="card">
    <div class="card-header">
      <h3>管理者向け</h3>
    </div>
    <div class="card-body">
      <ol>
        <li><strong>Cloud Serviceへのオンボード </strong>:<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service"> オンボーディングガイド </a> に従って、AEM Forms as a Cloud Serviceを設定します。</li>
        <li><strong> サービスの設定 </strong>:Adobe Analyticsなどの他のAdobe サービスとの <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation"> 統合 </a> を設定します。</li>
        <li><strong>AEM 6.5 から移行 </strong>:AEM 6.5 を使用している場合は、<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=ja"> 移行ガイド </a> に従って、Cloud Serviceに移行してください。</li>
      </ol>
    </div>
  </div>
</div>

## 早期導入者の機能

<div class="card">
  <div class="card-header">
    <h3>AEM Forms アーリーアクセスプログラム</h3>
  </div>
  <div class="card-body">
    <p><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms早期アクセスプログラム </a> では、次のような最先端の機能を、一般に利用する前に排他的に利用できます。</p>
    <ul>
      <li><strong>AEM Forms AI アシスタント（Gen AI） </strong> - AI を利用した提案でフォームをより迅速に作成します</li>
      <li><strong>AEM Forms Workfront Fusion コネクタ </strong> - フォームの送信によってトリガーされるワークフローの自動化</li>
      <li><strong> 対話型Forms</strong> – 任意のAEM Sites ページでチャットスタイルのフォームエクスペリエンスを作成します</li>
      <li><strong>Edge DeliveryのWYSIWYG オーサリング </strong> - Edge Delivery Servicesのユニバーサルエディターを使用してフォームを作成します</li>
      <li><strong>AEM FormsからMarketo コネクタへ </strong> - フォーム送信をMarketo Engageと統合します</li>
    </ul>
    <p>早期アクセスの革新的な機能と詳細なドキュメントの一覧については、<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms早期アクセス プログラム ページ </a> を参照してください。</p>
  </div>
</div>

<div class="cta-card">
  <h3>始める準備はよろしいでしょうか。</h3>
  <p><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">AEM Forms as a Cloud Serviceへのオンボード </a> 今すぐ、組織のデジタルフォームエクスペリエンスを変革してください。</p>
</div>

<style>
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-bottom: 30px;
}

.card {
  flex: 1 1 calc(50% - 20px);
  min-width: 300px;
  border: 1px solid #e1e1e1;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
}

.card-header {
  background-color: #f5f5f5;
  padding: 15px 20px;
  border-bottom: 1px solid #e1e1e1;
}

.card-header h3 {
  margin: 0;
  color: #2c2c2c;
  font-size: 1.25rem;
}

.card-body {
  padding: 20px;
  background-color: #ffffff;
}

.card-body ul, .card-body ol {
  margin-top: 10px;
  padding-left: 25px;
}

.card-body li {
  margin-bottom: 8px;
}

.cta-card {
  background-color: #f0f7ff;
  border-left: 4px solid #1473e6;
  padding: 20px;
  margin: 30px 0;
  border-radius: 4px;
}

.cta-card h3 {
  margin-top: 0;
  color: #1473e6;
}

.cta-card a {
  font-weight: bold;
  color: #1473e6;
}

@media (max-width: 768px) {
  .card {
    flex: 1 1 100%;
  }
}
</style>
