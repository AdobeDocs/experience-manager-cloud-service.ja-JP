---
title: AEM バージョンのアップデート
description: 'AEM バージョンのアップデート '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 100%

---

# AEM バージョンのアップデート {#aem-version-updates}

## はじめに {#introduction}

AEM as a Cloud Service では、継続的統合および継続的配信（CI／CD）を使用して、プロジェクトが確実に最新の AEM バージョンで稼働できるようになっています。つまり、ユーザーに対するサービスが中断することなく、実稼働インスタンスとステージングインスタンスが AEM の最新バージョンに更新されます。

>[!NOTE]
>実稼働環境へのアップデートに失敗した場合、Cloud Manager はステージング環境を自動的にロールバックします。これは、アップデート完了後も、ステージング環境と実稼働環境の両方が確実に同じ AEM バージョンに基づくようにするために、自動的に行われます。

AEM バージョンのアップデートには、次の 2 種類があります。

* **AEM プッシュアップデート**

   * 毎日リリース可能です。

   * 主に、最新のバグ修正やセキュリティの更新などのメンテナンス作業です。

      変更が定期的に適用されるので影響は増分的で、サービスへの影響が少なくなります。

* **新機能アップデート**

   * 予測可能な月次スケジュールでリリースされます。

AEM のアップデートは、複数の手順が関係する集中的かつ完全に自動化された製品検証パイプラインを経て行われ、実稼働環境にあるシステムへのサービスが中断しないようになっています。ヘルスチェックは、アプリケーションのヘルスを監視するために使用されます。AEM as a Cloud Service のアップデート中にこれらのチェックが失敗した場合、リリースは続行されず、アップデートがこの予期しない動作を引き起こした原因をアドビが調査します。

[製品テストおよび顧客機能テスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html?lang=ja#functional-testing)は、製品のアップグレードや顧客コードのプッシュによる実稼動環境での障害発生を防ぐためのもので、これらも AEM バージョンのアップデート時に検証されます。

>[!NOTE]
>
>カスタムコードがステージング環境にプッシュされた後で拒否された場合、次回の AEM アップデートでは、それらの変更は削除され、顧客が前回実稼動環境に正常にリリースしたコードの Git タグを反映するようになります。

## 複合ノードストア {#composite-node-store}

ノードのクラスターであるオーサーの場合も含め、前述のように、ほとんどの場合、アップデートでダウンタイムは発生しません。Oak の&#x200B;*複合ノードストア*&#x200B;機能により、ローリングアップデートが可能です。

この機能を利用すると、AEM で複数のリポジトリーを同時に参照できます。ローリングデプロイメントでは、新しいグリーン AEM バージョンに古いブルー AEM バージョンとは異なる独自の `/libs`（TarMK ベースの不変リポジトリー）が含まれていますが、どちらも、`/content`、`/conf`、`/etc` などの領域を含んだ DocumentMK ベースの共有の可変リポジトリーを参照しています。ブルーバージョンにもグリーンバージョンにも独自の `/libs` があるので、ローリングアップデート中はどちらもアクティブになり、ブルーバージョンが完全にグリーンバージョンに置き換わるまでトラフィックを処理することができます。
