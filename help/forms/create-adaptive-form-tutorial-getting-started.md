---
title: Adobe Adaptive Formsの導入方法。
description: モバイルレスポンシブアダプティブFormsの作成方法については、このチュートリアルを参照してください。 これらのフォームはデバイス間でシームレスに適応し、スムーズなエクスペリエンスを実現します。
keywords: アダプティブフォーム、モバイルフォーム、レスポンシブフォーム、HTML5 フォーム
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: 77f7d21eed1322de768ee07e3518638f60e3ae40
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 14%

---

# アダプティブフォームの作成（コアコンポーネント） – チュートリアル

今日のオーディエンスは、あらゆるやり取りにおいて、モバイルフレンドリーな体験が提供されることを期待しています。フォームも例外ではありません。 アダプティブフォームは、モバイルフレンドリーであるだけでなく、ユーザーエンゲージメントを向上させ、フォームを完了するのにかかる時間を短縮するのに役立ちます。

このチュートリアルでは、アダプティブフォームを作成する手順を説明します。 ユースケースと複数のガイドに分かれており、それぞれアダプティブフォームに新しい機能を追加する方法を説明します。

チュートリアルの終わりまでに、次のことが可能になります。

* アダプティブフォームとそのデータモデルの作成
* アダプティブフォームのスタイル設定
* アダプティブフォームのルールエディターを使用したビジネスルールの作成
* アダプティブフォームフィールドの事前入力
* フォームに電子サインを追加する
* Google reCAPTCHAを使用してボットからフォームを保護する
* アダプティブフォームを様々な言語にローカライズする
* 構造化データを生成するようにフォームを設定します
* REST エンドポイントにデータを送信するフォームの設定
* アダプティブフォームの公開


## コアコンポーネントにもとづくフォームを作成する理由？

AEM Formsには、フォームのエクスペリエンスを作成するための基盤コンポーネントとコアコンポーネントが用意されています。 コアコンポーネントは、新しいフォームエクスペリエンスを作成するための最新かつ推奨されるアプローチです。 コアコンポーネントを導入する理由？ これらのコンポーネントは、軽量でオープンソース（githubで利用可能）、優れたGoogle Lighthouseとweb Vitalsのスコア、アクセシビリティに準拠し、AEM Sitesのすべての使い慣れた機能（バージョン管理やローカライズなど）をもたらします。 さらに、これらのコンポーネントはスタイル設定が簡単で、組織のブランドガイドラインに従って外観を簡単にカスタマイズできます。 サードパーティ製の依存関係がないため、JavaScriptとCSSの知識を持つ開発者であれば、これらのコンポーネントを簡単にカスタマイズできます。

