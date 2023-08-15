---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 4c38285f9e75618ad181a85034212c7c24030e99
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 18%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13099 {#release-13099}

2023 年 8 月 16 日に公開されたメンテナンスリリース13099の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12874 からのアップデートです。

2023.8.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13099}

- SITES-13906: GraphQL - graphql-java 20.1 にアップグレードします。
- SITES-8972: GraphQL — オプションを追加```label``` （「列挙」データタイプの JSON）。
- SITES-9689: GraphQL — コンテンツ参照データタイプ用のタイトルと説明を JSON で追加します。
- SITES-13052：コンテンツフラグメント — コンテンツフラグメントをAdobe Targetに書き出す

### 修正された問題 {#fixed-issues-13099}

- SITES-14937: MSM — ロールアウト設定を親値から継承は、ライブコピーで「保存して閉じる」を押すと切り替えられます。
- SITES-14847：コンテンツフラグメント — コンテンツフラグメントリンクはハイライト表示されません。
- SITES-11620：コンテンツフラグメント — 参照パスが UI で少し切り取られます。
- SITES-14171: GraphQL — キャッシュされたデータの循環参照が壊れないことがあります。
- SITES-14577：エクスペリエンスフラグメント — 一括公開がライブコピーに対して機能しない。
- SITES-14341：管理 UI — 削除権限が削除された場合の「プロパティ」ボタンの動作に一貫性がありません。
- SITES-11000：管理 UI — 参照：一部のページでリンクが見つからない。
- SITES-11559：管理 UI — 参照：受信リンクで間違ったページが表示される。
- SITES-14337：管理 UI — エディターページを開くと、特定のケースでエラーが発生する。
- SITES-13425:ContextHub - ContextHub ボタンをクリックすると、メニューバーが表示されない。
- FORMS-9971：アダプティブフォームが異なるロケールでレンダリングされると、コンポーネントの表示が正しく解釈されず、適用されなくなります。
- FORMS-9888：アダプティブフォームがフォーム送信時に外部 URL（ありがとうございますページ）にリダイレクトするように設定されている場合、外部 URL にリダイレクトできません。
- FORMS-9845：ルールエディターを使用してドロップダウンをクリアした後、以前に指定した値は、想定されるクリアランスにもかかわらず保持されます。
- FORMS-9263：チェックボックスのラベルに特殊文字が含まれ、ユーザーがチェックボックスをクリックした場合、それぞれのチェックボックスは選択されません。
- FORMS-9254：ユーザーが利用条件コンポーネントのテキストをスクロールすると、ユーザーがテキスト全体をスクロールする前でも、コンポーネント内のチェックボックスが自動的に有効になります。
- FORMS-9045：スクリプトタグはベース XDP 内の外部フラグメント参照を解決しません。
- FORMS-9026：空の文字列を持つ Enums を持ち、エラーなしで検証する JSON スキーマを使用してアダプティブフォームを作成しようとすると、プロセスが失敗します。 次に、ページを更新すると、フォームが正しく読み込まれず、空白のフォームとログにエラーが表示されます。
- FORMS-8964: Android™ Chrome/Firefox では、最大文字数に達すると、テキストボックスコンポーネントでテキストが編集不可になります。
- FORMS-8668：機能的なフォームレンダリングにもかかわらず、エラーログに過剰な Java™スタックダンプが発生し、ログファイルが膨張する。
- FORMS-8554：遅延読み込みが有効になっているアダプティブFormsは、オーサーインスタンスのプレビューモードで機能しません。
- FORMS-8177: forms サービスがアクティブな場合、例外「com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Failed to retrieve asset dependencies」が発生する。 が発生します。 このエラーは、フォームサービスを無効にすると消えます。
- FORMS-3691：一部のオブジェクトで、IIFE（即時に呼び出される関数式）スコーピングが欠落しています。 IIFE の主な目的は、関数内の変数のスコープを作成し、これらの変数がグローバルスコープを汚染するのを防ぐことです。


### 既知の問題 {#known-issues-13099}

- SITES-15359：バリエーション名のパターンが、 ```'_'``` を含める必要があります。

### 組み込みテクノロジー {#embedded-tech-13099}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
