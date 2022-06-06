---
title: カスタムフォントを使用
description: カスタムフォントを使用
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '456'
ht-degree: 100%

---

# カスタムフォントを使用

**Cloud Service 通信のドキュメントはベータ版です**

Forms as a Cloud Service 通信を使用すると、XDP テンプレート、XDP ベースの PDF ドキュメント、または Acrobat フォーム（AcroForms）を XML データと組み合わせて PDF ドキュメントを生成できます。通信機能を使用すると、PDF ドキュメントや XDP ドキュメントの結合、並べ替えおよび拡張のほか、PDF ドキュメントに関する情報の取得もできます。

前述の操作に加えて、Cloud Service に含まれているフォントやカスタムフォント（組織の承認済みフォント）を使用して、生成された PDF ドキュメントをレンダリングすることができます。Cloud Service 開発プロジェクトを使用して、カスタムフォントを Cloud Service 環境に追加できます。

## PDF ドキュメントの動作

PDF ドキュメントに [フォントを埋め込む](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) ことができます。フォントを埋め込むと、PDF ドキュメントはすべてのプラットフォームで同じように表示されます（見えます）。一貫したルックアンドフィールを確保するために、埋め込みフォントが使用されます。フォントが埋め込まれていない場合、フォントのレンダリングは、Acrobat や Acrobat Reader などの PDF ビューアクライアントのレンダリング設定によって決まります。フォントがクライアントマシンで使用可能な場合、PDF は指定されたフォントを使用します。使用可能でない場合、PDF はデフォルトのフォールバックフォントでレンダリングされます。

## Forms as a Cloud Service 環境へのカスタムフォントの追加 {#custom-fonts-cloud-service}

カスタムフォントを Cloud Service 環境に追加するには：

1. [ローカル開発プロジェクト](setup-local-development-environment.md)をセットアップして開きます。任意の IDE を使用できます。
1. プロジェクトの最上位フォルダー構造で、カスタムフォントを保存するフォルダー（モジュール）を作成し、そのフォルダーにカスタムフォントを追加します。例：fonts/src/main/resources
   ![フォントフォルダー](assets/fonts.png)

1. 開発プロジェクトのフォントモジュールの pom.xml ファイルを開きます。
1. pom.xml ファイルに jar プラグインを追加します。

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


1. `<Font-Archive-Version>` マニフェストエントリを .pom ファイルに追加し、バージョンの値を 1 に設定します。

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

1. フォントフォルダーを pom ファイルにリストされている `<modules>` に追加します。次に例を示します。

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

   フォントフォルダーには、すべてのカスタムフォントが含まれています。

1. 更新されたコードをチェックインして [パイプラインを実行](/help/implementing/cloud-manager/deploy-code.md) し、フォントを Cloud Service 環境にデプロイします。

1. （オプション）コマンドプロンプトを開き、ローカルプロジェクトフォルダに移動して、次のコマンドを実行します。このコマンドは、フォントを関連情報と共に .jar ファイルにパッケージ化します。この .jar ファイルを使用して、 Forms Cloud Service のローカル開発環境にカスタムフォントを追加できます。

   ```shell
   mvn clean install
   ```

## ローカル Forms Cloud Service 開発環境へのカスタムフォントの追加 {#custom-fonts-cloud-service-sdk}

1. ローカル開発環境を開始します。
1. `<aem install directory>/crx-quickstart/install` フォルダーに移動します。
1. `<jar file contaning custom fonts and relevant deployment code>.jar` をインストールフォルダーに配置します。.jar ファイルがない場合は、[Forms as a Cloud Service 環境へのカスタムフォントの追加](#custom-fonts-cloud-service)の節で示されている手順を実行して、ファイルを生成します。
1. [Docker ベースの SDK 環境](setup-local-development-environment.md#docker-microservices)を実行します。


   >[!NOTE]
   >
   >更新されたカスタムフォントの .jar ファイルをローカル開発環境にデプロイするたびに、Docker ベースの SDK 環境を再起動します。
