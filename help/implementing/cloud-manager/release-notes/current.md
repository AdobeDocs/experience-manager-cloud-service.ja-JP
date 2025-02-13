---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.2.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2025.2.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: c2a0961cae6d36d8ea3116c6e7982889257f90c8
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 35%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.2.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.2.0 のリリースについて説明します。


[Adobe Experience Manager as a Cloud Serviceの最新のリリースノート ](/help/release-notes/release-notes-cloud/release-notes-current.md) も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.2.0 のリリース日は 2025年2月13日木曜日（PT）です。

次回のリリース予定は 2025年3月13日木曜日（PT）です。

## 新機能 {#what-is-new}

* **コード品質ルールを更新します。**
2025 年 2 月 13 日木曜日（PT）より、Cloud Manager コード品質ステップで、アップグレードされた SonarQube バージョン 9.9.5.90363 が使用されるようになりました。

  [このリンク](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)の AEM as a Cloud Service での Cloud Manager に使用可能な更新されたルールにより、Cloud Manager パイプラインのセキュリティスコアとコード品質が決定されます。この更新は、品質ゲートに影響を与え、デプロイメントをブロックする可能性があります。

* **Java 17 および Java 21 ビルドのサポート。**

  お客様は Java 17 または Java 21 を使用してビルドできるようになり、パフォーマンスの強化や新しい言語機能にアクセスできます。 Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)を参照してください。ビルドバージョンを Java 17 または Java 21 に設定した際、デプロイされるランタイムは Java 21 です。

   * **機能の有効化**
      * この機能は、新しい SonarQube バージョンのデフォルトのロールアウトと同時に、2025年2月13日木曜日（PT）にすべてのお客様に対して有効になります。
      * お客様は、SonarQube 9.9 バージョンをアップグレードするために、上記の 2 つの変数設定を行って、*直ちに*&#x200B;有効にすることができます。

   * **Java 21 ランタイムのデプロイメント**
      * Java 17 または Java 21 を使用してビルドすると、Java 21 ランタイムがデプロイされます。
      * すべての Cloud Manager 環境への段階的なロールアウトは、サンドボックスと開発環境向けに 2月に開始され、4月には実稼動環境に拡張されます。
      * Java 11 を使用してビルドし、Java 21 ランタイムを&#x200B;*早期*&#x200B;に導入するお客様は、アドビ（[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)）にお問い合わせください。

* Edge Delivery Servicesの稼動時間レポートの **99.99%。**
対象となるEdge Delivery Services プログラムで、99.99% の高可用性の稼動時間レポートが利用できるようになりました。 この機能を有効にするには、Edge Delivery Services サイトを正常にオンボーディングし、99.99% Service level agreement（SLA）をCloud Manager内に適用する必要があります。

  [SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) も参照してください。

* **Edge Delivery Servicesのユーザー招待エクスペリエンスが向上しました。**
Edge Delivery Servicesに関連付けられたコンテンツリポジトリーにユーザーを招待する際の操作性が向上しました。<!-- CMGR-65331 -->

* **パブリッシュインスタンスでの管理者プロファイルの自動作成。**
以前は、Cloud Managerでは、パブリッシュインスタンス上に管理者プロファイルを手動で作成できましたが、デフォルトでは自動作成はサポートされていませんでした。 この更新により、パブリッシュインスタンスで管理プロファイルが自動的に作成されるようになり、ユーザビリティが向上し、顧客の設定時間が短縮されました。

  詳しくは、[ カスタム権限 ](/help/implementing/cloud-manager/custom-permissions.md) を参照してください。

  ![パイプラインアクティビティフィルタリング](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **Cloud Service環境向けの OAuth への移行**
新しいCloud Service環境では、以前に使用されていた JWT 認証方法の代わりに、Adobe Developer Console統合プロジェクトに対して、OAuth ベースのサービス間認証を使用するようになりました。 JWT 認証は非推奨（廃止予定）となり、2025 年 6 月に提供終了になる予定です。

* **EC （楕円曲線）秘密鍵（secp384r1）のサポート。**
Cloud Managerは `secp384r1` 楕円曲線（EC）秘密鍵をサポートするようになり、顧客管理の OV/EV SSL 証明書のセキュリティとコンプライアンスを向上させます。
詳しくは、[ 顧客が管理する OV/EV SSL 証明書の要件 ](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) を参照してください。<!-- CMGR-63636 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## バグ修正

* **（UI）Cloud Managerで、ドメインの CDN 設定ができない問題を修正しました。**
Cloud Managerで CDN 設定を追加しようとすると、ドロップダウンメニューからドメインを選択した際に画面エラーが発生しました。 このユーザーインターフェイスのバグにより、実稼動環境でのドメインマッピングが妨げられ、設定プロセスがブロックされていました。

  さらに、ユーザーインターフェイスから削除されているにもかかわらず、一部のドメインはバックエンドでアクセスできないままでした。 この問題は、既存の CDN 設定との競合を引き起こしました。

  この修正により、エラーを発生させずに、ドロップダウンからドメインを正常に選択できるようになりました。 ドメインの再設定を妨げるバックエンドの不整合は解決されました。 最後に、検証の改善により、競合するドメインを再追加する前に、適切に削除できるようになりました。<!-- CMGR-64888 -->
* **（バックエンド） SSL の有効期限通知が複数回送信される問題を修正しました。**
午前 0 時に 1 日 1 回実行するように設計されている SSL 有効期限通知スケジューラーが、1 日 2 回、午前 0 時と午前 12 時 30 分に誤ってトリガーされていたバグが特定されました。 この問題により、SSL 証明書の有効期限に関する複数の冗長な通知が送信されていました。

  通知スケジューラーは、意図したとおりに 1 日に 1 回だけ正しく実行されるようになりました。 また、SSL の重複する有効期限切れ通知を受け取らなくなりました。<!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
