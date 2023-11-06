---
title: Adobe Experience Manager as a Cloud Service のアーキテクチャの概要
description: Adobe Experience Manager as a Cloud Service のアーキテクチャの概要。
exl-id: 3fe856b7-a0fc-48fd-9c03-d64c31a51c5d
source-git-commit: 689b672e75c4e4d2fa8f716d93c65418f332a266
workflow-type: tm+mt
source-wordcount: '2656'
ht-degree: 11%

---

# Adobe Experience Manager as a Cloud Service のアーキテクチャの概要 {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="intro_aem_cloudservice_architecture"
>title="AEM as a Cloud Service アーキテクチャの概要"
>abstract="ここでは、AEM as a Cloud Service の新しいアーキテクチャを概観し、変更点を理解します。AEMは、様々な数の画像を含む動的なアーキテクチャになったので、クラウドアーキテクチャを理解するのに時間をかけることが重要です。"
>additional-url="https://video.tv.adobe.com/v/330542/" text="アーキテクチャの概要"

Adobe Experience Manager(AEM)as a Cloud Serviceは、影響の大きいエクスペリエンスを作成および管理するための、合成可能な一連のサービスを提供します。

このページでは、AEM as a Cloud Serviceの論理アーキテクチャ、サービスアーキテクチャ、システムアーキテクチャ、および開発アーキテクチャの概要を説明します。

## 論理アーキテクチャ {#logical-architecture}

AEM as a Cloud Serviceは、AEM Sites、AEM Assets、AEM Formsなどの高度なソリューションで構成されています。 これらのサービスは個別にライセンスを受けますが、共同で使用できます。 各ソリューションは、それぞれの使用例に応じて、AEM as a Cloud Serviceが提供する合成可能なサービスの組み合わせを使用します。

### プログラム {#programs}

AEMアプリケーションは、 [プログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) ライセンス権限に従って Cloud Manager アプリケーションで作成する これらのプログラムを使用すると、特定のプロジェクトのコンテキストで、関連するAEMアプリケーションの命名、設定、権限の割り当て方法を完全に制御できます。

