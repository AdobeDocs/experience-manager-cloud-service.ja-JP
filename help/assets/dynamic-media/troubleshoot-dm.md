---
title: Dynamic Media のトラブルシューティング
description: Dynamic Media 使用時のトラブルシューティングのヒント
topic: 「管理者、実業家」
role: Administrator,Business Practitioner
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 77%

---

# Dynamic Media のトラブルシューティング {#troubleshooting-dynamic-media-scene-mode}

以下のトピックでは、Dynamic Media のトラブルシューティングについて説明します。

## 新しい Dynamic Media 設定 {#new-dm-config}

[新しいDynamic Media構成のトラブルシューティング](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)を参照してください。

## 一般（すべてのアセット） {#general-all-assets}

次に全般的なヒントやテクニックを示します。

### アセット同期ステータスプロパティ  {#asset-synchronization-status-properties}

次のアセットプロパティをCRXDE Liteで確認し、Adobe Experience ManagerからDynamic Mediaへのアセットの同期が正常に完了していることを確認できます。

| **プロパティ** | **例** | **説明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | ノードが Dynamic Media にリンクされていることを示す全般的インジケーター。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** またはエラーテキスト | Dynamic Media へのアセットアップロードのステータス。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic MediaのリモートアセットへのURLを生成するには、URLを入力する必要があります。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** または **failed:`<error text>`** | セット（スピンセット、画像セットなど）、画像プリセット、ビューアプリセット、アセットの画像マップの更新、編集された画像などの同期ステータス。 |

### 同期のログ  {#synchronization-logging}

同期エラーと問題が`error.log` (Experience Managerサーバーディレクトリ`/crx-quickstart/logs/`)に記録されます。 ログにはほとんどの問題の根本原因を突き止めるのに十分な情報が記録されますが、Sling コンソール（[https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)）を通じて `com.adobe.cq.dam.ips` パッケージのログレベルをデバッグに引き上げると、さらに詳しい情報を集めることができます。

### バージョン管理 {#version-control}

既存のDynamic Mediaアセット（同じ名前と場所）を置き換える場合、両方のアセットを保持するか、バージョンを置き換え/作成できます。

* 両方を維持すると、発行済みアセットURLに対して一意の名前を持つアセットが作成されます。 例えば、`image.jpg` は元のアセットで、`image1.jpg` は新しくアップロードされたアセットです。

