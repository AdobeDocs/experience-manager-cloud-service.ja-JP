---
title: コンテンツ転送の検証
description: コンテンツ転送ツールを使用して、コンテンツ転送を検証します
source-git-commit: c542b631a94b9fcbda4790ca9ca5a461d104c790
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---


# コンテンツ転送の検証 {#validating-content-transfers}

## はじめに {#getting-started}

コンテンツ転送ツールで抽出されたすべてのコンテンツがターゲットインスタンスに正常に取り込まれたかどうかを確実に判断できます。 この検証機能は、抽出時に関与したノードのダイジェストと、取得時に関係したノードのダイジェストを比較することで機能します。 取り込みダイジェストに見つからないノードパスが抽出ダイジェストに含まれている場合、検証は失敗したと見なされ、追加の手動検証が必要な場合があります。

>[!INFO]
>
>この機能は、コンテンツ転送ツール (CTT) バージョン 1.8.x リリース以降で使用できるようになります。 AEM Cloud Serviceのターゲット環境は、バージョン 6158 以降を実行している必要があります。 また、実行するには、ソース環境を設定する必要があります [プリコピー](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). 検証機能は、ソース上の azcopy.config ファイルを探します。 このファイルが見つからない場合は、検証は実行されません。 azcopy.config ファイルの設定方法について詳しくは、 [このページ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

コンテンツ転送の検証はオプションの機能です。 この機能を有効にすると、抽出の実行に要する時間と取り込みの実行に要する時間の両方が長くなります。 この機能を使用するには、次の手順に従って、ソースAEM環境のシステムコンソールでこの機能を有効にします。

1. ソースインスタンス上のAdobe Experience Manager Web コンソールに移動するには、次の手順に従います。 **ツール/操作/ Web コンソール** または URL( ) に直接アクセスします。 *https://serveraddress:serverport/system/console/configMgr*
1. を検索 **コンテンツ転送ツール抽出サービス設定**
1. 鉛筆アイコンボタンを使用して、設定値を編集します
1. を有効にします。 **抽出中に移行検証を有効にする** 設定してから、 **保存**:

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

この設定を有効にし、互換性のあるリリースを実行しているターゲットAEM Cloud Service環境では、以降のすべての抽出および取り込み中に移行の検証がおこなわれます。

コンテンツ転送ツールのインストール方法について詳しくは、 [コンテンツ転送ツールの概要](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## コンテンツ転送の検証方法 {#how-to-validate-a-content-transfer}

ソースAEM環境で移行検証が有効になっている状態で、抽出を開始します。

If **抽出時にステージングコンテナを上書き** が有効になっている場合、抽出に関係するすべてのノードが抽出パスダイジェストに記録されます。 この設定を使用する場合、 **取り込み前にクラウドインスタンス上の既存のコンテンツを消去** 取り込み中に設定をおこなうと、取り込みダイジェストにノードが欠落しているように見える場合があります。 これらは、以前の取り込みからターゲットに既に存在するノードです。

この例については、以下の例を参照してください。

### 例 1 {#example-1}

* **抽出（上書き）**

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTextractionoverwrite.png)

* **取り込み（ワイプ）**

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTingestionwipe.png)

* **備考**

   この「上書き」と「ワイプ」の組み合わせにより、繰り返し取り込みの場合でも、検証結果が一貫して表示されます。

### 例 2 {#example-2}

* **抽出**

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTextraction.png)

* **取り込み**

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTTingestion.png)

* **備考**

   この「上書き」と「ワイプ」の組み合わせにより、初期取り込みでの検証結果が一貫しておこなわれます。

   取り込みを繰り返すと、取り込みダイジェストは空になり、検証が失敗したように見えます。 この抽出からのすべてのノードは既にターゲット上に存在するので、取り込みダイジェストは空になります。

抽出が完了したら、取り込みを開始します。

取り込みログの上部には、 `aem-ethos/tools:1.2.438`. このバージョン番号が **1.2.438** それ以上の場合、使用しているAEM as a Cloud Serviceのリリースでは検証がサポートされません。

取り込みが完了し、検証が開始されると、次のログエントリが取り込みログに記録されます。

```
Gathering artifacts for migration validation...  
```

検証の詳細は、このエントリに従います。 以下に大規模な移行の例を示します。

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

抽出ダイジェストに存在する取り込みダイジェストに見つからないエントリがないので、成功した検証の例は次のとおりです。

比較すると、検証が失敗した場合の検証レポートの表示方法は次のとおりです。

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
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上記の失敗例は、取り込みを実行し、取り込み中にノードが関与しないように、取り込みを無効にして同じ取り込みを再実行することで達成されました。すべてはターゲット上に既に存在していました。

検証レポートは、取り込みログに含まれるだけでなく、コンテンツ転送ツールのユーザーインターフェイスからもアクセスできます。 それには、移行セットを選択し、 **検証** ボタンをクリックします。


![画像](/help/journey-migration/content-transfer-tool/assets/CTTvalidatebutton.png)

検証ログダイアログが開きます。

![画像](/help/journey-migration/content-transfer-tool/assets/CTTvalidationlogs.png)

以下を使用： **発行/作成者の検証レポート** ボタンを使用して、ターゲット環境の特定の層に対する最新の取り込みの検証レポートを表示します。 小規模なパブリッシュ取り込みの例を以下に示します。

![画像](/help/journey-migration/content-transfer-tool/assets/CTTvalidationreport.png)

>[!NOTE]
>
>この **発行/作成者の検証レポート** リンクは、取り込みが完了すると表示されます。 また、検証レポートは持続されるので、取り込みログと同様に、取り込みが完了した後で期限切れになることはありません。

## トラブルシューティング {#troubleshooting}

### 検証できませんでした。次は何をすればよいでしょうか。 {#validation-fail}

最初の手順は、取り込みが実際に失敗したか、または抽出したコンテンツが既にターゲット環境に存在するかを判断することです。 これは、 **取り込み前にクラウドインスタンス上の既存のコンテンツを消去** オプションが無効です。

検証するには、検証レポートからパスを選択し、ターゲット環境にパスが存在するかどうかを確認します。 この環境がパブリッシュ環境の場合、ページやアセットを直接確認することに制限される場合があります。 この手順に関するサポートが必要な場合は、カスタマーケアにチケットを開いてください。

### ノード数が予想より少ない。 なぜ？ {#node-count-lower-than-expected}

抽出および取り込みのダイジェストからの一部のパスは、これらのファイルのサイズを管理しやすくする目的で除外され、取り込みが完了してから 2 時間以内に移行の検証結果を計算できるようになります。

現在ダイジェストから除外しているパスは次のとおりです。 `cqdam.text.txt` レンディション、内のノード `/home`、および内のノード `/jcr:system`.




