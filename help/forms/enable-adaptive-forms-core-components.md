---
title: AEM Formsのas a Cloud Serviceおよびローカル開発環境でアダプティブFormsコアコンポーネントを有効にする方法
description: AEM Forms as a Cloud ServiceでアダプティブFormsコアコンポーネントを有効にする方法を説明します。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 61%

---

# アダプティブFormsコアコンポーネントの有効化 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

AEM Formsas a Cloud ServiceのアダプティブFormsコアコンポーネントを有効にすると、AEM FormsCloud Serviceインスタンスを使用して、複数のチャネルに対して、アダプティブFormsおよびヘッドレスFormsベースのコアコンポーネントの作成、公開、配信を開始できます。 ヘッドレスアダプティブフォームを使用するには、アダプティブフォームコアコンポーネントを有効にした環境が必要です。

## 検討事項

* 新しいAEM Formsas a Cloud Serviceプログラムを作成する場合、 [アダプティブFormsコアコンポーネントとヘッドレスアダプティブFormsは、お使いの環境で既に有効になっています](#are-adaptive-forms-core-components-enabled-for-my-environment).

* 古い Forms as a Cloud Service プログラム（コアコンポーネントが[有効になっていない](#enable-components)）がある場合は、[アダプティブフォームコアコンポーネントの依存関係を追加](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment)し、そのリポジトリを Cloud Service 環境にデプロイしてヘッドレスアダプティブフォームを有効にすることができます。

* 既存のCloud Service環境で [コアコンポーネントベースのアダプティブFormsの作成](creating-adaptive-form-core-components.md)、アダプティブFormsコアコンポーネントとヘッドレスアダプティブFormsは、お使いの環境で既に有効になっており、コアコンポーネントベースのアダプティブFormsを、Adaptive Formsのヘッドレス表現を必要とするモバイル、Web、ネイティブアプリ、サービスなどのチャネルにヘッドレスフォームとして提供できます。


## アダプティブFormsコアコンポーネントとヘッドレスアダプティブFormsの有効化 {#enable-headless-forms}

AEM Formsas a Cloud Service環境でアダプティブFormsコアコンポーネントとヘッドレスアダプティブFormsを有効にするには、次の手順を上の順に実行します


![コアコンポーネントとヘッドレスアダプティブフォームの有効化](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. AEM Forms as a Cloud Service Git リポジトリを複製する {#clone-git-repository}

1. [Cloud Manager](https://my.cloudmanager.adobe.com/) にログインし、組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**リポジトリ情報にアクセス**」ボタンをクリックして、Git リポジトリにアクセスして管理します。このページには以下の情報が含まれます。

   * Cloud Manager Git リポジトリへの URL。
   * Git リポジトリの資格情報（ユーザー名とパスワード）Git ユーザー名。

   「**パスワードを生成**」をクリックして、パスワードを表示または生成します。

1. ローカルコンピューターでターミナルまたはコマンドプロンプトを開いて、次のコマンドを実行します。

   ```Shell
   git clone [Git Repository URL]
   ```

   プロンプトが表示されたら、資格情報を入力します。リポジトリがローカルコンピューターに複製されます。


## 2. Git リポジトリにアダプティブフォームコアコンポーネントの依存関係を追加する {#add-adaptive-forms-core-components-dependencies}

1. プレーンテキストコードエディターで Git リポジトリフォルダーを開きます。例：VS Code
1. `[AEM Repository Folder]\pom.xml` ファイルを編集用に開きます。
1. `core.forms.components.version`、`core.forms.components.af.version` および `core.wcm.components.version` のコンポーネントのバージョンを、[コアコンポーネントのドキュメント](https://github.com/adobe/aem-core-forms-components)で指定されているバージョンに置き換えます。コンポーネントが存在しない場合は、これらのコンポーネントを追加します。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![フォームのコアコンポーネントの最新バージョンについて言及](/help/forms/assets/latest-forms-component-version.png)

1. `[AEM Repository Folder]\pom.xml` ファイルの依存関係セクションに次の依存関係を追加し、ファイルを保存します。

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. `[AEM Repository Folder]/all/pom.xml` ファイルを編集用として開きます。次の依存関係を `<embeddeds>` セクションに追加し、ファイルを保存します。

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  `${appId}` を appId に置き換えます。
   >
   >  `${appId}` を見つけるには、`[AEM Repository Folder]/all/pom.xml` ファイル内で `-packages/application/install` を検索します。`-packages/application/install` の前のテキストが `${appId}` です。例えば、次のコードは `myheadlessform` が `${appId}` です。
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. `[AEM Repository Folder]/all/pom.xml` ファイルの `<dependencies>` セクションに、次の依存関係を追加し、ファイルを保存します。

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. `[AEM Repository Folder]/ui.apps/pom.xml` を開いて編集します。`af-core bundle` 依存関係を追加し、ファイルを保存します。

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >次のアダプティブフォームのコアコンポーネントアーティファクトがプロジェクトに含まれていないことを確認します。
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > および
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. ファイルを保存して閉じます。

## 3.更新したコードをビルドしてデプロイする

更新したコードをローカル開発環境とCloud Service環境にデプロイして、両方の環境でコアコンポーネントを有効にします。

* [更新されたコードをビルドし、ローカル開発環境にデプロイする (AEMas a Cloud ServiceSDK)](#core-components-on-aem-forms-local-sdk)

* [更新されたコードをビルドし、AEM Forms as a Cloud Service環境にデプロイする](#core-components-on-aem-forms-cs)

### 更新されたコードをビルドし、ローカル開発環境にデプロイする {#core-components-on-aem-forms-local-sdk}

1. コマンドプロンプトまたはターミナルを開きます。

1. Git リポジトリープロジェクトのルートディレクトリに移動します。

1. 次のコマンドを実行して、環境用のパッケージをビルドします。

   ```Shell
       mvn clean install
   ```



   パッケージが正常にビルドされたら、次の場所で見つけることができます。 [Git リポジトリフォルダー]\all\target\[appid].all-[version].zip

1. 以下を使用します。 [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja) をデプロイするには [AEM Archetype プロジェクトフォルダー]\all\target\[appid].all-[version]ローカル開発環境の.zip パッケージ。


### 更新されたコードをビルドし、AEM Forms as a Cloud Service環境にデプロイする {#core-components-on-aem-forms-cs}

1. ターミナルまたはコマンドプロンプトを開きます。
1. `[AEM Repository Folder]` に移動し、次のコマンドを順番に実行します。

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. ファイルが Git リポジトリにコミットされた後、[パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja)します。

   パイプラインが正常に実行されると、対応する環境でアダプティブフォームのコアコンポーネントが有効になります。また、アダプティブフォーム（コアコンポーネント）テンプレートと Canvas 3.0 テーマが、Forms as a Cloud Service 環境に追加され、コアコンポーネントベースのアダプティブフォームをカスタマイズして作成するオプションが提供されます。


## よくある質問 {#faq}

### コアコンポーネントとは何ですか？ {#core-components}

[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)は、AEM で web サイトの開発時間を短縮しメンテナンスコストを削減するための、標準化された web コンテンツ管理（WCM）コンポーネントのセットです。

### コアコンポーネントを有効にすると追加される機能は？ {#core-components-capabilities}

お使いの環境でアダプティブフォームのコアコンポーネントを有効にすると、空白のコアコンポーネントベースのアダプティブフォームテンプレートと Canvas 3.0 テーマが環境に追加されます。お使いの環境でアダプティブフォームのコアコンポーネントを有効にすると、次の操作を実行できます。

* [コアコンポーネントベースのアダプティブFormsを作成する](/help/forms/creating-adaptive-form-core-components.md).
* [コアコンポーネントベースのアダプティブフォームテンプレートを作成する](/help/forms/template-editor.md).
* [コアコンポーネントベースのアダプティブフォームテンプレート用のカスタムテーマを作成する](/help/forms/using-themes-in-core-components.md).
* [コアコンポーネントベースのアダプティブフォームの JSON 表現を、フォームのヘッドレス表現を必要とするモバイル、Web、ネイティブアプリ、サービスなどのチャネルに提供する](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp).

### アダプティブフォームのコアコンポーネントは、自分の環境で有効になっていますか？ {#enable-components}

お使いの環境でアダプティブフォームのコアコンポーネントが有効になっていることを確認するには、次の操作を行います。

1. [AEM Forms as a Cloud Service リポジトリを複製します](#1-clone-your-aem-forms-as-a-cloud-service-git-repository)。

1. AEM Forms Cloud Service Git リポジトリの `[AEM Repository Folder]/all/pom.xml` ファイルを開きます。

1. 次の依存関係を検索します。

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![all/pom.xml で core-forms-components-af-core アーティファクトを見つける](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   依存関係が存在する場合、お使いの環境でアダプティブフォームのコアコンポーネントが有効になります。
