---
title: コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築
seo-title: Build Engaging Forms Using Core Components and Headless
description: コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: b68902ef4f7c61f77aa0d03ad718d5bf3023dea0
workflow-type: tm+mt
source-wordcount: '2465'
ht-degree: 1%

---


# コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築

## ラボの概要

この実践ラボでは、次のことを学習します。

AEM Formsを使用してAEM Sitesと一貫性のある最新のコアコンポーネントを簡単にアダプティブフォームを作成する方法。アダプティブフォームをヘッドレスフォームとして Web、モバイル、チャットに配信することで、オムニチャネルのデータ取得機能を有効にします。 また、スタイル設定、カスタマイズ、フロントエンド開発に関するベストプラクティスについても学習します。

## 重要な留意点

* **ビジネスの俊敏性**:ビジネスユーザーは、複数のチャネル用のフォームエクスペリエンスを簡単に作成できます。

* **フロントエンド開発者に対するパワー**:フロントエンド開発者は、ヘッドレスフォームを使用してエンドユーザーエクスペリエンスを制御できます。

* **開発者の速度**:開発者は、 Sites コンポーネントとFormsコンポーネントを簡単かつ一貫してカスタマイズできます。

## 前提条件

AEM Forms as aCloud Servicesandbox

## レッスン 1

### 目的

AEM Forms as a Cloud Service環境の理解。

### レッスンのコンテキスト

このレッスンでは、ユーザーインターフェイスを移動して、 AEM Formsas a Cloud Serviceの環境について理解します。

### 演習

