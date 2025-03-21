---
title: アセットのプレビュー
description: ユーザーが独自の web ブラウザーでアセットを確認できるように、Dynamic Mediaでアセットをプレビューする方法を説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 3928798d-352a-42a8-a544-7104fc9b3cf1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 97%

---

# アセットのプレビュー{#previewing-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

プレビューを使用して、アップロードしたデジタルアセットがユーザーによる Web ブラウザーでの閲覧時にどのように表示されるかを確認できます。アセットに割り当てられたデフォルトのクロスデバイス対応組み込みビューアがプレビューに使用されます。

ビューアは、様々な設定や「プリセット」の集まりです。例えば、ビューアの表示サイズ、ズーム時の動作、配色、境界線、フォントなどがあります。これらは、ユーザーのコンピューター画面やモバイルデバイスでリッチメディアアセットがどのように表示されるかを決定するものです。

ビデオ、スピンセット、および画像セット専用のプレビュー機能を使用する以外に、作成したビューアプリセットを使用してアセットをプレビューすることもできます。または、画像プリセットを使用して、画像のレンディションをプレビューします。

* [画像プリセットの適用](/help/assets/dynamic-media/image-presets.md)
* [ビューアプリセットの適用](/help/assets/dynamic-media/viewer-presets.md)

>[!NOTE]
>
>Adobe Experience Manager の Web ページ（Sites）で操作しているときは、**[!UICONTROL 編集]**&#x200B;モードでアセットをプレビューできません。プレビューモードに移るには、ページの右上隅の「**[!UICONTROL プレビュー]**」を選択します。

ユーザーインターフェイスでビューアプリセットを有効または無効にする方法については、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

**アセットをプレビューするには：**

