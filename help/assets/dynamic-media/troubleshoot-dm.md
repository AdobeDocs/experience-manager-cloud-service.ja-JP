---
title: ダイナミックメディアのトラブルシューティング
description: ダイナミックメディアのトラブルシューティング
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# ダイナミックメディアのトラブルシューティング {#troubleshooting-dynamic-media-scene-mode}

次のドキュメントでは、ダイナミックメディアのトラブルシューティングについて説明します。

## General (All Assets) {#general-all-assets}

次に全般的なヒントやテクニックを示します。

### アセット同期ステータスプロパティ {#asset-synchronization-status-properties}

CRXDE Lite で次のアセットプロパティを見直すと、AEM から Dynamic Media へのアセットの同期に成功したことが確認できます。

| **プロパティ** | **例** | **説明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | ノードが Dynamic Media にリンクされていることを示す全般的インジケーター。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** またはエラーテキスト | Dynamic Media へのアセットアップロードのステータス。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic Media のリモートアセットへの URL を生成するには、これを入力する必要があります。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** or **failed:`<error text>`** | セット（スピンセット、画像セットなど）、画像プリセット、ビューアプリセット、アセットの画像マップの更新、編集された画像などの同期ステータス。 |

### 同期のログ {#synchronization-logging}

Synchronization errors and issues are logged in `error.log` (AEM server directory `/crx-quickstart/logs/`). Sufficient logging is available to determine the root cause of most issues, however you can increase the logging to DEBUG on the `com.adobe.cq.dam.ips` package through the Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) to gather more information.

### 移動、コピー、削除 {#move-copy-delete}

移動、コピーまたは削除の処理を実行する前に次をおこなってください。

* For images and videos, confirm that a `<object_node>/jcr:content/metadata/dam:scene7ID` value exists before performing move, copy, or delete operations.
* For image and viewer presets, confirm that an `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` value exists before performing move, copy, or delete operations.
* 上記のメタデータ値がない場合、移動、コピーまたは削除処理の前にアセットを再度アップロードする必要があります。

### バージョン管理 {#version-control}

既存の Dynamic Media アセット（同じ名称、同じ場所）を置換する際、双方のアセットを保持またはバージョンを置換・作成の選択が可能です。

* 両方を保持すると、公開済みアセットURLに対して一意の名前を持つ新しいアセットが作成されます。 例えば、は元のア `image.jpg` セットで、は新しくアッ `image1.jpg` プロードされたアセットです。

* バージョンの作成はダイナミックメディアではサポートされていません。 配信で新しいバージョンが既存のアセットを置換します。

## 画像とセット {#images-and-sets}

画像とセットで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>OS クリップボードと内部 AEM クリップボードを使用した</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>アセットの詳細表示で URL をコピー／埋め込みボタンにアクセスできない</td>
   <td>
    <ol>
     <li><p>CRX/DE に移動します。</p>
      <ul>
       <li>JCR内のプリセットが定義されているかどうかを確認 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> します。 この場所は、AEM 6.x から 6.4 にアップグレードし、移行をオプトアウトした場合に適用されます。それ以外の場所はです <code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>Check to make sure that the asset in the JCR has <code>dam:scene7FileStatus</code><strong> </strong>under Metadata shows as <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>ページを更新するか、別のページに移動してから戻ります（サイドレール JSP を再コンパイルする必要があります）。</p> <p>それでも解決しない場合：</p>
    <ul>
     <li>アセットを公開します。</li>
     <li>アセットを再度アップロードして公開します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>設定エディターのアセットセレクターが永続的に読み込み中の状態になっている</td>
   <td><p>6.4 で解決予定の既知の問題です。</p> </td>
   <td><p>セレクターを閉じて再度開きます。</p> </td>
  </tr>
  <tr>
   <td>セットの編集でアセットを選択した後、<strong>選択</strong>ボタンが有効にならない</td>
   <td><p> </p> <p>6.4 で解決予定の既知の問題です。</p> <p> </p> </td>
   <td><p>アセットセレクターで別のフォルダーをクリックしてからアセットの選択に戻ります。</p> </td>
  </tr>
  <tr>
   <td>スライドを切り替えた後、カルーセルホットスポットが移動する</td>
   <td><p>すべてのスライドが同じサイズであることを確認します。</p> </td>
   <td><p>カルーセルにはすべて同じサイズの画像のみを利用します。</p> </td>
  </tr>
  <tr>
   <td>Dynamic Media ビューアで画像がプレビューされない</td>
   <td><p>Check that the asset contains <code>dam:scene7File</code> in the Metadata properties (CRXDE Lite)</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アップロードしたアセットがアセットセレクターに表示されない</td>
   <td><p>Check asset has property <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アセットの処理がまだ開始していないときに、カード表示のバナーに「<strong>新規</strong>」と表示される</td>
   <td>Check asset <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> it was not picked up by the workflow.</td>
   <td>ワークフローがアセットの処理を始めるまで待ちます。</td>
  </tr>
  <tr>
   <td>画像やセットでビューア URL や埋め込みコードが表示されない</td>
   <td>ビューアプリセットが公開されているかどうかを確認します。</td>
   <td><p>Go to <strong>Tools</strong> &gt; <strong>Assets</strong> &gt; <strong>Viewer Presets</strong> and publish the viewer preset.</p> </td>
  </tr>
 </tbody>
