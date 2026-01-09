---
title: AEM Forms Communications API – 概要
description: 認証方法を含むAEM Forms Communications API の概要と完全な API リファレンス
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 9%

---


# AEM Forms API – 概要

AEM Forms API は、ドキュメントワークフローの自動化に役立つように設計された、クラウドネイティブな API の包括的なスイートを提供します。

AEM Forms API は、次の 2 つの主要なコンソールを通じて構造化され、アクセスされます。

* [Adobe Developer Console（ADC） ](https://developer.adobe.com/developer-console/) - Adobe Developer Consoleは、Adobe API、イベント、ランタイム、App Builderへのゲートウェイです。

* [AEM Developer Console](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Consoleでは、運用タスクや統合タスクをサポートするために、環境レベルの詳細、設定、技術アカウント、サービス資格情報にアクセスできます。

API が異なると、サポートする [ 認証方法 ](#authentication-methods) も異なります。

## 認証方法

Forms API によって、リリースタイムラインに基づいて使用される認証方法が異なります。

* [OAuth サーバー間](/help/forms/oauth-api-authetication.md)
* [JWT （JSON web トークン）サーバー間 ](/help/forms/jwt-api-authentication.md)

以前の API は、JWT ベースのサーバー間認証をサポートしていました。この認証は、AEM Developer Consoleを通じて設定および管理されます。 新しい API は、OAuth サーバー間認証を使用し、Adobe Developer Consoleを通じて設定されます。

>[!NOTE]
>
> Adobeは、すべての API で認証方法を標準化しており、OAuth サーバー間認証方法をサポートするAdobe Developer Consoleに API を徐々にオンボーディングしています。

## API 分類の概要

すべてのAEM Forms API は、次の 2 つの主な部分に分かれています。

* [ アダプティブフォーム配信およびランタイム API](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms通信 API](#aem-forms-communications-apis)

| 詳細 | アダプティブフォーム配信およびランタイム API | 通信 API |
|--------------|----------------------------|--------------------------|
| 目的 | アダプティブフォームの配信とランタイム操作を処理 | ドキュメントの生成と操作 |
| ユースケース | - フォームのレンダリング <br>- データの事前入力 <br>- フォーム送信 <br> - ドラフト管理 | - PDFの生成 <br> – 文書結合 <br>- バッチ処理 <br> – 印刷処理 |
| 認証方法 | OAuth サーバー間/ユーザー認証方法をサポートします。 | API に応じて、サーバーからサーバーへの認証（JWT または OAuth）をサポートします。 1 つの API で両方の認証方法をサポートすることはできません。 |

### AEM Forms通信 API

通信 API は、ドキュメント中心の操作の主な焦点です。

次の表に、すべての [AEM Forms Communications API と ](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) サポートされる認証方法および実行モデルを示します。

#### ドキュメント生成 API


| API エンドポイント | 説明 | 実行モデル | 認証方法 |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | ドキュメント生成ジョブ用の新しいバッチ構成を作成します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | 特定のバッチ設定の詳細を取得します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | 使用可能なすべてのバッチ設定のリストを返します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | 設定を使用してバッチ出力生成の実行を開始します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | バッチジョブの実行ステータスを取得します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 特定のバッチ設定の実行中のすべてのインスタンスを一覧表示します。 | 非同期/バッチ | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | テンプレートとデータに基づいて、PDF出力を同期的に生成します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 印刷用の出力形式（PCL、PostScriptなど）を生成します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | 大容量印刷用の AFP 出力を生成します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | データが結合されたPDF フォーム（XFA/XDP）をレンダリングします。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | PDF フォーム生成ジョブのステータスを取得します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | 完了したPDF フォームジョブの出力/結果を取得します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |


#### ドキュメント操作 API

| API エンドポイント | 説明 | 実行モデル | 認証方法 |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | DDX 命令を実行して、PDF を結合、分割または操作します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | PDF ドキュメントをPDF/A 形式に変換します。 | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | PDFがPDF/A 標準に準拠しているかどうかを検証します | 同期 | [JWT](/help/forms/jwt-api-authentication.md) |

#### ドキュメント変換 API

| API エンドポイント | 説明 | 実行モデル | 認証方法 |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | PDF フォームを XDP 形式に変換します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### ドキュメント抽出 API

| API エンドポイント | 説明 | 実行モデル | 認証方法 |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | PDFからプロパティおよび構造情報を書き出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | PDFに埋め込まれている使用権限を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | タイトル、作成者、キーワードなどのメタデータを抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | PDF formsからフォームデータ（XML/JSON）を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | 権限や暗号化などのセキュリティ設定を抽出します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### ドキュメント変換 API


| API エンドポイント | 説明 | 実行モデル | 認証方法 |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | PDF ドキュメントのメタデータを更新または追加します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | PDFにデジタル署名フィールドを追加します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | 署名フィールドの内容をクリアします。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | PDFから署名フィールドを削除します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### Document Assurance API

| API エンドポイント | 説明 | 実行モデル | 認証方法 |
|---------|-------|---------|----------------------|
| [/adobe/document/assure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | PDFに使用権限を適用します（コメント、入力、署名など）。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | PDFをパスワードまたは証明書セキュリティで暗号化します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | セキュリティで保護されたPDF ドキュメントを復号化します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | PDF ドキュメントにデジタル署名します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | デジタル証明書でPDFを認証します。 | 同期 | [OAuth](/help/forms/oauth-api-authetication.md) |


## 関連する手順

同期（オンデマンド）および非同期（バッチ）Forms通信 API の環境を設定する方法について説明します。

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同期 API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同期 API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms通信 API – 同期">AEM Forms通信 API – 同期 </a>
                    </p>
                    <p class="is-size-6">ドキュメントを即座に生成または処理する、同期（オンデマンド）Forms Communications API の環境を設定する方法を説明します。 </p>
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
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms通信 API – 非同期" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同期 API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同期 API">AEM Forms通信 API – 非同期（バッチ） </a>
                    </p>
                    <p class="is-size-6">複数のドキュメントをスケジュールに従って生成または処理する、非同期（バッチ）Forms通信 API の環境を設定する方法について説明します。</p>
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
>* [ 通信処理 – オンデマンド API](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
