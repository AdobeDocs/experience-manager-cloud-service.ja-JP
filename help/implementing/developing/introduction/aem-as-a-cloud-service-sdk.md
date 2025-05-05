---
title: AEM as a Cloud Service の SDK
description: AEM as a Cloud Service Software Development Kit の概要です。
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 82f5078740b2cf6ac481d83df40bbbc4fb3c1a77
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 48%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK は、次のアーティファクトで構成されます。

* **クイックスタート JAR** -ローカル開発に使用するAEM ランタイム。
* **Java™ API JAR** - AEM as a Cloud Service に対応した開発に使用できる、許可されたすべての Java™ API を公開する Java™ JAR/Maven 依存関係。以前は Uberjar と呼んでいました。
* **Javadoc Jar** - Java™ API Jar の Java ドキュメント。
* **Dispatcher ツール** - Dispatcher に対応するローカル開発に使用される一連のツール。UNIX® と Windows のアーティファクトを分離します。

さらに、これまでに AEM 6.5 以前のバージョンでデプロイした場合は、以下のアーティファクトを使用することになります。ローカルコンパイルが QuickStart Jar で機能せず、AEMからデプロイされたas a Cloud Serviceのインターフェイスが削除されていることが疑われる場合は、カスタマーサポートにお問い合わせください。 アクセスが必要かどうかを判断できます。バックエンドの変更が必要です。

* **6.5 非推奨の Java™ API Jar** - AEM 6.5 以降で削除された、インターフェイスの追加セットです。
* **6.5 非推奨（廃止予定）の Javadoc Jar** - インターフェイスの追加セットに関する Java ドキュメント。

>[!NOTE]
> 
> AEM as a Cloud ServiceとSDKには、様々な違いがあります。 迅速かつ反復的に変更が必要な状況に対応するために、アドビは迅速な開発環境を導入しました。詳しくは、[迅速な開発環境](/help/implementing/developing/introduction/rapid-development-environments.md)を参照してください。

## SDK を使用する場合のビルド {#building-for-the-sdk}

AEM as a Cloud Service SDK は、カスタムコードのビルドとデプロイに使用されます。[AEM プロジェクトアーキタイプドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/using)を参照してください。実行する手順の概要は次のとおりです。

* **コードのコンパイル** - Source コードがコンパイルされ、結果として生成されるコンテンツパッケージが生成されます。
* **アーティファクトを作成** - アーティファクトはこのプロセス中に作成されます。
* **バンドルの分析** - バンドルは、Maven アナライザープラグインを使用して分析され、依存関係の欠落などの問題が Maven プロジェクトで見つかります。
* **アーティファクトをデプロイ** - アーティファクトはローカルサーバーにデプロイされます。

Cloud Managerは、クラウド環境にデプロイする場合と同じ手順を実行します。 ローカルでビルドを実行すると、ローカル開発とテストが可能になります。開発者は、ソース管理にコミットする前に、コードや構造の問題を効率的に特定できます。 このプロセスは、Cloud Managerのデプロイメントのトリガーに起因する遅延（時間がかかる場合がある）の防止に役立ちます。

>[!NOTE]
>
>AEM as a Cloud Service SDK は、[Cloud Manager のビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)によりサポートされている Java の配布とバージョンで構築する必要があります。AEM as a Cloud Serviceのお客様は、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html) からOracle JDK をダウンロードできます。 2026 年 9 月まで Java 11 サポートが延長されます。これは、Adobe Experience Manager プロジェクトでのAdobeのOracle Java テクノロジーのライセンス条件およびサポート条件が原因です。

## AEM as a Cloud Service の SDK へのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Consoleの「**Adobe Experience Managerについて**」アイコンをチェックすると、実稼動環境で実行しているAEMのバージョンを確認できます。
* QuickStart Jar とDispatcher ツールは、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html) から zip ファイルでダウンロードできます。 SDK リストへのアクセスは、AEM Managed Services または AEM as a Cloud Service の環境を持つユーザーに限られます。
* Java™ API Jar と Javadoc Jar は、Maven ツールを使用して、コマンドラインまたは好みの IDE でダウンロードできます。
* Maven プロジェクトの POM では、以下の API JAR パッケージを参照する必要があります。サブパッケージの POM への依存も参照する必要があります。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>SDK のバージョンエントリは、AEM as a Cloud Service のバージョンと一致する必要があります。AEM にログオンすると、使用中のバージョンを確認できます。画面の右上隅にある疑問符に移動し、「**[!UICONTROL Adobe Experience Managerについて]** をクリックします。


## 新しいSDK バージョンでローカルプロジェクトを更新 {#refreshing-a-local-project-with-a-new-skd-version}

