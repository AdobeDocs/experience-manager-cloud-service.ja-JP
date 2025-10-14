---
title: アダプティブFormsの概要。
description: モバイルレスポンシブアダプティブFormsの作成方法については、このチュートリアルを参照してください。 これらのフォームはデバイス間でシームレスに適応し、スムーズなエクスペリエンスを実現します。
keywords: アダプティブフォーム、モバイルフォーム、レスポンシブフォーム、HTML5 フォーム
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: af58a784f24f212962ad73f11015fb788493d8b5
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 6%

---

# アダプティブフォーム（コアコンポーネント）の作成 – チュートリアル

現在の時代、ユーザーはすべてのインタラクションでモバイルに適したエクスペリエンスを期待していますが、フォームも例外ではありません。 アダプティブフォームは、モバイルに対応しているだけでなく、ユーザーエンゲージメントを向上させ、フォームの完了に要する時間を短縮するフォームを作成する際に役立ちます。

このチュートリアルでは、アダプティブフォームを作成する手順を説明します。 ユースケースといくつかのガイドに分類され、それぞれがアダプティブフォームに新機能を追加する方法を説明します。

このチュートリアルを終了すると、次の操作を実行できるようになります。

* アダプティブフォームとそのデータモデルを作成する
* アダプティブフォームのスタイル設定
* アダプティブフォームのルールエディターを使用してビジネスルールを作成する
* アダプティブフォームのフィールドの事前入力
* フォームへの電子サインの追加
* Google reCAPTCHA を使用してボットからフォームをProtect
* アダプティブフォームを様々な言語用にローカライズする
* 構造化データを生成するためのフォームの設定
* REST エンドポイントにデータを送信するためのフォームの設定
* アダプティブフォームのPublish


## コアコンポーネントベースのフォームを作成する理由

AEM Formsは、フォームエクスペリエンスを作成するための基盤コンポーネントとコアコンポーネントを提供します。 コアコンポーネントは、新しいフォームエクスペリエンスを作成するための最新の推奨アプローチです。 コアコンポーネントを使用する理由 これらのコンポーネントは軽量なオープンソース（github で利用可能）で、優れたGoogle Lighthouse と web バイタルスコアを提供し、アクセシビリティに準拠し、AEM Sitesの使い慣れた機能（バージョン管理やローカリゼーションなど）をすべて備えています。 さらに、これらのコンポーネントはスタイル設定が容易で、組織のブランディングガイドラインに従って外観を簡単にカスタマイズできます。 これらはサードパーティの依存関係がなく、JavaScriptと CSS に関する知識があれば、これらのコンポーネントを簡単にカスタマイズできます。

