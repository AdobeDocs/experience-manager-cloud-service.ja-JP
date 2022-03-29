---
title: '"[!DNL Adobe Experience Manager] as a Cloud Service プレリリースチャネル"'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service プレリリースチャネル"'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service プレリリースチャネル {#prerelease-channel}


## はじめに {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service では、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja#aem-as-cloud-service)のスケジュールに従って、毎月 1 回のペースで新しい機能を提供します。翌月に公開予定の機能を把握できるように、プレリリースチャネルを購読できます。プレリリースチャネルにアクセスするには、標準のプログラム開発環境または任意のサンドボックスプログラム環境で適切に設定します。ユーザーは、サイトコンソールの変更内容をプレビューできるほか、新しいプレリリース API に対応してコードをビルドできます。

特定月のプレリリース機能の一覧は、[月次リリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)に掲載されています。

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## プレリリースを有効にする方法 {#enable-prerelease}

プレリリース機能は、次のような異なる方法で使用できます。

* クラウド環境（標準プログラム開発環境または任意の種類のサンドボックスプログラム環境）
* ローカル SDK

### クラウド環境 {#cloud-environments}

クラウド開発環境でのサイトコンソールの新機能と、プロジェクトのカスタマイズの結果を確認するには：

* [Cloud Manager API の環境変数エンドポイント](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)を使用して、**AEM_RELEASE_CHANNEL** 環境変数を **prerelease** という値に設定します。

```
PATCH /program/{programId}/environment/{environmentId}/variables
[
        {
                "name" : "AEM_RELEASE_CHANNEL",
                "value" : "prerelease",
                "type" : "string"
        }
]
```

[https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) に記載の手順に従って、次のように、Cloud Manager CLI も使用できます。
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


環境を通常の（プレリリース以外の）チャネルの動作に戻す場合は、変数を削除するか、別の値に設定し直します。

* または、[Cloud Manager UI](/help/implementing/cloud-manager/environment-variables.md) から環境変数を設定することもできます。

### ローカル SDK {#local-sdk}

Maven Central にあるプレリリース `API Jar` を Maven プロジェクトで参照すると、ローカル Quickstart SDK のサイトコンソールの新機能とプレリリースの新しい API に対応するコードを確認できます。また、通常の Quickstart SDK をプレリリースモードで起動すると、ローカルコンピューター上でこれらのプレリリース機能を確認することもできます。

* SDK をソフトウェア配布ポータルからダウンロードし、[AEM as a Cloud Service SDK へのアクセス](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)の説明に従ってインストールします。
* SDK Quickstart を起動する際に、引数 `-r prerelease` を含めます。
* この値は、*sticky* なので最初の起動時にのみ選択できます。コマンドラインオプションを変更するには、SDK を再インストールします。

毎月の機能リリースの間に複数の AEM メンテナンスリリースが行われる可能性があるので、これらの新しい SDK をダウンロードし、Maven プロジェクトで新しい SDK API Jar バージョンを参照するいことができます。メンテナンスリリースには、追加のプレリリース機能はありませんが、バグ修正、セキュリティ修正、パフォーマンス強化などの小規模な変更が含まれる場合があります。
Javadoc は Maven Central に公開されます。

プレリリース SDK に対応してビルドするには：

1. Maven Central に公開される個別のプレリリース SDK API Jar を参照するように、Maven プロジェクトの pom.xml を変更します。このファイルには、プレリリース機能の新しい Java API が記載されており、SDK API Jar に対する依存関係が宣言されています。同じバージョンが使用されます。

   例えば、通常の API JAR を参照する親 POM の依存関係管理セクションから抜粋したコードを次に示します。

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   この場合、モジュールでの使用方法は次のようになります。

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   プレリリース SDK に変更するには、次に示すように、依存関係を `com.adobe.aem:aem-sdk-api` から `com.adobe.aem:aem-prerelease-sdk-api` に変更するだけです。

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   通常どおり、個々のプロジェクトでこの依存関係を使用できます。

1. ローカルサーバーにデプロイします。
1. ローカルで想定どおりに動作することを確認したら、コードを開発ブランチにコミットし、Cloud Manager の実稼動以外のパイプラインを使用して、プレリリースチャネルをサブスクライブする環境にデプロイします。

>[!CAUTION]
> 
> ステージングまたは実稼動環境にデプロイする場合は、`aem-prerelease-sdk-api` artifactId を使用しないでください。実稼動パイプラインを使用してデプロイする場合は、必ず aem-sdk-api を使用します。同様に、プレリリース API を参照するコードは、実稼動パイプラインを使用してデプロイしないでください。

[AEM CS SDK ビルドアナライザー Maven プラグイン v1.0 以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)では、依存関係を調べて、プレリリース API がプロジェクトで使用されているかどうかを検出します。アナライザーで検出された場合は、プレリリース SDK API を使用してプロジェクトの分析が行われます。

## 考慮事項 {#considerations}

プレリリースチャネルに関しては、次の点に注意してください。

* 翌月のリリースでロールアウトされる一部の機能は、プレリリースチャネルには含まれない場合があります。
* プレリリースの機能は厳しい品質保証検査を通り、ベータ版の品質ではなく完全な機能を実現することを目的としています。通常の AEM リリースの機能にバグがあると思われる場合と同様に、問題に気がついた場合は報告してください。
* 環境がプレリリースチャネル用に設定されているかどうかを確認するには、AEM コンソールの&#x200B;**バージョン情報**&#x200B;ページに移動し、AEM バージョン番号に *PRERELEASE* というサフィックスが含まれている（```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE``` など）かどうかを確認します。

![バージョン情報](/help/release-notes/assets/about.png)
