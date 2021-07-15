---
title: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 06dca3b3e94b27f592681e661cd5c9883c0f6422
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 24%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.7.0のCloud Managerのリリース日は2021年7月15日です。
次回のリリースは2021年8月13日に予定されています。

### 新機能 {#what-is-new}

* お客様は、Cloud ManagerのビルドプロセスにAzul 8および11 JDKを使用できるようになり、ツールチェーン互換のMavenプラグインに対してこれらのJDKの1つを使用するか、Mavenプロセスの実行全体を&#x200B;*または*&#x200B;使用するかを選択できます。

* 送信エグレスIPがビルドステップログファイルに記録されます。

* 古いバージョンのAEMを実行しているステージ環境と実稼動環境で、「使用可能な更新」のステータスがレポートされるようになりました。

* サポートされるSSL証明書の最大数が、プログラムあたり20に増えました。

* 増加：設定可能なドメインの最大数が、環境ごとに500に増加しました。

* 「 Gitを管理」ボタンのタイトルが「 Access Git Info 」に変更され、ダイアログが視覚的に更新されました。

### バグ修正 {#bug-fixes}

* IP環境をバインドする際に、「プレビュー」オプションが使用できない場合があ許可リストりました。

* 存在しない実行の実行の詳細ページに手動で移動しても、エラーが表示されず、無限の読み込み画面のみが表示されていた問題を修正しました。

* SSL証明書の最大数に達した場合に表示されるエラーメッセージは役に立ちませんでした。

* 状況によっては、概要ページのパイプラインカードに表示されるリリースバージョンに矛盾が生じる場合がありました。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていた問題を修正しました。

* IP環境をバインドする際に、「プレビュー」オプションが使用できない場合があ許可リストりました。

### 既知の問題 {#known-issues}

Azul JDKを使用するように切り替えるお客様は、Azul JDKでエラーなしにコンパイルされるとは限らないことに注意する必要があります。 切り替える前に、ローカルでテストすることを強くお勧めします。

