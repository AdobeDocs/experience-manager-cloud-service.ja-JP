---
title: デモサイトで AEM Screens を有効にする
description: デモサイトでAEM Screensのas a Cloud Service的なエクスペリエンスを完全に有効にする手順を説明します。
exl-id: 369eea9f-2e81-4b87-841c-188b67657bab
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 57%

---

# デモサイトで AEM Screens を有効にする {#enable-screens}

デモサイトでAEM Screensのas a Cloud Service的なエクスペリエンスをフルに活用する手順を説明します。

>[!NOTE]
>
>AEM Screensデモを Cloud Manager プログラムに追加するには、Screens アドオンが必要です。 学ぶ [ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/adding-screens-addon/add-on-new-program-screens-cloud.html) 追加する方法を説明します。

## これまでの説明内容 {#story-so-far}

前のドキュメントのAEM Reference Demos アドオンジャーニーでは、 [デモサイトの作成、](create-site.md) 参照デモアドオンのテンプレートに基づいてデモサイトを作成しました。 その結果、以下を習得しました。

* AEM オーサリング環境へのアクセス方法の理解。
* テンプレートに基づくサイトの作成方法の理解。
* サイト構造内を移動し、ページを編集する際の基本事項の理解。

デモサイトを参照して管理するためのツールを理解できた独自のデモサイトがあるので、デモサイトでAEM Screensas a Cloud Serviceのフルエクスペリエンスを有効にできます。

## 目的 {#objective}

AEM Reference Demos Add-on には、コーヒーショップの業務部門である We.Cafe のAEM Screensコンテンツが含まれています。 このドキュメントでは、AEM Screens のコンテキストで We.Cafe デモの設定を実行する方法を説明します。読み終えると、次のことができるようになります。

* AEM Screens の基本的な知識。
* We.Cafe デモコンテンツの理解。
* We.Cafe 用の AEM Screens の設定方法。
   * We.Cafe 用の Screens プロジェクトの作成方法。
   * Google シートおよび API を使用してシミュレーションした気象サービスの設定。
   * 「天気予報サービス」に基づいて動的に変化する Screens コンテンツのシミュレーション。
   * Screens Player のインストールと使用。

## Screens について {#understand-screens}

AEM Screens as a Cloud Service は、マーケターが動的なデジタルエクスペリエンスを大規模に作成および管理できるデジタルサイネージソリューションです。AEM Screens as a Cloud Service を使用すると、公共の場所で使用するための魅力的で動的なデジタルサイネージエクスペリエンスを作成できます。

