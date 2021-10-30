---
title: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノート
feature: リリース情報
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: ht
source-wordcount: '379'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.5.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.5.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.5.0 Cloud Manager のリリース日は 2021 年 5 月 6 日です。

### 新機能 {#what-is-new}

* PackageOverlaps 品質ルールは、同じパッケージが複数回デプロイされたケース（同一のデプロイ済みパッケージセット内の複数の埋め込み場所にデプロイされたケース）を検出するようになりました。

* パブリック API のリポジトリーエンドポイントに Git の URL が含まれるようになりました。

* Cloud Manager ユーザーがダウンロードしたデプロイメントログは、失敗と成功シナリオに関する詳細が含まれるようになり、よりわかりやすくなりました。

* コードを Adobe Git にプッシュ中に発生していた断続的なエラーが解決されました。

* Commerce アドオンは、プログラムの編集ワークフロー中に、サンドボックスプログラムに適用できるようになりました。

* 「*プログラムを編集*」エクスペリエンスが更新されました。

* 環境の詳細ページの「ドメイン名」テーブルには、ページネーションを使用して最大 250 個のドメイン名が表示されるようになります。

* プログラムに使用可能なソリューションが 1 つだけの場合でも、**プログラムを追加**&#x200B;ワークフローと&#x200B;**プログラムを編集**&#x200B;ワークフローの「**ソリューションとアドオン**」タブにソリューションが表示されるようになります。

* デプロイ可能なコンテンツパッケージがビルドで生成されなかった場合にビルドステップログに記録されるエラーメッセージが不明確でした。

### バグ修正 {#bug-fixes}

* 該当する設定がデプロイされていない場合でも、IP 許可リストの横に緑色の「アクティブ」ステータスが表示される場合がありました。

* パイプライン変数 API は、「削除済み」の変数を削除する代わりに、 **DELETED** ステータスを示すだけでした。

* 「コードの臭い」の品質問題の一部が、信頼性評価に誤って影響していました。

* ワイルドカードドメインはサポートされていないので、UI ではワイルドカードドメインを送信できません。

* UTC の午前 0 時から午前 1 時の間にパイプラインの実行が開始された場合、Cloud Manager で生成されるアーティファクトのバージョンが前日に作成されたバージョンよりも大きくなることが保証されていませんでした。

* サンドボックスプログラムのセットアップ中に、サンプルコードを含んだプロジェクトが正常に作成されると、「Git を管理」がヒーローカードからのリンクとして概要ページに表示されるようになります。
