---
title: サンプル React アプリのコンテンツのカスタマイズ
description: サンプルの React アプリを使用して、AEM as a Cloud Serviceのヘッドレス機能セットを使用してコンテンツをカスタマイズする方法を学びます。
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---


# サンプル React アプリのコンテンツのカスタマイズ {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="サンプル React アプリのコンテンツのカスタマイズ"
>abstract="AEMのヘッドレス体験版には、カスタマイズ可能なサンプル React アプリが統合されています。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="コンテンツフラグメントエディターを起動します。"
>abstract="AEMのヘッドレス体験版には、サンプルの React アプリが統合されているので、開発時間をかけずに誰でも個別にコンテンツを簡単に管理できます。<br><br>以下をクリックして、新しいタブでこのモジュールを起動し、このガイドに従ってください。"
>additional-url="https://video.tv.adobe.com/v/328618" text="アプリの導入ビデオのカスタマイズ"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="このモジュールでは、サンプル React アプリをカスタマイズする方法を学びました。<br><br>市場投入までの時間：加速！<br>開発サイクル：縮小！<br><br>AEMのヘッドレス機能を利用した Web サイトやアプリで、ヘッドレスコンテンツを容易に管理できる方法を理解できます。"
>abstract=""

## アプリのプレビュー {#preview}

クリック **コンテンツフラグメントエディターを起動します。** 上のボタンをクリックすると、コンテンツフラグメントエディターが新しいタブに開きます。

![コンテンツフラグメントエディター](assets/customize-app/content-fragment-editor.png)

AEMヘッドレストライアルで提供されるサンプルアプリは、GraphQL経由で配信されたコンテンツフラグメントを利用しています。 サンプルをプレビューして、コンテンツフラグメントエディターを使用してコンテンツを把握します。

1. をタップまたはクリックします。 **プレビュー** ボタンをクリックします。

1. 新しいタブでデモアプリが開きます。 このアプリは架空の WKND 屋外ライフスタイルブランド用です。 クリックしてサンプルコンテンツに移動します。

   ![デモアプリのプレビュー](assets/customize-app/preview-demo-app.png)

1. 続行するには、コンテンツフラグメントエディターの「ブラウザー」タブに戻ります。

## アプリのヘッダーの編集 {#edit-app}

コンテンツフラグメントエディターは、アプリの基本レイアウトをページのコンテンツフラグメントとして表示します。 この **パネル** は、アプリの様々なページを表し、それぞれが独自のコンテンツフラグメントです。 これらのフラグメントを変更すると、アプリのコンテンツを変更できます。

1. タップまたはクリック **Mtn Biker in Canyon** 内 **パネル** 」セクションに入力します。

   ![キャニオンフラグメントで Mtn Biker をタップします](assets/customize-app/mtn-biker-in-canyon.png)

1. エディターがマウンテンバイカー用のアプリのヘッダーパネルを開きます。 各パネルは、様々な画像やエクスペリエンスを構成するテキストを表すレイヤーで構成されています。

   ![パネル](assets/customize-app/panels.png)

