---
title: ソースからのコンテンツの抽出
description: ソースからのコンテンツの抽出
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 5075482f48bf9aaf2c7386af74c14a50b4469840
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 56%

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
>Amazon S3、Azure Data Store、またはファイルデータストアをデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、抽出段階を大幅に高速化できます。 事前コピー手順は、最初の完全な抽出および取り込みに最も効果的です。 それには、抽出を実行する前に `azcopy.config` ファイルを設定する必要があります。詳しくは、[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照してください。

>[!IMPORTANT]
>ソースからコンテンツを抽出する前に、ユーザーマッピングツールを実行する必要があります。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=ja)を参照してください。

1. **コンテンツ転送**&#x200B;ウィザードで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >!![IMPORTANT]
   抽出キーが有効で、有効期限に近づいていないことを確認します。 有効期限が近い場合は、移行セットを選択して「プロパティ」をクリックすることで、抽出キーを更新できます。 クリック **更新**. Cloud Acceleration Manager が表示され、 **抽出キーをコピー**. をクリックするたびに **抽出キーをコピー**に設定すると、新しい抽出キーが生成され、作成日から 14 日間有効です。
   [!画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 抽出ダイアログが表示されます。 クリック **抽出** をクリックして、抽出段階を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
抽出段階でステージングコンテナを上書きするオプションがあります。 If **ステージングコンテナを上書き** が無効になっている場合、コンテンツパスやインクルードバージョンの設定が変更されていない後続の移行で、抽出を高速化できます。 ただし、コンテンツのパスまたはコンテンツを含むバージョン設定が変更されている場合、 **ステージングコンテナを上書き** を有効にする必要があります。

   >[!IMPORTANT]
ソースからコンテンツを抽出する前に、この移行セットでユーザーマッピングが実行されていない場合は、上の図に示すように、ユーザーマッピング手順が保留中であることを示す警告が表示されます。 「**ユーザーをマッピング**」をクリックして、ユーザーマッピングツールを実行します。

1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   次をクリックできます。 **進行状況を表示** を使用して、進行中の抽出の詳細を把握できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   また、コンテンツ転送ページに移動して、Cloud Acceleration Manager で抽出段階の進行状況を監視することもできます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 抽出が完了したら、次のような他の列を確認します。 **ソース** および **パス** をクリックして入力した移行セットの詳細を表示するには、 **...** そしてそれから **詳細を表示**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。最初の完全抽出に対してコピー前の手順を使用した場合は、プロセス全体に時間がかかる可能性があるので、後続の追加抽出に対しては（追加移行セットのサイズが 200GB 未満の場合）プリコピーをスキップできます。
さらに、最初の抽出を実行した時点から、追加抽出を実行する時点まで、既存コンテンツのコンテンツ構造が変わらないことが不可欠です。最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行プロセス中は、必ずこの制限を実施してください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。

次の手順に従います。

1. **コンテンツ転送** ウィザードに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. **移行セットの抽出**&#x200B;ダイアログボックスが表示されます。「**抽出**」をクリックします。

   >[!IMPORTANT]「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 次の手順 {#whats-next}

コンテンツ転送ツールでソースからコンテンツを抽出する方法について理解したら、コンテンツ転送ツールでの取り込みプロセスについて学ぶ準備が整いました。コンテンツ転送ツールから移行セットを取り込む方法については、[Target へのコンテンツの取り込み](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)を参照してください。
