---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: db0f60537a65c426dae88b5440622c9034c736e2
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 34%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 14697 {#release-14697}

2023年12月18日（PT）に公開された、メンテナンスリリース 14697 の継続的な改善点を以下にまとめます。問題が発生したリリース14538に代わるものです。 以前のメンテナンスリリースはリリース14227でした。

2023.12.0機能のアクティベーションは、このメンテナンスリリースの完全な機能セットを提供します。 詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-14697}

* GRANITE-46723：ユーザー同期 — SAML Migration from default-sync to IDP-based sync.
* OAK-10311：レプリケーション — BLOB 比較を最適化して、AEM内の大きなアセットバッチのレプリケーション時間を短縮します。
* OAK-10511：レプリケーション — AEMでの大きなアセットのレプリケーション時間を短縮するために、ネットワークのラウンドトリップを削減します。
* GRANITE-48334：パブリッシャー — RUM のコレクションスクリプトが見つかりません。

### 修正された問題 {#fixed-issues-14697}

* CQ-4354867: ToggleCondition 参照は、InstanceActionServlet 内の存在しないフィールドを参照します。
* CQ-4349948：ツール→セキュリティ→ユーザーの「ユーザー設定を編集」での「プロファイルプロパティ」文字列のローカライゼーション。
* GRANITE-44541：ツール→セキュリティ→ユーザーの下のユーザーを編集/キーストアの秘密鍵ファイルを追加する際のエラーダイアログのローカライゼーション。
* GRANITE-45341:Tools → Security → Users の下で、ユーザーアクションのアクティベート/アクティベート解除の成功/失敗文字列のローカライズ。
* GRANITE-46650：エラーメッセージ「UserId/Password mismatch」のローカリゼーション。 文字列を「ツール」→「セキュリティ→ユーザー作成ダイアログ」の下に表示します。
* GRANITE-47764:Sling Models API 1.5.0 への更新：Sling Model 内の静的変数にインジェクションすると、コンパイルエラーが発生します (SLING-11507)。
* GRANITE-48452：ステータスコード 200 の空の clientlibs を送信しています。
* GRANITE-48410: ResourceResolver が閉じられていません。
* ASSETS-31297:Dynamic Media からコピーしたアセットが削除されないようにします。
* ASSETS-30811:Blocktag Service のバインドに対する参照の更新。
* GRANITE-46418: AEMでの Sling イベントの更新： GaugeSupport は registerWithSuffix で無限再帰を持っています (SLING-11918)。

### 既知の問題 {#known-issues-14697}

なし。

### 組み込みテクノロジー {#embedded-tech-14697}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.58-T20231123092841-619e1bd | [Oak API 1.58.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
