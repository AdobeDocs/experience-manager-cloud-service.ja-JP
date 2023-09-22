---
title: AEM バージョンのアップデート
description: Adobe Experience Manager(AEM)as a Cloud Serviceで継続的な統合および配信 (CI/CD) を使用して、プロジェクトを最新バージョンに保つ方法を説明します。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 57d6b50ef5256bf6e8fce84100eed4690b77cb87
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 17%

---


# AEM バージョンのアップデート {#aem-version-updates}

Adobe Experience Manager(AEM)as a Cloud Serviceで継続的な統合および配信 (CI/CD) を使用して、プロジェクトを最新バージョンに保つ方法を説明します。

## CI／CD {#ci-cd}

AEM as a Cloud Service では、継続的統合および継続的配信（CI／CD）を使用して、プロジェクトを確実に最新の AEM バージョンで稼働できます。このプロセスは、ユーザーに混乱を与えることなく、実稼動、ステージング、開発の各インスタンスをシームレスに更新します。

インスタンスが自動的に更新される前に、新しいAEMメンテナンスリリースが 3 ～ 5 日前に公開されています。 この期間中は、オプションで [トリガーインスタンスの開発用の手動更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). この期間が経過すると、バージョンの更新が最初に開発環境に自動的に適用されます。 更新が成功すると、更新プロセスはステージインスタンスと実稼動インスタンスに進みます。 開発インスタンスとステージングインスタンスは、自動品質ゲートとして機能し、カスタムで作成されたテストは、実稼動環境にアップデートが適用される前に実行されます。

>[!NOTE]
>
> 注意：開発環境の自動更新は、2023 年にすべてのお客様に対して段階的に有効になります。 開発環境が自動的に更新されない場合は、手動更新を使用して、ステージ環境および実稼動環境との同期を維持できます。


## 更新のタイプ {#update-types}

AEMバージョンのアップデートは、次の 2 種類があります。

* **AEM メンテナンスアップデート**

   * 毎日リリースできます。
   * 最新のバグ修正やセキュリティ更新など、主にメンテナンス目的です。
   * 変更は定期的に適用されるので、影響は最小限に抑えられます。

* **新機能アップデート**

   * これらは、 [予測可能な月次スケジュール](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)

## 更新の失敗 {#update-failure}

AEM のアップデートは、複数のステップを含む集中的かつ完全に自動化された製品検証パイプラインを経て行われるため、実稼働環境にあるシステムへのサービスが中断されることはありません。ヘルスチェックは、アプリケーションのヘルスを監視するために使用されます。AEMのas a Cloud Serviceアップデート中にこれらのチェックが失敗した場合、リリースは続行されず、アップデートがこの予期しない動作を引き起こした原因をAdobeが調べます。

環境に新しいバージョンのカスタムコードをデプロイする場合、 [製品およびカスタム機能テスト](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) 重要な役割を果たす。 これにより、変更を加えた後でも、本番システムの安定性と機能性が確保されます。 これらのテストは、AEM Version Update プロセスでも適用されます。

実稼動環境への更新が失敗した場合、Cloud Manager はステージング環境を自動的にロールバックします。 これは、更新が完了した後で、ステージング環境と実稼動環境の両方が同じAEMバージョンであることを確認するために、自動的におこなわれます。
同様に、開発環境の自動更新が失敗した場合、ステージング環境と実稼動環境は更新されません。

>[!NOTE]
>
>カスタムコードがステージング環境にプッシュされ、実稼動環境にプッシュされなかった場合、次回のAEM更新でこれらの変更が削除され、顧客が前回実稼動環境に正常にリリースした際の git タグが反映されます。 したがって、ステージングでのみ使用可能なカスタムコードを再度デプロイする必要があります。

## ベストプラクティス {#best-practices}

* **ステージ環境の使用状況**
   * 長い QA/UAT サイクルに対しては、異なる環境（ステージではなく）を使用します。
   * ステージでサニティテストが完了したら、実稼動環境での検証に移行します。

* **実稼動パイプライン**
   * 実稼動環境にデプロイする前に一時停止.
   * ステージデプロイ後にパイプラインをキャンセルすると、コードが「スローウェイ」で実稼動用の有効な候補ではないことが示されます。を参照してください。 [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **実稼動以外のパイプライン**
   * の設定 [実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * 実稼動パイプラインの障害に対する配信速度/頻度を高速化します。 製品機能テスト、カスタム機能テスト、カスタム UI テストを有効にして、実稼動以外のパイプラインの問題を特定します。

* **コンテンツのコピー**
   * 用途 [コンテンツのコピー](/help/implementing/developing/tools/content-copy.md) 類似のコンテンツセットを実稼動以外の環境に移動する場合。

* **自動機能テスト**
   * 重要な機能をテストできるよう、パイプラインに自動テストを含めます。
   * [顧客機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) および [カスタム UI テスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) AEMのリリースに失敗した場合、がブロックされていても、ロールアウトはおこなわれません。

## 回帰 {#regression}

回帰に関する問題が発生した場合は、Admin Consoleでサポートケースを送信します。 問題が致命的で、その影響が実稼動に及ぶ場合は、P1 を発生させる必要があります。 回帰の問題の再現に必要なすべての詳細を指定します。

## 複合ノードストア {#composite-node-store}

通常、ノードのクラスターであるオーサリングインスタンスを含め、更新でダウンタイムは発生しません。 [Oak の複合ノードストア機能](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)により、ローリングアップデートが可能です。

この機能を利用すると、AEM で複数のリポジトリを同時に参照できます。内 [ローリングデプロイメント](/help/implementing/deploying/overview.md#how-rolling-deployments-work)の場合、新しいAEMバージョンには独自の `/libs` （TarMK ベースの不変リポジトリ）。 古いAEMとは異なりますが、どちらも、次のような領域を含む共有 DocumentMK ベースの可変リポジトリを参照します `/content` , `/conf` , `/etc` その他

古いバージョンと新しいバージョンの両方には、 `/libs`に値を指定しない場合、両方をローリング更新時にアクティブにできます。 また、古いが新しいに完全に置き換えられるまで、両方ともトラフィックを引き継ぐことができます。
