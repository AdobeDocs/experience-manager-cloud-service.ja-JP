---
title: クラウドサービスSDKとしてのAEM
description: '完了予定 '
translation-type: tm+mt
source-git-commit: a7dc007230632bf8343004794b2bc4c5baaf4e05

---


# クラウドサービスSDKとしてのAEM {#aem-as-a-cloud-service-sdk}

クラウドサービスSDKとしてのAEMは、次のアーティファクトで構成されます。

* **Quickstart Jar** — ローカル開発に使用するAEMランタイム
* **Java API Jar** - AEMに対してクラウドサービスとして開発するために使用できる、許可されているすべてのJava APIを公開するJava Jar/Maven依存関係。 以前はUberjarと呼ばれていた
* **Javadoc Jar** - Java API Jarのjavadoc
* **ディスパッチャーツール** — ディスパッチャーに対してローカルで開発するために使用されるツールのセット。 UNIXとWindows用の個別のアーティファクト

また、以前AEM 6.5以前のバージョンでデプロイした場合は、以下のアーティファクトを使用する場合もあります。 ローカルコンパイルがQuickstart jarで機能せず、Quickstart jarがクラウドサービスとしてデプロイされたAEMから削除されたインターフェイスが原因であると思われる場合は、カスタマーサポートに連絡して、アクセスが必要かどうかを判断してください。 これにはバックエンドでの変更が必要です。

* **6.5非推奨のJava API Jar** - AEM 6.5以降に削除された追加のインターフェイスセット
* **6.5 Javadoc Jar** — インターフェイスされた追加セットのJavadoc

## クラウドサービスSDKとしてのAEMへのアクセス {#accessing-the-aem-as-a-cloud-service-sdk}

* AEM Admin Consoleの **About Adobe Experience Manager** （Adobe Experience Managerについて）アイコンを確認して、実稼働環境で実行しているAEMのバージョンを確認できます。
* クイックスタートjarおよびディスパッチャーツールは、ソフトウェア配布ポータルからzipファイル [としてダウンロードできま](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)す。 SDKリストへのアクセスは、クラウドサービス環境としてAEM Managed ServicesまたはAEMを使用するものに制限されます。
* Java API jarとJavadoc jarは、コマンドラインまたは任意のIDEを使用して、Mavenツールを使用してダウンロードできます。
* Mavenプロジェクトフォームは、次のAPI jarパッケージを参照する必要があります。 この依存関係は、サブパッケージの任意のプロモーションでも参照する必要があります。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] SDKのバージョンエントリは、クラウドサービスとしてのAEMのバージョンと一致する必要があります。 AEMにログインし、画面の右上隅の疑問符に移動して、「Adobe Experience Managerについて」を選択すると、使用しているバージョンを確認で **[!UICONTROL きます。]**

* パッケージがホストされるMavenリポジトリのリモート座標をpomファイルに含める必要があります。

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

少なくとも *月別のメンテナンス* ・リリースの後に更新することをお勧めします。

毎日のメンテナンス *リリースの後* 、更新することはオプションです。 実稼働インスタンスが新しいAEMバージョンに正常にアップグレードされると、お客様に通知されます。 毎日のメンテナンスリリースでは、新しいSDKが大幅に変更されるとは限りません。 ただし、ローカルのAEM開発者環境を最新のSDKで更新し、カスタムアプリケーションを再構築してテストすることをお勧めします。 通常、月別のメンテナンスリリースには、より効果的な変更が含まれるので、開発者はすぐに更新、再構築およびテストを行う必要があります。

ローカル環境を更新する場合の推奨手順を次に示します。

1. 役に立つコンテンツがソース管理のプロジェクトにコミットされているか、後でインポートできる可変コンテンツパッケージで使用できることを確認します
1. ローカルの開発テストコンテンツは、Cloud Managerのパイプラインビルドの一部としてデプロイされないように、個別に保存する必要があります。 これは、ローカル開発にのみ使用する必要があるためです
1. 現在実行中のクイックスタートの停止
1. 安全に保持す `crx-quickstart` るために、フォルダーを別のフォルダーに移動します
1. 新しいAEMバージョンをメモしておきます。これはCloud Managerに記載されています（これは、さらにダウンロードする新しいQuickStart Jarバージョンを識別するために使用されます）。
1. ソフトウェア配布ポータルから、実稼働AEMバージョンとバージョンが一致するQuickStart JARをダウンロードします。
1. 新しいフォルダーを作成し、新しいQuickStart jarを
1. 目的の実行モードで新しいQuickStartを起動します(ファイル名を変更するか、またはを使用して実行モードを渡 `-r`します)。
   * フォルダーに古いクイックスタートの名残がないことを確認します。
1. AEMアプリケーションの構築
1. PackageManagerを使用してAEMアプリケーションをローカルAEMにデプロイします
1. PackageManagerを使用したローカル環境のテストに必要な可変コンテンツパッケージのインストール
1. 必要に応じて、開発を続け、変更を展開

新しいAEMクイックスタートバージョンごとにインストールする必要のあるコンテンツがある場合は、そのコンテンツをコンテンツパッケージに含め、プロジェクトのソース管理に含めます。 その後、毎回インストールします。

SDKを頻繁に（例えば隔週的に）更新し、完全なローカル状態を毎日破棄して、アプリケーションのステートフルデータに誤って依存しないようにすることをお勧めします。

CryptoSupport(Cloudservicesの資格情報をAEMで設定するか、アプリケーションでCryptoSupport APIを使用して[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html))に依存している場合、暗号化されたプロパティは、AEM環境の初回起動時に自動生成されるキーによって暗号化されます。 クラウド設定は、環境固有のCryptoKeyを自動的に再利用しますが、ローカル開発環境に暗号鍵を挿入する必要があります。

デフォルトでは、AEMはフォルダーのdataフォルダー内にキーデータを保存するように設定されていますが、開発時に再利用しやすくするため、AEMプロセスを初回起動時に「`-Dcom.adobe.granite.crypto.file.disable=true`」を使用して初期化できます。 これにより、「」に暗号化データが生成さ`/etc/key`れます。

暗号化された値を含むコンテンツパッケージを再利用するには、次の手順に従う必要があります。

* ローカルのquickstart.jarを初めて起動する場合は、次のパラメーターを必ず追加します。「`-Dcom.adobe.granite.crypto.file.disable=true`」 常に追加することをお勧めしますが、オプションです。
* インスタンスを初めて起動したときに、ルート「」のフィルターを含むパッケージを作成し`/etc/key`ます。 これは、再利用を希望するすべての環境で再利用する秘密を保持します
* シークレットを含む可変コンテンツを書き出すか、を使用して暗号化された値を参照し、 `/crx/de` インストール時に再利用できるパッケージに追加します
* 新しいインスタンスをスピンアップする場合（新しいバージョンに置き換える場合、または複数の開発環境でテスト用に秘密鍵証明書を共有する必要がある場合）は、手動で再設定する必要なく、手順2と3で作成したパッケージをインストールします。 これは、現在、暗号鍵が同期しているからです。