1. ブラウザーを開き、ブラウザーオーサー環境の URL をCloud Serviceします。 次に例を示します。
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. 共有された資格情報に従って、Cloud Serviceオーサー環境にログインします。 例：ユーザー名： [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
パスワード： 
**Adobe123!**

1. ログインした後、AEM Forms UI に移動します。 クリック **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. クリック **Forms &amp; Documents**. 環境設定や情報に関連するポップアップを解除します。

   ![](/help/forms/assets/screenshot2028113929.png)

   使用可能なすべてのフォームが表示されます。

   ![](/help/forms/assets/screenshot2028114029.png)

## レッスン 2

### 目的

最新のコアコンポーネントを使用してアダプティブフォームを作成し、フォームを設定して送信します。

## レッスンのコンテキスト

このレッスンでは、ビジネスユーザーとして、データ取得用の標準化された OOTB コアコンポーネントを使用したアダプティブフォームオーサリングを使用して、Web、モバイル、チャットなど複数のチャネル用のアダプティブフォームを作成します。

## 演習

1. フォームの送信エンドポイントを作成します。

   1. 開く <https://requestbin.com/> をクリックします。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. クリック **公開 bin の作成** エンドポイント URL をコピーします。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. ウィザードインターフェイスを使用してアダプティブフォームを作成するには、次の手順を実行します。

   1. レッスン 1 で使用するブラウザータブで、 AEM Forms as aCloud ServiceWeb インターフェイスに移動し、 Formsとドキュメントに移動します。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. クリック **作成** 「アダプティブフォーム」を選択します。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. を選択します。 **コアコンポーネントで空白** テンプレートを選択画面から選択します（下図を参照）。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 次をクリック： **スタイル** 」タブで「 **wknd-theme** テーマを次に示します。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 次をクリック： **送信** 」タブで「 **REST エンドポイントに送信** カードを選択し、
      **POST要求の URL** フィールドには次のように表示されます。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 「**作成**」をクリックします。フォームの名前とタイトルを指定します。 例： **接触**. 「**作成**」をクリックします。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. アダプティブフォームエディターが開きます。 ポップアップまたはダイアログを閉じて、環境設定や情報を表示します。 左側のパネルでコンポーネントブラウザーをクリックし、 **フッター** コンポーネントを空白のフォームの下部に配置します。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. を **ヘッダー** コンポーネントをフォームの上部に配置します。
      ![](/help/forms/assets/screenshot2028122029.png)

   1. を追加します。 **タイトル** コンポーネントをフォームの中央に配置します。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. を追加します。 **テキスト入力** コンポーネントをタイトルコンポーネントの後に追加します。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. を追加します。 **数値入力** コンポーネント。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. を追加します。 **送信ボタン** コンポーネントをフォームに追加します。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 次をクリック： **タイトル** そのような要素 **ポップアップメニュー** が表示されます。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 入力 `Contact Us` をタイトルテキストとして使用します。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 次をクリック： **テキスト入力** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 入力 **氏名** をフィールドラベルとして使用します。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 次をクリック： **数値入力** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 次を入力します。 **電話番号** をフィールドラベルとして使用します。
      ![](/help/forms/assets/screenshot2028123829.png)


1. フォームに検証機能を追加：

   1. 次をクリック： **電話番号** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **レンチアイコン** をクリックして、フィールドを設定します。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. を開きます。 **「検証」タブ**、フィールドに **必須**&#x200B;をクリックし、 **完了**. 成功メッセージが表示されます。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. クリック **プレビュー** をクリックして、エンドユーザーの観点からフォームをプレビューします。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. ダミーデータでフォームに入力
      ![](/help/forms/assets/screenshot2028125629.png)

   1. フォームを送信
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 「 Request bin 」タブで、送信されたデータを確認します。
      ![](/help/forms/assets/screenshot2028125829.png)

ここで、残りの練習では、事前に作成した登録フォームを使用します。

1. AEM Forms管理インターフェイスを開きます。例： `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`をクリックし、登録フォームを選択します。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 「**公開する**」をクリックします。

   ![](/help/forms/assets/screenshot2028115629.png)

   成功メッセージが表示されます。

   ![](/help/forms/assets/screenshot2028115729.png)

   フォームの発行 URL は、次のようになります。 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. 公開されたフォームを表示するには、上記の URL のプログラム ID(pXXXXXX) と環境 ID(eXXXXXX) を、お使いの環境の ID に置き換えます。

## レッスン 3

### 目的

フロントエンド開発のベストプラクティスを使用してスタイルを更新します。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者が、以前に作成したアダプティブフォームのスタイル設定を簡単に更新する方法を学習します。

### 演習

テーマのローカルリポジトリを設定します。

1. 管理者権限でコマンドプロンプトまたはシェルを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、テーマのフロントエンドコードを複製します。

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 次のコマンドをリストに表示された順序で使用して、 **aem-forms-theme-canvas** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 選択 **親フォルダー内のすべてのファイルの作成者を信頼する** をクリックし、 **はい、私は著者を信頼しています**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. クラウドサービスのパブリッシュ環境でホストされているフォームをレンダリングするには、 `env_template` ファイル。  ファイル名を変更するには、 **env_template** ファイルを開き、 **名前を変更** オプション。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. .env ファイルの変数に次の値を設定して、ファイルを保存します。

   * **AEM_URL**:クラウドサービスのパブリッシュ環境を指定します。 例：`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**:フォームのパスを指定します。 例えば、フォームのパスが `/content/forms/af/registration`の場合、この変数の値は次のようになります。 `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * を使用して npm を更新するように求めるメッセージが表示された場合、 `npm notice Run npm nstall -g npm@9.6.0`コマンドを使用して、メッセージを無視します。
   > * ワークブックでの指示がない限り、他の npm コマンドを実行しないでください。


1. 次のコマンドを実行して、フォームをプレビューします。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   上記のコマンドを実行したら、 `webpack compiled` メッセージ。 フォームがブラウザータブに表示されます。

   >[!NOTE]
   >
   >を実行した後、ブラウザーで空白の画面が表示される場合、 `npm run live` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. Visual Studio Code で、 `PROJECT\src\site\_variables.scss` ファイル。 注意： `$error` 色は赤の影です。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーで、フォームを送信し、 **名** フィールドに入力します。

   ![](/help/forms/assets/screenshot2028120829.png)

1. を **$error** 色付け **#5736eb** ファイルを保存します。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーを更新し、フォームを送信します。 名フィールドのエラー色は、それに応じて変更されています。

   ![](/help/forms/assets/screenshot2028121129.png)

1. コマンドプロンプトで、 **Ctrl + C**&#x200B;を入力して、 **Y**&#x200B;を押し、 **入力** npm プロセスを終了するためのキー。 次の一連の演習と競合しないように、npm サーバーを停止することが重要です。
1. Visual Studio の [ コード ] ウィンドウと [ コマンドプロンプト ] ウィンドウを閉じます。

## レッスン 4

### 目的

フォームをヘッドレスフォームとして Web/モバイルおよび他のインターフェイスにレンダリングします。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者として、React スペクトルデザインフレームワークを使用して、前にヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

React スタータープロジェクトを使用してローカルリポジトリを設定する：

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、アダプティブフォームの React スタータープロジェクトを複製します。

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 次のコマンドをリストに表示された順序で使用して、 **react-starter-kit-aem-headless-forms** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   「Visual Studio Code」ウィンドウが開きます。

   ![](/help/forms/assets/screenshot2028117429.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには：

1. env_template ファイルの名前を.env ファイルに変更します。 名前を変更するには、 **env_template** ファイルを開き、 **名前を変更** オプション。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. .env ファイル内の変数に次の値を設定します。 変数を更新したら、ファイルを保存します。

   * **AEM_URL**:クラウドサービスパブリッシュ環境の URL を指定します。 例：`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**:前のレッスンで作成したアダプティブフォームのパスを指定します。 例：`/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. コマンドウィンドウを開き、 react-starter-kit-aem-headless-forms ディレクトリに移動し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上記のコマンドは、react-spectrum フロントエンドローカル開発を使用して、AEMから取得したフォーム定義をヘッドレス方式でレンダリングするライブラリサーバーを起動します。

   >[!NOTE]
   >
   > 
   > を実行した後、ブラウザーで空白の画面が表示される場合、 `npm start` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.

   ![](/help/forms/assets/screenshot2028118229.png)

このヘッドレスフォームでのルールの実行を確認しましょう。

1. を選択します。 **チェックボックスをオンにして 5%オフにします** オプション。 クレジットカードを適用する後続のオプションは無効になります。

   ![](/help/forms/assets/screenshot2028126229.png)

1. オフ **チェックボックスをオンにして 5%オフにします** をクリックして、クレジットカードオプションを有効にします。

   ![](/help/forms/assets/screenshot2028126329.png)

サーバー上のフォームをビジネスユーザーとして変更し、ヘッドレスフォームに自動的に反映された変更を表示します。

1. ブラウザーでAEM Forms管理インターフェイスを開きます。 例： [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. を選択します。 **登録** フォームとクリック **編集。** アダプティブフォームエディターでフォームが開きます。

   ![](/help/forms/assets/screenshot2028118529.png)

1. を選択します。 **電話番号** フィールドに入力し、 **編集アイコン（鉛筆アイコン）** 」と入力します。 ポップアップツールバーが表示されない場合は、 **編集** 右上のボタン、左から **プレビュー** 」ボタンをクリックします。

   ![](/help/forms/assets/screenshot2028119629.png)

1. ラベルを「モバイル番号」に変更します。 フォーム内の空のスペースをクリックすると、フォームに加えた変更が保存されます。

   ![](/help/forms/assets/screenshot2028119729.png)

更新したフォームを発行して、変更を発行環境に反映します。

1. 「 AEM Forms管理インターフェイス」タブで、登録フォームを選択し、 **非公開**. 次の項目が表示されない場合、 **非公開** ボタンをクリックし、手順 3 に進んで変更を直接公開します。

   ![](/help/forms/assets/screenshot2028119829.png)

1. **非公開**&#x200B;をクリックします。クリック **閉じる** を設定します。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. ブラウザーが更新されたら、登録フォームを選択し、 **公開**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. 「**公開する**」をクリックします。クリック **閉じる** を設定します。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. ヘッドレスフォームが表示された状態で、ブラウザータブを更新します。 「電話番号」のラベルが「モバイル番号」に変更されていることに注意してください。

   ![](/help/forms/assets/screenshot2028120529.png)

1. を起動するために使用する [ コマンドプロンプト ] ウィンドウを開きます。 **react-starter-kit-aem-headless-forms** プロジェクト、押す **Ctrl + C**&#x200B;を入力し、 **Y** をクリックし、Enter キーを押して npm プロセスを終了します。 次の一連の演習と競合しないように、npm サーバーを停止することが重要です。

1. Visual Studio の [ コード ] ウィンドウと [ コマンドプロンプト ] ウィンドウを閉じます。


## レッスン 5

### 目的

Google Material UI を使用してフォームをヘッドレスフォームとしてレンダリング

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者がGoogle Material UI を使用して、前の手順でヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

Material UI スタータープロジェクトを使用してローカルリポジトリを設定します。

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)


1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー：

   ```Shell
   cd c:\git
   ```

1. 次のコマンドをリストに表示された順序で実行して、mui という名前のフォルダーを作成し、次のコマンドを使用して mui フォルダーに移動します。

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 次のコマンドを使用して、アダプティブフォームの React スタータープロジェクトを複製します。

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 次のコマンドをリストに表示された順序で使用して、 **react-starter-kit-aem-headless-forms** フォルダーに移動し、Visual Studio コードでコードを開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには：

1. 名前を変更 **env_template** ～に提出する **.env** ファイル。 名前を変更するには、 **env_template** ファイルと選択 **名前を変更**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. .env ファイル内の変数に次の値を設定します。 変数を更新したら、ファイルを保存します。 以下を使用： **Ctrl + S** 組み合わせを切り替えてファイルを保存します。

   * **AEM_URL**:クラウドサービスパブリッシュ環境の URL を指定します。 例： [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**:前のレッスンで作成したアダプティブフォームのパスを指定します。 例： /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. コマンドウィンドウを開き、 **react-starter-kit-aem-headless-forms** ディレクトリに移動し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   このコマンドは、ローカル開発サーバーを起動し、Google Material UI フロントエンドライブラリを使用して、AEMから取得したフォーム定義をヘッドレスにレンダリングします。

   >[!NOTE]
   >
   >を実行した後、ブラウザーで空白の画面が表示される場合、 `npm start` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. このフォームレンディションでの同じビジネスロジックの実行を評価するには：

   選択 **チェックボックスをオンにして 5%オフにします**. 後続のオプション **We.Finance 社のクレジットカードフォームを申し込みますか？** は無効になります。

   ![](/help/forms/assets/screenshot2028127329.png)

## レッスン 6

### 目的

マテリアル UI コンポーネントのバリエーションを使用して、ヘッドレスフォームの代替ルックアンドフィールを作成する

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者がビジネスユーザーによって以前に作成されたアダプティブフォームの Material UI を使用して、様々なコンポーネントの代替表現を作成する方法を学びます。

### 演習

ヘッドレスプロジェクト内のコンポーネントのバリエーションを更新します。 マテリアル UI のテキスト入力コンポーネントのバリアントをに変更するには `OutlinedInput`:

1. ビジュアルコードで、 `index.tsx` ～にファイルを送る `src/components/textinput/index.tsx`.

1. 追加 `//` コード行 103 の先頭に配置されます。 行がコメントに変換されます。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 104 行目で次のコードを追加して、別のバリアントのコンポーネントを使用し、ファイルを保存します。 以下を使用： **Ctrl + S** 組み合わせを切り替えてファイルを保存します。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   「OutlinedInput」バリアントで正しい大文字を使用する必要があります。大文字を使用しない場合、コンパイルが失敗します。 ローカル開発環境のコンパイルは、コマンドプロンプトで自動的に開始されます。 次のメッセージが表示されるまで待ちます

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. ブラウザを更新し、自動的に更新されない場合は、テキスト入力コンポーネントが別のバリアントを使用していることを確認します。

   ![](/help/forms/assets/screenshot2028127729.png)


   この変更は、AEM Forms Server のフォーム定義に変更を加えずにエンドユーザーに対しておこなわれ、考慮中のヘッドレスチャネルに固有のものです。 例えば、この実習では Web チャネルを使用します。

   ![](/help/forms/assets/screenshot2028127529.png)


1. Visual Studio コードとコマンドプロンプトウィンドウを閉じます。

## よくある質問 (FAQ)

+++ アダプティブフォームウィザードは一般に使用できますか？

はい、AEM FormsでCloud Serviceとして使用できます。

+++


+++ コアコンポーネントは一般公開されていますか？

はい、アダプティブFormsのコアコンポーネントは、AEM FormsでCloud Serviceとして使用できます。

+++

+++ ヘッドレスフォームは公開されていますか？

はい、ヘッドレスフォームは、AEM FormsでCloud Serviceとして使用できます。

+++

+++ ヘッドレスフォームには別のライセンスが必要ですか？

いいえ、ヘッドレスフォームは同じライセンス値指標、フォーム送信数を使用します。

+++

+++ コアコンポーネントとヘッドレスフォームはAEM 6.5 Formsで利用できますか？

はい。アダプティブフォームのコアコンポーネントとヘッドレスフォームは、AEM Forms 6.5 Service Pack 16 以降で使用できます。

+++


## 次の手順

これで、アダプティブフォームの構築方法を学び、ヘッドレスフォームを使用して複数のチャネルにアダプティブフォームを配信する方法を学びました。新しいスキルを活用する必要があります。 優れたデータキャプチャエクスペリエンスを作成し、大規模なエンドユーザーに提供することで、楽しみながら先に進むことができます。

## リソース

* [アダプティブフォームのコアコンポーネントの概要](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [コアコンポーネントを使用してアダプティブフォームを作成する](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [コアコンポーネントベースの AF のスタイル設定を更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [ヘッドレス React スターターキットの使用](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


