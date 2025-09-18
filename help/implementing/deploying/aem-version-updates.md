---
title: AEM バージョンのアップデート
description: Adobe Experience Manager (AEM) as a Cloud Service で継続的統合および継続的配信（CI/CD）を使用して、プロジェクトを最新バージョンに保つ方法について説明します。
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
role: Admin
source-git-commit: 01de7b0c4e0408a3bbc5322e37db5075d43c4c5f
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 100%

---


# AEM バージョンのアップデート {#aem-version-updates}

Adobe Experience Manager (AEM) as a Cloud Service で継続的統合および継続的配信（CI/CD）を使用して、プロジェクトを最新バージョンに保つ方法について説明します。

## CI/CD {#ci-cd}

AEM as a Cloud Service では、継続的インテグレーションおよび継続的配信（CI/CD）を使用して、プロジェクトを確実に最新の AEM バージョンで稼働できます。このプロセスは、ユーザーに混乱を与えることなく、実稼動、ステージング、開発の各インスタンスをシームレスに更新します。

>[!NOTE]
> 開発インスタンスは既に自動的に更新されているので、開発インスタンスの手動更新は、_一部_&#x200B;のプログラムで利用できない場合があります。この機能は、自動更新への切り替えが行われているところです。

インスタンスが自動的に更新される前に、新しい AEM メンテナンスリリースが 3～5 日前に公開されています。その期間中に、開発インスタンスが自動的に更新される可能性があります。または、利用できる場合は、オプションで[開発インスタンスの更新をトリガー](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)することもできます。バージョンの更新がまず開発環境に自動的に適用されます。更新が成功すると、更新プロセスはステージングインスタンスと実稼動インスタンスに進みます。開発インスタンスとステージングインスタンスは、自動品質ゲートとして機能し、カスタムで作成されたテストは、実稼動環境に更新が適用される前に実行されます。

### NIMU（非侵入型メンテナンス更新） {#nimu}

非侵入型メンテナンス更新は、顧客のパイプラインを必要とせずに適用される自動更新です。
NIMU を通じて、AEM バージョンの更新がスケジュールされている場合や進行中の場合でも、お客様はいつでもパイプラインを使用できます。また、メンテナンス更新は顧客パイプライン実行履歴に表示されなくなるので、コードのデプロイメント履歴を追跡しやすくなります。

#### アクティビティの更新

Cloud Manager の UI 環境パネルを使用して、以前と同様、環境ごとに現在の AEM のバージョンを確認することができます。顧客側で作成したテストを含め、パイプラインで使用される品質ゲートと同じものが非侵入型メンテナンス更新で使用されます。
プログラムの環境に非侵入型メンテナンス更新が適用されるたびに、[Cloud Manager UI 通知](/help/implementing/cloud-manager/notifications.md)が送信されます。この通知をメールにも送信するように設定することができます。

>[!NOTE]
>
> メモ：2024 年には、すべてのお客様に対して、非侵入型メンテナンス更新が段階的に有効になる予定です。

## 更新のタイプ {#update-types}

AEM バージョンの更新には、次の 2 種類があります。

* [**AEM メンテナンスアップデート**](/help/release-notes/maintenance/latest.md)

   * この更新は主にメンテナンスを目的としており、最新のバグ修正やセキュリティ更新などを含みます。
   * 変更は定期的に適用されるので、影響は最小限に抑えられます。

