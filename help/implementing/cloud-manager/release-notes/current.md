---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.10.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2024.10.0 のリリースノートについて説明します。
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.10.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2024.10.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager リリース 2024.10.0 のリリース日は 2024年10月3日（PT）です。

次回のリリースは 2024年11月14日（PT）に予定されています。

## 新機能 {#what-is-new}

* <!-- BOTH CS & AMS --> Cloud Manager で使用される AEM アーキタイプバージョンがバージョン 26 に更新されました。[https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases) を参照してください

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> 新しいカスタムドメインの追加時、以前の検証方法では長い DNS 検証プロセスが必要でした。アドビは、お客様向けにこのプロセスを簡略化しました。現在は、所有権の証明として機能する有効な SSL 証明書（EV または OV）を指定するだけ済みます。DNS の TXT レコードを更新する必要はなくなりました。

  >[!NOTE]
  >
  >この機能は、お客様が管理する EV および OV 証明書にのみ適用されます。アドビが管理する DV 証明書には、引き続き CNAME レコードが必要です。

  [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。

  ![顧客が管理する EV/OV 証明書のドメイン検証](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> ネットワークインフラストラクチャを追加または編集する際、IP アドレスフィールドとネットワークマスクフィールドの値は、次のルールに従って検証されます。

   * アドレス空間は、接続アドレス空間で定義されているアドレスと重複しないようにする必要があります。
   * DNS アドレスは、接続アドレス空間で定義されているたネットワークマスクに属しているか、パブリックである必要があります。

  ![ネットワークインフラストラクチャを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> インデックス作成、可変コンテンツのインストール、およびジョブの変換のための環境デプロイメントログの形式が変更されています。

  >[!NOTE]
  >
  >この変更は、段階的にロールアウトされる予定で、完了予定日は 2024年12月です。

  ![実稼動カードへのデプロイ](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  ログの形式は、次に示す単純なエントリから変更されます。

  ![単純なエントリを表示するログファイル](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  次のような JSON エントリになります。

  ![JSON エントリを表示するログファイル](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## 早期導入プログラム {#early-adoption}

Cloud Manager の早期導入プログラムに参加すると、今後の機能をテストする機会を得ることができます。

### 独自の Git の導入 - GitLab と Bitbucket をサポートするようになりました {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**独自の Git の導入**&#x200B;機能が拡張され、GitLab や Bitbucket などの外部リポジトリのサポートが含まれるようになりました。この新しいサポートは、プライベートおよびエンタープライズ GitHub リポジトリに対する既存のサポートに追加されます。これらの新しいリポジトリを追加すると、パイプラインに直接リンクすることもできます。これらのリポジトリは、パブリッククラウドプラットフォーム上や、プライベートクラウドまたはインフラストラクチャ内でホストできます。また、この統合により、Adobe リポジトリと常にコード同期を行う必要がなくなり、プルリクエストをメイン分岐に結合する前に検証できるようになります。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>現在、標準のプルリクエストコード品質チェックは、GitHub でホストされるリポジトリ専用ですが、この機能を他の Git ベンダーに拡張する更新が進行中です。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) にメールを送信します。使用する Git プラットフォームと、プライベート／パブリックまたはエンタープライズリポジトリ構造のいずれを使用するかを必ず含めてください。


<!-- ## Bug fixes




## Known issues {#known-issues} -->
