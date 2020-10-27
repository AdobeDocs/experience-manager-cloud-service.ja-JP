---
title: Cloud Serviceリリース2020.8.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.8.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 18%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.8.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.8.0のリリース日は2020年8月7日です。

## 新機能 {#whats-new-cloud-manager}

* 「コンテンツ監査」は、Cloud Managerサイト実稼働パイプラインで有効になる機能です。 Sitesを使用するプログラムの実稼働パイプライン設定に、「 **Content Audit**」という名前の3番目のタブが含まれるようになりました。 実稼働パイプラインを実行するたびに、カスタム機能テストの後、新しいContent Auditステップがパイプラインに含まれます。このステップは、パフォーマンス、SEO(Search Engine Optimization)、アクセシビリティ、ベストプラクティス、PWA(Progressive Web App)など、多数の次元に対してサイトを評価します。


   >[!NOTE]
   >「コンテンツ監査」は、「エクスペリエンス監査」に名称変更されました。

   Refer to [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md) for more details.

* アセットプログラムーで新しく作成した環境が、Smart Content Servicesで自動的に設定されるようになりました。

* 休止状態の環境は、Cloud Managerの **概要** ページで非冬眠にできます。

* Google Lighthouseによるページに対してエクスペリエンスチェックを実行する機能。 Cloud Managerのパイプラインの一部として、エクスペリエンスKPIに対して最大25のページをチェックして検証でき、スコアがCloud Manager UIに表示されます。

### バグ修正 {#bug-fixes-cm}

* 不要で望ましくない一部の SonarQube プラグインが、コード品質スキャンの一部として実行されていました。

* パイプラインの実行ページで、ブランチ名の形式が正しくありませんでした。

* 一部のケースで、パイプラインの実行完了が正常に記録されなかったため、パイプラインが新たに実行されないことがありました。

* 内部通信の問題が原因で、パイプラインの実行が&#x200B;*停止*&#x200B;することがあります。

* 新しい組織をプロビジョニングすると、システム管理者以外の管理者ロールを持つ一部のユーザーに、誤ってCloud Managerへのアクセス権が与えられました。

* 特定の条件下で、更新インデックスジョブが複数回並行して開始され、展開エラーが発生しました。

* プログラムカードのツールチップの一貫性が適切に保てていませんでした。

* ユーザーインターフェイスで、削除中に環境に対して操作を試行することが誤って許可されました。

* There was a color mismatch on the Cloud Manager&#39;s **Overview** page.

### 既知の問題 {#known-issues-cm}

* 無効なページは、コンテンツ監査平均スコアが本来の値を下回る場合に含まれます。

* 「コンテンツ監査」タブに、発行ドメインではなく作成者ドメインを使用したベースURLが正しく表示されません。

* コンテンツ監査手順をアクティブにするには、ユーザーはパイプラインを編集し、必要に応じてページを追加する必要があります。 ページが追加されない場合、ホームページは監査されます。