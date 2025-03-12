---
title: コンテンツ転送の検証
description: コンテンツ転送ツールを使用してコンテンツ転送を検証します
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: 9b05ed38e8eb337b3a07ee2051c6a0d530088af2
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 96%

---


# コンテンツ転送の検証 {#validating-content-transfers}

## はじめに {#getting-started}

コンテンツ転送ツールで抽出されたすべてのコンテンツが、ターゲットインスタンスに正常に取り込まれたかどうかをユーザーが確実に判断できます。この検証機能は、抽出中に関与したすべてのノードのパスのダイジェストと、取り込み中に関与したすべてのノードのパスのダイジェストを比較することによって機能します。抽出ダイジェストに含まれているノードパスが取り込みダイジェストにない場合、検証は失敗したと見なされ、追加の手動検証が必要になる可能性があります。

>[!INFO]
>
>この機能は、コンテンツ転送ツール（CTT）バージョン 1.8.x リリース以降で使用できるようになります。AEM Cloud Service のターゲット環境は、バージョン 6158 以降を実行している必要があります。また、[事前コピー](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step)を実行するようにソース環境をセットアップする必要があります。検証機能は、ソース上の azcopy.config ファイルを探します。このファイルが見つからない場合、検証は実行されません。azcopy.config ファイルを設定する方法について詳しくは、[大規模なコンテンツリポジトリの処理 - azcopy.config ファイルの設定](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file)を参照してください。

コンテンツ転送の検証はオプション機能です。この機能を有効にすると、抽出にかかる時間と取り込みにかかる時間の両方が長くなります。この機能を使用するには、次の手順に従って、ソース AEM 環境のシステムコンソールで有効にします。

1. **ツール／運営／Web コンソール**&#x200B;を選択するか、URL（*https://serveraddress:serverport/system/console/configMgr*）に直接アクセスして、ソースインスタンス上の Adobe Experience Manager Web コンソールに移動します。
1. **Content Transfer Tool Extraction Service Configuration** を検索します。
1. 鉛筆アイコンボタンを使用して、設定値を編集します。
1. 「**Enable Migration Validation during extraction**」設定を有効にししてから、「**保存**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

この設定を有効にし、ターゲット AEM Cloud Service 環境で互換性のあるリリースを実行している場合は、以降のすべての抽出および取り込み時に移行の検証が行われます。

コンテンツ転送ツールのインストール方法について詳しくは、[コンテンツ転送ツールの基本を学ぶ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)を参照してください。

## コンテンツ転送の検証方法 {#how-to-validate-a-content-transfer}

ソース AEM 環境で移行の検証を有効にしたうえで、抽出を開始します。

**抽出時にステージングコンテナを上書き**&#x200B;が有効になっている場合は、抽出に関係するすべてのノードが抽出パスダイジェストに記録されます。この設定を使用する場合は、取り込み時に「**取り込み前にクラウドインスタンス上の既存のコンテンツを消去**」設定を有効にすることが重要です。そうしないと、取り込みダイジェストに見つからないノードがあるように見える場合があります。これらは、以前の取り込み時からターゲットに既に存在するノードです。

これを図で示した例については、次の例を参照してください。

### 例 1 {#example-1}

* **抽出（上書き）**

  ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/example1-extraction.png)

* **取り込み（ワイプ）**

  ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **備考**

  この「上書き」と「ワイプ」の組み合わせにより、取り込みを繰り返す場合でも、一貫した検証結果が得られます。

### 例 2 {#example-2}

* **抽出**

  ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/example2-extraction.png)

* **取り込み**

  ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **備考**

  この「上書き」と「ワイプ」の組み合わせにより、最初の取り込みでは一貫した検証結果が得られます。

  取り込みを繰り返すと、取り込みダイジェストが空になり、検証が失敗したように見えます。この抽出からのすべてのノードが既にターゲット上に存在するので、取り込みダイジェストは空です。

抽出が完了したら、取り込みを開始します。

取り込みログの冒頭には、`aem-ethos/tools:1.2.438` のようなエントリが含まれています。このバージョン番号が **1.2.438** 以上であることを確認します。そうでない場合、使用している AEM as a Cloud Service リリースでは検証がサポートされていません。

取り込みが完了し、検証が開始されると、次のログエントリが取り込みログに記録されます。

```
Gathering artifacts for migration validation...
```

