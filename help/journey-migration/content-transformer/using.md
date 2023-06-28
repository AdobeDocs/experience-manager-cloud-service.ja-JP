---
title: Content Transformer の使用
description: Content Transformer の使用
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Content Transformer の使用 {#using-ct}

## Content Transformer を使用する際の重要な考慮事項 {#imp-considerations-ct}

コンテンツトランスフォーマー (CT) を使用する際に重要な考慮事項については、以下の節を参照してください。

* Content Transformer を使用するには、まずAdobe Experience Manager(AEM) 環境でベストプラクティスアナライザーを実行する必要があります。
* 実稼動環境で Content Transformer を実行できますが、実稼動環境のクローンで Content Transformer を実行することをお勧めします。 さらに重要なのは、BPA と CT が同じ環境で実行されていることを確認する必要があることです。
* コンテンツ変換サービスを実行する環境の管理者である必要があります。
* ソースコンテンツを変更できる操作（移動/削除/名前変更）は、デフォルトで、以下にソースパスのバックアップパッケージを作成します。 `/etc/packages/content-transformation` 変換前に 各操作ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に有効パッケージの作成を選択するようにすることを強くお勧めします。
* CT の各ページは、最大 50 個の結果をリストするように構成されているので、一度に最大 50 個の結果を変換できます。 これは、UI にタイムリーな応答を提供するためにおこなわれます。

## 入手方法 {#availability-ct}

Content Transformer は、 [コンテンツ転送ツール](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) これは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。 パッケージマネージャーを使用して、パッケージをソースAEMインスタンスにインストールできます。

>[!NOTE]
>Content Transformer は、コンテンツ転送ツール v2.0.20 以降で使用できます。

## Content Transformer を開く {#opening-ct}

1. ソースAEMインスタンスに管理者としてログインし、開始ページに移動します。https://host:port/aem/start.html.
1. ツール/操作/コンテンツ移行に移動します。

   ![画像](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > BPA レポートを以前に実行したことを確認し、URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.htmlで検証してください

1. タイトル付きのカードをクリックします。 **BPA レポートのコンテンツ変換サービス**

   ![画像](/help/journey-migration/content-transformer/assets/ct-2.png)

   BPA レポートの作成に成功した場合、およびコンテンツに関連する問題が見つかった場合に、コンテンツ変換サービスの概要ページがどのように表示されるかの例を以下に示します。

   BPA レポートの残り有効期限がサイドレールに表示されます。 コンテンツ関連の結果が見つからないように、最新の BPA レポートでコンテンツトランスフォーマーを実行することをお勧めします。

   ![画像](/help/journey-migration/content-transformer/assets/ct-3.png)

1. 問題を `Pattern Code`, `Subtype`, `Importance`、および `Source`.

   ![画像](/help/journey-migration/content-transformer/assets/ct-4.png)

1. すべての問題または特定の問題を選択し、移動、削除、名前変更などのアクションを実行して、問題を解決できます。 カスタムパスは、 **パスを追加** 」ボタンを使用して設定できます。

   >[!NOTE]
   > 移動操作を使用する場合は、すべてのパスを 1 つのフォルダーにのみ移動することをお勧めします ( 例： `/etc/packages/content-transformation/paths`) の場合は、バックアップパッケージがインストールされてインスタンスが元の状態に戻るときに、フォルダー (`/etc/packages/content-transformation/paths`) は、削除操作を使用して削除し、リポジトリのサイズを小さくすることができます。

   ![画像](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![画像](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > ソースコンテンツ (`move`/`remove`/`rename`) は、デフォルトで、以下のソースパスのバックアップパッケージを作成します。 `/etc/packages/content-transformation` 変換前に 各操作ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に有効パッケージの作成を選択するようにすることを強くお勧めします。

1. パスの移動操作用に作成されたバックアップパッケージの例を以下に示します。「インストール」をクリックして、ソースパスを戻します。 インストールによって元の場所に戻されるのはソースパスのみであり、変換中に移動されたパスは削除されないことに注意してください。 移動した場所のパスを削除するには、 **パスを追加** 場所を追加するボタン ( 例： `/etc/packages/content-transformation/paths`)、場所を選択して、 **削除**.

   >[!CAUTION]
   > 削除しない `/etc/packages/content-transformation` これは、バックアップパッケージが存在する場所です。 これらのパッケージが不要になった場合にのみ、この場所を削除してリポジトリのサイズを小さくできます。

   ![画像](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![画像](/help/journey-migration/content-transformer/assets/ct-8.png)