1. **[!UICONTROL Experience Manager]** で、**[!UICONTROL ナビゲーション]**&#x200B;ページの「**[!UICONTROL アセット]**」を選択したあと、「**[!UICONTROL ファイル]**」を選択してアセットにアクセスします。
1. ページの右上隅付近にある「**[!UICONTROL 表示]**」ドロップダウンリストで「**[!UICONTROL リスト表示]**」を選択します。
1. （オプション）「**[!UICONTROL 種類]**」列を使用して、プレビューする種類でアセットを並べ替えます。
1. 「**[!UICONTROL タイトル]**」列で、プレビューするアセットの（サムネール画像ではなく）タイトル名を選択します。
1. 選択したアセットの種類に応じて、次のいずれかの操作を行います。

   <table>
    <tbody>
      <tr>
      <td><strong>選択したアセットタイプ</strong><br /> </td>
      <td><strong>特定のレンディションでアセットをプレビューできるか</strong></td>
      <td><strong>特定のビューアでアセットをプレビューできるか</strong></td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>いいえ</td>
      <td>はい</td>
      <td><p><strong>3D アセットをディメンショナルビューアにプレビューするには</strong></p>
      <ul>
      <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストで「<strong>ビューア</strong>」を選択したあと、ディメンショナルビューアを選択します。</li>
      <li>画像を元のズームに戻すには、「<strong>リセット</strong>」を選択します。</li>
      <li>表示デバイスのビューアを最大化するには、「<strong>フルスクリーン</strong>」を選択します。</li>
      </ul>
      <p><strong>3D シーンの操作</strong></p>
      <ul>
      <li><p><strong>3D カメラを回転</strong> - 3D シーンとオブジェクトの周りを回転します。</p> マウス：左クリックしながらドラッグします。</p> タッチスクリーン：指で押しながらドラッグします。</p></li>
      <li><p><strong>カメラをパン</strong> - ビューを左右上下にパンします。</p> マウス：右クリックしながらドラッグします。</p> タッチスクリーン：2 本指で押しながらドラッグします。</p></li>
      <li><p><strong>カメラをズーム</strong> - 3D シーンの領域をズームインまたはズームアウトする場合に使用します。</p> マウス：ホイールをスクロールします。</p> タッチスクリーン：指でつまみます。</p></li>
      <li><p><strong>カメラ視野の中心を変更</strong> - 3D シーンとオブジェクトの周りを回転します。</p> マウス：ダブルクリックします。</p> タッチスクリーン：ダブルクリックします。</li></ul></td>
      </tr>
      <tr>
      <td><p>画像</p> </td>
      <td>はい</td>
      <td>はい</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>レンディション</strong>」を選択したあと、プレビューする特定のレンディションを選択します。</li>
        </ul> <p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」を選択して、アセットに適用するビューアを選択します。</li>
        </ul><p>「<strong>+</strong>」および「<strong>-</strong>」アイコンを使用して、選択した画像のズームを増減します。画像を元のズームマップに戻すには、「<strong>リセット</strong>」を選択します。<br>タッチスクリーンを使用している場合は、画像をダブルクリックすると、画像を少しずつズームインできます。最大ズームに達したら、画像を再度ダブルクリックして、ズーム状態をリセットします。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>マルチメディア</td>
      <td>はい</td>
      <td>はい</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>レンディション</strong>」を選択したあと、プレビューする特定のレンディションを選択します。</li>
        </ul><p>高解像度のビデオレンディションをプレビュー用に選択すると、ビデオが切り詰められて表示される場合があります。これは、レンディションプレビューがすべて、プレビューに使用される組み込みビューアのコンテキストで、ユーザー向けの解像度で表示されるからです。</p><p>アセットレベルでアダプティブビデオセットをプレビューすると、レンディションが一度の再生にまとめられます。つまり、アダプティブビデオのサイズが閲覧用に適切に調整され、現在の表示デバイスと接続速度のコンテキストにおいて最適な解像度で再生されます。<br /></p><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」を選択して、アセットに適用するビューアを選択します。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>画像セット</td>
      <td>不可</td>
      <td>可</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」を選択して、アセットに適用するビューアを選択します。</li>
        </ul> <p>「<strong>+</strong>」および「<strong>-</strong>」アイコンを使用して、選択した画像のズームを増減します。画像を元のズームマップに戻すには、「<strong>リセット</strong>」を選択します。<br />タッチスクリーンを使用している場合は、画像をダブルクリックすると、画像を少しずつズームインできます。最大ズームに達したら、画像を再度ダブルクリックして、ズーム状態をリセットします。画像全体をドラッグするように動かすと、パンします。</p></td>
      </tr>
      <tr>
      <td>スピンセット</td>
      <td>不可</td>
      <td>可</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」を選択して、アセットに適用するビューアを選択します。</li>
        </ul><p>「<strong>+</strong>」および「<strong>-</strong>」アイコンを使用して、選択した画像のズームを増減します。画像を元のズームマップに戻すには、「<strong>リセット</strong>」を選択します。<br />タッチスクリーンを使用している場合は、画像をダブルクリックすると、画像を少しずつズームインできます。最大ズームに達したら、画像を再度ダブルクリックして、ズーム状態をリセットします。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>混在メディアセット</td>
      <td>不可</td>
      <td>可</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」を選択して、アセットに適用するビューアを選択します。</li>
        </ul> <p>「<strong>+</strong>」および「<strong>-</strong>」アイコンを使用して、選択した画像のズームを増減します。画像を元のズームマップに戻すには、「<strong>リセット</strong>」を選択します。<br />タッチスクリーンを使用している場合は、画像をダブルクリックすると、画像を少しずつズームインできます。最大ズームに達したら、画像を再度ダブルクリックして、ズーム状態をリセットします。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>カルーセルセット</td>
      <td>不可</td>
      <td>可</td>
      <td><strong>特定のビューアでアセットをプレビューするには：</strong>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。アセットに適用するビューアを選択します。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360 ビデオ<br /> </td>
      <td>はい</td>
      <td>はい</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。「<strong>レンディション</strong>」を選択した後、プレビューするレンディションを選択します。</li>
        </ul> <p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンを選択して、ドロップダウンリストを表示します。「<strong>ビューア</strong>」を選択した後、アセットに適用するビューアを選択します。</li>
        </ul> <p>「<strong>+</strong>」および「<strong>-</strong>」アイコンを使用して、選択した画像のズームを増減します。画像を元のズームマップに戻すには、「<strong>リセット</strong>」を選択します。<br />タッチスクリーンを使用している場合は、画像をダブルクリックすると、画像を少しずつズームインできます。最大ズームに達したら、画像を再度ダブルクリックして、ズーム状態をリセットします。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
    </tbody>
    </table>
