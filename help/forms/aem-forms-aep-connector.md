---
title: AEM FormsとAdobe Experience Platformの接続（AEP） | データ統合ガイド
description: AEM FormsをAdobe Experience Platformと統合して、顧客プロファイルの活用、フォームデータの送信、パーソナライズされたエクスペリエンスの作成をおこなう方法について説明します。 ステップバイステップガイド。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: b0eb19d3-0297-4583-8471-edbb7257ded4
source-git-commit: 628e60e43d0810ef9e871dd77ed1674d7646072b
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 2%

---

# AEM Forms と Adobe Experience Platform（AEP）の統合 {#aem-forms-aep-integration}

<span class="preview"> アダプティブForms（AEM Forms）とAdobe Experience Platform（AEP）を連携させる機能は、早期アクセスプログラムに基づいています。 機能へのアクセスをリクエストするには、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D) にメールを送信するだけです。 また、<a href="/help/forms/early-access-ea-features.md"> 早期アクセスプログラム </a> ページでは、利用可能なすべてのイノベーションと機能を確認できます。. </span>

## 概要 {#overview}

AEM FormsをAdobe Experience Platformと接続して、フォームエクスペリエンスを変換できます。 この強力な統合機能により、組織は、パーソナライズされたフォームエクスペリエンスにリアルタイム顧客プロファイルを活用したり、**Experience PlatformへのAEM Forms データ送信を効率化したり** Adobe エコシステム全体で統合された顧客レコードを作成したりできます。 アダプティブフォームをExperience Platformの堅牢なデータ管理機能に接続することで、顧客データの情報源を一元化しながら、より関連性の高いエクスペリエンスを作成し、コンバージョン率を向上させることができます。

### AEM Forms Connector for Adobe Experience Platform（AEP）とは {#what-is-connector}

Adobe Experience Platform（AEP）用AEM Forms コネクタは、AEM Formsが提供する標準搭載（OOTB）コネクタで、AEM FormsとAdobe Experience Platform（AEP）のシームレスな統合を可能にします。 この統合により、AEPで使用可能な XDM スキーマを使用してフォームを作成し、パーソナライゼーションやプロファイルのハイドレーションの目的でデータをAEPに送信することができます。

## AEM FormsをAdobe Experience Platform（AEP）と接続する理由 {#benefits}

アダプティブFormsとAdobe Experience Platformを接続すると、組織とお客様の両方に次の大きな利点があります。

* **統合顧客プロファイル** - フォーム送信データを使用して顧客プロファイルを強化し、顧客のインタラクションと好みを包括的に把握できます
* **パーソナライズされたフォームエクスペリエンス** – 既存のプロファイルデータを活用してフィールドに事前入力し、既知の顧客情報に基づいてフォームをカスタマイズします
* **効率的なデータ収集** - カスタムコネクタや統合コードを作成せずに、フォームデータをAEP データセットに直接キャプチャします
* **リアルタイムデータのアクティベーション** - フォーム送信データをReal-Time CDPを通じて他のAdobe アプリケーションに送信し、即座にアクティベーションを行います
* **シンプルなコンプライアンス管理** - AEPを使用して、同意およびデータガバナンスポリシーを一元的に管理します
* **開発時間の短縮** - ベストプラクティスに従った事前定義済みコネクタを使用すると、カスタム統合作業が不要になります
* **フォームデータによる顧客プロファイルのエンリッチメント** - フォームが送信されるたびに顧客プロファイルを自動的に更新および強化し、より豊富な顧客インサイトを作成します

## 主な機能 {#key-features}

* AEP XDM スキーマを使用したフォームの作成
* パーソナライゼーションのためにフォームデータをAEPに送信する
* ストリーミングデータ取り込みのサポート
* ユーザーエクスペリエンスを向上させるためにプロファイルのハイドレーションを有効にする
* AEP プロファイルシステムとの統合
* 標準化されたデータ収集用のアダプティブフォームとの XDM スキーマ統合
* フォーム用のAEP ストリーミング接続によるリアルタイムデータ処理の実現

次のビデオでは、スキーマの作成、データ設定と認証などの前提条件に関する手順と、Adaptive FormsをAdobe Experience Platform（AEP）に作成して接続する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

## 前提条件 {#prerequisites}

AEM FormsでAEP コネクタを設定する前に、Adobe Experience Platformで次の手順を完了していることを確認してください。

