---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 96%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

>[!NOTE]
>
> リリース 20936 および 20783 は非公開になりました。

## リリース 20626 {#20626}

2025年4月29日（PT）に公開された、メンテナンスリリース 20626 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 20476 でした。

2025.5.0 機能のアクティベーションは、このメンテナンスリリースのすべての機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20626}

* ASSETS-46413、ASSETS-46580：新しいレビュステータス「プレビュー」を追加。
* ASSETS-49542：ビデオとオーディオの文字起こしと翻訳でサポートされる言語の拡張。
* ASSETS-48264：レンディションの PNG 画質サポートの拡張。

### 修正された問題 {#fixed-issues-20626}

* ASSETS-50387：GenStudio で使用するコンテンツフラグメントのデフォルトのサムネールを修正。
* ASSETS-49006：ユーザーに書き込み権限がない場合でもビデオのプロパティを表示。
* ASSETS-46757、ASSETS-46997：スマート切り抜きエディターのアクセシビリティを向上。
* ASSETS-48018：アセット公開レポートでのアセット参照トラッキングを改善。
* ASSETS-35846：オーサー層と配信層間のアクセスの一貫性を向上。
* ASSETS-48171：キャンバスを使用した Dynamic Media テンプレートの一貫性を向上。
* ASSETS-49813：有効期限通知を改善。
* ASSETS-47768、ASSETS-49825、ASSETS-49008、ASSETS-48287：一括操作の管理と視認性を向上。
* ASSETS-50003、ASSETS-50004：アセットのダウンロードに含まれるレンディションの命名と制御を改善。
* ASSETS-47939：コンテンツハブの応答の編成を改善。
* ASSETS-46738：非常に大規模なコレクションのパフォーマンスを向上。
* ASSETS-50121：アセット公開イベントの信頼性を向上。
* ASSETS-48490：画像取り込み中の自動処理の回復性を向上。
* ASSETS-28106、ASSETS-49404：フルテキスト検索の堅牢性を向上。
* ASSETS-50006、ASSETS-50423：大きなフォルダー内での検索とトラバーサルのパフォーマンスを向上。
* ASSETS-46021：Safari およびモバイルブラウザーのビデオ表示を改善。
* ASSETS-49002：Dynamic Media テンプレートの編集処理を改善。
* ASSETS-48376：コンテンツハブ UI のその他の改善。
* ASSETS-48504、ASSETS-49378：UI の動作に対するその他の改善。
* ASSETS-49540：アセットの関連付け OpenAPI を実験段階から移行。
* ASSETS-40284：Adobe Stock 統合に関するドキュメントを更新。
* ASSETS-49739：アセットセレクターから Figma を統合。

#### AEM ガイド {#guides}

* GUIDES-21734：XMLEditorConfig で「ID を自動生成」オプションが有効になっている場合でも、スニペット経由で要素を追加したり、テンプレート経由で要素を作成したりすると、その要素に対して新しい ID が生成されない。
* GUIDES-25969：DITA トピックの外部リンクに `scope=external` 属性が欠落している場合、特にマイクロサービスが有効になっている場合に、この属性が欠落しているファイルがエラーログに示されずに HTML5 の公開が失敗する。
* GUIDES-27288：新しい AEM Sites 公開を使用して生成されたマップランディングページにメタデータプロパティを渡すことができない。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-20626}

なし。

### 廃止された機能と API {#deprecated-20626}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-20626}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 11 個の脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-20626}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
