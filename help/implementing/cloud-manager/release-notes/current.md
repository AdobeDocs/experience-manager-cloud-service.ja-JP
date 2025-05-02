---
title: Cloud Manager 2025.4.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.4.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 7ae9d2bb3cf6066d13567c54b18f21fd4b1eff9e
workflow-type: ht
source-wordcount: '614'
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

<!--
### AEM Home {#aem-home}

AEM Home introduces a centralized starting point for managing content, assets, and sites within Adobe Experience Manager. Designed to deliver a personalized experience, AEM Home lets you navigate the AEM ecosystem seamlessly according to your roles and goals. Acting as a guide, it provides key insights and recommended actions to help you achieve your objectives efficiently. With a clear, persona-driven layout, AEM Home ensures quick access to essential tools, supporting a streamlined and effective experience across all AEM features.

Available to early adopters, AEM Home offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence AEM Home's development by providing feedback that helps shape its future and enhances its value for the entire AEM community.

If you are interested in testing this new capability and sharing your feedback, send an email to [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) from your email address associated with your Adobe ID. Be sure to include the following information:

* The role that best fits your profile: Content author, Developer, Business owner, Admin, or Other (provide a description).
* Your primary AEM access surface: AEM Sites, AEM Assets, AEM Forms, Cloud Manager, or Other (provide a description). -->

## バグ修正

* **証明書に「共通名（CN）」フィールドが欠落している問題**

  Cloud Manager では、「サブジェクト」フィールドに共通名（CN）が含まれていない EV/OV 証明書を処理する際に、NullPointerException（NPE）および 500 HTTP 応答をスローしなくなりました。最新の証明書では、多くの場合、CN が省略され、代わりにサブジェクト代替名（SAN）が使用されます。この修正により、SAN が存在する場合に CN が存在しないことで設定ビルドプロセス中に障害が発生しなくなりました。<!-- CMGR-67548 -->

* **証明書の一致が正しくない場合のドメイン検証の問題**

  Cloud Manager では、間違った証明書を使用してドメインを誤って検証しなくなりました。以前は、検証ロジックで完全一致ではなくパターンベースの一致が使用されていたので、`should-not-be-verified.example.com` などのドメインは `example.com` の有効な証明書との重複により検証済みとして表示されていました。この修正により、ドメイン検証で完全一致が確認され、エラーのある証明書の関連付けが防止されるようになりました。<!-- CMGR-67225 -->

* **高度なネットワークポート転送名の一意性の適用**

  Cloud Manager では、高度なネットワークポート転送に一意の名前が適用されるようになりました。以前は、重複する名前が許可されていたので、競合が発生する可能性がありました。この修正により、ネットワーク設定の整合性に関するベストプラクティスに合わせて、各ポート転送エントリに個別の名前が付けられます。<!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