![&#x200B; コアコンポーネントベースのアダプティブFormsを作成する理由 これらのコンポーネントは軽量で、スタイル設定が容易で、高い Lighthouse スコアを提供し、アクセシビリティ標準に対応し、簡単にカスタマイズ可能で、オープンソースであり、github で利用でき、サードパーティのライブラリに依存せず、AEM開発者やAEM作成者が短期間で学習できるAEM Forms コアコンポーネントは、AEM WCM コアコンポーネントのすべての機能を備えています。](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## ユースケース：Adaptive Formsを使用した合理化されたホームローンの事前選定

このチュートリアルでは、大規模な銀行用のアダプティブフォームを作成します。 ユースケースを次に示します。

潜在的な住宅購入者は、銀行の Web サイトまたは支店を訪問して、住宅ローンのオプションを調べます。 従来のアプリケーションプロセスは時間がかかり、圧倒的です。多くの場合、事前にドキュメントが必要です。 これにより、一部の買い手がプロセスを開始するのを阻止し、銀行のリードジェネレーションと買い手が自信を持って夢の家を探す能力の両方を妨げます。

インタラクティブな住宅ローンの事前検証フォームを作成する必要があります。 このフォームは、基本情報を収集し、入力に基づいて借り手を事前に選定し、推定ローン額、潜在的な頭金のニーズ、様々なローンタイプに基づく金利を提供します。 事前資格のあるユーザーは、事前資格認定フォームから直接、完全なローン申し込みを開始できます。

フォームはアダプティブフォームを使用して作成されます。 これにより、パーソナライズされたエクスペリエンスが可能になり、正確な住宅ローンの事前選定に必要な財務データを収集できます。

チュートリアルが完了すると、フォームは次のフォームのようになります。

![&#x200B; 作業用フォームをここに追加 &#x200B;](/help/forms/assets/cc-tutorial-final-form.png)

## 開発環境のセットアップ

アダプティブフォームをCloud Service環境にデプロイする前に、ローカルマシンで直接アダプティブフォームを作成およびテストできます。 Adobeでは、次のことを可能にするローカル開発用のAEM SDK をに提供しています

* フォームをローカルで作成、カスタマイズ、テストする。
* フォームテーマをデザインし、ローカルに設定を作成する。
* 完成したアセットをクラウドに簡単にデプロイできます。

AEM SDK とローカル開発することで、時間が節約され、開発プロセスが簡単になります


**開始する準備はできていますか？**

1. [AEM プロジェクト用の開発ツールの設定 &#x200B;](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects)：最新リリースの [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#local-development-environment-set-up)、[Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#install-git)、[Node.js （npm） &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#node-js)、[Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=ja#install-maven) をダウンロードしてインストールします。 また、プレーンテキストエディターもインストールします。このチュートリアルの例は Visual Studio Code に基づいています。

1. [AEM SDK のインストール &#x200B;](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development):AEM SDK の最新バージョンをダウンロードしてインストールします。 これは、AEM開発に不可欠なツールとなります。 AEM SDK のバージョンを書き留めます。

   ![&#x200B; ソフトウェア配布 &#x200B;](/help/forms/assets/software-distribution.png)

   ![AEM SDK のインストール &#x200B;](/help/forms/assets/start-aem-sdk.png)

1. [AEM Forms アドオンを追加 &#x200B;](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): [&#x200B; ソフトウェア配布 &#x200B;](https://experience.adobe.com/#/downloads) ポータルから、お使いのAEM SDK のバージョンに一致するAEM Forms アドオンをダウンロードしてインストールしてください。
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++AEM Forms アドオンをインストールします。

   AEM Forms アドオンをインストールするには：

   1. AEM SDK を停止します。
   1. AEM Forms アドオン（.far）ファイルを `AEM SDK/crx-quickstart/install` フォルダーに追加します。
   1. AEM SDK を再起動します。

   +++

1. [&#x200B; ユーザー権限の設定 &#x200B;](/help/forms/setup-local-development-environment.md#configure-users-and-permissions)：開発、オーサリングなどの権限を持つユーザーを作成し、これらのユーザーを事前定義済みのフォームグループに追加します。


1. [&#x200B; アダプティブ Forms テンプレートの追加 &#x200B;](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype):AEM アーキタイプ 48 以降を使用して、新しいAEM プロジェクトを作成し、AEM SDK にデプロイします。 このプロジェクトにより、AEM SDK にアダプティブFormsテンプレートが追加されます。

   ![&#x200B; アダプティブフォームテンプレート &#x200B;](/help/forms/assets/adaptive-forms-templates.png)

   +++AEM SDK にアダプティブ Forms テンプレートを追加するには、次の手順を実行します。

   1. 以下のコマンドを実行して、AEM プロジェクトを作成します。

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Archetyoe-Project](/help/forms/assets/aem-archetype-project.png)

   1. プロジェクトをローカル開発環境にデプロイします。以下のコマンドを使用して、ローカル開発環境にデプロイできます

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   AEM プロジェクトをデプロイすると、お使いの環境でアダプティブFormsテンプレートを表示できます。

   +++


AEM Formsのローカル開発環境を設定する手順とガイドについて詳しくは、「AEM Formsのローカル開発環境の設定 [&#x200B; を参照してください &#x200B;](/help/forms/setup-local-development-environment.md)。



## 次の手順

開発環境を設定すると、アダプティブフォームを作成する準備が整います。 次の記事では、以下について説明します

* 空白テンプレートからのアダプティブフォームの作成
* 情報を表示して簡単に受け入れることができるレイアウトフィールド。
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
