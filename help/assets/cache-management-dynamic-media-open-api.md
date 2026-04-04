---
title: オープン APIを使用したDynamic Mediaのキャッシュ管理
description: オープン APIを使用したDynamic Mediaのキャッシュ管理
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 203a5291-edb5-4900-8b0a-32e1ebae5395
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---

# オープン APIを使用したDynamic Mediaのキャッシュ管理 {#cache-management-dynamic-media-open-apis}

効果的なキャッシュ管理は、高性能で拡張性が高く、最新のデジタルアセットを提供するために不可欠です。 オープン APIを備えたDynamic Mediaでは、キャッシュ管理により、配信パイプラインのさまざまなレイヤーをまたいでコンテンツを保存、更新、配信する方法が定義されます。 アセット配信の応答は、最適なパフォーマンスと迅速なコンテンツ配信を実現するために、複数のレイヤーでキャッシュされます。

オープン APIを使用したDynamic Mediaでの長時間キャッシュは、[CDN レイヤーキャッシュ &#x200B;](#cdn-layer-caching)と[外部キャッシュ制御（BYOCDNおよびブラウザーキャッシュ） &#x200B;](#byocdn-browser-caching)で構成されます。

## CDN レイヤーキャッシュ {#cdn-layer-caching}

アセット配信の応答は、[Adobe Managed CDN](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn)で長期間キャッシュされ、パフォーマンスを最大化し、オリジンへの負荷を最小限に抑えます。 このキャッシュは、エンドユーザーに一貫して高品質なエクスペリエンスを提供するために、Adobeによって完全に管理されます。 キャッシュ時間は、パフォーマンスのために意図的に最適化されており、すべての顧客にわたって信頼性と効率的なコンテンツ配信を維持するためにユーザーがカスタマイズすることはできません。

最適なパフォーマンスを確保するために、あらゆる配信URLはエッジ（Fastly）で長時間キャッシュされます。 キャッシュされた配信オブジェクトには、静的レンディション、ビデオ、元の画像バイナリ、および動的に変換された画像（URL パラメーターを通じて生成されたサイズ変更または再フォーマットされたアセットなど）が含まれます。<!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## 外部キャッシュ制御（BYOCDNおよびブラウザーキャッシュ） {#byocdn-browser-caching}

アセット配信の応答には、`Cache-Control` ヘッダーが含まれ、ダウンストリームのキャッシングレイヤーに対して`max-age`10分&#x200B;**の**&#x200B;がデフォルトです。 これは、カスタム *Bring-Your-Own-CDN （BYOCDN）設定*、*エンドユーザーブラウザー*、および&#x200B;*中間キャッシュプロキシ*&#x200B;に適用され、配信パス全体で一貫したキャッシュ制御を確保します。

### キャッシュ制御ヘッダーのカスタマイズ {#customizing-cache-control-headers}

デフォルトの設定を超えてキャッシュが有効になるまでの時間を長くすると、古いコンテンツを配信する可能性が高くなり、エンドユーザーエクスペリエンスにおけるコンテンツ更新の可視性が遅れる可能性があります。 特定のユースケースに合わせてキャッシュ制御の動作を変更する必要がある場合は、カスタム CDN ルールを設定して応答ヘッダーを調整できます。 これにより、必要に応じて異なるキャッシュ期間を設定できます。 応答ヘッダー[については、](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic)AEM カスタム CDN ルールを参照してください。

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

キャッシュ管理に関する詳細なサポートや質問については、[Adobe サポート &#x200B;](https://helpx.adobe.com/jp/contact.html)にお問い合わせください。

## アクティブキャッシュの無効化 {#active-cache-invalidation}

アセットが更新、削除、または変更（メタデータの変更）されると、Open APIを使用したDynamic Mediaは、Adobe Managed CDN上の関連するすべての配信URLを自動的に無効にします。 これは、バニティ IDまたはエイリアスを使用するURLと、幅、形式、品質などの変換パラメーターを含むURLに適用されます。 このイベント駆動型の無効化により、ユーザーは手作業なしで常に最新バージョンのアセットを受け取ることができます。

### 手動キャッシュの消去 {#manual-cache-purging}

キャッシュされたコンテンツを手動でパージする必要がある場合は、AEMのキャッシュ無効化を使用してパージできます。 特定のキャッシュ URLをパージする方法について詳しくは、[AEM CDN キャッシュ無効化](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge)を参照してください。

## よくある質問{#faq-cache-management}

+++**キャッシュ管理は既存の統合にどのように影響しますか？**

アセット URLは変更されず、Adobe Managed CDNからブラウザー（およびその他のダウンストリームの仲介者）に送信されるキャッシュ制御ヘッダーは、[`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean)で10分が継続されます。これにより、ダウンストリームシステムが引き続きキャッシュを最適に活用できます。

+++

+++**どのようなトリガーでキャッシュをパージしますか？**

アセットが更新、変更、アーカイブ、または削除されると、キャッシュのパージトリガーは自動的に実行されます。

<!--
The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.
 -->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **長期間有効なキャッシュでは、すべてのアセットタイプがサポートされますか？**

イベント駆動型アクティブキャッシュ無効化による長期キャッシュは、アセットのタイプや形式に関係なく、オープン APIを使用したDynamic Mediaのすべてのタイプのアセットに適用されます。

+++

+++ **自分のリポジトリの永続キャッシュをオプトアウトできますか？**

長時間キャッシュをオプトアウトするには、[Adobe サポート &#x200B;](https://helpx.adobe.com/jp/contact.html)に連絡し、リクエストの根拠を提供してください。

+++


>[!MORELIKETHIS]
>
>- [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
>- [&#x200B; バニティ URL](/help/assets/vanity-urls.md)
