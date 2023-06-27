---
title: 準備段階
description: AEMのインストールをクラウドに移行する準備ができていることを確認するために実行する必要がある手順について説明します。
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: a9aa82c8258e6a5f43680069c65518093c0baf8d
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 57%

---

# 準備段階 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="移行の計画"
>abstract="Cloud Serviceへの移行プロセスを開始する前に、AEM as a Cloud Serviceについて理解しておいてください。 主な変更点と、置き換えられた機能または非推奨となった機能を確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja" text="ベストプラクティスアナライザー"

AEMas a Cloud Service移行ジャーニーのこの段階では、AEMのas a Cloud Serviceについて理解しておく必要があります。 導入された主な変更点を確認し、クラウドへの移行を成功させるために計画する必要がある事項を理解できます。

## これまでの説明内容 {#story-so-far}

前のドキュメント [AEM as a Cloud Serviceへの移行の手引き](/help/journey-migration/getting-started.md)、AEM as a Cloud Serviceに移行するために必要なフェーズのリストの概要を説明します。 また、移行のメリットについても説明します。

## 目的 {#objective}

このドキュメントでは、考慮する必要のある要因を理解し、AEMのインストールをクラウドに移行する準備が整っていることを確認できます。

* 主な変更点と非推奨（廃止予定）の機能を確認します。
* AEM as a Cloud Service への移行を計画する方法を確認します。

## AEM as a Cloud Service アーキテクチャの主な変更点の確認 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Serviceは、AEMプロジェクトを管理するための様々な新機能と可能性を提供します。

これらの改善に伴い、AEM as a Cloud Service と比較して、AEM のオンプレミスインストールと Adobe Managed Services の間にいくつかの違いが導入されました。

次の表の項目リストは、AEM as a Cloud Service への移行に大きく関わる変更点を集めたものです。主な変更点の完全なリストについては、 [こちら](/help/release-notes/aem-cloud-changes.md) を参照してください。

