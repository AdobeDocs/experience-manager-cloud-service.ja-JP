---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
source-git-commit: 87a43c0a37db732c66073f9582d4ab3574304aed
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 38%

---


# Adobe Experience Manager as a Cloud Service 2021.5.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as aCloud Service版の最新のリリースノートを確認するには、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as aCloud Service2021.5.0のCloud Managerのリリース日は2021年5月6日です。

### 新機能 {#what-is-new}

* PackageOverlaps 品質ルールは、デプロイされたパッケージセットに同じパッケージが複数回（複数の埋め込み場所に）デプロイされた場合に検出するようになりました。

* Public API のリポジトリーエンドポイントに、Git URL が含まれるようになりました。

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

* コードの臭いのタイプの品質問題が、誤って信頼性の評価に影響していました。

* ワイルドカードドメインはサポートされていないので、UIではユーザーがワイルドカードドメインを送信できません。

* パイプラインの実行が午前 0 時から午前 1 時（UTC）の間に開始された場合、Cloud Manager で生成されるアーティファクトのバージョンが、前日に作成されたバージョンより大きいことが保証されませんでした。

* サンドボックスプログラムの設定中に、サンプルコードを含むプロジェクトが正常に作成されると、「 Gitを管理」が概要ページのヒーローカードからのリンクとして表示されます。
