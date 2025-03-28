---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 32%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース X {#X}

2025 年 4 月 1 日に公開された、メンテナンスリリース X の継続的な改善点を以下にまとめます。 前回のメンテナンスリリースは、リリース 19823 でした。

2025.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-X}

FORMS-19068: フォームデータの統合機能を強化するために、Forms Manager API でAEP コネクタの送信アクションがサポートされるようになりました。

FORMS-18513: AEP コネクタにデータツリー変換のサポートを実装して、ウィザード機能とデータ処理機能を強化しました。

FORMS-18432: フォーム固有の（正規表現ベースの）クライアントサイドの事前入力設定が実装されて、OSGI レベルを変更せずに選択的に事前入力機能が有効になりました。

FORMS-17551:SharePoint リスト統合でレコードのドキュメント（DoR）がサポートされるようになりました。

### 修正された問題 {#fixed-issues-X}

FORMS-19028：クライアントサイドの事前入力機能により、フォームイベントの処理が中断され、値の commit イベントや DOMContentLoaded イベントがフォーム読み込み時に正しくトリガーされない。

FORMS-18360: SharePoint Document Management でチームサイトのForms リスト範囲の管理を強化して、データ編成とアクセス制御を改善しました。

FORMS-18325: フォームデータの統合機能と処理機能を強化するためにAdobe Experience Platform（AEP）クラウド設定を追加しました。

FORMS-18213：レコードのドキュメント（DoR）から無効なフィールドを非表示/除外する機能が実装され、ドキュメントの明確さとユーザーエクスペリエンスが向上しました。

FORMS-18189：空のクライアントライブラリのエラーがログに記録されないようにし、UI でのエラー表示を改善するために、カスタム関数処理を変更。

FORMS-18426：リスト名に特殊文字（「–」など）が含まれていると、SharePoint リストとのフォームの統合に影響し、SharePoint リスト検索機能が失敗します。

FORMS-18375：特定の設定コンテナが選択されていない場合、基盤コンポーネントベースのフォームで `conf/global` フォルダーから recaptcha 設定が誤って選択される。

FORMS-18304:Acrobatおよび LiveCycle ES4 で検証に成功したPDF/A-1b ドキュメントは、デバイス依存のカラーエラーが原因で、AEM 6.5 Formsで誤って非準拠としてフラグ付けされます。

FORMS-18271:Forms テーマエディターにローカライズされていないエラーメッセージが表示され、フォーム設定やテーマのカスタマイズのユーザーエクスペリエンスに影響する。

FORMS-18068：リッチテキストフィールドを使用するラジオボタンおよびチェックボックスグループのレコードのドキュメント（DoR）で、太字テキストレンダリングの問題が発生する。

FORMS-7016：フォームエディターのキーボードフォーカスの順序が、論理的なナビゲーションに従わない。

FORMS-6950：スクリーンリーダーのアクセシビリティを向上し、WCAG 4.1.2 の名前、役割、値（レベル A）の標準に準拠するために、必要な ARIA ロールと属性がファイルシステムナビゲーターツリービューコンポーネントに追加されました。

### 既知の問題 {#known-issues-X}

なし。

### 廃止された機能と API {#deprecated-X}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-X}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースは、X で特定された脆弱性に対処し、堅牢なシステム保護への取り組みを強化するものです。

### 組み込みテクノロジー {#embedded-tech-X}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
