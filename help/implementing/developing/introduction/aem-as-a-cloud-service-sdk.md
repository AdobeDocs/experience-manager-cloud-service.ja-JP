---
title: AEM as a Cloud Service の SDK
description: AEM as a Cloud Service ソフトウェア開発キットの概要
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: 33ba3e88a4116674c70c44a29273a04544b6b39b
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 36%

---

# AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

AEMas a Cloud ServiceSDK は、次のアーティファクトで構成されています。

* **クイックスタート JAR** - ローカル開発に使用される AEM ランタイム
* **Java™ API Jar** - AEM as a Cloud Serviceに対する開発に使用できる、許可されたすべての Java™ API を公開する Java™ Jar/Maven 依存関係。 これまでは Uberjar と呼ばれていました
* **Javadoc JAR** - Java™ API JAR の JavaDoc
* **Dispatcher ツール** - Dispatcher に対応するローカル開発に使用される一連のツール。UNIX®と Windows 用に別個のアーティファクトを作成

また、AEM 6.5 以前のバージョンで以前にデプロイした場合は、以下のアーティファクトを使用する場合もあります。 ローカルコンパイルがクイックスタート JAR で機能せず、デプロイされたAEMのインターフェイスがas a Cloud Serviceから削除されたと思われる場合は、カスタマーサポートにお問い合わせください。 アクセスが必要かどうかを判断できます。 バックエンドの変更が必要です。

* **6.5 非推奨（廃止予定）の Java™ API Jar** - AEM 6.5 以降に削除された追加のインターフェイスセット
* **6.5 で非推奨（廃止予定）の Javadoc JAR** - 追加のインターフェイスセットの Javadoc

## SDK を使用する場合のビルド {#building-for-the-sdk}

AEM as a Cloud Service SDK は、カスタムコードのビルドとデプロイに使用されます。詳しくは、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=ja)に関するドキュメントを参照してください。実行する手順の概要は次のとおりです。

* **コードのコンパイル**：ソースコードがコンパイルされ、その結果としてコンテンツパッケージが生成されます。
* **アーティファクトのビルド**：アーティファクトがビルドされます。
* **バンドルの分析**：Maven アナライザープラグインを使用してバンドルが分析され、依存関係が見つからないといった問題が Maven プロジェクトにないかどうかを調べます。
* **アーティファクトのデプロイ**：アーティファクトがローカルサーバーにデプロイされます。

クラウド環境へのデプロイ時と同じ手順が Cloud Manager により実行されます。ローカルでビルドを実行すると、ローカル開発とテストが可能になります。 開発者は、ソース管理にコミットして Cloud Manager のデプロイメントをトリガーする前に、コードや構造的な問題を効率的に見つけることができます。これには時間がかかる場合があります。

>[!NOTE]
>
>AEMas a Cloud ServiceSDK は、 [Cloud Manager のビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). AEMのas a Cloud Serviceのお客様は、次の URL からOracleJDK をダウンロードできます。 [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html) また、Adobe Experience Managerプロジェクトで使用する際のAdobeの JavaOracleのライセンスおよびサポート条件が原因で、2026 年 9 月まで Java 11 拡張サポートを受けています。

## AEM as a Cloud Service の SDK へのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Console の「**Adobe Experience Manager について**」アイコンで、実稼動環境で実行している AEM のバージョンを確認できます。
* クイックスタート JAR と Dispatcher ツールは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)から zip ファイルとしてダウンロードできます。SDK リストへのアクセスは、AEM Managed ServicesまたはAEM as a Cloud Serviceの環境を持つユーザーに限られます。
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
>SDK のバージョンエントリは、AEM as a Cloud Service のバージョンと一致する必要があります。AEMにログオンすると、使用しているバージョンを確認できます。 画面の右上隅で、疑問符に移動して、「 」を選択します。 **[!UICONTROL Adobe Experience Managerについて]**.


## 新しい SDK バージョンでのローカルプロジェクトの更新 {#refreshing-a-local-project-with-a-new-skd-version}

新しい SDK でローカルプロジェクトを更新するとよいのはいつでしょうか。

Adobe *推奨* 毎月のメンテナンスリリースの後に更新します。