新しい SDK でローカルプロジェクトを更新するとよいのはいつでしょうか。

アドビでは、毎月のメンテナンスリリース後に更新することを&#x200B;*推奨*&#x200B;しています。

毎日のメンテナンスリリースの後に更新する&#x200B;*オプション*&#x200B;もあります。実稼動インスタンスが新しい AEM バージョンに正常にアップグレードされると、お客様にその通知が届きます。毎日のメンテナンスリリースについては、新しい SDK に仮に変更があったとしても大幅な変更があるとは思われません。Adobeでは、場合によっては最新のSDKでローカル AEM開発者環境を更新し、カスタムアプリケーションを再構築してテストすることをお勧めします。 通常、毎月のメンテナンスリリースには、より影響の大きい変更が含まれるので、開発者は直ちに更新、再ビルド、テストを行う必要があります。

**ローカルプロジェクトを新しいSDK バージョンで更新するには：**

1. すべての有用なコンテンツが、ソースコントロールにコミットされるようにします。 または、後で読み込むために可変コンテンツパッケージに格納される。
1. ローカル開発のテストコンテンツは、Cloud Manager パイプラインのビルドの一環としてデプロイされないように、別個に保存する必要があります。理由は、これはローカル開発にのみ使用されるためです。
1. 現在実行中のクイックスタートを停止します。
1. `crx-quickstart` フォルダーを安全に保管するために別のフォルダーに移動します。
1. 新しい AEM のバージョンをメモしておきます。これは Cloud Manager で参照できます（後でダウンロードする新しいクイックスタート JAR のバージョンを識別するために使用されます）。
1. 実稼動AEMのバージョンに一致するバージョンの QuickStart Jar を、ソフトウェア配布ポータルからダウンロードします。
1. 新しいフォルダーを作成し、その中に新しいクイックスタート JAR を格納します。
1. 新しいクイックスタートを目的の実行モードで起動します（ファイル名を変更するか、`-r` を使用して実行モードを渡します）。
フォルダーに古いクイックスタートの残骸がないことを確認します。
1. AEM アプリケーションをビルドします。
1. パッケージマネージャーを使用して AEM アプリケーションをローカル AEM にデプロイします。
1. ローカル環境のテストに必要な可変コンテンツパッケージを、パッケージマネージャーを介してインストールします。
1. 必要に応じて、開発を続け変更をデプロイします。

新しい AEM クイックスタートバージョンごとにインストールが必要なコンテンツがある場合は、それをコンテンツパッケージに含めると共にプロジェクトのソース管理下に置きます。その後、毎回そのコンテンツをインストールします。

Adobeでは、SDKを頻繁に（例：隔週で）アップデートすることをお勧めします。 また、完全なローカル状態を毎日破棄して、アプリケーション内で誤ってステートフルデータに依存しないようにします。

クラウドサービス用の CryptoSupport、SMTP メール設定または CryptoSupport API を使用している場合、暗号化されたプロパティはキーで保護されます。 詳しくは、[CryptoSupport API ドキュメント ](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html) を参照してください。 この鍵は、AEM 環境の初回起動時に自動生成されます。クラウド設定では環境固有の暗号鍵の自動的な再利用に対応できますが、ローカル開発環境に暗号鍵を組み込む必要があります。

デフォルトでは、AEMはキーデータをフォルダーのデータフォルダー内に格納するように設定されていますが、開発時に再利用しやすくするために、初回起動時に「`-Dcom.adobe.granite.crypto.file.disable=true`」を使用してAEM プロセスを初期化できます。 このプロセスは、「`/etc/key`」に暗号化データを生成します。

**暗号化された値を含むコンテンツパッケージを再利用するには：**

* 最初にローカルの quickstart.jar を起動するときは、必ず次のパラメーターを追加してください。「`-Dcom.adobe.granite.crypto.file.disable=true`」 Adobeでは、オプションで常に追加することをお勧めします。
* インスタンスを初めて起動するときは、ルート「`/etc/key`」のフィルターを含むパッケージを作成します。 このパッケージには、対象となるすべての環境で再利用される秘密鍵が格納されます。
* シークレットを含む可変コンテンツを書き出します。 または、`/crx/de` を使用して暗号化された値を検索し、インストール全体で再利用されるパッケージに追加することもできます。
* 新しいインスタンスをスピンアップする場合（新しいバージョンに置き換える場合、または複数の開発環境でテスト用の資格情報を共有する場合）は、手順 2 および 3 で生成したパッケージをインストールします。これにより、手動で再設定しなくても、コンテンツを再利用できます。これは、暗号鍵が同期されるようになったためです。

