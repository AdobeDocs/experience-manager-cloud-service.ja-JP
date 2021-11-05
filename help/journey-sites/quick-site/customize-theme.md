---
title: サイトテーマのカスタマイズ
description: サイトテーマの構築方法、カスタマイズ方法、およびAEMのライブコンテンツを使用したテスト方法について説明します。
source-git-commit: 348e26a9af260d89841d19d00ce4102c00ae34ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---


# サイトテーマのカスタマイズ {#customize-the-site-theme}

サイトテーマの構築方法、カスタマイズ方法、およびAEMのライブコンテンツを使用したテスト方法について説明します。

>[!CAUTION]
>
>現在、クイックサイト作成ツールはテクニカルプレビューです。 テストおよび評価の目的で使用できるようになり、Adobeサポートに同意しない限り、実稼動での使用は意図されません。

## これまでの説明内容 {#story-so-far}

前のドキュメントのAEM Quick Site Creation ジャーニーでは、 [Git リポジトリのアクセス情報の取得](retrieve-access.md) フロントエンド開発者ユーザー Cloud Manager が git リポジトリ情報にアクセスする方法を学びました。次の手順を実行する必要があります。

* Cloud Manager の概要を説明します。
* カスタマイズをコミットできるよう、AEM Git にアクセスするための資格情報を取得しました。

ジャーニーのこの部分では、次の手順に進み、サイトテーマを掘り下げ、そのテーマをカスタマイズし、取得したアクセス資格情報を使用してそれらのカスタマイズをコミットする方法を示します。

## 目的 {#objective}

このドキュメントでは、AEMサイトのテーマの構築方法、テーマのカスタマイズ方法、およびライブAEMのコンテンツを使用したテスト方法について説明します。 ドキュメントを読めば、以下が可能です。

* サイトテーマの基本構造と編集方法を理解します。
* ローカルプロキシを介した実際のAEMコンテンツを使用したテーマのカスタマイズのテスト方法を参照してください。
* 変更をAEM Git リポジトリにコミットする方法を説明します。

## 担当ロール {#responsible-role}

このジャーニーの部分は、フロントエンド開発者に適用されます。

## テーマの構造について {#understand-theme}

AEM管理者が提供するテーマをテーマの編集先に抽出し、目的のエディターで開きます。

![テーマの編集](assets/edit-theme.png)

テーマが一般的なフロントエンドプロジェクトであることがわかります。 構造の最も重要な部分は次のとおりです。

* `src/main.ts`:JS および CSS テーマの主なエントリポイント
* `src/site`:サイト全体に適用される JS および CSS ファイル
* `src/components`:AEMコンポーネント固有の JS および CSS ファイル
* `src/resources`:アイコン、ロゴ、フォントなどの静的ファイル

