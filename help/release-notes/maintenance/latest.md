---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e8ea040ba3f8c73d7ed64c9669ac1d0a22d3a3c8
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 20%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 12441 {#release-12441}

2023 年 6 月 27 日に公開されたメンテナンスリリース12441の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12255 からのアップデートです。

2023.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-12441}

- SITES-8769:ResponsiveGrid の StyleImpl 呼び出しを改善する
- Forms-5054:すべての [像](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) Adobe Signがサポート。

### 修正された問題 {#fixed-issues-12441}

- 各種アクセシビリティ関連の更新
- SITES-12688:ページエディター：アセットファインダー検索で論理演算子 OR が正しく機能しない
- SITES-4951:ページエディター：ページエディターでのタグ検索でサブタグが見つからない
- SITES-12465:エクスペリエンスフラグメント：エクスペリエンスフラグメントコンポーネントダイアログで矢印キーが機能しない
- SITES-12893:エクスペリエンスフラグメント：エクスペリエンスフラグメントに循環参照検証を適用
- SITES-12715:エクスペリエンスフラグメント：エクスペリエンスフラグメントフォルダーに適用されたクラウドサービス設定は保持されません
- SITES-13097:エクスペリエンスフラグメント：翻訳プロジェクトにエクスペリエンスフラグメントを追加できません
- SITES-13165:GraphQL:null 値のフィルタリングのデフォルト動作を復元
- SITES-12577:リンクチェック：変換サービスがリンクを断続的に書き換えない
- SITES-13559:MSM:コンポーネントのロールアウト時に「変更不可」例外がスローされました
- SITES-11757:MSM:親からロールアウト設定を継承は、子ページに戻りません
- SITES-14073:サイト管理者：書き出すプロパティを選択しない場合、CSV レポートが 500 で失敗する
- Forms-7648:数値ボックスコンポーネントの最大桁数を検証できません。 検証スクリプトが機能していません。
- Forms-8177:Formsサービスがアクティブな場合、 `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Failed to retrieve asset dependencies` エラーが発生しました。
- Forms-8300:ユーザーがタスクを開いた後に委任しようとすると、委任応答は、ユーザーのAEMインボックス UI を開く代わりに、タスクを再読み込みします。
- Forms-8500:IE モードオプションが有効なMicrosoft® Edge ブラウザーで、HTML5 Formsを開けません。
- Forms-8541:アダプティブFormsのレンダリング時に、ヌルポインター例外が発生します。
- Forms-8964:Google Chrome または Mozilla Firefox 上の Android™デバイスでフォームを開くと、テキストボックスコンポーネントに入力されたテキストは削除できません。
- Forms-9026:複雑で有効な JSON スキーマに基づいてアダプティブフォームを作成し、関連する JSON スキーマフィールドをアダプティブFormsエディターにドラッグしてアダプティブFormsフィールドを作成し、Adaptive Forms Editor ウィンドウを更新すると、すべてのフィールドが削除され、Adaptive Formsエディターは空白で表示されます。
- Forms-9263:チェックボックスオプションの表示テキストに特殊文字が含まれている場合、ユーザーはそのようなチェックボックスを選択できません。
- Forms-8668:フォームのPDFプレビューをレンダリングする際に、不要な Java™スタックダンプがエラーログに表示されます。 ただし、フォームのレンダリングに問題はありません。
- Forms-8116:アダプティブFormsコンテナコンポーネントにルールが適用されている場合、適用されたルールは保存されません。
- Forms-7906:アダプティブフォームがAEM Sitesコンテナコンポーネントに追加されると、ルールエディターが開けません。
- Forms-8846:Bind 参照プロパティは、アダプティブForms添付ファイルコンポーネントに対しては機能しません。
- Forms-9072:フォームフラグメントの作成中にスキームを検索した場合、検索結果は選択用のスキーマを返しません。
- Forms:AEM Formsの機能のアクセシビリティを改善するために、複数のアクセシビリティ関連のバグを修正しました。

### 既知の問題 {#known-issues-12441}

なし。

### 組み込みテクノロジー {#embedded-tech-12441}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | バージョン 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
