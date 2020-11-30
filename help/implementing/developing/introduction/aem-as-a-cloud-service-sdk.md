---
title: AEM as a Cloud Service の SDK
description: AEM as a Cloud Service ソフトウェア開発キットの概要
translation-type: tm+mt
source-git-commit: 0b46cc8ce4229138df84c70193cf9068e1200f0a
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 87%

---


# AEM as a Cloud Service の SDK {#aem-as-a-cloud-service-sdk}

AEM as a Cloud Service の SDK は、次のアーティファクトで構成されます。

* **クイックスタート JAR** - ローカル開発に使用される AEM ランタイム
* **Java API JAR** - AEM as a Cloud Service に対応した開発に使用できる、許可されたすべての Java API を公開する Java JAR/Maven 依存関係。これまでは Uberjar と呼ばれていました
* **Javadoc JAR** - Java API JAR の Javadoc
* **Dispatcher ツール** - Dispatcher に対応するローカル開発に使用される一連のツール。UNIX 用と Windows 用に別個のアーティファクトになっています

さらに、これまでに AEM 6.5 以前のバージョンでデプロイした場合は、以下のアーティファクトを使用することになります。ローカルコンパイルがクイックスタート JAR で機能せず、AEM as a Cloud Service から削除されたインターフェイスがその原因であると疑われる場合は、カスタマーサポートに連絡して、アクセスが必要かどうかを判断してください。これには、バックエンドの変更が必要になります。

* **6.5 で非推奨（廃止予定）の Java API JAR** - AEM 6.5 以降に削除された追加のインターフェイスセット
* **6.5 で非推奨（廃止予定）の Javadoc JAR** - 追加のインターフェイスセットの Javadoc

## SDKの構築 {#building-for-the-sdk}

Cloud ServiceSDKとしてのAEMは、カスタムコードを構築しデプロイするために使用されます。 詳細は、『 [AEM Project Archetypeドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en)』を参照してください。 高いレベルで、次の手順を実行します。

* **コードをコンパイルします**。 期待どおり、ソースコードがコンパイルされ、結果のコンテンツパッケージが生成されます
* **アーティファクトを作成します**。 アーティファクトは、このプロセス中に作成されます
* **バンドルを分析します**。 バンドルはMavenアナライザープラグインを使用して分析され、Mavenプロジェクト内で依存関係の欠落などの問題を探します
* **アーティファクトをデプロイします**。 アーティファクトは、ローカルサーバーにデプロイされます。

同じ手順がCloud Managerで実行されるのは、Cloud環境に展開する場合です。 ローカルでビルドを実行すると、開発者はコードや構造の問題を効率的に発見できるので、ソース管理にコミットしてCloud Managerのデプロイメントを開始するまでに時間がかかる場合があります。

## AEM as a Cloud Service の SDK へのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Console の「**Adobe Experience Manager について**」アイコンで、実稼動環境で実行している AEM のバージョンを確認できます。
* クイックスタート JAR と Dispatcher ツールは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)から zip ファイルとしてダウンロードできます。なお、SDK リストにアクセスできるのは、AEM Managed Services 環境または AEM as a Cloud Service 環境のあるユーザーに限られます。
* Java API JAR と Javadoc JAR は、Maven ツール（コマンドラインまたは推奨 IDE）を使用してダウンロードできます。
* Maven プロジェクトの POM では、以下の API JAR パッケージを参照する必要があります。サブパッケージのあらゆる POM でも、この依存関係を参照する必要があります。

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
>SDK のバージョンエントリは、AEM as a Cloud Service のバージョンと一致する必要があります。AEM にログインし、画面の右上隅にある疑問符アイコンに移動して、「**[!UICONTROL Adobe Experience Manager について]**」を選択すると、使用しているバージョンを確認できます。


## 新しい SDK バージョンでのローカルプロジェクトの更新 {#refreshing-a-local-project-with-a-new-skd-version}

新しい SDK でローカルプロジェクトを更新するとよいのはいつでしょうか。

少なくとも毎月のメンテナンスリリースの後に更新することを&#x200B;*お勧め*&#x200B;します。

