---
title: 開発者およびデプロイメントマネージャーのタスク
description: システム管理者が必要なクラウドリソースを設定したら、開発者とデプロイメントマネージャーが Git にアクセスしてアプリケーションを開発し、パイプラインを使用してデプロイする方法を学びます。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 17%

---


# 開発者およびデプロイメントマネージャーのタスク {#developer-deployment-manager}

このオプションの部分は、 [オンボーディングジャーニー](overview.md) 開発者とデプロイメントマネージャーが git にアクセスしてアプリケーションを開発し、パイプラインを使用してデプロイする方法を学びます。

## これまでの説明内容 {#story-so-far}

オンボーディングジャーニーの道のりはずいぶん遠くにきたぞ！ おめでとうございます。システム管理者は、必要なクラウドリソースを設定し、ドキュメント内でアクセス権を付与することで、オンボーディングジャーニーを完了しました [AEM製品プロファイルの割り当て](assign-profiles-aem.md)

この時点で、開発者およびデプロイメントマネージャーは、独自のアプリケーションの作成を開始できますが、AEMユーザーはコンテンツの作成を開始できます。 この意味で、オンボーディングは完了し、今、新しいAEMas a Cloud Serviceシステムを使用する時です。このドキュメントでは、このドキュメントで説明します。

## 対象読者 {#audience}

この文書は、 **開発者** および **デプロイメントマネージャー**.

システム管理者も同じタスクを実行できますが、通常、これらの役割は異なるユーザーが持ちます。

## 目的 {#objective}

このドキュメントは、オンボーディングジャーニーの補足事項で、システム管理者がすべてのユーザーをオンボーディングして必要なクラウドリソースを作成した後に、開発者とデプロイメントマネージャーの基本的なタスクを示します。

読み終えると、次のことができるようになります。

* デベロッパーは、Cloud Manager の Git リポジトリにアクセスして管理する方法を理解します。
* デプロイメントマネージャーは、パイプラインを設定して Cloud Manager にコードをデプロイできます。

## 開発者およびデプロイメントマネージャー {#roles}

システム管理者がユーザーの作成とクラウドリソースの設定の主なオンボーディングタスクを完了すると、一般に、システムへのアクセスを最も強く望むのは開発者とデプロイメントマネージャーです。 これは、AEM as a Cloud Service上でカスタムアプリケーションを構築する責任を持つユーザーであるためです。

* **開発者**  — これらのユーザーは、AEMカスタムアプリケーションのコードを管理する Cloud Manager Git リポジトリーにアクセスします。
* **デプロイメントマネージャー**  — これらのユーザーは、Cloud Manager を使用して、git リポジトリーから実行中のAEM環境にコードをデプロイするパイプラインを作成および実行します。

組織のニーズに応じて、同じユーザーが両方の役割を持つことができます。

## 前提条件 {#prerequisites}

このドキュメントで説明するタスクを開始する前に、開発者またはデプロイメントマネージャーとしてシステム管理者がこのオンボーディングジャーニーのすべての手順を完了していることを確認してください。 つまり、

* システム管理者が、開発者およびデプロイメントマネージャーをそれぞれの製品プロファイルに割り当てています。
* 開発者は、 **AEM Users** または **AEM Administrators** AEMも使用するための製品プロファイルを作成します。
* クラウドリソースが設定されました。

## Git へのアクセス {#accessing-git}

