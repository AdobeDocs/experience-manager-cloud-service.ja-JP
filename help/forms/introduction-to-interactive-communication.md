---
title: インタラクティブ通信の概要
description: AEM Forms インタラクティブ通信を使用して、動的でデータ駆動型の通信を簡単に設計します
feature: Release Information
role: Admin
hide: true
hidefromtoc: true
source-git-commit: a771aa7e683cfbcacc8a9d5765c63d50169a2756
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 4%

---


# インタラクティブ通信

インタラクティブ通信を使用すると、業務上の書簡、ドキュメント、取引明細書、給付金通知、マーケティング用メール、請求書、ウェルカムキットなど、データ駆動型のインタラクティブ通信の作成、集計、配信を一元的に管理できます。

直感的なポイント&amp;クリック操作によるグラフィカルデザインツール（インタラクティブ通信エディター）を使用して、印刷、web、アーカイブ用の通信とビジネスドキュメントを生成できます。 エディターを使用して、通信をデザインし、データソースに接続し、ロジックを定義し、紙の対応する相手と一致するように、または厳密な法的要件を満たすように変更できます。

金融機関が口座取引明細書を作成してから政府機関がメリットの通知を合理化するなど、インタラクティブ通信は高品質で安全な法的準拠の通信を簡単かつ効率的に作成するための頼れるツールです。

![インタラクティブ通信エディター](/help/forms/assets/ic-editor.png)

## コア機能

インタラクティブ通信エディターの主な機能は次のとおりです。

| 機能 | 説明 |
|------------|-------------|
| **使いやすいデザイン** | 技術的な知識を必要としない直感的なポイント・アンド・クリック・インタフェース |
| **データ統合** | 動的コンテンツ生成のためのスキーマ、データベース、Web サービスへの接続 |
| **マルチチャネルデザイン** | 規制への準拠により、印刷形式とデジタル形式の間で統一されたエクスペリエンスを作成します |
| **動的コンテンツ** | ビジネスロジックとデータバインディングを使用してパーソナライズされたコンテンツを生成する |
| **柔軟なフォーマット** | PDF、HTML、PCL、PostScript®および ZPL 形式への出力 |
| **言語サポート** | カスタムフォントのサポートによる複数言語でのコミュニケーションの作成 |
| **リッチメディア** | テキスト、画像、インタラクティブ要素をシームレスに組み込む |
| **バージョン管理** | 変更の追跡とドキュメント履歴の管理 |
| **テンプレートのサポート** | ゼロから作成するか、テンプレートを使用して効率的なドキュメント生成を行う |
| **クラウド統合** | AEM Formsのas a Cloud Serviceでドキュメントを直接編集する |


## オンボーディング

Formsas a Cloud Serviceデプロイメントの早期アクセスプログラムで使用できるインタラクティブ通信エディター。 アクセスをリクエストするには、Formsのas a Cloud Serviceデプロイメントの組織 ID とプログラムの詳細を、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールで送信します。 アクセス権を付与されたら、[ 最初の通信の作成 ](/help/forms/create-your-first-communication.md) を開始します。








<!-- 


The Interactive Communication editor runs in any modern browser. It can be used to: 

* generate dynamic data-driven documents or correspondences and customized business documents or correspondences for print, web, or archival. 

* develop PDF documents for integration into existing workflows by binding communications to adaptive forms, XML schemas, XML sample files, databases, and web services. 

* integrate business data and render communications as a number of file types, including Adobe PDF, HTML, and printing for PCL, Adobe PostScript&reg; and Zebra (ZPL) printers.

* create interactive data capture applications by leading users through a series of visually appealing and streamlined panels, improving usability and reducing data entry errors.

## Key Features of the editor 

* **User-Friendly Interface**: The Interactive Communication editor features a point-and-click design tool that is easy to use, allowing designers to create professional communications without extensive technical knowledge.

* **Design Flexibility**: Users can design communications that match both paper and digital formats, ensuring consistency and compliance with legislative requirements.

* **Data Integration**: The tool seamlessly connects communication fields to various data sources, including XML schemas, sample files, databases, and web services.

* **Logic Definition**: Designers can define intricate logic within their communications, enhancing functionality and interactivity. 

* **Communication Creation**: Create a communication from scratch or from a template, offering flexibility and efficiency in document generation.

* **Rich Media Integration**: Add text, images, and art to your communications, creating visually appealing and engaging communication.

* **Seamless Editing**: Edit your communication documents saved in AEM Forms as a Cloud Service, ensuring easy access and continuous updates.

* **Change Tracking**: Track and review changes, maintaining a clear record of document modifications and ensuring version control.


![Output Formats and Usages](/help/assets/interactive-communication.png){align="center"}

## Usage across AEM Forms

Documents, templates, or designs created in Interactive Communication editor offer several key applications:

| **Usage**                                      | **Description**                                                                 |
|-------------------------------------------------|---------------------------------------------------------------------------------|
| PDF Document or Correspondence Creation                          | Used to generate PDF documents or correspondence for various business needs.                      |
| Document of Record Templates                   | Serves as custom templates for Documents of Record.                    |
| AEM Forms Communication APIs                   | Used as a template for various AEM Forms Communication APIs for seamless integration and automation. |


## Onboarding

The Interactive Communication editor is available for free to AEM Forms as a Cloud Service customers. You can write to mailto:aem-forms-ea@adobe.com from your official address to request access.

Adobe enables access for your organization and provide required privileges to the person designated as administrator in your organization. 

## Supported languages 

You can use the editor to create communication in languages of your choice. You can also use custom fonts in a communication. 


<!-- Communications that are created in Interactive Communication Editor can be merged with business data and rendered as a number of file types, including Adobe PDF, HTML, and printing for PCL, Adobe PostScript&reg; and Zebra (ZPL) printers.

Communication author can fill fields of a communication to personalize it for a reciever and print it, or print and fill the communication by hand. 

Communication developers can also use Interactive Communication Editor to create applications that generate dynamic, data-driven documents and produce customized business documents for print, web, or archival. 

Using communication designs, developers can create, interactive data capture applications by leading users through a series of visually appealing and streamlined panels, improving usability and reducing data entry errors. 

You can also build and maintain data capture solutions that read from, validate against, and add to corporate data sources. 

With Interactive Communication, you can integrate PDF documents into existing workflows by binding forms to XML schemas, XML sample files, databases, and web services. Forms and documents that are created in Designer can be merged with business data and rendered as a number of file types, including Adobe PDF, HTML, and printing for PCL, Adobe PostScript&reg; and Zebra (ZPL) printers. -->

## 次へ

* [最初の通信を作成](/help/forms/create-your-first-communication.md)
* [よくある問題](/help/forms/interactive-communications-faq.md)
* 用語と概念を理解する
* インタラクティブ通信エディターのチュートリアル
* フラグメントの作成
* 通信のプレビューとテスト

