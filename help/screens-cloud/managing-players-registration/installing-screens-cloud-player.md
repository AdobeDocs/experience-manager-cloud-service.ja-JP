---
title: Screens as a Cloud Service でのプレーヤーのインストールと設定
description: ここでは、Screens as a Cloud Service でプレーヤーをインストールおよび設定する方法について説明します。
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: af7793ca7ad3d11bfff980a4d00f537fd0871755
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 100%

---

# Screens as a Cloud Service でのプレーヤーのインストールと設定 {#installing-players-screens-cloud}

この節では、オンプレミスの AEM インスタンスに登録されている AEM Screens プレーヤーのインストール方法について説明します。また、既存のプレーヤーの工場出荷時リセットを実行し、新しいプレーヤーを AEM Screens as a Cloud Service に登録する必要があります。

## 目的 {#objective}

このドキュメントでは、プレーヤーを登録する前に設定する方法を説明します。読み終えると、次のことを理解できるようになります。

* プレーヤーのインストール元
* プレーヤーをクラウドモードに更新する方法

## プレーヤーをクラウドモードに設定する手順 {#cloud-mode-setup}

[AEM Screens Player ダウンロード](https://download.macromedia.com/screens/)から最新のプレーヤーをダウンロードしたら、プレーヤーをクラウドモードにアップデートする準備が整います。

以下の手順に従って、プレーヤーをアップデートします。

1. AEM Screens プレーヤーを開きます。

   >[!NOTE]
   >専用のハードウェアデバイスでテストするか、自分のプレーヤーの Web 拡張機能でテストするかを選択できます。

1. 「**設定**」タブをクリックし、「**リセット**」オプションの下の「**工場出荷時**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-2.png)

1. 「**確認**」をクリックして、プレーヤーをリセットします。

1. 「**設定**」タブから、「**実行モードを切り替え**」オプションの下の「**クラウドモードに変更**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-1.png)

1. クラウドモードに切り替えるときに「**確認**」をクリックすると、プレーヤーの登録が解除されます。

## 基本的な再生モニタリング {#playback-monitoring}

プレーヤーは、各 `ping`（デフォルトは 30 秒）で様々な再生指標を報告します。これらの指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白の画面、スケジュールの問題など）を検出できます。この検出により、デバイスの問題を把握してトラブルシューティングできるので、調査や修正を迅速に行えます。

AEM Screens Player での基本的な再生モニタリングにより、以下が可能になります。

* プレーヤーがコンテンツを適切に再生しているかどうかのリモート監視

* 空白の画面やフィールド内のエクスペリエンスの不具合に対する反応性の向上

* 不具合のあるエクスペリエンスがユーザーに表示されるリスクの軽減

### プロパティについて {#understand-properties}

各 `ping` には、次のプロパティが含まれています。

| プロパティ | 説明 |
|---|---|
| id {string} | プレーヤーの識別子 |
| activeChannel {string} | 現在再生中のチャネルパス。何もスケジュールされていない場合は null |
| activeElements {string} | コンマ区切りの文字列。再生中のすべてのシーケンスチャネルに現在表示されている要素（マルチゾーンレイアウトの場合は複数）を表します |
| isDefaultContent {boolean} | 再生チャネルがデフォルトチャネルまたはフォールバックチャネルと見なされる（つまり、優先度が 1 でスケジュールが設定されていない）場合は true |
| hasContentChanged {boolean} | コンテンツが過去 5 分間に変更された場合は true、それ以外の場合は false |
| lastContentChange {string} | 最後にコンテンツが変更されたときのタイムスタンプ |

>[!NOTE]
>
>オプションで、プレーヤーの環境設定から、より高度なプロパティを有効にできます（再生モニタリングを有効にする）。
>
>| プロパティ | 説明 |
>|---|---|
>| isContentRendering {boolean} | GPU が実際のコンテンツを再生していることを（ピクセル分析に基づいて）確認できる場合は true |

### 制限事項 {#limitations}

基本的な再生モニタリングに関するいくつかの制限事項を以下に示します。

* プレーヤーが自分自身の再生状態をサーバーに報告するので、アクティブな接続が必要です。

* GPU が大量のリソースを消費しているかどうかを確認する `isContentRendering` プロパティがデフォルトで有効になっている必要があり、プレーヤーの環境設定で明示的にオプトインする必要があります。実稼動環境では、ビデオと組み合わせて使用しないことをお勧めします。

* この機能はシーケンスチャネルの場合にのみサポートされており、インタラクティブチャネル（SPA）のユースケースにはまだ対応していません。

* 指標は、まだお客様に完全に公開されていません。アドビは、近日中にダッシュボードに似たレポートおよび警告メカニズムを実現できるように取り組んでいます。

## 次の手順 {#whats-next}

プレーヤーをインストールし、クラウドモードに設定したら、Screens as a Cloud Service のジャーニーを続けましょう。詳しくは、Screens サービスプロバイダーから [Screens as a Cloud Service でのプレーヤーの登録](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)を参照してください。
