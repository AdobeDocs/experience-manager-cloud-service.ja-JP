---
title: 開発者およびデプロイメントマネージャーのタスク
description: システム管理者が必要なクラウドリソースを設定したので、開発者とデプロイメントマネージャーが Git にアクセスしてアプリケーションを開発し、パイプラインを使用してデプロイする方法を説明します。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1397'
ht-degree: 100%

---


# 開発者およびデプロイメントマネージャーのタスク {#developer-deployment-manager}

[オンボーディングジャーニー](overview.md)のこのオプションのパートでは、開発者とデプロイメントマネージャーが Git にアクセスしてアプリケーションを開発し、パイプラインを使用してデプロイする方法を説明します。

## これまでの説明内容 {#story-so-far}

オンボーディングジャーニーで長い道のりを歩んできました。おめでとうございます。システム管理者は、必要なクラウドリソースを設定し、[AEM 製品プロファイルの割り当て](assign-profiles-aem.md)のドキュメントでアクセス権を付与することで、オンボーディングジャーニーを完了しました。

この時点で、開発者とデプロイメントマネージャーは独自のアプリケーションの作成を開始でき、AEM ユーザーはコンテンツの作成を開始できます。つまり、オンボーディングは完了し、新しい AEM as a Cloud Service システムを使用できるようになりました。その方法について、このドキュメントで説明します。

## 対象読者 {#audience}

このドキュメントは、**開発者**&#x200B;および&#x200B;**デプロイメントマネージャー**&#x200B;の視点で作成されています。

システム管理者も同じタスクを実行できますが、通常、これらの役割は別のユーザーが担当します。

## 目的 {#objective}

このドキュメントは、オンボーディングジャーニーの補足であり、システム管理者がすべてのユーザーをオンボーディングして必要なクラウドリソースを作成した後の、開発者とデプロイメントマネージャーの基本的なタスクを示すものです。

このドキュメントを読み終えると、次をできるようになります。

* 開発者として、Cloud Manager Git リポジトリにアクセスして管理する方法を理解する。
* デプロイメントマネージャーとして、Cloud Manager でパイプラインを設定し、コードをデプロイできるようになる。

## 開発者およびデプロイメントマネージャー {#roles}

システム管理者がユーザーの作成とクラウドリソースの設定という主なオンボーディングタスクを完了すると、一般に、システムへのアクセスを最も必要とするユーザーは開発者とデプロイメントマネージャーになります。 これは、AEM as a Cloud Service 上にカスタムアプリケーションを構築する責任を負うユーザーであるためです。

* **開発者** - これらのユーザーは、AEM カスタムアプリケーションのコードを管理する Cloud Manager Git リポジトリにアクセスします。
* **デプロイメントマネージャー** - これらのユーザーは、Cloud Manager を使用して、コードを Git リポジトリから実行中の AEM 環境にデプロイするパイプラインを作成および実行します。

組織のニーズに応じて、同じユーザーが両方の役割を持つことができます。

## 前提条件 {#prerequisites}

開発者またはデプロイメントマネージャーは、このドキュメントで説明するタスクを開始する前に、システム管理者がこのオンボーディングジャーニーのすべての手順を完了していることを確認してください。以下の手順です。

* システム管理者が、開発者とデプロイメントマネージャーをそれぞれの製品プロファイルに割り当てている。
* また、AEM を使用するためには、開発者を **AEM ユーザー**&#x200B;または **AEM 管理者**&#x200B;製品プロファイルに追加で割り当てる必要があります。
* クラウドリソースが設定されている。

## Git へのアクセス {#accessing-git}

