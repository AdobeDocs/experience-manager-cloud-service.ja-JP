---
title: Cloud Manager 2025.4.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.4.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 0712ba8918696f4300089be24cad3e4125416c02
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.4.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.4.0 のリリースについて説明します。


[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.4.0 のリリース日は 2025年4月10日木曜日（PT）です。

次回のリリース予定は 2025年5月8日木曜日（PT）です。

## 新機能 {#what-is-new}

* **（UI）デプロイメントの表示の向上**

  Cloud Manager のパイプライン実行の詳細ページに、デプロイメントが別のデプロイメントの完了を待機している際に、ステータスメッセージ（「*待機中 - その他の更新中*」）が表示されるようになりました。このワークフローにより、環境のデプロイメント中にシーケンスの理解が容易になります。<!-- CMGR-66890 -->

  ![詳細と分類を表示する開発デプロイメントダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **（UI）ドメイン検証の機能強化**

  ドメインを追加する際に、ドメインが既に Fastly アカウントにインストールされている場合、Cloud Manager に次のエラーが表示されるようになりました。「*ドメインは既に Fastly アカウントにインストールされています。Cloud Service に追加する前に、まずここから削除してください。*」

## 早期導入プログラム {#early-adoption}

Cloud Manager の早期導入プログラムに参加すると、一般リリース前に今後の機能に排他的にアクセスできます。

現在、次の早期導入の機会が利用可能です。

### 独自の Git の導入 - GitLab と Bitbucket をサポートするようになりました。 {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**独自の Git の導入**&#x200B;機能が拡張され、GitLab や Bitbucket などの外部リポジトリのサポートが含まれるようになりました。 この新しいサポートは、プライベートおよびエンタープライズ GitHub リポジトリに対する既存のサポートに追加されます。 これらの新しいリポジトリを追加すると、パイプラインに直接リンクすることもできます。 これらのリポジトリは、パブリッククラウドプラットフォーム上や、プライベートクラウドまたはインフラストラクチャ内でホストできます。 また、この統合により、Adobe リポジトリと常にコード同期を行う必要がなくなり、プルリクエストをメイン分岐に結合する前に検証できるようになります。

外部リポジトリ（GitHub でホストされているリポジトリを除く）を使用するパイプラインと、**Git 変更時**&#x200B;に設定した&#x200B;**デプロイメントトリガー**&#x200B;が自動的に開始されるようになりました。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>現在、標準のプルリクエストコード品質チェックは、GitHub でホストされるリポジトリ専用ですが、この機能を他の Git ベンダーに拡張する更新が進行中です。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) にメールを送信します。 使用する Git プラットフォームと、プライベート／パブリックまたはエンタープライズリポジトリ構造のいずれを使用するかを必ず含めてください。

### AEM ホーム {#aem-home}

AEM ホームでは、Adobe Experience Manager 内でコンテンツ、アセット、サイトを管理する一元的な開始点が導入されています。パーソナライズされたエクスペリエンスを提供するように設計された AEM ホームを使用すると、役割と目標に応じて AEM エコシステムをシームレスに操作できます。ガイドとして機能し、目的を効率的に達成するのに役立つ重要なインサイトと推奨されるアクションを提供します。AEM ホームは、明確でペルソナ主導型のレイアウトにより、重要なツールにすばやくアクセスでき、すべての AEM 機能にわたって効率化された効果的なエクスペリエンスをサポートします。

早期導入者が使用できる AEM ホームは、ワークフローの改善、目標の優先順位付け、結果の提供に焦点を当てた最適化されたエクスペリエンスを提供します。オプトインすると、AEM ホームの今後を形成し、AEM コミュニティ全体の価値を高めるフィードバックを提供することで、AEM ホームの開発に影響を与えることができます。

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) にメールを送信してください。次の情報を必ず含めてください。

* プロファイルに最適な役割：コンテンツ作成者、開発者、ビジネス所有者、管理者、その他（説明を入力）。
* プライマリ AEM アクセスサーフェス：AEM Sites、AEM Assets、AEM Forms、Cloud Manager、その他（説明を入力）。

## バグ修正

* **証明書に「共通名（CN）」フィールドが欠落している問題**

  Cloud Manager では、「サブジェクト」フィールドに共通名（CN）が含まれていない EV/OV 証明書を処理する際に、NullPointerException（NPE）および 500 HTTP 応答をスローしなくなりました。最新の証明書では、多くの場合、CN が省略され、代わりにサブジェクト代替名（SAN）が使用されます。この修正により、SAN が存在する場合に CN が存在しないことで設定ビルドプロセス中に障害が発生しなくなりました。<!-- CMGR-67548 -->

* **証明書の一致が正しくない場合のドメイン検証の問題**

  Cloud Manager では、間違った証明書を使用してドメインを誤って検証しなくなりました。以前は、検証ロジックで完全一致ではなくパターンベースの一致が使用されていたので、`should-not-be-verified.example.com` などのドメインは `example.com` の有効な証明書との重複により検証済みとして表示されていました。この修正により、ドメイン検証で完全一致が確認され、エラーのある証明書の関連付けが防止されるようになりました。<!-- CMGR-67225 -->

* **高度なネットワークポート転送名の一意性の適用**

  Cloud Manager では、高度なネットワークポート転送に一意の名前が適用されるようになりました。以前は、重複する名前が許可されていたので、競合が発生する可能性がありました。この修正により、ネットワーク設定の整合性に関するベストプラクティスに合わせて、各ポート転送エントリに個別の名前が付けられます。<!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