Cloud Manager のセルフサービス Git アカウント管理を使用して、Git リポジトリーにアクセスし、管理できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. に移動します。 **パイプライン** カードから **プログラムの概要** ページで **リポジトリ情報にアクセス** ボタンをクリックして、git リポジトリにアクセスして管理します。

   ![環境カードの「リポジトリ情報」ボタンにアクセス](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. をクリックします。 **リポジトリ情報を表示** ボタンをクリックして、表示するダイアログを開きます。

   * Cloud Manager の Git リポジトリの URL です。
   * Git のユーザー名。
   * git パスワード。この値は、 **パスワードを生成** 」ボタンがクリックされたときに表示されます。

   ![リポジトリ情報](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

ユーザーは、これらの資格情報を使用して、リポジトリのローカルコピーを複製し、そのローカルリポジトリで変更を加えることができます。準備が整ったら、Cloud Manager のリモートコードリポジトリにコードの変更をコミットして戻すことができます。

## パイプラインを設定 {#setup-pipeline}

開発者が Git リポジトリにカスタムコードを追加すると、デプロイメントマネージャーはパイプラインを作成して実行し、そのコードをAEM環境にデプロイできます。

次の手順に従って、最初の非実稼動デプロイメントパイプラインを作成します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。「**+追加**」をクリックし、「**実稼動以外のパイプラインを追加**」を選択します。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. の **設定** タブ **実稼動以外のパイプラインを追加** ダイアログで、追加する非実稼動パイプラインのタイプを選択します。 この例では、「 **デプロイメントパイプライン**.

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. **実稼動以外のパイプライン名**&#x200B;を指定して、次の追加情報と共にパイプラインを特定します。

1. の **デプロイメントトリガー** 選択 **手動** したがって、パイプラインは開始時にのみ実行されます。

1. 「**続行**」をクリックします。

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**ソースコード**」タブで、パイプラインが処理するコードのタイプを選択する必要があります。この例では、「 **フルスタックコード**.

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境**  — パイプラインのデプロイ先となる環境を選択する必要があります。
   * **リポジトリ** - このオプションは、パイプラインがコードを取得する Git リポジトリを定義します。
   * **Git ブランチ** - このオプションは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択に役立ちます。

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

これで、最初のパイプラインが作成されました。 デプロイメントマネージャーの役割を持つユーザーは、Cloud Manager UI からパイプラインを開始できるようになりました。

##  のデプロイ {#deploy}

開発者がカスタムコードを Git リポジトリに追加し、そのコードをデプロイするためのパイプラインを作成したので、パイプラインを実行して、そのコードを Git から環境に実際に移動します。

![Cloud Manager のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページに移動し、前のセクションで作成したパイプラインの横の省略記号ボタンをクリックし、「 」を選択します。 **実行** を選択します。

1. パイプラインの実行が開始され、「**ステータス**」列に示されます。

実行の詳細を確認するには、省略記号ボタンをもう一度クリックし、「 」を選択します。 **詳細を表示**.

おめでとうございます。これで、Git リポジトリから実稼動以外の環境にコードをデプロイしました。

## 次の手順 {#whats-next}

このドキュメントを読んだら、次の操作を行う必要があります。

* デベロッパーは、Cloud Manager の Git リポジトリにアクセスして管理する方法を理解します。
* デプロイメントマネージャーは、パイプラインを設定して Cloud Manager にコードをデプロイできます。

Cloud Manager に関する実務知識だけでなく、作業環境、リポジトリ、パイプラインに関する実務知識も持つ開発者またはデプロイメントマネージャーとして実行されている状況が発生しました。 AEM as a Cloud Serviceの強力な CI/CD ツールについて詳しく説明します。 以下を確認します。 [その他のリソース](#additional-resources) 」の節を参照してください。

コンテンツ作成者がAEM as a Cloud Service にアクセスして使用する方法に興味がある場合は、オンボーディングジャーニーの最後の部分に進みます。 [AEMユーザータスク。](aem-users.md)

>[!TIP]
>
>オンボーディングした後は、最小限の AEM 構成でサンドボックス環境に [AEM Reference Demos Add-On を簡単に追加する方法を学ぶ](/help/journey-sites/demos-add-on/overview.md) ことができ、ベストプラクティスに基づいた豊富な例を使用して AEM の強力な機能をテストできます。

## その他のリソース {#additional-resources}

* [リポジトリへのアクセス](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Cloud Manager のセルフサービス Git アカウント管理を使用して、Git リポジトリにアクセスし、管理する方法について説明します。
* [Cloud Manager での git の使用](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
* [ローカル開発環境の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=ja)  — このチュートリアルでは、AEMas a Cloud ServiceSDK を使用してAdobe Experience Manager(AEM) 用のローカル開発環境をセットアップする手順を説明します。
* [AEM Sites使用の手引き — WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)  — この複数パートのチュートリアルは、Adobe Experience Manager(AEM) を初めて使用する開発者向けに設計されています。 このチュートリアルでは、架空のライフスタイルブランド WKND 向けのAEMサイトの実装について説明します。 このチュートリアルでは、プロジェクトの設定、コアコンポーネント、編集可能テンプレート、クライアント側ライブラリ、Adobe Experience Manager Sitesでのコンポーネント開発など、基本的なトピックについて説明します。
* [React を使用したAEMでのSPAの概要](/help/implementing/developing/hybrid/getting-started-react.md)  — この記事では、サンプルのSPAアプリケーションを紹介し、その設定方法を説明し、React フレームワークを使用して独自のSPAをすぐに使い始める方法について説明します。
* [AEMのSPA使用の手引きAngular](/help/implementing/developing/hybrid/getting-started-angular.md)  — この記事では、サンプルのSPAアプリケーションを紹介し、その設定方法を説明し、Angularフレームワークを使用して独自のSPAをすぐに使い始める方法を説明します。
* [ヘッドレス開発者ジャーニー](/help/journey-headless/developer/overview.md) - AEMでヘッドレスアプリケーションを開発する際のガイド付きコースについては、ここから始めてください。
