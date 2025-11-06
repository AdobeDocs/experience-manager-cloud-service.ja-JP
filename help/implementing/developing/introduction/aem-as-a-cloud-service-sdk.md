---
title: AEM as a Cloud Service SDK
description: AEM as a Cloud Service ソフトウェア開発キットの概要。
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 100%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service SDK は、次のアーティファクトで構成されます。

* **クイックスタート JAR** - ローカル開発に使用される AEM ランタイム。
* **Java™ API JAR** - AEM as a Cloud Service に対応した開発に使用できる、許可されたすべての Java™ API を公開する Java™ JAR/Maven 依存関係。これまでは Uberjar と呼ばれていました。
* **Javadoc JAR** - Java™ API JAR の Java ドキュメント。
* **Dispatcher ツール** - Dispatcher に対応するローカル開発に使用される一連のツール。UNIX® 用と Windows 用に別個のアーティファクトになっています。

さらに、これまでに AEM 6.5 以前のバージョンでデプロイした場合は、以下のアーティファクトを使用することになります。ローカルコンパイルがクイックスタート JAR で機能せず、デプロイされた AEM as a Cloud Service からインターフェイスが削除されたと思われる場合は、カスタマーサポートにお問い合わせください。アクセスが必要かどうかを判断できます。バックエンドの変更が必要です。

* **6.5 で非推奨（廃止予定）の Java™ API JAR** - AEM 6.5 以降に削除された追加のインターフェイスセット。
* **6.5 で非推奨（廃止予定）の Javadoc JAR** - 追加のインターフェイスセットの Java ドキュメント。

>[!NOTE]
> 
> AEM as a Cloud Service と SDK には、様々な領域で違いがあります。迅速かつ反復的に変更が必要な状況に対応するために、アドビは高速開発環境を導入しました。詳しくは、[高速開発環境](/help/implementing/developing/introduction/rapid-development-environments.md)を参照してください。

## SDK を使用する場合のビルド {#building-for-the-sdk}

AEM as a Cloud Service SDK は、カスタムコードのビルドとデプロイに使用されます。[AEM プロジェクトアーキタイプドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/using)を参照してください。実行する手順の概要は次のとおりです。

* **コードをコンパイル** - ソースコードがコンパイルされ、その結果としてコンテンツパッケージが生成されます。
* **アーティファクトをビルド** - アーティファクトがビルドされます。
* **バンドルを分析** - Maven アナライザープラグインを使用してバンドルが分析され、依存関係が見つからないといった問題が Maven プロジェクトにないかどうかを調べます。
* **アーティファクトをデプロイ** - アーティファクトがローカルサーバーにデプロイされます。

Cloud Manager は、クラウド環境にデプロイする際に同じ手順を実行します。ローカルでビルドを実行すると、ローカル開発とテストが可能になります。開発者は、ソース管理にコミットする前に、コードや構造的な問題を効率的に見つけることができます。このプロセスは、時間がかかる場合がある Cloud Manager のデプロイメントのトリガーによって発生する遅延を防ぐのに役立ちます。

>[!NOTE]
>
>AEM as a Cloud Service SDK は、[Cloud Manager のビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)によりサポートされている Java の配布とバージョンで構築する必要があります。AEM as a Cloud Service のお客様は、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)から Oracle JDK をダウンロードできます。Adobe Experience Manager プロジェクトの Oracle Java テクノロジーに対して、アドビのライセンスとサポート条件により 2026年9月まで Java 11 の延長サポートを受けられます。

## AEM as a Cloud Service の SDK へのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Console の「**Adobe Experience Manager について**」アイコンで、実稼動環境で実行している AEM のバージョンを確認できます。
* クイックスタート JAR と Dispatcher ツールは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)から zip ファイルとしてダウンロードできます。SDK リストへのアクセスは、AEM Managed Services または AEM as a Cloud Service の環境を持つユーザーに限られます。
* Java™ API JAR と Javadoc JAR は、Maven ツール（コマンドラインまたは推奨 IDE）を使用してダウンロードできます。
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
>SDK のバージョンエントリは、AEM as a Cloud Service のバージョンと一致する必要があります。AEM にログオンすると、使用中のバージョンを確認できます。画面の右上隅にある疑問符に移動し、「**[!UICONTROL Adobe Experience Manager について]**」をクリックします。


## 新しい SDK バージョンでのローカルプロジェクトの更新 {#refreshing-a-local-project-with-a-new-skd-version}

新しい SDK でローカルプロジェクトを更新するとよいのはいつでしょうか。

