---
title: Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.4.0 のリリースノート
description: AEM as a Cloud Serviceの Cloud Manager 2022.4.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: e448ee4ee2928a136bdab382c67104bedce28732
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 7%

---


# Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.4.0 のリリースノート {#release-notes}

このページでは、AEM as a Cloud Serviceの Cloud Manager 2022.4.0 のリリースノートについて説明します。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEMas a Cloud Service2022 年 4 月 7 日にリリースされた Cloud Manager リリース 2022.4.0 のリリース日です。 次回のリリースは 2022 年 5 月 5 日に予定されています。

## 新機能 {#what-is-new}

* パイプラインビルド手順の期間と成功率が改善され、4 月を通じてすべてのお客様に段階的に展開される予定です。
* パイプラインの追加と編集ウィザードの入力フィールドに名前の最初の数文字を入力し、両方で推奨される一致項目から選択することで、Git ブランチを簡単に見つけることができるようになりました [実稼動](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) および [非実稼動](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) パイプライン。
* 4 月のリリース後すぐに、環境の作成中にクラウド領域を定義する際に、インドが選択可能になります。
* この **パイプライン** 多数のパイプラインを持つプログラムのユーザビリティを向上させるために、ページネーションが追加されました。
   * 1 ページにつき 50 行が表に表示されます。
* のバージョン。 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) Cloud Manager で使用されているをバージョン 36 に更新しました。
* OracleJDK は、AEMアプリケーションの開発と操作のためのデフォルト JDK になりました。 Cloud Manager のビルドプロセスは、Maven ツールチェーンで代替オプションが明示的に選択されている場合でも、OracleJDK を使用してに自動的に切り替わります。
   * oracleJDK への切り替え方法の詳細については、 [ビルド環境に関するドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * 詳しくは、 [Adobe Experience Manager FAQ の Java サポートポリシー](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) を使用して、この変更に関するよくある質問に対処します。
* 検証ステップ中に古いAEMバージョンを検出することで、パイプラインの実行がより高速に失敗するようになりました。 UI に、ユーザーをガイドするメッセージが表示されます。

## バグの修正 {#bug-fixes}

* UI テスト手順で作成したログを、UI からダウンロードできるようになりました。
* Web 層設定パイプラインで、Web 層設定の実行からのみパッケージを再利用できるようになりました。
* 古い環境でAEMを更新する方法に関する UI のメッセージに、より明確に記述されました。
