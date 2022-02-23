---
title: 準備段階
description: AEMのインストールをクラウドに移行する準備ができていることを確認するために必要な手順について説明します。
source-git-commit: 8988f184b7a2153ff32aa3bdc26283f9a7b414b8
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 10%

---

# 準備段階 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="移行の計画"
>abstract="Cloud Service への移行プロセスを開始する前に、AEM as a Cloud Service に習熟し、AEM as a Cloud Service に対する主要な変更点を確認すると共に、置換または廃止された機能も確認する必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja" text="ベストプラクティスアナライザー"

AEMas a Cloud Service移行ジャーニーのこのフェーズでは、AEMのas a Cloud Serviceについて理解し、導入された主な変更点を確認し、クラウドへの移行を成功に導くための計画に必要な事項を理解します。

## これまでの説明内容 {#story-so-far}

前のドキュメント [AEM as a Cloud Serviceへの移行の手引き](/help/journey-migration/getting-started.md)では、AEM as a Cloud Serviceに移行するために必要なフェーズのリストと、その利点について説明します。

## 目的 {#objective}

このドキュメントでは、AEMのインストールをクラウドに移行する準備ができていることを確認するために考慮する必要がある要因を理解するのに役立ちます。

* 主な変更点と廃止された機能について説明します
* AEM as a Cloud Serviceへの移行の計画方法を説明します。

## AEM as a Cloud Service Architecture の主な変更点の確認 {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。

これらの改善に加えて、AEM as a Cloud Serviceと比較して、AEMのオンプレミスインストールと Adobe Managed Services の間にいくつかの違いが導入されました。

