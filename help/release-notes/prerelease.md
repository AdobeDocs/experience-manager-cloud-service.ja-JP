---
title: Adobe Experience Manager as a Cloud Service プレリリースチャネル
description: プレリリースチャネルを使用して、AEM as a Cloud Service の今後の機能のプレビューを取得する方法について説明します。
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 95%

---


# Adobe Experience Manager as a Cloud Service プレリリースチャネル {#prerelease-channel}

プレリリースチャネルを使用して、AEM as a Cloud Service の今後の機能のプレビューを取得する方法について説明します。

## はじめに {#introduction}

Adobe Experience Manager as a Cloud Serviceは、[Experience Managerリリースロードマップ ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja#aem-as-cloud-service) に従って、毎月のリリースサイクルで新機能を提供します。

次の機能リリースで公開予定の機能を把握できるように、プレリリースチャネルを購読できます。プレリリースチャネルにアクセスするには、開発環境または任意のサンドボックス環境を設定します。AEM ユーザーインターフェイスからアクセス可能な変更をプレビューしたり、新しいプレリリース API に対してコードを作成したりできます。

特定の機能リリースのプレリリース機能のリストは、[リリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)に掲載されています。

## AEM as a Cloud Service のリリース {#releases}

AEM as a Cloud Service には 2 種類のリリースがあります。

* **機能リリース**&#x200B;は、アクティベーション時に AEM as a Cloud Service に機能と特徴を追加します
* **メンテナンスリリース**&#x200B;は、セキュリティ更新、パフォーマンス強化、バグ修正を追加し、定期的かつ頻繁に適用されます。

このパターンにより、サービスが中断されることなく継続的にリリースされます。

プレリリースチャネルでは、今後の機能を評価し、独自のプロジェクトで可能な実装を計画するために、今後の機能リリースでスケジュールされている機能をプレビューできます。これにより、次の機能リリースに向けて事前に計画できます。

例えば、5月にプレリリースチャネルを購読している場合、今後の 6月のリリースで機能を評価できます。

![プレリリースサイクルの図](assets/prerelease-cadence.png)

プレリリースでは、今後の AEMaaCS の機能を 1 か月間にわたって利用できるので、この期間に、新機能がプロジェクトやカスタマイズに与える影響を評価し、これらの機能、テスト、ユーザートレーニングの展開を計画できます。

プレリリースチャネルを効果的に活用するには、4 つの手順が必要です。

1. [カレンダーをマークする](#mark-calendars)
1. [リリースノートを確認する](#release-notes)
1. [新機能にアクセスして試す](#new-features)
1. [ユーザーをトレーニングする](#train-users)

## カレンダーをマークする {#mark-calendars}

機能リリースは事前にスケジュールされており、リリース日は ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja#aem-as-cloud-service)0}Adobe Experience League} に公開されています。[

リリース日を控えておくと、今後の機能の確認やテストを計画できます。

## リリースノートを確認する {#release-notes}

カレンダーにリリース日をマークしたら、リリース日に [Adobe Experience League](/help/release-notes/release-notes-cloud/release-notes-current.md) の web サイトで最新のリリースノートを確認します。

各リリースには、そのリリースの新機能だけでなく、プレリリース評価で使用できる機能についても記載したリリースノートが付属しています。事前に情報を取得して、AEMaaCS の最新機能を活用する計画を立ててください。

また、すべてのリリースと共に公開されている[既知の問題を確認](/help/release-notes/maintenance/latest.md)することもできます。これにより、新機能の評価や最終的な採用に課題が生じる可能性のある技術的な問題を認識することもできます。

## プレリリースチャネルを有効にして新機能にアクセスして試す {#new-features}

プレリリースチャネルは、任意の開発環境またはサンドボックス環境で有効にできます。プレリリースは、ステージング環境または実稼動環境では有効にできません。

プレリリース機能は、次のような異なる方法で使用できます。

* [クラウド環境](#cloud-environments)
* [ローカル SDK](#local-sdk)

### クラウド環境 {#cloud-environments}

プレリリースを使用するようにクラウド環境を更新するには、新しい環境変数を追加する必要があります。これは、Cloud Manager UI または CLI を使用して実行できます。

#### UI を使用した環境変数の追加 {#add-with-ui}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. プレリリースを有効にするプログラムに移動します。

1. プレリリースを有効にする環境を選択し、**プログラム**／**環境**／**環境設定**&#x200B;に移動して、設定にアクセスします。

1. 新しい [ 環境変数 ](../implementing/cloud-manager/environment-variables.md) を追加します

   | 名前 | 値 | 適用されるサービス | タイプ |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | すべて | 変数 |

1. 変更内容を保存すると、プレリリース機能の切り替えが有効になった状態で環境が更新されます。

   ![新しい環境変数](assets/env-configuration-prerelease.png)

#### CLI を使用した環境変数の追加 {#add-with-cli}

Cloud Manager API と CLI を使用して環境変数を更新することもできます。

* [Cloud Manager API の環境変数エンドポイント ](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables) を使用して、`AEM_RELEASE_CHANNEL` 環境変数に値 `prerelease` を設定します。

  ```text
  PATCH /program/{programId}/environment/{environmentId}/variables
  [
          {
                  "name" : "AEM_RELEASE_CHANNEL",
                  "value" : "prerelease",
                  "type" : "string"
          }
  ]
  ```

* [Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) も使用できます

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

環境を通常の（プレリリース以外の）チャネルの動作に戻す場合は、変数を削除するか、別の値に設定し直します。

### ローカル SDK {#local-sdk}

Maven Central にあるプレリリース `API Jar` を参照するように Maven プロジェクトを設定することで、ローカル Quickstart SDK の Sites コンソールの新機能と、プレリリースの新しい API に対応するコードを確認できます。通常の Quickstart SDK をプレリリースモードで起動することにより、ローカル開発環境でこれらのプレリリース機能を確認することもできます。

#### プレリリースモードで Quickstart SDK を起動 {#prerelease-mode}

1. SDK をソフトウェア配布ポータルからダウンロードし、[AEM as a Cloud Service SDK へのアクセス](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)の説明に従ってインストールします。
1. SDK Quickstart を起動する際に、引数 `-r prerelease` を含めます。

この値は、sticky なので最初の起動時にのみ選択できます。コマンドラインオプションを変更するには、SDK を再インストールします。

毎月の機能リリースの間に複数の AEM メンテナンスリリースが行われる可能性があるので、これらの新しい SDK をダウンロードし、Maven プロジェクトで新しい SDK API Jar バージョンを参照できます。メンテナンスリリースには、追加のプレリリース機能はありませんが、バグ修正、セキュリティ修正、パフォーマンス強化などの小規模な変更が含まれる場合があります。
Javadoc は Maven Central に公開されます。

#### プレリリース SDK に対応するビルド {#build-sdk}

1. Maven プロジェクトの `pom.xml` を変更して、Maven Central に公開されている個別のプレリリース SDK API jar を参照するようにします。これには、プレリリース機能の新しい Java API が含まれており、SDK API jar に依存しています。同じバージョンが使用されます。

   例として、通常の API jar を参照する親 POM の依存関係管理セクションのスニペットを次に示します。

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
> `aem-prerelease-sdk-api` artifactId は、ステージまたは実稼働環境にデプロイするときには使用しないでください。実稼働パイプラインでデプロイする場合は、必ず `aem-sdk-api` を使用します。同様に、プレリリース API を参照するコードは、実稼動パイプラインでデプロイしないでください。

[AEM CS SDK ビルドアナライザー Maven プラグイン v1.0 以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)では、依存関係を調べて、プレリリース API がプロジェクトで使用されているかどうかを検出します。アナライザーで検出すると、プレリリース SDK API を使用してプロジェクトを分析します。

## ユーザーのトレーニング {#train-users}

プレリリースチャネルの新機能をテストし、プロジェクトで活用することにしたら、ユーザーのトレーニングを行う必要があります。

Adobe Experience League では、AEMaaCS を学ぶための多くのリソースを提供しています。

* [AEMaaCS のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)
* [チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-tutorials/overview.html?lang=ja)
* リリースノートの[月次リリース概要ビデオ](/help/release-notes/release-notes-cloud/release-notes-current.md#release-video)

## 検討事項 {#considerations}

プレリリースチャンネルを使用する際には、いくつかの注意事項があります。

* プレリリースチャネルには、次のリリースでロールアウトされるすべての新機能が含まれているとは限りません。
* プレリリースの機能は厳しい品質保証検査を通り、ベータ版の品質ではなく完全な機能を実現することを目的としています。通常の AEM リリースの機能にバグがあると思われる場合と同様に、問題に気がついた場合は報告してください。
* 環境がプレリリースチャネル用に設定されているかどうかを判断するには、AEM コンソールの&#x200B;**バージョン情報**&#x200B;ページに移動し、AEM バージョン番号に ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE``` などの&#x200B;*プレリリース*&#x200B;サフィックスが含まれているかどうかを確認します。

![バージョン情報](/help/release-notes/assets/about.png)
