---
title: コンテンツ移行後のインデックス作成
description: 移行プロセスで、宛先 Cloud Service インスタンスで取り込んだコンテンツのインデックスを作成する方法を説明します。
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
source-git-commit: 58195fcb10312c89042f555665d4c8b3642f82ba
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 57%

---

# コンテンツ移行後のインデックス作成 {#Indexing-content}

## インデックス作成 {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="コンテンツのインデックス作成"
>abstract="AEM のインデックス作成とは、Cloud Service インスタンスにコンテンツを移行した後の、Cloud Service インスタンス上のコンテンツのインデックス作成を指します。インデックス作成は、そのインスタンスでのコンテンツの検索をサポートするために必要です。"

Cloud Acceleration Manager がコンテンツの Cloud Service インスタンスへの取り込みを完了すると、コンテンツの使用準備が整います。最初は、コンテンツのインデックスが作成されず、不安定な環境に陥り、検索不可能なコンテンツやパフォーマンスの低下などの問題が予想される可能性があります。 インスタンスのパフォーマンスを最適化するために、移行プロセスはコンテンツのインデックス作成を自動的に開始します。インデックス作成の進行状況を監視する以外は、実行することはありません。

> 取り込みの開始方法について詳しくは、[Cloud Service へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。

以下の手順は、インデックス作成中に UI で期待できる一般的なフローを示しています。一部のラベルはツールチップで便利なコンテキストを提供するので、項目の上にマウスポインターを置いて、現在のインデックス作成状態の詳細を確認してください。

開始するには、Cloud Acceleration Manager に移動します。プロジェクトカードをクリックし、次に、コンテンツ転送カードをクリックします。に移動します。 **取り込みジョブ** リストに表示されているジョブを確認します。

>[!NOTE]
>インデックス作成ログを表示またはダウンロードするには、取り込みジョブのアクションの「...」ドロップダウンリストを使用します。インデックス作成ジョブが完了すると、このログは
> 「インデックス作成ログ」アクションセクションで利用できるようになります

### 保留

取り込みジョブが開始される前に、取り込み実行中に取り込みジョブの行がこのように表示されます。ユーザーからのアクションは必要ありません。 何らかの理由で取り込みが失敗した場合、インデックスジョブのキューは取り消され、開始されません。

![画像](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### 実行中

取り込みが成功すると、インデックス作成ジョブが自動的に開始されます。取り込みジョブ行には、AEMのインデックス作成ステータスの進行状況アイコンが表示されます。 期間ダイアログを開いて、ジョブの進行状況を確認できます。

![画像](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### 完了

インデックス作成ジョブが成功すると、インスタンスは最適なパフォーマンスで使用できる状態になります。この時点で、インデックス作成ジョブログを表示またはダウンロードして、ジョブを調べることができます。

![画像](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### エラー

宛先 Cloud Service インスタンスのインデックス作成は、成功する可能性が高いでしょう。場合によっては、失敗し、取り込みジョブ行が次のように表示されることがあります。 どの場合でも、失敗のステータスの上にマウスポインターを置くと、失敗の詳細を確認でき、次の手順を判断するのに役立つ詳細情報が表示される場合があります。 この時点で、インデックス作成ジョブのログを表示またはダウンロードして、失敗の原因を見つけることができます。 次の手順が明確でない場合は、取り込みとインデックス作成ログの詳細をAdobeサポートに問い合わせてください。

>[!TIP]
>
> インデックス作成ジョブが長すぎるような場合は、 [IP許可リストに加えるが適用されていません](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) Cloud Acceleration Manager を使用すると、Cloud Acceleration Manager が移行サービスに到達するのをブロックします。

![画像](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## 次の手順 {#whats-next}

宛先クラウドサービスインスタンスのインデックスが作成されたら、インデックス作成ジョブのログを表示し、詳細とエラーを探すことができます。

移行が完了しました。宛先クラウドサービスインスタンスのテストと検証を開始できます。
