---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
source-git-commit: 3f579f6871da8e8b2fcea921e5abf57dfc14f5f8
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 17%

---


# Adobe Experience Manager as a Cloud Service 2021.6.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.6.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as aCloud Service版の最新のリリースノートを確認するには、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.6.0のCloud Managerのリリース日は2021年6月10日です。
次回のリリースは2021年7月16日に予定されています。

### 新機能 {#what-is-new}

* プレビューサービスは、すべてのプログラムに周期的にデプロイされます。 お客様は、プログラムがプレビューサービスに対して有効になると、製品内で通知を受けます。 詳しくは、[Preview Serviceへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)を参照してください。

* ビルド手順中にダウンロードされたMavenの依存関係は、パイプライン実行の間でキャッシュされるようになりました。 この機能は、今後数週間のお客様に対して有効になる予定です。

* プログラムの名前は、プログラムを編集ダイアログで編集できるようになりました。

* プロジェクトの作成時と、Gitワークフローを管理するデフォルトのプッシュコマンドで使用されるデフォルトのブランチ名が`main`に変更されました。

* UIでのプログラムの編集エクスペリエンスが更新されました。

* 品質ルール`ImmutableMutableMixCheck`が更新され、`/oak:index`ノードが不変として分類されるようになりました。

* 品質ルール`CQBP-84`と`CQBP-84--dependencies`は、1つのルールに統合されました。

* 混乱を避けるために、環境の詳細ページのパブリッシュAEMとパブリッシュDispatcherのセグメント行が統合されました。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* `damAssetLucene`インデックスの構造を検証するための新しいコード品質ルールが追加されました。 詳しくは、[カスタムDAM Asset Lucene Oakインデックス](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)を参照してください。

* 環境の詳細ページに、公開サービスとプレビューサービスの複数のドメイン名が表示されるようになりました（該当する場合）。 詳しくは、[環境の詳細](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。

### バグ修正 {#bug-fixes}

* ルート要素名の後に改行を含むJCRノード定義が正しく解析されなかった問題を修正しました。

* リストリポジトリAPIは、削除されたリポジトリをフィルタリングしません。

* スケジュール手順に無効な値が指定された場合、誤ったエラーメッセージが表示されていました。

* 場合によっては、IP許可リストがデプロイされていない場合でも、その設定の横に緑色の&#x200B;*アクティブ*&#x200B;ステータスが表示されることがあります。

* 一部のプログラム編集シーケンスでは、実稼動パイプラインを作成または編集できなくなる可能性があります。

* 一部のプログラム編集シーケンスでは、**概要**&#x200B;ページに、プログラム設定を再実行する際に誤解を招くようなメッセージが表示される場合があります。