Cloud Manager でセルフサービスの Git アカウント管理を使用すると、Git リポジトリにアクセスして管理できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**リポジトリ情報にアクセス**」ボタンを見つけて、Git リポジトリにアクセスして管理します。

   ![環境カードの「リポジトリ情報にアクセス」ボタン](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 「**リポジトリ情報を表示**」ボタンをクリックして、以下を表示するダイアログを開きます。

   * Cloud Manager Git リポジトリへの URL。
   * Git ユーザー名。
   * Git パスワード。この値は、「**パスワードを生成**」ボタンをクリックすると表示されます。

   ![リポジトリ情報](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

これらの資格情報を使用して、リポジトリのローカルコピーを複製し、そのローカルリポジトリで変更を加えることができます。変更できたら、Cloud Manager のリモートコードリポジトリにコードの変更をコミットして戻すことができます。

## パイプラインの設定 {#setup-pipeline}

開発者が Git リポジトリにカスタムコードを追加すると、デプロイメントマネージャーはパイプラインを作成して実行し、そのコードを AEM 環境にデプロイできます。

次の手順に従って、最初の実稼動以外のデプロイメントパイプラインを作成します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. Cloud Manager のホーム画面から&#x200B;**パイプライン**&#x200B;カードにアクセスします。「**+追加**」をクリックし、「**実稼動以外のパイプラインを追加**」を選択します。

   ![実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**設定**」タブで、追加する実稼動以外のパイプラインのタイプを選択します。この例では、「**デプロイメントパイプライン**」を選択します。

   ![実稼動以外のパイプラインを追加ダイアログ](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. **実稼動以外のパイプライン名**&#x200B;を指定して、次の追加情報と共にパイプラインを特定します。

1. **デプロイメントトリガー**&#x200B;で「**手動**」を選択して、開始時にのみパイプラインが実行されるようにします。

1. 「**続行**」をクリックします。

1. **実稼動以外のパイプラインを追加**&#x200B;ダイアログの「**ソースコード**」タブで、パイプラインが処理するコードのタイプを選択する必要があります。この例では、「**フルスタックコード**」を選択します。

1. 「**ソースコード**」タブで、次のオプションを定義する必要があります。

   * **適格なデプロイメント環境** - パイプラインのデプロイ先となる環境を選択する必要があります。
   * **リポジトリ** - このオプションでは、パイプラインがコードを取得する Git リポジトリを定義します。
   * **Git ブランチ** - このオプションでは、選択したパイプラインのどのブランチからコードを取得するかを定義します。
      * ブランチ名の最初の数文字を入力すると、このフィールドのオートコンプリート機能により、一致するブランチが検索され、選択の助けになります。

   ![フルスタックパイプライン](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 「**保存**」をクリックします。

これで、最初のパイプラインを作成できました。デプロイメントマネージャーの役割を持つユーザーは、Cloud Manager UI からパイプラインを開始できるようになりました。

## デプロイ {#deploy}

開発者がカスタムコードを Git リポジトリに追加し、デプロイメントマネージャーがそのコードをデプロイするためのパイプラインを作成したので、パイプラインを実行して、そのコードを Git からご利用の環境に実際に移動します。

![Cloud Manager のパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 「**プログラムの概要**」ページから&#x200B;**パイプライン**&#x200B;カードに移動し、前のセクションで作成したパイプラインの横にある省略記号ボタンをクリックして、メニューで「**実行**」を選択します。

1. パイプラインの実行が開始され、「**ステータス**」列に示されます。

実行の詳細を確認するには、省略記号ボタンをもう一度クリックし、「**詳細を表示**」を選択します。

おめでとうございます。これで、Git リポジトリから実稼動以外の環境にコードをデプロイしました。

## 次のステップ {#whats-next}

このドキュメントを読み終えたので、次のことをできるようになりました。

* 開発者として、Cloud Manager Git リポジトリにアクセスして管理する方法を理解する。
* デプロイメントマネージャーとして、Cloud Manager でパイプラインを設定し、コードをデプロイできるようになる。

開発者またはデプロイメントマネージャーとして、Cloud Manager の実務知識だけでなく、作業環境、リポジトリ、パイプラインを使用して作業に取りかかれるようになりました。ただし、AEM as a Cloud Service の強力な CI/CD ツールについて学ぶべきことは他にもあります。詳しくは、[その他のリソース](#additional-resources)のセクションを参照してください。

コンテンツ作成者がどのようにして AEM as a Cloud サービスにアクセスして使用できるかに関心がある方は、オンボーディングジャーニーの最後のパートである [AEM ユーザータスク](aem-users.md)に進んでください。

>[!TIP]
>
>オンボーディングした後は、最小限の AEM 構成でサンドボックス環境に [AEM Reference Demos Add-On を簡単に追加する方法を学ぶ](/help/journey-sites/demos-add-on/overview.md) ことができ、ベストプラクティスに基づいた豊富な例を使用して AEM の強力な機能をテストできます。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えてさらに詳しく知りたい場合に役立つ、追加のオプションリソースを次に示します。

* [リポジトリへのアクセス](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Cloud Manager でセルフサービスの Git アカウント管理を使用して、Git リポジトリにアクセスして管理する方法について説明します。
* [Cloud Manager での Git の使用](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Cloud Manager の Git リポジトリを使用する方法と、オンプレミスで顧客管理された独自の Git リポジトリを Cloud Manager と統合する方法について説明します。
* [ローカル開発環境の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=ja) - このチュートリアルでは、AEM as a Cloud Service SDK を使用して Adobe Experience Manager（AEM）用のローカル開発環境を設定する手順について説明します。
* [AEM Sites の概要 - WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja) - 複数パートから成るこのチュートリアルは、Adobe Experience Manager（AEM）を初めて使用する開発者向けに設計されています。このチュートリアルでは、架空のライフスタイルブランド WKND の AEM Sites の実装について説明します。このチュートリアルでは、Adobe Experience Manager Sites を使用したプロジェクトの設定、コアコンポーネント、編集可能なテンプレート、クライアントサイドライブラリ、コンポーネント開発などの基本的なトピックについて説明します。
* [React を使用した AEM での SPA の概要](/help/implementing/developing/hybrid/getting-started-react.md) - この記事では、サンプルの SPA アプリケーションとその組み立てについて紹介します。また、React フレームワークを使用して独自の SPA の運用を速やかに開始する方法についても説明します。
* [Angular を使用した AEM での SPA の概要](/help/implementing/developing/hybrid/getting-started-angular.md) - この記事では、サンプルの SPA アプリケーションとその組み立てについて紹介します。また、Angular フレームワークを使用して独自の SPA の運用を速やかに開始する方法についても説明します。
* [ヘッドレス開発者ジャーニー](/help/journey-headless/developer/overview.md) - AEMでヘッドレスアプリケーションを開発する際のガイド付きコースについては、ここから始めてください。
