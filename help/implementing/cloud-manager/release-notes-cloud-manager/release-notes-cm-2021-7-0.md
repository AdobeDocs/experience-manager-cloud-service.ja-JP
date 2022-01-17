---
title: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
feature: Release Information
source-git-commit: 3542d5a6b89b8673444786e3f9062dae0d315946
workflow-type: ht
source-wordcount: '340'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.7.0 の Cloud Manager のリリース日は 2021 年 7 月 15 日です。


### 新機能 {#what-is-new}

* お客様は、Cloud Manager のビルドプロセスに Azul 8 および 11 JDK を使用できるようになりました。ツールチェーン対応の Maven プラグイン&#x200B;*または* Maven プロセスの実行全体に対して、これらの JDK のいずれかを使用するように選択できます。

* 送信エグレス IP がビルドステップログファイルに記録されるようになりました。

* 古いバージョンの AEM を実行しているステージ環境と実稼動環境で、**アップデートが使用可能**&#x200B;のステータスがレポートされるようになりました。

* サポートされる SSL 証明書の最大数が、プログラムあたり 20 に増えました。

* 設定できるドメインの最大数が、環境あたり 500 に増えました。

* 「**Git を管理**」ボタンのタイトルが「**Git 情報にアクセス**」に変更され、ダイアログが視覚的に更新されました。

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 28 に更新されました。

### バグ修正 {#bug-fixes}

* 許可リストを IP 環境をバインドする際に、「プレビュー」オプションが使用できないことがありました。

* 存在しない実行の実行詳細ページに手動で移動しても、エラーが表示されず、読み込みが無限に繰り返される画面が表示されるだけでした。

* SSL 証明書の最大数に達した場合に表示されるエラーメッセージが参考になりませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンが矛盾していることがありました。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていました。

### 既知の問題 {#known-issues}

Azul JDK の使用に切り替えるお客様は、すべての既存アプリケーションが Azul JDK でエラーなしにコンパイルされるとは限らないことに注意してください。切り替える前に、ローカルでテストすることを強くお勧めします。

