---
title: コンテンツ変換サービスの使用
description: AEM as a Cloud Serviceへの移行に備えて、コンテンツ構造を変換する方法を説明します。
exl-id: 40516ff7-5686-42e6-bdd1-c9c6de432b09
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 75%

---

# コンテンツ変換サービスの使用 {#using-ct}

## コンテンツ変換サービスを使用する際の重要な考慮事項 {#imp-considerations-ct}

コンテンツ変換サービス（CT）を使用する際の重要な考慮事項について詳しくは、以下の節を参照してください。

* コンテンツ変換サービスを使用するには、まず Adobe Experience Manager（AEM）環境でベストプラクティスアナライザーを実行する必要があります。
* 実稼動環境でコンテンツ変換サービスを実行できますが、実稼動環境のクローンでコンテンツ変換サービスを実行することをお勧めします。さらに重要なのは、BPA および CT が同じ環境で実行されていることを確認する必要があることです。
* コンテンツ変換サービスを実行する環境の管理者である必要があります。
* ソースコンテンツを変更できる操作（移動／削除／名前変更）は、デフォルトで `/etc/packages/content-transformation` 下にソースパスのバックアップパッケージを変換前に作成します。各操作ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に有効パッケージの作成を選択することを強くお勧めします。
* コンテンツ変換サービスの各ページは、最大 50 個の結果をリストするように設定されているので、一度に最大 50 個の結果を変換できます。 これは、UI でタイムリーに応答するために行われます。

## 入手方法 {#availability-ct}

コンテンツ変換サービスは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできる[コンテンツ転送ツール](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)とバンドルされています。パッケージマネージャーを介して、ソース AEM インスタンスでパッケージをインストールできます。

>[!NOTE]
>コンテンツ変換サービスは、コンテンツ転送ツール v2.0.20 以降で使用できます。

## コンテンツ変換サービスを開く {#opening-ct}

1. ソース AEM インスタンスに管理者としてログインし、次の開始ページに移動します。https://host:port/aem/start.html
1. ツール／操作／コンテンツの移行に移動します。

   ![画像](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > BPA レポートを以前に実行したことを確認し、次の URL で検証してください。http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. **BPA レポートのコンテンツ変換サービス**&#x200B;のタイトルが付くカードをクリックします。

   ![画像](/help/journey-migration/content-transformer/assets/ct-2.png)

   BPA レポートの作成に成功した場合およびコンテンツに関連する問題が見つかった場合に、コンテンツ変換サービスの概要ページがどのように表示されるかの例を以下に示します。

   BPA レポートの残り有効期限がサイドレールに表示されます。コンテンツ関連の結果を見逃さないように、最新の BPA レポートでコンテンツ変換サービスを実行することをお勧めします。

   ![画像](/help/journey-migration/content-transformer/assets/ct-3.png)

1. 問題を `Pattern Code`、`Subtype`、`Importance`および `Source` に基づいてフィルターできます。

   ![画像](/help/journey-migration/content-transformer/assets/ct-4.png)

1. すべての問題または特定の問題を選択し、移動、削除または名前変更して解決できます。 また、カスタムパスは右上隅にある「**パスを追加**」ボタンを使用して追加できます。

   >[!NOTE]
   > 移動操作を使用する場合は、すべてのパスを 1 つのフォルダー ( 例： `/etc/packages/content-transformation/paths`) の場合は、バックアップパッケージがインストールされてインスタンスが元の状態に戻るときに、フォルダー (`/etc/packages/content-transformation/paths`) は、削除操作を使用して削除し、リポジトリのサイズを小さくすることができます。

   ![画像](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![画像](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > ソースコンテンツ（`move`／`remove`／`rename`）を変更できる操作は、デフォルトで変換前にソースパスのバックアップパッケージを `/etc/packages/content-transformation` 下に作成します。各操作ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に有効パッケージの作成を選択することを強くお勧めします。

1. パスの移動操作で作成されたバックアップパッケージの例を以下に示します。「インストール」をクリックして、ソースパスを戻します。インストールによって、ソースパスが元の場所に戻るだけで、変換中に移動されたパスは削除されません。 移動した場所のパスを削除するには、 **パスを追加** 場所を追加するボタン ( 例： `/etc/packages/content-transformation/paths`)、場所を選択して、 **削除**.

   >[!CAUTION]
   > `/etc/packages/content-transformation` は削除しないでください。ここには、バックアップパッケージが格納されています。これらのパッケージが確実に不要になった場合にのみ、この場所を削除してリポジトリのサイズを縮小できます。

   ![画像](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![画像](/help/journey-migration/content-transformer/assets/ct-8.png)
