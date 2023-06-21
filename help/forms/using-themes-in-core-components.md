---
title: テーマの作成および使用
description: テーマとコアコンポーネントを使用して、アダプティブフォームのスタイルを設定し、視覚的に表現できます。任意の数のアダプティブフォームで、テーマを共有できます。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 98%

---

# アダプティブフォーム（コアコンポーネント）のテーマ {#themes-for-af-using-core-components}

コアコンポーネントを使用してテーマを作成および適用することで、アダプティブフォームのスタイルを設定できます。テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマは、アダプティブフォームを参照せずに、独立して管理されます。

コアコンポーネントを使用して[アダプティブフォームを作成](/help/forms/creating-adaptive-form.md)すると、標準テーマが「**スタイル**」タブの下に表示されます。デフォルトでは、**キャンバス**&#x200B;テーマのみ使用できます。

>[!NOTE]
>
>アダプティブフォームのテーマを[アダプティブフォームのテンプレートと混同しないでください。](/help/forms/template-editor.md)アダプティブフォームのテーマには、アダプティブフォームのスタイル設定情報のみが含まれます。アダプティブフォームテンプレートは、フォーム構造と初期コンテンツを定義し、新しい [アダプティブフォーム。](/help/forms/creating-adaptive-form.md)

## コアコンポーネントを使用したアダプティブフォームでのキャンバステーマの使用 {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用するには、次の手順を実行します。

1. AEM Forms オーサーインスタンスにログインします。

1. **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;の順にタップします。

1. **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。アダプティブフォームを作成するためのウィザードが開きます。

1. 「**ソース**」タブでコアコンポーネントテンプレートを選択します。

   >[!NOTE]
   >
   > コアコンポーネントを含むアダプティブフォームを作成すると、「スタイル」タブの下にキャンバステーマが表示されます。これは、すぐに使用できる唯一の標準テーマです。ただし、テーマを好みに合わせて変更し、フロントエンドパイプラインを設定することで、あとで使用するために保存できます。

1. 「**スタイル**」タブでキャンバステーマを選択します。
1. 「**作成**」をクリックします。

アダプティブフォームのテーマは、アダプティブフォームの作成時にスタイルを定義する、アダプティブフォームのテンプレートの一部として使用されます。

## テーマのカスタマイズ {#customizing-theme}

テーマをカスタマイズするには、次の手順を実行します。

