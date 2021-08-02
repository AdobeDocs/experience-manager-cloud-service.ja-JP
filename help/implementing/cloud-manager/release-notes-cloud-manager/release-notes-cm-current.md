---
title: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.7.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
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

* 古いバージョンのAEMを実行しているステージ環境と実稼動環境で、ステータスが&#x200B;**Update Available**&#x200B;とレポートされるようになりました。

* サポートされるSSL証明書の最大数が、プログラムあたり20に増えました。

* 設定できるドメインの最大数は、環境ごとに500に増えました。

* **「Gitを管理」**&#x200B;ボタンのタイトルが&#x200B;**「Git情報にアクセス」**&#x200B;に変更され、ダイアログが視覚的に更新されました。

* Cloud Managerで使用されるAEMプロジェクトアーキタイプのバージョンがバージョン28に更新されました。

### バグ修正 {#bug-fixes}

* IP環境をバインドする際に、「プレビュー」オプションが使用できない許可リストが発生することがありました。

* 存在しない実行の実行の詳細ページに手動で移動しても、エラーが表示されず、無限の読み込み画面のみが表示されていた問題を修正しました。

* SSL証明書の最大数に達した場合に表示されるエラーメッセージは役に立ちませんでした。

* 状況によっては、**概要**&#x200B;ページのパイプラインカードに表示されるリリースバージョンに矛盾が生じる場合があります。

* プログラムの追加ウィザードで、作成後に名前を変更できないと誤って表示されていた問題を修正しました。

### 既知の問題 {#known-issues}

Azul JDKを使用するように切り替えるお客様は、Azul JDKでエラーなしにコンパイルされるとは限らないことに注意する必要があります。 切り替える前に、ローカルでテストすることを強くお勧めします。