1. スキーマの設定
   * [XDM スキーマの作成 ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [ プロファイル用にスキーマを有効にする ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [ID フィールドを定義 ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. データ設定
   * [ データセットの作成 ](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [ ストリーミング接続の設定 ](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/tutorials/create-streaming-connection) （ストリーミングエンドポイント URL は後で必要になるので、今すぐメモを取ります）。

3. 認証
   * Adobe Developer Consoleから [API 資格情報を生成 ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) （クライアント ID およびクライアント秘密鍵）


## 実装手順

### &#x200B;1. AEP クラウド設定の作成

1. **Adobe Experience Manager インスタンス** / **ツール** / **Cloud Services** / **Adobe Experience Platform** に移動します。
1. **設定コンテナ** を選択して、設定を保存します。
1. **作成** をクリックして、AEP設定ウィザードを開きます
1. 以下の詳細を入力します。
   * タイトル
   * クライアント ID （developer console から取得）
   * クライアントの秘密鍵（developer console から取得）
   * OAuth URL （デフォルトの URL がありますが、開発者コンソールからも取得できます）

   ![AEP クラウド設定 ](/help/forms/assets/aep-cloud-configuration.png)

1. **接続** をクリックして、接続を確立します。 接続を確立したら、次の追加設定を行います。
   * ベース URL:platform.adobe.io （これはデフォルトの URL で、開発者コンソールから取得できます。oauth および platform の URL は実稼動 URL にデフォルト設定されます。 場合によっては、ステージに接続する必要があります（ステージ URL を使用する必要があります）。
   * 組織 ID （これは、クライアント ID/シークレットと共に Developer Console から取得されます）
   * サンドボックス名（開発環境と実稼動環境の両方で必要）

### &#x200B;2. XDM スキーマ統合によるフォームの作成 {#form-creation}

1. フォーム作成ウィザードにアクセスします。
   * **Adobe Experience Manager インスタンス** / **Forms** / **Formsとドキュメント** に移動します。
   * **作成**/**アダプティブフォーム** をクリックします。
1. 「**ソース**」タブで、テンプレートを選択します
1. 「**Data**」タブで、「**Adobe Experience Platform**」オプションを選択します。

1. プロパティペインで、クラウド設定を選択します。

   ![](/help/forms/assets/xdm-schema-integration.png)

   使用可能なすべてのスキーマがAdobe Experience Platformから読み込まれます

   >[!NOTE]
   >
   >
   > * プロファイルが有効なスキーマとシステムで生成されていないスキーマのみが取得されます。
   > * 最初のスキーマの読み込みには、時間がかかる場合があります。

1. スキーマの適切なフィールド/必須フィールドを選択します。 （詳しい手順についてはビデオを参照してください）
1. 「送信」タブで、次の手順に従います。
   * **Adobe Experience Platformに送信** 送信アクションを選択します
   * Experience Platformへの **AEM Forms データ送信のフォーム送信設定を指定します**
1. プロパティパネルで、次の操作を行います。
   * ストリーミング URL を追加します（AEP ソース/ストリーミング接続から取得）。
   * データフロー ID を追加します（AEP ソース/フロー/API の使用状況に関する情報で検出）。
1. 「**保存**」をクリックします。 フォームの詳細を入力します。
   * タイトル
   * 名前
   * ストレージパス
1. 送信ボタンをフォームに追加します。 フォームが、AEPにデータを送信する準備ができました。


## 重要な注意事項 {#important-notes}

* フォームを通じて送信されたデータは、約 10～15 分後にAEPに表示されます
* デフォルトでは、プロファイルが有効になっているスキーマのみが表示されます
* データ送信はすべてのスキーマで機能しますが、事前入力機能はプロファイルが有効になっているスキーマに限定されます
* プロファイルが有効になっていないスキーマのデータは、後でプロファイルが有効になった場合でも、プロファイルの作成には使用されません
* **フォームデータを使用した顧客プロファイルエンリッチメント** には、XDM スキーマで適切な ID フィールド設定が必要です
* **Experience PlatformへのAEM Forms データ送信** は、フォームの **AEP ストリーミング接続を使用して** リアルタイムのデータフローを確保します

## ベストプラクティス {#best-practices}

1. プロファイルを有効にする前に、スキーマ構造を慎重に計画します
1. **フォームのAEP ストリーミング接続を設定する際は、データ量とシステムのスケーリング要件を考慮してください**
1. 実稼動デプロイメントの前に、統合のテストを十分に行ってください
1. データ取り込みプロセスとプロファイル作成プロセスの監視
1. 必要なデータのみを収集するように、**XDM スキーマとアダプティブフォームの統合** をデザインします
1. **フォームデータを使用した顧客プロファイルのエンリッチメント** を戦略的に使用して、パーソナライゼーションを強化する

## 技術上の考慮事項 {#technical-considerations}

* コネクタは、データ送信にパブリックストリーミング API を使用します
* プロファイルの作成は、ID フィールドに基づきます
* AEPでのデータ統合は自動的に行われます
* この統合では、新しいフォームの作成と既存のフォームの変更の両方をサポートしています
* アダプティブフォームとの XDM スキーマ統合は、異なるタッチポイント間でデータ構造を標準化します
* forms のAEP ストリーミング接続は、リアルタイムのデータ取得機能を提供します

## よくある質問（FAQ） {#faq}

### 一般的な質問 {#general-questions}

**Q:「このコネクタは、AEM Formsの複数の製品で使用できますか？**
回答：いいえ。この統合は、AEM Forms as a Cloud Serviceでのみ使用でき、早期アクセス プログラムの下にあります。

**Q：このコネクタは、アダプティブ Forms コアコンポーネントと基盤コンポーネントの両方で動作しますか？**
回答：このコネクタは、アダプティブFormsコアコンポーネントとアダプティブForms基盤コンポーネントの両方で機能します。

**Q:1 つのフォームから複数のAEP データセットにデータを送信できますか？**
A：現在、各フォームは 1 つのデータセットにのみ送信できます。

**Q：処理可能なフォーム送信の数に制限はありますか。**
回答：フォームの送信は、AEPのストリーミング取り込み [ 割り当て量とレート制限 ](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/api/quota) の影響を受けます。

<!-- >
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### 実装に関する質問 {#implementation-questions}

**Q:AEM FormsとAEP間の接続の問題をトラブルシューティングする方法を教えてください。**
回答：クラウド設定を確認し、API 資格情報が正しいことを確認し、ストリーミングエンドポイント URL が正しく設定されていることを確認します。

**Q：この統合でカスタム XDM スキーマを使用できますか？**
A：はい。AEPで適切に設定され、事前入力機能としてプロファイルに対して有効になっている限り、任意のカスタム XDM スキーマを使用できます。

**Q:AEP プロファイルデータを使用したフォームの事前入力を有効にするにはどうすればよいですか？**
回答：スキーマがプロファイル対応であり、スキーマで定義されているのと同じ ID フィールドを使用するようにフォームが設定されていることを確認します。

**Q：データをAEPに送信する前に変換する必要がある場合はどうすればよいですか？**
回答：送信前にフォームルールまたはカスタム関数を使用して、データを変換できます。 複雑な変換の場合は、カスタム送信アクションの使用を検討してください。

**Q：この統合をハイブリッドデプロイメントモデルで使用できますか？**
A：いいえ。この統合は、AEM Forms as a Cloud Serviceに固有の機能です。

## 概要と次の手順 {#summary-next-steps}

AEM FormsとAdobe Experience Platformの統合により、企業はフォームとより広範なExperience Platform エコシステムとの間でシームレスなデータフローを実現できます。 この統合により、よりパーソナライズされたフォームエクスペリエンスを作成し、データ収集を効率化し、貴重なフォーム送信データで顧客プロファイルを強化できるようになります。

この統合を開始するには：

1. **アクセスの要求** – まだ参加していない場合は、[aem-forms-ea@adobe.comに連絡して早期アクセス プログラムに参加してください ](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)
2. **環境の準備** - AEM FormsとAdobe Experience Platformの両方で必要な権限および設定があることを確認します
3. **実装手順に従う** – 上記のガイドを使用してクラウド設定をセットアップし、XDM スキーマ統合を使用した最初のAEP接続フォームを作成します
4. **十分にテスト** – 開発環境でのデータ送信機能と事前入力機能の両方の検証
5. **実稼動用に計画** – 実装チームと協力して、AEM Forms データ送信のExperience Platformへの実稼動環境でのデプロイメントをスケジュールします

## 関連リソース {#related-resources}

* [AEM Forms as a Cloud Service ドキュメント ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja)
* [Adobe Experience Platform ドキュメント ](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=ja)
* [XDM システムの概要 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ja)
* [Adobe Experience Platformでのストリーミング取得 ](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html)
* [ リアルタイム顧客プロファイルの概要 ](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [AEM Formsの早期アクセス機能](/help/forms/early-access-ea-features.md)
* [コアコンポーネントを使用したアダプティブFormsの作成](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Formsでのフォームデータモデルの使用](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->
