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

* SecurBank アプリをインストールするには、**AEM管理者** [ 製品プロファイル ](/help/journey-onboarding/assign-profiles-aem.md) に割り当てられている必要があります。
* ローカル開発するには、[Node.js](https://nodejs.org) バージョン 20 以降がインストールされている必要があります。

## SecurBank のインストール {#installation}

SecurBank アプリのインストールは簡単ですが、AEM as a Cloud Serviceの多くの領域に影響を与えるため、いくつかの手順が必要になります。 主な手順の概要を次に示します。

1. [Cloud Managerでサンドボックスプログラムを作成します。](#create-sandbox-program)
1. [プログラムの Git リポジトリを複製し、SecurBank AEM プロジェクトのコンテンツを使用して更新します。](#clone-and-update)
1. [パイプラインを実行して SecurBank AEM プロジェクトをデプロイします。](#run-pipeline)
1. [ローカル web アプリ開発用のCloud Manager資格情報を取得します。](#retrieve-credentials)
1. [SecurBank Web アプリをダウンロードして構成します。](#download-web-app)
1. [SecurBank Web アプリを実行します。](#run-web-app)

次のセクションでは、必要な個々のタスクについて詳しく説明します。

### Cloud Managerでサンドボックスプログラムを作成します。 {#create-sandbox-program}

SecurBank をインストールできる新しいCloud Managerプログラムが必要になります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. SecurBank アプリ用の新しいサンドボックスプログラムを作成します。

   * **ソリューションとアドオン** を選択する場合は、デフォルトのオプションを使用します。
   * サンドボックスプログラムの作成方法について詳しくは、ドキュメント [ サンドボックスプログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) を参照してください。

### プログラムの Git リポジトリを複製し、SecurBank AEM プロジェクトのコンテンツを使用して更新します。 {#clone-and-update}

1. プログラムを作成したら開き、「**リポジトリ**」タブで「**リポジトリ情報にアクセス**」ボタンをタップまたはクリックして **リポジトリ情報** ダイアログを開き、サンドボックス環境の Git リポジトリへのアクセスに必要な資格情報を表示します。

   * リポジトリ情報へのアクセス方法について詳しくは、[ リポジトリへのアクセス ](/help/implementing/cloud-manager/managing-code/accessing-repos.md) のドキュメントを参照してください。

1. **リポジトリ情報** ダイアログの資格情報を使用して、ローカルマシンにリポジトリのクローンを作成します。

1. ローカルクローンのフォルダーを探して開き、hidden/dot ファイルを除くすべてのコンテンツを削除します。

1. [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) の GitHub から、最新の SecurBank AEM プロジェクトコードを取得します。**コード** をクリックし、ドロップダウンで **ZIP をダウンロード** します。

1. ローカルファイルシステム上の zip ファイルの内容を解凍し、サンドボックスプログラムのローカルクローンの空になったフォルダーに移動します。

1. ターミナルを使用して、複製されたプロジェクトのフォルダーに切り替え、すべてのコンテンツをコミットして Git にプッシュします。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### パイプラインを実行して SecurBank AEM プロジェクトをデプロイします。 {#run-pipeline}

SecurBank のAEM プロジェクトをサンドボックスリポジトリにコミットした状態で、パイプラインを使用してデプロイできます。

1. Cloud Managerのサンドボックスプログラムの「**概要**」タブに戻り、フルスタックの実稼動以外のパイプラインを実行します。

   * パイプライン実行のすべてのオプションをオフにします。
   * パイプラインの実行について詳しくは、[ パイプラインの管理 ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) のドキュメントを参照してください。

### ローカル web アプリ開発用のCloud Manager資格情報を取得します。 {#retrieve-credentials}

SecurBank アプリを実行する前に、アプリをCloud Managerに接続するためにCloud Manager資格情報が必要です。

1. パイプラインを実行中に、Cloud Managerの「**概要**」タブに戻り、環境名の横にある省略記号ボタンをタップまたはクリックして、「**Developer Console**」を選択します。

1. Developer Consoleで、「**統合**」タブを選択し、「**ローカルトークン**」タブを選択して、「**ローカル開発トークンの取得**」をタップまたはクリックします。

1. アクセストークンを使用して JSON ファイルが生成されます。 Developer Consoleを閉じてCloud Managerに戻る前に、トークン自体（残りの JSON は不要）のみを、今後の手順で使用するために安全な場所にコピーします。

1. Cloud Managerに戻り、「**概要**」タブで環境の URL を右クリックしてコピーし、今後の手順で使用するために安全な場所に保存します。

### SecurBank Web アプリをダウンロードして構成します。 {#download-web-app}

これで、SecurBank の Web アプリケーションをダウンロードして構成できます。

1. [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) の GitHub から最新の SecurBank アプリコードを取得するには、ドロップダウンで「**コード**」をクリックし、「**ZIP をダウンロード**」をクリックします。

1. ローカルファイルシステム上の zip ファイルの内容を解凍します。

1. 任意のコードエディターを起動し、SecurBank アプリプロジェクト内の非表示の環境ファイル（`summit-2024-l425-ue-z-final-with-events/react-app/.env`）を開きます。

1. `.env` ファイルに次の変更を加え、変更内容を保存します。

   * `REACT_APP_HOST_URI`：以前にコピーした環境の URL の値を貼り付けます。
   * `REACT_APP_DEV_TOKEN`：以前にコピーしたローカル開発トークンの値をペーストします。

### SecurBank Web アプリを実行します。 {#run-web-app}

すべてがCloud Managerとローカルの両方で設定されているので、SecurBank web アプリを実行できます。

1. ローカルマシンのコマンドラインで、ダウンロードして解凍した SecurBank アプリプロジェクトの `react-app` フォルダーに移動します。

1. `react-app` フォルダーに、`node -i` コマンドを使用して SecurBank アプリをインストールします。

1. インストールが完了したら、`npm start` のコマンドを使用して SecurBank アプリを起動します。

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

   * ブラウザーウィンドウが開き、URL `https://localhost:3000` が表示されます。

      * これは開発目的なので、有効な証明書は提供されません。 そのため、ページにアクセスできるようにブラウザーに通知する必要がある場合があります。

これで完了です。これで、ブラウザで SecurBank アプリが正常に実行されていることがわかります。

コンテンツがまだ表示されない場合は、実行した **開発にデプロイ** パイプラインが正常に完了したことを確認します。

![ ブラウザーの SecurBank アプリ ](assets/securbank.png)
