---
title: Dynamic Media のトラブルシューティング
description: Dynamic Mediaで画像、セット、ビューアを操作する際に試すことができるトラブルシューティングのヒントについて説明します。
contentOwner: Rick Brough
feature: Troubleshooting,Image Sets,Viewers
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 96%

---

# Dynamic Media のトラブルシューティング {#troubleshooting-dynamic-media-scene-mode}

以下のトピックでは、Dynamic Media のトラブルシューティングについて説明します。

## 新しい Dynamic Media 設定 {#new-dm-config}

[新しい Dynamic Media 設定のトラブルシューティング](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)を参照してください。

## 一般（すべてのアセット） {#general-all-assets}

以下に、すべてのアセットに関する一般的なヒントとテクニックを示します。

### アセット同期ステータスプロパティ {#asset-synchronization-status-properties}

CRXDE Lite で次のアセットプロパティを見直すと、Adobe Experience Manager から Dynamic Media へのアセットの同期に成功したことが確認できます。

| **プロパティ** | **例** | **説明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | ノードが Dynamic Media にリンクされていることを示す全般的インジケーター。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** またはエラーテキスト | Dynamic Media へのアセットアップロードのステータス。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic Media のリモートアセットへの URL を生成するには、これを入力する必要があります。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** または **failed:`<error text>`** | セット（スピンセット、画像セットなど）、画像プリセット、ビューアプリセット、アセットの画像マップの更新、編集された画像などの同期ステータス。 |

### 同期のログ {#synchronization-logging}

同期のエラーと問題は `error.log`（Experience Manager サーバーディレクトリの `/crx-quickstart/logs/`）に記録されます。ログにはほとんどの問題の根本原因を突き止めるのに十分な情報が記録されますが、Sling コンソール（`com.adobe.cq.dam.ips`https://localhost[/system/console/slinglog:4502）を通じて ](https://localhost:4502/system/console/slinglog) パッケージのログレベルをデバッグに引き上げると、さらに詳しい情報を集めることができます。

### バージョン管理 {#version-control}

既存の Dynamic Media アセット（同じ名称、同じ場所）を置換する際、双方のアセットを保持またはバージョンを置換／作成の選択が可能です。

* 両方を保持すると、公開済みアセット URL の名前が一意なアセットが作成されます。例えば、`image.jpg` は元のアセットで、`image1.jpg` は新しくアップロードされたアセットです。

* Dynamic Media ではバージョンの作成はサポートされていません。配信の既存アセットが新しいバージョンに置き換わります。

## 画像とセット {#images-and-sets}

画像とセットで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>アセットの詳細表示で URL／埋め込みコードのコピーボタンにアクセスできない</td>
   <td>
    <ol>
     <li><p>CRX/DE に移動します。</p>
      <ul>
       <li>JCR 内のプリセット <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> が定義されているかどうかを確認します。この場所は、Experience Manager 6.x から 6.4 にアップグレードし、移行をオプトアウトした場合に適用されます。それ以外の場合、場所は <code>/conf/global/settings/dam/dm/presets/viewer</code> になります。</li>
       <li>JCR のアセットに <code>dam:scene7FileStatus</code><strong> </strong> があり、それが「メタデータ」で <code>PublishComplete</code> と表示されていることを確認します。</li>
      </ul> </li>
    </ol> </td>
   <td><p>ページを更新するか、別のページに移動してから戻ります（サイドレール JSP を再コンパイルする必要があります）。</p> <p>それでも解決しない場合：</p>
    <ul>
     <li>アセットを公開します。</li>
     <li>アセットを再度アップロードして公開します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>スライドを切り替えた後、カルーセルホットスポットが移動する</td>
   <td><p>すべてのスライドが同じサイズであることを確認します。</p> </td>
   <td><p>カルーセルには同じサイズの画像のみを使用します。</p> </td>
  </tr>
  <tr>
   <td>Dynamic Media ビューアで画像がプレビューされない</td>
   <td><p>アセットのメタデータプロパティに <code>dam:scene7File</code> が含まれていることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が完了したことを確認します。</p> </td>
  </tr>
  <tr>
   <td>アップロードしたアセットがアセットセレクターに表示されない</td>
   <td><p>アセットのプロパティ <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> が <code>processed</code> であることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が完了したことを確認します。</p> </td>
  </tr>
  <tr>
   <td>アセットの処理がまだ開始していないときに、カードビューのバナーに「<strong>新規</strong>」と表示される</td>
   <td>アセットの <code>jcr:content</code> &gt; <code>dam:assetState</code> を確認します。<code>unprocessed</code> の場合は、アセットの処理がワークフローで開始されていません。</td>
   <td>ワークフローがアセットの処理を始めるまで待ちます。</td>
  </tr>
  <tr>
   <td>画像やセットにビューア URL や埋め込みコードが表示されない</td>
   <td>ビューアプリセットが公開されているかどうかを確認します。</td>
   <td><p><strong>ツール</strong>／<strong>アセット</strong>／<strong>ビューアプリセット</strong>に移動し、ビューアプリセットを公開します。</p> </td>
  </tr>
 </tbody>
</table>

## ビデオ {#video}

