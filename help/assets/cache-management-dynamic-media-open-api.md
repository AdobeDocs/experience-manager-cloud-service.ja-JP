---
title: Open API を使用した Dynamic Media のキャッシュ管理
description: Open API を使用した Dynamic Media のキャッシュ管理
role: User
exl-id: 203a5291-edb5-4900-8b0a-32e1ebae5395
source-git-commit: 8c9e59108d28ee02a4609c58bf7a2543783f47e2
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# Open API を使用した Dynamic Media のキャッシュ管理 {#cache-management-dynamic-media-open-apis}

パフォーマンスと拡張性に優れた最新のデジタルアセットを実現するには、効果的なキャッシュ管理が不可欠です。 オープン API を使用した Dynamic Media では、キャッシュ管理により、配信パイプラインの様々なレイヤーでコンテンツを保存、更新および配信する方法が定義されます。 アセット配信応答は、最適なパフォーマンスと高速なコンテンツ配信を確保するために、複数のレイヤーでキャッシュされます。

Open API を使用した Dynamic Media の長期キャッシュは、[CDN レイヤーキャッシュ ](#cdn-layer-caching) および [ 外部キャッシュ制御（BYOCDN およびブラウザーキャッシュ） ](#byocdn-browser-caching) で構成されています。

## CDN レイヤーキャッシュ {#cdn-layer-caching}

アセット配信応答は、パフォーマンスを最大化しオリジンの負荷を最小限に抑えるために、長期間 [0}Adobeの管理による CDN} にキャッシュされます。 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn)このキャッシングは、エンドユーザーに一貫して高品質のエクスペリエンスを提供するために、Adobeによって完全に管理されます。 キャッシュ時間は、パフォーマンスのために意図的に最適化されており、すべての顧客に対して信頼性と効率的なコンテンツ配信を維持するためにユーザーがカスタマイズすることはできません。

最適なパフォーマンスを確保するために、すべての配信 URL が長期間エッジ（Fastly）にキャッシュされます。 キャッシュされた配信オブジェクトには、静的レンディション、ビデオ、元の画像のバイナリおよび動的に変換された画像（URL パラメーターを使用して生成されたサイズ変更や再フォーマットのアセットなど）が含まれます。<!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## 外部キャッシュ制御（BYOCDN およびブラウザーキャッシュ） {#byocdn-browser-caching}

アセット配信応答には、ダウンストリームキャッシュレイヤーのデフォルト `Cache-Control` が `max-age`10 分 **の** ヘッダーが含まれています。 これは、カスタム *Bring-Your-Own-CDN （BYOCDN）設定*、*エンドユーザーブラウザー* およびその他 *中間キャッシュプロキシ* に適用され、配信パス全体で一貫したキャッシュ制御を確保します。

### キャッシュ制御ヘッダーのカスタマイズ {#customizing-cache-control-headers}

デフォルト設定を超えてキャッシュの有効期限の値を長くすると、古いコンテンツが提供される可能性が高くなり、エンドユーザーエクスペリエンスでのコンテンツ更新の表示が遅れる可能性があります。 特定のユースケースに合わせてキャッシュ制御動作を変更する必要がある場合、カスタム CDN ルールを設定して、応答ヘッダーを調整できます。 これにより、要件に応じて異なるキャッシュ時間を設定できます。 応答ヘッダーについては、[AEMのカスタム CDN ルール ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic) を参照してください。

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

キャッシュ管理に関するその他のサポートや質問については、[Adobe サポート ](https://helpx.adobe.com/jp/contact.html) にお問い合わせください。

## アクティブなキャッシュの無効化 {#active-cache-invalidation}

アセットが更新、削除、変更（メタデータの変更）されるたびに、Dynamic Media と Open API は、Adobeの管理による CDN の関連するすべての配信 URL を自動的に無効にします。 これは、バニティ ID またはエイリアスを使用する URL と、幅、形式、品質などの変換パラメーターを含むすべての URL に適用されます。 このイベント駆動型の無効化により、手動の介入なしで、ユーザーがアセットの最新バージョンを常に受け取れるようになります。

### 手動でのキャッシュのパージ {#manual-cache-purging}

キャッシュされたコンテンツを手動でパージする必要がある場合は、AEMのキャッシュ無効化機能を使用してパージできます。 特定のキャッシュ URL のパージ方法について詳しくは、[AEM CDN キャッシュの無効化 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge) を参照してください。

## よくある質問{#faq-cache-management}

+++**キャッシュ管理は既存の統合にどのような影響を与えますか？**

アセット URL は変更されず、Adobe管理 CDN からブラウザー（およびその他のダウンストリーム仲介者）に送信されるキャッシュ制御ヘッダーは [`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean) で 10 分に維持され、ダウンストリームシステムがキャッシュを最適に活用し続けることを保証します。

+++

+++**キャッシュパージにはどのようなトリガーがありますか？**

トリガーが更新、変更、アーカイブまたは削除されると、キャッシュのアセットが自動的にパージされます。

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

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

+++ **長期間有効なキャッシュでサポートされているアセットタイプは何ですか？**

イベント駆動型のアクティブキャッシュの無効化を含む長時間のキャッシュは、アセットのタイプや形式に関係なく、Open API を使用して Dynamic Media 内のすべてのタイプのアセットに適用できます。

+++

+++ **リポジトリの長期間有効なキャッシュをオプトアウトできますか？**

長期にわたるキャッシングをオプトアウトするには、[Adobe サポートに連絡し ](https://helpx.adobe.com/jp/contact.html) リクエストの根拠を示してください。

+++


>[!MORELIKETHIS]
>
>- [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
>- [ バニティ URL](/help/assets/vanity-urls.md)
