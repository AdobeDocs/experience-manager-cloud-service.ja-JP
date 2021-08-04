---
title: '[!DNL Adobe Experience Manager] (Cloud Serviceプレリリースチャネル)'
description: '[!DNL Adobe Experience Manager] (Cloud Serviceプレリリースチャネル)'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: bcd106a39bec286e2a09ac7709758728f76f9544
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] (Cloud Serviceプレリリースチャネル) {#prerelease-channel}


## はじめに {#introduction}

[!DNL Adobe Experience Manager] は、Cloud Serviceリリースロードマップのスケジュールに従って、月次サイクルで新しい機能を [Experience Managerに提供します](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service)。翌月に公開予定の機能を理解できるように、プレリリースチャネルを購読することができます。プレリリースチャネルには、標準のプログラム開発環境またはサンドボックスプログラム環境で適切に設定することでアクセスできます。 お客様は、サイトコンソールに対する変更をプレビューし、新しいプレリリースAPIに対するコードを構築できます。

特定の月のプレリリース機能のリストは、月別リリースノート[に掲載されています。](/help/release-notes/release-notes-cloud/release-notes-current.md)

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## プレリリースを有効にする方法 {#enable-prerelease}

プレリリース機能は、様々な方法で使用できます。

* クラウド環境（標準プログラム開発環境または任意のサンドボックスプログラム環境タイプ）
* ローカル SDK

### クラウド環境 {#cloud-environments}

クラウド開発環境のサイトコンソールの新機能と、プロジェクトのカスタマイズの結果を確認するには、次の手順を実行します。

* [Cloud Manager APIの環境変数エンドポイント](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)を使用して、**AEM_RELEASE_CHANNEL**&#x200B;環境変数を&#x200B;**prerelease**&#x200B;に設定します。

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

Cloud Manager CLIも、[https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)の手順に従って使用できます。
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


通常の（プレリリース以外の）チャネルの動作に環境を復元したい場合は、変数を削除するか、別の値に戻すことができます

### ローカル SDK {#local-sdk}

ローカルのクイックスタートSDKのSitesコンソールに新機能が表示され、Maven Centralにあるプレリリース`API Jar`をMavenプロジェクトで参照させると、プレリリースの新しいAPIに対するコードを確認できます。 また、プレリリースモードで通常のクイックスタートSDKを起動すると、ローカルコンピューター上でこれらのプレリリース機能を確認できます。

* ソフトウェア配布ポータルからSDKをダウンロードし、[Cloud ServiceSDKとしてのAEMへのアクセス](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)の説明に従ってインストールします。
* SDKクイックスタートを起動する際に、引数`-r prerelease`を含めます。
* 値は&#x200B;*sticky*&#x200B;なので、最初の起動時にのみ選択できます。 SDKを再インストールして、コマンドラインオプションを変更します。

毎月の機能リリースの間に複数のAEMメンテナンスリリースが存在する可能性があるので、これらの新しいSDKをダウンロードし、Mavenプロジェクトで新しいSDK API Jarバージョンを参照できます。 メンテナンスリリースには、プレリリース機能は追加されませんが、バグ修正、セキュリティ修正、パフォーマンス強化など、より小さな変更が含まれる場合があります。
JavadocはMaven Centralに公開されます。

プレリリースSDKに対してをビルドするには：

1. Maven Centralに公開される、個別のプレリリースsdk api jarを参照するようにmavenプロジェクトのpom.xmlを変更します。 プレリリース機能用の新しいJava apiが含まれ、sdk api jarに依存します。 同じバージョンを使用します。

   例えば、通常のAPI JARを参照する親POMの依存関係管理セクションのスニペットを次に示します。

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

   次に、モジュールでの使用方法を次に示します。

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   プレリリースSDKに変更するには、次に示すように、依存関係を`com.adobe.aem:aem-sdk-api`から`com.adobe.aem:aem-prerelease-sdk-api`に変更します。

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

   通常どおり、個々のプロジェクトで依存関係を使用できます。

1. ローカルサーバーにデプロイする
1. ローカルで正常に動作することを確認したら、コードを開発ブランチにコミットし、 Cloud Manager非実稼動パイプラインを使用して、プレリリースチャネルをサブスクライブする環境にデプロイします

>[!CAUTION]
`aem-prerelease-sdk-api` artifactIdは、ステージングまたは実稼動にデプロイする際には使用しないでください。 実稼動パイプラインを介してデプロイする場合は、必ずaem-sdk-apiを使用します。 同様に、プレリリースAPIを参照するコードは、実稼動パイプラインを介してデプロイしないでください。

[AEM CS SDK Build Analyzer maven plugin v1.0以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)は、依存関係を調べて、プレリリースapiがプロジェクトで使用されているかどうかを検出します。 アナライザーが検出した場合は、プレリリースsdk apiを使用してプロジェクトを分析します。

## 検討事項 {#considerations}

プレリリースチャネルに関しては、次の点に注意してください。

* 来月のリリースで展開される一部の機能は、プレリリースチャネルには含まれない場合があります。
* プレリリースの機能は厳しい品質保証を受け、ベータ版の品質ではなく機能を完全に実現することを目的としています。 通常のAEMリリースの機能にバグがあると思われる場合と同様に、問題が見つかった場合は報告します。
* プレリリースチャネル用に環境が設定されているかどうかを確認するには、AEMコンソールの「**About**」ページに移動し、AEMバージョン番号に&#x200B;*prerelease*&#x200B;サフィックス（```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```など）が含まれているかどうかを確認します。

![概要](/help/release-notes/assets/about.png)