次の表に示す項目のリストは、AEM as a Cloud Serviceへの移行に最も関連する変更のサブセットです。 主要な変更点の完全なリストは、こちらをご覧ください [ここ](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>変更点?</th>
    <th>参照</th>
    <th>重要な留意点</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>可変フィルターと不変フィルターを対応するパッケージに分割する</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=ja">AEMas a Cloud Serviceの主な変更点</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM AEM as a Cloud Serviceのプロジェクト構造</a></td>
    <td>AEM as a Cloud Serviceにデプロイできる単一のパッケージには、サブパッケージを含めることができます。主に、独自のパッケージに分けられた可変コンテンツと不変コンテンツを含めるために使用します。</td>
  </tr>
  <tr>
    <td>Repo Init </td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Apache Sling RepoInit ドキュメント</a></td>
    <td>repoinit スクリプトは、最初のノード構造、ユーザー、グループまたはサービスユーザーを作成することをお勧めします。 これらのスクリプトは、実行モードによってターゲット設定され、コードパッケージのデプロイメントによって管理可能なので、リポジトリの初期化タスクを柔軟に実行できます。</td>
  </tr>
  <tr>
    <td>カスタム実行モードは許可されていません</td>
    <td></td>
    <td>AEM as a Cloud Serviceで標準で提供されている実行モードのみがサポートされます。<br>追加の開発環境が追加されると、すべての開発環境が「開発」実行モードに結び付けられます。</td>
  </tr>
  <tr>
    <td>Cloud Manager パイプラインの実行は、をデプロイする唯一の方法です</td>
    <td></td>
    <td>AEM as a Cloud Serviceでは、/system/console へのアクセスは許可されていません。したがって、すべての OSGi 設定はコードの一部である必要があり、コードとしてデプロイする必要があります。<br>OSGi 設定は読み取り専用モードで使用でき、Cloud Manager を通じて開発者コンソールで表示できます</td>
  </tr>
  <tr>
    <td>レプリケーションエージェントは Sling コンテンツ配布で置き換えられます</td>
    <td></td>
    <td>レプリケーションエージェントの概念は、「コンテンツ配布を使用」に置き換えられます。 レプリケーションエージェントを利用したカスタマイズがある場合は、再設計する必要があります。<br>リバースレプリケーションはサポートされていません</td>
  </tr>
  <tr>
    <td>CRX/DE とパッケージマネージャー</td>
    <td></td>
    <td>CRX/DE は開発環境でのみ使用できます。<br>パッケージマネージャーにはすべてのオーサーインスタンスでアクセスできますが、デプロイされるパッケージには可変コンテンツのみを含める必要があります ( 例：/content または/conf)</td>
  </tr>
  <tr>
    <td>組み込み CDN と独自の CDN の取得</td>
    <td></td>
    <td>AEM as a Cloud Serviceには、ほとんどの使用例に最適化されたすべての環境の CDN が含まれます。<br>独自の CDN を設定したい場合、承認を得るには、Adobeサポートにリクエストを送信する必要があります。<br>承認されると、CDN は Fastly を指し、どの環境のAEMインスタンスを指すのではなくなります。</td>
  </tr>
  <tr>
    <td>長時間実行されているジョブ</td>
    <td></td>
    <td>コンテナで実行するAEMインスタンスがいつ来ても移動できるので、Sling スケジューラーや Cron ジョブなどの長時間実行されるジョブは実行しないでください。<br>これらの機能を再考して、Adobe I/Oにオフロードします。</td>
  </tr>
  <tr>
    <td>非同期操作に切り替え</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">非同期操作の設定</a></td>
    <td>環境の全体的なパフォーマンスを向上させるために、特定の操作が非同期モードで実行されます。 システムリソースが使用可能になると、非同期ジョブはキューに入れられ、実行されます。</td>
  </tr>
  <tr>
    <td>トークンベースの認証と統合戦略</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">サーバー側 API 用のアクセストークンの生成</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=ja#authentication">トークンベースの認証に関するチュートリアル</a></td>
    <td>AEM外のシステムがAEM内で HTTP 操作を実行しようとするのは一般的です。<br>推奨されるアプローチは、AEMでのパスワードを使用したローカルユーザー名の作成に依存するのではなく、ここで説明する戦略を実装することです。</td>
  </tr>
  <tr>
    <td>ファイル I/O/ディスク使用量</td>
    <td></td>
    <td>割り当てられるディスク容量と、コンテナ内のインスタンスの入れ替えが保証されないので、AEMインスタンスに接続されたディスクに書き込んだり読み取ったりする際に、ファイル I/O 操作を使用することはお勧めしません。</td>
  </tr>
  <tr>
    <td>DAM アセットの更新ワークフロー</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Asset Compute Service</a></td>
    <td>DAM アセットの更新ワークフローに含まれるメディア処理ステップが、Asset computeサービスに置き換えられました</td>
  </tr>
  <tr>
    <td>AEM as a Cloud Serviceでのアセットのアップロード方法とサポートされるワークフロープロセスステップ</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">API 比較のアップロードとサポートされる WF プロセスステップ</a></td>
    <td>AEM as a Cloud Serviceでは、アセットのアップロード中またはダウンロード中に、アセットがバイナリストレージに直接ストリーミングするか、バイナリストレージから直接ストリーミングします。</br>AEMaaCS では、一部のワークフロープロセスステップがサポートされていません。</td>
  </tr>
  <tr>
    <td>ワークフローランチャー</td>
    <td></td>
    <td>コードから、OOTB またはカスタム DAM アセットの更新ワークフローのいずれかをトリガーしているワークフローランチャーをすべて削除します。</br>AEM as a Cloud Serviceにアップロードされたアセットはすべて、アセット処理サービスによって処理されます。 カスタム手順については、 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> 後処理ワークフロー</a> 後処理ワークフローの設定方法を説明します。</td>
  </tr>
  <tr>
    <td>カスタムレンディション手順</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">処理プロファイル</a></td>
    <td>カスタムレンディション生成、画像変換、ビデオエンコーディングは、対応する処理プロファイルを作成して、アセット処理サービスにオフロードする必要があります。</td>
  </tr>
  <tr>
    <td>コンテンツの検索とインデックス作成</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">コンテンツの検索とインデックス作成の変更</a></td>
    <td>インデックスの基になる処理と、インデックスが開始されるタイミングに大きな変更があります。<br>デプロイするコードで Oak インデックスを管理する前に、Oak インデックスを完全に理解し、リファクタリングします。</td>
  </tr>
  <tr>
    <td>すべてのメンテナンスタスクが設定可能とは限りません</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEMas a Cloud Serviceメンテナンスタスク</a></td>
    <td>AEM as a Cloud Serviceでは、特定のメンテナンスタスクのみを設定できます。</td>
  </tr>
  <tr>
    <td>発行リポジトリに対する変更</td>
    <td></td>
    <td>/home 以下のものを除き、パブリッシュリポジトリに直接変更することはできません。 作成者に変更を加え、配布することを常にお勧めします。 すべてのコードと設定の変更は、対応する Cloud Manager パイプラインを通じてデプロイする必要があります。</td>
  </tr>
  <tr>
    <td>Dispatcher の設定とキャッシュ</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#content-delivery">クラウド内の Dispatcher</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">キャッシュ管理<br></td>
    <td>Dispatcher の設定は、特定の構造に従う必要があります。<br>設定は、コードの一部として管理され、Cloud Manager パイプラインを通じてデプロイする必要があります。</td>
  </tr>
  <tr>
    <td>バックアップと復元</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">AEMas a Cloud Serviceバックアップと復元</a></td>
    <td></td>
  </tr>
</tbody>
</table>

## 非推奨（廃止予定）の機能 {#deprecated-features}

アドビでは、製品の機能を絶えず評価して、常に下位互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

アドビでは、 [廃止された機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=ja#deprecated-features) を参照して、AEMas a Cloud ServiceExperience Managerで非推奨とマークされている機能について確認し、デプロイメントへの影響を確認してください。

## AEMのインストールのレビューの計画 {#review-planning}

AEM as a Cloud Serviceで導入された変更に慣れたら、既存のインストールのレビューを計画し、クラウドに移行するために必要な変更のレベルを測定するために、今度は既存のインストールのレビューを計画します。

次の図は、レビューフェーズで必要となる主な手順を示しています。

![画像](/help/journey-migration/assets/planning-phaseimg1.png)

次に、これらの各手順の意味を詳しく説明します。

### Cloud Service への対応準備状況の評価 {#assess-cloud-readiness}

最初の手順は、既存のAEMバージョンからCloud Serviceに移行する準備ができているかを評価し、AEM as a Cloud Serviceとの互換性を保つためにリファクタリングが必要な領域を決定することです。

移行プロセスで予想される作業レベルを決定するには、主な変更点および廃止される機能に照らした現在のAEMソースコードの包括的な評価を実施する必要があります。

結果の数は、タイムラインおよびプロジェクト全体の成功に直接影響します。 したがって、配信を計画したり、AEMのas a Cloud Service的なベストプラクティスに沿ってカスタマイズを行うために必要なデザインを変更するために必要な会話を開始したりする際に、可能な限り明確にすることをお勧めします。

**ベストプラクティスアナライザー**

現在のAEMバージョンに対してベストプラクティスアナライザーを実行すると、評価を高速化できます。 その仕組みを十分に理解することが、評価計画を迅速に立ち上げるための鍵となります。

その仕組みについては、 [ベストプラクティスアナライザー](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) ドキュメント。

**Cloud Readiness Assessment レポートの作成**

次のステップでは、これまでに得られたすべての知識に基づいてレポートを作成します。 これをおこなうには、ステージインスタンスと実稼動インスタンスからベストプラクティスアナライザーレポートを生成します。 [次に、Cloud Acceleration Manager にアップロードします](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) 可能性の高い項目に関する消化可能なレポートを

典型的なレポートには、次の入力情報が含まれます。

* 特定のAEMインストールの機能セットの詳細を説明するドキュメント
* AEMカスタム設定およびコードの詳細
* 実稼動 Dispatcher の設定
* CDN 設定（存在する場合）

**レポートをソーシャル化**

ベストプラクティスアナライザーレポートが完了したら、関連するチームと共有して、結果を確認し、次の手順の計画を立てます。 好みに応じて、 [印刷プレビュー](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### リソース計画のレビュー {#review-resource-planning}

Cloud Serviceへの移行に必要な作業レベルを推定したら、リソースを特定し、チームを作成し、移行プロセスに関する役割と責務をマッピングする必要があります。

### KPI の設定 {#establish-kpis}

主要業績評価指標 (KPI) をまだ設定していない場合は、AEMの実装に関する KPI を設定して、最も重要な項目にチームが専念できるようにすることをお勧めします。

詳しくは、 [KPI の開発](https://guided.adobe.com/welcome/aem/part6.html) ビジネス目標に合った適切な KPI を選択する方法を学ぶ

## 次のステップ {#what-is-next}

AEM as a Cloud Serviceへの移行に必要な変更の範囲を理解したら、次の手順に従います。 [コードとコンテンツクラウドの準備](/help/journey-migration/implementation.md) 実際に移行を実行する前に。

## その他のリソース {#additional-resources}

* [Cloud Acceleration Manager の概要](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Cloud Acceleration Manager を使用してクラウドへの移行を迅速におこなう方法に関する包括的なガイド
* [AEMas a Cloud Service:概要、アーキテクチャ、考え方の違い](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEMCloud Serviceホーム](/help/overview/home.md) -Experience Managerのas a Cloud Serviceドキュメントの概要については、まずこちらを参照してください。
* [AEMas a Cloud Serviceの概要](/help/overview/home.md)  — このガイドでは、導入、用語、アーキテクチャなど、Experience Manageras a Cloud Service の概要を説明します。
* [オンボーディング](/help/onboarding/home.md) — このガイドでは、Experience Manageras a Cloud Serviceの使用を開始する方法の概要を示します。この概要には、チームにアクセスして設定する方法などが含まれます