ビデオで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>ビデオをプレビューできない</td>
   <td>
    <ul>
     <li>（サポートされていないファイル形式の場合）フォルダーにビデオプロファイルが割り当てられていることを確認します。サポートされていない場合は、画像のみが表示されます。</li>
     <li>AVS セットを生成するには、ビデオプロファイルに複数のエンコーディングプリセットが含まれている必要があります（単一のエンコーディングは MP4 ファイルのビデオコンテンツとして扱われます。サポートされていないファイルの場合は、未処理のファイルと同じように扱われます）。</li>
     <li>メタデータで <code>dam:scene7File</code> の <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>エンコーディングプリセットを 2 つ以上含むよう、ビデオプロファイルを編集します。</li>
     <li>ビデオの処理が終了するまで待ちます。</li>
     <li>ビデオを再度読み込む前に、「Dynamic Media エンコーディングビデオ」ワークフローが実行されていないことを確認します。<br/> </li>
     <li>ビデオを再度アップロードします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオがエンコードされていない</td>
   <td>
    <ul>
     <li>Dynamic Media Cloud Service が設定されていることを確認します。</li>
     <li>ビデオプロファイルがアップロードフォルダーに関連付けられていることを確認します。</li>
    </ul> </td>
   <td>
    <ol>
     <li>クラウドサービスページで Dynamic Media 設定が正しくセットアップされていることを確認します。</li>
     <li>フォルダーにビデオプロファイルが含まれていることを確認します。そのビデオプロファイルも確認します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオの処理に時間がかかりすぎる</td>
   <td><p>ビデオのエンコーディングがまだ進行中か、エラー状態になっているかを判断するには、次の手順を実行します。</p>
    <ul>
     <li>ビデオのステータスを確認します。<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ビデオレンディションがありません</td>
   <td><p>ビデオがアップロードされたが、エンコードされたレンディションがない場合。</p>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します。</li>
     <li>メタデータで <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>ビデオの処理が終わるまで待ちます。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## ビューア {#viewers}

ビューアで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

### 問題：ビューアプリセットが公開されていない {#viewers-not-published}

**デバッグの方法**

1. サンプルマネージャー診断ページ `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html` に移動します。
1. 計算された値を確認します。正しく動作すると、次のように表示されます。`_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`。

   >[!NOTE]
   >
   >Dynamic Media クラウドの設定後、ビューアアセットが同期するまで 10 分ほどかかることがあります。

1. アクティブでないアセットが残る場合は、「**アクティブでないアセットをすべて表示**」ボタンのどちらかを選択して詳細を確認してください。

**解決策**

1. 管理ツールのビューアプリセットリスト（`https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`）に移動します。
1. すべてのビューアプリセットを選択したあと、「**公開**」を選択します。
1. サンプルマネージャーに戻り、アクティブでないアセット数がゼロになったことを確認します。

### 問題：ビューアプリセットのアートワークが、アセット詳細のプレビューまたは URL をコピー／埋め込みコードで 404 を返す {#viewer-preset-404}

**デバッグの方法**

CRXDE Lite で以下を行います。

1. Dynamic Media 同期フォルダー内の `<sync-folder>/_CSS/_OOTB` フォルダー（例えば `/content/dam/_CSS/_OOTB`）に移動します。
1. 問題のあるアセットのメタデータノードを見つけます（例えば `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`）。
1. `dam:scene7*` プロパティがあることを確認します。アセットの同期と公開に成功した場合は `dam:scene7FileStatus` が **PublishComplete** に設定されています。
1. 次のプロパティと文字列リテラルの値を連結して Dynamic Media に直接アートワークを要求します。

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
例：`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解決策**

サンプルアセットまたはビューアプリセットのアートワークが同期されていないか、公開されてない場合は、コピー／同期処理全体を再起動します。

1. CRXDE Lite に移動します。
1. `<sync-folder>/_CSS/_OOTB` を削除します。
1. CRX パッケージマネージャー（`https://localhost:4502/crx/packmgr/`）に移動します。
1. リストでビューアパッケージを検索します（`cq-dam-scene7-viewers-content` で始まります）。
1. 「**再インストール**」を選択します。
1. クラウドサービスページで、Dynamic Media 設定ページに移動した後、Dynamic Media - Scene7 設定の設定ダイアログボックスを開きます。
1. 何も変更せず、「**保存**」をクリックします。この保存アクションで、サンプルアセット、ビューアプリセット CSS およびアートワークを作成および同期するロジックが、再度トリガーされます。

### 問題：ビューアプリセットのオーサリングで画像プレビューが読み込まれない {#image-preview-not-loading}

**解決策**

1. Experience Manager で、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。
1. 左側のパネルで、次の場所にあるサンプルコンテンツフォルダーに移動します。

   `/content/dam/_DMSAMPLE`

1. `_DMSAMPLE` フォルダーを削除します。
1. 左側のパネルで、次の場所にあるプリセットフォルダーに移動します。

   `/conf/global/settings/dam/dm/presets/viewer`

1. `viewer` フォルダーを削除します。
1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。
1. CRXDE Lite ページの左上隅にある「**ホームに戻る**」アイコンを選択します。
1. [Cloud Services の Dynamic Media 設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)を再作成します。