* [**AEM 機能のアクティベーション**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * この更新は予測可能な月次スケジュールでリリースされます。

>[!NOTE]
>
> [Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja#aem-as-cloud-service)の月次リリースの主な日付を確認し、リリースの準備に関する主要なアクティビティに備えるためにカレンダーをマークします。

## 更新の失敗 {#update-failure}

AEM のアップデートは、複数のステップを含む集中的かつ完全に自動化された製品検証パイプラインを経て行われるため、実稼働環境にあるシステムへのサービスが中断されることはありません。ヘルスチェックは、アプリケーションのヘルスを監視するために使用されます。AEM as a Cloud Service のアップデート中にこれらのチェックが失敗した場合、リリースは続行されず、アップデートがこの予期しない動作を引き起こした原因をアドビが調査します。

環境に新しいバージョンのカスタムコードをデプロイする場合、[製品機能テストとカスタム機能テスト](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)が重要な役割を果たします。変更を加えた後でも、実稼働システムの安定性と機能性が確保されます。これらのテストは、AEM バージョンアップデートプロセスでも適用されます。

実稼働環境へのアップデートに失敗した場合、Cloud Manager はステージング環境を自動的にロールバックします。これは、アップデート完了後、ステージング環境と実稼働環境の両方が必ず同じ AEM バージョンであるようにするために、自動的に行われます。
同様に、開発環境の自動更新が失敗した場合、ステージング環境と実稼動環境は更新されません。

>[!NOTE]
>
>カスタムコードが実稼動環境ではなくステージング環境にプッシュされた場合、次回の AEM アップデートでは、それらの変更が削除され、実稼動環境に対して正常に行われた最後の顧客リリースの Git タグが反映されます。したがって、ステージング環境でのみ使用可能なカスタムコードを再度デプロイする必要があります。

## ベストプラクティス {#best-practices}

* **ステージング環境の使用**
   * 長い QA/UAT サイクルに対しては、異なる環境（ステージング環境以外）を使用します。
   * ステージング環境で健全性テストが完了したら、実稼動環境での検証に移行します。

* **実稼動パイプライン**
   * 実稼動環境にデプロイする前に一時停止します。
   * ステージング環境にデプロイした後でパイプラインをキャンセルすると、コードが「使い捨て」であり、実稼動用の有効な候補ではないことが示されます。[実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を参照してください。

* **実稼動以外のパイプライン**
   * [実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)を設定します。
   * 実稼動パイプラインの障害に対する配信速度と頻度を向上します。製品機能テスト、カスタム機能テスト、カスタム UI テストを有効にして、実稼動以外のパイプラインのイシューを特定します。

* **コンテンツのコピー**
   * [コンテンツのコピー](/help/implementing/developing/tools/content-copy.md)を使用し、類似のコンテンツセットを実稼動以外の環境に移動します。

* **自動機能テスト**
   * 重要な機能をテストできるよう、パイプラインに自動テストを含めます。
   * [顧客機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)と[カスタム UI テスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)がブロックしており、失敗すると AEM リリースはロールアウトされません。

## 回帰 {#regression}

回帰に関するイシューが発生した場合は、Admin Console からサポートケースを送信します。イシューが致命的で、その影響が実稼動に及ぶ場合は、P1 を発生させる必要があります。回帰のイシューを再現するために必要なすべての詳細を提供します。

## 複合ノードストア {#composite-node-store}

ノードのクラスターであるオーサリングインスタンスの場合も含め、通常、アップデートでダウンタイムは発生しません。[Oak の複合ノードストア機能](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)により、ローリングアップデートが可能です。

この機能を利用すると、AEM で複数のリポジトリを同時に参照できます。[ローリングデプロイメント](/help/implementing/deploying/overview.md#how-rolling-deployments-work)の場合、新しい AEM バージョンには独自の `/libs` （TarMK ベースの不変リポジトリ）が含まれます。古い AEM バージョンとは異なりますが、どちらも、`/content`、`/conf`、`/etc` などのエリアを含む共有 DocumentMK ベースの可変リポジトリを参照します。

古いバージョンにも新しいバージョンにも独自の `/libs` のバージョンがあるので、ローリングアップデート中に両方ともアクティブにできます。そして、古いバージョンが新しいバージョンに完全に置き換えられるまで両方がトラフィックを処理できます。

## その他の情報 {#further-information}

関連するテーマについて詳しくは、以下を参照してください。

* [Cloud Manager CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)
* [Cloud Manager UI 通知](/help/implementing/cloud-manager/notifications.md)
* [Adobe Experience Manager as a Cloud Service のアーキテクチャ](/help/overview/architecture.md)
