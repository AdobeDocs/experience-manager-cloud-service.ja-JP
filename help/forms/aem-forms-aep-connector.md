---
title: AEM Forms と Adobe Experience Platform（AEP）の接続 | データ統合ガイド
description: AEM Forms を Adobe Experience Platform と統合して、顧客プロファイルを活用し、フォームデータを送信し、パーソナライズされたエクスペリエンスを作成する方法について説明します。ステップバイステップガイド。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: b0eb19d3-0297-4583-8471-edbb7257ded4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 100%

---

# AEM Forms と Adobe Experience Platform（AEP）の統合 {#aem-forms-aep-integration}

<span class="preview">アダプティブフォーム（AEM Forms）を Adobe Experience Platform（AEP）に接続する機能は、早期アクセスプログラムに基づいています。この機能へのアクセス権をリクエストするには、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D) にメールを送信するだけです。また、<a href="/help/forms/early-access-ea-features.md">早期アクセスプログラム</a>ページにアクセスして、使用可能なすべてのイノベーションと機能を確認することもできます。</span>

## 概要 {#overview}

AEM Forms を Adobe Experience Platform に接続して、フォームエクスペリエンスを変換できます。この強力な統合により、組織はリアルタイムの顧客プロファイルを活用してパーソナライズされたフォームエクスペリエンスを実現し、**Experience Platform への AEM Forms データの送信**&#x200B;を効率化し、Adobe エコシステム全体で統合された顧客レコードを作成できます。アダプティブフォームを Experience Platform の強力なデータ管理機能に接続することで、お客様データの信頼できる唯一の情報源を維持しながら、より関連性の高いエクスペリエンスを作成し、コンバージョン率を向上させることができます。

### Adobe Experience Platform（AEP）用 AEM Forms コネクタとは {#what-is-connector}

Adobe Experience Platform（AEP）用 AEM Forms コネクタは、AEM Forms によって提供される標準（OOTB）コネクタであり、AEM Forms と Adobe Experience Platform（AEP）間のシームレスな統合を可能にします。この統合により、AEP で使用可能な XDM スキーマを使用してフォームを作成し、パーソナライゼーションとプロファイルハイドレーションの目的でデータを AEP に送信できます。

## AEM Forms を Adobe Experience Platform（AEP）と接続する理由 {#benefits}

Adaptive Forms を Adobe Experience Platform に接続すると、組織と顧客の両方に次の大きなメリットがもたらされます。

* **統合顧客プロファイル** - フォーム送信データで顧客プロファイルを強化させ、顧客とのインタラクションや好みの包括的なビューを作成します
* **パーソナライズされたフォームエクスペリエンス** - 既存のプロファイルデータを活用してフィールドを事前入力し、既知の顧客情報に基づいてフォームをカスタマイズします
* **効率化されたデータ収集** - カスタムコネクタや統合コードを作成せずに、フォームデータを AEP データセットに直接キャプチャします
* **リアルタイムデータのアクティベーション** - フォーム送信データを Real-Time CDP を通じて他のアドビアプリケーションに送信し、即座にアクティブ化します。
* **簡素化されたコンプライアンス管理** - AEP を通じて同意とデータガバナンスポリシーを一元化します。
* **開発時間の短縮** - ベストプラクティスに従った事前定義済みコネクタにより、カスタム統合作業が不要になります
* **フォームデータによる顧客プロファイルのエンリッチメント** - フォームの送信ごとに顧客プロファイルを自動的に更新および強化し、よりリッチな顧客インサイトを作成します

## 主な機能 {#key-features}

* AEP XDM スキーマを使用してフォームを作成
* パーソナライゼーション用にフォームデータを AEP に送信
* ストリーミングデータ取り込みのサポート
* ユーザーエクスペリエンスを向上させるためにプロファイルのハイドレーションを有効にする
* AEP のプロファイルシステムとの統合
* 標準化されたデータ収集用のアダプティブフォームとの XDM スキーマ統合
* リアルタイムデータ処理を可能にするフォーム用の AEP ストリーミング接続

次のビデオでは、前提条件（スキーマの作成、データ設定の指定、認証など）に関するステップバイステップのガイドを示し、アダプティブフォームを作成して Adobe Experience Platform（AEP）に接続する方法について説明します

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

<span>このビデオは、コアコンポーネントのみに適用されます。UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

## 前提条件 {#prerequisites}

AEM Forms で AEP コネクタを設定する前に、Adobe Experience Platform で次の作業が完了していることを確認します。

