---
sub-product: AEM as a Cloud Service のオンボーディング
user-guide-title: AEM as a Cloud Service のオンボーディング
breadcrumb-title: オンボーディングガイド
user-guide-description: このガイドでは、アクセス方法、データ保護に関する重要な情報など、Adobe Experience Manager as a Cloud Service の基本について概要を説明します。
feature-set: Experience Manager Sites
feature: デプロイ
role: アーキテクト、開発者
translation-type: tm+mt
source-git-commit: 974c7d20d7896b749e07b05d0149ed16dc7e0cd5
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 93%

---


# オンボーディング {#onboarding}

+ [AEM as a Cloud Service のオンボーディング](/help/onboarding/home.md)
+ Cloud ServiceとしてAEMを使い始める{#what-is-required}
   + [アクセス権の付与](what-is-required/access-rights-granted.md)
   + [役割に基づく権限](what-is-required/role-based-permissions.md)
   + [ソースコードリポジトリー](what-is-required/source-code-repository.md)
+ クラウド内の AEM へのアクセス {#getting-access}
   + [Cloud ServiceとしてのAEM版Cloud Managerへのアクセス](getting-access-to-aem-in-cloud/navigation.md)
   + Cloud Manager へのアクセス{#cloud-service-programs}
      + [Cloud Manager ランディングページ](getting-access-to-aem-in-cloud/first-time-login.md)
      + [プログラムとプログラムの種類について](getting-access-to-aem-in-cloud/understand-program-types.md)
      + 本番プログラム{#production-programs}
         + [概要](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)
         + [実稼働プログラムの作成](getting-access-to-aem-in-cloud/creating-production-program.md)
         + [実稼働プログラムの編集](/help/onboarding/getting-access-to-aem-in-cloud/editing-production-program.md)
      + サンドボックスプログラム {#sandbox-programs}
         + [概要](getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
         + [サンドボックスプログラムの作成](getting-access-to-aem-in-cloud/creating-sandbox-program.md)
         + [サンドボックスプログラムの編集](/help/onboarding/getting-access-to-aem-in-cloud/editing-sandbox-program.md)
         + [Sandboxプログラムの削除](getting-access-to-aem-in-cloud/deleting-sandbox-program.md)
         + [サンドボックス環境の休止と休止解除](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)
   + Cloud Manager の使用 {#using-cloud-manager}
      + [環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)
      + [CI/CD パイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=ja)
      + [コードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)
   + テスト結果について {#test-results}
      + [概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=ja)
      + [コード品質テスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/code-quality-testing.html?lang=ja)
      + [カスタムコード品質ルール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/custom-code-quality-rules.html?lang=ja)
      + [機能テスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=ja)
      + [エクスペリエンス監査テスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/experience-audit-testing.html?lang=ja)
   + [ログへのアクセスと管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja)
   + [通知について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/notifications.html?lang=ja)
   + AEM アプリケーションプロジェクトの作成 {#create-application-project}
      + [ウィザードの使用](getting-access-to-aem-in-cloud/using-the-wizard.md)
      + [プロジェクトの設定](getting-access-to-aem-in-cloud/setting-up-project.md)
      + [ビルド環境について](getting-access-to-aem-in-cloud/build-environment-details.md)
   + SSL 証明書の管理 {#manage-ssl-certificates}
      + [概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/introduction.html?lang=ja)
      + [SSL 証明書の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/get-ssl-certificate.html?lang=ja)
      + [SSL 証明書の追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=ja)
      + [SSL 証明書の表示、更新、置換](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html?lang=ja)
      + [SSL 証明書のステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html?lang=ja)
      + [SSL 証明書の削除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/delete-ssl-certificate.html?lang=ja)
   + カスタムドメイン名の管理 {#custom-domain-names}
      + [概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/introduction.html?lang=ja)
      + [カスタムドメイン名の取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/get-custom-domain-name.html?lang=ja)
      + [カスタムドメイン名の追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=ja)
      + [TXT レコードの追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=ja)
      + [カスタムドメイン名ステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=ja)
      + [DNS 設定の指定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=ja)
      + [DNS レコードのステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=ja)
      + [カスタムドメイン名の表示と更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html?lang=ja)
      + [カスタムドメイン名の SSL 証明書の更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/update-cdn-ssl-certificate.html?lang=ja)
      + [カスタムドメイン名の削除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/delete-custom-domain-name.html?lang=ja)
   + IP 許可リストの管理 {#ip-allow-lists}
      + [概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/introduction.html?lang=ja)
      + [IP 許可リストの追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=ja)
      + [IP 許可リストの表示と更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=ja)
      + [IP 許可リストの適用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=ja)
      + [IP 許可リストの適用解除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/unapply-ip-allow-list.html?lang=ja)
      + [IP 許可リストの削除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/delete-ip-allow-list.html?lang=ja)
      + [IP 許可リストのステータスの確認](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/check-ip-allow-list-status.html?lang=ja)
   + Cloud Manager のリリースノート {#release-notes-cloud-manager}
      + [最新のリリースノート（2021.3.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-current.md)
      + [リリースノート（2021.2.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2021-2-0.md)
      + [リリースノート（2021.1.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2021-1-0.md)
      + [リリースノート（2020.12.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-12-0.md)
      + [リリースノート（2020.11.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-11-0.md)
      + [リリースノート（2020.10.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-10-0.md)
      + [リリースノート（2020.9.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-9-0.md)
      + [リリースノート（2020.8.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-8-0.md)
      + [リリースノート（2020.7.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-7-0.md)
      + [リリースノート（2020.6.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-6-0.md)
      + [リリースノート（2020.5.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-5-0.md)
      + [リリースノート（2020.4.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-4-0.md)
      + [リリースノート（2020.3.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-3-0.md)
      + [リリースノート（2020.2.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-2020-2-0.md)
+ データのプライバシーと保護への対応 {#data-privacy}
   + [データ保護およびデータプライバシーに関する規制に対する AEM の対応](data-privacy-and-protection-readiness/aem-readiness.md)
   + [データ保護およびデータプライバシーに関する規制に対する AEM Foundation の対応](data-privacy-and-protection-readiness/foundation-readiness.md)
   + [データ保護およびデータプライバシーに関する規制に対する AEM Sites の対応](data-privacy-and-protection-readiness/sites-readiness.md)
+ アクセシビリティ {#accessibility}
   + [AEM as a Cloud Service と Web アクセシビリティのガイドライン](accessibility/web-accessibility.md)
   + [WCAG 2.1 クイックガイド](accessibility/quick-guide-wcag.md)
+ 移行手法 {#migration-methodology}
   + [Adobe Experience Manager as a Cloud Service への移行](migration-methodology/getting-started.md)
+ ベストプラクティス {#best-practices}
   + [SEO と URL の管理](best-practices/seo-and-url-management.md)
   + [KPIの評価](best-practices/assessing-kpis.md)
   + [KPIの調整](best-practices/aligning-kpis.md)
   + [適切なチームを選択](best-practices/choose-right-team.md)
+ [ツールコンソールの概要](tools-consoles.md)
