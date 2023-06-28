---
title: Adobe Target との統合
description: Adobe Target との統合
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 67%

---

# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Experience Cloudに含まれているAdobe Targetを使用すると、あらゆるチャネルにわたってターゲティングと測定をおこない、コンテンツの関連性を高めることができます。 Adobe Target と AEM as a Cloud Service の統合には、次のものが必要です。

* タッチ操作対応 UI を使用して、AEM as a Cloud Service で Target 設定を作成します（IMS 設定が必要）。
* [Adobe Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=ja) の拡張機能として Adobe Target を追加し、設定する方法について説明します。

Adobe Launch は、AEM ページの Analytics と Target（JS ライブラリ／タグ）の両方のクライアントサイドプロパティを管理するために必要です。ただし、「エクスペリエンスのターゲット設定」には、Launch との統合が必要です。

エクスペリエンスフラグメントやコンテンツフラグメントを Target に書き出す場合は、[Adobe Target 設定と IMS](/help/sites-cloud/integrating/integration-adobe-target-ims.md) のみ必要です。

>[!NOTE]
>
>既存の Target アカウントを持たないお客様は、Experience Cloud用の Target Foundation パックへのアクセスをリクエストできます。 この Foundation パックでは、Target の使用量が制限されます。

## Adobe Target 設定の作成 {#create-configuration}

1. **ツール**／**クラウドサービス**に移動します。
   ![ナビゲーション](assets/cloudservice1.png "ナビゲーション")
2. 「**Adobe Target**」を選択します。
3. 「**作成**」ボタンを選択します。
   ![作成](assets/tenant1.png "作成")
4. 詳細（以下を参照）を入力し、「**接続**」を選択します。
   ![接続](assets/open_screen1.png "接続")

### IMS 設定 {#ims-configuration}

Target を AEM および Launch と適切に統合するには、Launch と Target の両方の IMS 設定が必要です。Launch の IMS 設定は AEM as a Cloud Service で事前に設定されていますが、Target の IMS 設定は、Target のプロビジョニング後に作成する必要があります。詳しくは、 [Adobe Targetとの統合時に使用する IMS 設定](/help/sites-cloud/integrating/integration-adobe-target-ims.md) とビデオ [Experience Platform LaunchとAEMの統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=ja) Target IMS 設定の作成方法を説明します。

### Adobe Target テナント ID と Adobe Target クライアントコード {#tenant-client}

「 Adobe Targetテナント ID 」フィールドと「 Adobe Targetクライアントコード」フィールドを設定する際は、次の点に注意してください。

1. ほとんどのお客様の場合、テナント ID とクライアントコードは同じです。つまり、両方のフィールドに同じ情報が含まれ、同一です。 両方のフィールドにテナント ID を必ず入力してください。
2. 従来の目的では、テナント ID とクライアントコードのフィールドに異なる値を入力することもできます。

どちらの場合も、次のようになります。

* デフォルトでは、（最初に追加された場合は）「クライアントコード」も「テナント ID」フィールドに自動的にコピーされます。
* オプションで、デフォルトのテナント ID セットを変更できます。
* Target へのバックエンド呼び出しはテナント ID に基づき、Target へのクライアント側呼び出しはクライアントコードに基づきます。

前述したように、AEM as a Cloud Service では最初のケースが最も一般的です。どちらの場合も、**両方の**&#x200B;フィールドに、要件に応じた正しい情報が含まれていることを確認してください。

>[!NOTE]
>
> 既存の Target 設定を変更する場合：
>
> 1. テナント ID を再入力します。
> 2. Target に再接続します。
> 3. 設定を保存します。

### Target 設定の編集 {#edit-target-configuration}

Target 設定を編集するには、次の手順に従います。

1. 既存の設定を選択し、「**プロパティ**」をクリックします。
2. プロパティを編集します。
3. 「**Adobe Target に再接続**」を選択します。
4. 「**保存して閉じる**」を選択します。

### サイトへの設定の追加 {#add-configuration}

タッチ UI 設定をサイトに適用するには、次の場所に移動します。 **サイト** > **任意のサイトページを選択** > **プロパティ** > **詳細** > **設定** /設定テナントを選択します。