1. スキーマの設定
   * [XDM スキーマを作成](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [プロファイリング用にスキーマを有効にする](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [ID フィールドを定義](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. データ設定
   * [データセットを作成](https://experienceleague.adobe.com/ja/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [ストリーミング接続を設定](https://experienceleague.adobe.com/ja/docs/experience-platform/ingestion/tutorials/create-streaming-connection)（ストリーミングエンドポイント URL は後で必要になるので、今すぐメモを取ります。）

3. 認証
   * Adobe Developer Console から [API 資格情報を生成](https://experienceleague.adobe.com/ja/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials)（クライアント ID およびクライアント秘密鍵）


## 実装手順

### &#x200B;1. AEP クラウド設定の作成

1. **Adobe Experience Manager インスタンス**／**ツール**／**Cloud Services**／**Adobe Experience Platform** に移動します。
1. **設定コンテナ**&#x200B;を選択して、設定を保存します。
1. 「**作成**」をクリックして、AEP 設定ウィザードを開きます
1. 次の詳細を入力します。
   * タイトル
   * クライアント ID（Developer Console から取得）
   * クライアント秘密鍵（Developer Console から取得）
   * OAuth URL（デフォルトの URL がありますが、Developer Console からも取得できます）

   ![AEP クラウド設定](/help/forms/assets/aep-cloud-configuration.png)

1. 「**接続**」をクリックして接続を確立します。接続を確立したら、次の追加設定を行います。
   * ベース URL：platform.adobe.io（これはデフォルトの URL で、Developer Console からも取得できます。OAuth および Platform URL はデフォルトで実稼動 URL に設定されています。ステージに接続する必要がある場合は、ステージ URL を使用する必要があります。）
   * 組織 ID（これは、クライアント ID／秘密鍵と共に Developer Console から取得されます）
   * サンドボックス名（開発環境と本番環境の両方で必要）

### &#x200B;2. XDM スキーマ統合によるフォームの作成 {#form-creation}

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

スキーマ統合を使用して基盤コンポーネントに基づいてアダプティブフォームを作成するには、次の手順を実行します。

1. フォーム作成ウィザードにアクセスします。
   * **Adobe Experience Manager インスタンス**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   * **作成**／**アダプティブフォーム**&#x200B;をクリックします。
1. 「**ソース**」タブで、基盤テンプレートを選択します。
1. 「**データ**」タブで、**Adobe Experience Platform** オプションを選択します。
1. プロパティパネルで、クラウド設定を選択します。

   ![](/help/forms/assets/xdm-schema-integration.png)

   使用可能なすべてのスキーマが Adobe Experience Platform から読み込まれます

   >[!NOTE]
   >
   >
   > * プロファイルが有効なスキーマとシステムで生成されていないスキーマのみが取得されます。
   > * 初回設定時には、最初のスキーマの読み込みに時間がかかる場合があります。

1. スキーマの適切なフィールド／必須フィールドを選択します（詳しい手順について詳しくは、ビデオをご覧ください）。
1. 「送信」タブで、次の操作を実行します。
   * **REST エンドポイントに送信**&#x200B;送信アクションを選択します
   * **Experience Platform への AEM Forms データ送信**&#x200B;のフォーム送信設定を指定します
1. プロパティパネルで、次の操作を実行します。
   * ストリーミング URL を追加します（AEP ソース／ストリーミング接続から取得）
   * データフロー ID を追加します（AEP ソース／フロー／API の使用状況に関する情報で検出）。
1. 「**保存**」をクリックします。フォームの詳細を指定します。
   * タイトル
   * 名前
   * ストレージパス
1. 送信ボタンをフォームに追加します。フォームで AEP にデータを送信する準備ができました。

>[!TAB コアコンポーネント]

スキーマ統合を使用してコアコンポーネントに基づいてアダプティブフォームを作成するには、次の手順を実行します。

1. フォーム作成ウィザードにアクセスします。
   * **Adobe Experience Manager インスタンス**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   * **作成**／**アダプティブフォーム**&#x200B;をクリックします。
1. 「**ソース**」タブで、コアコンポーネントベースのテンプレートを選択します。
1. 「**データ**」タブで、**Adobe Experience Platform** オプションを選択します。
1. プロパティパネルで、クラウド設定を選択します。

   ![](/help/forms/assets/xdm-schema-integration.png)

   使用可能なすべてのスキーマが Adobe Experience Platform から読み込まれます

   >[!NOTE]
   >
   >
   > * プロファイルが有効なスキーマとシステムで生成されていないスキーマのみが取得されます。
   > * 初回設定時には、最初のスキーマの読み込みに時間がかかる場合があります。

1. スキーマの適切なフィールド／必須フィールドを選択します（詳しい手順について詳しくは、ビデオをご覧ください）。
1. 「送信」タブで、次の操作を実行します。
   * **REST エンドポイントに送信**&#x200B;送信アクションを選択します
   * **Experience Platform への AEM Forms データ送信**&#x200B;のフォーム送信設定を指定します
1. プロパティパネルで、次の操作を実行します。
   * ストリーミング URL を追加します（AEP ソース／ストリーミング接続から取得）
   * データフロー ID を追加します（AEP ソース／フロー／API の使用状況に関する情報で検出）。
1. 「**保存**」をクリックします。フォームの詳細を指定します。
   * タイトル
   * 名前
   * ストレージパス
1. 送信ボタンをフォームに追加します。フォームで AEP にデータを送信する準備ができました。

>[!TAB ユニバーサルエディター]

スキーマ統合を使用してユニバーサルエディターを使用してアダプティブフォームを作成するには、次の手順を実行します。

1. フォーム作成ウィザードにアクセスします。
   * **Adobe Experience Manager インスタンス**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   * **作成**／**アダプティブフォーム**&#x200B;をクリックします。
1. 「**ソース**」タブで、Edge Delivery ベースのテンプレートを選択します。
1. 「**データ**」タブで、**Adobe Experience Platform** オプションを選択します。
1. プロパティパネルで、クラウド設定を選択します。

   ![スキーマの統合](/help/forms/assets/xdm-schema-integration.png)

   使用可能なすべてのスキーマが Adobe Experience Platform から読み込まれます

   >[!NOTE]
   >
   >
   > * プロファイルが有効なスキーマとシステムで生成されていないスキーマのみが取得されます。
   > * 初回設定時には、最初のスキーマの読み込みに時間がかかる場合があります。

1. スキーマの適切なフィールド／必須フィールドを選択します（詳しい手順について詳しくは、ビデオをご覧ください）。
1. 「送信」タブで、次の操作を実行します。
   * **REST エンドポイントに送信**&#x200B;送信アクションを選択します
   * **Experience Platform への AEM Forms データ送信**&#x200B;のフォーム送信設定を指定します

     >[!NOTE]
     >
     >* ユニバーサルエディターインターフェイスの「データソース」アイコンや、右側のプロパティパネルの連結参照プロパティが表示されない場合は、Extension Manager で&#x200B;**データソース**&#x200B;拡張機能を有効にします。
     >* ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Manager で&#x200B;**フォームプロパティを編集**&#x200B;拡張機能を有効にします。
     > 
     >* ユニバーサルエディターで拡張機能を有効または無効にする方法については、[Extension Manager 機能のハイライト](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)の記事を参照してください。

   ユニバーサルエディターのフォームの事前入力サービスは、現在サポートされていません。

1. プロパティパネルで、次の操作を実行します。
   * ストリーミング URL を追加します（AEP ソース／ストリーミング接続から取得）
   * データフロー ID を追加します（AEP ソース／フロー／API の使用状況に関する情報で検出）。
1. 「**保存**」をクリックします。フォームの詳細を指定します。
   * タイトル
   * 名前
   * ストレージパス
1. 送信ボタンをフォームに追加します。フォームで AEP にデータを送信する準備ができました。

>[!ENDTABS]

## 重要な注意事項 {#important-notes}

* フォームを通じて送信されたデータは、約 10～15 分後に AEP に表示されます
* デフォルトでは、プロファイルが有効になっているスキーマのみが表示されます
* データ送信はすべてのスキーマで機能しますが、事前入力機能はプロファイルが有効になっているスキーマに制限されます
* プロファイルが有効になっていないスキーマのデータは、後でスキーマがプロファイリング用に有効になった場合でも、プロファイルの作成には使用されません
* **フォームデータを使用した顧客プロファイルエンリッチメント**&#x200B;には、XDM スキーマで適切な ID フィールド設定が必要です
* **Experience Platform への AEM Forms データ送信**&#x200B;では、フォームの **AEP ストリーミング接続**&#x200B;を使用して、リアルタイムのデータフローを確保します

## ベストプラクティス {#best-practices}

1. プロファイリングを有効にする前に、スキーマ構造を慎重に計画します
1. **フォームの AEP ストリーミング接続**&#x200B;を設定する際は、データ量とシステムのスケーリング要件を考慮します
1. 実稼動デプロイメントの前に、統合を徹底的にテストします
1. データ取り込みとプロファイル作成のプロセスを監視します
1. 必要なデータのみを収集するように&#x200B;**アダプティブフォームとの XDM スキーマ統合**&#x200B;をデザインします
1. パーソナライゼーションを強化するために、**フォームデータを使用した顧客プロファイルのエンリッチメント**&#x200B;を戦略的に使用します

## 技術的な考慮事項 {#technical-considerations}

* コネクタは、データ送信にパブリックストリーミング API を使用します
* プロファイルの作成は、ID フィールドに基づきます
* AEP では、データ統合が自動的に行われます
* 統合では、新しいフォームの作成と既存のフォームの変更の両方がサポートされます
* スキーマとアダプティブフォームの統合により、様々なタッチポイントをまたいでデータ構造が標準化されます
* フォームの AEP ストリーミング接続では、リアルタイムのデータ取り込み機能を提供します

## よくある質問（FAQ） {#faq}

### 一般的な質問 {#general-questions}

**Q：「このコネクタは、AEM Forms の複数の製品で使用できますか？**
A：いいえ、この統合は AEM Forms as a Cloud Service でのみ使用可能であり、早期アクセスプログラムに基づいています。

**Q：このコネクタは、アダプティブフォームコアコンポーネントと基盤コンポーネントの両方で動作しますか？**
A：このコネクタは、アダプティブフォームコアコンポーネントとアダプティブフォーム基盤コンポーネントの両方で動作します。

**Q：単一のフォームから複数の AEP データセットにデータを送信できますか？**
A：現在、各フォームは 1 つのデータセットにのみ送信できます。

**Q：処理できるフォーム送信数に制限はありますか？**
A：フォームの送信は、AEP ストリーミング取得[クォータとレート制限](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/api/quota)の対象となります。

<!-- 
>
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### 実装に関する質問 {#implementation-questions}

**Q：AEM Forms と AEP 間の接続の問題をトラブルシューティングするにはどうすればよいですか？**
A：クラウド設定を検証し、API 資格情報が正しいことを確認し、ストリーミングエンドポイント URL が適切に設定されていることを確認します。

**Q：この統合でカスタム XDM スキーマを使用できますか？**
A：はい、AEP で適切に設定され、事前入力機能がプロファイルに対して有効になっている限り、任意のカスタム XDM スキーマを使用できます。

**Q：AEP プロファイルデータを使用してフォームの事前入力を有効にするにはどうすればよいですか？**
A：スキーマがプロファイル対応であり、フォームがスキーマで定義されているものと同じ ID フィールドを使用するように設定されていることを確認します。

**Q：AEP に送信する前にデータを変換する必要がある場合はどうすればよいですか？**
A：フォームルールまたはカスタム関数を使用して、送信前にデータを変換できます。複雑な変換の場合は、カスタム送信アクションの使用を考慮します。

**Q：この統合をハイブリッドデプロイメントモデルで使用できますか？**
A：いいえ。この統合は、AEM Forms as a Cloud Service に固有です。

## 概要と次の手順 {#summary-next-steps}

AEM Forms と Adobe Experience Platform の統合により、組織はフォームとより広範な Experience Platform エコシステムの間でシームレスなデータフローを作成できます。この統合により、よりパーソナライズされたフォームエクスペリエンスを作成し、データ収集を効率化し、貴重なフォーム送信データを使用して顧客プロファイルを強化できます。

この統合を開始するには：

1. **アクセスをリクエスト** - まだ参加していない場合は、[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D) に連絡して早期アクセスプログラムに参加してください
2. **環境を準備** - AEM Forms と Adobe Experience Platform の両方で必要な権限と設定があることを確認します
3. **実装手順に従う** - 上記のガイドを使用してクラウド設定を指定し、XDM スキーマ統合を使用して最初の AEP 接続フォームを作成します
4. **徹底的にテスト** - 開発環境でデータの送信機能と事前入力機能の両方を検証します
5. **実稼動用に計画** - 実装チームと連携して、実稼動環境の Experience Platform への AEM Forms データ送信のデプロイメントをスケジュールします

## 関連リソース {#related-resources}

* [AEM Forms as a Cloud Service ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja)
* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=ja)
* [XDM システムの概要](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ja)
* [Adobe Experience Platform でのストリーミング取得](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=ja)
* [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [AEM Forms の早期アクセス機能](/help/forms/early-access-ea-features.md)
* [コアコンポーネントを使用したアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Forms でのフォームデータモデルの使用](/help/forms/using-form-data-model.md)

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
