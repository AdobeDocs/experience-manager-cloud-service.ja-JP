---
sub-product: AEM as a Cloud Service のオンボーディング
user-guide-title: AEM as a Cloud Service のオンボーディング
breadcrumb-title: オンボーディングガイド
user-guide-description: このガイドでは、アクセス方法、データ保護に関する重要な情報など、Adobe Experience Manager as a Cloud Service の基本について概要を説明します。
translation-type: tm+mt
source-git-commit: d1301d4414f87b30f5ab732eacbb61c96f102262
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 66%

---


# オンボーディング {#onboarding}

+ [AEM as a Cloud Service のオンボーディング](/help/onboarding/home.md)
+ 要件 {#what-is-required}
   + [アクセス権の付与](what-is-required/access-rights-granted.md)
   + [ユーザーとロールの追加](what-is-required/add-users-roles.md)
   + [役割に基づく権限](what-is-required/role-based-permissions.md)
   + [ソースコードリポジトリ](what-is-required/source-code-repository.md)
+ クラウド内の AEM へのアクセス {#getting-access}
   + [Adobe Experience Manager as a Cloud Service へのアクセス](getting-access-to-aem-in-cloud/navigation.md)
   + Cloud Service のプログラム {#cloud-service-programs}
      + [プログラムへのアクセス](getting-access-to-aem-in-cloud/first-time-login.md)
      + [プログラムとプログラムの種類について](getting-access-to-aem-in-cloud/understand-program-types.md)
      + [プログラムの作成](getting-access-to-aem-in-cloud/creating-a-program.md)
      + [サンドボックスプログラム](getting-access-to-aem-in-cloud/sandbox-programs.md)
   + Cloud Manager の使用 {#using-cloud-manager}
      + [環境の管理](/help/implementing/cloud-manager/manage-environments.md)
      + [CI/CD パイプラインの設定](/help/implementing/cloud-manager/configure-pipeline.md)
      + [コードのデプロイ](/help/implementing/cloud-manager/deploy-code.md)
   + テスト結果について {#test-results}
      + [概要](/help/implementing/cloud-manager/overview-test-results.md)
      + [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)
      + [カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)
      + [機能テスト](/help/implementing/cloud-manager/functional-testing.md)
      + [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)
   + [ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)
   + [通知について](/help/implementing/cloud-manager/notifications.md)
   + AEM アプリケーションプロジェクトの作成 {#create-application-project}
      + [ウィザードの使用](getting-access-to-aem-in-cloud/using-the-wizard.md)
      + [プロジェクトの設定](getting-access-to-aem-in-cloud/setting-up-project.md)
      + [ビルド環境について](getting-access-to-aem-in-cloud/build-environment-details.md)
   + SSL証明書の管理{#manage-ssl-certificates}
      + [概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
      + [SSL証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)
      + [SSL証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
      + [SSL証明書の表示と更新または置き換え](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
      + [SSL証明書のステータスの確認](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md)
      + [SSL証明書の削除](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
   + カスタムドメイン名の管理{#custom-domain-names}
      + [概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
      + [カスタムドメイン名の取得](/help/implementing/cloud-manager/custom-domain-names/get-custom-domain-name.md)
      + [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
      + [TXTレコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)
      + [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)
      + [DNS設定の構成](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)
      + [DNSレコードの状態を確認しています](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)
      + [カスタムドメイン名の表示と更新](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)
      + [カスタムドメイン名のSSL証明書の更新](/help/implementing/cloud-manager/custom-domain-names/update-cdn-ssl-certificate.md)
      + [カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)
   + IP許可リストの管理{#ip-allow-lists}
      + [概要](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)
      + [IP許可リストの追加](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
      + [IP許可リストの表示と更新](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
      + [IP許可リストの適用](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
      + [IP許可リストの適用の解除](/help/implementing/cloud-manager/ip-allow-lists/unapply-ip-allow-list.md)
      + [IP許可リストの削除](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
      + [IP許可リストのステータスの確認](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)
   + [Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
   + Cloud Manager {#release-notes-cloud-manager}のリリースノート
      + [最新のリリースノート（2020.12.0）](/help/onboarding/release-notes-cloud-manager/release-notes-cm-current.md)
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
+ 移行手法{#migration-methodology}
   + [Cloud ServiceとしてのAdobe Experience Manager移住](migration-methodology/getting-started.md)
+ ベストプラクティス {#best-practices}
   + [SEO と URL の管理](best-practices/seo-and-url-management.md)
+ [ツールコンソールの概要](tools-consoles.md)
