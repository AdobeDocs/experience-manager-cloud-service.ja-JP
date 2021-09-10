---
title: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
feature: Release Information
source-git-commit: a707968483dc1196628b737ad207bfefe63ca94b
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 64%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.7.0のCloud Managerのリリース日は2021年7月15日です。
次回のリリースは 2021 年 8 月 12 日（PT）に予定されています。

### 新機能 {#what-is-new}

* お客様は、Cloud Manager のビルドプロセスに Azul 8 および 11 JDK を使用できるようになりました。ツールチェーン対応の Maven プラグイン&#x200B;*または* Maven プロセスの実行全体に対して、これらの JDK のいずれかを使用するように選択できます。

* 送信エグレス IP がビルドステップログファイルに記録されるようになりました。

* 古いバージョンのAEMを実行しているステージ環境と実稼動環境で、ステータスが&#x200B;**Update Available**&#x200B;とレポートされるようになりました。

* サポートされるSSL証明書の最大数が、プログラムあたり20に増えました。

* 設定できるドメインの最大数は、環境ごとに500に増えました。

* 「**Git を管理**」ボタンのタイトルが「**Git 情報にアクセス**」に変更され、ダイアログが視覚的に更新されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes}

* IP環境をバインドする際に、「プレビュー」オプションが使用できない許可リストが発生することがありました。

* 存在しない実行の実行詳細ページに手動で移動しても、エラーが表示されず、読み込みが無限に繰り返される画面が表示されるだけでした。

* SSL証明書の最大数に達した場合に表示されるエラーメッセージは役に立ちませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンに矛盾が生じる場合があります。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていた問題を修正しました。

### 既知の問題 {#known-issues}

Azul JDK の使用に切り替えるお客様は、すべての既存アプリケーションが Azul JDK でエラーなしにコンパイルされるとは限らないことに注意してください。切り替える前に、ローカルでテストすることを強くお勧めします。

