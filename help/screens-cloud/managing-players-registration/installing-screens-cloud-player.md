---
title: Screens as a Cloud Service でのプレーヤーのインストールと設定
description: ここでは、Screens as a Cloud Service でプレーヤーをインストールおよび設定する方法について説明します。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 52%

---

# Screens as a Cloud Service でのプレーヤーのインストールと設定 {#installing-players-screens-cloud}

この節では、オンプレミスの AEM インスタンスに登録されている AEM Screens プレーヤーのインストール方法について説明します。また、既存のプレーヤーの工場出荷時リセットを実行してから、新しいプレーヤーをAEM Screens as a Cloud Serviceに登録する必要があります。

## 目的 {#objective}

このドキュメントでは、プレーヤーを登録する前にプレーヤーを設定する方法を説明します。 読み終えたら、次の内容を理解できるようになります。

* プレーヤーのインストール元
* プレーヤーをクラウドモードに更新する方法

## プレーヤーをクラウドモードに設定する手順 {#cloud-mode-setup}

最新のプレーヤーを [AEM Screens Player のダウンロード](https://download.macromedia.com/screens/)、プレーヤーをクラウドモードに更新する準備が整いました。

以下の手順に従って、プレーヤーをアップデートします。

1. AEM Screens プレーヤーを開きます。

   >[!NOTE]
   >専用のハードウェアデバイスでテストするか、自分のプレーヤーの Web 拡張機能でテストするかを選択できます。

1. 次をクリック： **設定** タブをクリックし、 **工場出荷時** 下のボタン **リセット** オプション。

   ![画像](/help/screens-cloud/assets/player/installplayer-2.png)

1. クリック **確認** プレーヤーをリセットする場合。

1. 再び **設定** タブをクリックし、 **クラウドモードに変更** 下のボタン **実行モードを切り替え** オプション。

   ![画像](/help/screens-cloud/assets/player/installplayer-1.png)

1. クリック **確認** クラウドモードに切り替えるときにプロンプトが表示され、プレーヤーの登録が解除されます。

## 基本的な再生モニタリング {#playback-monitoring}

プレーヤーは、各 `ping`（デフォルトは 30 秒）で様々な再生指標を報告します。これらの指標に基づいて、Adobeは、動きのないエクスペリエンス、空白の画面、スケジュールの問題など、様々なエッジケースを検出できます。 この検出により、デバイスの問題を把握し、トラブルシューティングできるので、調査や修正の手順を迅速におこなうことができます。

AEM Screens Player での基本的な再生モニタリングにより、以下が可能になります。

* プレーヤーがコンテンツを適切に再生しているかどうかのリモート監視

* 空白の画面やフィールド内のエクスペリエンスの不具合に対する反応性の向上

* 不具合のあるエクスペリエンスがエンドユーザーに表示されるリスクの軽減

### プロパティについて {#understand-properties}

各 `ping` には、次のプロパティが含まれています。

| プロパティ | 説明 |
|---|---|
| id {string} | プレーヤーの識別子 |
| activeChannel {string} | 現在再生中のチャネルパス。何もスケジュールされていない場合は null |
| activeElements {string} | コンマ区切りの文字列。現在は、再生中のすべてのシーケンスチャネルに表示される要素（マルチゾーンレイアウトの場合は複数） |
| isDefaultContent {boolean} | 再生チャネルがデフォルトチャネルまたはフォールバックチャネルと見なされる（つまり、優先度が 1 でスケジュールが設定されていない）場合は true |
| hasContentChanged {boolean} | コンテンツが過去 5 分間に変更された場合は true、それ以外の場合は false |
| lastContentChange {string} | 最後にコンテンツが変更されたときのタイムスタンプ |

>[!NOTE]
>オプションで、プレーヤーの環境設定（再生監視を有効にする）から、より高度なプロパティを有効にできます。
>|プロパティ|説明|
>|---|---|
>|isContentRendering {boolean}|GPU が実際のコンテンツを再生していることを（ピクセル分析に基づいて）確認できる場合は true|

### 制限事項 {#limitations}

基本的な再生モニタリングに関するいくつかの制限事項を以下に示します。

* プレーヤーが自分自身の再生状態をサーバーに報告するので、アクティブな接続が必要です。

* この `isContentRendering` GPU をチェックするプロパティは、リソースを大量に消費し、デフォルトで有効にする必要があり、プレーヤーの環境設定で明示的にオプトインする必要があります。 実稼動環境ではビデオと一緒に使用しないことをお勧めします。

* この機能はシーケンスチャネルの場合にのみサポートされており、インタラクティブチャネル（SPA）のユースケースにはまだ対応していません。

* 指標は、まだお客様に完全に公開されていません。Adobeは、近日中にダッシュボードに似たレポートおよび警告メカニズムの有効化に取り組んでいます。

## 次の手順 {#whats-next}

プレーヤーをインストールし、クラウドモードに設定したら、Screensas a Cloud Serviceのジャーニーを続行します。 詳しくは、 [Screens へのプレーヤーの登録as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) Screens Services Provider から。
