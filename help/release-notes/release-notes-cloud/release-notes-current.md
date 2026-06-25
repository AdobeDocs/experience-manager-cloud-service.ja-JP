---
title: 現在の [!DNL Adobe Experience Manager] as a Cloud Service リリースノート
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 06fa3a08c34299df3c5de78b8b7740cfc0200ed1
workflow-type: tm+mt
source-wordcount: '3035'
ht-degree: 21%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（2024年や2025年など）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

現在の機能リリース（2026.6.0）である[!DNL Cloud Service]のリリース日は2026年6月25日（PT）です。 [!DNL Adobe Experience Manager]次回の機能リリース（2026.7.0）は2026年7月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the May 2026 Release Overview video for a summary of the features added in the 2026.5.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3491490/?quality=12)

-->

## AEM Beta プログラム {#aem-beta-programs}

Adobe Experience Manager（AEM）ベータプログラムは、お客様がプレリリース機能とコードにアクセスし、フィードバックを提供し、AEMの将来を導く方法です。

>[!IMPORTANT]
>
>Beta リリースには欠陥が含まれている場合があり、いかなる保証もなしに「現状のまま」提供されます。 Adobeは、ベータ版のリリースを（Adobe サポートサービスまたはその他の方法により）維持、修正、更新、変更、またはその他の方法でサポートする義務を負いません。 Adobeでは、ベータ版リリースの正しい機能やパフォーマンス、または付随するドキュメントや資料に依存しないように注意することをお勧めします。 ベータ版の機能およびAPIは、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様の責任で行います。

**参加のメリット**

Adobeが開発している機能をいち早く利用することで、お客様やパートナーはフィードバックを提供し、商品の開発をサポートできます。 また、新機能を一般公開する前に導入する準備にも役立ちます。

**現在のベータ版プログラム**

以下のセクションでは、アクティブなベータ版プログラムの一覧を示します。

### AEMの担当者 {#agents-in-aem}

