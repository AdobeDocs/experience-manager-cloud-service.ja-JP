---
title: 'カスタムフォントを使用 '
description: 'カスタムフォントを使用 '
source-git-commit: 94fe397d6ce08380ef08b65b47fe2c1aeb015ca3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# カスタムフォントを使用

**Cloud Service通信のドキュメントはベータ版です**

Formsas a Cloud Serviceコミュニケーションを使用して、XDPPDF、XDP ベースのテンプレートドキュメント、またはAcrobatフォーム (AcroForms) を XML データと組み合わせてPDFドキュメントを生成できます。 コミュニケーションを使用して、PDFドキュメントと XDP ドキュメントを組み合わせ、並べ替え、拡大し、PDFドキュメントに関する情報を取得することもできます。

前述の操作と共に、Cloud Serviceまたはカスタムフォント（組織の承認済みフォント）に含まれるフォントを使用して、生成されたPDFドキュメントをレンダリングできます。 Cloud Service開発プロジェクトを使用して、カスタムフォントをCloud Service環境に追加できます。

## PDF文書の動作

以下が可能です。 [フォントを埋め込む](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) をPDF文書に フォントが埋め込まれると、PDFドキュメントはすべてのプラットフォームで同じように表示されます（外観は同じ）。 埋め込みフォントを使用して、外観と操作性を一貫させます。 フォントが埋め込まれていない場合のフォントのレンダリングは、AcrobatやAcrobat ReaderなどのPDFビューアクライアントのレンダリング設定に依存します。 フォントがクライアントマシンで使用可能な場合、PDFは指定されたフォントを使用します。使用しない場合、PDFはデフォルトのフォールバックフォントでレンダリングされます。

## Formsas a Cloud Service環境へのカスタムフォントの追加 {#custom-fonts-cloud-service}

カスタムフォントをCloud Service環境に追加するには：

1. を設定して、 [ローカル開発計画](setup-local-development-environment.md). 任意の IDE を使用できます。
1. プロジェクトの最上位のフォルダー構造で、カスタムフォントを保存し、そのフォルダーにカスタムフォントを追加するフォルダー（モジュール）を作成します。 例： fonts/src/main/resources
   ![フォントフォルダー](assets/fonts.png)

1. 開発プロジェクトのフォントモジュールの pom.xml ファイルを開きます。
1. POM ファイルに jar プラグインを追加します。

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```


1. を `<Font-Archive-Version>` manifest エントリ.pom ファイルを開き、バージョンの値を 1 に設定します。

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. フォントフォルダーの追加先 `<modules>` pom ファイルに一覧表示されます。 次に例を示します。

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

   fonts フォルダーには、すべてのカスタムフォントが含まれています。

1. 更新されたコードを確認し、 [パイプラインを実行](/help/implementing/cloud-manager/deploy-code.md) フォントを環境にデプロイする場合は、Cloud Serviceを使用します。

1. （オプション）コマンドプロンプトを開き、ローカルプロジェクトフォルダに移動して、次のコマンドを実行します。 このコマンドは、フォントを関連情報と共に.jar ファイルにパッケージ化します。 .jar ファイルを使用して、FormsCloud Serviceローカル開発環境にカスタムフォントを追加できます。

   ```shell
   mvn clean install
   ```

## ローカルのFormsCloud Service開発環境へのカスタムフォントの追加 {#custom-fonts-cloud-service-sdk}

1. ローカル開発環境を開始します。
1. に移動します。 `<aem install directory>/crx-quickstart/install` フォルダー。
1. を `<jar file contaning custom fonts and relevant deployment code>.jar` を install フォルダーに追加します。 .jar ファイルがない場合は、 [Formsas a Cloud Service環境へのカスタムフォントの追加](#custom-fonts-cloud-service) セクションを開いて、ファイルを生成します。
1. を実行します。 [Docker ベースの SDK 環境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >更新されたカスタムフォント.jar ファイルをローカル開発環境にデプロイする際には、Docker ベースの SDK 環境を再起動します。