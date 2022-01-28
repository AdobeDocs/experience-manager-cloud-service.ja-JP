---
title: 'カスタムフォントを使用 '
description: 'カスタムフォントを使用 '
source-git-commit: f435751c9c4da8aa90ad0c6705476466bde33afc
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# カスタムフォントを使用

**Cloud Service通信のドキュメントはベータ版です**

Formsas a Cloud Serviceコミュニケーションを使用して、XDPPDF、XDP ベースのテンプレートドキュメント、またはAcrobatフォーム (AcroForms) を XML データと組み合わせてPDFドキュメントを生成できます。 生成されたフォントドキュメントをレンダリングするには、Cloud Serviceまたはカスタムフォント ( 組織の承認済みPDF) に含まれるフォントを使用できます。 Cloud Service開発プロジェクトを使用して、カスタムフォントをCloud Service環境に追加できます。

## PDF文書の動作

以下が可能です。 [フォントを埋め込む](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) をPDF文書に フォントが埋め込まれると、PDFドキュメントはすべてのプラットフォームで同じ (Look) で表示されます。 一貫した外観と操作性を確保するために、埋め込みフォントを使用しました。 フォントが埋め込まれていない場合、フォントのレンダリングは、PDFビューアクライアントのレンダリング設定に依存します。 フォントがクライアントマシンで使用可能な場合、PDFは指定されたフォントを使用します。使用しない場合、PDFはフォールバックフォントでレンダリングされます。

## Formsas a Cloud Service環境へのカスタムフォントの追加 {#custom-fonts-cloud-service}

カスタムフォントをCloud Service環境に追加するには：

1. を設定して、 [ローカル開発計画](setup-local-development-environment.md). 任意の IDE を使用できます。
1. プロジェクトの最上位フォルダー構造で、カスタムフォントを保存するフォルダーを作成し、そのフォルダーにカスタムフォントを追加します。 例： fonts/src/main/resources
   ![フォントフォルダー](assets/fonts.png)

1. 開発プロジェクトの最上位 pom.xml ファイルを開きます。
1. 追加 `<Font-Archive-Version>` .pom ファイルのマニフェストエントリを次のように指定し、バージョンの値を 1 に設定します。

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
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

1. 更新されたコードを確認し、 [パイプラインを実行](/help/implementing/cloud-manager/deploy-code.md) フォントを環境にデプロイする場合は、Cloud Serviceを使用します。

1. コマンドプロンプトを開き、ローカルプロジェクトフォルダに移動して、次のコマンドを実行します。 フォントを.jar ファイルにパッケージ化します。 プロジェクトのローカルデプロイメントには.jar ファイルを使用できます。

```shell
mvn clean install
```

## ローカルのFormsCloud Service開発環境へのカスタムフォントの追加 {#custom-fonts-cloud-service-sdk}

1. ローカル開発環境を開始します。
1. に移動します。 [crx-repository]\install フォルダ
1. カスタムフォントと関連するデプロイメントコードを含む.jar ファイルを install フォルダーに配置します。 .jar ファイルがない場合は、 [Formsas a Cloud Service環境へのカスタムフォントの追加](#custom-fonts-cloud-service) セクションを開いて、ファイルを生成します。
1. を実行します。 [Docker ベースの SDK 環境](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >更新された.jar ファイルをデプロイして、ローカルデプロイメント環境にカスタムフォントを追加または削除する場合は、Docker ベースの SDK 環境を停止し、起動します。