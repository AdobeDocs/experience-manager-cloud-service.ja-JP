---
title: AEM FormsEdge Delivery Servicesの概要 — 開発者向けチュートリアル
description: このチュートリアルでは、新しいAdobe Experience Manager Forms(AEM) プロジェクトを導入する方法について説明します。 10～20 分で、独自のフォームが作成されます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 30dfe0cfd7f845ba7a27699db22f8c4e61a0f7ed
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# はじめに - 開発者向けチュートリアル

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM FormsEdge Delivery Services(EDS) を使用すると、Google Docs やMicrosoft Office などの使い慣れたツールを使用してフォームを作成できます。

これらのフォームは、Microsoft Excel またはGoogleシートファイルに直接データを送信します。Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

AEM Formsには、アダプティブFormsブロックと呼ばれるブロックが用意されており、これを使用すると、キャプチャしたデータを取得して保存するためのフォームを簡単に作成することができます。 アダプティブFormsブロックが事前に装備された新しいAEMプロジェクトを作成したり、既存のAEMプロジェクトにアダプティブFormsブロックを追加したりできます。

このAEM Formsチュートリアルでは、新しいAdobe Experience Manager(AEM)Formsプロジェクトを使用して独自のカスタムフォームを作成、プレビュー、公開する手順を説明します。 また、アダプティブFormsブロックを既存のAEMプロジェクトに追加する方法についても説明します。

