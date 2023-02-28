---
title: ' [!DNL AEM Forms] as a Cloud Service の概要'
description: AEM Forms を理解し、ビジネスに適したドキュメントやコンテンツの作成にどのように役立つのかを学びます。サービスとしてのプラットフォーム（PaaS）、エンタープライズクラスのデジタルフォームとビジネスプロセスを管理する方法、現在のデータソースに Forms を接続する方法について学びます。
landing-page-description: AEM as a Cloud Service でのフォームの使用方法を理解します。
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 6861f83b292dfb8a8e62e685830289e3a2eded2d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 42%

---

# はじめに {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] は、複雑なデジタルフォームを作成、管理、公開、更新しながら、送信データをバックエンドプロセス、ビジネスルール、外部データストアに保存する、クラウドネイティブのサービスとしてのプラットフォーム（PaaS）ソリューションを提供します。

## 登録とオンボーディングエクスペリエンスをデジタル化し、合理化

このサービスを使用して、インタラクティブで魅力的なデジタルフォームを作成し、展開できます。例えば、顧客登録ジャーニーのデジタル化を検討している組織について考えてみます。既存の顧客データを持つ複数のデータソースがあります。フォームに事前入力したり、フォームの電子サインを追加したり、入力済みのフォームを PDF ファイルとしてアーカイブしたりすることを検討しています。さらに、組織には複数の印刷フォーム（PDF フォーム）があり、すべての印刷フォームをデジタルフォームに変換することも検討しています。

組織は、[!DNL AEM Forms] as a Cloud Service を使用して、デジタルフォームを作成したり、フォームを既存のデータソースに接続したり、フォームを [!DNL Adobe Sign] と統合して電子サインをフォームに追加したり、送信されたフォームを PDF ファイルとしてアーカイブするためにレコードのドキュメント（DoR）を生成したりできます。また、このサービスを使用して、既存の PDF フォームをデジタルフォームに変換することもできます。

![データ収集 — レスポンシブフォームデザイン](/help/forms/assets/data-collection.jpeg)
レスポンシブフォームデザイン

大企業では、一度フォームを作成し、その後はコンテンツ管理システムにコピーして再利用されることも多くあります。フォームの大規模なデータベースを最新状態に維持し、検索可能な状態に保つことは非常に頭の痛い課題となることもあります。AEM はカスタマイズ可能な「フォームポータル」を提供することにより、Web チャネルおよびモバイルチャネルの双方から必要なフォームを見つけ、アクセスできる状態に保ちます。

## パーソナライズされた通信

効率的なデジタルセルフサービス体験を実現する上で重要な要素は、パーソナライズされた情報をタイムリーにやり取りすること、そしてどのようなデバイスからでも場所を問わずにアクセスできることです。パーソナライズされたタイムリーな通信により、ユーザーのコンバージョン率と満足度の両方を向上させることができます。

AEM Formsを使用すると、ビジネスユーザーは、ドキュメントテンプレートをカスタマイズし、バックエンドプロセスからテンプレートに情報を組み込むことで、魅力的なパーソナライズされたユーザーエクスペリエンスを作成できます。 一連の状態 API は、問い合わせに基づいて、または一定の間隔で一括して通信を生成するタイミングを決定するビジネスセットルールを支援します。

領収書、ウェルカムキット、明細書など、パーソナライズされたドキュメントを簡単に生成できます。 組織では、パーソナライズされた Web ポータルへトラフィックを引き込み、別のサービスへの登録や購入を促進することができます。


![パーソナライズされたコミュニケーション — レスポンシブデザイン](/help/forms/assets/personalized-communication.jpeg)
パーソナライズされた請求書

このサービスは常に最新で、常に利用可能で、常に学習可能です。組織では [!DNL AEM Forms] as a Cloud Serviceのインフラストラクチャを必要とせずに、クラウド内のこれらの機能をすべて入手できます。 また、このサービスは常に最新の機能を備えているので、複雑なアップグレードサイクルから組織を解放します。

## 主な機能 {#key-features}

|  |  |
|---|---|
| アダプティブフォーム | Web サイト、アプリ、その他のデジタルチャネルや印刷チャネル向けの、インタラクティブで動的で、レスポンシブで、モバイルに適した、データ駆動型のフォームを作成および管理します。 登録エクスペリエンスを開始、理解、実装するには、以下を確認します。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> アダプティブフォームの作成 </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">アダプティブフォームのスタイル設定</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> データをデータストアまたはワークフローに送信する</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> 長期保存用のフォームのレコードを作成する</a></li></ul> |
| 通信 API | RESTful API を使用して、パーソナライズされたデータ駆動型通信の作成、管理、配信をオンデマンドで、または月次の明細書やアカウント通知などのスケジュールに沿って自動化します。 以下を確認して、作業を開始、理解および作成します。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> パーソナライズされた通信を生成 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> アセンブリドキュメントのアセンブリまたはPDF解除 </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">PDF/A 準拠のドキュメントを作成 </a></li></ul> |
| 自動フォーム変換サービス | 従来のPDFベースのフォームを、オンラインで容易に管理および配布できるアダプティブFormsに変換する。 以下を確認して開始します。 <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=ja">automated forms conversionサービスの設定</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=ja">PDF フォームをアダプティブフォームに変換する</a></li></ul> |
| Forms Workflow | フォームとドキュメントサービスに関するビジネスプロセスを自動化します。 ビジネスプロセスの様々な段階を進めるにつれ、フォームとドキュメントの割り当て、ルーティング、確認、承認を行います。 以下を確認して開始します。  <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">レビュー用のフォームまたはドキュメントの送信</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">承認却下ワークフローの作成</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">レコードのドキュメントを追加 </a> または <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step"> 電子サイン </a> ビジネスワークフローの手順</a></li></ul> |
| 電子署名 | Adobe Signや DocuSign と統合して、電子署名用にFormsとドキュメントを簡単にユーザーに送信できます。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">Adobe Signでのアダプティブフォームの電子署名 </a></li><li></a> <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-docusign-adaptive-forms.html">DocuSign を使用したアダプティブフォームの電子署名 </a></li></ul> |
| Forms Analytics | Adobe Analyticsを使用して、ユーザーの行動と環境設定に関する貴重なインサイトを得ます。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html?lang=en">アダプティブフォームとAdobe Analyticsの接続</a></li></ul> |
| データソース | フォームとドキュメントを外部データソースと簡単に接続して、データを取得して送信します。 <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=en">RDBMS または Rest エンドポイントへの接続</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en">Microsoft Dynamics 365 または Salesforce クラウドサービスに接続</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=en">Microsoft Azure Blob Storage に接続</a></li></ul> |