検証の詳細は、このエントリの後に記録されます。以下に大規模な移行の例を示します。

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

抽出ダイジェストに存在していて取り込みダイジェストに見つからないエントリはないので、これは成功した検証の例になります。

比較すると、検証が失敗した（または追加移行が実行された）場合の検証レポートは次のように表示されます。

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上記の失敗例は、取り込みを実行したあと、取り込み時にノードが関係しないように、ワイプを無効にして同じ取り込みを再度実行することで得られたものです。すべてのノードが既にターゲット上に存在していたケースです。

検証レポートは、取り込みログに含まれるだけでなく、Cloud Acceleration Manager の&#x200B;**取り込みジョブ**&#x200B;ユーザーインターフェイスからアクセスすることも可能です。これを行うには、3 つのドット（**...**）をクリックし、ドロップダウンで「**検証レポート**」をクリックして検証レポートを表示します。


![画像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## プリンシパルの移行を検証する方法 {#how-to-validate-group-migration}

プリンシパルの移行の詳細とその必要性について詳しくは、[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照してください。

抽出と取り込みが正常に完了すると、プリンシパルの移行の概要とレポートが使用可能になります。この情報を使用して、どのグループが正常に移行されたかを検証し、一部のグループが正常に移行されなかった理由を判断することもできます。

この情報を表示するには、Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、コンテンツ転送カードをクリックします。**取り込みジョブ**&#x200B;に移動し、検証する取り込みを見つけます。その取り込みの 3 つのドット（**...**）をクリックし、ドロップダウンで「**プリンシパルの概要を表示**」をクリックします。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

概要情報を含むダイアログが表示されます。ヘルプアイコンを使用して、詳細な説明を参照します。完全なコンマ区切り（CSV）プリンシパル移行レポートをダウンロードするには、「**ファイルをダウンロード…**」のドロップダウンリストから「**プリンシパル移行レポート**」を選択し、「**ダウンロード**」ボタンをクリックします。 また、このレポートの末尾には、移行後のユーザー管理に使用できるユーザーレポートもあります。

![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

プリンシパルの移行レポートでは、次の情報が報告されます。

* 移行された各グループと、そのグループの移行をトリガーした最初のコンテンツパス。グループは他のパス上にある場合もありますが、特定のグループに対して最初に見つかったパスのみが報告されます。また、ACL または CUG ポリシーで見つかったかどうかも報告されます。
* ローカルグループとして移行された各グループには、グループの行に「local」という単語が示されます。
* 移行されなかった各グループと、移行されなかった理由。通常は、次のいずれかの理由になります。
   * 組み込みのグループである
   * 既にターゲットシステム上にある
   * 移行するコンテンツの ACL または CUG ポリシーに含まれていない
   * 一意のフィールドが重複している（rep:principalName、rep:authorizableId、jcr:uuid、rep:externalId のいずれかが既に宛先に存在しますが、これらはすべて一意である必要があります）

## トラブルシューティング {#troubleshooting}

### 検証に失敗した。次は何をすればよいでしょうか。 {#validation-fail}

まず、取り込みが本当に失敗したか、それとも抽出したコンテンツが既にターゲット環境に存在しているのかを確認することです。後者の状況は、「**取り込み前にクラウドインスタンス上の既存のコンテンツを消去する**」オプションを無効にして取り込みが繰り返される場合に発生する可能性があります。

検証するには、検証レポートからパスを選択し、そのパスがターゲット環境に存在するかどうかを確認します。これがパブリッシュ環境の場合、できることはページやアセットの直接確認に限られる可能性があります。この手順に関してサポートが必要な場合は、カスタマーケアに連絡してチケットをオープンします。

### ノード数が予想より少ない。なぜでしょう？ {#node-count-lower-than-expected}

ファイルを扱いやすいサイズにして、取り込みの完了後 2 時間以内に移行の検証結果を計算できるように、一部のパスは抽出ダイジェストと取り込みダイジェストから意図的に除外されています。

現在ダイジェストから除外されているパスには、`cqdam.text.txt` レンディション、`/home` 内のノード、`/jcr:system` 内のノードなどがあります。

### クローズドユーザーグループ {#validating-cugs}

クローズドユーザーグループ（CUG）ポリシーを使用する際のその他の考慮事項について詳しくは、[クローズドユーザーグループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)を参照してください。
