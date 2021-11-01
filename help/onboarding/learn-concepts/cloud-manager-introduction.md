---
title: Cloud Manager とは
description: ここでは、Cloud Manager、Cloud Manager プログラム、環境について説明します。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: c206bc241bccf6f8a5bfb4946d6231f53438861a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 92%

---

# Cloud Manager の概要 {#intro-cloud-manager}

Cloud Manager は、AEM as a Cloud Service の必須コンポーネントであり、チームの単一のエントリポイントとして機能します。

エンタープライズ開発環境を持つ企業をサポートするために、AEM as a Cloud Service は、Cloud Manager とその専用 CI／CD パイプラインに完全に統合されています。これらのパイプラインは、徹底したテストを行い最高のコード品質を確保することで、優れたエクスペリエンスを提供することができます。

Cloud Manager は、ユーザーが AEM as a Cloud Service をすぐに使い始めることができるように、クラウドリソースや環境を作成する機能など、セルフサービス方式で利用を始めるために必要なあらゆる機能を備えています。このようにして、AEM 開発者は Cloud Manager を使用して Git リポジトリーにアクセスできます。開発チームは、Cloud Manager を使用して、セルフサービス方式で頻繁に変更内容をコミットすることができます。

システム管理者は、クラウドリソースを作成する個人や開発者からなる Cloud Manager チームの設定を担当します。エンタープライズチーム開発の設定で Cloud Manager がサポートを提供する方法については、[AEM as a Cloud Service のエンタープライズチーム開発の設定](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)を参照してください。

## Cloud Manager の概要ページへの移動 {#navigate-cloud-manager}

Cloud Manager にアクセスするには、次の手順に従います。

1. から Cloud Manager のログインページに直接移動します。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

   >[!NOTE]
   >今後の参照用として、Cloud Manager のランディングページに直接移動する際に役立つように、このページにブックマークを付けてください。

1. Cloud Manager の **プログラムと製品** 起動するページ **概要** ページ。

さらに、 Adobe Experience Cloudホームページから Cloud Manager のプログラムと製品ページに移動することもできます。 次の手順に従います。

1. [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) に直接移動し、Adobe ID を使用してログインします。

1. **Experience Manager** を選択します。

1. Cloud Manager カードの「**Launch**」をクリックします。
Cloud Manager に正常にログインすると、ユーザーインターフェイス（UI）を使用する準備が整います。

   正常にログインすると、Cloud Manager のランディングページが表示されます。

## Cloud Manager での役割ベースの権限 {#role-based-permissions}

| 権限 | 説明 | ビジネスオーナー | デプロイメントマネージャー | プログラムマネージャー | デベロッパー |
|--- |--- |--- |--- |--- |--- |
| プログラムを追加<br>プログラムを編集 | 新しいプログラムを追加<br>プログラムを編集 - ソリューションを追加／削除またはアドオンを追加 | x |  |  |  |
| 環境を作成 | 本番+ステージ、開発の各環境を作成 | x | x |  |  |
| 環境の更新 | 本番+ステージ、開発の各環境をアップデート | x | x |  |  |
| 開発環境を削除 | 開発環境を削除 | x | x |  |  |
| パイプラインを設定 | パイプラインを設定または編集 |  | x |  |  |
| パイプラインの実行 | パイプラインを開始 | x | x |  |  |
| パイプラインの実行 | 重大な 3 層エラーを却下／承認 | x | x | x |  |
| パイプラインの実行 | GoLive 承認を提供します。 | x | x | x |  |
| パイプラインの実行 | 実稼動環境へのデプロイメントのスケジュールを設定します。 | x | x | x |  |
| パイプラインの削除 | パイプラインの削除を許可 |  | x |  |  |
| 実行のキャンセル | 現在の実行をキャンセル |  | x |  |  |
| 個人用アクセストークンの生成 | Git にアクセスします。 |  | x |  | x |

>[!NOTE]
>1 人のユーザーを複数のロールに割り当てることができます。例えば、ビジネスオーナーとデプロイメントマネージャーの両方のロールをユーザーに割り当てると、これらの権限の組み合わせ（合計）が割り当てられます。

## Cloud Manager プログラム {#cloud-manager-programs}

Cloud Manager プログラムは、ビジネスイニシアチブの論理セットをサポートする Cloud Manager 環境セットであり、通常、購入したサービスレベル契約（SLA）に対応しています。例えば、あるプログラムが、グローバルなパブリック Web サイトをサポートする AEM リソースを表す一方で、別のプログラムは社内の中核的 DAM を表します。Cloud Manager プログラムの使用方法について詳しくは、こちらの[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)をご覧ください。

ユーザーは、**サンドボックス**&#x200B;または&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* *実稼動プログラム*&#x200B;が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。詳しくは、[実稼動プログラムの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=ja)を参照してください。

* *サンドボックスプログラム*は、通常、トレーニング、デモの実行、イネーブルメント、POC、ドキュメントの実行の目的で作成されます。ライブトラフィックを運ぶことを目的としたものではなく、実稼動プログラムにはない制限が課されます。Sites と Assets が含まれ、サンプルコード、開発環境、非実稼動パイプラインを含む Git ブランチが自動生成されて配信されます。
詳しくは、[サンドボックスプログラムの紹介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=ja)を参照してください。

## Cloud Manager 環境 {#cloud-manager-environments}

クラウド環境は、Cloud Manager で作成、アクセス、表示されます。これらは、実稼動環境、ステージング環境、開発環境のいずれかになります。環境が異なれば目的も異なり、環境のエンゲージメントに使用できる CI/CD パイプラインも異なります。環境は、次のようなサービスで構成されます。

* [AEM オーサーサービス](#author-services)
* [AEM パブリッシュサービス](#publish-services)
* [Dispatcher サービス](#dispatcher-services)

   >[!NOTE]
   > 使用可能な環境について詳しくは、[Adobe Cloud Manager の使用 - 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja#cloud-manager)のビデオを参照してください。また、作成可能な環境のタイプと環境の作成方法について詳しくは、[環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)を参照してください。

### AEM オーサーサービス {#author-services}

AEM オーサーサービスは、サイトコンテンツとデジタルアセットの作成、管理、更新を行う環境に含まれています。通常、オーサーサービスにアクセスできるのは内部ユーザーのみです。オーサーサービスはログイン画面の背後で動作しています。オーサーサービスは、オーサリング環境とプレビュー環境の両方として設計されています。

### AEM パブリッシュサービス {#publish-services}

AEM パブリッシュサービスは、Web サイトなどのエンドユーザーエクスペリエンスをホストする環境に含まれています。これは、サイト訪問者が表示して操作するサービスです。通常、パブリッシュサービスは公開されています。

### AEM Dispatcher サービス {#dispatcher-services}

Dispatcher は、セキュリティとパフォーマンスのレイヤーを提供する `Apache HTTP Web server` モジュールで、AEM パブリッシュサービスの前面に位置します。
