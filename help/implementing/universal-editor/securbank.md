---
title: ユニバーサルエディター用 SecurBank サンプルアプリ
description: SecurBank アプリを使用して実践的なエクスペリエンスを持つユニバーサルエディターについて説明します。このアプリは、ユニバーサルエディターの機能、柔軟性、使いやすさを紹介して、コンテンツの作成を高速化するように設計されています。
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---

# ユニバーサルエディター用 SecurBank サンプルアプリ {#securbank}

SecurBank アプリを使用して実践的なエクスペリエンスを持つユニバーサルエディターについて説明します。このアプリは、ユニバーサルエディターの機能、柔軟性、使いやすさを紹介して、コンテンツの作成を高速化するように設計されています。

## 前提条件 {#prerequisites}

* に割り当てられている必要があります **AEM管理者** [製品プロファイル](/help/journey-onboarding/assign-profiles-aem.md) :SecurBank アプリをインストールします。
* 以下が必要です [Node.js](https://nodejs.org) ローカル開発のためにバージョン 20 以降がインストールされています。

## SecurBank のインストール {#installation}

SecurBank アプリのインストールは簡単ですが、AEMas a Cloud Serviceの多くの領域に影響を与えるので、いくつかの手順が関係します。 主な手順の概要を次に示します。

1. [Cloud Manager でサンドボックスプログラムを作成します。](#create-sandbox-program)
1. [プログラムの Git リポジトリを複製し、SecurBank AEM プロジェクトのコンテンツを使用して更新します。](#clone-and-update)
1. [パイプラインを実行して SecurBank AEM プロジェクトをデプロイします。](#run-pipeline)
1. [ローカル web アプリ開発用の Cloud Manager 資格情報を取得します。](#retrieve-credentials)
1. [SecurBank Web アプリをダウンロードして構成します。](#download-web-app)
1. [SecurBank Web アプリを実行します。](#run-web-app)

次のセクションでは、必要な個々のタスクについて詳しく説明します。

### Cloud Manager でサンドボックスプログラムを作成します。 {#create-sandbox-program}

SecurBank をインストールできる新しい Cloud Manager プログラムが必要になります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. SecurBank アプリ用の新しいサンドボックスプログラムを作成します。

   * 選択時にデフォルトのオプションを使用 **ソリューションとアドオン**.
   * サンドボックスプログラムの作成方法について詳しくは、ドキュメントを参照してください。 [サンドボックスプログラムの作成。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### プログラムの Git リポジトリを複製し、SecurBank AEM プロジェクトのコンテンツを使用して更新します。 {#clone-and-update}

1. プログラムを作成したら、プログラムを開いて **リポジトリ** タブで、 **リポジトリ情報にアクセス** を開くためのボタン **リポジトリ情報** ダイアログを開いて、サンドボックス環境用の git リポジトリへのアクセスに必要な資格情報を表示します。

   * リポジトリ情報へのアクセス方法について詳しくは、ドキュメントを参照してください [リポジトリへのアクセス。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. の資格情報の使用 **リポジトリ情報** ローカルマシン上にリポジトリのクローンを作成します。

1. ローカルクローンのフォルダーを探して開き、hidden/dot ファイルを除くすべてのコンテンツを削除します。

1. で GitHub から最新の SecurBank AEM プロジェクトコードを取得します。 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) クリックして **コード** その後 **ZIP をダウンロード** ドロップダウンで選択します。

1. ローカルファイルシステム上の zip ファイルの内容を解凍し、サンドボックスプログラムのローカルクローンの空になったフォルダーに移動します。

1. ターミナルを使用して、複製されたプロジェクトのフォルダーに切り替え、すべてのコンテンツをコミットして Git にプッシュします。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### パイプラインを実行して SecurBank AEM プロジェクトをデプロイします。 {#run-pipeline}

SecurBank のAEM プロジェクトをサンドボックスリポジトリにコミットした状態で、パイプラインを使用してデプロイできます。

1. に戻る **概要** cloud Manager でサンドボックスプログラムの「」タブをクリックし、フルスタックの実稼動以外のパイプラインを実行します。

   * パイプライン実行のすべてのオプションをオフにします。
   * パイプラインの実行について詳しくは、ドキュメントを参照してください [パイプラインの管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### ローカル web アプリ開発用の Cloud Manager 資格情報を取得します。 {#retrieve-credentials}

SecurBank アプリを実行する前に、アプリを Cloud Manager に接続するために Cloud Manager 資格情報が必要です。

1. パイプラインを実行している間に、 **概要** cloud Manager でタブをクリックし、環境名の横にある省略記号ボタンをタップまたはクリックして、を選択します。 **Developer Console**.

1. 開発者コンソールで、 **統合** tab キーを押して、 **ローカルトークン** tab キーを押しながらタップまたはクリック **ローカル開発トークンを取得**.

1. アクセストークンを使用して JSON ファイルが生成されます。 開発者コンソールを閉じて Cloud Manager に戻る前に、トークン自体（残りの JSON は不要）のみを、今後の手順で使用するために安全な場所にコピーします。

1. Cloud Manager に戻り、次の操作を行います **概要** タブをクリックし、環境の URL を右クリックしてコピーし、今後の手順で使用するために安全な場所に保存します。

### SecurBank Web アプリをダウンロードして構成します。 {#download-web-app}

これで、SecurBank の Web アプリケーションをダウンロードして構成できます。

1. で GitHub から最新の SecurBank アプリコードを取得します。 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) クリックして **コード** その後 **ZIP をダウンロード** ドロップダウンで選択します。

1. ローカルファイルシステム上の zip ファイルの内容を解凍します。

1. 任意のコードエディターを起動し、SecurBank アプリプロジェクトの非表示環境ファイル（）を開きます。 `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. に次の変更を加えます。 `.env` ファイルを作成して変更を保存します。

   * の場合 `REACT_APP_HOST_URI` 以前にコピーした環境の URL の値を貼り付けます。
   * の場合 `REACT_APP_DEV_TOKEN` 以前にコピーしたローカル開発トークンの値を貼り付けます。

### SecurBank Web アプリを実行します。 {#run-web-app}

すべてが Cloud Manager とローカルの両方で設定されているので、SecurBank web アプリを実行できます。

1. ローカルマシンのコマンドラインで、に移動します。 `react-app` ダウンロードして解凍した SecurBank アプリプロジェクトのフォルダー。

1. あなたの `react-app` フォルダーと SecurBank アプリをインストールします `node -i` コマンド。

1. インストールが完了したら、次のコマンドを使用して SecurBank アプリを起動します `npm start` コマンド。

1. インストールと開始が成功した場合は、次のように表示されます。

* 次に、ターミナルでの出力を示します。

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * URL へのブラウザーウィンドウが開きます `https://localhost:3000`.

      * これは開発目的なので、有効な証明書は提供されません。 そのため、ページにアクセスできるようにブラウザーに通知する必要がある場合があります。

これで完了です。これで、ブラウザで SecurBank アプリが正常に実行されていることがわかります。

コンテンツがまだ表示されない場合は、 **開発環境にデプロイ** 実行したパイプラインは正常に完了しました。

![ブラウザーでの SecurBank アプリ](assets/securbank.png)
