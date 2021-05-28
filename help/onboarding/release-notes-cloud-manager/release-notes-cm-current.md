---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
source-git-commit: 13d45a02169fc99be60d73dde91dbc8c2ce03ef8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 17%

---


# Adobe Experience Manager as a Cloud Service 2021.5.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as aCloud Service版の最新のリリースノートを確認するには、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.5.0のCloud Managerのリリース日は2021年5月6日です。
次回のリリースは2021年6月11日に予定されています。

### 新機能 {#what-is-new}

* PackageOverlaps品質ルールで、同じパッケージが複数回（同じデプロイ済みパッケージセット内の複数の埋め込み場所など）デプロイされた場合を検出するようになりました。

* パブリックAPIのリポジトリエンドポイントにGitのURLが含まれるようになりました。

* Cloud Managerユーザーがダウンロードしたデプロイメントログは、より洞察に富み、失敗と成功シナリオに関する詳細が含まれるようになります。

* コードをAdobeGitにプッシュ中に発生した断続的なエラーが解決されました。

* Commerceアドオンは、プログラムの編集ワークフロー中にサンドボックスプログラムに適用できるようになりました。

* *編集プログラム*&#x200B;のエクスペリエンスが更新されました。

* 環境の詳細ページの「ドメイン名」テーブルには、ページネーション経由で最大250個のドメイン名が表示されます。

* プログラムで使用可能なソリューションが1つだけでも、**プログラムを追加**&#x200B;ワークフローと&#x200B;**プログラムを編集**&#x200B;ワークフローの「**ソリューションとアドオン**」タブにソリューションが表示されます。

* ビルドでデプロイ済みコンテンツパッケージが生成されなかった場合のビルド手順ログのエラーメッセージが不明でした。

### バグ修正 {#bug-fixes}

* 場合によっては、その設定がデプロイされていない場合でも、IP許可リストの横に緑色の「アクティブ」ステータスが表示されることがあります。

* パイプライン変数APIは、「削除済み」の変数を削除する代わりに、ステータス&#x200B;**DELETED**&#x200B;のみをマークします。

* コードスメルタイプの品質の問題の一部が、信頼性評価に誤って影響していました。

* ワイルドカードドメインはサポートされていないので、UIではユーザーがワイルドカードドメインを送信できません。

* UTCの午前0時から午前1時の間にパイプラインの実行が開始された場合、Cloud Managerで生成されるアーティファクトのバージョンが前日に作成されたバージョンより大きくなることは保証されていませんでした。

* サンドボックスプログラムの設定中に、サンプルコードを含むプロジェクトが正常に作成されると、「 Gitを管理」が概要ページのヒーローカードからのリンクとして表示されます。