>[!TIP]
>
>AEM Screens as a Cloud Service の詳細については、このドキュメントの最後にある、[その他のリソース](#additional-resources)の節を参照してください。

AEM Reference Demos Add-on をインストールすると、デモオーサリング環境でAEM Screensの We.Cafe コンテンツを自動的に使用できるようになります。 以下に示す手順については、 [デモ用スクリーンプロジェクトのデプロイ](#deploy-project) は、そのコンテンツを公開し、メディアプレーヤーにデプロイするなどして、AEM Screensのフルエクスペリエンスを有効にするのに役立ちます。

## デモコンテンツについて {#demo-content}

We.Cafe コーヒーショップは、米国の 3 か所に 3 つの店舗で構成されています。 3 つの店では 3 つの同じようなエクスペリエンスを提供しています。

* カウンター上に設置された、縦パネルが 2 つまたは 3 つのメニューボード
* 客を誘い込むために通りに面してエントランス設置された、横パネルまたは縦パネルが 1 つのディスプレイ
* 1 台の縦型タブレットで行列を回避するセルフオーダーのキオスクブース

>[!NOTE]
>
>現在のバージョンのデモでは、エントランスのディスプレイのみテストできます。その他のディスプレイは、今後のバージョンで対応予定です。
>
>キオスクは、現在のバージョンのデモには含まれていません。今後のバージョンに含まれる予定です。

New-York の場所は、スペースの少ない小さな店舗にあると想定され、次のようになります。

* 縦パネルが 2 つのみのメニューボード。サンフランシスコとサンノゼでは縦パネルは 3 つ
* エントランスの表示は、横ではなく縦に配置

>[!NOTE]
>
>ScreensCloud Service( [Screens にas a Cloud Service](#connect-screens) 「 」セクションで、「 」の下にフォルダーとしてロケーションを作成します。 ディスプレイについて詳しくは、このドキュメントの最後にある[その他のリソース](#additional-resources)の節を参照してください。

### カフェレイアウト {#care-layouts}

We.Cafe の場所のレイアウトは次のとおりです。

![We.Cafe レイアウト](assets/cafe-layouts.png)

>[!NOTE]
>
>画面の測定値はインチ単位です。

### エントランス {#entrance}

入り口のディスプレイは日分割され、朝から午後に、最初の画像を変えるだけです。 また、シーケンスの各パスでは、別の特別なコーヒーの準備を広告し、有料埋め込みシーケンスを使用して、毎回異なるアイテムを再生します。

入り口チャネルの最後の画像も、外部温度に基づいて（つまり動的に変化する）ターゲット設定され、 [シミュレートされたデータソースを作成](#data-source) 」セクションに入力します。

## デモ用 Screens プロジェクトのデプロイ {#deploy-project}

で作成したサンドボックスのデモコンテンツを使用するには [プログラムを作成](create-program.md) 手順：サイトは、テンプレートに基づいて作成する必要があります。

We.Cafe デモサイトをまだ作成していない場合は、[デモサイトの作成](create-site.md)の節の同じ手順に従ってください。テンプレートを選択する場合は、**We.Cafe web サイトテンプレート**&#x200B;を選択します。

![We.Cafe テンプレート](assets/wecafe-template.png)

ウィザードが完了したら、「サイト」の下にコンテンツがデプロイされ、他のコンテンツと同様に移動して参照できます。

![We.Cafe コンテンツ](assets/wecafe-content.png)

We.Cafe デモコンテンツが用意できたので、AEM Screens のテスト方法を選択します。

* AEM Sites コンソール内のコンテンツのみを参照する場合は、[その他のリソース](#additional-resources)の節で詳細を参照および確認します。これ以上のアクションは必要ありません。
* AEM Screens のすべての動的機能を体験したい場合は、次の節 [Screens コンテンツの動的な変更](#dynamically-change)に進みます。

## Screens コンテンツの動的な変更 {#dynamically-change}

AEM Sites と同様に、AEM Screens もコンテキストに基づいて動的にコンテンツを変更できます。We.Cafe デモでは、現在の気温に応じて異なるコンテンツを表示するようにチャネルが設定されています。このエクスペリエンスをシミュレートするには、独自のシンプルな気象サービスを作成する必要があります。

### シミュレーションデータソースの作成 {#data-source}

デモ中やテスト中は天候を変えるのが難しいので、温度の変化をシミュレートする必要があります。 天気予報サービスは、AEM ContextHub が呼び出して温度を取得するGoogleシートスプレッドシートに温度値を保存することでシミュレートされます。

#### Google API キーの作成 {#create-api-key}

まず、データ交換を容易にするGoogle API キーを作成する必要があります。

1. Googleアカウントにログオンします。
1. このリンク `https://console.cloud.google.com`.を使用して Cloud Console を開きます。
1. ツールバーの左上にある、現在のプロジェクト名 ( **Google Cloud Platform** ラベル

   ![Google Cloud Console](assets/google-cloud-console.png)

1. プロジェクトの選択ダイアログで、「**新しいプロジェクト**」をクリックします。

   ![新しいプロジェクト](assets/new-project.png)

1. プロジェクトに名前を付け、「**作成**」をクリックします。

   ![プロジェクトを作成](assets/create-project.png)

1. 新しいプロジェクトが選択されていることを確認し、Cloud Console のダッシュボードにあるハンバーガーメニューを使用して、「 」を選択します。 **API とサービス**.

   ![API とサービス](assets/apis-services.png)

1. API とサービスウィンドウの左側のパネルで、ウィンドウ上部の「**認証情報**」をクリックし、「**認証情報を作成**」で「**API キー**」をクリックします。

   ![認証情報](assets/credentials.png)

1. ダイアログボックスで、新しい API キーをコピーし、後で使用するために保存します。 クリック **閉じる** ダイアログボックスを終了できます。

#### Google Sheets API の有効化 {#enable-sheets}

API キーを使用してGoogle Sheets のデータを交換できるようにするには、Google Sheets API を有効にする必要があります。

1. Google Cloud Console（`https://console.cloud.google.com`）のプロジェクトに戻り、ハンバーガーメニューを使用して、**API とサービス／ライブラリ**&#x200B;を選択します。

   ![API ライブラリ](assets/api-library.png)

1. API ライブラリ画面で、検索場所までスクロールします。 **Google Sheets API**&#x200B;をクリックし、次にクリックします。

   ![API ライブラリ検索](assets/api-library-search.png)

1. 内 **Google Sheets API** ウィンドウ、クリック **有効にする**.

   ![Google Sheets API](assets/sheets-api.png)

#### Google Sheets スプレッドシートの作成 {#create-spreadsheet}

これで、Google Sheets のスプレッドシートを作成して天気データを保存できます。

1. に移動します。 `https://docs.google.com` をクリックし、Google Sheet スプレッドシートを作成します。
1. 気温を定義するには、セル A2 に、`32` のように入力します。
1. 「 **共有** 窓の右上の下に **リンクを取得**&#x200B;をクリックし、 **変更**.

   ![シートを共有](assets/share-sheet.png)

1. 次の手順のために、リンクをコピーします。

   ![リンクを共有](assets/share-link.png)

1. シート ID を探します。

   * シート ID は、シートリンクの後にコピーした文字のランダムな文字列です `d/` 以前 `/edit`.
   * 次に例を示します。
      * URL が `https://docs.google.com/spreadsheets/d/1cNM7j1B52HgMdsjf8frCQrXpnypIb8NkJ98YcxqaEP30/edit#gid=0` の場合
      * シート ID は `1cNM7j1B52HgMdsjf8frCQrXpnypIb8NkJ98YcxqaEP30`.です。

1. 後で使用するためにシート ID をコピーします。

#### 気象サービスのテスト {#test-weather-service}

データソースを Google シートのスプレッドシートに作成し、API を介したアクセスを有効にしたので、テストして「気象サービス」にアクセスできることを確認します。

1. Web ブラウザーを開きます。

1. 次のリクエストを入力し、以前に保存したシート ID と API キーの値を置き換えます。

   ```
   https://sheets.googleapis.com/v4/spreadsheets/<yourSheetID>/values/Sheet1?key=<yourAPIKey>
   ```

1. 次のような JSON データを受け取った場合は、適切に設定されています。

   ```json
   {
     "range": "Sheet1!A1:Z1000",
     "majorDimension": "ROWS",
     "values": [
       [],
       [
         "32"
       ]
     ]
   }
   ```

AEM Screensも同じサービスを使用して、次の手順で設定したシミュレーション済みの天気データにアクセスできます。

### ContextHub の設定 {#configure-contexthub}

AEM Screens は、コンテキストに基づいて動的にコンテンツを変更できます。We.Cafe デモでは、AEM ContextHub を使用して、現在の温度に応じて異なるコンテンツを表示するようにチャネルを設定しています。

>[!TIP]
>
>ContextHub の詳細については、このドキュメントの最後にある、[その他のリソース](#additional-resources)の節を参照してください。

画面コンテンツが表示されると、ContextHub が気象サービスを呼び出して現在の温度を見つけ、表示するコンテンツを決定します。

デモ用に、シートの値を変更できます。ContextHub はこの事実を認識し、更新された温度に応じてコンテンツがチャネル内で調整されます。

1. AEMaaCS オーサーインスタンスで、**グローバルナビゲーション／ツール／Sites／ContextHub** に移動します。
1. **We.Cafe web サイトテンプレート**&#x200B;から Screens プロジェクトを作成した際に付けた名前と同じ名前の設定コンテナを選択します。
1. **設定／ContextHub 設定／Google Sheets** を選択し、右上の「**次へ**」をクリックします。
1. 設定には、既に JSON データが設定されている必要があります。次の 2 つの値を変更する必要があります。
   1. 置換 `[your Google Sheets id]` を、 [以前に保存した](#create-spreadsheet).
   1. 置換 `[your Google API Key]` を [以前に保存した](#create-api-key).
1. 「**保存**」をクリックします。

これで、Googleシートのスプレッドシートで温度値を変更し、ContextHub で Screens を「天気の変化を確認」するたびに動的に更新できるようになりました。

### 動的データのテスト {#test-dynamic}

これで、AEM Screensと ContextHub が天気予報サービスに接続されたので、これをテストして、Screens でコンテンツを動的に更新する方法を確認できます。

1. サンドボックスオーサーインスタンスにアクセスします。
1. **グローバルナビゲーション／Sites** からサイトコンソールに移動し、以下のページを選択します。**Screens／&lt;project-name>／チャネル／エントランス朝（縦）**

   ![デモプロジェクトのコンテンツを選択](assets/project-content.png)

1. クリック **編集** ツールバーで、またはショートカットキーを入力します。 `e` ページを編集できます。

1. エディターで、コンテンツを表示できます。1 つの画像が青色でハイライトされ、隅にターゲティングアイコンが表示されます。

   ![エディター内の Screens コンテンツ](assets/screens-content-editor.png)

1. スプレッドシートに入力した温度を 32 から 70 に変更し、内容の変更を確認します。

   ![エディター内の Screens コンテンツ](assets/screens-content-editor-2.png)

凍えるような 32 °F（0 °C）から快適な 70 °F（21 °C）に変化したことにより、フィーチャー画像が温かい飲み物から涼しげなアイスコーヒーに変わりました。

>[!IMPORTANT]
>
>説明されている Google Sheets のソリューションは、デモ目的のみに使用してください。アドビでは、実稼動環境への Google Sheets の使用はサポートしていません。

## Screens as a Cloud Service に接続 {#connect-screens}

デジタルサイネージデバイスやコンピューターで動作する Player を含め、実際のデジタルサイネージエクスペリエンスも設定する場合は、次の手順に従います。

または、AEMaaCS のチャネルエディターで簡単にデモをプレビューできます。

>[!TIP]
>
>チャネルエディターの詳細については、このドキュメントの最後にある、[その他のリソース](#additional-resources)の節を参照してください。

### AEM Screens as a Cloud Service の設定 {#configure-screens}

まず、Screens デモコンテンツをAEM Screensas a Cloud Serviceに公開し、サービスを設定する必要があります。

1. デモスクリーンプロジェクトのコンテンツを公開します。
1. Screens as a Cloud Service `https://experience.adobe.com/screens` に移動し、ログインします。
1. 画面の右上に、自分の組織が表示されていることを確認します。

   ![Screens 組織を確認する](assets/screens-org.png)

1. 左上隅付近で、 **設定を編集** 歯車のような形をしたアイコン。

   ![設定を編集](assets/screens-edit-settings.png)

1. デモサイトを作成した AEMaaCS オーサーインスタンスとパブリッシュインスタンスの URL を指定し、 **保存**.

   ![画面設定](assets/screens-settings.png)

1. デモインスタンスに接続すると、Screens はチャネルコンテンツを取り込みます。 クリック **チャネル** が左側のパネルに表示され、公開済みのチャネルが表示されます。 情報が表示されるまでしばらく時間がかかる場合があります。画面右上の青い「**同期**」ボタンをクリックすると、情報を更新できます。

   ![デモチャネル情報](assets/screens-channels.png)

1. クリック **表示** をクリックします。 まだデモ用に作成していません。We.Cafe の場所をシミュレートするには、それぞれのフォルダを作成します。 クリック **作成** 画面の右上にある「 」をクリックし、 **フォルダー**.

   ![ディスプレイを作成](assets/screens-displays.png)

1. ダイアログボックスで、次のようなフォルダ名を指定します。 **サンノゼ** をクリックし、 **作成**.

1. フォルダーをクリックして開き、「 **作成** 右上にあるを選択し、 **表示**.

1. ディスプレイ名を入力し、「**作成**」をクリックします。

   ![ディスプレイを作成](assets/create-display.png)

1. ディスプレイの作成後、ディスプレイの名前をクリックしてディスプレイの詳細画面を開きます。 デモサイトから同期されたチャネルがディスプレイに割り当てられている必要があります。クリック **チャネルを割り当て** をクリックします。

   ![チャネルの詳細](assets/channel-detail.png)

1. ダイアログで、チャネルを選択し、「**割り当て**」をクリックします。

   ![チャネルを割り当て](assets/assign-channel.png)

追加の場所とディスプレイに対して、これらの手順を繰り返します。完了したら、デモサイトをAEM Screensにリンクし、必要な設定を完了しました。

AEMaaCS のチャネルエディターで簡単にデモをプレビューできます。

### Screens Player の使用 {#screens-player}

実際の画面に表示されるようにコンテンツを表示するには、Player をダウンロードして、ローカルに設定します。AEM Screens as a Cloud Serviceがプレーヤーにコンテンツを配信

#### 登録コードの生成 {#registration-code}

まず、プレーヤーをAEM Screens as a Cloud Serviceに安全に接続するための登録コードを作成する必要があります。

1. Screens as a Cloud Service `https://experience.adobe.com/screens` に移動し、ログインします。
1. 画面の右上に、自分の組織が表示されていることを確認します。

   ![Screens 組織を確認する](assets/screens-org.png)

1. 左側のパネルで、 **プレーヤー管理/登録コード** 次に、 **コードの作成** をクリックします。

![登録コード](assets/registration-codes.png)

1. コードの名前を入力し、「**作成**」をクリックします。

   ![コードの作成](assets/create-code.png)

1. コードが作成されると、リストに表示されます。クリックして、コードをコピーします。

   ![登録コード](assets/registration-code.png)

#### Player のインストールおよび設定 {#install-player}

1. お使いのプラットフォーム用の Player を `https://download.macromedia.com/screens/` からダウンロードしてインストールします。
1. プレーヤーを実行し、 **設定** タブをクリックします。
1. 下までスクロールし、「 」をクリックして両方を確定します。 **工場出荷時にリセット** および **クラウドモードに変更** オプション。

   ![Player 設定](assets/player-configuration.png)

1. プレーヤーが自動的に **プレーヤーの登録** タブをクリックします。 以前に生成したコードを入力し、 **登録**.

   ![Player 登録](assets/player-registration-code.png)

1. 「**システム情報**」タブに移動し、Player が登録されたことを確認します。

   ![登録済みの Player](assets/player-registered.png)

#### Player のディスプレイへの割り当て {#assign-player}

1. Screens as a Cloud Service `https://experience.adobe.com/screens` に移動し、ログインします。
1. 画面の右上に、自分の組織が表示されていることを確認します。

   ![Screens 組織を確認する](assets/screens-org.png)

1. 左側のパネルで、 **プレーヤー管理/プレーヤー** 以前にインストールして登録したプレーヤーが表示されます。

   ![Player](assets/players.png)

1. プレーヤー名をクリックして、詳細を開きます。 クリック **表示に割り当て** をクリックします。

   ![Player のディスプレイへの割り当て](assets/assign-to-display.png)

1. ダイアログボックスで、以前に作成した表示を選択し、 **選択**.

   ![ディスプレイの割り当て](assets/assign-a-display.png)

#### 再生 {#playback}

Player にディスプレイを割り当てると、AEM Screens as a Cloud Service はコンテンツを Player に配信し、コンテンツが表示されるようにします。

![エントランス（縦）](assets/entrance-portrait.jpg)

![エントランス（横）](assets/entrance-landscape.jpg)

## 次の手順 {#what-is-next}

これで、AEM Reference Demo アドオンのジャーニーのこの部分が完了し、以下をおこなう必要があります。

* AEM Screens の基本的な知識。
* We.Cafe デモコンテンツの理解。
* We.Cafe 用の AEM Screens の設定方法。

これで、独自のデモサイトを使用して AEM Screens の機能を試す準備が整いました。続いてジャーニーの次の節、[デモサイトの管理](manage.md)に進んで、デモサイトの管理に役立つツールと、デモサイトを削除する方法を学びます。

また、このジャーニーで説明した機能について詳しくは、[その他のリソース](#additional-resources)の節で紹介しているその他のリソースを参照してください。

## その他のリソース {#additional-resources}

* [ContextHub ドキュメント](/help/sites-cloud/authoring/personalization/contexthub.md) - ContextHub を使用して、天気に関係なく、ユーザーコンテキストに基づいてコンテンツをパーソナライズする方法を説明します。
* [API キーの使用 - Google ドキュメント](https://developers.google.com/maps/documentation/javascript/get-api-key) - Google の API キーの使用の詳細に関する便利なリファレンスです。
* [ディスプレイ](/help/screens-cloud/creating-content/creating-displays-screens-cloud.md) - AEM Screens でのディスプレイの詳細と機能について説明します。
* [Player をダウンロード](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md) - Screens Player へのアクセス方法とインストール方法について説明します。
* [Player を登録](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) - Player を設定して AEM Screens プロジェクトに登録する方法を説明します。
* [ディスプレイへの Player の割り当て](/help/screens-cloud/managing-players-registration/assigning-player-display.md) - Player でコンテンツを表示するように設定します。
