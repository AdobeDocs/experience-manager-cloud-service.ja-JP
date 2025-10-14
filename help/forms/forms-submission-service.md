---
title: Edge Delivery ServicesのForms送信サービス
description: AdobeがホストするForms送信サービスを使用して、フォーム送信をスプレッドシートに直接保存します。 Google シート、OneDrive およびSharePoint統合のセットアップ、設定、API 使用について説明します。
keywords: Forms送信サービス，Edge Delivery Services フォーム，スプレッドシート統合，Google シートフォーム，OneDrive フォーム，SharePoint フォーム，フォームデータ収集
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 4ed2444dac60fe08ae3de13f62aa7a400c06473a
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 2%

---

# Edge Delivery ServicesのForms送信サービス

Forms送信サービスは、Adobeがホストするソリューションであり、フォーム送信データを好みのスプレッドシート（Google シート、Microsoft OneDrive、SharePoint）に自動的に直接保存します。 これにより、リアルタイムのデータ収集と管理を実現しながら、複雑なバックエンドインフラストラクチャが不要になります。

## 概要

![Forms送信サービス &#x200B;](/help/forms/assets/form-submission-service.png)
*図：Forms送信サービスのワークフロー – フォーム送信からスプレッドシートストレージへ*

+++ このサービスの利用者

**次に最適：**

- **コンテンツ作成者** シンプルなデータ収集フォームの作成
- **迅速なフォームからスプレッドシートへのワークフローが必要な中小規模企業**
- **マーケティングチーム** リード情報の収集
- **主催者** 登録の管理

**次の代替策を検討してください：**

- カスタムロジックが必要な複雑なワークフロー
- データベースとのエンタープライズ統合
- 高度な検証または処理を必要とするForms

+++

+++ 一般的なユースケース

| ユースケース | 例 | スプレッドシートの利点 |
|----------|---------|-------------------|
| **Formsへのお問い合わせ** | Googleシーツ→ホームページのお問い合わせ | 簡単なフォローアップと CRM のインポート |
| **イベントの登録** | Excel Online での会議→サインアップ | リアルタイムの出席者トラッキング |
| **リードジェネレーション** | SharePoint→のニュースレターのサインアップ | マーケティングキャンペーン分析 |
| **フィードバックの収集** | Google シート→対する調査の回答 | データのクイックビジュアライゼーション |

+++

## 主なメリット

Forms送信サービスには、データ収集を効率化するための次のような利点があります。

+++ 設定の簡素化

- **バックエンドインフラストラクチャなし** 必須 – Adobeは送信エンドポイントをホストします
- 一般的なスプレッドシートプラットフォームを使用した **直接統合**
- フォームフィールドからスプレッドシート列への **自動データマッピング**

+++


+++ リアルタイムデータ管理

- **即時のデータ取得** – 送信された内容は、即座にスプレッドシートに表示されます
- **構造化ストレージ** – 分析を容易にする整理された列
- **ライブコラボレーション** – 複数のチームメンバーがデータにアクセスして分析できます。

+++

+++ 組み込みのセキュリティとアクセス制御

- **既存の権限を活用** - スプレッドシートプラットフォームの共有コントロールを使用します。
- **Adobeで管理されるセキュリティ** - エンタープライズクラスの保護により、送信エンドポイントを保護します
- **データの所有権** - データは、選択したスプレッドシートプラットフォームにとどまります

+++

## 前提条件

Forms送信サービスを設定する前に、次のことを確認してください。



+++ 技術要件

- **GitHub リポジトリ** 最新のアダプティブ Forms ブロックがインストールされたEdge Delivery Services プロジェクト用に設定されます
- **アクセスの承認** - リポジトリが許可リストに追加されました

+++

+++ Spreadsheet Platform の設定


サポートされているプラットフォームを選択します。

- **Google シート** - シート作成権限のあるGoogle アカウント
- **Microsoft OneDrive** - Microsoft 365 アカウント （Excel Online アクセスあり）
- **SharePoint** - リスト/ライブラリ権限を持つSharePoint アクセス

+++

+++ 権限とアクセス

- 対象スプレッドシートの **編集権限**
- **へのアクセスを許可する** 共有機能 `forms@adobe.com`
- 選択したプラットフォームの **リンクの生成** 権限

+++

>[!TIP]
>
>**Edge Delivery Servicesを初めて使用する場合** はじめに [&#x200B; チュートリアル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) から始めて、プロジェクトの基盤を設定します。

## 設定方法

Forms送信サービスには、2 つの設定方法があります。 ワークフローに最適な方法を選択してください。


+++ 設定方法を選択

| メソッド | 次に最適 | 所要時間 | 技術レベル |
|--------|----------|---------------|-----------------|
| **[手動設定](#manual-configuration)** | コンテンツ作成者、1 回限りの設定 | 10～15 分 | 初心者 |
| **[API 設定](#api-configuration)** | 開発者、自動ワークフロー | 5～10 分 | 中級者 |

+++

+++ プロジェクトのセットアップ

どちらの方法を設定する場合でも、事前にAEM プロジェクト基盤の準備が整っていることを確認してください。

1. **AEM プロジェクトを作成または更新** し、最新のアダプティブ Forms ブロックを使用します（[&#x200B; はじめる前にチュートリアル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial)）。

2. **プロジェクトルートの`fstab.yaml`** を更新します。

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **プロジェクトフォルダーの共有** を `forms@adobe.com` と共有する（編集権限が必要）

+++

## 手動設定

![Forms 送信サービスのワークフロー &#x200B;](/help/forms/assets/forms-submission-service-workflow.png)
*図：Forms送信サービスの手動設定の完全なワークフロー*

スプレッドシート送信を使用してフォームを設定するには、次のステップバイステップの手順に従います。



+++ 手順 1：フォーム定義を作成する

Google Sheets またはMicrosoft Excel を使用してフォーム構造を作成します。

**フォーム作成手順：**

1. **スプレッドシートプラットフォームを開く** （Google Sheets またはMicrosoft Excel）
2. フォームプロジェクトの **新しいスプレッドシートの作成**
3. **シートに名前を付ける** （`helix-default` または `shared-aem` のいずれかにする必要があります）
4. **フォーム作成ガイド** 使用した [&#x200B; フォーム構造の定義 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![&#x200B; フォームの定義 &#x200B;](/help/forms/assets/form-submission-definition.png)
*例：フィールドタイプ、ラベル、検証ルールを含むフォーム定義*

>[!IMPORTANT]
>
>**シートの命名要件**
>
>フォーム定義シートには、次のいずれかの名前を付ける必要があります。
>
>- `helix-default` （単一のフォームに推奨）
>- `shared-aem` （マルチフォームプロジェクトの場合）
>
>他のシート名はシステムで認識されません。

**検証チェックポイント：**

- すべての必須フィールドでフォーム構造が完了しています
- シートに正しい名前を付ける（`helix-default` または `shared-aem`）
- フィールドタイプと検証ルールが適切に設定されている

+++

+++ 手順 2：データ収集シートの作成

フォーム送信データを受け取る専用シートを設定します。

**データ シートの設定：**

1. 既存のスプレッドシートに **新しいシートを追加** します
2. **シートに正確に`incoming`** の名前を付ける（大文字と小文字を区別）
3. フォームフィールドに一致する **列ヘッダーの設定**
4. **スプレッドシートを保存** して、変更が保持されるようにします

![&#x200B; 受信シート &#x200B;](/help/forms/assets/form-submission-incoming-sheet.png)
*例：フォームフィールドと一致する列ヘッダーを持つ受信シート*

>[!WARNING]
>
>**重要な要件**
>
>シートの名前は正確に `incoming` （小文字）にする必要があります。 このシートを使用しない場合：
>
>- フォーム送信は拒否されます
>- データは保存されません
>- 送信エラーが表示されます

**検証チェックポイント：**

- シート `incoming` スプレッドシートに存在します
- 列ヘッダーは、フォームフィールド名と一致します
- シートは適切に保存され、アクセス可能です

>[!TIP]
>
>**ヒント：** フォーム定義から正確なフィールド名をコピーして、フォームフィールドとスプレッドシートの列の間で完全に一致するようにします。

+++

+++ 手順 3:Adobe サービスとスプレッドシートを共有する

スプレッドシートへのAdobe Forms送信サービスへのアクセス権を付与します。

**共有プロセス：**

1. スプレッドシートの右上隅にある **「共有」ボタンをクリック** します
2. **Adobe サービスアカウントを追加します。**

   - 電子メール：`forms@adobe.com`
   - 権限レベル：**エディター** （データの書き込みに必要）

3. **共有招待を送信する**
4. 次の手順のために **スプレッドシートリンクをコピー** します

   ![&#x200B; 受信シートの共有 &#x200B;](/help/forms/assets/form-submission-share-incoming.png)
   *Adobe サービスアクセスを許可するためのステップバイステップの共有プロセス*

**プラットフォーム固有の手順：**

**Google シート：**

- `forms@adobe.com` をエディターとして追加
- 「リンクを持つすべてのユーザーが表示できる」が有効になっていることを確認します
- 共有可能なリンクをコピー

**Microsoft Excel （OneDrive/SharePoint）:**

- 編集権限を持つ `forms@adobe.com` を追加
- リンク共有を「リンクを持つすべてのユーザーが編集できる」に設定します
- 共有 URL をコピー

  ![&#x200B; 受信シートのリンクをコピー &#x200B;](/help/forms/assets/form-submission-copy-link.png)
  *例：フォーム設定の共有可能なリンクをコピーする*

**検証チェックポイント：**

- `forms@adobe.com` はスプレッドシートに編集者としてアクセスできます
- スプレッドシートのリンクがコピーされ、使用できるようになりました
- 共有権限による外部アクセス

+++

+++ 手順 4：フォームをスプレッドシートに接続

フォーム定義を送信スプレッドシートにリンクします。

**フォームとスプレッドシートの接続：**

1. **フォーム定義スプレッドシートを開きます** （`helix-default` または `shared-aem` シートが含まれているスプレッドシート）。
2. フォーム定義で **送信フィールドの行を見つけます**
3. **コピーしたスプレッドシートリンク** を送信フィールドの **アクション** 列に貼り付けます
4. フォーム定義に **変更を保存** します

   ![&#x200B; スプレッドシートをリンクする &#x200B;](/help/forms/assets/form-submission-sheet-linking.png)

*例：送信アクションをデータ収集スプレッドシートに接続する*

**フォームの公開：**

1. ブラウザーで **AEM Sidekickを開く**
2. **フォームをプレビュー** して、設定をテストします
3. **フォームを公開** してライブにする

**最終検証：**

- スプレッドシートリンクが「フィールドを送信」アクションに正しく追加される
- フォーム定義が保存され、公開されます
- フォームのプレビューに、すべてのフィールドが正しく表示される
- 「送信」ボタンが正しく設定されている

>[!SUCCESS]
>
>**セットアップが完了しました。** これで、フォームがForms送信サービスに接続されました。 サンプルデータを送信し、`incoming` シートを確認してテストします。

**参考資料：**

- 適切に設定された [&#x200B; 完全なスプレッドシートの例 &#x200B;](/help/forms/assets/spreadsheet.xlsx)
- 公開ガイダンスの [AEM Sidekick ドキュメント &#x200B;](https://www.aem.live/docs/sidekick)

+++

## API 設定

この API メソッドを使用すると、開発者はプログラムによってデータをForms送信サービスに送信できます。これは、自動ワークフローとカスタム統合に最適です。


+++ API を使用すべき状況

**次に最適：**

- 自動データ収集システム
- カスタムフォームの実装
- 既存のアプリケーションとの統合
- 一括データ送信ワークフロー

+++

+++ API の前提条件

API を使用する前に、次のことを確認します。

- **スプレッドシート設定** 完了（`incoming` シートを含む）
- **Adobe サービスアクセス** が `forms@adobe.com` に付与されました
- 公開済みフォームの **フォーム ID**
- **リポジトリ情報** （組織およびサイト名）

>[!IMPORTANT]
>
>**必要な設定手順**
>
>この API では、手動設定と同じスプレッドシート設定が必要です。
>
>- `incoming` シートが存在する必要があります
>- `forms@adobe.com` は編集者のアクセス権が必要です
>- シートはAEM Sidekickからパブリッシュする必要があります

+++

+++ API エンドポイントと認証

**ベース URL:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**必須ヘッダー：**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**API ドキュメント：**&#x200B;[&#x200B; 完全な API リファレンス &#x200B;](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ Postmanの使用

Postmanは、API 送信をテストするための使いやすいインターフェイスを提供します。

**設定手順：**

1. Postmanでの **新しい POST リクエストの作成**
2. **エンドポイントを設定します：** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **プレースホルダーを置換：**
   - 実際→フォーム ID を `{id}` します
   - `[repository]` → GitHub リポジトリ名
   - `[organization]` → GitHub 組織/ユーザー名

**リクエスト設定：**

```json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Headers:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main--your-repo--your-org

Body (JSON):
{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Mary",
            "age": "35",
            "subscribe": null,
            "email": "mary@gmail.com"
                }
}
```

**期待される応答：**

- **状態コード：** `201 Created`
- **データがすぐに** スプレッドシート シートに表示されます `incoming`

![postman 画面 &#x200B;](/help/forms/assets/postman-api.png)
*例：Postman インターフェイスを使用した API 送信の成功*

+++

+++ コマンドライン（curl）の使用

ターミナル/コマンドプロンプトを希望する開発者は、curl を使用してプログラムによりデータを送信します。

**コマンドライン設定：**

以下のコマンドの次のプレースホルダーを置き換えます。

- 実際→フォーム ID を `{id}` します
- `[repository]` → GitHub リポジトリ名
- `[organization]` → GitHub 組織/ユーザー名

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
```

>[!TAB Windows コマンドプロンプト ]

```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
```

>[!ENDTABS]

+++

+++ API の応答と検証

**成功した応答：**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**データ検証：**

送信に成功したら、データがスプレッドシートに表示されることを確認します。

![&#x200B; 更新されたシート &#x200B;](/help/forms/assets/updated-sheet.png)
*例：データが API を介して受信シートに正常に書き込まれた*

**応答の検証：**

- **HTTP ステータス：** `201 Created` は、送信が成功したことを示します
- **X-Request-Id:** 送信をトラッキングするための一意の識別子
- **データが** 秒以内に `incoming` シートに表示されます
- **すべてのフォームフィールド** は、スプレッドシートの列に正しくマッピングされます

+++

## トラブルシューティング



+++ よくある問題と解決策

**問題：403 Forbidden エラー**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**問題：404 エラーが見つかりません**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**問題：スプレッドシートにデータが表示されない**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**問題：無効な JSON 形式のエラー**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


+++

+++ ヘルプの表示

**サポートチャネル：**

- **アーリーアクセスの問題：** 電子メール [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **API ドキュメント：**&#x200B;[&#x200B; 開発者向けリファレンス &#x200B;](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **コミュニティサポート：**&#x200B;[Adobe Experience League コミュニティ &#x200B;](https://experienceleaguecommunities.adobe.com/?profile.language=ja)

+++

## 次の手順

Forms送信サービスを設定したので、次の関連トピックを参照してください。


+++ Formsの強化

- **[詳細Formsの作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** – 検証、条件付きロジック、カスタムスタイル設定を追加します
- **[フォームコンポーネントガイド &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** – 使用可能なフォームフィールドタイプを調べます

+++

+++ 代替送信方法

- **[AEM送信内容の公開](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** – 複雑なワークフローおよび企業の統合の場合
- **[カスタム送信アクション](/help/forms/configure-submit-actions-core-components.md)** – 高度な送信処理

+++

+++ データ管理

- **[Form Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)** - フォームのパフォーマンスと使用状況の追跡
- **[データ統合](/help/forms/configure-data-sources.md)** - フォームをデータベースおよび CRM システムに接続します

+++

## 概要

Forms送信サービスは、フォームデータをスプレッドシートに直接収集するための強力なコードレスのソリューションです。 主なメリットは次のとおりです。

- **クイックセットアップ** - バックエンドインフラストラクチャは不要
- **リアルタイムデータ** – 即時の送信キャプチャ
- **柔軟なプラットフォーム** - Google Sheets、OneDrive、SharePoint
- **API アクセス** - プログラムによる送信機能
- **エンタープライズセキュリティ** - Adobeが管理する、アクセス制御のあるエンドポイント

**使用を開始する準備はできていますか？** 視覚的な設定の場合は [&#x200B; 手動設定 &#x200B;](#manual-configuration) ガイドに従い、プログラムによる統合の場合は [API 設定 &#x200B;](#api-configuration) に移動します。
