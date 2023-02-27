---
title: テーマの作成および使用
description: テーマを使用して、コアコンポーネントを使用してアダプティブフォームのスタイルを設定し、視覚的な ID を付けることができます。 任意の数のアダプティブフォームで、テーマを共有できます。
source-git-commit: 0205ffeabcb422ad70fd9439a1af246f438c52d5
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 20%

---


# アダプティブForms（コアコンポーネント）のテーマ {#themes-for-af-using-core-components}

テーマを作成し適用して、コアコンポーネントを使用してアダプティブフォームのスタイルを設定することができます。 テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマは、アダプティブフォームを参照せずに、独立して管理されます。

次の場合： [アダプティブフォームの作成](/help/forms/creating-adaptive-form.md) コアコンポーネントを使用すると、標準テーマが **スタイル** タブをクリックします。 デフォルトでは、 **キャンバス** テーマを使用できます。

>[!NOTE]
>
>アダプティブフォームのテーマを [アダプティブフォームテンプレート](/help/forms/template-editor.md) アダプティブフォームテーマには、アダプティブフォームのスタイル設定情報のみが含まれます。 アダプティブフォームテンプレートは、新しい [アダプティブフォーム。](/help/forms/creating-adaptive-form.md)

## コアコンポーネントを使用したアダプティブFormsでのキャンバステーマの使用 {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用する手順は次のとおりです。

1. AEM Forms オーサーインスタンスにログインします。

1. タップ **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.

1. クリック **作成** > **アダプティブForms**. アダプティブフォームを作成するためのウィザードが開きます。

1. でコアコンポーネントテンプレートを選択します。 **ソース** タブをクリックします。

   >[!NOTE]
   >
   > コアコンポーネントを含むアダプティブフォームを作成すると、「スタイル」タブの下にキャンバステーマが表示されます。 これは、すぐに使用できる唯一の標準テーマです。 ただし、テーマを好みに合わせて変更し、フロントエンドパイプラインを設定して保存し、将来の使用のために保存することができます。

1. でキャンバステーマを選択します。 **スタイル** タブをクリックします。
1. 「**作成**」をクリックします。

アダプティブフォームテーマは、アダプティブフォームの作成時にスタイル設定を定義するアダプティブフォームテンプレートの一部として使用されます。

## テーマのカスタマイズ {#customizing-theme}

テーマをカスタマイズするには

