---
title: カスタマイズしたテーマのデプロイ
description: パイプラインを使用してサイトテーマをデプロイする方法を説明します。
source-git-commit: 97c7590fd7b77e78cf2d465454fac80906d37803
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 7%

---


# カスタマイズしたテーマのデプロイ {#deploy-your-customized-theme}

パイプラインを使用してサイトテーマをデプロイする方法を説明します。

## これまでの説明内容 {#story-so-far}

前のドキュメントのAEM Quick Site Creation ジャーニーでは、 [サイトテーマのカスタマイズ](customize-theme.md) テーマの構築方法、テーマのカスタマイズ方法、ライブAEMコンテンツを使用したテスト方法を学び、次の操作を行う必要があります。

* サイトテーマの基本構造と編集方法を理解します。
* ローカルプロキシを介した実際のAEMコンテンツを使用したテーマのカスタマイズのテスト方法を参照してください。
* 変更をAEM Git リポジトリにコミットする方法を説明します。

これで、最後の手順を実行し、パイプラインを使用してそれらをデプロイできます。

## 目的 {#objective}

このドキュメントでは、パイプラインを使用してテーマをデプロイする方法を説明します。 ドキュメントを読めば、以下が可能です。

* パイプラインデプロイメントのトリガー方法を説明します。
* デプロイメントのステータスを確認する方法を参照してください。

## 担当ロール {#responsible-role}

このジャーニーの部分は、フロントエンド開発者に適用されます。

## パイプラインの開始 {#start-pipeline}

テーマのカスタマイズの変更をAEM Git リポジトリにコミットしたら、 [管理者が作成したパイプライン](pipeline-setup.md) をクリックして変更をデプロイします。

1. Cloud Manager にログイン [git のアクセス情報の取得と同様に](retrieve-access.md) プログラムにアクセスします。 の **概要** タブには、次のカードが表示されます： **パイプライン**.

   ![Cloud Manager の概要](assets/cloud-manager-overview.png)

1. 開始する必要があるパイプラインの横の省略記号をタップまたはクリックします。 ドロップダウンメニューから、 **実行**.

   ![パイプラインを実行](assets/run-pipeline.png)

1. 内 **パイプラインを実行** 確認ダイアログで、をタップまたはクリックします。 **はい**.

   ![パイプライン実行を確認](assets/pipeline-confirm.png)

1. パイプラインのリストで、「ステータス」列にパイプラインが現在実行中であることが示されます。

   ![パイプライン実行ステータス](assets/pipeline-running.png)

## パイプラインステータスの確認 {#pipeline-status}

パイプラインのステータスを確認して、進行状況の詳細をいつでも確認できます。

1. パイプラインの横にある省略記号をタップまたはクリックします。

   ![パイプラインの詳細を表示](assets/view-pipeline-details.png)

1. パイプラインの詳細ウィンドウに、パイプラインの進行状況の分類が表示されます。

   ![パイプラインの詳細](assets/pipeline-details.png)

