---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: 6194df9d-8c3c-4c7f-be59-099b970a565a
source-git-commit: 47b6d7871201cd7dbc1db77620879e69bce4ad3a
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 83%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.7.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.7.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2022年、2023年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在の機能リリース（2024.7.0）は、2024年7月25日（PT）に提供開始となりました。次回の機能リリース（2024.8.0）は、2024年8月29日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.7.0 リリースで追加された機能の概要については、2024年7月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-feature-sites}

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットのブラウジング**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像やその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットブラウジング](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合早期導入プログラムの詳細をご案内いたしますので、ご自身の正式なメール ID から aemcs-headless-adopter@adobe.com までご連絡ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**アセットセレクターによるアセットのアップロード**

アセットセレクターで、コンテンツ作成者がローカルファイルシステムからドラッグまたは参照して、セレクターから直接最終アセットをアップロードできるようになりました。 この機能を使用すると、選択したアプリケーションから最終的なアセットを DAM にアップロードできます。

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。 これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

### アセットビューの新機能 {#assets-view-new-features}

**Content Credentials の統合**

Experience Manager Assets で、サポートされる画像形式の Content Credentials がサポートされるようになりました。この機能は、アセットの系列と作成方法に関する情報を提供します（GenAI を使用して変更されたかどうかなど）。

![Content Credentials](/help/assets/assets/content-credentials.png)

**フォルダーのコンテンツの視覚的なプレビュー**

Experience Manager Assetsでは、コンテンツの参照時や検索時に、フォルダーのサムネールにフォルダーコンテンツの視覚的なプレビューが表示されるようになりました。これにより、AEM Assets リポジトリー内で使用可能なアセットを見つけやすくなります。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースのアダプティブフォーム用のビジュアルルールエディターの強化

アダプティブフォームの作成者は、繰り返し可能なフォームフィールドと、すぐに使用できるビジュアルルールエディターの機能を使用して、開発チームのカスタマイズやサポートを必要とせずに、フォーム内で複雑なビジネスロジックを作成できます。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、他のユーザーよりも先に最先端のイノベーションに独占的にアクセスし、その開発に貢献できるユニークな機会を提供します。プログラムを利用すると、複数のイノベーションにアクセスできます。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### ユニバーサルエディターによるアダプティブフォームの作成

Adobe Experience Manager [ユニバーサルエディター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)を活用して、WYSIWYG ドラッグ＆ドロップオーサリングを使用してアダプティブフォームを作成し、ヘッドレス登録エクスペリエンスとヘッドフル登録エクスペリエンスの両方を Edge Delivery Service 経由で配信します。アダプティブフォームの作成者は、web ページ内のフォームのバリエーションに対する実験を簡単に作成して開始できます。 この機能を使用すると、エンドユーザーにとって最もパフォーマンスの高いエクスペリエンスを決定できます。

>[!IMPORTANT]
>
> 早期アクセスイノベーションの早期アクセスプログラムへの参加に興味がある方は、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信して利用申請してください。すべてのイノベーションまたは特定のイノベーションに対して利用申請できます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### セルフサービス API キーを使用した CDN のコンテンツのパージ {#purge-cdn}

HTTP キャッシュ制御ヘッダーを使用した TTL の設定は、コンテンツ配信のパフォーマンスとコンテンツの鮮度のバランスを取る効果的なアプローチです。ただし、更新されたコンテンツを直ちに提供することが重要なシナリオでは、CDN キャッシュを直接パージすると有益な場合があります。

Cloud Manager設定パイプラインを使用してパージ API トークンの設定をセルフサービスで行う [ 方法を説明します ](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)。これにより、次のバリエーションのいずれかを使用して [ パージ API を呼び出す ](/help/implementing/dispatcher/cdn-cache-purge.md) ことができます。

* 単一の URL
* タグを使用した複数の URL
* 完全な CDN キャッシュのパージ

### 顧客管理 CDN 用 X-AEM-Edge-Key のセルフサービス設定 {#customermanaged-keys}

以前は、顧客管理 CDN の設定に必要な X-AEM-Edge-Key を生成するには、サポートチケットが必要でした。このワークフローは、設定パイプラインを使用してデプロイされた設定ファイルでキーの値を宣言することで、セルフサービスになり、新しい環境のオンボーディングの遅延を取り除きます。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

### トラフィックフィルタールールアラート {#traffic-filter-rules-alerts}

トラフィックフィルタールール（オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールを含む）を使用すると、ブロックするトラフィックを設定できます。

トラフィックフィルタールールがトリガーされるたびに、[ アラートを登録 ](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts) できるようになりました。 特定のトラフィック状況が発生するとアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

### コンテンツ配信関連の早期導入プログラム {#foundation-early-adopter}

以下の早期導入プログラムのどれに興味があるかを明記して、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信してください。

#### CDN での基本認証（早期導入プログラム） {#basicauth-cdn}

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する包括的なソリューションとして機能するのではなく、主にビジネス関係者によるコンテンツのレビューなど、簡易な認証ユースケースを対象としています。ユーザー名とパスワードのリストは、秘密鍵タイプの Cloud Manager 環境変数を参照して、設定パイプライン経由でデプロイされる Git の設定ファイルを通じて管理されます。[詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### サーバーサイドのリダイレクト（早期導入プログラム） {#server-side-redirects-early-adopter}

ソース管理で 301/302 サーバーサイドのリダイレクトを設定し、CDN にデプロイします。 [詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. -->リクエストと応答の変換、AEM 外のサイトへのトラフィックのルーティングなど、[CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)に関連して既に利用可能な他の機能がいくつかあります。

#### ビジネスユーザーが Git 外部でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。このアプローチにより、ビジネスユーザーは、スプレッドシートや、ACS Commons リダイレクトマップマネージャーやカスタムアプリケーションなどの UI を使用してリダイレクトを宣言できます。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含め、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### コンテンツヘルス関連アクションセンター通知早期導入プログラム {#actions-center-notifications}

[アクションセンター](/help/operations/actions-center.md)は、重要なインシデントが発生した場合や、コードや設定に関してプロアクティブなアクションを実行する必要がある場合にメール通知を送信します。アドビでは、コンテンツヘルスに関連するいくつかの新しいタイプの通知を導入しました。この機能は、早期導入プログラムを通じて利用できます。参加するには、アドビカスタマーケアにお問い合わせください。

#### ページに多数のノードが含まれる {#page-nodes}

ノードの数が多いと、レンダリングのパフォーマンスが低下し、ページの読み込み時間が短縮される可能性があります。あるページ上で大量のノードが検出されると、アクションセンターを通じて事前通知が届きます。これを受けて、ユーザーは、ページ内のノードの合計数を減らすために必要な手順を実行できます。

#### 実行中のワークフローインスタンスの数が多い {#running-workflows}

オーサー環境で多数のワークフローの数を実行している場合は、ワークフローエンジンのパフォーマンスが影響を受けます。実行中のワークフローインスタンスの数が多く検出された場合は、アクションセンターを通じて事前通知が届きます。このプロセスにより、不要な実行中のワークフローを終了するためのパージジョブを設定できます。

#### ユーザーがカスタムグループに直接追加される {#users-customgroups}

ユーザーがカスタムグループに直接追加されると、アクションセンターを通じて事前通知が届きます。このプロセスでは、関連する IMS グループにユーザーを追加し、これらの IMS グループを AEM グループのメンバーとして含めることで、IMS のベストプラクティスに従うことができます。

#### JCR コンテンツが欠落しています {#jcr-content}

JCR コンテンツが欠落していることが検出されると、アクションセンターは事前に通知します。このアプローチでは、欠落しているコンテンツを追加し、特定の AEM Assets 機能のエラーを防ぐことができます。

#### 完了したワークフローがパージされない {#workflows}

完了したワークフローが 90 日以上経過してもパージされていないと、アクションセンターは事前に通知します。このアプローチは、ワークフローインスタンスの数を減らすことで、ワークフローエンジンのパフォーマンスを向上させるのに役立ちます。

#### Sling リソースが欠落している {#sling-resource}

Sling リソースが欠落していることが検出されると、アクションセンターは事前に通知します。このアプローチでは、欠落しているリソースを追加し、特定の AEM Assets 機能のエラーを防ぐことができます。

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
