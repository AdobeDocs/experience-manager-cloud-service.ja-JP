---
title: Cloud Manager の概要
description: Cloud Manager のプログラム、環境、パイプラインを通じてAEMプロジェクトを Cloud Manager がサポートする方法について説明します。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 26%

---

# Cloud Manager の概要 {#intro-cloud-manager}

Cloud Manager は、AEM as a Cloud Service の必須コンポーネントであり、チームの単一のエントリポイントとして機能します。専用の CI/CD パイプラインが装備され、徹底したテストと最高のコード品質が実現し、優れたエクスペリエンスを提供します。 顧客がすばやくプロジェクトを開始できるように、Cloud Manager は、クラウドのリソースと環境を作成し、Git リポジトリにアクセスする機能など、セルフサービス方式で必要なすべてを提供します。 これらの機能は、企業の開発の設定をサポートし、チームは頻繁に変更をコミットし、優れたデジタルエクスペリエンスを迅速に提供し、価値創出までの時間を短縮できます。

システム管理者は、クラウドリソースおよび開発者を作成する個人を含む Cloud Manager チームを設定する必要があります。 エンタープライズ開発チームの設定と拡張の方法、およびAEMas a Cloud Serviceが開発プロセスをサポートする方法について詳しくは、このドキュメントを参照してください [AEM as a Cloud Service向けエンタープライズチーム開発設定](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## Cloud Manager の概要ページへの移動 {#navigate-cloud-manager}

Cloud Manager に移動するには、次の手順に従います。

1. Cloud Manager のログインページ ( ) に移動します。 [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Cloud Manager の **プログラムと製品** 起動するページ **概要** ページ。

次の手順に従うことで、Adobe Experience Cloudのホームページから Cloud Manager のプログラムと製品ページに移動することもできます。

1. Adobe Experience Cloud( ) に移動します。 [`https://experience.adobe.com`](https://experience.adobe.com) Adobe IDを使用してログインします。

1. ツールバーの右上に表示される組織名を参照して、正しい組織に属していることを確認します。

1. **Experience Manager** を選択します。

1. の **Cloud Manager** カード、クリック **起動**

## Cloud Manager での役割ベースの権限 {#role-based-permissions}

| 権限 | 説明 | ビジネスオーナー | デプロイメントマネージャー | プログラムマネージャー | デベロッパー |
|--- |--- |--- |--- |--- |--- |
| プログラムを追加<br>プログラムを編集 | 新しいプログラムの追加<br>ソリューションまたはアドオンの追加または削除 | x |  |  |  |
| 環境を作成 | 実稼動環境とステージング環境および開発環境の作成 | x | x |  |  |
| 環境の更新 | 実稼動環境とステージング環境および開発環境の更新 | x | x |  |  |
| 開発環境を削除 | 開発環境の削除 | x | x |  |  |
| パイプラインを設定 | パイプラインの設定と編集 |  | x |  |  |
| パイプラインの実行 | パイプラインを開始 | x | x |  |  |
| パイプラインの実行 | 重要な 3 層品質ゲートエラーの拒否/承認 | x | x | x |  |
| パイプラインの実行 | 運用開始の承認を提供 | x | x | x |  |
| パイプラインの実行 | 実稼動デプロイメントのスケジュール設定 | x | x | x |  |
| パイプラインの削除 | パイプラインの削除を許可 |  | x |  |  |
| 実行のキャンセル | 現在の実行をキャンセル |  | x |  |  |
| 個人用アクセストークンの生成 | Git にアクセス |  | x |  | x |

>[!NOTE]
>
>1 人のユーザーを複数のロールに割り当てることができます。例えば、 **ビジネスオーナー** および **デプロイメントマネージャー** ユーザーに対する役割は、ユーザーにこれらの権限の合計を提供します。

## Cloud Manager プログラム {#cloud-manager-programs}

Cloud Manager プログラムは、ビジネスイニシアチブの論理的なグループをサポートする、Cloud Manager 環境のセットを表します。 これらのグループは通常、購入したサービスレベル契約 (SLA) に対応しています。 例えば、あるプログラムは組織のパブリック Web サイトをサポートするAEMリソースを表し、別のプログラムは内部 DAM を表す場合があります。


Cloud Manager プログラムの使用方法について詳しくは、こちらの[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)をご覧ください。

ユーザーは、**サンドボックス**&#x200B;または&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* A **生産計画** は、将来の適切な時間にライブトラフィックを有効にするために作成されます。
   * 詳しくは、[実稼動プログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)のドキュメントを参照してください。

* A **サンドボックスプログラム** は、通常、トレーニング、デモの実行、イネーブルメント、POC の作成またはドキュメントの目的で作成されます。
   * ライブトラフィックを運ぶためのものではなく、実稼動プログラムが運ぶことを制限します。
   * Sites と Assets が含まれ、サンプルコード、開発環境、実稼動以外のパイプラインを含む Git ブランチが自動入力されて配信されます。
   * 詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)のドキュメントを参照してください。

## Cloud Manager 環境 {#cloud-manager-environments}

クラウド環境は、Cloud Manager で作成、アクセス、表示されます。これらの環境は、実稼動環境、ステージング環境または開発環境にすることができます。 環境が異なれば、目的も異なり、CI/CD パイプラインで使用できます。 環境は、次のようなサービスで構成されます。

* [AEM Authoring Services](#author-services)
* [AEM Publishing Services](#publish-services)
* [Dispatcher サービス](#dispatcher-services)

>[!TIP]
>
> ビデオを参照してください。 [AdobeCloud Manager 環境の使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja) 使用可能な環境の概要。
>
>ドキュメントを参照します。 [環境の管理](/help/implementing/cloud-manager/manage-environments.md) ユーザーが作成できる環境のタイプと、環境の作成方法について詳しく説明します。

### AEM Authoring Service {#author-services}

AEMオーサリングサービスは、サイトコンテンツやデジタルアセットが作成、管理、更新される環境に含まれています。 通常、オーサリングサービスにアクセスできるのは内部ユーザーのみで、ログイン画面の後ろで維持されます。 オーサリングサービスは、オーサリング環境とプレビュー環境の両方で機能します。

### AEM Publishing Service {#publish-services}

AEMパブリッシュサービスは、Web サイトなど、エンドユーザーエクスペリエンスをホストする環境に含まれます。 これは、サイト訪問者が表示して操作するサービスです。通常、公開サービスを利用できます。

### AEM Dispatcher サービス {#dispatcher-services}

Dispatcher は `Apache HTTP Web server` AEMパブリッシュサービスの前に配置されるセキュリティおよびパフォーマンスレイヤーを提供するモジュール。