>[!TIP]
>
>パイプラインの詳細ウィンドウで、をタップまたはクリックします **ログをダウンロード** デバッグ目的でパイプラインの任意のステップを実行する場合に、いずれかのステップが失敗する可能性があります。 パイプラインのデバッグは、このジャーニーの範囲外です。 詳しくは、 [その他のリソース](#additional-resources) 」セクションに表示されます。

## デプロイ済みのカスタマイズの検証 {#view-customizations}

パイプラインが完了したら、管理者に変更を検証するように通知できます。 管理者は次の操作を実行します。

1. AEMオーサリング環境を開きます。
1. に移動します。 [管理者が以前作成したサイト。](create-site.md)
1. いずれかのコンテンツページを編集します。
1. 適用された変更を確認します。

![適用された変更](assets/changes-applied.png)

## ジャーニーの終了 {#end-of-journey}

おめでとうございます。AEM Quick Site Creation ジャーニーを完了しました。 その結果、以下を達成できました。

* Cloud Manager とフロントエンドパイプラインがフロントエンドカスタマイズを管理およびデプロイする仕組みを理解します。
* テンプレートに基づいてAEMサイトを作成する方法と、サイトテーマをダウンロードする方法を説明します。
* AEM Git リポジトリにアクセスできるようにフロントエンド開発者をオンボーディングする方法。
* プロキシ化されたAEMコンテンツを使用してテーマをカスタマイズおよびテストし、その変更をAEM Git にコミットする方法。
* パイプラインを使用してフロントエンドのカスタマイズをデプロイする方法。

これで、独自のAEMサイトのテーマをカスタマイズする準備が整いました。 ただし、複数のフロントエンドパイプラインを使用して異なるワークストリームの作成を開始する前に、ドキュメントを確認してください [フロントエンドパイプラインを使用したサイトの開発。](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 次の方法でフロントエンド開発を最大限に活用できます。

* 一つの情報源を維持する。
* 懸念の分離を維持する。

AEMは強力なツールで、他にも多くのオプションを使用できます。 このジャーニーで説明した機能について詳しくは、[その他のリソース](#additional-resources)の節で紹介しているその他のリソースを参照してください。

## その他のリソース {#additional-resources}

以下の追加リソースでは、このドキュメントで言及したいくつかの概念について詳しく説明しています。

* [サイトレールを使用したサイトテーマの管理](/help/sites-cloud/administering/site-creation/site-rail.md)  — サイトパネルの強力な機能を学び、テーマソースのダウンロードやテーマバージョンの管理など、サイトテーマを簡単にカスタマイズして管理するのに役立ちます。
* [AEMas a Cloud Service技術ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)  — 既にAEMに関する十分な理解を得ている場合は、詳細な技術ドキュメントを直接参照することをお勧めします。
* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Cloud Manager の機能の詳細については、詳細な技術ドキュメントを直接お問い合わせください。
* [ロールに基づく権限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager には、適切な権限を持つ事前設定済みのロールが用意されています。 これらの役割の詳細と管理方法については、このドキュメントを参照してください。
* [Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - AEMaCS プロジェクトの Git リポジトリーの設定および管理方法について詳しくは、このドキュメントを参照してください。
* [CI/CD Pipeline の設定 —Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)  — このドキュメントでは、フルスタックとフロントエンドの両方のパイプラインの設定に関する詳細を説明します。
* [AEM Standard Site Template](https://github.com/adobe/aem-site-template-standard)  — これはAEM Standard Site テンプレートの GitHub リポジトリです。
* [AEM Site テーマ](https://github.com/adobe/aem-site-template-standard-theme-e2e)  — これはAEM Site Theme の GitHub リポジトリです。
* [npm](https://www.npmjs.com) - AEMテーマを使用してサイトをすばやく作成する場合は、npm に基づきます。
* [webpack](https://webpack.js.org) - AEMテーマは、webpack に依存するサイトをすばやく構築するために使用します。
* [ページの作成と整理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)  — このガイドでは、AEMサイトをテンプレートから作成した後にさらにカスタマイズする場合の、テンプレートサイトのページの管理方法について詳しく説明します。
* [パッケージの操作方法](/help/implementing/developing/tools/package-manager.md)  — パッケージを使用すると、リポジトリコンテンツのインポートおよびエクスポートが可能になります。 このドキュメントでは、AEM 6.5（AEMaaCS にも適用）でのパッケージの操作方法を説明します。
* [オンボーディングジャーニー](/help/journey-onboarding/home.md)  — このガイドは、チームが確実に設定され、AEM as a Cloud Serviceにアクセスできるようにするための出発点となります。
* [Adobe Experience Manager Cloud Manager ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja) - Cloud Manager の機能の詳細については、 Cloud Manager のドキュメントを参照してください。
* [サイト管理ドキュメント](/help/sites-cloud/administering/site-creation/create-site.md)  — クイックサイト作成ツールの機能の詳細については、サイト作成に関する技術ドキュメントを参照してください。
* [フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)  — このドキュメントでは、フロントエンドパイプラインを使用してフロントエンド開発プロセスから最大限の能力を引き出すために考慮すべき事項について説明します。
