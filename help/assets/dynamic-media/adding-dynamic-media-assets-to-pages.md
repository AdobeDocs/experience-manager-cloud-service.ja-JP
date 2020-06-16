---
title: ページへの Dynamic Media アセットの追加
description: AEM 内のページに Dynamic Media コンポーネントを追加する方法
translation-type: tm+mt
source-git-commit: a4c06ed7a01cd61ab1e53bba8acc5e276c8bad99
workflow-type: tm+mt
source-wordcount: '3124'
ht-degree: 98%

---


# ページへの Dynamic Media アセットの追加{#adding-dynamic-media-assets-to-pages}

Web サイトで使用するアセットに Dynamic Media 機能を追加するには、**Dynamic Media**、**インタラクティブメディア**、**パノラマメディア**、**ビデオ 360 メディア**&#x200B;のいずれかのコンポーネントをページに直接追加します。これをおこなうには、レイアウトモードに入り、Dynamic Media コンポーネントを有効にします。次に、これらのコンポーネントをページに追加し、そのコンポーネントにアセットを追加できます。Dynamic Media コンポーネントはスマートです。追加しようとしているアセットが画像、ビデオのどちらなのかが検出され、それに応じて利用可能なオプションが変わります。

AEM を WCM として使用している場合は、Dynamic Media アセットを直接ページに追加します。サードパーティの製品を WCM として使用している場合は、アセットの[リンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)または[埋め込み](/help/assets/dynamic-media/embed-code.md)をおこないます。サードパーティのレスポンシブ Web サイトについては、[レスポンシブサイトへの最適化された画像の配信](/help/assets/dynamic-media/responsive-site.md)を参照してください。

