---
title: DocuSign をアダプティブフォームに統合する方法
description: アダプティブフォームで DocuSign を使用して電子サインを収集する方法を説明します。
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 99%

---

# アダプティブフォームでの DocuSign の使用 {#integrate-aem-forms-with-DocuSign}

DocuSign は優れた電子サインソリューションです。契約の電子サインに使用できます。DocuSign をアダプティブフォームと統合することができます。電子サイン用のアダプティブフォームを複数の受信者に送信する場合に役立ちます。電子サインを使用すると、次のことができます。

- 完全に自動化された提案プロセス、見積りプロセス、契約プロセスを使用して、任意のデバイスで契約を締結する。
- 人事プロセスを短時間で完了し、従業員に対してデジタルエクスペリエンスを提供する。
- 契約のサイクルタイムを短縮し、ベンダーとの取引を早期に開始する。

AEM Forms as a Cloud Service には [DocuSign 用のカスタム送信アクション](#deploy-custom-submit-action)が用意されています。この送信アクションは、DocuSign API を使用して電子サイン用のアダプティブフォームを送信する場合に役立ちます。

| また、アドビの電子サインソリューションである Adobe Sign を使用して、アダプティブフォームに電子サインを行うこともできます。AEM Forms は、Adobe Sign とはるかに深く統合されており、連続署と並列署名、複数の認証方法、フォーム内署名機能など、一段ときめ細かい制御が可能です。詳しくは、[アダプティブフォームでの Adobe Sign の使用](working-with-adobe-sign.md)を参照してください。 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 前提条件 {#prerequisites}

DocuSign を AEM Forms と統合するには、以下が必要です。

- DocuSign の[開発者アカウント](https://developers.docusign.com/platform/account/)
- DocuSign アプリケーション
- DocuSign API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）
- [DocuSign 用のカスタム送信アクションと Cloud Service](https://github.com/adobe/aem-forms-docusign-sample)
- （ローカル開発環境のみ）[レコードのドキュメントのセットアップ](setup-local-development-environment.md#docker-microservices)

## DocuSign 用のカスタム送信アクションと Cloud Service の設定 {#deploy-custom-submit-action}

AEM Forms as a Cloud Service には DocuSign 用のカスタム送信アクションが用意されています。この送信アクションは、DocuSign API を使用して電子サイン用のアダプティブフォームを送信する場合に役立ちます。カスタム送信アクションのコードは、[AEM Forms サンプルの公開 Git リポジトリ](https://github.com/adobe/aem-forms-docusign-sample)で入手可能です。このコードは、AEM Forms 環境にそのままデプロイすることもできますし、組織の要件に従ってカスタマイズすることもできます。

標準のカスタム送信アクションと DocuSign Cloud Service を設定するには、次の手順を実行します。

1. [AEM Forms as a Cloud Service プロジェクトのクローンを作成](setup-local-development-environment.md#forms-cloud-service-local-development-environment) するか、[AEM アーキタイプ 27](https://github.com/adobe/aem-project-archetype) 以降に基づいて [!DNL Experience Manager Forms] as a [!DNL Cloud Service] プロジェクトを作成します。AEM アーキタイプに基づいて [!DNL Experience Manager Forms] as a [!DNL Cloud Service] プロジェクトを作成するには：
   </br>コマンドプロンプトを開き、以下のコマンドを実行して [!DNL Experience Manager Forms] as a Cloud Service プロジェクトを作成します。

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   また、上記のコマンドで `appTitle`、`appId`、`groupId` を変更し、環境に反映します。

1. [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) リポジトリのクローンを作成します。このリポジトリには、DocuSign 用のカスタム送信アクションと、DocuSign サーバーに接続するための設定の詳細が含まれています。

1. 手順 1 で作成した AEM Forms as a Cloud Service プロジェクトを任意の IDE で編集用に開きます。

1. `[AEM Forms as a Cloud Service project]\pom.xml` ファイルを編集用に開き、以下の変更を行います。

   1. `<properties>` タグの末尾に次のテキストを追加します。

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. `<repositories>` タグの末尾に次のテキストを追加します。

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      `<repositories>` タグがない場合は、`<properties>` タグの下に作成します。

   1. `<dependencyManagement>` タグの末尾に次のテキストを追加します。

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Cloud Service プロジェクトフォルダーにある `all/pom.xml` ファイルで次の手順を実行します。

   1. `<embeddeds>` タグの末尾に次のテキストを追加します。

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. `<dependencies>` タグの末尾に次のテキストを追加します。

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. コマンドプロンプトを開き、`aem-forms-samples\forms-integration-docusign`（手順 3 で作成したクローン）に移動して、次のコマンドを実行します。

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` は、上記の手順 1 で作成したフォルダーの名前を指します。

1. プロジェクトをローカル開発環境にデプロイします。以下のコマンドを使用して、ローカル開発環境にデプロイできます

   `mvn -PautoInstallPackage clean install`

   これらの手順を実行すると、アダプティブフォームの送信オプションのリストと、ローカル開発環境の [DocuSign Cloud Service 設定](#configure-docusign-with-aem-forms)に [DocuSign 電子サインを使用して送信](#enabledocusign)という新しいカスタム送信アクションが表示されます。

1. コードをコンパイルして[ [!DNL AEM Forms] as a Cloud Service 環境にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#customer-releases)します。

## [!DNL DocuSign] と [!DNL AEM Forms] の統合 {#configure-docusign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順に従って、オーサーインスタンス上で [!DNL DocuSign] と [!DNL AEM Forms] を統合します。

1. **[!UICONTROL ツール]** （![ハンマーアイコン](assets/hammer.png)）／**[!UICONTROL クラウドサービス]**／**[!UICONTROL DocuSign]** に移動し、設定をホストするフォルダーを選択します。

1. 設定ページで「**[!UICONTROL 作成]**」を選択して、AEM Forms 内に [!DNL DocuSign] の設定を作成します。
1. **[!UICONTROL DocuSign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」を選択します。オプションで、「**[!UICONTROL タイトル]**」も指定できます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。この URL は、後の手順で [!DNL AEM Forms] と [!DNL DocuSign] アプリケーションを設定する際に必要です。

1. 以下の手順に従って、[!DNL DocuSign] アプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、[!DNL DocuSign] [開発者アカウント](https://admindemo.docusign.com/apps-and-keys)にログインします。
   1. [!DNL AEM Forms] 用に設定したアプリを開きます。
   1. 上記の手順でコピーした URL を「**[!UICONTROL リダイレクト URL]**」ボックスに追加して、「**[!UICONTROL 保存]**」をクリックします。
   1. 統合キーと秘密鍵をメモしておきます。

   [!DNL DocuSign] アプリケーションの OAuth 設定を指定しキーを取得するための手順について詳しくは、 [アプリケーションの OAuth 設定の指定方法](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) に関する開発者ドキュメントを参照してください。

1. **[!UICONTROL DocuSign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。

   `https://account-d.docusign.com/oauth/auth`

1. 「**[!UICONTROL クライアント ID]**」（DocuSign 統合キー）と「**[!UICONTROL クライアントの秘密鍵]**」（DocuSign 秘密鍵）を指定します。

1. 「**[!UICONTROL DocuSign に接続]**」を選択します。資格情報の入力画面が表示されたら、[!DNL DocuSign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。`your developer account` へのアクセスを確認するメッセージが表示されたら、「**[!UICONTROL アクセスを許可]**」をクリックします。資格情報が正しい場合は、成功メッセージが表示されます。

1. 「**[!UICONTROL 作成]**」を選択して、[!DNL DocuSign] 設定を作成します。

1. 設定を選択し、「**[!UICONTROL 公開]**」をクリックします&#x200B;**[!UICONTROL 。]**&#x200B;これにより、対応するパブリッシュ環境に設定が複製されます。

1. 開発者、ステージ、実稼働用のインスタンス（残っているいずれか）で上記の手順をすべて繰り返し、お使いの環境用に [!DNL DocuSign] を [!DNL AEM Forms] で設定する作業を完了します。

これで、DocuSign を使用するように AEM Forms 環境が設定されました。[!DNL DocuSign] 用に有効化するすべてのアダプティブフォームに、Cloud Service に使用する設定コンテナを追加してください。設定コンテナは、アダプティブフォームのプロパティから指定できます。

### アダプティブフォームでの [!DNL DocuSign] の使用 {#enabledocusign}

既存のアダプティブフォーム用に [!DNL DocuSign] を有効にするか、[!DNL DocuSign] 対応アダプティブフォームを作成できます。次のいずれかの操作を行います。

- [ [!DNL DocuSign]  対応のアダプティブフォームを作成する](#create-an-adaptive-form-for-docusign)
- [既存のアダプティブフォームで [!DNL DocuSign] を有効にする](#editafsign)

#### DocuSign 対応のアダプティブフォームの作成 {#create-an-adaptive-form-for-docusign}

署名が有効なアダプティブフォームを作成するには：

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**[!UICONTROL 作成]**」を選択して、「**[!UICONTROL アダプティブフォーム]**」をクリックします。テンプレートのリストが表示されます。テンプレートを選択して、「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 基本]**」タブで次の操作を行います。

   1. アダプティブフォームの&#x200B;**[!UICONTROL 名前]**&#x200B;と&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   1. [ [!DNL DocuSign]  を  [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) と統合するときに作成した [設定コンテナ](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) を選択します。

   設定コンテナには、お使いの環境用に設定された [!DNL DocuSign] クラウドサービスが含まれています。これらのサービスは、アダプティブフォームエディターで選択できます。

1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   - カスタムフォームテンプレートがあり、そのフォームテンプレートに基づいてレコードのドキュメントが必要な場合は、「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメントテンプレート」を選択します。このオプションを使用すると、署名用に送信されたドキュメントには、関連付けられたフォームテンプレートに基づくフィールドのみが表示されます。アダプティブフォームのすべてのフィールドは表示されません。

   - カスタムフォームテンプレートがない場合は、「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。このオプションを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 作成]**」を選択します。 署名付きのアダプティブフォームが作成されます。 [!DNL DocuSign] フィールドをフォームに追加し、署名用に送信できます。
1. アダプティブフォームを編集モードで開きます。「**[!UICONTROL コンテンツ]**」タブで「**[!UICONTROL フォームコンテナ]**」を選択し、「![設定](assets/configure-icon.svg)」をクリックします。

1. 「**[!UICONTROL 送信]**」セクションの「**[!UICONTROL 送信アクション]**」ドロップダウンリストで、「**[!UICONTROL DocuSign 電子サインを使用して送信]**」を選択します。

1. 「**[!UICONTROL アクション設定]**」セクションで「**[!UICONTROL 追加]**」を選択して受信者を追加し、その受信者のメールアドレスを指定します。「**[!UICONTROL 追加]**」を再度選択して、受信者をさらに追加します。

1. メールメッセージの件名を「**[!UICONTROL メールの件名]**」フィールドに指定します。メールメッセージに添付ファイルを含める場合は、「**添付ファイルを含める**」を選択します。

1. 「![保存](assets/save_icon.svg)」を選択して、プロパティを保存します。

#### アダプティブフォームでの [!DNL DocuSign] の有効化 {#editafsign}

既存のアダプティブフォームで [!DNL DocuSign] を使用するには：

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL 基本]**」タブで、[!DNL DocuSign] を [!DNL AEM Forms] と統合するときに作成した [設定コンテナ](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) を選択します。
1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   - カスタムフォームテンプレートがあり、そのフォームテンプレートに基づいてレコードのドキュメントが必要な場合は、「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメントテンプレート」を選択します。このオプションを使用すると、署名用に送信されたドキュメントには、関連付けられたフォームテンプレートに基づくフィールドのみが表示されます。アダプティブフォームのすべてのフィールドは表示されません。

   - カスタムフォームテンプレートがない場合は、「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。このオプションを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 保存して閉じる]**」を選択します。アダプティブフォームは [!DNL DocuSign] に対して有効になっています。これで、[!DNL DocuSign] フィールドをフォームに追加し、署名用に送信できます。

1. アダプティブフォームを編集モードで開きます。「**[!UICONTROL コンテンツ]**」タブで「**[!UICONTROL フォームコンテナ]**」を選択し、「![設定](assets/configure-icon.svg)」をクリックします。

1. 「**[!UICONTROL 送信]**」セクションの「**[!UICONTROL 送信アクション]**」ドロップダウンリストで、「**[!UICONTROL DocuSign 電子サインを使用して送信]**」を選択します。

1. 「**[!UICONTROL アクション設定]**」セクションで「**[!UICONTROL 追加]**」を選択して受信者を追加し、その受信者のメールアドレスを指定します。「**[!UICONTROL 追加]**」を再度選択して、受信者をさらに追加します。

1. メールメッセージの件名を「**[!UICONTROL メールの件名]**」フィールドに指定します。メールメッセージに添付ファイルを含める場合は、「**添付ファイルを含める**」を選択します。

1. 「![保存](assets/save_icon.svg)」を選択して、プロパティを保存します。