</table>

## ビデオ {#video}

ビデオで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>OS クリップボードと内部 AEM クリップボードを使用した</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>ビデオをプレビューできない</td>
   <td>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します（サポートされていないファイル形式の場合）。サポートされていない場合、画像だけが表示されます。</li>
     <li>ビデオプロファイルには AVS セットを生成するためのエンコーディングプリセットが 2 つ以上含まれている必要があります（MP4 ファイルでは 1 つのエンコーディングがビデオコンテンツとして扱われます。サポートされていないファイルでは、処理されていないものと同じ扱いになります）。</li>
     <li>Check that the video has finished processing by confirming <code>dam:scene7FileAvs</code> of <code>dam:scene7File</code> in metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>エンコーディングプリセットを 2 つ以上含むよう、ビデオプロファイルを編集します。</li>
     <li>ビデオの処理が終わるのを待ちます。</li>
     <li>ビデオを再度読み込み、「Dynamic Media エンコーディングビデオ」ワークフローが実行されていないことを確認します。<br/> </li>
     <li>ビデオを再度アップロードします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオがエンコードされていない</td>
   <td>
    <ul>
     <li>Dynamic Media クラウドサービスが設定されていることを確認します。</li>
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
     <li>ビデオの状態を確認しま <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> す。 <code>dam:assetState</code></li>
     <li>Monitor the video from the workflow console <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Instances, Archive, Failures tabs.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ビデオレンディションがない</td>
   <td><p>ビデオがアップロードされても、エンコードされたレンディションがない場合：</p>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します。</li>
     <li>Check that the video has finished processing by confirming <code>dam:scene7FileAvs</code> in metadata.</li>
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
   <td><strong>OS クリップボードと内部 AEM クリップボードを使用した</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>ビューアプリセットが公開されていない</td>
   <td><p>サンプルマネージャーの診断ページに進みます。 <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>計算された値を確認します。正常に動作している場合は、次のようになります。</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>：Dynamic Media クラウドの設定後、ビューアアセットが同期するまで 10 分ほどかかることがあります。</p> <p>アクティブでないアセットが残る場合は、「<strong>アクティブでないアセットをすべて表示</strong>」ボタンのどちらかをクリックして詳細を確認してください。</p> </td>
   <td>
    <ol>
     <li>管理ツールでビューアプリセットリストに移動します。 <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>すべてのビューアプリセットを選択し、「<strong>公開</strong>」をクリックします。</li>
     <li>サンプルマネージャーに戻り、アクティブでないアセット数がゼロになったことを確認します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビューアプリセットのアートワークが、アセット詳細のプレビューまたはコピー URL／埋め込みコードで 404 を返す場合</td>
   <td><p>CRXDE Lite で以下をおこないます。</p>
    <ol>
     <li>Navigate to <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> folder within your Dynamic Media sync folder (for example, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Find the metadata node of the problematic asset (for example, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Check for the presence of <code>dam:scene7*</code> properties. If the asset was successfully synced and published you see the <code>dam:scene7FileStatus</code> set is to <strong>PublishComplete</strong>.</li>
     <li>次のプロパティと文字列リテラルの値を連結して Dynamic Media に直接アートワークを要求します。
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>サンプルアセットまたはビュープリセットのアートワークが同期されていないか、公開されてない場合は、コピー／同期処理全体をやり直します。</p>
    <ol>
     <li>CRXDE Lite に移動します。
      <ul>
       <li>削除 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Navigate to the CRX package manager: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>リストでビューアパッケージを検索します（<code>cq-dam-scene7-viewers-content</code> で始まります）。</li>
       <li>「<strong>再インストール</strong>」をクリックします。</li>
      </ol> </li>
     <li>クラウドサービスページで、Dynamic Media 設定ページに移動した後、Dynamic Media - Scene7 設定の設定ダイアログボックスを開きます。
      <ul>
       <li>何も変更せず、「<strong>保存</strong>」をクリックします。これで、サンプルアセット、ビューアプリセット CSS およびアートワークを作成および同期するロジックが再度トリガーされます。<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

