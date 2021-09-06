---
title: Cloud Managerについて説明します
description: このページでは、Cloud Manager、Cloud Managerのプログラム、環境について説明します。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: a21116e9ea59e608590151dc2682ff6e73dde9ed
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 36%

---

# Cloud Manager の概要 {#intro-cloud-manager}

Cloud Managerは、AEMのCloud Serviceとしての不可欠なコンポーネントで、チームの単一のエントリポイントとして機能します。

エンタープライズ開発の設定をおこなうお客様をサポートするために、AEM as aCloud ServiceはCloud Managerとその専用に構築されたCI/CDパイプラインに完全に統合され、優れたエクスペリエンスを提供するための徹底的なテストと最高のコード品質を保証します。

お客様がAEM as aCloud Serviceをすぐに使い始められるように、Cloud Managerは、クラウドのリソースや環境を作成する機能など、セルフサービス方式で開始するために必要なすべての機能を備えています。 この方法で、AEM開発者はCloud Managerを使用してGitリポジトリにアクセスできます。 開発チームは、Cloud Managerを使用して、セルフサービス方式で頻繁に変更をコミットするよう取り組むことができます。

システム管理者は、クラウドリソースおよび開発者を作成する個人を含むCloud Managerチームの設定を担当します。 エンタープライズチーム開発設定でのCloud Managerのサポート方法については、 AEM as aCloud Service向けの[エンタープライズチーム開発設定](/help/implementing/cloud-manager/enterprise-team-dev-setup.md)を参照してください。

## Cloud Managerの概要ページへの移動 {#navigate-cloud-manager}

次の手順に従って、Cloud Managerに移動します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)からCloud Managerのログインページに直接移動します。

   >[!NOTE]
   >今後の参照用に、またCloud Managerのランディングページに直接移動する際に役立つ情報については、このページをブックマークに追加してください。

1. Cloud Managerの&#x200B;**プログラムと製品**&#x200B;ページからプログラムを選択し、**概要**&#x200B;ページを起動します。

さらに、 Adobe Experience CloudのホームページからCloud Managerのプログラムと製品ページに移動することもできます。 次の手順に従います。

1. [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)に直接移動し、Adobe IDを使用してログインします。

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

Cloud Managerプログラムは、通常、購入したサービスレベル契約(SLA)に対応する、ビジネスイニシアチブの論理的なセットをサポートするCloud Manager環境のセットを表します。 例えば、あるプログラムは、グローバルなパブリックWebサイトをサポートするAEMリソースを表し、別のプログラムは、内部のCentral DAMを表します。 Cloud Managerプログラムの使用について詳しくは、この[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)をご覧ください。

ユーザーは、**サンドボックス**&#x200B;または&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* *実稼動プログラム*&#x200B;が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。詳しくは、[実稼動プログラムの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en)を参照してください。

* *サンドボックスプログラム*は、通常、トレーニング、デモの実行、イネーブルメント、POC、ドキュメントの実行の目的で作成されます。ライブトラフィックを運ぶことを目的としたものではなく、実稼動プログラムにはない制限が課されます。Sites と Assets が含まれ、サンプルコード、開発環境、非実稼動パイプラインを含む Git ブランチが自動生成されて配信されます。
詳しくは、[サンドボックスプログラムの紹介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en)を参照してください。

## Cloud Manager環境 {#cloud-manager-environments}

クラウド環境は、Cloud Managerを使用して作成、アクセスおよび表示されます。 実稼動環境、ステージ環境、または開発環境を指定できます。 環境が異なれば、サポートする目的も異なり、様々なCI/CDパイプラインを使用して関与できます。 環境は、次のようなサービスで構成されます。

* [AEMオーサーサービス](#author-services)
* [AEMパブリッシュサービス](#publish-services)
* [Dispatcherサービス](#dispatcher-services)

   >[!NOTE]
   > 使用可能な環境の詳細については、ビデオ[Using Using Cloud Manager Environments](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja#cloud-manager)を参照してください。 さらに、[環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)を参照して、ユーザーが作成できる環境のタイプと、ユーザーが環境を作成する方法について詳しく知ってください。

### AEMオーサーサービス {#author-services}

AEMオーサーサービスは、サイトコンテンツとデジタルアセットが作成、管理、更新される環境に含まれています。 通常、オーサーサービスにアクセスできるのは内部ユーザーのみで、ログイン画面の後ろにあります。 オーサリングサービスは、オーサリング環境とプレビュー環境の両方として設計されています。

### AEMパブリッシュサービス {#publish-services}

AEMパブリッシュサービスは、Webサイトなどのエンドユーザーエクスペリエンスをホストする環境に含まれます。 これは、サイト訪問者が表示し、操作するサービスです。 通常、パブリッシュサービスは公開されています。

### AEM Dispatcherサービス {#dispatcher-services}

Dispatcherは、AEMパブリッシュサービスの前に配置されるセキュリティとパフォーマンスのレイヤーを提供する`Apache HTTP Web server`モジュールです。
