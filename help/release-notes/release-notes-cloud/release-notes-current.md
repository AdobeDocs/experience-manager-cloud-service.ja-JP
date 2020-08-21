---
title: Cloud Serviceの2020.8.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.8.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: 27f9f4441a95964a4ae0db798577510c726133c5
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 22%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

Experience Manager as a Cloud Service 2020.8.0 の一般的なリリースノートの概要を次に説明します。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* 新しい [!DNL Experience Manager Assets] 配置は、既定でと統合 [!DNL Adobe Developer Console] されます。 これにより、スマートタグ機能の設定を迅速に行うことができます。 既存のデプロイメントでは、管理者は以前と同様にスマートタグ統合 [](/help/assets/smart-tags-configuration.md#aio-integration) を設定します。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品コンソール機能が使用できるようになりました。 これにより、AEMのマーケターや作成者は、コマースバックエンドに保存されているカテゴリや製品を表示してナビゲートできます。 製品コンソールでのカテゴリおよび製品のプロパティのサポートも提供されました。

* 製品とカテゴリの選択機能が強化され、マーケティング担当者はSKUを使用して製品を選択したり、カテゴリIDを使用してカテゴリを選択したりできるようになりました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.8.0 のリリース日は 2020 年 8 月 06 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」は、Cloud Managerサイト実稼働パイプラインで有効になる機能です。 Sitesを使用するプログラムの実稼働パイプライン設定に、「 **Content Audit**」という名前の3番目のタブが含まれるようになりました。 実稼働パイプラインを実行するたびに、カスタム機能テストの後、新しいContent Auditステップがパイプラインに含まれます。このステップは、パフォーマンス、SEO(Search Engine Optimization)、アクセシビリティ、ベストプラクティス、PWA(Progressive Web App)など、多数の次元に対してサイトを評価します。

   Refer to [Content Audit Testing](/help/implementing/cloud-manager/content-audit-testing.md) for more details.

* アセットプログラムーで新しく作成した環境が、Smart Content Servicesで自動的に設定されるようになりました。

* 休止状態の環境は、Cloud Managerの **概要** ページで非冬眠にできます。


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

## コンテンツ転送ツール {#content-transfer-tool}

このセクションでは、新機能とコンテンツ転送ツールリリースv1.0.4の更新点について説明します。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールで共有S3 DataStoreがサポートされるようになりました。

### バグ修正 {#ctt-bug-fixes}

* アクションを完了するための追加のタイムアウトが追加されました。

* 以前のバージョンのUIで、ログにエラーが表示されていたにもかかわらず、正常に抽出されたことがありました。

