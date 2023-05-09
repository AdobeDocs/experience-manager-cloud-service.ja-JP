---
title: Cloud Manager の概要
description: プログラム、環境、パイプラインを通じて、Cloud Manager がどのように AEM プロジェクトをサポートするかについて説明します。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 33d587baba27ad54b1c9e34a36fadbd1dc56e3f5
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 100%

---

# Cloud Manager の概要 {#intro-cloud-manager}

Cloud Manager は、AEM as a Cloud Service に不可欠なコンポーネントであり、チームにとって単一のエントリポイントとして機能します。専用の CI/CD パイプラインが装備され、徹底したテストと最高のコード品質が実現し、優れたエクスペリエンスを提供します。顧客がすばやくプロジェクトを開始できるように、Cloud Manager は必要なものをすべてセルフサービス方式で提供します。これには、クラウドのリソースと環境を作成し、Git リポジトリにアクセスする機能も含まれます。これらの機能で企業の開発体制をサポートすることにより、チームは頻繁に変更をコミットし、優れたデジタルエクスペリエンスを迅速に提供し、価値創出までの時間を短縮できるようになります。

システム管理者は、クラウドリソースを作成する人や開発者からなる Cloud Manager チームの構築を担当します。企業の開発チームの構築と拡張の方法や、AEM as a Cloud Service で開発プロセスをサポートする方法について詳しくは、[AEM as a Cloud Service 向けエンタープライズ開発チームの構築](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)のドキュメントを参照してください。

## Cloud Manager の概要ページへの移動 {#navigate-cloud-manager}

次の手順に従って、 Cloud Manager に移動します。

1. Cloud Manager のログインページ（[`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/)）に移動します。

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページでプログラムを選択して、**概要**&#x200B;ページを起動します。

次の手順に従って、Adobe Experience Cloud のホームページから Cloud Manager のプログラムと製品ページに移動することもできます。

1. Adobe Experience Cloud（[`https://experience.adobe.com`](https://experience.adobe.com)）に移動し、Adobe ID を使用してログインします。

1. ツールバーの右上に表示される組織名を参照して、正しい組織に属していることを確認します。

1. **Experience Manager** を選択します。

1. **Cloud Manager** カードで、「**起動**」をクリックします。

## Cloud Manager での役割ベースの権限 {#role-based-permissions}

| 権限 | 説明 | ビジネスオーナー | デプロイメントマネージャー | プログラムマネージャー | デベロッパー |
|--- |--- |--- |--- |--- |--- |
| プログラムを追加<br>プログラムを編集 | 新しいプログラムの追加<br>ソリューションまたはアドオンの追加または削除 | x |  |  |  |
| 環境を作成 | 実稼動とステージング環境および開発環境の作成 | x | x |  |  |
| 環境の更新 | 実稼動とステージング環境および開発環境の更新 | x | x |  |  |
| 開発環境を削除 | 開発環境の削除 | x | x |  |  |
| パイプラインを設定 | パイプラインの設定と編集 |  | x |  |  |
| パイプラインの実行 | パイプラインの開始 | x | x |  |  |
| パイプラインの実行 | 重要な 3 層品質ゲートエラーの拒否/承認 | x | x | x |  |
| パイプラインの実行 | 運用開始の承認の提供 | x | x | x |  |
| パイプラインの実行 | 実稼動デプロイメントのスケジュール設定 | x | x | × |  |
| パイプラインの削除 | パイプラインの削除の許可 |  | x |  |  |
| 実行のキャンセル | 現在の実行のキャンセル |  | x |  |  |
| 個人用アクセストークンの生成 | Git へのアクセス |  | x |  | x |
| RDE を作成 | 迅速な開発環境の作成 | x |  |  | x |
| RDE をリセット | 迅速な開発環境のリセット | x |  |  | x |

>[!NOTE]
>
>1 人のユーザーを複数の役割に割り当てることができます。例えば、**ビジネスオーナー**&#x200B;と&#x200B;**デプロイメントマネージャー**&#x200B;の両方の役割をユーザーに割り当てると、これらを足し合わせた権限がユーザーに付与されます。

## Cloud Manager プログラム {#cloud-manager-programs}

Cloud Manager プログラムは、ビジネスイニシアチブの論理的なグループをサポートする一連の Cloud Manager 環境を表します。これらのグループは、通常、購入したサービスレベル契約（SLA）に対応しています。例えば、あるプログラムは組織の公開 web サイトをサポートする AEM リソースを表し、別のプログラムは社内の DAM を表しているかもしれません。


Cloud Manager プログラムの使用方法について詳しくは、こちらの[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)をご覧ください。

ユーザーは、**サンドボックス**&#x200B;プログラムまたは&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* **実稼動プログラム**&#x200B;は、将来の適切なタイミングで実トラフィックを扱えるように作成されます。
   * 詳しくは、[実稼動プログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)のドキュメントを参照してください。

* **サンドボックスプログラム**&#x200B;は、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されます。
   * 実トラフィックを流すことを目的としたものではなく、実稼働プログラムにはない制限があります。
   * Sites と Assets が含まれており、サンプルコード、開発環境および実稼動以外のパイプラインを含む Git ブランチが自動入力されて提供されます。
   * 詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)のドキュメントを参照してください。

## Cloud Manager 環境 {#cloud-manager-environments}

クラウド環境は、Cloud Manager で作成、アクセス、表示されます。これらの環境は、実稼動環境、ステージング環境または開発環境にすることができます。環境が異なれば目的も異なり、異なる CI/CD パイプラインで使用できます。環境は、次のようなサービスで構成されます。

* [AEM オーサーサービス](#author-services)
* [AEM パブリッシュサービス](#publish-services)
* [Dispatcher サービス](#dispatcher-services)

>[!TIP]
>
> 使用可能な環境の概要については、[Adobe Cloud Manager 環境の使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja)のビデオを参照してください。
>
>ユーザーが作成できる環境のタイプと、ユーザーが環境を作成する方法について詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)のドキュメントを参照してください。

### AEM オーサーサービス {#author-services}

AEM オーサーサービスは、サイトコンテンツとデジタルアセットの作成、管理、更新を行う環境に含まれています。通常、オーサーサービスにアクセスできるのは内部ユーザーのみです。オーサーサービスはログイン画面の背後で動作しています。オーサーサービスは、オーサリング環境とプレビュー環境の両方で機能します。

### AEM パブリッシュサービス {#publish-services}

AEM パブリッシュサービスは、web サイトなどのエンドユーザーエクスペリエンスをホストする環境に含まれています。これは、サイト訪問者が表示して操作するサービスです。通常、パブリッシュサービスは公開されています。

### AEM Dispatcher サービス {#dispatcher-services}

Dispatcher は、セキュリティとパフォーマンスのレイヤーを提供する `Apache HTTP Web server` モジュールで、AEM パブリッシュサービスの前面に位置します。