* **[アダプティブFormsブロックが事前に装備された新しいAEMプロジェクトを作成する](#create-a-new-eds-project-pre-equipped-with-adaptive-forms-block)**
* **[アダプティブFormsブロックを既存のAEMプロジェクトに追加する](#add-adaptive-forms-block-to-an-existing-eds-project)**



## 前提条件

* GitHub アカウントを持っており、Git の基本を理解している。
* GoogleまたはMicrosoft SharePointアカウントがある。
* HTML、CSS、JavaScript の基本について理解します。
* ローカル開発用の Node/npm がインストールされている。

**上がれ！** このチュートリアルでは、macOS、Chrome および Visual Studio Code を使用します。 この手順は他の設定にも適応できますが、スクリーンショットと特定の UI 要素は、選択したオペレーティングシステム、ブラウザー、コードエディターに応じて異なる場合があります。


## アダプティブFormsブロックが事前に装備された新しいAEMプロジェクトを作成する

AEM Forms Boilerplate テンプレートを使用すると、アダプティブFormsブロックが事前に設定されたAEMプロジェクトをすばやく開始できます。 AEMのベストプラクティスに従って、すぐにフォームを作成する方法です。

### AEM Formsテンプレートリポジトリテンプレートの概要

1. AEMプロジェクト用の GitHub リポジトリを作成します。 リポジトリを作成するには：
   1. に移動します。 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. 次をクリック： **このテンプレートを使用** オプションを選択し、 **新しいリポジトリを作成** オプション。 「新しいリポジトリを作成」画面が開きます。

      ![AEM Forms Boilerplate を使用して新しいリポジトリを作成](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. 新しいリポジトリを作成画面で、「 **所有者**、を指定します。 **リポジトリ名** . Adobeでは、リポジトリを **公開**. そのため、 **公開** オプションを選択し、をクリックします。 **リポジトリを作成**.

   ![リポジトリをパブリックに設定](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. AEM Code Sync GitHub アプリをリポジトリにインストールします。 をインストールするには：
   1. に移動します。 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. AEM Code Sync をインストール画面で、 **選択したリポジトリのみ** 」オプションを選択し、新しく作成したリポジトリを選択します。 「保存」をクリックします。

   ![リポジトリをパブリックに設定](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > IP フィルタリングで Github Enterprise を使用している場合は、許可リストに次の IP を追加できます。 3.227.118.73

   これですべて完了です。新しい Web サイトがで実行されています `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。

   例えば、ブランチ名が `main`、リポジトリは `wefinance`、および所有者は `wkndforms`を使用する場合、Web サイトは次の場所で起動および実行されます： [https://main—wefinance—wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### 独自のコンテンツソースをリンク

新しく作成された GitHub リポジトリがを指している場所は、 [Google Drive フォルダーに保存されたサンプルコンテンツ](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_). この読み取り専用コンテンツは、フォームの出発点として最適です。 必要に応じて、自由に独自のGoogle Drive にコピーし、カスタマイズしてください。

![Google Drive のサンプルコンテンツ](/help/edge/assets/folder-with-sample-content.png)

サンプルコンテンツを独自のコンテンツフォルダーにコピーし、GitHub リポジトリを独自のコンテンツフォルダーに指すようにするには、次の手順を実行します。

1. Google Drive またはMicrosoft SharePointで、AEMコンテンツ専用の新しいフォルダーを作成します。 このドキュメントでは、Microsoft SharePointで作成されたフォルダーを使用します。

1. フォルダーをAdobe Experience Managerユーザー (helix@adobe.com) と共有します。

   ![「アクセスを管理」オプションを使用して、AEM User とフォルダーを共有します — SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![「アクセスを管理」オプションを使用して、AEM User - Google Drive とフォルダーを共有します。](/help/edge/assets/share-google-drive-folder.png)


   フォルダーに対する編集権限がAdobe Experience Managerユーザーに付与されていることを確認します。

   ![フォルダーをAEM User と共有し、編集権限を付与します。SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![フォルダーをAEM User と共有し、編集権限を付与します (Google Drive)。](/help/edge/assets/add-aem-user-google-folder.png)

1. をコピーします。 [Google Drive フォルダーに保存されたサンプルコンテンツ](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) をフォルダーに追加します。 コピーする手順は、次のとおりです。

   1. ファイルを一緒にダウンロードするか、個々のファイルをダウンロードします。

      ![サンプルコンテンツをダウンロード](/help/edge/assets/download-sample-content.png)

      The `index`, `nav`、および `footer` ファイルはページの基本レイアウトを定義し、プロジェクト全体で変更されることはほとんどありません。 また、他のほとんどのコンテンツファイルとは異なる特定の構造を持っています。 これらのファイルを調べると、AEMプロジェクトでのコンテンツの編成方法を確認できます。


   1. これらのファイルをMicrosoft SharePointまたはGoogle Drive フォルダーにアップロードします。

      ![Google Drive のサンプルコンテンツ](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      必ず  `enquiry` シートを、サンプルコンテンツからGoogle Drive またはMicrosoft SharePointのフォルダーにコピーします。 サンプルフォームの構造が含まれています。

1. コンテンツフォルダーを設定したら、次に、以前にAEM Forms Boilerplate を使用して作成した GitHub 上のプロジェクトにリンクします。 接続するには：

   1. AEM Forms Boilerplate を使用して以前に作成した GitHub リポジトリに移動します。
   1. `fstab.yaml` を開いて編集します。
   1. 既存の参照を、AEMユーザー (helix@adobe.com) と共有したフォルダーのパスに置き換えます。

      ![Google Drive のサンプルコンテンツ](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Microsoft SharePointを使用する場合、フォルダーパスは次の形式を使用します。

      ```HTML
      https://<tenant>.sharepoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      例：

      ```HTML
      https://adobe.sharepoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Microsoft SharePoint内でのファイル管理について詳しくは、 [AdobeSharePoint の使用方法](https://www.aem.live/docs/setup-customer-sharepoint).



   1. 更新をコミット `fsatb.yaml` ファイルを編集した後、参照を更新すると、すべて正しく表示されます。 ビルドの問題が発生した場合は、 [GitHub ビルドの問題のトラブルシューティング](#troubleshooting-github-build-issues).



      ![更新された fsatab.yaml ファイルをコミット](/help/edge/assets/commit-updated-fstab-yaml.png)

      これにより、コンテンツフォルダーが Web サイトに接続されます。 参照を更新した後、最初に「404 Not Found」というエラーが発生する場合があります。 これは、コンテンツがまだプレビューされていないためです。 次の節では、コンテンツのオーサリングとプレビューを開始する方法について説明します。

      ![更新された fsatab.yaml ファイルをコミット](/help/edge/assets/aem-forms-project-folder-error.png)

### コンテンツのプレビューと公開

最後の手順を完了すると、新しいコンテンツソースは空にはなりませんが、プレビューまたはライブステージに昇格されるまで、Web サイトには表示されません。 現在、これにより 404 エラーが発生する場合があります。

非公開のコンテンツをプレビューするには：

1. という名前の Chrome 拡張機能をインストールします。 [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![インストールAEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   拡張機能を Chrome にインストールした後、必ずピン留めしておくと、見つけやすくなります。

   ![ピンAEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. SidekickChrome 拡張機能を設定するには、以前に共有したGoogle Drive またはMicrosoft SharePointフォルダーに移動し、ブラウザーツールバーの拡張機能アイコンを右クリックして、「 」を選択します。 `Add this project`.

   ![AEM Sidekick — プロジェクトを追加](/help/edge/assets/aem-sidekick-add-a-project.png)

   拡張機能がインストールされ、プロジェクトが追加され次第、Google Drive からコンテンツをプレビューして公開する準備が整います。

1. Microsoft SharePointまたはGoogle Drive フォルダー内のすべてのドキュメントを選択します。 Ctrl キー (Windows/Linux) または Cmd キー (Mac) を押しながらクリックすると、複数のドキュメントを選択できます。

   ![すべてのファイルを選択](/help/edge/assets/select-all-files.png)

1. Chrome 拡張機能バーに固定されているAEM Sidekickアイコンをクリックします。 画面にツールバーが表示されます。 コンテンツのプレビューまたは公開を選択できます。

   コピーした場合 `index`, `nav`, `footer` および `enquiry` ファイルはすべて、それぞれ別々のドキュメントで、それぞれのプレビューとパブリッシュのサイクルを持つので、すべてをプレビュー（およびパブリッシュ）してください。

   ファイルをプレビューすると、新しいブラウザータブにドキュメントが表示されます。 サンプルフォームをプレビューするには、次の URL に移動します。


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` は、GitHub リポジトリのブランチを参照します。
   * `<repository>` は GitHub リポジトリを示します。
   * `<owner>` は、GitHub リポジトリをホストする GitHub アカウントのユーザー名を指します。


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL。

   例えば、プロジェクトのリポジトリの名前が「wefinance」で、アカウント所有者「wkndforms」の下にあり、「main」ブランチを使用している場合、URL は次のようになります。



   [https://main—wefinance—wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### フォームの作成

サンプルコンテンツには、「問い合わせ」フォームのテンプレートとして機能する「問い合わせ」シートが含まれています。 シートの各行は、 [フォームフィールド](/help/edge/docs/forms/form-components.md#available-components)を定義し、列ヘッダーによって [フィールドプロパティ](/help/edge/docs/forms/form-components.md#available-components). このサンプルフォームを使用すると、フォームの作成を簡単に開始できます。

![問い合わせフォーム](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

まず、フィールドラベルを更新します。 「問い合わせ」シートを編集用に開き、送信ボタンのラベルをに変更します。 `Let's Chat`をクリックし、サイドキックを使用してパブリッシュします。

![問い合わせフォーム](/help/edge/assets/enquiry-form-preview-publish.png)

更新された問い合わせフォームをプレビューするには、次の URL に移動します。


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

送信ボタンのラベルがに更新されます。 `Let's Chat`.

![問い合わせフォーム](/help/edge/assets/updated-form.png)

新しいフォームの作成と公開について詳しくは、 [フォームの作成](/help/edge/docs/forms/create-forms.md) ガイド。

### スタイルと機能の開発を開始する


ローカルのAEM開発環境をすぐに使用して稼働させるには、次の手順を実行します。

1. AEM CLI のインストール： AEM CLI は開発タスクを簡素化します。 npm を使用してグローバルにインストールしましょう。

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. GitHub プロジェクトのクローンを作成します：次のコマンドを使用して、GitHub からプロジェクトリポジトリのクローンを作成します。 <owner> リポジトリの所有者と <repo> リポジトリ名：

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. ローカル環境を起動します。プロジェクトディレクトリに移動し、次の 1 つのコマンドでローカルAEMインスタンスを起動します。

   ```
   cd <repo>
   aem up
   ```

アダプティブFormsブロック `blocks/form` フォルダーは、フォームのスタイル設定やコードを行うための遊び場です。 任意の編集 `.css` または `.js` このディレクトリ内のファイルを参照し、変更がブラウザーに即座に反映されます。

作品を紹介する準備はできましたか？ Git を使用して、変更をコミットおよびプッシュします。 これにより、次の URL でアクセスできるプレビューおよび実稼動環境が更新されます（プレースホルダーをプロジェクトの詳細に置き換えます）。

プレビュー： `https://<branch>--<repo>--<owner>.hlx.page/`
実稼動： `https://<branch>--<repo>--<owner>.hlx.live/`
おめでとうございます。 ローカル開発環境を正常に設定し、変更をデプロイしました。



## アダプティブFormsブロックを既存のAEMプロジェクトに追加する


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

既存のAEMプロジェクトがある場合は、アダプティブFormsブロックを現在のプロジェクトに統合して、フォームの作成を開始できます。 統合する手順は次のとおりです。

1. アダプティブFormsブロックリポジトリ ( https://github.com/adobe-rnd/aem-boilerplate-forms ) をコンピューターに複製します。

1. ダウンロードしたフォルダー内で、 `blocks/form` フォルダー。 このフォルダーをコピーします。 次に、AEMプロジェクトのローカルに移動します `blocks` フォルダーにコピーしたフォームフォルダーをここに貼り付けます。

1. これらの変更を GitHub のAEMプロジェクトにコミットしてプッシュします。


これで作業は完了です。アダプティブFormsブロックがAEMプロジェクトに含まれます。 フォームの作成とAEMページへの追加を開始できます。


## GitHub ビルドの問題のトラブルシューティング

潜在的な問題に対処し、GitHub のビルドプロセスをスムーズに進めます。

* **モジュールパスの解決エラー：**
「モジュール「../../scripts/lib-franklin.js」へのパスを解決できません」というエラーが発生した場合は、 [EDS プロジェクト]/blocks/forms/form.jsファイルを参照してください。 lib-franklin.js ファイルを aem.js ファイルに置き換えて、import 文を更新します。

* **リントエラーを処理：**
リントエラーが発生した場合は、それらを回避できます。 を開きます。 [EDS プロジェクト]/package.jsonファイルを編集し、&quot;lint&quot;スクリプトを&quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot;から&quot;lint&quot;: &quot;echo &#39;今すぐのリントをスキップ&#39;&quot;に変更します。 ファイルを保存し、変更を GitHub プロジェクトにコミットします。


## 関連トピック

* [Google Sheet またはMicrosoft Excel を使用したフォームの作成](/help/edge/docs/forms/create-forms.md)
* [Microsoft Excel またはGoogleシートに直接フォームを送信する](/help/edge/docs/forms/submit-forms.md)
* [フォームの外観を変更する](/help/edge/docs/forms/style-theme-forms.md)