>[!TIP]
>
>標準のAEMサイトテーマの詳細については、 [その他のリソース](#additional-resources) 」セクションを開きます。

テーマプロジェクトの構造に慣れたら、ローカルプロキシを起動して、実際のAEMコンテンツに基づいて、テーマのカスタマイズをリアルタイムで確認できるようにします。

## ローカルプロキシの開始 {#starting-proxy}

1. コマンドラインから、ローカルマシン上のテーマのルートに移動します。
1. 実行 `npm install` および npm は依存関係を取得し、プロジェクトをインストールします。

   ![npm install](assets/npm-install.png)

1. 実行 `npm run live` プロキシサーバーが起動します。

   ![npm run live](assets/npm-run-live.png)

1. プロキシサーバーが起動すると、次の場所へのブラウザーが自動的に開きます。 `http://localhost:7001/`. タップまたはクリック **ローカルでログイン（管理者タスクのみ）** をクリックし、AEM管理者から提供されたプロキシユーザーの資格情報を使用してサインオンします。

   ![ローカルでサインイン](assets/sign-in-locally.png)

1. ログインしたら、AEM管理者が指定したサンプルコンテンツのパスを指すように、ブラウザーで URL を変更します。

   * 例えば、指定されたパスが `/content/<your-site>/en/home.html?wcmmode=disabled`
   * URL をに変更します。 `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![プロキシ化されたサンプルコンテンツ](assets/proxied-sample-content.png)

サイトに移動して、コンテンツを参照できます。 サイトがライブAEMインスタンスから取り出され、実際のコンテンツに対してテーマをカスタマイズできます。

## テーマのカスタマイズ {#customize-theme}

これで、テーマのカスタマイズを開始できます。 次に、プロキシ経由でライブに変更を表示する方法を示す簡単な例を示します。

1. エディターで、ファイルを開きます。 `<your-theme-sources>/src/site/_variables.scss`

   ![テーマを編集](assets/edit-theme.png)

1. 変数を編集します `$color-background` 白以外の値に設定します。 この例では、 `orange` が使用されます。

   ![編集されたテーマ](assets/edited-theme.png)

1. ファイルを保存すると、プロキシサーバーが行を介して変更を認識していることがわかります。 `[Browsersync] File event [change]`.

   ![プロキシブラウザー同期](assets/proxy-browsersync.png)

1. プロキシサーバーのブラウザーに切り替えると、変更が直ちに表示されます。

   ![オレンジのテーマ](assets/orange-theme.png)

AEM管理者から提供された要件に基づいて、テーマのカスタマイズを続行できます。

## 変更のコミット {#committing-changes}

カスタマイズが完了したら、それらをAEM Git リポジトリにコミットできます。 まず、リポジトリをローカルマシンに複製する必要があります。

1. コマンドラインから、リポジトリのクローン先に移動します。
1. コマンドを実行します。 [以前に Cloud Manager から取得されたもの。](retrieve-access.md) 次のようになります。 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`. 次の Git ユーザー名とパスワードを使用します。 [このジャーニーの前の部分で取得しました。](retrieve-access.md)

   ![リポジトリの複製](assets/clone-repo.png)

1. 編集中のテーマプロジェクトを、次のようなコマンドを使用して、クローンリポジトリに移動します。 `mv <site-theme-sources> <cloned-repo>`
1. クローンリポジトリのディレクトリで、先ほど移動したテーマファイルを次のコマンドでコミットします。

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. カスタマイズ内容はAEM Git リポジトリにプッシュされます。

   ![コミット済みの変更](assets/changes-committed.png)

これで、カスタマイズ内容がAEM Git リポジトリに安全に保存されました。

## 次の手順 {#what-is-next}

これで、AEM Quick Site Creation ジャーニーのこの部分が完了し、次の作業をおこなう必要があります。

* サイトテーマの基本構造と編集方法を理解します。
* ローカルプロキシを介した実際のAEMコンテンツを使用したテーマのカスタマイズのテスト方法を参照してください。
* 変更をAEM Git リポジトリにコミットする方法を説明します。

この知識に基づいてドキュメントを次に確認し、AEMクイックサイト作成のジャーニーを続行します [カスタマイズしたテーマのデプロイ](deploy-theme.md) フロントエンドパイプラインを使用したテーマのデプロイ方法を学ぶ場所です。

## その他のリソース {#additional-resources}

クイックサイト作成ジャーニーの次の部分に進むことをお勧めしますが、ドキュメントを確認してください [カスタマイズしたテーマのデプロイ](deploy-theme.md) 以下に、このドキュメントで取り上げたいくつかの概念について詳しく説明する、その他のオプションのリソースを示します。ただし、このジャーニーを続行する必要はありません。

* [AEM Site テーマ](https://github.com/adobe/aem-site-template-standard-theme-e2e)  — これはAEM Site Theme の GitHub リポジトリです。
* [npm](https://www.npmjs.com) - AEMテーマを使用してサイトをすばやく作成する場合は、npm に基づきます。
* [webpack](https://webpack.js.org) - AEMテーマは、webpack に依存するサイトをすばやく構築するために使用します。