<table>
<thead>
  <tr>
    <th>変更点</th>
    <th>参照</th>
    <th>重要な留意点</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>可変フィルターと不変フィルターを対応するパッケージに分割する</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=ja">AEM as a Cloud Service の主な変更点</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM as a Cloud Service の AEM プロジェクト構造</a></td>
    <td>AEM as a Cloud Service にデプロイできる単一のパッケージには、サブパッケージを含めることができます。主に、独自のパッケージに分けられた可変コンテンツと不変コンテンツを含めるために使用します。</td>
  </tr>
  <tr>
    <td>Repo Init </td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit ドキュメント</a></td>
    <td>repoinit スクリプトは、最初のノード構造、ユーザー、グループまたはサービスユーザーを作成することをお勧めします。 これらのスクリプトは、実行モードによってターゲット設定され、コードパッケージのデプロイメントによって管理可能なので、リポジトリの初期化タスクを柔軟に実行できます。</td>
  </tr>
  <tr>
    <td>カスタム実行モードは許可されていません</td>
    <td></td>
    <td>AEM as a Cloud Service で標準で提供されている実行モードのみがサポートされます。<br>追加の開発環境が追加されると、すべての環境が「開発」実行モードに結び付けられます。</td>
  </tr>
  <tr>
    <td>Cloud Manager パイプラインの実行は、デプロイする唯一の方法です</td>
    <td></td>
    <td>AEM as a Cloud Service では、/system/console へのアクセスは許可されていません。したがって、すべての OSGi 設定はコードの一部である必要があり、コードとしてデプロイする必要があります。<br>OSGi 設定は読み取り専用モードで使用でき、Cloud Manager を通じて開発者コンソールで表示できます</td>
  </tr>
  <tr>
    <td>レプリケーションエージェントは Sling コンテンツ配信で置き換えられます</td>
    <td></td>
    <td>レプリケーションエージェントの概念は Sling コンテンツ配信で置き換えられます。レプリケーションエージェントを使用するカスタマイズがある場合は、再設計する必要があります。<br>リバースレプリケーションはサポートされていません</td>
  </tr>
  <tr>
    <td>CRX/DE とパッケージマネージャー</td>
    <td></td>
    <td>CRX/DE は開発環境でのみ使用できます。<br>パッケージマネージャーにはすべてのオーサーインスタンスでアクセスできますが、デプロイされるパッケージには可変コンテンツのみを含める必要があります（例：/content または /conf）</td>
  </tr>
  <tr>
    <td>組み込み CDN と独自の CDN の取得</td>
    <td></td>
    <td>AEM as a Cloud Service には、ほとんどの使用例に最適化されたすべての環境用の CDN が含まれています。<br>独自の CDN を設定する場合、アドビサポートにリクエストを送信して承認を得る必要があります。<br>承認された場合、CDN は Fastly を指し、どの環境のAEMインスタンスを指すのではありません。</td>
  </tr>
  <tr>
    <td>長時間実行されているジョブ</td>
    <td></td>
    <td>コンテナ内で実行されるAEMインスタンスがどの時点で来ても移動できるので、Sling スケジューラーや Cron ジョブなどの長時間実行されるジョブを避けます。<br>これらの機能を再考し、Adobe Developerにオフロードできるようにします。</td>
  </tr>
  <tr>
    <td>非同期操作に切り替え</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">非同期操作の設定</a></td>
    <td>環境の全体的なパフォーマンスを向上させるために、特定の操作は非同期モードで実行されます。 システムリソースが使用可能になると、非同期ジョブはキューに入れられ、実行されます。</td>
  </tr>
  <tr>
    <td>トークンベースの認証と統合戦略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">サーバーサイド API 用のアクセストークンの生成</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=ja#authentication">トークンベースの認証に関するチュートリアル</a></td>
    <td>AEM 外のシステムが AEM 内で HTTP 操作を実行しようとするのは一般的です。<br>推奨されるアプローチは、AEM でのパスワードを使用したローカルユーザー名の作成に依存するのではなく、ここで説明する戦略を実装することです。</td>
  </tr>
  <tr>
    <td>ファイル I/O とディスク使用量</td>
    <td></td>
    <td>割り当てられるディスク容量は保証されず、コンテナ内のインスタンスが実行/実行されます。 したがって、AEMインスタンスに接続されたディスクに対してファイル I/O 操作を使用して書き込みや読み取りをおこなうことはお勧めしません。</td>
  </tr>
  <tr>
    <td>DAM アセットの更新ワークフロー</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=ja">Asset Compute サービス</a></td>
    <td>DAM アセットの更新ワークフローに含まれるメディア処理ステップが、Asset Compute サービスに置き換えられました</td>
  </tr>
  <tr>
    <td>AEM as a Cloud Service でのアセットのアップロード方法とサポートしているワークフロープロセスの手順</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">API 比較のアップロードとサポートされる WF プロセスステップ</a></td>
    <td>AEM as a Cloud Service では、アセットのアップロード中またはダウンロード中に、アセットがバイナリストレージに直接ストリーミングするか、バイナリストレージから直接ストリーミングします。<br>AEMaaCS では、すべてのワークフロープロセスの手順がサポートされているわけではありません。</td>
  </tr>
  <tr>
    <td>ワークフローランチャー</td>
    <td></td>
    <td>標準またはカスタムの DAM アセットの更新ワークフローのいずれかをコードからトリガーしているワークフローランチャーをすべて削除します。 <br>AEM as a Cloud Service にアップロードされたアセットはすべて、アセット処理サービスによって処理されます。カスタム手順については、 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=ja#post-processing-workflows"> 後処理ワークフロー</a> 後処理ワークフローの設定方法を説明します。</td>
  </tr>
  <tr>
    <td>カスタムレンディション手順</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=ja">処理プロファイル</a></td>
    <td>カスタムレンディション生成、画像変換、ビデオエンコーディングは、対応する処理プロファイルを作成して、アセット処理サービスにオフロードする必要があります。</td>
  </tr>
  <tr>
    <td>コンテンツの検索とインデックス作成</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=ja">コンテンツの検索とインデックス作成の変更</a></td>
    <td>インデックス作成の基になる処理と、インデックス作成が開始されるタイミングに大きな変更があります。<br>デプロイするコードで Oak インデックスを管理する前に、Oak インデックスを完全に理解し、リファクタリングします。</td>
  </tr>
  <tr>
    <td>すべてのメンテナンスタスクが設定可能とは限りません</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html?lang=en">AEM as a Cloud Service メンテナンスタスク</a></td>
    <td>AEM as a Cloud Service では、特定のメンテナンスタスクのみを設定できます。</td>
  </tr>
  <tr>
    <td>公開リポジトリに対する変更</td>
    <td></td>
    <td>パブリッシュリポジトリに対する直接の変更は、/home 以下での変更を除き、許可されません。 作成者に対しておこなった変更をすべて配布することを常にお勧めします。 すべてのコードと設定の変更は、対応する Cloud Manager パイプラインを通じてデプロイする必要があります。</td>
  </tr>
  <tr>
    <td>Dispatcher の設定とキャッシュ</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=ja">クラウド内の Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html?lang=en#other-content"> キャッシュ管理<br></td>
    <td>Dispatcher の設定は、特定の構造に従う必要があります。<br>設定は、コードの一部として管理され、Cloud Manager パイプラインを通じてデプロイする必要があります。</td>
  </tr>
  <tr>
    <td>バックアップと復元</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=ja">AEM as a Cloud Service のバックアップと復元</a></td>
    <td></td>
  </tr>
  <tr>
    <td>認証の変更</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=ja">AEM as a Cloud Service の IMS サポート</td>
    <td>Cloud Serviceに移行する前に、オーサーとパブリッシュの両方で SAML 2.0 統合を使用していた場合、主な変更点は、AEM as a Cloud ServiceオーサーがAdobe IMSとのみ統合される点です。 ただし、AEMas a Cloud Serviceパブリッシュ層では、SAML または他の認証統合を引き続き使用できます。 AEM as a Cloud Serviceでは、オーサー、管理者、開発者ユーザーに対してのみ IMS 認証をサポートしています。 IMS 認証では、サイト訪問者など、顧客サイトの外部エンドユーザーに対してはサポートしていません。</td>
  </tr>