毎日のメンテナンスリリースの後に更新する&#x200B;*オプション*&#x200B;もあります。実稼動インスタンスが新しい AEM バージョンに正常にアップグレードされると、お客様にその通知が届きます。毎日のメンテナンスリリースについては、新しい SDK に仮に変更があったとしても大幅な変更があるとは思われません。それでも、ローカルの AEM 開発環境を最新の SDK で時々更新し、カスタムアプリケーションを再ビルドしてテストすることをお勧めします。通常、毎月のメンテナンスリリースには、より影響の大きい変更が含まれるので、開発者は直ちに更新、再ビルド、テストをおこなう必要があります。

ローカル環境を更新するお勧めの手順を以下に示します。

1. 有用なコンテンツがソース管理下のプロジェクトにコミットされているか、可変コンテンツパッケージ内にあり後の読み込みに使用できることを確認します。
1. ローカル開発のテストコンテンツは、Cloud Manager パイプラインのビルドの一環としてデプロイされないように、別個に保存する必要があります。ローカル開発にのみ使用する必要があるからです。
1. 現在実行中のクイックスタートを停止します。
1. `crx-quickstart` フォルダーを安全に保管するために別のフォルダーに移動します。
1. 新しい AEM のバージョンをメモしておきます。これは Cloud Manager で参照できます（後でダウンロードする新しいクイックスタート JAR のバージョンを識別するために使用されます）。
1. 実稼動環境の AEM バージョンと一致するバージョンのクイックスタート JAR をソフトウェア配布ポータルからダウンロードします。
1. 新しいフォルダーを作成し、その中に新しいクイックスタート JAR を格納します。
1. 目的の実行モードで新しいクイックスタートを起動します（ファイル名を変更するか、`-r` を使用して実行モードを渡します）。
   * 古いクイックスタートの残存物がフォルダーにないことを確認します。
1. AEM アプリケーションをビルドします。
1. パッケージマネージャーを使用して、AEM アプリケーションをローカル AEM にデプロイします。
1. ローカル環境でのテストに必要な可変コンテンツパッケージがあれば、パッケージマネージャーを使用してインストールします。
1. 必要に応じて、開発を続け変更をデプロイします。

新しい AEM クイックスタートバージョンごとにインストールが必要なコンテンツがある場合は、それをコンテンツパッケージに含めると共にプロジェクトのソース管理下に置きます。その後、毎回そのコンテンツをインストールします。

SDK を頻繁に（例えば、隔週など）更新し、完全なローカル状態を毎日破棄して、アプリケーション内のステートフルデータに誤って依存しないようにすることをお勧めします。

（[AEM の Cloud Services または SMTP メールサービスの認証情報を設定するか、アプリケーションで CryptoSupport API を使用して）](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)CryptoSupport に基づいている場合、暗号化されるプロパティは、AEM 環境の初回起動時に自動生成されるキーで暗号化されます。クラウド設定では環境固有の暗号鍵の自動的な再利用に対応できますが、ローカル開発環境に暗号鍵を組み込む必要があります。

デフォルトでは、AEM はデータフォルダー内に鍵データを保存するように設定されていますが、開発時に再利用しやすいように、「`-Dcom.adobe.granite.crypto.file.disable=true`」を使用して AEM プロセスを初回起動時に初期化できます。これにより、「`/etc/key`」に暗号化データが生成されます。

暗号化された値を含んだコンテンツパッケージを再利用できるようにするには、次の手順に従う必要があります。

* ローカルの quickstart.jar を初めて起動する場合は、「`-Dcom.adobe.granite.crypto.file.disable=true`」というパラメーターを必ず追加します。常に追加することをお勧めしますが、あくまでオプションです。
* インスタンスを初めて起動したときに、ルート「`/etc/key`」のフィルターを含んだパッケージを作成します。ここには、対象となるすべての環境で再利用される秘密鍵が格納されます。
* 秘密鍵を含んだ可変コンテンツを書き出すか、暗号化された値を `/crx/de` から参照して、すべてのインストールで再利用されるパッケージに追加します。
* （新しいバージョンに置き換えるために、または複数の開発環境でテスト用の認証情報を共有する必要があるので）新しいインスタンスをセットアップする場合は、手動で再設定しなくてもコンテンツを再利用できるように、手順 2 および 3 で生成したパッケージをインストールします。これは、暗号鍵が同期するようになったからです。
