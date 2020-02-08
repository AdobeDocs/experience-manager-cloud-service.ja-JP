---
title: AEM Connectorの実装
description: AEM Connectorの実装
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


AEM Connectorの実装
=============================

以下に、 [AEM Connectorsの構築に役立つリファレンスを示します](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) 。コネクタの送信と保守に関するガイダンスと共に [お読](submit.md) みく [ださい](maintain.md) 。

AEMの開発者用ライセンスは、 [Adobe Exchange Programを通じて取得できます](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。

一般的な統合パターン
---------------------------

AEMは最先端のWebエクスペリエンス管理ソリューションで、統合の可能性が高い多数の領域を提供します。 一般的な統合パターンは次のとおりです。

* 外部システムからAEMにデータを取り込みます。 例えば、AEMを利用するWebサイトを訪問する広範な閲覧者が連絡先情報を利用できるように、CRMから連絡先情報を書き出します。  実装では、Slingのスケジュール済みジョブ [を使用する必要があります](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)。コンテナがダウンした場合でも、ジョブが確実に実行されます。 ジョブが複数回トリガーされる可能性があることを前提としてコードを設計する必要があります。
* AEMから外部システムへのデータの書き出し 例えば、AEMを利用するWebサイトでCRMに送信されるニュースレター購読の設定などです。
* AEMからのアセットの取得を参照してください。 例えば、AEM Assetsに保存されたアセットを参照する外部コンテンツ管理システム(CMS)などです。 別の例として、AEM Assets内の画像にリンクするPIMシステムがあります。
* AEMインフラストラクチャへのアセットの保存。 例えば、承認されたアセットをAEM Assetsに保存するマーケティングリソース管理(MRM)システムなどです。
* カスタムUIコンポーネントの設定とレンダリング 例えば、作成者がビデオコンポーネントをドラッグ&amp;ドロップし、ライブサイトで再生する特定のビデオを設定できるようにします。
* パートナーサービスを持つアセットに対する操作。 例えば、ページが公開されたときにビデオプラットフォームにアセットを送信する場合などです。
* AEM管理コンソールでのサイト、ページまたはアセットの分析。 例えば、既存のページまたは未公開のページに対するSEOレコメンデーションの作成など。
* 外部サービスによって保持されるユーザーデータへのページレベルのアクセス。 例えば、人口統計情報を利用してサイトのエクスペリエンスをパーソナライズできます。 コンテキストデータの保存、操作、および表示のためのフレームワークであるContextHubについて説明します。
* サイトコピーまたはアセットメタデータの変換。 AEM Translation Frameworkを使用したサンプルコードについては、 [](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) AEM Translation Framework Bootstrap Connectorを参照してください。これは、Translation Connectorsの推奨される実装です。


役立つドキュメント
--------------------

クラウドサービスドキュメントとしてのExperience Manager [は](../overview/introduction.md) 、AEMでの開発に関する貴重なインサイトを提供します。 AEM Connectorの実装時に役立つ、次に示す特定の技術トピックおよびリファレンスを示します。

* アドビコンサルティングサービス(ACS) [AEMサンプル](http://adobe-consulting-services.github.io/acs-aem-samples/) （AEM開発者の教育に役立つコメント付きコード）
* この記事の「共通の統合パターン」の節にある様々なドキュメントのリンク

コミュニティリソース
--------------------

上記の静的ドキュメントに加えて、アドビおよびAEMコミュニティでは、コネクターを市場に導くのに役立つリソースを提供しています。

* アドビコミュニティの [AEMフォーラムは](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) 、仲間が質問をし、質問に答えるアクティブなサイトです。
* アドビのその他のテクニカルリソースは、特定のパートナーレベルで利用できます。 詳しくは、 [Adobe Exchange Programを参照してください](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html)。
* 導入の支援を希望する場合は、アドビのプロフェッショナルサービスチームを検討するか [、](http://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html)[](https://solutionpartners.adobe.com/home/partnerFinder.html) Solution Partner Finderで世界中のアドビのパートナーのリストを確認してください

パッケージ構造ルール
-----------------------

ローリングデプロイメントをサポートするために、AEMは、例えばコネクターを含むクラウドサービスパッケージで、「不変」コンテンツと「可変」コンテンツを厳密に区切っています。 パッケージは、次のものを含むものの間で明確に区切る必要があります。

* `/apps`
* `/content` および `/conf`

コネクタは、この記事で説明するパッケージ化のガイドラインに従う [必要があります](/help/implementing/developing/introduction/aem-project-content-package-structure.md)。 既存のコネクタも同様にリファクタリングする必要があります。

さらに、アドビのみがにコードを書き込み、お客様とパ `/libs`ートナーがにコードを書き込む必要がありま `/apps`す。

既存のコネクタをリファクタリングして、一度配置した設定を他の最上位フォルダ（など）に移動する `/etc` 必要がある場合もありま `/conf`す。 これは、 [AEMのドキュメントで説明されています](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

複数のコネクタを持つお客様向けに、クリーンなリポジトリ構造を推進するた `/apps/connectors/<vendor>` めに、コネクタコードの大部分をの下に置くことをお勧めします。

クラウドサービス設定
-----------------------------

コネクタ実装の1つの側面は、コネクタの設定を裏付けるコードです。 このコードを使用すると、ツール/操作/クラウドサービスの下に、コネクタ名の付いたカードが表示されます。 クリックすると、設定ブラウザーがポップアップ表示され、顧客がコネクタ設定を含む親フォルダーを選択します。 コネクタのコードによって、設定する必要があるすべてのプロパティを持つフォームが生成され、最終的には、の設定フォルダーに値が格納されま `/conf`す。 このフォルダは、後で「サイトのプロパティ」タブまたは「アセットのプロパティ」タブで選択できます。


コンテキスト対応設定
-----------------------------

[コンテキスト対応設定では](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 、、、およびのサブフォルダーを含む異なるフォルダー間で `/libs`レイ `/apps`ヤー設 `/conf` 定を行うことがで `/conf`きます。 継承をサポートし、顧客が各マイクロサイトに特定の変更を加えながらグローバル設定を行えるようにします。 この機能をクラウドサービス設定で利用できるので、コネクタコードは、特定の設定ノードを参照する代わりに、Context-Aware Configuration APIを使用して設定を参照する必要があります。

変更した設定がコネクタで使用されている場合、コネクタを設計して、コネクタが提供するデフォルト設定に対する今後の更新を任意の顧客設定に含めたり、マージしたりします。 カスタマイズされた（お客様が変更したように）コンテンツや設定を、お客様の警告や同意なしに変更すると、Connectorで破損(または予期しない動作を引き起こす可能性があります。

コーディングのベストプラクティス
----------------------

クラウドサービスとしてのAEMはクラウドネイティブのソリューションであるため、コネクタのコード戦略に影響を与える可能性のあるガイドラインがいくつかあります。 詳しくは [、「AEM as a Cloud Service Development Guidelines](/help/implementing/developing/introduction/development-guidelines.md) 」を参照してください。

AEM Connectorのテスト
-------------------------

新しいコネクタは、ローカル環境開発テクニックを使用して作成（または既存のコネクタを変更）する必要があります。 パートナーチームは、ISVパートナーにサンドボックス環境を提供し、AEM Connectorをバニラアプリケーションにデプロイして、確実に機能するようにします。
