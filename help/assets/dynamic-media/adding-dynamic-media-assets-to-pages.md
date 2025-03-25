---
title: ページへの Dynamic Media アセットの追加
description: Adobe Experience Manager as a Cloud Service で Dynamic Media コンポーネントをページに追加する方法を説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3165'
ht-degree: 100%

---

# ページへの Dynamic Media アセットの追加{#adding-dynamic-media-assets-to-pages}

Web サイトで使用するアセットに Dynamic Media 機能を追加するには、**Dynamic Media**、**インタラクティブメディア**、**パノラマメディア**、**ビデオ 360 メディア**&#x200B;のいずれかのコンポーネントをページに直接追加します。レイアウトモードに入り、Dynamic Media コンポーネントを有効にします。次に、これらのコンポーネントをページに追加し、そのコンポーネントにアセットを追加します。Dynamic Media コンポーネントはスマートです。追加しようとしているアセットが画像、ビデオのどちらなのかが検出され、それに応じて利用可能なオプションが変わります。

[!DNL Adobe Experience Manager] を WCM として使用している場合は、Dynamic Media アセットをページに直接追加します。サードパーティの製品を WCM として使用している場合は、アセットの[リンク](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)または[埋め込み](/help/assets/dynamic-media/embed-code.md)を行います。サードパーティのレスポンシブ web サイトの場合は、[レスポンシブサイトへの最適化された画像の配信](/help/assets/dynamic-media/responsive-site.md)を参照してください。

>[!NOTE]
>
>[!DNL Experience Manager] でページに追加する前にアセットを必ず公開してください。[Dynamic Media アセットの公開](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)を参照してください。

## ページに Dynamic Media コンポーネントを追加する {#adding-a-dynamic-media-component-to-a-page}

3D メディア、Dynamic Media、インタラクティブメディア、パノラマメディア、スマート切り抜きビデオ、ビデオ 360 メディアのいずれかのコンポーネントを 1 つのページに追加することは、コンポーネントを任意のページに追加することと同じです。

**ページに Dynamic Media コンポーネントを追加するには：**