* Dynamic Media ではバージョンの作成はサポートされていません。配信内の既存のアセットが、新しいバージョンに置き換えられます。

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
       <li>JCR 内のプリセット <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> が定義されているかどうかを確認します。この場所は、Experience Manager6.xから6.4にアップグレードし、移行をオプトアウトした場合に適用されます。 それ以外の場合は、<code>/conf/global/settings/dam/dm/presets/viewer</code>が場所になります。</li>
       <li>JCR のアセットに <code>dam:scene7FileStatus</code><strong> </strong> があり、それが「メタデータ」で <code>PublishComplete</code> と表示されていることを確認します。</li>
      </ul> </li>
    </ol> </td>
   <td><p>ページを更新/別のページに移動して戻る（サイドレールJSPを再コンパイルする必要がある）</p> <p>それでも解決しない場合：</p>
    <ul>
     <li>アセットを公開します。</li>
     <li>アセットを再アップロードして公開します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>スライドを切り替えた後、カルーセルホットスポットが移動する</td>
   <td><p>すべてのスライドが同じサイズであることを確認します。</p> </td>
   <td><p>カルーセルにはすべて同じサイズの画像のみを利用します。</p> </td>
  </tr>
  <tr>
   <td>Dynamic Media ビューアで画像がプレビューされない</td>
   <td><p>アセットのメタデータプロパティに <code>dam:scene7File</code> が含まれていることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アップロードしたアセットがアセットセレクターに表示されない</td>
   <td><p>アセットのプロパティ <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> が <code>processed</code> であることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アセットの処理がまだ開始していないときに、カード表示のバナーに「<strong>新規</strong>」と表示される</td>
   <td>アセットの <code>jcr:content</code> &gt; <code>dam:assetState</code> を確認します。<code>unprocessed</code> の場合は、アセットの処理がワークフローで開始されていません。</td>
   <td>ワークフローがアセットの処理を始めるまで待ちます。</td>
  </tr>
  <tr>
   <td>画像やセットでビューア URL や埋め込みコードが表示されない</td>
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
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します（サポートされていないファイル形式の場合）。サポートされていない場合、画像だけが表示されます。</li>
     <li>ビデオプロファイルには AVS セットを生成するためのエンコーディングプリセットが 2 つ以上含まれている必要があります（MP4 ファイルでは 1 つのエンコーディングがビデオコンテンツとして扱われます。サポートされていないファイルでは、処理されていないものと同じ扱いになります）。</li>
     <li>メタデータで <code>dam:scene7File</code> の <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>エンコーディングプリセットを 2 つ以上含むよう、ビデオプロファイルを編集します。</li>
     <li>ビデオの処理が終わるのを待ちます。</li>
     <li>ビデオを再読み込みする前に、Dynamic Mediaエンコードビデオワークフローが実行されていないことを確認してください。<br/> </li>
     <li>ビデオを再アップロードします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオがエンコードされていない</td>
   <td>
    <ul>
     <li>Dynamic MediaCloud Serviceが設定されているかどうかを確認します。</li>
     <li>ビデオプロファイルがアップロードフォルダーに関連付けられていることを確認します。</li>
    </ul> </td>
   <td>
    <ol>
     <li>クラウドサービスページで Dynamic Media 設定が正しくセットアップされていることを確認します。</li>
     <li>フォルダーにビデオプロファイルがあることを確認します。そのビデオプロファイルも確認します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオの処理に時間がかかりすぎる</td>
   <td><p>ビデオのエンコーディングがまだ進行中か、エラー状態になっているかを判断するには：</p>
    <ul>
     <li>ビデオのステータスを確認します。<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ビデオレンディションがない</td>
   <td><p>ビデオがアップロードされても、エンコードされたレンディションがない場合：</p>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します。</li>
     <li>メタデータで <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>ビデオの処理が終わるのを待ちます。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## ビューア {#viewers}

ビューアで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>ビューアプリセットが公開されていない</td>
   <td><p>次のサンプルマネージャー診断ページに移動します。 <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>計算された値を確認します。正しく動作している場合は、次の項目が表示されます。</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>：Dynamic Media クラウドの設定後、ビューアアセットが同期するまで 10 分ほどかかることがあります。</p> <p>アクティブでないアセットが残る場合は、「<strong>アクティブでないアセットをすべて表示</strong>」ボタンのどちらかをクリックして詳細を確認してください。</p> </td>
   <td>
    <ol>
     <li>管理ツールのビューアプリセットリストに移動します。 <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>すべてのビューアプリセットを選択し、「<strong>公開</strong>」をクリックします。</li>
     <li>サンプルマネージャーに戻り、アクティブでないアセット数がゼロになったことを確認します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビューアプリセットのアートワークが、アセット詳細のプレビューまたは URL／埋め込みコードのコピーで 404 を返す場合</td>
   <td><p>CRXDE Lite で以下をおこないます。</p>
    <ol>
     <li>Dynamic Media 同期フォルダー内の <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> フォルダー（例えば <code>/content/dam/_CSS/_OOTB</code>）に移動します。</li>
     <li>問題のあるアセットのメタデータノードを見つけます（例えば <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li>
     <li><code>dam:scene7*</code> プロパティがあることを確認します。アセットが正常に同期および公開された場合は、<code>dam:scene7FileStatus</code>セットが<strong>PublishComplete</strong>に設定されていることが表示されます。</li>
     <li>次のプロパティと文字列リテラルの値を連結して Dynamic Media に直接アートワークを要求します。
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>例： <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>サンプルアセットまたはビューアプリセットのアートワークが同期または公開されていない場合は、コピー/同期処理全体を再起動します。</p>
    <ol>
     <li><code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code> に移動します。
     </li>
     <li>次のアクションを順に選択します。
      <ol>
       <li>「Sync」フォルダーを削除します。</li>
       <li>プリセットフォルダを削除します（<code>/conf</code>の下）。
       <li>DM セットアップ非同期ジョブをトリガします。</li>
      </ol> </li>
     <li>Experience Managerの受信トレイで同期が成功したという通知が表示されるまで待ちます。
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
