---
title: ソースからのコンテンツの抽出
description: ソースからのコンテンツの抽出
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---

# ソースからのコンテンツの抽出 {#extracting-content}

## コンテンツ転送ツールの抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース AEM インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。移行セットは、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#top-up-extraction-process" text="追加抽出"


コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。
>[!NOTE]
>Amazon S3 または Azure データストアをデータストアのタイプとして使用する場合は、オプションの事前コピーステップを実行して、抽出段階を大幅に迅速化できます。それには、抽出を実行する前に `azcopy.config` ファイルを設定する必要があります。詳しくは、[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照してください。

>[!IMPORTANT]
>ソースからコンテンツを抽出する前に、ユーザーマッピングツールを実行する必要があります。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=ja)を参照してください。

1. **コンテンツ転送**&#x200B;ウィザードで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されるので、「**抽出**」をクリックして抽出段階を完了します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >抽出段階では、ステージングコンテナを上書きするオプションがあります。

   >[!IMPORTANT]
   >この移行セットに対してユーザーマッピングを実行しないでソースからコンテンツを抽出すると、ユーザーマッピングステップが保留中であることを示す警告が表示されます（下図を参照）。「**ユーザーをマッピング**」をクリックして、ユーザーマッピングツールを実行します。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   抽出が完了すると、移行セットのステータスが&#x200B;**完了**&#x200B;に更新され、*緑で塗りつぶされた*&#x200B;雲のアイコンが「**情報**」フィールドに表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI には自動リロード機能があり、30 秒ごとに&#x200B;**コンテンツ転送**ウィザードをリロードします。
   >抽出フェーズが開始されると、書き込みロックが作成され、*60 秒*&#x200B;後に解放されます。したがって、抽出が停止した場合は、ロックが解除されるまで 1 分待ってから、抽出を再開する必要があります。

## 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。
>さらに、最初の抽出を実行した時点から、追加抽出を実行する時点まで、既存コンテンツのコンテンツ構造が変わらないことが不可欠です。最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行プロセス中は、必ずこの制限を実施してください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。

次の手順に従います。

1. **コンテンツ転送** ウィザードに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。「**抽出**」をクリックします。

   >[!IMPORTANT]
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >![画像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## 次の手順 {#whats-next}

コンテンツ転送ツールでソースからコンテンツを抽出する方法について理解したら、コンテンツ転送ツールでの取り込みプロセスについて学ぶ準備が整いました。コンテンツ転送ツールから移行セットを取り込む方法については、[Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。