![&#x200B; アダプティブ Formsをベースにしたコアコンポーネントを作成する理由 これらのコンポーネントは、軽量で、スタイルが簡単で、高いLighthouse スコアを提供し、アクセシビリティ標準をサポートし、簡単にカスタマイズ可能で、オープンソースであり、githubで利用でき、サードパーティライブラリに依存せず、AEM開発者とAEM オーサーの学習曲線はほとんどありません。さらに、AEM Forms コアコンポーネントには、AEM WCM コアコンポーネントのすべての機能が含まれています。](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## ユースケース：Adaptive Formsによる効率的な住宅ローンの事前選定

このチュートリアルでは、大規模な銀行向けのアダプティブフォームを作成します。 ユースケースは次のとおりです。

潜在的な住宅バイヤーは、銀行のweb サイトや支店にアクセスして、住宅ローンの選択肢を調べます。 従来の申し込み手続きでは、多くの場合、事前の文書化が必要となり、時間と手間がかかります。 そのため、一部のバイヤーは、このプロセスを開始することができず、銀行のリードジェネレーションと、自信を持って夢のマイホームを探すバイヤーの能力の両方が妨げられています。

あなたは、インタラクティブな住宅ローンの事前資格フォームを開発する必要があります。 このフォームでは、基本的な情報を収集し、借り手の情報にもとづいて事前に選定を行い、ローンの推定金額、潜在的な頭金ニーズ、さまざまなローンのタイプにもとづく金利を提示します。 事前に承認されたユーザーは、事前承認フォームから直接、ローンの申し込みを行うことができます。

フォームはアダプティブフォームを使用して作成されます。 これにより、正確な住宅ローンの事前選定に必要な財務データを収集しながら、パーソナライズされた体験を実現できます。

チュートリアルが完了すると、フォームは次のフォームのように表示されます。

![ここで作業フォームを追加](/help/forms/assets/cc-tutorial-final-form.png)

## 開発環境のセットアップ

アダプティブフォームは、Cloud Service環境にデプロイする前に、ローカルマシンで直接作成してテストできます。 Adobeでは、AEM SDKを使用してローカル開発を強化し、以下を実現できます

* フォームをローカルで作成、カスタマイズ、テストできます。
* フォームのテーマをデザインし、ローカルで設定を構築し，
* 完成したアセットを容易にクラウドにデプロイできます。

AEM SDKとのローカル開発により、時間を節約し、開発プロセスを簡素化できます


**開始する準備ができましたか？**

1. [AEM プロジェクト用の開発ツールを設定](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects): [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#local-development-environment-set-up)、[Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#install-git)、[Node.js （npm） &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#node-js)、[Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#install-maven)の最新リリースをダウンロードしてインストールします。 プレーンテキストエディターもインストールします。このチュートリアルの例はVisual Studio Codeに基づいています。

1. [AEM SDKをインストールする](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development)：最新バージョンのAEM SDKをダウンロードしてインストールします。 これにより、AEMの開発に必要なツールが提供されます。 AEM SDKのバージョンを確認します。

   ![&#x200B; ソフトウェア配布](/help/forms/assets/software-distribution.png)

   ![AEM SDKのインストール &#x200B;](/help/forms/assets/start-aem-sdk.png)

1. [AEM Forms アドオンを追加](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): [&#x200B; ソフトウェア配布](https://experience.adobe.com/#/downloads) ポータルから、お使いのAEM SDKのバージョンに一致するAEM Forms アドオンをダウンロードしてインストールします。
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++AEM Forms アドオンをインストールします。

   AEM Forms アドオンをインストールするには：

   1. AEM SDKを停止します。
   1. AEM Forms アドオン （.far） ファイルを`AEM SDK/crx-quickstart/install` フォルダーに追加します。
   1. AEM SDKを再起動します。

   +++

1. [&#x200B; ユーザー権限の設定](/help/forms/setup-local-development-environment.md#configure-users-and-permissions)：開発、オーサリング、その他の権限を持つユーザーを作成し、これらのユーザーを事前定義されたフォームグループに追加します。


1. [&#x200B; アダプティブ Forms テンプレートを追加](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype):AEM アーキタイプ 48以降を使用して、新しいAEM プロジェクトを作成し、それをAEM SDKにデプロイします。 このプロジェクトは、アダプティブ Forms テンプレートをAEM SDKに追加します。

   ![&#x200B; アダプティブフォームテンプレート &#x200B;](/help/forms/assets/adaptive-forms-templates.png)

   +++アダプティブForms テンプレートをAEM SDKに追加します。

   1. 次のコマンドを実行して、AEM プロジェクトを作成します。

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Archetyoe-Project](/help/forms/assets/aem-archetype-project.png)

   1. プロジェクトをローカル開発環境にデプロイします。 以下のコマンドを使用して、ローカル開発環境にデプロイできます

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   AEM プロジェクトをデプロイすると、アダプティブ Forms テンプレートが表示されます。

   +++


ローカル ローカル開発環境の設定に関する詳細な手順と手順ガイドについては、「[AEM Forms開発環境の設定](/help/forms/setup-local-development-environment.md)」を参照してください。



## 次の手順

開発環境を設定したら、アダプティブフォームを作成する準備が整います。 次の記事では、次のことを説明します

* 空白のテンプレートからアダプティブフォームを作成する
* 表示するフィールドをレイアウトし、情報を簡単に受け入れることができます。
* フォームをプレビューします。

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->
