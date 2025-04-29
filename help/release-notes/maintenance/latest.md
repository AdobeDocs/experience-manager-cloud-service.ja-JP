---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 437125b6819edf70539ebacb4a8beddb755fcb7a
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 39%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 20626 {#20626}

2025年4月29日（PT）に公開された、メンテナンスリリース 20626 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 20476 でした。

2025.5.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20626}

* ASSETS-46413、ASSETS-46580：新しいレビューステータス「プレビュー」が追加されました。
* ASSETS-49542：映像・音声のトランスクリプションと翻訳に対応した言語を拡充
* ASSETS-48264：レンディションに対する PNG 品質サポートの拡張。

### 修正された問題 {#fixed-issues-20626}

* ASSETS-50387:GenStudioで使用するために、コンテンツフラグメントのデフォルトのサムネールを修正する。
* ASSETS-49006：書き込み権限がない場合にビデオのプロパティを表示します。
* ASSETS-46757、ASSETS-46997: スマート切り抜きエディターでアクセシビリティを向上しました。
* ASSETS-48018:Assets公開レポートのアセット参照のトラッキング機能が向上しました。
* ASSETS-35846：オーサー層と配信層の間でアクセスの一貫性を向上させます。
* ASSETS-48171：キャンバスを使用した Dynamic Media テンプレートの一貫性を向上させます。
* ASSETS-49813：有効期限通知の改善。
* ASSETS-47768、ASSETS-49825、ASSETS-49008、ASSETS-48287：一括操作の管理と可視性を向上させます。
* ASSETS-50003、ASSETS-50004: アセットのダウンロードに含まれるレンディションの命名と制御を改善します。
* ASSETS-47939:Content Hubの対応の編成を改善します。
* ASSETS-46738：非常に大きなコレクションのパフォーマンスを向上させます。
* ASSETS-50121：アセット公開イベントの信頼性を向上します。
* ASSETS-48490：画像取得中の自動処理の回復性が向上します。
* ASSETS-28106、ASSETS-49404：フルテキスト検索の堅牢性を向上します。
* ASSETS-50006、ASSETS-50423：大きなフォルダー内での検索とトラバーサルのパフォーマンスを向上させます。
* ASSETS-46021:Safari およびモバイルブラウザーのビデオ表示が改善されました。
* ASSETS-49002:Dynamic Media テンプレートの編集処理を改善しました。
* ASSETS-48376:Content Hub UI のその他の機能強化。
* ASSETS-48504、ASSETS-49378:UI の動作のその他の改善点。
* ASSETS-49540:Asset Relations OpenAPI を実験段階から移動しました。
* ASSETS-40284:Adobe Stock統合に関するドキュメントの更新。
* ASSETS-49739：アセットセレクターから Figma を統合する作業をします。

#### AEM ガイド {#guides}

* GUIDES-21734：スニペットを使用して追加された場合、またはテンプレートを使用して作成された場合は、XMLEditorConfig で「ID を自動生成」オプションが有効になっている場合でも、要素の新しい ID を生成できません。
* GUIDES-25969: DITA トピック内の外部リンクに `scope=external` 属性がない場合、特にマイクロサービスが有効な場合に、HTML5 への公開が失敗し、エラーログにこの属性がないことが示されません。
* GUIDES-27288：新しいAEM Sites公開を使用して生成されたランディングページをマッピングするためにメタデータプロパティを渡すことができない。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)をご覧ください。

### 既知の問題 {#known-issues-20626}

なし。

### 廃止された機能と API {#deprecated-20626}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-20626}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 11 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-20626}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