>[!NOTE]
>
>AEM のページに追加する前にアセットを公開する必要があります。[Dynamic Media アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## ページへの Dynamic Media コンポーネントの追加 {#adding-a-dynamic-media-component-to-a-page}

ページに3Dメディア、Dynamic Media、インタラクティブメディア、パノラマメディア、スマート切り抜きビデオまたはビデオ360メディアの各コンポーネントを追加する方法は、ページにコンポーネントを追加する方法と同じです。 Dynamic Media コンポーネントについては、後の節で説明します。

**ページへの Dynamic Media コンポーネントの追加**

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. 左側のウィンドウで、「**[!UICONTROL コンポーネント]**」アイコンをタップし、「Dynamic Media」でフィルタリングします。

   Dynamic Media コンポーネントのリストがない場合は、使用する Dynamic Media コンポーネントを有効にしなければならない可能性があります。詳しくは、[Dynamic Media コンポーネントの有効化](#enabling-dynamic-media-components)を参照してください。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. **[!UICONTROL Dynamic Media]** コンポーネントをドラッグし、ページ上の目的の場所でドロップします。

1. コンポーネントの上に直接マウスポインターを置きます。コンポーネントが青色のボックスで囲まれた時点で 1 回タップすると、コンポーネントのツールバーが表示されます。**[!UICONTROL 設定（レンチ）]** アイコンをタップします。

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. ページにドロップした Dynamic Media コンポーネントに対応する設定ダイアログボックスが開きます。[必要に応じて、コンポーネントのオプションを設定します](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)。

   以下の例では、Dynamic Media **[!UICONTROL ビデオ 360 メディア]**&#x200B;コンポーネントのダイアログボックスと、「ビューアプリセット」ドロップダウンリストで利用可能なオプションが表示されています。

   ![ビデオ 360 メディアコンポーネント](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media ビデオ 360 メディアコンポーネント。

1. 完了したら、ダイアログボックスの右上隅にあるチェックマークをタップして、変更を保存します。

### Dynamic Media コンポーネントの有効化 {#enabling-dynamic-media-components}

ページに追加できる Dynamic Media コンポーネントがない場合は、使用するコンポーネントをまず有効にしなければならない可能性があります。

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. ページ上部付近のツールバーの左側にあるページ情報アイコンをタップした後、ドロップダウンリストから「**[!UICONTROL テンプレートを編集]**」をタップします。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 構造]**」をタップします。

   ![ポリシー](/help/assets/assets-dm/structure-mode.png)

1. ページ下部付近の「**[!UICONTROL レイアウトコンテナ]**」をタップしてツールバーを開き、ポリシーアイコンをタップします。
1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの「**[!UICONTROL プロパティ]**」見出しの下で、「**[!UICONTROL 許可されたコンポーネント]**」タブが選択されていることを確認します。

   ![許可されたコンポーネント](/help/assets/assets-dm/allowed-components.png)

1. **[!UICONTROL Dynamic Media]** が表示されるまでスクロールします。
1. **[!UICONTROL Dynamic Media]** の左側にある「>」アイコンをタップしてリストを展開し、有効にする Dynamic Media コンポーネントを選択します。

   ![Dynamic Media コンポーネントリスト](/help/assets/assets-dm/dm-components-select.png)

1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの右上隅付近にある「完了」（チェックマーク）アイコンをタップします。

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 初期コンテンツ]**」をタップした後、通常どおりに[ページに Dynamic Media コンポーネントを追加](#adding-a-dynamic-media-component-to-a-page)します。

## Dynamic Media コンポーネントのローカライズ {#localizing-dynamic-media-components}

Dynamic Media コンポーネントのローカライズの方法は 2 つあります。

* Sites の Web ページ内で、**[!UICONTROL プロパティ]**&#x200B;を開き、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* サイトセレクターからページあるいはページグループを選択します。「**[!UICONTROL プロパティ]**」をタップし、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

   >[!NOTE]
   >
   >現在&#x200B;**[!UICONTROL 言語]**&#x200B;メニューに表示される言語すべてにトークンが割り当てられているわけではないことに注意してください。

## 使用可能な Dynamic Media コンポーネント {#dynamic-media-components}

「**[!UICONTROL コンポーネント]**」アイコンをタップし、「**[!UICONTROL Dynamic Media]**」でフィルタリングすると、Dynamic Media コンポーネントが利用可能になります。

利用可能な Dynamic Media コンポーネントは次のとおりです。

* **** Dynamic Media - 画像、ビデオ、eCatalog、スピンセットなどのアセットに使用します。
* **[!UICONTROL インタラクティブメディア]** - すべてのインタラクティブアセット（インタラクティブビデオ、インタラクティブ画像、カルーセルセットなど）に使用します。
* **[!UICONTROL パノラマメディア -]** パノラマ画像またはパノラマ VR 画像アセットに使用します。
* **[!UICONTROL ビデオ 360 メディア]** - 360 ビデオおよび 360 VR ビデオアセットに使用します。

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用前にテンプレートエディターで使用可能にする必要があります。テンプレートエディターでコンポートを使用可能にした後は、他の AEM コンポーネントと同様にページに追加することができます。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### コンポーネント：Dynamic Media {#dynamic-media-component}

Dynamic Media コンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されている Dynamic Media コンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。

>
>
そのページの各 Dynamic Media コンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされないことに注意してください。
>
>一方、ページ内で、同じタイプのアセットを使用するすべての Dynamic Media コンポーネントで同じビューアプリセットを使用することは可能です。

Dynamic Media コンポーネントを追加したときに、「**[!UICONTROL Dynamic Media 設定]**」が空であるかアセットを適切に追加できない場合は、次の点を確認してください。

* 画像が PTIFF（Pyramid TIFF）ファイルであること。Dynamic Media を有効にする前に読み込まれた画像には、pyramid tiff ファイルはありません。

#### 画像を操作する場合 {#when-working-with-images}

Dynamic Media コンポーネントでは、画像セット、スピンセット、混在メディアセットなどの動的イメージを追加できます。ズームイン、ズームアウト、スピンセット内での画像の回転（該当する場合）または別のタイプのセットからの画像の選択をおこなうことができます。

また、ビューアプリセット、画像プリセットまたは画像形式をコンポーネント内で直接設定することもできます。画像をレスポンシブにするために、ブレークポイントの設定かレスポンシブ画像プリセットの適用のいずれかを実行できます。

コンポーネント内の&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをタップし、次に「**[!UICONTROL Dynamic Media 設定]**」をタップすると、次の Dynamic Media 設定を編集することができます。

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>デフォルトでは、Dynamic Media 画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL ビューアプリセット]** - ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

   これは、画像セット、スピンセットまたは混在メディアセットを表示している場合に唯一使用できるオプションです。表示されるビューアプリセットもスマートであり、関連するビューアプリセットのみが表示されます。

* **[!UICONTROL ビューア修飾子]** - ビューア修飾子は、名前=値の組み合わせで &amp; を区切り文字とした形式です。ビューア修飾子を使用すると、ビューアリファレンスガイドに概略が記されているとおり、ビューアを変更することができます。`posterimage=img.jpg&caption=text.vtt,1` はビューア修飾子の一例で、これはビデオのサムネールに異なる画像を設定し、ビデオにクローズキャプションや字幕ファイルを関連付けます。

* **[!UICONTROL 画像プリセット]** - ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。「画像プリセットの管理」を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 画像の修飾子]** - 追加の画像コマンドを指定すると、画像エフェクトを適用できます。これらは画像プリセットと画像をサーブするコマンドリファレンスに記述されています。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL ブレークポイント]** - レスポンシブサイトでこのアセットを使用する場合は、画像のブレークポイントを追加する必要があります。画像のブレークポイントをコンマ（,）で区切って指定する必要があります。このオプションを使用できるのは、画像プリセットで高さまたは幅が定義されていないときです。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

   コンポーネントの「**[!UICONTROL 編集]**」をタップして、次の詳細設定を編集できます。

