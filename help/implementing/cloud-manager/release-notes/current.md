---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.10.0 のリリースノート
description: AEM as a Cloud ServiceのCloud Manager 2024.10.0 のリリースノートについて説明します。
feature: Release Information
role: Admin
source-git-commit: b90ace2250277005d8ac250c841104c93298a605
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 15%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.10.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.10.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager リリース 2024.10.0 のリリース日は 2024 年 10 月 3 日（PT）です。

次回のリリースは 2024年11月14日（PT）に予定されています。

## 新機能 {#what-is-new}

* <!-- BOTH CS & AMS --> Cloud Managerで使用されるAEM アーキタイプのバージョンが、バージョン 26 に更新されました。 [https://github.com/adobe/aem-project-archetype/releasesを参照してください ](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> ネットワークインフラストラクチャを追加または編集すると、「IP アドレス」フィールドと「ネットワークマスク」フィールドの値は、次のルールに従って検証されます。

   * アドレス空間は、接続アドレス空間に定義されたアドレスと重複してはなりません。
   * DNS アドレスは、接続アドレス空間で定義されたネットワーク マスクに属するか、パブリックである必要があります。

  ![ ネットワークインフラストラクチャを追加ダイアログボックス ](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> インデックス作成、可変コンテンツのインストール、ジョブの変換のために、環境デプロイメントログの形式が変更されています。

  >[!NOTE]
  >
  >この変更は、2024 年 12 月の完了日を想定して、段階的にロールアウトされる予定です。

  ![ 実稼動カードにデプロイ ](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  ログの形式が、次に示すような単純なエントリから変更されます。

  ![ 単純なエントリを示すログファイル ](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  JSON エントリに対して行われる処理は次のとおりです。

  ![JSON エントリを示すログファイル ](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## 早期導入プログラム {#early-adoption}

Cloud Managerの早期導入プログラムに参加して、今後の機能をテストする機会を得ます。

### 独自の Git の導入 – GitLab と Bitbucket をサポート {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**独自の Git を取り込む** 機能が拡張され、GitLab や Bitbucket などの外部リポジトリがサポートされるようになりました。 この新しいサポートは、プライベートおよびエンタープライズ GitHub リポジトリの既存のサポートに加わるものです。 これらの新しいリポジトリを追加する際に、パイプラインに直接リンクすることもできます。 これらのリポジトリは、パブリッククラウドプラットフォーム上、またはプライベートクラウドやインフラストラクチャ内でホストできます。 また、この統合により、Adobeリポジトリとの継続的なコード同期が不要になり、メインブランチにマージする前にプルリクエストを検証できるようになります。

[Cloud Managerでの外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md) を参照してください。

![ リポジトリを追加ダイアログボックス ](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>現在、標準のプルリクエストコード品質チェックは、GitHub でホストされるリポジトリ専用ですが、この機能を他の Git ベンダーに拡張する更新が現在進行中です。

この新機能のテストやフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) にメールを送信してください。 使用する Git プラットフォームと、プライベート/パブリックまたはエンタープライズリポジトリ構造のいずれを使用しているかをを必ず含めてください。


<!-- ## Bug fixes




## Known Issues {#known-issues} -->
