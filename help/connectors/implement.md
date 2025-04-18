---
title: AEM コネクタの実装
description: コネクタとその機能、および Experience Manager にコネクタを実装する方法について説明します。
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: ht
source-wordcount: '922'
ht-degree: 100%

---


AEM コネクタの実装
=============================

以下に、AEM コネクタの作成に役立つリファレンスを示します。コネクタの[送信](submit.md)と[保守](maintain.md)に関するガイダンスと併せてお読みください。

AEM の開発者用ライセンスは、[Adobe Exchange プログラム](https://partners.adobe.com/technologyprogram/experiencecloud.html)を通じて取得できます。

一般的な統合パターン
---------------------------

AEM は最先端の Web エクスペリエンス管理ソリューションで、様々な領域で統合をおこなえる可能性があります。一般的な統合パターンは次のとおりです。

* 外部システムから AEM にデータを取り込む。例えば、CRM から連絡先情報を書き出して、AEM を利用した Web サイトを訪問する広範なオーディエンスに公開するような場合です。実装では、Sling の[スケジュール済みジョブ](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)を使用する必要があります。これにより、コンテナが停止してもジョブの実行が保証されます。ジョブが複数回トリガーされる可能性があることを前提として、コードを設計する必要があります。
* AEM から外部システムにデータを書き出す。例えば、ニュースレターの購読設定は、AEM を活用した web サイトで CRM に送信されます。
* AEM からアセットを取得する。例えば、AEM Assets に保存されているアセットを外部のコンテンツ管理システム（CMS）で参照するような場合です。別の例としては、PIM システムから AEM Assets 内の画像にリンクする場合もあります。
* アセットを AEM インフラストラクチャに保存する。例えば、マーケティングリソース管理（MRM）システムで承認済みアセットを AEM Assets に保存するような場合です。
* カスタム UI コンポーネントを設定およびレンダリングする。例えば、作成者がビデオコンポーネントをドラッグ＆ドロップして、ライブサイトで特定のビデオを再生できるように設定するような場合です。
* パートナーサービスを使用してアセットに対する操作をおこなう。例えば、ページが公開されたときにアセットをビデオプラットフォームに送信するような場合です。
* AEM Admin Console でサイト、ページ、アセットを分析する。例えば、既存ページまたは未公開ページの SEO のレコメンデーションを提示するような場合です。
* 外部サービスで管理されているユーザーデータにページレベルでアクセスする。例えば、人口統計情報を利用してサイトのエクスペリエンスをパーソナライズするような場合です。詳しくは、ContextHub に関する情報を参照してください。ContextHub は、コンテキストデータを保存、操作、表示するためのフレームワークです。
* サイトコピーまたはアセットメタデータを翻訳する。AEM 翻訳フレームワークを使用したサンプルコード（翻訳コネクタの推奨される実装）については、[AEM 翻訳フレームワークブートストラップコネクタ](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector)を参照してください。


有用なドキュメント
--------------------

Adobe Experience Manager as a Cloud Service の[ドキュメント](../overview/introduction.md)では、AEM での開発に関する有益なインサイトを提供します。また、以下に示す特定の技術トピックおよびリファレンスは、AEM コネクタの実装時に役に立つ可能性があります。

* アドビコンサルティングサービス（ACS）の [AEM サンプル](https://adobe-consulting-services.github.io/acs-aem-samples/)：AEM 開発者の参考になるコメント付きコードを参照できます
* この記事の「一般的な統合パターン」の節で示した様々なドキュメントリンク

コミュニティリソース
--------------------

上記の静的ドキュメントに加えて、アドビおよび AEM コミュニティでは、コネクタの市場投入に役立つ以下のリソースを提供しています。

* アドビコミュニティの [AEM フォーラム](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html)は、同業者が質問をしたり質問に答えたりする活発なサイトです。
* アドビのその他の技術リソースは、個々のパートナーレベルで利用できます。詳しくは、[Adobe Exchange プログラム](https://partners.adobe.com/technologyprogram/experiencecloud.html)を参照してください。
* 組織が実装の支援を希望する場合は、アドビの [Professional Services](https://solutionpartners.adobe.com/s/directory) チームへの依頼を検討するか、[ソリューションパートナーファインダー](https://solutionpartners.adobe.com/s/directory/)でアドビの世界中のパートナーのリストを確認してください。

パッケージ構成ルール
-----------------------

ローリングデプロイメントを容易にするために、コネクタなどの AEM as a Cloud Service パッケージでは、「不変」コンテンツと「可変」コンテンツを厳密に区別しています。パッケージは、次の内容を含むように明確に整理する必要があります。

* `/apps`
* `/content` および `/conf`

コネクタは、パッケージ化に関するこれらのガイドラインに従う必要があります。ガイドラインについては、[AEM プロジェクトの構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)を参照してください。既存のコネクタは、ガイドラインに準拠するためにリファクタリングも必要になります。

さらに、`/libs` にコードを書き込むのはアドビだけで、ユーザーとパートナーは `/apps` にコードを書き込みます。

既存のコネクタの場合、一度 `/etc` に配置した設定を他の最上位フォルダー（`/conf` など）に移動するには、コネクタのリファクタリングも必要になる可能性があります。この再構築は AEM 6.5 の一部としておこなわれ、[AEM 6.5 のドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring)で説明されています。

アドビでは、特に複数のコネクタを使用するお客様向けに、クリーンなリポジトリ構造を維持するために、コネクタコードのほとんどを `/apps/connectors/<vendor>` の配下に格納することをお勧めします。

クラウドサービスの設定
-----------------------------

コネクタ実装の 1 つの側面として、コネクタの設定をサポートするコードがあります。このコードにより、ツール／操作／Cloud Services で、コネクタ名の付いたカードが表示されるようになります。カードをクリックすると、[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)がポップアップ表示され、コネクタ設定を含んだ親フォルダーをユーザーが選択できます。コネクタのコードによって、設定が必要なすべてのプロパティを含んだフォームが生成され、最終的に、`/conf` の配下の設定フォルダーにプロパティ値が格納されます。このフォルダーは、後ほど「サイトのプロパティ」タブまたは「アセットのプロパティ」タブで選択できます。


コンテキスト対応の設定
-----------------------------

[コンテキスト対応の設定](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)により、`/libs`、`/apps`、`/conf` および `/conf` 配下のサブフォルダーなど、異なるフォルダーにわたって設定を階層化できます。継承をサポートしているので、ユーザーがグローバル設定をおこないながら、マイクロサイトごとに個別に変更を加えることができます。この機能をクラウドサービスの設定に利用できるので、コネクタコードでは、特定の設定ノードを参照するのではなく、Context-Aware Configuration API を使用して設定を参照する必要があります。

変更した設定がコネクタで使用される場合は、コネクタ提供のデフォルト設定に対する今後の更新をユーザー側のあらゆる設定と結合できるようにコネクタを設計します。事前の通知や同意なしにお客様がカスタマイズしたコンテンツや設定を変更すると、コネクタの動作が中断したり、予期しない動作が発生したりする場合があることに注意してください。

コーディングのベストプラクティス
----------------------

AEM as a Cloud Service はクラウドネイティブソリューションなので、コネクタのコード戦略に影響を与える可能性のあるガイドラインがいくつかあります。詳しくは、[AEM as a Cloud Service の開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md)を参照してください。

AEM コネクタのテスト
-------------------------

ローカル環境の開発テクニックを使用して新しいコネクタを作成（または既存のコネクタを変更）する必要があります。パートナーチームが ISV パートナーにサンドボックス環境を提供するので、その環境でパートナーは AEM コネクタをバニラアプリケーションにデプロイして動作を確認できます。