1. テキストレイヤーを選択 **Mtn Biker in Canyon Text Layer**. これにより、エディタで画層の詳細が開きます。 レイヤーは、アプリのこのパネルに表示されるテキストを制御する複数のコンテンツフラグメントで構成されます。

   ![キャニオンのタイトルで Mtn Biker を選択](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. を選択します。 **Mtn Biker in Canyon Title** テキスト項目。 コンテンツフラグメントエディターが開きます。

   ![「キャニオンのタイトル」テキスト項目で「Mtn Biker」を選択します。](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 次のテキストを変更： `Your next great adventure is calling` から `Choose your own adventure`. 変更はエディターによって自動的に保存されます。

1. タップまたはクリック **プレビュー** をクリックして、変更内容を確認します。 新しいタブにデモアプリのプレビューが開きます。

   ![デモアプリのプレビュー](assets/customize-app/preview-demo-app-text.png)

AEMヘッドレス CMS に統合した場合に、React アプリ内のコンテンツを更新するのは、その方が簡単です。

## アプリ内での画像のスワップ {#change-image}

アプリのヘッドラインを変更したので、画像を変更してみてください。

1. コンテンツフラグメントエディターの「ブラウザー」タブに戻ります。

1. コンテンツフラグメントエディター内の正しい場所に戻る必要があります。 エディターの左上にあるパンくずリストには、コンテンツ階層内の位置が表示されます。 タップまたはクリック **Mtn Biker in Canyon** 」をクリックして、そのページに戻ります。

   ![パンくずリスト](assets/customize-app/breadcrumbs.png)

1. を選択します。 **Mtn Biking - Biker** 画像レイヤー。 コンテンツフラグメントエディターが開きます。

   ![画像フラグメントを編集](assets/customize-app/mtn-biking-biker.png)

1. をタップまたはクリックします。 **X** バイカー画像を削除します。 画像はこのコンテンツフラグメントモデルに必要なデータなので、画像が消え、エディターにエラーが表示されます。

   ![フラグメントから削除された画像](assets/customize-app/mtn-biking-biker-no-image.png)

1. タップまたはクリック **アセットを追加**.

1. この **アセットを選択** ダイアログが開き、パスが表示されます。 **sample-wknd-app** > **en** > **image-files** が自動的に選択されます。

1. 画像を選択 `biker-yellow.png` その後、タップまたはクリックします **選択**.

   ![アセットを選択](assets/customize-app/select-asset.png)

1. バイカーの画像は、選択された画像に置き換えられる。 エディターが自動的に変更を保存します。

   ![バイカー画像のフラグメントを編集しました](assets/customize-app/mtn-biking-biker-edited.png)

1. タップまたはクリック **プレビュー** をクリックして、変更内容を確認します。 新しいタブにデモアプリのプレビューが開きます。 ブラウザーの「更新」をクリックすると、新しいバイカー画像に黄色のショートが表示されます。

AEMヘッドレス CMS を使用して、アプリ内の画像やアセットを簡単に更新できます。

## 新しいコンテンツフラグメントへの参照をアプリに追加する {#create-moment}

バイカーの画像を更新したので、新しいコンテンツフラグメントを作成して参照することで、アプリに新しいコンテンツを追加する方法を順を追って説明します。 アプリの 2 番目のパネルに、「ショッパブルモーメント」コンテンツフラグメントで管理される製品コールアウトを追加します。

![ショッパブルモーメントの例](assets/customize-app/example-shoppable-moment.png)

1. コンテンツフラグメントエディターの「ブラウザー」タブに戻ります。

1. コンテンツフラグメントエディター内の正しい場所に戻る必要があります。 エディターの左上にあるパンくずリストには、コンテンツ階層内の位置が表示されます。 タップまたはクリック **WKND ホーム** 」をクリックして、そのページに戻ります。

   ![レイアウト画面に戻ります。](assets/customize-app/breadcrumbs-2.png)

1. を選択します。 **Mtn Biker on WKND Yellow** パネル。

   ![ショッパブルモーメントの作成](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. を選択します。 **Mtn Biking - Shoppable** レイヤー。

   ![ショッパブルモーメントレイヤーを選択](assets/customize-app/mtn-biking-shoppable.png)

1. このパネルで新しいコールアウトを作成するには、新しいショッパブルモーメントコンテンツフラグメントを作成する必要があります。 をタップまたはクリックします。 **+新しいフラグメントを作成** 」ボタンをクリックします。

   ![ショッパブルモーメントを追加](assets/customize-app/create-new-fragment.png)

1. 最初に、新しいコンテンツフラグメントのベースとなるモデルを選択する必要があります。 を選択します。 **ショッパブルモーメント項目** モデル **コンテンツフラグメントモデル** 」ドロップダウンリストから選択できます。

1. 「コンテンツフラグメント」に名前を付けます。 例えば、 `Shorts` に **名前** フィールドに入力します。

   ![ショッパブルモーメントの名前を付ける](assets/customize-app/new-content-fragment.png)

1. タップまたはクリック **作成して開く**.

1. 新しいコンテンツフラグメント用のエディターが開きます。

1. ショッパブルモーメントに **テキスト** 次のようなフィールド： `Yellow shorts`.

1. 次の値を設定： **X** および **Y**. このコールアウトは、パネル上にオーバーレイする必要があります。 フラグメントに対する変更は、エディターによって自動的に保存されます
   * **X**: `-18`
   * **Y**: `-28`

   ![ショッパブルモーメントを編集](assets/customize-app/edit-shoppable-moment.png)

1. タップまたはクリック **プレビュー** をクリックして、変更内容を確認します。 新しいタブにデモアプリのプレビューが開きます。 ブラウザの [ 更新 ] をクリックして、位置をテストし、必要に応じてエディタで調整します。

これで、新しいコンテンツを作成し、アプリ内でコンテンツフラグメントとして参照する方法を、開発サイクルを経ずに完了できる方法を理解できます。
