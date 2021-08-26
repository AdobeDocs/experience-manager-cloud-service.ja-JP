---
title: ScreensでのプレーヤーのインストールとCloud Service
description: ここでは、ScreensでプレーヤーをCloud Serviceとしてインストールおよび設定する方法について説明します。
source-git-commit: 1fc06f987bb40d940bbec9c37e6d58c2c1ca9266
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---


# ScreensでのプレーヤーのインストールとCloud Service {#installing-players-screens-cloud}

この節では、オンプレミスのAEMインスタンスに登録されているAEM Screens Playerのインストール方法について説明します。 さらに、既存のプレーヤーのファクトリリセットを実行し、新しいプレーヤーをAEM ScreensにCloud Serviceとして登録する必要があります。

## 目的 {#objective}

このドキュメントでは、プレーヤーを登録する前にプレーヤーを設定する方法を説明します。 読み終えたら、次の内容を理解できるようになります。

* プレーヤーのインストール元
* プレーヤーをクラウドモードに更新する方法

## プレーヤーをクラウドモードに設定する手順 {#cloud-mode-setup}

[AEM Screens Playerのダウンロード](https://download.macromedia.com/screens/)から最新のプレーヤーをダウンロードしたら、プレーヤーをCloudモードに更新する準備が整いました。

以下の手順に従って、プレーヤーを更新します。

1. AEM Screens Playerを開きます。

   >[!NOTE]
   >専用のハードウェアデバイスでテストするか、独自のプレーヤーのWeb拡張機能でテストするかを選択できます。

1. 「**設定**」タブをクリックし、「**リセット**」オプションの下の「**To Factory**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-2.png)

1. **確認**&#x200B;をクリックして、プレーヤーをリセットします。

1. 「**設定**」タブから、「**実行モードを切り替え**」オプションの下の「**クラウドモードに変更**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-1.png)

1. クラウドモードに切り替えると、**確認**&#x200B;をクリックすると、プレーヤーの登録が解除されます。

## 基本的な再生の監視 {#playback-monitoring}

プレーヤーが様々な再生指標をレポートする際に、各`ping`のデフォルト値が30秒に設定されます。 指標に基づいて、動きのないエクスペリエンス、空白の画面、スケジュールの問題など、様々なエッジケースを検出できます。 これにより、デバイスの問題を把握し、トラブルシューティングでき、調査や修正の際に役立ちます。

AEM Screens Playerの基本的な再生監視では、次の操作を実行できます。

* プレーヤーがコンテンツを適切に再生しているかどうかをリモートで監視する

* フィールド内の空白の画面や壊れたエクスペリエンスに対する反応性を向上させる

* エンドユーザーに壊れたエクスペリエンスを表示するリスクを軽減する

### プロパティについて {#understand-properties}

各`ping`には、次のプロパティが含まれます。

| プロパティ | 詳細 |
|---|---|
| id {string} | プレーヤー識別子 |
| activeChannel {string} | 現在再生中のチャネルパス。何もスケジュールされていない場合はnull。 |
| activeElements {string} | コンマ区切りの文字列。現在は、すべての再生シーケンスチャネルに表示される要素（マルチゾーンレイアウトの場合は複数） |
| isDefaultContent {boolean} | 再生チャネルがデフォルトチャネルまたはフォールバックチャネルと見なされる（つまり、優先度が1でスケジュールが設定されていない）場合はtrue |
| hasContentChanged {boolean} | 過去5分間にコンテンツが変更された場合はtrue 、それ以外の場合はfalse |
| lastContentChange {string} | 前回のコンテンツ変更のタイムスタンプ |

>[!NOTE]
>オプションで、プレーヤーの環境設定（「再生監視を有効にする」）から、より高度なプロパティを有効にできます。つまり、
>|プロパティ|説明|
>|—|—|
>|isContentRendering {boolean}|GPUが実際のコンテンツの再生を確認できる場合はtrue（ピクセル分析に基づく）|

### 制限事項 {#limitations}

基本的な再生監視に関する制限の一部を以下に示します。

* プレーヤーがサーバーに独自の再生状態を報告するので、アクティブな接続が必要です。

* 現在、GPUをチェックする`isContentRendering`プロパティは、デフォルトで有効にするためにリソースを集中的に消費しており、プレーヤーの環境設定からの明示的なオプトインが必要です。 ビデオと組み合わせて使用しないことをお勧めします。

* シーケンスチャネルでサポートされています。

## 次の手順 {#whats-next}

これで、プレーヤーをCloud Serviceモードに設定できました。次に、Screensサービスプロバイダーの[Cloud ServiceとしてのScreensへのプレーヤーの登録](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)ドキュメントを確認し、Screensをクラウドジャーニーとして続行する必要があります。