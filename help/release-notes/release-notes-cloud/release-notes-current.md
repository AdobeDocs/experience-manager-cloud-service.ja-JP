---
title: Cloud Serviceの2020.8.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.8.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: fe2439e506f84a191922416e9c99b496fd90016c
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 9%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

Experience Manager as a Cloud Service 2020.8.0 の一般的なリリースノートの概要を次に説明します。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.8.0 のリリース日は 2020 年 8 月 06 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」は、Cloud Managerサイト実稼働パイプラインで有効になる機能です。 Sitesを使用するプログラムの実稼働パイプライン設定に、「 **Content Audit**」という名前の3番目のタブが含まれるようになりました。 実稼働パイプラインを実行するたびに、カスタム機能テストの後、新しいContent Auditステップがパイプラインに含まれます。このステップは、パフォーマンス、SEO(Search Engine Optimization)、アクセシビリティ、ベストプラクティス、PWA(Progressive Web App)など、多数の次元に対してサイトを評価します。

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* アセットプログラムーで新しく作成した環境が、Smart Content Servicesで自動的に設定されるようになりました。

* 休止状態の環境は、Cloud Managerの概要ページで非冬眠にすることができます。

* 認証バウンドのプライベートMavenリポジトリがサポートされるようになりました。

### バグ修正 {#bug-fixes-cm}

* 不要で望ましくない一部のSonarQubeプラグインが、コード品質スキャンの一部として実行されていました。

* パイプラインの実行ページで、ブランチ名の形式が正しくありませんでした。

* 完了したパイプライン実行が正常に完了したと記録されなかったため、パイプラインの新しい実行が行われない場合がありました。

* 内部通信の問題が原因で、パイプライン実行が「停止」する場合があります。

* 新しい組織をプロビジョニングすると、システム管理者以外の管理者ロールを持つ一部のユーザーに、誤ってCloud Managerへのアクセス権が与えられました。

* 特定の条件下で、更新インデックスジョブが複数回並行して開始され、展開エラーが発生しました。

* プログラムカードのツールチップが、一貫して正しくなかった。

* ユーザーインターフェイスで、削除中に環境に対して操作を試行することが誤って許可されました。

* 概要ページで色が一致していません。

### 既知の問題 {#known-issues}

* 無効なページは、コンテンツ監査平均スコアが本来の値を下回る場合に含まれます。

* 「コンテンツ監査」タブに、発行ドメインではなく作成者ドメインを使用したベースURLが正しく表示されません。

* コンテンツ監査手順をアクティブにするには、ユーザーはパイプラインを編集し、必要に応じてページを追加する必要があります。 ページが追加されない場合、ホームページは監査されます。

