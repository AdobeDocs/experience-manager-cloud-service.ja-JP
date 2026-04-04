---
title: AEM Forms Communications API – 概要
description: 認証方法と完全なAPI リファレンスを含むAEM Forms Communications APIの概要
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 1f9fb00c-c284-45c1-a8ba-51a59dbaee3d
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 10%

---

# AEM Forms Communications API – 概要

AEM Forms APIは、ドキュメントワークフローの自動化を支援するために設計された、包括的なクラウドネイティブ API スイートを提供します。

AEM Forms APIは、構造化されており、次の2つの主要コンソールからアクセスできます。

* [Adobe Developer Console （ADC） &#x200B;](https://developer.adobe.com/developer-console/) - Adobe Developer Consoleは、Adobe API、Events、Runtime、およびApp Builderへのゲートウェイです。

* [AEM Developer Console](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Consoleでは、環境レベルの詳細、設定、テクニカルアカウント、サービス資格情報へのアクセス権を提供し、運用タスクと統合タスクをサポートします。

異なるAPIは、異なる[認証方法](#authentication-methods)をサポートしています。

## 認証方法

様々なForms APIでは、リリースタイムラインに基づいて様々な認証方法を使用します。

* [OAuth サーバー間](/help/forms/oauth-api-authetication.md)
* [JWT （JSON Web トークン） サーバー間](/help/forms/jwt-api-authentication.md)

以前のAPIでは、AEM Developer Consoleを通じて設定および管理されるJWT ベースのサーバー間認証をサポートしていました。 新しいAPIでは、OAuth Server-to-Server認証を使用し、Adobe Developer Consoleを通じて設定します。

<!--
>[!NOTE]
>
> Adobe is standardizing authentication method across all APIs and is gradually onboarding APIs to the Adobe Developer Console, which supports the OAuth Server-to-Server authentication method.
 -->

## API分類の概要

すべてのAEM Forms APIは、次の2つの主要な部分に分かれています。

* [&#x200B; アダプティブフォーム配信とランタイム API](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms Communication API](#aem-forms-communications-apis)

| 詳細 | アダプティブフォーム配信とランタイム API | 通信 API |
|--------------|----------------------------|--------------------------|
| 目的 | アダプティブフォームの配信とランタイム操作の処理 | ドキュメントの生成と操作 |
| ユースケース | - フォーム レンダリング <br>- データ事前入力<br>- フォーム送信<br>- ドラフト管理 | - PDF generation<br>- ドキュメント結合<br>- バッチ処理<br>- プリント処理 |
| 承認方法 | OAuth サーバー間/ユーザー認証方法をサポートしています。 | APIに応じて、JWTまたはOAuthのサーバー間認証をサポートします。 APIは、両方の認証方法をサポートすることはできません。 |

### AEM Forms Communications API

コミュニケーション APIは、ドキュメント中心のオペレーションに最も注力しています。

次の表は、すべての[AEM Forms Communications API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/)と、サポートされている認証方法および実行モデルを示しています。

#### ドキュメント生成API


| API エンドポイント | 説明 | 運用モデル | 認証方法 |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | ドキュメント生成ジョブ用に新しいバッチ設定を作成します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | 特定のバッチ設定の詳細を取得します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | 使用可能なすべてのバッチ設定のリストを返します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | 設定を使用して、バッチ出力生成の実行を開始します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | バッチジョブの実行ステータスを取得します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 特定のバッチ設定のすべての実行中のインスタンスを一覧表示します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | テンプレートとデータに基づいて、PDF出力を同期的に生成します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 印刷可能な出力形式（PCL、PostScriptなど）を生成します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | 大容量プリント用にAFP出力を生成します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | 結合されたデータを含むPDF フォーム（XFA/XDP）をレンダリングします。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | PDF フォーム生成ジョブのステータスを取得します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | 完了したPDF フォームジョブの出力/結果を取得します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |


#### ドキュメント操作API

| API エンドポイント | 説明 | 運用モデル | 認証方法 |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | DDX命令を実行して、PDFを結合、分割、操作します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | PDF ドキュメントをPDF/A フォーマットに変換します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | PDFがPDF/A標準に準拠しているかどうかを検証します | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |

#### ドキュメント変換API

| API エンドポイント | 説明 | 運用モデル | 認証方法 |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | PDF フォームをXDP フォーマットに変換します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### ドキュメント抽出API

| API エンドポイント | 説明 | 運用モデル | 認証方法 |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | PDFからプロパティと構造情報を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | PDFに埋め込まれた使用権限を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | タイトル、作成者、キーワードなどのメタデータを抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | PDF formsからフォームデータ（XML/JSON）を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | 権限や暗号化などのセキュリティ設定を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### ドキュメント変換API


| API エンドポイント | 説明 | 運用モデル | 認証方法 |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | PDF ドキュメントのメタデータを更新または追加します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | PDFにデジタル署名フィールドを追加します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | 署名フィールドの内容を消去します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | PDFから署名フィールドを削除します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### Document Assurance API

| API エンドポイント | 説明 | 運用モデル | 認証方法 |
|---------|-------|---------|----------------------|
| [/adobe/document/assure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | PDFに使用権限を適用します（例：コメント、入力、署名）。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | パスワードまたは証明書のセキュリティを使用してPDFを暗号化します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | 保護されたPDF ドキュメントを復号します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | PDF ドキュメントにデジタル署名します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | デジタル証明書を使用してPDFを認証します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |


## 関連するステップ

同期（オンデマンド）および非同期（バッチ）Forms Communications APIの環境を設定する方法について説明します。

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同期API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同期API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API – 同期">AEM Forms Communications API – 同期</a>
                    </p>
                    <p class="is-size-6">ドキュメントを即座に生成または処理する同期（オンデマンド）Forms Communications APIの環境を設定する方法について説明します。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API – 非同期" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同期API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同期API">AEM Forms Communications API – 非同期（バッチ） </a>
                    </p>
                    <p class="is-size-6">複数のドキュメントをスケジュールされた方法で生成または処理する非同期（バッチ）Forms Communications APIの環境を設定する方法について説明します。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service の概要](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [アダプティブフォームおよび通信 API 用のAEM Forms as a Cloud Service アーキテクチャ](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信処理 - 同期 API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信処理 - バッチ API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Forms Communications API - チュートリアル &#x200B;](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
