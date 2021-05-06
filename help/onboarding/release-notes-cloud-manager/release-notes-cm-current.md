---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
translation-type: tm+mt
source-git-commit: 29bc3d02295fb04f3aacda41c43d1733092e1f27
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 17%

---


# Adobe Experience Manager as a Cloud Service 2021.5.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>現在のAdobe Experience ManagerのリリースノートをCloud Serviceとして表示するには、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2021.5.0のリリース日は2021年5月6日です。
次回のリリースは2021年6月3日に予定されています。

### 新機能 {#what-is-new}

* PackageOverlaps品質ルールは、同じパッケージが複数回（同じ展開済みパッケージセット内の複数の埋め込み場所など）展開された場合を検出するようになりました。

* Public APIのリポジトリエンドポイントにGit URLが含まれるようになりました。

* Cloud Managerユーザーがダウンロードした展開ログは、より洞察に富んでおり、失敗や成功シナリオに関する詳細が含まれるようになります。

* コードをAdobeGitにプッシュ中に発生した断続的なエラーが解決されました。

* コマースアドオンは、編集プログラムワークフロー中にSandboxプログラムに適用できるようになりました。

* *編集プログラム*&#x200B;のエクスペリエンスが更新されました。

* 環境の詳細ページの「ドメイン名」テーブルには、最大250個のドメイン名がページ番号を使用して表示されます。

* **追加プログラム**&#x200B;と&#x200B;**プログラム**&#x200B;の追加編集ワークフローの&#x200B;**ソリューション&amp;オン**&#x200B;タブは、プログラムで使用できるソリューションが1つだけであっても、ソリューションを表示します。

* ビルドでデプロイ済みのコンテンツパッケージが生成されなかった場合のビルド手順ログのエラーメッセージが不明確でした。

### バグ修正 {#bug-fixes}

* 場合によっては、IP許可リストの横に緑色の「アクティブ」ステータスが表示される場合があります。このステータスは、その設定が展開されていない場合でも表示されます。

* パイプライン変数APIは、「削除済み」変数を削除する代わりに、ステータス&#x200B;**DELETED**&#x200B;のみをマークします。

* コードのにおいタイプの品質の問題が、信頼性の評価に誤って影響していました。

* ワイルドカードドメインはサポートされていないので、UIではユーザーがワイルドカードドメインを送信できなくなります。

* パイプラインの実行が午前0時から午前1時のUTCの間に開始された場合、Cloud Managerで生成されるアーティファクトのバージョンが、前日に作成されたバージョンより大きいことは保証されませんでした。

* サンドボックスプログラムのセットアップ中に、サンプルコードを含むプロジェクトが正常に作成されると、Gitの管理は、概要ページのヒーローカードからのリンクとして表示されます。