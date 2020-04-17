---
title: ビデオレンディション
description: ビデオレンディション
contentOwner: AG
translation-type: ht
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# ビデオレンディション {#video-renditions}

Adobe Experience Manager (AEM) Assets では、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションを生成します。

AEM Assets では、メディアアセットの静的レンディションと動的レンディション（DM エンコードされたレンディション）がサポートされています。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

AEM Assets では、クライアント側でのこのようなレンディションの再生をサポートしています。

特定のビデオアセットのレンディションを表示するには、アセットのページを開いて、グローバルナビゲーションアイコンをタップします。次に、リストから「**[!UICONTROL レンディション]**」を選択します。

ビデオレンディションのリストが&#x200B;**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

DM エンコードされたレンディションのプロキシサーバーを設定するには、Dynamic Media クラウドサービスを設定します。

<!-- To generate video renditions with desired parameters, [create a corresponding video profile](video-profiles.md). -->

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Internet Explorer 11 では、OGG および WAV ファイルのオーディオは再生できません。拡張子 OGG または WAV を持つアセットの場合、アセットの詳細ページに「無効なソース」というエラーメッセージが表示されます。MS Edge および iPad では、OGG ファイルは再生できません。サポートされていない形式であるというエラーが表示されます。