</tbody>
</table>

## 非推奨（廃止予定）の機能 {#deprecated-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

Adobeは、 [廃止された機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html#deprecated-features) を参照して、as a Cloud ServiceExperience Managerで非推奨とマークされている機能に慣れてください。 AEMの導入に与える影響を確認します。

## AEM インストールのレビューのプラン {#review-planning}

AEM as a Cloud Serviceで導入された変更に慣れたら、既存のインストールのレビューを計画し始めます。 これにより、クラウドに移動するのに必要な変更のレベルを測定できます。

レビュー段階で必要になる主なステップを次の図に示します。

![画像](/help/journey-migration/assets/planning-phaseimg1.png)

次に、これらの各手順の意味を詳しく調べます。

### Cloud Service への対応準備状況の評価 {#assess-cloud-readiness}

最初の手順は、既存のAEMバージョンからCloud Serviceに移行する準備ができているかを評価し、AEM as a Cloud Serviceと互換性を持たせるためにリファクタリングが必要な領域を決定することです。

移行プロセスで予想される作業レベルを決定するために、主要な変更点および廃止された機能に照らして、現在のAEMソースコードの包括的な評価を実施します。

結果の数は、タイムラインおよびプロジェクトの成功全体に直接影響を与える可能性があります。 したがって、Adobeでは、配信を計画できるよう、できる限り多くの情報を明らかにすることをお勧めします。 または、会話を開始して、AEMのas a Cloud Serviceのベストプラクティスに従って必要なカスタマイズを再設計できます。

**ベストプラクティスアナライザー**

現在の AEM バージョンでベストプラクティスアナライザーを実行すると、評価を高速化できます。その仕組みを十分に理解することが、評価計画を迅速に立ち上げるための鍵となります。

その仕組みについては、 [ベストプラクティスアナライザー](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) のドキュメントを参照してください。

**クラウド対応準備状況アセスメントレポートの作成**

次のステップでは、これまでに得られたすべての知識に基づいてレポートを作成します。 ステージインスタンスと実稼動インスタンスからベストプラクティスアナライザーレポートを生成することで、レポートを作成します。 [次に、Cloud Acceleration Manager にアップロードします。](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 可能性の高い項目に関する消化可能なレポートを

典型的なレポートには、次の入力情報が含まれます。

* 特定の AEM インストールの機能セットの詳細を説明するドキュメント
* AEM カスタム設定およびコードの詳細
* 実稼動 Dispatcher の設定
* CDN 設定（存在する場合）

**レポートをソーシャル化**

ベストプラクティスアナライザーレポートが完了したら、関連するチームとレポートを共有し、結果を確認して次の手順の計画を立てます。 必要に応じて、 [印刷プレビュー](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam) を使用してレポートの印刷バージョンを配布することもできます。

### リソース計画のレビュー {#review-resource-planning}

Cloud Service への移行に必要な労力のレベルを見定めたら、リソースを特定してチームを編成し、移行プロセスに必要な役割と責任を定める必要があります。

### KPI の設定 {#establish-kpis}

主要業績評価指標（KPI）をまだ設定していない場合は、最も重要なことにチームが専念できるように、AEM の実装に関する KPI を設定することをお勧めします。

詳しくは、 [KPI の開発](https://experienceleague.adobe.com/welcome/aem/part6.html?lang=ja) ビジネス目標に合った適切な KPI を選択する方法を学ぶことができます。

## 次の手順 {#what-is-next}

AEM as a Cloud Service に移行するために必要な変更の範囲を確認したら、実際に移行を実行する前に、[コードとコンテンツをクラウド対応にします](/help/journey-migration/implementation.md)。

## その他のリソース {#additional-resources}

* [Cloud Acceleration Manager の概要](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Cloud Acceleration Manager を使用してクラウドへの移行を迅速に行う方法に関する包括的なガイド。
* [AEMas a Cloud Service:概要、アーキテクチャ、考え方の違い](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=ja#dashboard/learning)
* [AEM a Cloud Service ホーム](/help/overview/home.md) - Experience Manager as a Cloud Service ドキュメントの概要については、まずこちらを参照してください。
* [AEM as a Cloud Service の概要](/help/overview/home.md) - このガイドでは、基礎知識、用語、アーキテクチャなど、Experience Manager as a Cloud service の概要を説明します。
* [オンボーディングジャーニー](/help/journey-onboarding/overview.md) - このガイドでは、アクセス方法やチームのセットアップ方法など、Experience Manager as a Cloud Service の基本について概要を説明します。。