本番環境、ガバナンス、最適化、検出、および開発に関する強力な新しいAEM エージェンティック機能を確認する場合は、[こちらからアクセスする方法をご確認ください。](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM財団（Betaプログラム） {#aem-foundation-beta-programs}

[AEM Foundation ベータプログラム &#x200B;](#foundation-early-adopter)を参照してください。

### Cloud Manager（Beta プログラム） {#cloud-manager-beta-programs}

[Cloud Manager ベータ版プログラム &#x200B;](/help/implementing/cloud-manager/release-notes/current.md)を参照してください。

### AEM Assets（Beta プログラム） {#aem-assets-beta-programs}

[AEM Assets ベータ版プログラム &#x200B;](#assets-beta-program-features)を参照してください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### ビジュアルコンテンツフラグメント {#visual-content-fragments}

AEMでは、[&#x200B; ビジュアルコンテンツフラグメント &#x200B;](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)がサポートされるようになりました。この機能では、添付されたHTML テンプレートを使用して、コンテンツフラグメント出力を書式設定されたHTML エクスペリエンスとしてレンダリングします。 これにより、コンテンツ制作者は、公開前に構造化されたコンテンツを最終ビジュアル形式でプレビュー、検証し、web、電子メール、Edge Delivery Servicesなどのチャネルをまたいで一貫性のあるモジュール型のエクスペリエンスを提供できます。 組み込みの汎用テンプレートは、カスタムテンプレートを必要とせずに基本的な品質保証を行うことができます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Adobe Express Embedded EditorでのPSD ファイルの編集**

Assets ビューから、Adobe Expressの埋め込みエディターで、JPEGおよびPNG形式に加えてPSD ファイルを編集できるようになりました。 この機能強化により、クリエイティブ部門とマーケティング部門は、AEM Assetsから離れることなく、階層化されたデザインファイルを使用できるようになり、コンテンツ更新を効率化し、アプリケーションを切り替える必要性を減らすことができます。 PSDのサポートにより、ソースデザインアセットの柔軟性を維持しながら、コンテンツ制作ワークフローを迅速化できます。

**Adobe IllustratorおよびAdobe InDesign アセットをAEM AssetsからAdobe Expressに読み込む**

Adobe Expressでは、AEM AssetsからのAdobe Illustrator（.ai）およびAdobe InDesign（.indd）ファイルの読み込みがサポートされるようになりました。 この機能により、クリエイティブ部門とマーケティング部門は、承認済みのデザインアセットにより簡単にアクセスして再利用できるようになり、コンテンツ制作を迅速化し、チャネルをまたいで一貫性のあるブランドエクスペリエンスを確保できるようになります。


**Adobe ExpressとAEM Assetsの間でアセットの系統を維持する**

AEM Assetsでは、AEMから取得したアセットを使用してAdobe Expressで作成されたアセットのリネージュ情報が保持されるようになりました。 この機能は、ソースアセットと結果として得られるコンテンツとの関係を記録し、組織が承認されたアセットがクリエイティブワークフローをまたいでどのように再利用されているかを追跡することを可能にします。

チームは、アセットの系統メタデータを管理することで、ガバナンス、コンプライアンス、コンテンツsupply chainの透明性を向上させることができます。 また、マーケターやコンテンツ管理者が、アセットの再利用をより深く理解し、著作権管理の取り組みをサポートして、公開されたコンテンツで使用されるアセットの由来を追跡するのに役立ちます。

>[!IMPORTANT]
>
>この機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

**AEMとWorkfront planning標準キャンペーンメタデータの統合**

AEM AssetsとWorkfront Planningを統合すると、Campaign、Region、Channel、Persona、Productなどのキャンペーンメタデータフィールドが、専用の読み取り専用の「Campaign」タブのアセットプロパティで使用できるようになりました。

この統合により、ユーザーはキャンペーン属性にもとづいてアセットをすばやく発見して検索できます。 これにより、アセットの見つけやすさ向上し、コンテンツ管理ワークフローを合理化して、特定のマーケティング施策に最適なアセットをより効率的に見つけることができます。

>[!IMPORTANT]
>
>この機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。


### OpenAPI機能を備えたDynamic Mediaの新機能 {#new-features-dynamic-media-openapi}

**AI 生成のビデオキャプション**

OpenAPI機能を備えたDynamic MediaでAIが生成した動画のキャプションは、人工知能を活用して動画コンテンツ用のキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。 これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

>[!IMPORTANT]
>
>この機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

**アクセシビリティとSEOを向上させる埋め込みビデオ文字起こし**

DynamicMedia コンポーネントには、顧客のアクセシビリティを向上させるために、ビデオ用の文字起こしが埋め込まれるようになりました。 これらは、ビデオのSEOとLLMの可視性を直接向上させるサーバーサイドレンダリング（SSR）トランスクリプトです。 また、検索エンジンとLLM ツールがページ内のビデオを認識するのに役立つ、準拠したVideoObject [ref https://schema.org/VideoObject]も組み込まれています。

>[!IMPORTANT]
>
>この機能は、制限付き可用性機能として利用できます。 [アドビカスタマーサポートケースを作成および送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、デプロイメントで有効にすることができます。

**ビデオのカスタムサムネール**

OpenAPI機能を備えたDynamic Mediaでは、ビデオアセット用のカスタムサムネールをアップロードできるようになりました。 自動生成されたサムネールをブランド化された、または目的に合わせて構築された画像に置き換えることで、企業はコンテンツのプレゼンテーションを向上させ、アセットの見つけやすさを高め、より魅力的な視聴体験を構築することができます。



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Formsの新機能

* Forms Managerでの&#x200B;**バージョン管理のサポート**
Forms Managerでは、アダプティブ Forms（コアコンポーネントおよび基盤コンポーネント） [&#128279;](/help/forms/manage-form-versions-forms-manager.md)、フォームフラグメント、テーマ、XDP テンプレート、バイナリアセットのバージョン管理が サポートされるようになりました。 Formsとドキュメント コンソールから直接、バージョンを作成し、バージョン履歴を表示したり、フォームアセットの以前の状態を復元したりできます。

* **OSGi**&#x200B;でreCAPTCHA クラウド設定を上書き 
ソースファイルに保持するreCAPTCHA Enterprise プロジェクト ID、サイトキー、およびシークレットは、[Cloud Managerを通じてコンテクストに応じた設定の上書きとデプロイを追加した後、各Cloud Service環境で異なる値に解決できます](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi)。

* **証明書ベースの認証** 
Microsoft SharePoint リストに送信するアダプティブ Formsで、OAuth URL認証と共に[証明書ベースの認証](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication)がサポートされるようになりました。 証明書ベースのサインインの場合は、AEMおよびMicrosoft Azureで証明書エイリアスとテナントの詳細を登録します。

* **ルールエディターの機能強化**

   * アダプティブ Forms ルールエディターは、すぐに使える（OOTB）トリガーおよびカスタムイベント [&#128279;](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events)の ディスパッチイベントおよびトリガーイベント時のルールに関する簡略化された文法をサポートするようになりました。そのため、作成者はカスタムトリガーの文法のみに限定されません。
   * コアコンポーネントに基づくアダプティブ Formsのルールに、ANDまたはOR ロジック [&#128279;](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component)を使用する他の条件と一緒に添付ファイル コンポーネントが含まれるようになったため、添付ファイルの状態と他のチェックがすべて意図したとおりに評価された場合にのみ、ルールがアクションを実行します。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### [!DNL Experience Manager]as a [!DNL Cloud Service]基盤の新機能 {#foundation-new}

#### Cloud Managerの質問に対応する会話型AI インターフェイス {#devagent-cloudmanager}

Development Agentは、[Cloud Manager Job](/help/ai-in-aem/agents/brand-experience/development/development.md#cloud-manager-job)を通じてCloud Managerに関する質問を処理する処理に拡張されます。 AI アシスタントで、プログラム、環境、パイプラインに関する情報（実行ステータスなど）を取得します。 エラーログ、アクセスログ、ビルドログへのリンクをすばやく見つけることができます。

#### パイプラインのトラブルシューティング エージェント ジョブの機能強化 {#devagent-pipeline-troubleshooting}

開発エージェントの[&#x200B; パイプラインのトラブルシューティング ジョブ &#x200B;](/help/ai-in-aem/agents/brand-experience/development/development.md#cloud-manager-pipeline-troubleshooting)は、開発者がAEM as a Cloud Serviceのデプロイメントの問題を診断し、解決するのに役立ちます。 新機能は次のとおりです。

* Web階層設定パイプラインのサポート – フルスタックパイプライン（デプロイメントとコード品質）のサポートに加えて、開発エージェントで&#x200B;**Web階層設定パイプライン**&#x200B;のトラブルシューティングがサポートされるようになりました

* 失敗したパイプラインのExperience Home Widget - Admin &amp; IT ロールに、パイプラインの失敗を示す[新しいウィジェット &#x200B;](/help/ai-in-aem/agents/brand-experience/development/development.md#troubleshoot-from-experience-home)が表示されます。 クリック可能なボタンは、AI アシスタントでのパイプラインのトラブルシューティングジョブを開始します。

#### AI アシスタントでサイレントアワーを管理し、無料期間を更新する {#quiet-hours-ai}

AEM AI アシスタントを通じて、[休眠時間および無料期間](/help/ai-in-aem/agents/brand-experience/development/development.md#control-updates-job)を直接表示、作成、編集できるようになりました。
主なメリットは、スケジュール設定のエラーが少ないことです。リクエストを行う際に、アシスタントは可能な限り案内し、適用される制限、例えば3期間の上限、期間の間の必須1週間の間隔、スケジュールできない予定されているメンテナンス除外ウィンドウなどをフラグ付けします。そのため、設定に失敗した後に制約を検出する代わりに、ビジネスオーナーとデプロイメントマネージャーは、同じ会話で有効なスケジュールに誘導されます。これにより、重要なビジネスウィンドウを自動メンテナンス更新から保護し、行き違いや設定ミスを減らすことができます。

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundationの重要なお知らせ {#foundation-notices}

#### IMS認証リッチエラー {#ims-auth-rich-errors}

IMS統合のトラブルシューティングを支援するために、`imsauth`は&#x200B;*リッチエラー*&#x200B;のサポートを追加しました。

これらのエラーは、HTTP ステータスコードのみを返す代わりに、認証とアクセスをブロックする可能性のある問題の診断と解決に役立つ追加のコンテキストを提供します。

#### Java APIの非推奨化 {#java-api-deprecation}

非推奨のAPIの使用を削除することが重要です。

2026年4月14日（PT）以降、2026年2月26日（PT）をターゲットとするAPIを使用したコードを含むCloud Manager パイプラインは、コードの品質&#x200B;**ステップ中に**&#x200B;削除&#x200B;**失敗します。**&#x200B;非推奨のAPI使用が削除されるまで、デプロイメントはブロックされます。 *これにより、時間の制約を受ける更新プログラムをリリースできなくなり、ビジネス運営に影響を与える可能性があります。*

**2026年7月23日**&#x200B;以降、非推奨のAPI **を使用している環境では、Adobeの重要なリリースアップデート**&#x200B;を受け取ることができず、パフォーマンスと可用性に関するAdobeの標準的なコミットメントの対象にはなりません。 その結果、新しい機能やバグ修正が提供されず、アプリケーションの安定性とアップタイムが悪影響を受ける可能性があり、セキュリティリスクにさらされる可能性があります。

詳しくは、[非推奨（廃止予定）に関する記事](/help/release-notes/deprecated-removed-features.md#aem-apis)を参照してください。便宜上、これらの API を次に示します。

+++ 展開して Java API の非推奨（廃止予定）について確認

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

#### Dispatcher Local MCP serverは、AEM SDKの一部です {#local-dispatcher-mcp}

Dispatcher ローカル MCP サーバーは、[Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)の&#x200B;**AEM SDK**&#x200B;に含まれ、AEM Dispatcher tools zip内にパッケージ化されています。 以前は、Dispatcherのローカル MCP サーバーは、AEM Dispatcher ツールの別のベータリストにパッケージ化されていました。

Dispatcherのローカル MCP サーバーを使用すると、AI ツールがDispatcherとApache HTTPDの設定を検証し、リクエスト処理をトレースして、Dockerでローカルに実行されているDispatcher インスタンスに対するキャッシュ動作を調べることができます。

#### Java 25の準備：AEM Cloud Service ランタイムのアップグレードタイムライン

Java 25は、Java 21に続く次の長期サポート（LTS）リリースであり、パフォーマンス、開発者の生産性、セキュリティの改善を実現します。

&#x200B;- **パフォーマンス** — メモリ使用量の削減、より効率的なガベージコレクション、より高速なJVM ウォームアップは、クラウドネイティブなデプロイメントに役立ちます。
&#x200B;- **開発者の生産性** — オブジェクトの初期化をよりクリーンにし、より表現力豊かなパターンマッチングを実現し、同時タスク管理を簡素化することで、ボイラープレートを削減し、コードの明確性を向上させます。
&#x200B;- **セキュリティ** – 一般的なセキュリティ ワークフローを簡素化するための最新の暗号鍵導出API。

組織がJava 25 ランタイムアップグレードに先立ってテストと検証を計画できるように、Adobeでは次の目標日を提供しています。 このタイムラインの更新は、リリースノートでお知らせします。

| 期間 | マイルストン |
|---|---|
| **2026年10月中旬** | AEM Cloud Service SDKは、Java 25 ランタイムをサポートしています。 Java 25 JDKは、Adobe ソフトウェア配布ポータルからダウンロードできます。 |
| **2026年11月** | お客様は、オプションでクラウド環境のJava 25 ランタイムを有効にして、動作を検証することをお勧めします。 早期導入により、問題を特定して解決するための時間を最大限に活用。 |
| **2027年2月～5月** | Adobeでは、下位環境（RDE、Dev）をJava 25 ランタイムに徐々に移行します。 顧客は、動作を検証し、予期しない問題を報告する必要があり、ステージング環境と実稼動環境も有効にすることをお勧めします。 問題を解決する際に、Java 21への一時的なロールバックを利用できます。 |
| **2027年6月** | すべての環境ランタイム（ステージングと実稼動を含む）はJava 25に移行されます。 Java 21 ランタイムは廃止されました。 AEM Cloud Service SDKでは、Java 21はサポートされなくなります。 |

AEM Cloud Serviceでは、Java 11、Java 17、Java 21での顧客コードのコンパイルを引き続きサポートします。 ただし、Adobeでは、最新の言語機能とパフォーマンスの向上を最大限に活用するために、Java 25 （AEMで利用可能）を使用して構築することをお勧めします。

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation アーリーアダプター機能 {#foundation-early-adopter}

#### AEM Edge Functions （*パブリック Beta* プログラム） {#edge-functions}

[AEM Edge Functions](/help/implementing/developing/introduction/edge-functions.md)は現在パブリックベータ版です。Adobeに連絡せずにセルフサービスで試して有効にすることができます。

この機能により、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより待ち時間が短縮され、エッジでレスポンシブな動的エクスペリエンスが実現します。 AEM Sitesのお客様は、AEM Cloud Service Java スタックとEdge Delivery Services プロジェクトの両方で使用できます。

一般的なユースケースを次に示します。

* 位置情報、デバイスタイプまたはユーザー属性に基づくコンテンツのパーソナライズ
* CDN と接触チャネルの間のミドルウェアとして機能させる
* サードパーティの API からの応答をブラウザーに配信する前に再フォーマットする（および複数の API 応答を集計する）
* 様々なバックエンドからステッチされたコンテンツを使用し、サーバーレンダリングされた HTML をエッジで作成および提供

*AEM Edge Functions Betaを使用すると、まだ開発中であり、テクノロジの正しい機能やデータの可用性に頼るべきではないことを理解できます。 この機能は、そのまま提供され，
予告なく変更される可能性があり、実稼動SLAの対象にはなりません。*

#### RDEのスナップショット （*パブリック Beta* プログラム） {#rde-snapshot-program}

迅速な開発環境（RDE）用のスナップショットは現在パブリックベータ版で、Adobeに連絡して有効にすることなくセルフサービスで試すことができます。

RDEは、コードとコンテンツの現在の状態のスナップショット [&#128279;](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots)を取得する機能をサポートするようになりました。これは、後で復元できます。 これは、元に戻す必要がある場合のあるコードを同期する場合や、異なる機能の開発を切り替える場合に役立つことがあります。 また、テストの既知の開始点として、可変コンテンツのみを復元することもできます。

*RDE スナップショット Betaを使用することにより、まだ開発中であり、テクノロジーの正しい機能やデータの可用性に頼るべきではないことを認めます。 この機能を広範囲にテストしましたが、RDEが不安定になる可能性は少しあります。 この問題が発生した場合、リセットを実行すると、動作状態に戻ります。*

#### レプリケーション AIのトラブルシューティング（Beta プログラム） {#replication-ai-troubleshooting-beta}

AEM オーサーのAI アシスタントやその他のインターフェイスを使用すると、ブロックされたキューなど、レプリケーションに関連する問題をトラブルシューティングできます。 Beta プログラムに参加するには、[aem-devagent@adobe.com](mailto:aem-devagent@adobe.com)にメールを送信して、興味を説明してください。

#### ライブトラフィックを受け入れる前にコードをテストするための Canary 実稼動デプロイメント（Beta プログラム） {#canary-beta}

エンドユーザーに公開する前に、内部専用テストトラフィックを使用して実稼動ビルドを検証します。 実稼動環境に出荷し、Canary トラフィックのみをルーティング（特別なヘッダーを使用）し、動作を監視してから、顧客に影響を与えることなく、ライブトラフィックに昇格するか、ロールバックします。

アクセスをリクエストしてフィードバックを共有するには、[aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) にメールを送信してください。

#### AEM コードの評価とIDE AI エージェントによる自動修正（Beta プログラム） {#ide-ai-aemcode-issues}

AEM Cloud Service Cursor、Claude Code、Visual Studio、IntelliJなどのツールでAI支援による開発を使用するJava スタックチームは、さらに進むことができます。 新しい[&#x200B; コード評価IDE エージェントスキル &#x200B;](/help/ai-in-aem/local-development-with-ai-tools.md#use-the-code-assessment-skill)は、AEM コードベースで問題を直接検出して自動修正し、レビューサイクルを短縮して、開発の早い段階で問題を検出します。

サポートされるチェックには次のものがあります。
* 非推奨のAPIの置き換え
* sling モデル依存関係インジェクションの最新化
* 古いMaven依存関係の更新
* 送信HTTP呼び出しにタイムアウトを追加する
* 境界のないクエリをバウンド
* Sling スケジューラー
* リソース変更リスナーのレプリケーション
* JCRまたはOSGi イベント処理

この機能はベータ版です。 試してみて、[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)のチームとフィードバックを共有してください。

#### Edge Delivery Services の Edge 認証（Beta プログラム） {#edge-authentication}

Edge 認証を使用すると、Edge Delivery Services ページへのアクセスを、ID プロバイダー（IdP）で認証されたユーザーのみに制限できます。 これを実現するには、OpenID Connect（OIDC）設定の YAML ファイルをデプロイします。

ご興味がある場合は、ユースケースの簡単な説明とご質問を [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までお問い合わせください。

#### OpenTelemetry for Application Performance Monitoring （APM）（Alpha プログラム） {#apm-alpha}

AEM as a Cloud Serviceでは、OpenTelemetry ベースのテレメトリ書き出しがサポートされるようになりました。これにより、チームが既に使用しているAPM ツール内の他のシステムと並行してAEMを監視できます。

この統合を使用して、以下を行います。

&#x200B;- 遅いリクエストまたは失敗したリクエストの調査
&#x200B;- JVMの正常性とリソースの使用状況を経時的に追跡
&#x200B;- AEM階層のダッシュボードとアラートを構築する
&#x200B;- インシデント時にAEMの動作を他のサービスと関連付ける

アルファ版に参加するには、ユースケースを説明したメール [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com)を送信してください。

### [!DNL Experience Manager]as a [!DNL Cloud Service] Assets Betaの機能 {#assets-beta-program-features}

#### ASSETS ビューのUI拡張性 {#ui-extensibility-assets-view}

Assets Viewは、開発者を第一に考えたUI拡張性に対応しています。この機能を利用すれば、顧客はすばやくエクスペリエンスをカスタマイズし、特定のビジネス要件に対応できます。
Adobeの開発者向けドキュメントに従うことで、最小限の労力で拡張機能を構築、デプロイし、既存の安定した拡張ポイントを活用できます。必要な拡張ポイントがまだ利用できないユースケースの場合、Adobeはお客様と直接連携して、要件を検討し、ニーズに合わせた新しい拡張性APIを提供することの技術的な実現可能性を評価します。また、**Beta リリース**&#x200B;などの新しいAPIを提供する場合があります。
さらに、Adobeでは、社内の早期導入フェーズで現在利用可能な&#x200B;**GenAIを活用した拡張機能ジェネレーションツール**&#x200B;を開発しました。このツールは、拡張機能の開発時間を大幅に短縮できます。このベータプログラムに参加されるお客様には、このツールへのアクセス権が付与され、その進化を形作るためにフィードバックを共有することが推奨されます。
参加または詳細を知りたい場合は、`GRP-ASSETSVIEWUIEXTENSIBILITY@adobe.com`さんにメールを送信してください。

#### ブランドに応じたメタデータ（BAM） {#brand-aware-metadata}

AEM Assetsでは、AIを活用した機能であるBrand Aware Metadataをサポートするようになりました。これにより、アップロードや再処理が行われたときに、アセットのカスタムメタデータを自動的に生成できます。 これにより、手作業による入力の必要性を大幅に減らし、アセットを見つけて新しいエクスペリエンスをより迅速に提供できるようになります。 顧客は、ブランドの用語や分類基準に合わせて、AIを活用して任意のメタデータフィールドを入力する方法を定義するプロンプトのライブラリを管理できます。 このプロンプトライブラリには、結果をプレビューするための遊び場と、提案された改善点を自動的にドラフトするプロンプトオプティマイザーが含まれています。

Adobeは、お客様との直接的な共同イノベーションを通じて、BAMの能力を積極的に拡大しています。 特定のユースケースがまだサポートされていない場合、Adobeは参加するお客様と連携してニーズを理解し、ベータ版の進行に合わせて拡張された機能を提供する場合があります。 このプログラムをご利用のお客様は、製品を出荷する際に新機能をいち早く利用し、ロードマップを形作るフィードバックを共有することが推奨されます。

参加または詳細を知りたい場合は、`GRP-AEM-ASSETS-BRANDAWAREMETADATA@adobe.com`さんにメールを送信してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターのリリースの完全なリストは、[こちら](/help/release-notes/universal-editor/current.md)で確認できます。

## バリエーションの生成 {#generate-variations}

バリエーションの生成のリリースの完全なリストは、[こちら](/help/generative-ai/release-notes-generate-variations.md)で確認できます。

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
