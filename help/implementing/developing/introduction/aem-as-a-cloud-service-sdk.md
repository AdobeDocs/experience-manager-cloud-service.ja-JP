---
title: AEM as a Cloud Service の SDK
description: '完了予定 '
translation-type: tm+mt
source-git-commit: 2142bce6296e671fd1039dec8b0686c609611d98

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

クラウドサービスSDKとしてのAEMは、次のアーティファクトで構成されています。

* **Quickstart Jar** — ローカル開発に使用するAEMランタイム
* **Java API Jar** - AEMに対してクラウドサービスとして開発するために使用できる、許可されているすべてのJava APIを公開するJava Jar/Mavenの依存関係。 旧称Uberjar
* **Javadoc Jar** - Java API Jarのjavadoc
* **ディスパッチャーツール** — ディスパッチャーに対してローカルに開発するために使用されるツールのセット。 UNIXとWindowsの個別のアーティファクト

また、以前にAEM 6.5以前のバージョンでデプロイした場合は、以下のアーティファクトを使用する場合もあります。 ローカルコンパイルがQuickstart jarで機能せず、Quickstart jarがクラウドサービスとしてデプロイされたAEMから削除されたインターフェイスが原因であると思われる場合は、カスタマーサポートに連絡して、アクセスが必要かどうかを判断してください。 これにはバックエンドでの変更が必要です。

* **6.5非推奨のJava API Jar** - AEM 6.5以降で削除された、追加のインターフェイスセット
* **6.5非推奨のJavadoc Jar** — インターフェイスされた追加のセットのJavadoc

## クラウドサービスSDKとしてのAEMへのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Consoleの **About Adobe Experience Manager** （Adobe Experience Managerのバージョン情報）アイコンを確認して、実稼働環境で実行しているAEMのバージョンを確認できます。
* クイックスタートjarおよびディスパッチャーツールは、ソフトウェア配布ポータルからzipファイルとし [てダウンロードできま](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)す。 SDKリストへのアクセスは、AEM Managed ServicesまたはAEMをクラウドサービス環境として持つものに限られます。
* Java API JarとJavadoc Jarは、コマンドラインまたは任意のIDEを使用して、Mavenツールを使用してダウンロードできます。
* Mavenプロジェクトフォームは、次のAPI Jarパッケージを参照する必要があります。 この依存関係は、サブパッケージpomでも参照する必要があります。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] SDKのバージョンエントリは、クラウドサービスとしてのAEMのバージョンと一致する必要があります。 AEMにログインし、画面の右上隅の疑問符に移動して、「 **[!UICONTROL Adobe Experience Managerについて」を選択すると、使用しているバージョンを確認できます。]**

* パッケージがホストされるMavenリポジトリのリモート座標は、pomファイルに含める必要があります。

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## 新しいSDKバージョンでのローカルプロジェクトの更新 {#refreshing-a-local-prokect-with-a-new-skd-version}

新しいSDKでローカルプロジェクトを更新することをお勧めするのはいつですか。

少なくとも月別 *のメンテナンス* ・リリースの後に更新することをお勧めします。

毎日のメンテナンス *リリースの後* 、更新するのはオプションです。 実稼働インスタンスが新しいAEMバージョンに正常にアップグレードされると、お客様に通知されます。 毎日のメンテナンスリリースでは、新しいSDKが大幅に変更されるとは限りません。 ただし、場合によっては、ローカルのAEM開発者環境を最新のSDKで更新し、カスタムアプリケーションを再構築してテストすることをお勧めします。 通常、月別のメンテナンスリリースには、より効果的な変更が含まれるので、開発者はすぐに更新、再構築、テストを行う必要があります。

ローカル環境を更新する場合の推奨手順を次に示します。

1. 役に立つコンテンツが、ソース管理のプロジェクトにコミットされているか、後で読み込むために可変コンテンツパッケージで使用できることを確認します。
1. ローカルの開発テストコンテンツは、Cloud Managerのパイプラインビルドの一部としてデプロイされないように、個別に保存する必要があります。 これは、ローカル開発にのみ使用する必要があるためです
1. 現在実行中のクイックスタートを停止する
1. 安全に保持す `crx-quickstart` るために、フォルダーを別のフォルダーに移動します
1. 新しいAEMバージョンをメモしておきます。これはCloud Managerで記載されています（これは、さらにダウンロードする新しいQuickStart Jarバージョンを識別するために使用されます）。
1. Software Distribution Portalから、実稼働AEMのバージョンと一致するバージョンのQuickStart JARをダウンロードします。
1. 新しいフォルダーを作成し、新しいQuickStart Jarを
1. 新しいQuickStartを目的の実行モードで開始します(ファイル名を変更するか、またはを介して実行モードを渡 `-r`します)。
   * フォルダー内に古いクイックスタートの残りがないことを確認します。
1. AEMアプリケーションの構築
1. PackageManagerを使用してAEMアプリケーションをローカルAEMにデプロイします。
1. PackageManagerを使用したローカル環境のテストに必要な可変コンテンツパッケージのインストール
1. 必要に応じて、開発を続け、変更を展開します。

新しいAEMクイックスタートバージョンごとにインストールする必要のあるコンテンツがある場合は、そのコンテンツをコンテンツパッケージに含め、プロジェクトのソース管理に含めます。 次に、毎回インストールします。

SDKを頻繁に（例えば隔週で）更新し、完全なローカル状態を毎日破棄して、アプリケーションのステートフルデータに誤って依存しないようにすることをお勧めします。

CryptoSupport(Cloudservicesの秘密鍵証明書または[AEMのSMTP Mailサービスを設定するか、アプリケーションでCryptoSupport APIを使用して](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html))に依存している場合、暗号化されたプロパティは、AEM環境の最初の開始で自動生成されるキーで暗号化されます。 クラウド設定は、環境固有のCryptoKeyを自動的に再利用しますが、ローカル開発環境に暗号鍵を挿入する必要があります。

デフォルトでは、AEMはフォルダーのdataフォルダー内にキーデータを格納するように設定されていますが、開発時に再利用しやすくするため、AEMプロセスを初回起動時に「`-Dcom.adobe.granite.crypto.file.disable=true`」を使用して初期化できます。 これにより、「」に暗号化データが生成さ`/etc/key`れます。

暗号化された値を含むコンテンツパッケージを再利用するには、次の手順に従う必要があります。

* 最初にローカルのquickstart.jarを開始する際は、次のパラメーターを必ず追加してください。「`-Dcom.adobe.granite.crypto.file.disable=true`」 常に追加することを推奨しますが、オプションです。
* インスタンスを初めて起動したときに、ルート「」のフィルターを含むパッケージを作成し`/etc/key`ます。 これは、再利用を希望するすべての環境で再利用する秘密を保持します
* 秘密を含む可変コンテンツを書き出すか、を使用して暗号化された値を参照し、 `/crx/de` インストール時に再利用できるパッケージに追加します。
* 新しいインスタンスをスピンアップする場合(新しいバージョンに置き換える場合、または複数の開発環境がテスト用に秘密鍵証明書を共有する必要がある場合)は、手動で再設定する必要なく、手順2と3で作成したパッケージをインストールします。 これは、現在、暗号鍵が同期しているからです。