* [Cloud Manager でのパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* を使用してユーザーを設定する [投稿者の役割](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* 以下の場合、 [Git の基本知識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) およびCloud ServiceGit リポジトリー。

キャンバステーマをカスタマイズするには：
1. [キャンバステーマのクローン](#1-download-canvas-theme-download-canvas-theme)
1. [テーマの構造を理解する](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [package.json と package_lock.json の名前を変更します。](#changename-packagelock-packagelockjson)
1. [を作成します。 ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [ローカルの プロキシサーバーを開始します。](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [テーマのカスタマイズ](#customize-the-theme-customizing-theme)
1. [変更をコミット](#6-committing-the-changes-committing-the-changes)
1. [パイプラインのデプロイ](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1.キャンバステーマを複製する {#download-canvas-theme}

コマンドプロンプトを開き、次のコマンドを実行してキャンバステーマのクローンを作成します。

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> フォーム作成ウィザードの「スタイル」タブには、package.json ファイルと同じテーマ名が表示されます。

### 2.テーマの構造を理解する {#structure-of-canvas-theme}

アダプティブフォームテーマは、フォームのスタイルを定義し、アダプティブフォームテーマの構造に準拠する CSS、JavaScript および静的リソースを含むパッケージです。 アダプティブフォームテーマは、フロントエンドプロジェクトに典型的な次の構造を持ちます。

* `src/components`:AEMコアコンポーネント固有の JavaScript および CSS ファイル
* `src/resources`：アイコン、ロゴ、フォントなどの静的ファイル
* `src/site`:AEM Sitesページ全体に適用される JavaScript および CSS ファイル
* `src/theme.ts`:JavaScript および CSS テーマの主なエントリポイント
* `src\theme.scss`:テーマ全体に適用される JavaScript および CSS ファイル

この `src/components` フォルダーには、すべてのAEMコアコンポーネント専用の JavaScript および CSS ファイル（ボタン、チェックボックス、コンテナ、フッターなど）が含まれます。 ボタンまたはチェックボックスのスタイルを設定するには、AEMコンポーネントに固有の CSS ファイルを編集します。

![テーマの編集](/help/forms/assets/theme_structure.png)

テーマをカスタマイズするには、ローカルプロキシサーバーを起動して、実際のAEMコンテンツに基づいたテーマのカスタマイズをリアルタイムで確認します。

### 4.キャンバステーマの package.json と package_lock.json で名前を変更する {#changename-packagelock-packagelockjson}

でキャンバステーマの名前とバージョンを更新する `package.json` および `package_lock.json` ファイル。

>[!NOTE]
>
> 名前に次の文字列を含めることはできません `@aemforms` タグを使用します。 ユーザーが指定した名前の単純なテキストにする必要があります。

![キャンバステーマ画像](/help/forms/assets/changename_canvastheme.png)

### 3.テーマフォルダーに.env ファイルを作成する {#creating-env-file-theme-folder}

の作成 `.env` theme フォルダーにファイルを作成し、次のパラメーターを追加します。

* **AEM url**
AEM_URL=https://[author-instance]

* **AEM site name**
AEM_ADAPTIVE_FORM=Form_name

* **AEMプロキシポート**
AEM_PROXY_PORT=7000


![キャンバステーマの構造](/help/forms/assets/env-file-canvas-theme.png)

### 4.ローカルプロキシサーバーを起動する {#starting-a-local-proxy-server}

1. コマンドラインから、ローカルマシン上のテーマのルートに移動します。
1. `npm install` を実行すると、npm は依存関係を取得し、プロジェクトをインストールします。
1. `npm run live` を実行すると、プロキシサーバーが起動します。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. タップまたはクリック **ローカルでログイン（管理者タスクのみ）** をクリックし、AEM管理者から提供されたプロキシユーザーの資格情報を使用してログインします。

   ![ローカルでログイン](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * ローカルユーザーを作成してローカルでログインします。 テーマデザイナーの寄稿者の役割を指定します。
   > * AEM URL を `http://localhost:[port]/` 内 `.env` キャンバステーマのファイルが、ブラウザーに直接リダイレクトされます。


1. ログインしたら、AEM 管理者が指定したサンプルコンテンツのパスを指すように、ブラウザーで URL を変更します。

   * 例えば、指定されたパスが `/content/formname.html?wcmmode=disabled` であった場合に設定する場合、URL をに変更します。 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![プロキシ化されたサンプルコンテンツ](/help/forms/assets/sample_af.png)

アダプティブフォームに移動して、アダプティブフォームに適用されたキャンバステーマを確認します。

### 5.テーマをカスタマイズする {#customize-theme}

1. エディターで、ファイルを開きます。 `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > サイト内のすべてのアダプティブフォームコンポーネントのスタイルを直接設定するには、 `site/_variables.scss` ファイル。

1. の変数を編集します。 `font colour` から `red`.

   ![テーマを編集](/help/forms/assets/edit_theme.png)

   **様々なAEMコンポーネントのスタイル設定**

   アダプティブフォームの様々なコンポーネントのスタイルを設定するには、エディターで CSS ファイルを変更します。 Canvas Theme フォルダー内のアダプティブフォームのコアコンポーネントごとに異なる CSS フォルダーがあります。

   ![コアコンポーネント](/help/forms/assets/theme-component.png)

   テーマエディターで特定のコンポーネントのスタイルを指定するには、テーマフォルダー内の CSS を編集します。 例えば、テキストボックスフィールドの境界線のカラーを変更する場合は、CSS ファイルをエディターで開き、境界線のカラーを変更します。

   ![テキストボックス CSS を編集](/help/forms/assets/edit_color_textbox.png)

1. ファイルを保存すると、プロキシサーバーは行を介して変更を認識します。 `[Browsersync] File event [change]`.

   ![プロキシブラウザー同期](/help/forms/assets/browser_sync.png)

1. ローカルプロキシサーバーのブラウザーに切り替えると、変更が直ちに表示されます。

   ![AF テーマを変更する](/help/forms/assets/edit_theme_af.png)

テーマデザイナーは、ローカルプロキシサーバーでの変更をプレビューし、様々なAEMコンポーネントの要件に応じてテーマをカスタマイズします。

変更をAEM Git リポジトリにコミットする前に、 [Git リポジトリ情報](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6.変更をコミットする {#committing-the-changes}

テーマに変更を加え、ローカルプロキシCloud Serviceでテストした後、その変更をAEM Formsサーバーの Git リポジトリにコミットします。 これにより、カスタマイズされたテーマがFormsCloud Service環境で使用でき、アダプティブFormsの作成者が使用できるようになります。

変更をAEM FormsCloud Serviceの Git リポジトリにコミットする前に、ローカルマシン上にリポジトリのクローンを作成する必要があります。 リポジトリを複製するには：

1. 新しいテーマリポジトリを作成するには、 **[!UICONTROL リポジトリ]** オプション。

   ![新しいテーマリポジトリを作成](/help/forms/assets/createrepo_canvastheme.png)

1. クリック **[!UICONTROL リポジトリを追加]** をクリックし、 **リポジトリ名** 内 **リポジトリを追加** ダイアログボックス 「**[!UICONTROL 保存]**」をクリックします。

   ![キャンバステーマリポジトリを追加](/help/forms/assets/addcanvasthemerepo.png)

1. クリック **[!UICONTROL リポジトリ URL をコピー]** 作成したリポジトリの URL をコピーします。

   ![キャンバステーマの URL](/help/forms/assets/copyurl_canvastheme.png)

1. コマンドプロンプトを開き、上記で作成したクラウドリポジトリのクローンを作成します。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 編集中のテーマリポジトリのファイルをクラウドリポジトリに移動するには、次のようなコマンドを使用します。
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例えば、次のコマンドを使用します。 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. クラウドリポジトリのディレクトリで、次のコマンドを使用して、に移動したテーマファイルをコミットします。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. カスタマイズ内容が Git リポジトリにプッシュされます。

   ![コミット済みの変更](/help/forms/assets/cmd_git_push.png)

これで、カスタマイズ内容が Git リポジトリに安全に保存されました。


### 7.フロントエンドパイプラインを実行する {#deploy-pipeline}

1. フロントエンドパイプラインを作成して、カスタマイズしたテーマをデプロイします。 学ぶ [カスタマイズしたテーマをデプロイするための最前線パイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. 作成したフロントエンドパイプラインを実行し、 **[!UICONTROL スタイル]** タブをクリックします。

>[!NOTE]
>
>今後、キャンバステーマフォルダーで変更を加える場合は、上記のパイプラインを再実行する必要があります。 したがって、パイプラインの名前を覚えておく必要があります。

## テーマをカスタマイズする例 {#example-to-customize-a-theme}

1. AEM Forms オーサーインスタンスにログインします。
1. コアコンポーネントを使用して作成されたアダプティブフォームを開きます。
1. コマンドプロンプトでローカルプロキシサーバーを起動し、 **ローカルでログイン（管理者タスクのみ）**.
1. サインインすると、ブラウザーにリダイレクトされ、適用されたテーマが表示されます。
1. をダウンロードします。 [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas) ダウンロードした zip フォルダーを展開します。
1. 展開した zip フォルダーを目的のエディターで開きます。
1. の作成 `.env` theme フォルダー内のファイルに次のパラメーターを追加します。 **AEM URL**, **AEM_ADAPTIVE_FORM** および **AEM_PROXY_PORT**.
1. キャンバステーマフォルダーのテキストボックスの CSS ファイルを開き、境界線の色を次のように変更します。 `red` 色を付けて変更を保存します。
1. ブラウザーを再度開くと、変更が直ちにアダプティブフォームに反映されます。
1. クローンリポジトリ内のキャンバステーマフォルダを移動します。
1. 変更をコミットし、フロントエンドパイプラインを実行します。

パイプラインを実行すると、「スタイル」タブでテーマを使用できるようになります。

## ベストプラクティス {#best-practices}

* **別のテーマのアセットの回避**

   テーマを編集する際、アセット（画像など）を他のテーマから参照して追加することができます。例えば、ページの背景を編集しているとします。例えば、**[!UICONTROL ページ]** ![edit-button](assets/edit-button.png)／**[!UICONTROL 背景]**／**[!UICONTROL 追加]**／**[!UICONTROL 画像]**&#x200B;を選択すると、他のテーマの画像を参照して追加することが可能なダイアログが表示されます。

   アセットを別のテーマから追加し、そのテーマが移動または削除されると、現在のテーマに問題が生じる場合があります。他のテーマからアセットを参照して追加しないようにすることをお勧めします。

* **コンテナパネルのレイアウト幅の変更**

   コンテナパネルのレイアウト幅の変更はお勧めしません。コンテナパネルの幅を指定すると、幅が静的になり、様々なディスプレイに合わせて調整されません。

* **ヘッダーとフッターを使用するためのフォームエディターまたはテーマエディターの使用**

   テーマエディターは、フォントスタイル、背景、透明度などのスタイル設定オプションを使用してヘッダーとフッターのスタイルを設定する場合に使用します。
ヘッダーにロゴイメージや企業名などの情報を表示し、フッターに著作権情報を表示する場合は、フォームエディターのオプションを使用します。
