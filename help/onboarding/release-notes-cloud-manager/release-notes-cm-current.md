---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 56%

---

# Adobe Experience Manager as a Cloud Service 2021.6.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.6.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.6.0のCloud Managerのリリース日は2021年6月10日です。
次回のリリースは 2021 年 6 月 15 日（PT）に予定されています。

### 新機能 {#what-is-new}

* プレビューサービスは、すべてのプログラムに周期的にデプロイされます。 お客様は、プログラムがプレビューサービスに対して有効になると、製品内で通知を受けます。 詳しくは、[Preview Serviceへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)を参照してください。

* ビルド手順中にダウンロードされた Maven の依存関係は、パイプライン実行から次回の実行までの間にキャッシュされるようになりました。この機能は、今後数週間にわたり、お客様に対して有効になる予定です。

* プログラムの名前は、プログラムを編集ダイアログで編集できるようになりました。

* プロジェクトの作成時に使用されるデフォルトのブランチ名と、Git 管理ワークフロー経由のデフォルトのプッシュコマンドで使用されるデフォルトのブランチ名が `main` に変更されました。

* UI でのプログラムの編集エクスペリエンスが更新されました。

* 品質ルール `ImmutableMutableMixCheck` が更新され、`/oak:index` ノードが不変として分類されるようになりました。

* 品質ルール `CQBP-84` と `CQBP-84--dependencies` は、1 つのルールに統合されました。この統合の一環として、AEM ランタイムにデプロイされるサードパーティの依存関係の問題を、依存関係のスキャンでより正確に特定できます。

* 混乱を避けるために、環境の詳細ページのパブリッシュAEMとパブリッシュDispatcherのセグメント行が統合されました。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* `damAssetLucene`インデックスの構造を検証するための新しいコード品質ルールが追加されました。 詳しくは、[カスタムDAM Asset Lucene Oakインデックス](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)を参照してください。

* 環境の詳細ページに、公開サービスとプレビューサービスの複数のドメイン名が表示されるようになりました（該当する場合）。 詳しくは、[環境の詳細](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。

### バグ修正 {#bug-fixes}

* ルート要素名の後に改行を含む JCR ノード定義が正しく解析されなかった問題を修正しました。

* リストリポジトリー API は、削除されたリポジトリをフィルタリングしません。

* スケジュール手順に無効な値が指定された場合、誤ったエラーメッセージが表示されていました。

* 場合によっては、IP許可リストがデプロイされていない場合でも、その設定の横に緑色の&#x200B;*アクティブ*&#x200B;ステータスが表示されることがあります。

* 一部のプログラム編集シーケンスでは、実稼動パイプラインを作成または編集できなくなる可能性があります。

* 一部のプログラム編集シーケンスでは、**概要**&#x200B;ページに、プログラム設定を再実行する際に誤解を招くようなメッセージが表示される場合があります。
