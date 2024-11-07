---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.11.0 のリリースノート
description: AEM as a Cloud ServiceのCloud Manager 2024.11.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 29%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2024.11.0 のリリースノート {#release-notes}

AEM（Adobe Experience Manager）as a Cloud ServiceのCloud Manager 2024.11.0 のリリースについて説明します。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2024.11.0 のリリース日は 2024 年 11 月 7 日（PT）です。

次回の予定リリースは 2024 年 12 月 5 日（PT）です。

## 新機能 {#what-is-new}

* AEM Cloud Serviceの最新のEdge Delivery Servicesイノベーションを体験してください。サンドボックスプログラムで参照できるようになりました。 [ 詳細情報 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* AEM Cloud Managerのドメイン設定ページに、名前でドメインをすばやく見つけることができる検索機能が追加されました。 検索フィールドにキーワードを入力すると、一致するドメインをフィルタリングして表示できるので、複数のドメインを効率的に管理しやすくなります。 さらに、ページには、「検証済み **、「未検証** などのステータスフィルターが用意されており、検索結果をさらに絞り込む **ことができます**。<!-- (CMGR-62615) -->

![ ドメイン設定の「検索」フィールド ](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## 早期導入プログラム {#early-adoption}

Cloud Manager の早期導入プログラムに参加すると、今後の機能をテストする機会を得ることができます。

### AEM ホーム {#aem-home}

AEM ホームは、Adobe Experience Manager内のコンテンツ、アセット、サイトを管理するための新しい一元的な開始点です。 AEM ホームは、パーソナライズされたエクスペリエンスを提供するようにカスタマイズされており、ユーザーの役割と目標に基づいてAEM エコシステムをシームレスに移動するのに役立ちます。 ガイドとなるよう設計されており、望ましい結果を効率的に達成するための重要なインサイトと推奨されるアクションを提供します。 AEM ホームでは、明確なペルソナ駆動型のロードマップを提示することで、目的を達成するために必要な情報を素早く見つけ、すべてのAEM機能でより効率的で効果的なエクスペリエンスをサポートできます。

AEM ホームでは、早期導入のお客様が利用できる、ワークフローの最適化、目標の優先順位付け、結果の促進につながる強化されたエクスペリエンスをまず紹介します。 オプトインすると、AEM ホームの発展を形作り、AEM コミュニティに最適なサービスを提供するための進化に影響を与えるフィードバックを提供できます。

この新しい機能のテストおよびフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスから [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) にメールを送信してください。 必ず次の情報を含めてください。

* プロファイルに最適な役割：コンテンツ作成者、開発者、ビジネスオーナー、管理者、またはその他（説明を入力）。
* プライマリ AEM アクセスサーフェス：AEM Sites、AEM Assets、AEM Forms、Cloud Manager、またはその他（説明を入力）。

### 独自の Git の導入 - GitLab と Bitbucket をサポートするようになりました {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**独自の Git の導入**&#x200B;機能が拡張され、GitLab や Bitbucket などの外部リポジトリのサポートが含まれるようになりました。この新しいサポートは、プライベートおよびエンタープライズ GitHub リポジトリに対する既存のサポートに追加されます。これらの新しいリポジトリを追加すると、パイプラインに直接リンクすることもできます。これらのリポジトリは、パブリッククラウドプラットフォーム上や、プライベートクラウドまたはインフラストラクチャ内でホストできます。また、この統合により、Adobe リポジトリと常にコード同期を行う必要がなくなり、プルリクエストをメイン分岐に結合する前に検証できるようになります。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>現在、標準のプルリクエストコード品質チェックは、GitHub でホストされるリポジトリ専用ですが、この機能を他の Git ベンダーに拡張する更新が進行中です。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) にメールを送信します。使用する Git プラットフォームと、プライベート/パブリックまたはエンタープライズリポジトリ構造のいずれを使用しているかをを必ず含めてください。—>


## バグ修正

* 最近のアップデートでは、SonarQube で、特定のケースでハードコードされたパスワードが検出されない問題が修正されました。 この修正には、拡張されたパターンチェックが含まれ、SonarQube のデフォルトの検出標準に従っています。<!-- CMGR-62682 -->
* Cloud Managerで SSL 証明書を更新しようとすると、**[!UICONTROL SSL 証明書を表示および更新]** ダイアログボックスで **[!UICONTROL 更新]** をクリックすると、不明なエラーが表示されます。<!-- CMGR-62848 -->
* Cloud Managerで SSL 証明書を更新すると、ドメインが同じでも、文字の大文字と小文字が異なる場合でも、「新しい証明書は既存のドメインに一致しません」というエラーで失敗します。 更新では、RFC 標準に合わせて、ドメインが大文字と小文字を区別せずに認識されるようになりました。<!-- CMGR-62844 -->
* Cloud Managerでは、ドメイン設定への外部キーリンクがないので、IP 許可リストバインディングが実行中の状態のままでした。 この修正により、関連するドメイン設定への IP許可リストバインディングのリンクが正しくなるようになりました。<!-- CMGR-62838 -->
* Cloud Managerは、SSL 証明書の OCSP （Online Certificate Status Protocol）ステータスを検証します。 Adobeでは、Cloud Managerを通じてインストールする前に、`openssl verify -untrusted intermediate.pem certificate.pem` などのツールを使用して証明書の整合性をローカルで検証することもお勧めします。 詳しくは、[SSL 証明書の要件ドキュメント ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements) を参照してください。<!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->