1. Dynamic Media コンポーネントを追加するページを [!DNL Experience Manager] で開きます。
1. 左側のウィンドウで、「**[!UICONTROL コンポーネント]**」アイコンを選択し、「ダイナミックメディア」でフィルタリングします。

   Dynamic Media コンポーネントのリストがない場合は、使用する Dynamic Media コンポーネントを有効にしなければならない可能性があります。詳しくは、[Dynamic Media コンポーネントの有効化](#enabling-dynamic-media-components)を参照してください。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. **[!UICONTROL Dynamic Media]** コンポーネントをドラッグし、ページ上の目的の場所でドロップします。

1. コンポーネントの上に直接ポインターを置きます。コンポーネントが青色のボックスで囲まれた時点で選択すると、コンポーネントのツールバーが表示されます。**[!UICONTROL 設定（レンチ）]**&#x200B;アイコンを選択します。

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. ページにドロップした Dynamic Media コンポーネントに対応する、設定ダイアログボックスが開きます。必要に応じて、[コンポーネントのオプションを設定します](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)。

   以下の例では、Dynamic Media **[!UICONTROL ビデオ 360 メディア]**&#x200B;コンポーネントのダイアログボックスと、「ビューアプリセット」ドロップダウンリストで利用可能なオプションが表示されています。

   ![ビデオ 360 メディアコンポーネント](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media ビデオ 360 メディアコンポーネント。

1. 完了したら、ダイアログボックスの右上隅にあるチェックマークを選択して、変更を保存します。

### Dynamic Media コンポーネントの有効化 {#enabling-dynamic-media-components}

ページに追加できる Dynamic Media コンポーネントがない場合は、使用するコンポーネントを有効にしなければならない可能性があります。

1. Dynamic Media コンポーネントを追加するページを [!DNL Experience Manager] で開きます。
1. ページ上部付近のツールバーの左側にあるページ情報アイコンを選択した後、ドロップダウンリストから「**[!UICONTROL テンプレートを編集]**」を選択します。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 構造]**」を選択します。

   ![ポリシー](/help/assets/assets-dm/structure-mode.png)

1. ページ下部付近の「**[!UICONTROL レイアウトコンテナ]**」を選択してツールバーを開き、ポリシーアイコンを選択します。
1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの「**[!UICONTROL プロパティ]**」見出しの下で、「**[!UICONTROL 許可されたコンポーネント]**」タブが選択されていることを確認します。

   ![許可されたコンポーネント](/help/assets/assets-dm/allowed-components.png)

1. **[!UICONTROL ダイナミックメディア]**&#x200B;が表示されるまでスクロールします。
1. **[!UICONTROL Dynamic Media]** の左側にある「>」アイコンを選択したあと、有効にする Dynamic Media コンポーネントを選択します。

   ![Dynamic Media コンポーネントリスト](/help/assets/assets-dm/dm-components-select.png)

1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ページの右上隅付近にある完了（チェックマーク）アイコンを選択します。

1. ページ上部付近のツールバーの右側で、ドロップダウンリストから「**[!UICONTROL 初期コンテンツ]**」を選択します。
1. 通常どおり、[Dynamic Media コンポーネントをページに追加](#adding-a-dynamic-media-component-to-a-page)します。

## Dynamic Media コンポーネントをローカライズする {#localizing-dynamic-media-components}

Dynamic Media コンポーネントのローカライズの方法は 2 つあります。

* Sites の Web ページ内で、**[!UICONTROL プロパティ]**&#x200B;を開き、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

  ![chlimage_1-172](assets/chlimage_1-538.png)

* サイトセレクターからページあるいはページグループを選択します。「**[!UICONTROL プロパティ]**」を選択し、「**[!UICONTROL 詳細]**」タブを選択します。ローカライズに使用したい言語を選択します。

  >[!NOTE]
  >
  >**[!UICONTROL 言語]**&#x200B;メニューに表示されるすべての言語にトークンが現在割り当てられているわけではありません。

## 使用可能な Dynamic Media コンポーネント {#dynamic-media-components}

「**[!UICONTROL コンポーネント]**」アイコンを選択し、「**[!UICONTROL Dynamic Media]**」でフィルタリングすると、Dynamic Media コンポーネントが利用可能になります。

利用可能な Dynamic Media コンポーネントは次のとおりです。

* **[!UICONTROL ダイナミックメディア]** - 画像、ビデオ、eCatalog、スピンセットなどのアセットに使用します。
* **[!UICONTROL インタラクティブメディア]** - すべてのインタラクティブアセット（インタラクティブビデオ、インタラクティブ画像、カルーセルセットなど）に使用します。
* **[!UICONTROL パノラマメディア -]** パノラマ画像またはパノラマ VR 画像アセットに使用します。
* **[!UICONTROL ビデオ 360 メディア]** - 360 ビデオおよび 360 VR ビデオアセットに使用します。

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用前にテンプレートエディターで使用可能にする必要があります。テンプレートエディターでコンポートを使用可能にした後は、他の [!DNL Experience Manager] コンポーネントの場合と同様にページに追加することができます。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### コンポーネント：Dynamic Media {#dynamic-media-component}

Dynamic Media コンポーネントはスマートであり、追加しているアセットが画像であってもビデオであっても、様々なオプションを使用できます。このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されている Dynamic Media コンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。
>
>そのページの各 Dynamic Media コンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされていません。
>
>ただし、ページ内で同じタイプのアセットを使用するすべての Dynamic Media コンポーネントで同じビューアプリセットを使用できます。

Dynamic Media コンポーネントを追加したときに、「**[!UICONTROL ダイナミックメディア設定]**」が空であるかアセットを適切に追加できない場合は、次の点を確認してください。

* 画像が PTIFF（Pyramid TIFF）ファイルであること。Dynamic Media を有効にする前に読み込まれた画像には、PTIFF（Pyramid TIFF）ファイルはありません。

#### 画像を操作する場合 {#when-working-with-images}

ダイナミックメディアコンポーネントを使用すると、画像セット、スピンセット、混在メディアセットなどの動的イメージを追加できます。ズームイン、ズームアウト、スピンセット内での画像の回転（該当する場合）または別のタイプのセットからの画像の選択を行うことができます。

また、ビューアプリセット、画像プリセット、画像形式をコンポーネント内で直接設定することもできます。画像をレスポンシブにするために、ブレークポイントの設定かレスポンシブ画像プリセットの適用のいずれかを実行できます。

コンポーネント内の&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンを選択し、次に「**[!UICONTROL ダイナミックメディア設定]**」を選択すると、次の Dnamic Media 設定を編集することができます。

![Dynamic Media の画像プリセット設定](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>デフォルトでは、ダイナミックメディアの画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL ビューアプリセット]** - ドロップダウンリストから既存のビデオビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

  画像セット、スピンセットまたは混在メディアセットを表示している場合は、このオプションのみ使用できます。表示されるビューアプリセットもスマートであり、関連するビューアプリセットのみが表示されます。

* **[!UICONTROL ビューア修飾子]** - ビューア修飾子は、名前=値の組み合わせで &amp; を区切り文字とした形式です。ビューア修飾子を使用すると、ビューアリファレンスガイドに概略が記されているとおり、ビューアを変更することができます。`posterimage=img.jpg&caption=text.vtt,1` はビューア修飾子の一例で、ビデオのサムネールに異なる画像を設定し、ビデオにクローズドキャプションファイルを関連付けます。

* **[!UICONTROL 画像プリセット]** - ドロップダウンリストから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/dynamic-media/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 画像の修飾子]** - 追加の画像コマンドを指定して画像エフェクトを適用できます。これらのコマンドについては、画像プリセットと画像サービングコマンドリファレンスを参照してください。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL ブレークポイント]** - レスポンシブサイトでこのアセットを使用する場合は、画像のブレークポイントを追加する必要があります。画像のブレークポイントは、コンマ（,）で区切って指定する必要があります。このオプションを使用できるのは、画像プリセットで高さまたは幅が定義されていないときです。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

  コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の詳細設定を編集できます。