お客様は通常、 **テナント**( 別名 *IMS 組織* (Identity Managementシステム )。 テナントは、必要な数のプログラムを持ち、ライセンスを受けることができます。 例えば、AEM Assetsの中央プログラムを見るのは非常に一般的ですが、AEM Sitesは、複数のオンラインエクスペリエンスに対応する複数のプログラムで使用される場合があります。

>[!NOTE]
>
>AEMEdge Delivery Servicesは、ライセンスの観点から他の主なソリューションの一部となりながら、Cloud Manager で最上位のソリューションとして公開されます。 例えば、AEM SitesとEdge Delivery Services。

プログラムは、高レベルのソリューションの任意の組み合わせで構成でき、各ソリューションは 1 対多のアドオンからサポートできます。 例えば、AEM Sitesの場合は Commerce や Screens、AEM Assetsの場合はDynamic Media、の場合はBrand Portalです。

![AEMas a Cloud Service — プログラム](assets/architecture-aem-edge-programs.png "AEMas a Cloud Service — デプロイメントアーキテクチャ")

### 環境 {#environments}

AEM Sites、AEM Assets、AEM Formsの各ソリューションを使用してプログラムを作成すると、関連するAEMインスタンスは、このプログラム内のAEM環境の形式で表されます。

次の 4 種類の [環境](/help/implementing/cloud-manager/manage-environments.md) AEM as a Cloud Serviceで使用可能：

* 実稼動環境：

   * 実稼動環境は、実務担当者向けのアプリケーションをホストし、ライブエクスペリエンスを実行します。

* ステージ環境：

   * ステージ環境は、通常、1 対 1 の関係で実稼動環境に結び付けられます。
   * ステージ環境は、主に、アプリケーションに対する変更が実稼動環境にプッシュされる前の自動テスト用に設計されています。
      * これは、メンテナンスアップデートの一環としてAdobeによって開始される変更や、コードのデプロイメントによって開始される変更とは独立しています。
      * また、コードをデプロイする場合は、手動でテストを実行することもできます。
   * 通常、ステージ環境のコンテンツは、セルフサービスのコンテンツコピー機能を使用して、実稼動コンテンツと同期を維持します。
* 開発環境:
   * 開発環境を使用すると、開発者は、ステージ環境および実稼動環境と同じランタイム条件でAEMアプリケーションを実装およびテストできます。
   * 変更は、デプロイメントパイプラインを通じておこなわれ、実稼動デプロイメントパイプラインと同じコード品質とセキュリティゲートを使用できます。
* 迅速な開発環境 (RDE):
   * RDE 環境を使用すると、通常の開発環境で見つかる正式なデプロイメントパイプラインを経ずに、新しいコードや既存のコードを RDE インスタンスにデプロイする際に、迅速な開発反復を実行できます。

### Edge 配信サービス {#logical-architecture-edge-delivery-services}

AEMプログラムは、 [Edge Delivery Services](/help/edge/overview.md) 同様に。

設定が完了すると、AEMは、Edge Delivery Servicesを使用したエクスペリエンスの構築に使用する GitHub コードリポジトリを参照できるようになります。 その結果、関連するエクスペリエンスで新しい設定オプションを使用できるようになります。 これには、Adobe管理 CDN の設定、ライセンス指標へのアクセス、SLA レポートなどが含まれます。

## サービスアーキテクチャ {#service-architecture}

AEM as a Cloud Serviceの合成可能なサービスの上位レベルのリストは、コンテンツ管理とエクスペリエンス配信の 2 つのセグメントで表すことができます。

![AEMas a Cloud Serviceの概要 —Edge Delivery Services](assets/architecture-aem-edge.png "AEMas a Cloud Serviceの概要 —Edge Delivery Services")

コンテンツ管理の場合、コンテンツのオーサリングに使用する 2 つの主なサービスセットがあり、どちらも *コンテンツソース*:

* AEMオーサー層：Web コンテンツを管理するための Web ベースのインターフェイス（および関連する API）を提供します。 これは、次の両方の方法で機能します。
   * ヘッドフル — ページエディターとユニバーサルエディターを使用
   * ヘッドレス — コンテンツフラグメントエディターを使用
* ドキュメントベースのオーサリング層：次のような標準アプリケーションを使用してコンテンツをオーサリングできます。
   * Microsoft Word と Excel - SharePoint経由
   * Google Drive 経由のドキュメントとシート

エクスペリエンス配信の場合、AEM SitesまたはAEM Formsを使用する際には、相互に排他的でなく、共有のAdobe管理 CDN（コンテンツ配信ネットワーク）の下で異なるオリジンとして動作する、2 つの主なサービスセットもあります。

* AEMパブリッシュ層：
   * 標準のAEMパブリッシャーおよび Dispatcher のファームを実行し、公開済みコンテンツと組み合わされた Web ページおよび API コンテンツ (GraphQLなど ) の動的レンダリングを可能にします。
   * 主にサーバー側のアプリケーションロジックに基づいています。
* エッジ配信パブリッシュ層：
   * AEMオーサー層やドキュメントベースのオーサリング層など、様々なコンテンツソースから Web ページや API コンテンツを動的にレンダリングできます。
   * クライアント側のアプリケーションロジックに基づき、最大のパフォーマンスを実現するように設計されています。

また、主な隣接サービスもあります。

* エッジ配信アセット層：
   * AEM Assetsから承認および公開されたメディア項目を配信できるようにします。 例：画像、ビデオ。
   * 通常、メディア項目は、AEMパブリッシュ層、エッジ配信パブリッシュ層で実行されるエクスペリエンス、またはAEM Assetsと統合された他のAdobe Experience Cloudアプリケーションから参照されます。
* AEMプレビュー層とEdge Delivery Servicesプレビュー層は、次のとおりです。
   * また、AEMパブリッシュ層とエッジ配信パブリッシュ層をそれぞれ使用して構築されたエクスペリエンスにも使用できます。
   * コンテンツ作成者が、公開操作の前にコンテキスト内のコンテンツをプレビューできるようにします。

>[!NOTE]
>
>デフォルトでは、Assets のみのプログラムには、パブリッシュ層もプレビュー層もありません。

他にも隣接するサービスがあります。

* レプリケーションサービス：
   * コンテンツ管理層とエクスペリエンス配信層の間に位置します。
   * を処理します。 *公開* 操作がコンテンツ作成者によって発行され、公開されたコンテンツがパブリッシュ層 (AEMまたは Edge Delivery) に提供される。

  >[!NOTE]
  >以前のバージョンのAEMのレプリケーションフレームワークはコンテンツの公開に使用されなくなったので、レプリケーションサービスはAEMの 6.x バージョンとは異なり、完全な再設計を行いました。
  >
  >最新のアーキテクチャは、 *公開と購読* クラウドベースのコンテンツキューを使用したアプローチ AEMパブリッシュ層では、多数のパブリッシャーがパブリッシュコンテンツをサブスクライブでき、AEMas a Cloud Serviceの実際の迅速な自動スケーリングを実現する上で不可欠な要素です

* Content Repository サービス：
   * AEMオーサー層で使用されます。
   * JCR 準拠のコンテンツリポジトリのクラウドベースのインスタンスで、Apache Oak テクノロジーによって実装されます。
   * コンテンツの永続性は、主に BLOB ベースのクラウドストレージに基づいています。
* CI/CD サービス：
   * AEM環境へのデプロイパイプラインの管理に関する Cloud Manager 機能のサブセットを表します。
* テストサービス：
   * 実行に使用される基盤となるインフラストラクチャを表します。
      * 機能テスト
      * UI テスト：例えば、Selenium や Cypress のスクリプトに基づく場合、
      * エクスペリエンス監査テスト：例えば、Lighthouse スコア、

     をAEM環境へのデプロイメントパイプラインの一環として、または GitHub のプルリクエストの一部として Edge Delivery コードリポジトリに送信します。
* Data サービスの場合：
   * ライセンス指標（コンテンツリクエスト、ストレージ、ユーザーなど）や使用状況レポート（アップロード数、ダウンロード数など）などの顧客データを公開します。
   * 顧客データは、API を介して、および製品ユーザーインターフェイス（Cloud Manager など）内で公開できます。
* Real-User Metric(RUM) サービス：
   * 顧客体験（ページビュー数、コア Web バイタル、コンバージョンイベントなど）から主要指標を収集し、関連クエリ（例えば、過去 7 日間の特定のドメインのトップページビュー数）に応答します。
* Assets Compute Service の主な機能は次のとおりです。
   * アップロードされた画像、ビデオ、ドキュメント (PDF、Adobe Photoshopファイルなど ) の処理を担当します。 処理では、Adobe Senseiを使用して画像およびビデオのメタデータ（説明タグや主要な色調など）を抽出し、レンディション（様々なサイズや形式など）を生成し、Adobe PhotoshopやAdobe Lightroom API などの API にアクセスできます。
* Identity Managementサービス (IMS):
   * は、特定のAdobe Experience Cloudアプリケーション (Cloud Manager やAEMオーサー層など ) のユーザーとユーザーグループを管理および認証する一元的な場所です。
   * Adobe Admin Consoleを介してアクセスされます。

## システムアーキテクチャ {#system-architecture}

### AEMのオーサー層、プレビュー層、パブリッシュ層 {#aem-author-preview-publish-tiers}

AEMオーサー層とパブリッシュ層は、標準の Container Orchestration サービスで操作される Docker コンテナのセットとして実装されています。 結果として得られるコンテナ化アーキテクチャは、実際のアクティビティ（コンテンツ管理の場合）と実際のトラフィック（エクスペリエンス配信の場合）に応じて、様々なポッド数の完全に動的なシステムを意味します。 これにより、AEMはトラフィックパターンの変化に対応できます。

AEMオーサー層は、1 つのコンテンツリポジトリを共有するAEMオーサーポッドのクラスターとして動作します。 少なくとも 2 つのポッドを使用すると、メンテナンスタスクの実行中や、デプロイメントプロセスの実行中にビジネスを継続できます。

AEMパブリッシュ層は、AEMパブリッシュインスタンスのファームとして操作され、それぞれに公開済みコンテンツの独自のコンテンツリポジトリが含まれます。 各パブリッシャーは、Adobeが管理する CDN のオリジンとして機能する、コンテンツの具体化されたビュー用のAEM Dispatcher モジュールを備えた単一の Apache インスタンスに結合されます。 2 つ以上のポッドを使用することで、ビジネスの継続性も実現できますが、トラフィックが多い期間にこの数が増えるのは珍しくありません。

AEMプレビュー層は、1 つのAEMノードで構成されます。 これは、パブリッシュ層に公開する前のコンテンツの品質保証に使用されます。 特にデプロイメント中に、時々ダウンタイムが発生する場合があります。これは、プレビュー層で発生する可能性があります。

### Edge 配信サービス {#system-architecture-edge-delivery-services}

Edge Delivery Servicesは、CDN と、最もパフォーマンスの高い方法でページを組み立てるためのサーバーレスインフラストラクチャの上で動作します。 リソースが要求されると、サーバーレスインフラストラクチャは、公開されたコンテンツをセマンティックHTMLに変換し、CDN の起源として機能します。

セマンティックHTMLへの変換は、AEMオーサー層またはドキュメントベースのオーサリング環境から提供される公開済みコンテンツからおこなわれます。

次の図は、Microsoft Word（ドキュメントベースのオーサリング）で Sites コンテンツを編集し、Edge 配信に公開する方法を示しています。 また、様々なエディターを使用した従来のAEMの公開方法も示します。

![AEM Sitesas a Cloud Service-Edge Delivery Services付き](assets/architecture-aem-edge-author-publish.png "AEM Sitesas a Cloud Service-Edge Delivery Services付き")

Edge Delivery ServicesはAdobe Experience Managerに含まれているので、Edge 配信、AEM Sites、AEM Assetsは同じドメイン上に共存できます。 これは、大規模な Web サイトの一般的な使用例です。 例えば、顧客はトラフィックの多い特定のページをEdge Delivery Servicesに移行し、その他のすべてのページがAEMパブリッシュ層に残る場合があります。

## 開発アーキテクチャ {#development-architecture}

### コードリポジトリー {#code-repositories}

AEMプロジェクトのコードと設定は、コードリポジトリに保存されます。コードリポジトリから、変更時にデプロイパイプラインが発行されます。 次のような様々なタイプのコードリポジトリがあります。

* AEMフルスタック：
   * AEMオーサー層とパブリッシュ層用のサーバー側 Java コードと OSGi 設定を保存する場合。
* AEMフロントエンド：
   * AEMオーサー層とパブリッシュ層用のクライアント側 JS、CSS およびHTMLコードを保存するため。
clientlibs について詳しくは、 [AEMでのクライアント側ライブラリの使用をas a Cloud Serviceします。](/help/implementing/developing/introduction/clientlibs.md)
* AEM Web 層：
   * AEMパブリッシュ層用の Dispatcher 設定ファイルを格納します。
* AEM設定：
   * AEMパブリッシュ層とEdge Delivery Servicesパブリッシュ層用の様々な設定オプション（CDN 設定やメンテナンスタスク設定など）を保存できます。
* AEMエッジ配信：
   * クライアント側 JS、CSS、およびHTMLコードをEdge Delivery Servicesで作成して保存する場合

### デプロイメントパイプライン {#deployment-pipelines}

開発者と管理者は、AEM Manager を通じて提供される継続的統合/継続的配信 (CI/CD) サービスを使用して、Cloud のas a Cloud Serviceアプリケーションを管理します。 また、監視、メンテナンス、トラブルシューティング（ログファイルへのアクセスなど）、ライセンスに関する情報もすべて公開されています。

![AEM as a Cloud Service - デプロイメントアーキテクチャ](assets/architecture-aem-edge-deployment-pipelines.png "AEM as a Cloud Service - デプロイメントアーキテクチャ")

AEM Manager は、as a Cloud Serviceのインスタンスに対するすべての更新を管理します。 これは、顧客アプリケーションを構築、テストし、オーサー層、プレビュー層、パブリッシュ層にデプロイする唯一の方法です。 これらの更新は、Adobe、新しいバージョンのAEM Cloud Serviceの準備ができたとき、または新しいバージョンのアプリケーションの準備ができたときに、自分でトリガーできます。

これは、プログラム内の各環境に結び付けられたデプロイメントパイプラインによって実装されます。 Cloud Manager パイプラインが実行されると、オーサー層とパブリッシュ層の両方に対応する、新しいバージョンの顧客アプリケーションが作成されます。これは、最新の顧客パッケージとアドビの最新ベースラインイメージを組み合わせて実現されます。

デプロイメントパイプラインは、顧客がコードを変更している場合、またはAdobeが新しいメンテナンスリリースをデプロイしている場合にトリガーされます。

どちらの場合も、同じ自動化されたテストのセットが実行されます。 テストで構成されます。

* 製品の整合性を確保するためにAdobeが寄与した
* お客様が提供するテスト
   * 機能テスト： http
   * UI テスト：Selenium または Cypress テクノロジーに基づく

これらの自動テストはステージング環境で実行されます。そのため、ステージ環境のコンテンツを実稼動インスタンス上のコンテンツにできる限り近づけることが重要です。

すべてのテストが正常に完了すると、新しいコードが実稼動環境にデプロイされます。

### 周期的な更新 {#rolling-updates}

Cloud Manager では、ローリング更新パターンを使用してすべてのサービスノードを更新することで、最新バージョンのAEMアプリケーションへのカットオーバーを完全に自動化します。 これは、 **ダウンタイムなし** オーサーサービスまたはパブリッシュサービスの場合。

## AEM 6.x 以降の主なイノベーション {#major-innovations-since-aem-6x}

AEMas a Cloud Serviceの最新のアーキテクチャでは、以前の世代 (AEM 6.x 以前 ) と比較して、次のように、基本的な変更とイノベーションが導入されています。

* すべてのファイルは、クラウドデータストアに直接アップロードされ、クラウドデータストアから提供されます。 関連するビットストリームは、AEM オーサーサービスおよび公開サービスの JVM を経由しません。その結果、AEMオーサーサービスとパブリッシュサービスのノードのサイズを小さくできるので、迅速な自動スケーリングの期待に応えることができます。 実務担当者にとっては、これにより、画像、ビデオなどのタスクをアップロードおよびダウンロードする際の操作性が向上します。

* コンテンツの公開で構成されるすべての操作に、サブスクリプションパターンに従ったパイプラインが含まれるようになりました。公開済みコンテンツは、パイプライン内の様々なキューにプッシュされ、パブリッシュサービスのすべてのノードがそれらのキューをサブスクライブします。その結果、パブリッシュサービスのノード数をオーサー層が把握している必要はなくなり、パブリッシュ層の迅速な自動スケーリングが可能になります。

* アーキテクチャでは、アプリケーションのコンテンツをアプリケーションのコードと設定から完全に切り離しています。すべてのコードと設定は実質的に不変で、オーサーサービスとパブリッシュサービスの様々なノードの作成に使用されるベースラインイメージに組み込まれています。その結果、各ノードが同一であることが完全に保証され、コードと設定の変更は Cloud Manager パイプラインの実行によってのみグローバルにおこなえます。

* アーキテクチャには、特にAdobe I/O・ランタイムを使用した、サーバレス・テクノロジー上に構築された複数のマイクロ・サービスが含まれます。

## その他の情報 {#further-information}

関連トピック：

* Edge 配信サービス:

   * [AEMas a Cloud Serviceの概要 —Edge Delivery Services](/help/edge/overview.md)
   * [使用Edge Delivery Services](/help/edge/using.md)
   * [Edge Delivery Servicesを使用して、基盤となるアーキテクチャと重要なAEMの部分をas a Cloud Serviceする](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/introduction/architecture.html?lang=ja)
