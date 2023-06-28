---
title: AEM バージョンのアップデート
description: AEMas a Cloud Serviceで継続的な統合および配信 (CI/CD) を使用して、プロジェクトを最新バージョンに保つ方法を説明します。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 54%

---


# AEM バージョンのアップデート {#aem-version-updates}

AEMas a Cloud Serviceで継続的な統合および配信 (CI/CD) を使用して、プロジェクトを最新バージョンに保つ方法を説明します。

## CI/CD {#ci-cd}

AEM as a Cloud Serviceでは、継続的統合と継続的配信 (CI/CD) を使用して、プロジェクトが確実に最新のAEMバージョンになるようにします。 これは、ユーザーへのサービスが中断されることなく、実稼働インスタンスとステージングインスタンスが AEM の最新バージョンに更新されることを意味します。

バージョンの更新は、実稼動インスタンスとステージングインスタンスにのみ自動的に適用されます。 [AEMの更新は、他のすべてのインスタンスに手動で適用する必要があります](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).

## 更新のタイプ {#update-types}

AEMバージョンのアップデートは、次の 2 種類があります。

* **AEM メンテナンスアップデート**

   * 日単位でリリースされる可能性があります。
   * 主にメンテナンス目的で、最新のバグ修正やセキュリティアップデートなどを含みます。
   * 変更が定期的に適用されるので、影響は最小限に抑えられます。

* **新機能アップデート**

   * が [予測可能な月次スケジュール](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)

## 更新エラー {#update-failure}

AEM のアップデートは、複数のステップを含む集中的かつ完全に自動化された製品検証パイプラインを経て行われるため、実稼働環境にあるシステムへのサービスが中断されることはありません。ヘルスチェックは、アプリケーションのヘルスを監視するために使用されます。AEM as a Cloud Service のアップデート中にこれらのチェックが失敗した場合、リリースは続行されず、アップデートがこの予期しない動作を引き起こした原因をアドビが調査します。

[製品テストと顧客機能テスト](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)は、製品のアップグレードや顧客コードのプッシュが実稼働システムを破壊するのを防ぎますが、AEM バージョンのアップデート中にも検証されます。

実稼働環境へのアップデートに失敗した場合、Cloud Manager はステージング環境を自動的にロールバックします。これは、アップデート完了後、ステージング環境と実稼働環境の両方が必ず同じ AEM バージョンであるようにするために、自動的に行われます。

>[!NOTE]
>
>カスタムコードが実稼動環境ではなくステージングにプッシュされた場合、次回の AEM アップデートでは、それらの変更が削除され、実稼動環境に対して正常に行われた最後の顧客リリースの git タグが反映されます。したがって、ステージングでのみ使用可能なカスタムコードを再度デプロイする必要があります。

## 複合ノードストア {#composite-node-store}

ほとんどの場合、ノードのクラスターであるオーサリングインスタンスを含め、更新でダウンタイムは発生しません。 次の理由により、ローリングアップデートが可能です： [Oak の複合ノードストア機能。](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

この機能を利用すると、AEM で複数のリポジトリを同時に参照できます。内 [ローリングデプロイメント](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 新しいAEMバージョンには独自の `/libs` （TarMK ベースの不変リポジトリ）古いAEMバージョンとは異なります。両方とも、以下のような領域を含む共有の DocumentMK ベースの可変リポジトリを参照します。 `/content` , `/conf` , `/etc` その他

古いバージョンと新しいバージョンの両方には、 `/libs`を使用すると、両方をローリング更新中にアクティブにでき、両方をトラフィックに引き継ぐことができます。このとき、古いが新しいに完全に置き換えられるまで、トラフィックは引き継がれます。