* **[!UICONTROL タイトル]** - 画像のタイトルを変更します。

* **[!UICONTROL 代替テキスト]** - グラフィックの表示をオフにしているユーザー向けのタイトルを画像に追加します。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL URL、次のウィンドウで開く]** - リンクを開くようにアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。


#### ビデオを操作する場合 {#when-working-with-video}

Dynamic Media コンポーネントを使用して、ダイナミックビデオを Web ページに追加します。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

![chlimage_1-173](assets/chlimage_1-540.png)

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の Dynamic Media 設定を編集できます。

>[!NOTE]
>
>デフォルトでは、Dynamic Media ビデオコンポーネントはアダプティブです。ビデオコンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **ビューアプリセット** - ドロップダウンメニューから既存のビデオビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **ビューア修飾子** - ビューア修飾子は、名前=値の組み合わせで &amp; を区切り文字とした形式です。ビューア修飾子を使用すると、Adobe ビューアリファレンスガイドに概略が記されているとおり、ビューアを変更することができます。`posterimage=img.jpg&caption=text.vtt,1` はビューア修飾子の一例です。

   ビューア修飾子を使用すると、例えば次のことが可能です。

   * ビデオにキャプションファイルを関連付ける：[キャプション](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * ビデオにナビゲーションファイルを関連付ける：[ナビゲーション](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の詳細設定を編集できます。

* **[!UICONTROL タイトル** - ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

#### スマート切り抜きを操作する場合 {#when-working-with-smart-crop}

Dynamic Media コンポーネントを使用して、スマート切り抜き画像アセットを Web ページに追加します。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

詳しくは、[AEM Assets Dynamic Media でのスマート切り抜きの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html)を参照してください。

[イメージプロファイル](/help/assets/dynamic-media/image-profiles.md)も参照してください。

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の Dynamic Media 設定を編集できます。

>[!NOTE]
>
>デフォルトでは、Dynamic Media 画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL 画像の修飾子]** - 追加の画像コマンドを指定すると、画像エフェクトを適用できます。これらは画像プリセットと画像をサーブするコマンドリファレンスに記述されています。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

   コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の詳細設定を編集できます。

* **[!UICONTROL 縦横比の一致を有効にする]** - 元の画像の縦横比に最も適した縦横比のスマート切り抜きレンディションを Dynamic Media で選択する場合に選択します。

* **[!UICONTROL タイトル]** - スマート切り抜き画像のタイトルを変更します。

* **[!UICONTROL 代替テキスト]** - グラフィックの表示をオフにしているユーザー向けのタイトルをスマート切り抜き画像に追加します。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL URL、次のウィンドウで開く]** - リンクを開くようにアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

   このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

### コンポーネント：インタラクティブメディア {#interactive-media-component}

インタラクティブメディアコンポーネントは、インタラクティビティ（ホットスポットまたは画像マップ）を含むアセット用です。インタラクティブ画像、インタラクティブビデオまたはカルーセルバナーがある場合は、**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントを使用します。

インタラクティブメディアコンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されているインタラクティブメディアコンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。

>
>
そのページの各インタラクティブメディアコンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされないことに注意してください。
>
>一方、ページ内で、同じタイプのアセットを使用するすべてのインタラクティブメディアコンポーネントで同じビューアプリセットを使用することは可能です。

![chlimage_1-174](assets/chlimage_1-541.png)

コンポーネントの「**[!UICONTROL 編集]**」をタップして、次の&#x200B;**[!UICONTROL 一般]**&#x200B;設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。ビューアプリセットを使用するには、あらかじめ公開する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **[!UICONTROL タイトル]** - ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

   コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 買い物かごに追加]**&#x200B;設定を編集できます。