## Adobe Launch を使用して、AEM サイトに Adobe Target を統合する {#integrate-target-launch}

AEM は、Experience Platform Launch との標準の統合を提供します。Adobe Target 拡張機能を Experience Platform Launch に追加すると、AEM web ページで Adobe Target の機能を使用できます。Target ライブラリは、Launch を使用してのみレンダリングされます。

>[!NOTE]
>
>既存の（レガシー）フレームワークは引き続き機能しますが、タッチ操作対応 UI では設定できません。Adobeでは、Launch で変数マッピング設定を再構築することをお勧めします。

一般的な概要として、統合手順は次のとおりです。

1. Launch プロパティの作成
2. 必要な拡張機能の追加
3. データ要素の作成（コンテキストハブのパラメーターを取り込むため）
4. ページルールの作成
5. ビルドと公開

### Launch プロパティの作成 {#create-property}

プロパティは、拡張機能、ルール、データ要素が入力されるコンテナです。

1. 「**新規プロパティ**」ボタンを選択します。
2. プロパティの名前を指定します。
3. ドメインとして、Launch ライブラリを読み込む IP／ホストを入力します。
4. 「**保存**」ボタンを選択します。
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### 必要な拡張機能の追加 {#add-extension}

**拡張機能** は、コアライブラリ設定を管理するコンテナです。 Adobe Target 拡張機能は at.js（最新の web 用 Target JavaScript SDK）によるクライアントサイド実装をサポートしています。次の **Adobe Target** および **AdobeContextHub** 拡張機能。

1. 「拡張機能カタログ」オプションを選択し、フィルターで Target を検索します。
2. 「**Adobe Target** at.js」を選択し、「インストール」オプションをクリックします。
   ![Target 検索 ](assets/search_ext1.png "Target 検索")
3. 「**設定**」ボタンを選択します。設定ウィンドウに、読み込まれた Target アカウントの資格情報と、この拡張機能の at.js バージョンが表示されます。
4. 「**保存**」を選択して、Target 拡張機能を Launch プロパティに追加します。「**インストール済みの拡張機能**」リストの下に Target 拡張機能が表示されます。
   ![拡張機能の保存](assets/configure_extension1.png "拡張機能の保存")
5. 上記の手順を繰り返して、 **AdobeContextHub** 拡張機能をインストールします（この拡張機能は、どのターゲティングがおこなわれているかに基づいて、contexthub パラメーターとの統合に必要です）。

### データ要素の作成 {#data-element}

**データ要素**&#x200B;は、コンテキストハブパラメーターをマッピングできるプレースホルダーです。

1. 「**データ要素**」を選択します。
2. 「**データ要素を追加**」を選択します。
3. データ要素の名前を指定し、コンテキストハブパラメーターにマッピングします。
4. 「**保存**」を選択します。
   ![データ要素](assets/data_elem1.png "データ要素")

### ページルールの作成 {#page-rule}

In **ルール**&#x200B;を定義し、ターゲティングを達成するために、一連のアクション（サイトで実行される）を並べ替えます。

1. スクリーンショットに示されたように、一連のアクションを追加します。
   ![アクション](assets/rules1.png "アクション")
2. 「すべての mbox にパラメーターを追加」で、前に設定したデータ要素（上記のデータ要素を参照）を、mbox 呼び出しで送信されるパラメーターに追加します。
   ![Mbox](assets/map_data1.png " アクション")

### ビルドと公開 {#build-publish}

ビルドと公開の方法については、 [ページ](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html?lang=ja).

## Classic とタッチ操作対応 UI の設定の間のコンテンツ構造の変更 {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>変更点</th>
    <th>クラシック UI の設定</th>
    <th>タッチ操作対応 UI の設定</th>
    <th>結果</th>
  </tr>
  <tr>
    <td>ターゲット設定の場所。</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudconfigs/target/</td>
    <td> 以前は、/etc/cloudservices/testandtarget 内に複数の設定が存在していましたが、現在は 1 つの設定がテナントの下に存在します。</td>
  </tr>
</table>

>[!NOTE]
>
>従来の設定は、既存のお客様でも引き続きサポートされます（編集または作成のオプションはありません）。 レガシー設定は、VSTS を使用して顧客がアップロードしたコンテンツパッケージの一部です。