アドビでは、毎月のメンテナンスリリース後に更新することを&#x200B;*推奨*&#x200B;しています。

毎日のメンテナンスリリースの後に更新する&#x200B;*オプション*&#x200B;もあります。実稼動インスタンスが新しい AEM バージョンに正常にアップグレードされると、お客様にその通知が届きます。毎日のメンテナンスリリースについては、新しい SDK に仮に変更があったとしても大幅な変更があるとは思われません。それでも、アドビでは、ローカルの AEM 開発環境を最新の SDK で時々更新し、カスタムアプリケーションを再ビルドしてテストすることをお勧めします。通常、毎月のメンテナンスリリースには、より影響の大きい変更が含まれるので、開発者は直ちに更新、再ビルド、テストを行う必要があります。

**新しい SDK バージョンでローカルプロジェクトを更新するには：**

1. すべての有用なコンテンツをソースコントロールにコミットします。または、後で読み込めるように、可変コンテンツパッケージに保存します。
1. ローカル開発のテストコンテンツは、Cloud Manager パイプラインのビルドの一環としてデプロイされないように、別個に保存する必要があります。理由は、これはローカル開発にのみ使用されるためです。
1. 現在実行中のクイックスタートを停止します。
1. `crx-quickstart` フォルダーを安全に保管するために別のフォルダーに移動します。
1. 新しい AEM のバージョンをメモしておきます。これは Cloud Manager で参照できます（後でダウンロードする新しいクイックスタート JAR のバージョンを識別するために使用されます）。
1. 実稼動環境の AEM バージョンと一致するバージョンのクイックスタート JAR を、ソフトウェア配布ポータルからダウンロードします。
1. 新しいフォルダーを作成し、その中に新しいクイックスタート JAR を格納します。
1. 目的の実行モードで新しいクイックスタートを起動します（ファイル名を変更するか、`-r` を使用して実行モードを渡します）。
古いクイックスタートの残存物がフォルダーにないことを確認します。
1. AEM アプリケーションをビルドします。
1. パッケージマネージャーを使用して AEM アプリケーションをローカル AEM にデプロイします。
1. ローカル環境でのテストに必要な可変コンテンツパッケージがあれば、パッケージマネージャーを使用してインストールします。
1. 必要に応じて、開発を続け変更をデプロイします。

新しい AEM クイックスタートバージョンごとにインストールが必要なコンテンツがある場合は、それをコンテンツパッケージに含めると共にプロジェクトのソース管理下に置きます。その後、毎回そのコンテンツをインストールします。

アドビでは、SDK を頻繁に（例えば、隔週など）更新することをお勧めします。また、アプリケーション内のステートフルデータに誤って依存しないように、完全なローカル状態を毎日破棄します。

クラウドサービス、SMTP メール設定または CryptoSupport API に CryptoSupport を使用する場合、暗号化されたプロパティは鍵で保護されます。詳しくは、[CryptoSupport API ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)を参照してください。この鍵は、AEM 環境の初回起動時に自動生成されます。クラウド設定では環境固有の暗号鍵の自動的な再利用に対応できますが、ローカル開発環境に暗号鍵を組み込む必要があります。

デフォルトでは、AEM はデータフォルダー内に鍵データを保存するように設定されていますが、開発時に再利用しやすいように、「`-Dcom.adobe.granite.crypto.file.disable=true`」を使用して AEM プロセスを初回起動時に初期化できます。このプロセスによって「`/etc/key`」で暗号化データが生成されます。

**暗号化された値を含むコンテンツパッケージを再利用するには：**

* ローカルの quickstart.jar を初めて起動する場合は、「`-Dcom.adobe.granite.crypto.file.disable=true`」というパラメーターを必ず追加します。アドビでは、オプションで常に追加することをお勧めします。
* インスタンスを初めて起動したときに、ルート「`/etc/key`」のフィルターを含んだパッケージを作成します。このパッケージには、対象となるすべての環境で再利用される秘密鍵が格納されます。
* 秘密鍵を含んだ可変コンテンツを書き出します。または、`/crx/de` を使用して暗号化された値を検出することで、すべてのインストールで再利用されるパッケージに追加できます。
* 新しいインスタンスをスピンアップする場合（新しいバージョンに置き換える場合、または複数の開発環境でテスト用の資格情報を共有する場合）は、手順 2 および 3 で生成したパッケージをインストールします。これにより、手動で再設定しなくても、コンテンツを再利用できます。これは、暗号鍵が同期されるようになったためです。