* **[!UICONTROL 高解像度デバイス向けに最適化]** - DPR（デバイスピクセル比）の最適化を許可する場合は、このチェックボックスをオン（デフォルト）にします。

  **[!UICONTROL 高解像度デバイス向けの最適化]**&#x200B;オプションは、次の条件が満たされる場合にのみ表示されます。
   * 「プリセットの種類」で、「**[!UICONTROL 画像プリセット]**」を選択し、**[!UICONTROL 画像プリセット]**&#x200B;ドロップダウンリストから「**[!UICONTROL RESS_IP]**」を選択します。

  ![画像プリセットのデバイスピクセル比設定](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

  [デバイスのピクセル比の最適化について](/help/assets/dynamic-media/imaging-faq.md#dpr)も参照してください。

  [!DNL Experience Manager] Dynamic Media スマートイメージング DPR 値は無視されます。

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

コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の Dynamic Media 設定を編集できます。

>[!NOTE]
>
>デフォルトでは、Dynamic Media のビデオコンポーネントはアダプティブです。ビデオコンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL ビューアプリセット]** - ドロップダウンリストから既存のビデオビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **[!UICONTROL ビューア修飾子]** - ビューア修飾子は、`name=value` のペアを `&` を区切り文字として並べた形式になります。ビューア修飾子を使用すると、Adobe ビューアリファレンスガイドの概要説明に従ってビューアを変更することができます。`posterimage=img.jpg&caption=text.vtt,1` はビューア修飾子の一例です。

  ビューア修飾子を使用すると、例えば次のことが可能です。

   * ビデオにキャプションファイルを関連付ける：[キャプション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html?lang=ja)
   * ビデオにナビゲーションファイルを関連付ける：[ナビゲーション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html?lang=ja)

     コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の詳細設定を編集できます。

* **[!UICONTROL タイトル]** - ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

#### スマート切り抜きを操作する場合 {#when-working-with-smart-crop}

Dynamic Media コンポーネントを使用して、スマート切り抜き画像アセットを Web ページに追加します。コンポーネントの編集時に、ページ上でビデオを再生するための事前定義済みのビデオビューアプリセットを使用するように選択できます。

詳しくは、[Experience Manager Assets Dynamic Media でスマート切り抜きを使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html?lang=ja)を参照してください。

[イメージプロファイル](/help/assets/dynamic-media/image-profiles.md)も参照してください。

![Dynamic Media スマートクロップの設定](assets/dm-settings-smart-crop.png)

コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の Dynamic Media 設定を編集できます。

>[!NOTE]
>
>デフォルトでは、ダイナミックメディアの画像コンポーネントはアダプティブです。画像コンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

* **[!UICONTROL 画像の修飾子]** - 追加の画像コマンドを指定して画像エフェクトを適用できます。これらのコマンドについては、画像プリセットと画像サービングコマンドリファレンスを参照してください。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

  コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の詳細設定を編集できます。

* **[!UICONTROL 縦横比の一致を有効にする]** - 元の画像の縦横比に最も適した縦横比のスマート切り抜きレンディションを Dynamic Media で選択する場合に、このオプションを選択します。

* **[!UICONTROL 高解像度デバイス向けに最適化]** - DPR（デバイスピクセル比）の最適化を許可する場合は、このチェックボックスをオン（デフォルト）にします。

  **[!UICONTROL 高解像度デバイス向けの最適化]**&#x200B;オプションは、次の条件が満たされる場合にのみ表示されます。

   * 「プリセットの種類」で、「**[!UICONTROL スマート切り抜き]**」オプションが選択されます。

  ![スマート切り抜きのデバイスピクセル比設定](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

  [デバイスのピクセル比の最適化について](/help/assets/dynamic-media/imaging-faq.md#dpr)も参照してください。

  [!DNL Experience Manager] Dynamic Media スマートイメージング DPR 値は無視されます。

* **[!UICONTROL タイトル]** - スマート切り抜き画像のタイトルを変更します。

* **[!UICONTROL 代替テキスト]** - グラフィックの表示をオフにしているユーザー向けのタイトルをスマート切り抜き画像に追加します。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL URL、次のウィンドウで開く]** - リンクを開くようにアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

  このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

### コンポーネント：インタラクティブメディア {#interactive-media-component}

インタラクティブメディアコンポーネントは、インタラクティビティ（ホットスポットまたは画像マップ）を含むアセット用です。インタラクティブ画像、インタラクティブビデオまたはカルーセルバナーがある場合は、**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントを使用します。

インタラクティブメディアコンポーネントはスマートであり、追加しているアセットが画像であってもビデオであっても、様々なオプションを使用できます。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されているインタラクティブメディアコンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。
>
>そのページの各インタラクティブメディアコンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされていません。
>
>一方、ページ内で、同じタイプのアセットを使用するすべてのインタラクティブメディアコンポーネントで同じビューアプリセットを使用することは可能です。

![chlimage_1-174](assets/chlimage_1-541.png)

コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の&#x200B;**[!UICONTROL 一般]**&#x200B;設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - ドロップダウンリストから既存のビデオビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。ビューアプリセットを使用するには、あらかじめ公開する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

* **[!UICONTROL タイトル]** - ビデオのタイトルを変更します。

* **[!UICONTROL 幅]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

* **[!UICONTROL 高さ]** - 画像を固定サイズで表示する場合は、値をピクセル単位で入力します。この値を空にすると、アダプティブなアセットになります。

  コンポーネントの「**[!UICONTROL 編集]**」を選択して、次の&#x200B;**[!UICONTROL 買い物かごに追加]**&#x200B;設定を編集できます。

* **[!UICONTROL 製品アセットを表示]** - デフォルトでは、この値が選択されています。製品アセットには、コマースモジュールで定義された製品の画像が表示されます。製品アセットを表示しない場合は、チェックマークをオフにします。

* **[!UICONTROL 製品価格を表示]** - デフォルトでは、この値が選択されています。製品価格には、コマースモジュールで定義されたアイテムの価格が表示されます。製品価格を表示しない場合は、チェックマークをオフにします。

* **[!UICONTROL 製品フォームを表示]** - デフォルトでは、この値は選択されていません。製品フォームには、サイズや色など製品のバリエーションが含まれます。製品のバリエーションを表示しない場合は、チェックマークをオフにします。

### コンポーネント：パノラマメディア {#panoramic-media-component}

パノラマメディアコンポーネントは、球状のパノラマ画像のアセット用です。このような画像は、部屋、不動産、場所、または風景の 360 度の視聴エクスペリエンスを提供します。画像が球状のパノラマとして認定されるには、以下の一方または両方の条件を満たしている必要があります。

* アスペクト比が 2:1 です。
* キーワード `equirectangular` または（`spherical` + `panorama`）または（`spherical` + `panoramic`）でタグ付けされている必要があります。[タグの使用](/help/sites-cloud/authoring/sites-console/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと「**[!UICONTROL パノラマメディア]**」WCM コンポーネントのパノラマアセットに適用されます。

>[!NOTE]
>
>Web ページに次のものが含まれている場合：
>
>* 同じページで使用されている&#x200B;**[!UICONTROL パノラマメディア]**&#x200B;コンポーネントの複数のインスタンス。
>* 各インスタンスが同じアセットタイプを使用している。
>
>そのページの各&#x200B;**[!UICONTROL パノラマメディア]**&#x200B;コンポーネントにそれぞれ異なるビューアプリセットを割り当てることは、サポートされていません。
>
>一方、ページ内で、同じタイプのアセットを使用するすべてのパノラマメディアコンポーネントで同じビューアプリセットを使用することは可能です。

![パノラマメディアビューアプリセット](assets/panoramic-media-viewer-preset.png)

コンポーネントの「**[!UICONTROL 設定]**」を選択して、次の設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - 「ビューアプリセット」ドロップダウンリストから既存のビューアを選択します。

探しているビューアプリセットが表示されない場合は、そのビューアプリセットが公開されていることを確認してください。ビューアプリセットは、公開してから使用してください。詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

### コンポーネント：ビデオ 360 メディア {#video-media-component}

Web ページ上でエクイレクタングラー形式のビデオをレンダリングするには、**[!UICONTROL ビデオ 360 メディア]**&#x200B;コンポーネントを使用します。それにより、部屋、物件、場所、風景、医療処置などの没入感のある視聴エクスペリエンスを実現できます。

フラットディスプレイでの再生時には、ユーザーは視野角を制御できます。また、モバイルデバイスでの再生では通常、デバイス組み込みのジャイロスコープ制御を使用します。

ビューアは、360 ビデオアセットの配信をネイティブでサポートしています。デフォルトでは、表示や再生のために追加の設定は必要ありません。360 ビデオは、.mp4、.mkv、.mov などの標準のビデオ拡張子を使用して配信します。最も一般的なコーデックは H.264 です。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

コンポーネントの「**[!UICONTROL 設定]**」を選択して、次の設定を編集できます。

* **[!UICONTROL ビューアプリセット]** - 「ビューアプリセット」ドロップダウンリストから既存のビューアを選択します。バーチャルリアリティグラスを使用するエンドユーザーには、Video360VR を使用します。基本的なビデオ再生コントロールとソーシャルメディア機能を含んでいます。基本的なビデオ再生コントロールを含む Video360_social を使用します。ビデオのレンダリングはステレオモードで行われます。視点の手動制御はオフになり、ジャイロスコープ制御がオンになります。ソーシャルメディア機能はありません。

探しているビューアプリセットが表示されない場合は、そのビューアプリセットが公開されていることを確認してください。ビューアプリセットは、公開してから使用してください。詳しくは、[ビューアプリセットの管理](/help/assets/dynamic-media/managing-viewer-presets.md)を参照してください。

### HTTP/2 を使用して Dynamic Media アセットを配信する {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](/help/assets/dynamic-media/http2faq.md)を参照してください。

>[!MORELIKETHIS]
>
>* [Experience Manager Dynamic Media でビデオプレーヤーを使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-player-feature-video-use.html?lang=ja)
>* [Experience Manager Dynamic Media でインタラクティブビデオを使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-interactive-video-feature-video-use.html?lang=ja)
>* [Experience Manager Dynamic Media でのアセットビューアについて](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/viewers/dynamic-media-viewer-feature-video-understand.html?lang=ja)
>* [Experience Manager Dynamic Media でカスタムビデオサムネールを使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-thumbnails-feature-video-use.html?lang=ja)
>* [Experience Manager Dynamic Media でのカラーマネジメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-color-management-technical-video-setup.html?lang=ja#dynamic-media)
>* [Experience Manager Dynamic Media で画像シャープ処理を使用する](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use.html?lang=ja)