毎日のメンテナンスリリースの後に更新する&#x200B;*オプション*&#x200B;もあります。実稼動インスタンスが新しいAEMバージョンに正常にアップグレードされると、お客様に通知されます。 毎日のメンテナンスリリースについては、新しい SDK が、まったくの場合でも大幅に変更されたとは思われません。 それでも、ローカルの AEM 開発環境を最新の SDK で時々更新し、カスタムアプリケーションを再ビルドしてテストすることをお勧めします。通常、月別メンテナンスリリースには、より影響の大きい変更が含まれているので、開発者は直ちに更新、再構築、テストをおこなう必要があります。

ローカル環境を更新するお勧めの手順を以下に示します。

1. 有用なコンテンツがソース管理下のプロジェクトにコミットされているか、可変コンテンツパッケージ内にあり後の読み込みに使用できることを確認します。。
1. ローカル開発テストのコンテンツは、Cloud Manager パイプラインのビルドの一環としてデプロイされないように、別々に保存する必要があります。 理由は、これはローカル開発にのみ使用されるためです。
1. 現在実行中のクイックスタートを停止します。
1. を `crx-quickstart` 別のフォルダーに保存し、安全に保管する。
1. 新しいAEMのバージョンをメモしておきます。Cloud Manager で参照できます（後でダウンロードする新しいクイックスタート JAR のバージョンを識別するために使用されます）。
1. ソフトウェア配布ポータルから、実稼動AEMバージョンと一致するバージョンのクイックスタート JAR をダウンロードします。
1. 新しいフォルダーを作成し、新しいクイックスタート JAR を内部に配置します。
1. 目的の実行モードで新しいクイックスタートを起動します ( ファイル名を変更するか、 `-r`) をクリックします。
   * 古いクイックスタートの残存物がフォルダーにないことを確認します。
1. AEM アプリケーションをビルドします。。
1. パッケージマネージャーを使用してAEMアプリケーションをローカルAEMにデプロイします。
1. ローカル環境でのテストに必要な可変コンテンツパッケージがあれば、パッケージマネージャーを使用してインストールします。
1. 必要に応じて、開発を続け、変更をデプロイします。

新しい AEM クイックスタートバージョンごとにインストールが必要なコンテンツがある場合は、それをコンテンツパッケージに含めると共にプロジェクトのソース管理下に置きます。その後、毎回そのコンテンツをインストールします。

SDK を頻繁に（例えば、隔週など）更新し、完全なローカル状態を毎日破棄して、アプリケーション内のステートフルデータに誤って依存しないようにすることをお勧めします。

CryptoSupport ([AEMのクラウドサービスまたは SMTP メールサービスの資格情報を設定するか、アプリケーションで CryptoSupport API を使用して、](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)) の場合、暗号化されたプロパティはキーで暗号化されます。 このキーは、AEM環境の初回起動時に自動生成されます。 クラウドの設定では、環境固有の CryptoKey の自動的な再利用に対応しますが、ローカル開発環境に暗号鍵を組み込む必要があります。

デフォルトでは、AEMはフォルダーの data フォルダー内に鍵データを格納するように設定されていますが、開発時に再利用しやすいように、「`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. このプロセスは、「 」に暗号化データを生成します。`/etc/key`&quot;.

暗号化された値を含むコンテンツパッケージを再利用できるようにするには、次の手順に従います。

* ローカルの quickstart.jar を初めて起動する場合は、「`-Dcom.adobe.granite.crypto.file.disable=true`」というパラメーターを必ず追加します。常に追加することをお勧めしますが、あくまでオプションです。
* インスタンスを初めて起動したときに、ルート「`/etc/key`&quot;. このパッケージには、再利用対象となるすべての環境で再利用される秘密鍵が格納されます。
* 秘密鍵を含んだ可変コンテンツを書き出すか、暗号化された値を `/crx/de` そのため、すべてのインストールで再利用されるパッケージに追加できます。
* 新しいインスタンスをスピンアップする場合（新しいバージョンに置き換える場合、または複数の開発環境でテスト用の資格情報を共有する場合）は、手順 2 および 3 で生成したパッケージをインストールします。 これにより、手動で再設定する必要なく、コンテンツを再利用できます。 理由は、暗号鍵が同期したからです。