* [Cloud Manager でパイプラインを設定します。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* ユーザーを[投稿者の役割](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html)として設定します。
* [Git リポジトリと Cloud Service Git リポジトリの基礎知識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git)が必要です。

キャンバステーマをカスタマイズするには、次の手順を実行します。

1. [キャンバステーマをクローン](#1-download-canvas-theme-download-canvas-theme)
1. [テーマの構造を理解する](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [package.json と package_lock.json の名前を変更する](#changename-packagelock-packagelockjson)
1. [テーマフォルダーで ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [ローカルの プロキシサーバーを開始します。](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [テーマのカスタマイズ](#customize-the-theme-customizing-theme)
1. [変更をコミットする](#6-committing-the-changes-committing-the-changes)
1. [パイプラインをデプロイする](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. キャンバステーマをクローンする {#download-canvas-theme}

コマンドプロンプトを開き、次のコマンドを実行してキャンバステーマをクローンします。

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> フォーム作成ウィザードの「スタイル」タブには、package.json ファイルと同じテーマ名が表示されます。

### 2. テーマの構造を理解する {#structure-of-canvas-theme}

アダプティブフォームのテーマは、フォームのスタイルを定義し、アダプティブフォームのテーマの構造に準拠する CSS、JavaScript、および静的リソースを含むパッケージです。アダプティブフォームのテーマは、フロントエンドプロジェクトに典型的な次の構造を持ちます。

* `src/components`：AEM コアコンポーネント固有の JavaScript ファイルおよび CSS ファイル
* `src/resources`：アイコン、ロゴ、フォントなどの静的ファイル
* `src/site`：AEM Sites ページ全体に適用される JavaScript ファイルおよび CSS ファイル
* `src/theme.ts`：JavaScript および CSS テーマの主なエントリポイント
* `src\theme.scss`：テーマ全体に適用される JavaScript および CSS ファイル

`src/components` フォルダーには、すべての AEM コアコンポーネント専用の JavaScript および CSS ファイル（ボタン、チェックボックス、コンテナ、フッターなど）が含まれます。 ボタンまたはチェックボックスのスタイルを設定するには、AEM コンポーネントに固有の CSS ファイルを編集します。

![テーマの編集](/help/forms/assets/theme_structure.png)

テーマをカスタマイズするには、ローカルプロキシサーバーを起動して、実際の AEM コンテンツに基づいてテーマのカスタマイズをリアルタイムで確認できます。

### 3. キャンバステーマの package.json と package_lock.json の名前を変更する {#changename-packagelock-packagelockjson}

`package.json` および `package_lock.json` ファイル内のキャンバステーマの名前とバージョンを更新します。

>[!NOTE]
>
> 名前に `@aemforms` タグを使用しないでください。ユーザーが指定した名前の単純なテキストにする必要があります。

![キャンバステーマの画像](/help/forms/assets/changename_canvastheme.png)

### 4. テーマフォルダーに .env ファイルを作成する {#creating-env-file-theme-folder}

テーマ フォルダーに `.env` ファイルを作成し、次のパラメーターを追加します。

* **AEM の URL**
AEM_URL=https://[author-instance]

* **AEM サイト名**
AEM_ADAPTIVE_FORM=Form_name

* **AEM のプロキシポート**
AEM_PROXY_PORT=7000


![キャンバステーマの構造](/help/forms/assets/env-file-canvas-theme.png)

### 5. ローカルプロキシサーバーを起動する {#starting-a-local-proxy-server}

1. コマンドラインから、ローカルマシン上のテーマのルートに移動します。
1. `npm install` を実行すると、npm は依存関係を取得し、プロジェクトをインストールします。
1. `npm run live` を実行すると、プロキシサーバーが起動します。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. 「**ローカルでログイン (管理者タスクのみ)**」をタップまたはクリックし、AEM 管理者から提供されたプロキシユーザーの資格情報を使用してログインします。

   ![ローカルでログイン](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * ローカルユーザーを作成してローカルでログインします。 テーマデザイナーの投稿者の役割を指定します。
   > * キャンバステーマの `.env` ファイルで AEM URL を `http://localhost:[port]/` として指定すると、ブラウザーに直接リダイレクトされます。

1. ログインしたら、AEM 管理者が指定したサンプルコンテンツのパスを指すように、ブラウザーで URL を変更します。

   * 例えば、指定されたパスが `/content/formname.html?wcmmode=disabled` であった場合URL を `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled` に変更します

   ![プロキシ化されたサンプルコンテンツ](/help/forms/assets/sample_af.png)

アダプティブフォームに移動して、アダプティブフォームに適用されたキャンバステーマを確認します。

### 6. テーマをカスタマイズする {#customize-theme}

1. エディターで、`<your-theme-sources>/src/site/_variables.scss` ファイルを開きます。

   >[!NOTE]
   >
   > サイト内のすべてのアダプティブフォームコンポーネントのスタイルを直接設定するには、`site/_variables.scss` ファイルを編集します。

1. `font colour` から `red` の変数を編集します。 

   ![テーマを編集](/help/forms/assets/edit_theme.png)

   **様々な AEM コンポーネントのスタイル設定**

   アダプティブフォームの様々なコンポーネントのスタイルを設定するには、エディターで CSS ファイルを変更します。 キャンバステーマフォルダー内にはアダプティブフォームのコアコンポーネントごとに異なる CSS フォルダーがあります。

   ![コアコンポーネント](/help/forms/assets/theme-component.png)

   テーマエディターで特定のコンポーネントのスタイルを指定するには、テーマフォルダー内の CSS を編集できます。例えば、テキストボックスフィールドの境界線の色を変更する場合は、CSS ファイルをエディターで開いて、境界線の色を変更します。

   ![テキストボックス CSS の編集](/help/forms/assets/edit_color_textbox.png)

1. ファイルを保存すると、プロキシサーバーが `[Browsersync] File event [change]` 行を介して変更を認識します。

   ![プロキシブラウザー同期](/help/forms/assets/browser_sync.png)

1. ローカルのプロキシサーバーのブラウザーに切り替えると、変更が直ちに表示されます。

   ![AF テーマの変更](/help/forms/assets/edit_theme_af.png)

テーマデザイナーは、ローカルプロキシサーバーで変更をプレビューし、様々な AEM コンポーネントの要件に応じてテーマをカスタマイズします。

変更を AEM Git リポジトリにコミットする前に、[Git リポジトリ情報](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)にアクセスする必要があります。

### 7. 変更をコミットする {#committing-the-changes}

テーマに変更を加え、ローカルプロキシサーバーでテストした後、その変更を AEM Forms Cloud Service の Git リポジトリにコミットします。 これにより、カスタマイズされたテーマが Forms Cloud Service 環境で使用でき、アダプティブフォームの作成者が使用できるようになります。

変更を AEM Forms Cloud Service の Git リポジトリにコミットする前に、ローカルマシン上にリポジトリのクローンを作成する必要があります。 リポジトリのクローンを作成するには、次を手順を実行します。

1. 新しいテーマリポジトリを作成するには、「**[!UICONTROL リポジトリ]**」オプションをクリックします。

   ![新しいテーマリポジトリの作成](/help/forms/assets/createrepo_canvastheme.png)

1. **[!UICONTROL リポジトリを追加]**&#x200B;をクリックし、**リポジトリを追加**&#x200B;ダイアログボックスで&#x200B;**リポジトリ名**&#x200B;を指定します。「**[!UICONTROL 保存]**」をクリックします。

   ![キャンバステーマリポジトリの追加](/help/forms/assets/addcanvasthemerepo.png)

1. **[!UICONTROL リポジトリ URL をコピー]**&#x200B;をクリックし、作成したリポジトリの URL をコピーします。

   ![キャンバステーマの URL](/help/forms/assets/copyurl_canvastheme.png)

1. コマンドプロンプトを開き、上記で作成したクラウドリポジトリをクローンします。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 編集中のテーマリポジトリのファイルをクラウドリポジトリに移動するには、次のようなコマンドを使用します。
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例えば、次のコマンドを使用します。 `cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. クラウドリポジトリのディレクトリで、先ほど移動したテーマファイルを次のコマンドでコミットします。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. カスタマイズ内容は Git リポジトリにプッシュされます。

   ![コミット済みの変更](/help/forms/assets/cmd_git_push.png)

これで、カスタマイズ内容が Git リポジトリに安全に保存されました。


### 8. フロントエンドパイプラインを実行する {#deploy-pipeline}

1. フロントエンドパイプラインを作成して、カスタマイズしたテーマをデプロイします。詳しくは、[カスタマイズしたテーマをデプロイするためのフロントラインパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)を参照してください。
1. 作成したフロントエンドパイプラインを実行し、アダプティブフォームの作成ウィザードの「**[!UICONTROL スタイル]**」タブで、カスタマイズしたテーマフォルダーをデプロイします。

>[!NOTE]
>
>今後、キャンバステーマフォルダーで変更を加える場合は、上記のパイプラインを再実行する必要があります。そのため、パイプラインの名前を覚えておく必要があります。

## テーマのカスタマイズ例 {#example-to-customize-a-theme}

1. AEM Forms オーサーインスタンスにログインします。
1. コアコンポーネントを使用して作成されたアダプティブフォームを開きます。
1. コマンドプロンプトでローカルプロキシサーバーを起動し、「**ローカルでログイン (管理者タスクのみ)**」をクリックします。
1. ログインすると、ブラウザーにリダイレクトされ、適用されたテーマが表示されます。
1. [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)をダウンロードし、ダウンロードした zip フォルダーを抽出します。
1. 抽出した zip フォルダーを任意のエディターで開きます。
1. テーマフォルダーで `.env` ファイルを作成し、**AEM URL**、**AEM_ADAPTIVE_FORM** および **AEM_PROXY_PORT** パラメーターを追加します。
1. キャンバステーマフォルダーのテキストボックスの CSS ファイルを開き、境界線のカラーを `red` に変更し、保存します。
1. ブラウザーを再度開くと、変更が直ちにアダプティブフォームに反映されます。
1. クローンしたリポジトリ内のキャンバステーマフォルダーを移動します。
1. 変更をコミットし、フロントエンドパイプラインを実行します。

パイプラインを実行すると、「スタイル」タブでテーマを使用できるようになります。

## ベストプラクティス {#best-practices}

* **別のテーマに属するアセットの回避**

  テーマを編集する際、アセット（画像など）を他のテーマから参照して追加することができます。例えば、ページの背景を編集しているとします。例えば、**[!UICONTROL ページ]** ![edit-button](assets/edit-button.png)／**[!UICONTROL 背景]**／**[!UICONTROL 追加]**／**[!UICONTROL 画像]**&#x200B;を選択すると、他のテーマの画像を参照して追加することが可能なダイアログが表示されます。

  アセットを別のテーマから追加し、そのテーマが移動または削除されると、現在のテーマに問題が生じる場合があります。他のテーマからアセットを参照して追加しないようにすることをお勧めします。

* **コンテナパネルのレイアウト幅の変更**

  コンテナパネルのレイアウト幅の変更はお勧めしません。コンテナパネルの幅を指定すると、幅が静的になり、様々なディスプレイに合わせて調整されません。

* **ヘッダーとフッターを操作する際のフォームエディターまたはテーマエディターの使用**

  テーマエディターは、フォントスタイル、背景、透明度などのスタイル設定オプションを使用してヘッダーとフッターのスタイルを設定する場合に使用します。
ヘッダーにロゴイメージや企業名などの情報を表示し、フッターに著作権情報を表示する場合は、フォームエディターのオプションを使用します。