* **[!UICONTROL 製品アセットを表示]** - デフォルトでは、この値が選択されています。製品アセットには、コマースモジュールで定義された製品の画像が表示されます。製品アセットを表示しない場合はチェックマークをオフにします。

* **[!UICONTROL 製品価格を表示]** - デフォルトでは、この値が選択されています。製品価格には、コマースモジュールで定義されたアイテムの価格が表示されます。製品価格を表示しない場合はチェックマークをオフにします。

* **[!UICONTROL 製品フォームを表示]** - デフォルトでは、この値は選択されていません。製品フォームには、サイズや色など製品のバリエーションが含まれます。製品のバリエーションを表示しない場合はチェックマークをオフにします。

### コンポーネント：パノラマメディア {#panoramic-media-component}

パノラマメディアコンポーネントは、球パノラマ画像のアセット用です。このような画像では、室内、物件、場所、風景などをあらゆる角度から見ることができます。画像が球パノラマとして適格となるには、以下の一方または両方の条件を満たしている必要があります。

* 縦横比が 2:1 である必要があります。
* キーワード `equirectangular` または（`spherical` + `panorama`）または（`spherical` + `panoramic`）でタグ付けされている必要があります。[タグの使用](/help/sites-cloud/authoring/features/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと「**[!UICONTROL パノラマメディア]**」WCM コンポーネントのパノラマアセットに適用されます。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されている&#x200B;**[!UICONTROL パノラマメディア]**&#x200B;コンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。

>
>
そのページの各&#x200B;**[!UICONTROL パノラマメディア]**&#x200B;コンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされないことに注意してください。
>
>一方、ページ内で、同じタイプのアセットを使用するすべてのパノラマメディアコンポーネントで同じビューアプリセットを使用することは可能です。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

コンポーネントの「**[!UICONTROL 設定]**」をタップして、次の設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - 「ビューアプリセット」ドロップダウンメニューから既存のビューアを選択します。

探しているビューアプリセットが表示されない場合は、そのビューアプリセットが公開されていることを確認してください。ビューアプリセットを使用するには、公開する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

### コンポーネント：ビデオ 360 メディア {#video-media-component}

Web ページ上でエクイレクタングラー形式のビデオをレンダリングして部屋、物件、場所、風景、医療処置などの没入感のある視聴体験が得られるようにするには、**[!UICONTROL ビデオ 360 メディア]**&#x200B;コンポーネントを使用します。

フラットディスプレイでの再生時には、ユーザーは視野角を制御できます。また、モバイルデバイスでの再生では通常、デバイス組み込みのジャイロスコープ制御を利用します。

ビューアでは、360 ビデオアセットの配信をネイティブサポートしています。デフォルトでは、表示または再生するための追加設定は不要です。360 ビデオは、.mp4、.mkv、.mov といった標準のビデオ拡張子を使用して配信されます。最も一般的なコーデックは H.264 です。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

コンポーネントの「**[!UICONTROL 設定]**」をタップして、次の設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - 「ビューアプリセット」ドロップダウンメニューから既存のビューアを選択します。バーチャルリアリティグラスを使用するエンドユーザーには、Video360VR を使用します。基本的なビデオ再生コントロールとソーシャルメディア機能を含んでいます。基本的なビデオ再生コントロールを含む Video360_social を使用します。ビデオのレンダリングはステレオモードでおこなわれます。視点の手動制御はオフになり、ジャイロスコープ制御がオンになります。ソーシャルメディア機能はありません。

探しているビューアプリセットが表示されない場合は、そのビューアプリセットが公開されていることを確認してください。ビューアプリセットを使用するには、公開する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

### HTTP/2 を使用した Dynamic Media アセットの配信 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの交信を強化する、新しく更新された Web プロトコルです。このプロトコルを使用すれば、情報の伝送を高速化し、必要な処理能力を抑えることができます。HTTP/2 上で Dynamic Media アセットの配信が可能になり、応答時間と読み込み時間が短縮されました。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](/help/assets/dynamic-media/http2faq.md)を参照してください。

>[!MORELIKETHIS]
>
>* [AEM Dynamic Media でのビデオプレーヤーの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [AEM Dynamic Media でのインタラクティブビデオの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [AEM Dynamic Media でのアセットビューアについて](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [AEM Dynamic Media でのカスタムビデオサムネールの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [AEM Dynamic Media でのカラーマネジメントについて](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [AEM Dynamic Media での画像シャープニングの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

