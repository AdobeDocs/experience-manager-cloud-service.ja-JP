---
title: ガバナンスエージェントの概要
description: AEM Governance Agentが、AEM全体のブランドの整合性とコンプライアンスをどのように保護するかをご確認ください
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2c73c578-6655-43bf-b03a-cb3eb2284d07
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---


# ガバナンスエージェントの概要 {#governance-agent}

**Governance Agent**&#x200B;は、Adobe Experience Manager全体のブランドの整合性とコンプライアンスを保護するために設計されたソリューションです。 セキュリティ、規制、ブランドに関するポリシーを実施し、あらゆるインタラクションとアクティベーションが確立された基準を遵守できるようにします。 ガバナンスエージェントはAI アシスタントに完全に統合されており、**A2A （Agent-to-Agent）**&#x200B;および&#x200B;**MCP （Model Control Protocol）** ツールを活用して、エンタープライズ環境内でシームレスに動作するように設計されています。 これらの統合により、ChatGPT、Claude、その他の外部AI システムなどの高度なAI オーケストレーターと連携することが可能になり、プラットフォームをまたいで柔軟かつスケーラブルなインテリジェンスを実現します。

主な機能は次のとおりです。

* **ブランドガバナンス：** コンテンツとアセットをまたいでブランドチェックを自動化することで、ブランドの一貫性を維持し、手作業によるレビューを減らします
* **権限とDigital Rights Management （DRM）:** デジタルアセット全体の権限と使用権限を管理することで、安全でコンプライアンスに準拠した共同作業を実現します。

これらの機能を組み合わせることで、ガバナンスエージェントはリスクを軽減し、迅速かつ安全で、ブランドに即した大規模な配信を可能にします。

>[!IMPORTANT]
>
>AIによる回答は、不正確または誤解を招く可能性があります。 修正案と回答案を再確認しましょう。
>
>[Adobe Experience Cloud生成AI ユーザーガイドライン ](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)も参照してください。

## Skills in AEM Governance Agent {#skills-in-aem-governance-agent}

### ブランドガバナンス {#brand-governance}

ガバナンスエージェントは、ブランドガイドラインに照らし合わせてコンテンツを検証し、あらゆるデジタルエクスペリエンスで一貫性を確保できます。 トーン、クレーム、ロゴの使用状況、タイポグラフィ、画像など、事前に取り込まれたブランドルールを使用します。 Experience Hubのチャットモード、エディターおよびバッチモードでリアルタイムに動作するので、AIによるコンテンツ生成、サイト移行、ブリーフベースのサイト作成に適しています。

![ ブランドガバナンスの概要](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**プロンプトの例：**

* *このページはブランドと一致していますか？`https://www.website/en.html`*
* *この`https://www.website/en.html`はブランドメッセージングガイドラインに従っていますか？*
* *`https://www.website/homepage`がブランドのガイドラインに従っているかどうかを確認する*
* *ブランドガイドラインを表示*

>[!NOTE]
>
>ガバナンスエージェントには、AIを活用したブランドポリシーのインポート機能も搭載されています。この機能では、AIを活用して、顧客の既存のブランドガイドラインドキュメントを、構造化された強制的なポリシーチェックに変換し、コンプライアンスに準拠したコンテンツ制作を自動的に管理、検証、ガイドします。 詳しくは、[ ブランドポリシーの読み込み方法](/help/ai-in-aem/agents/governance/how-to-import-a-brand-policy.md)を参照してください。

### Permission and Digital Rights Management {#permission-and-digital-rights-management}

#### Content Hubでの権限管理 {#permission-management-in-content-hub}

Content Hubでは、ガバナンスエージェントにより、適切なユーザーのみが適切なアセットにタイミングよくアクセスできるようになります。 きめ細かい属性ベースの制御と使用権限を適用することで、機密コンテンツを保護しながら、安全なコラボレーションを可能にします。 これにより、コンプライアンスリスクの低減、ブランドの一貫性の強化、ワークフローの高速化を実現し、不正アクセスや悪用を心配することなく、自信を持ってアセットを共有し、再利用することができます。 こうしたセキュリティと柔軟性のバランスにより、組織全体の業務効率と信頼性が向上します。

![権限管理の概要](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**プロンプトの例：**

* *既存のすべてのContent Hub ABAC ルールを表示します。*
* *すべてのアセットに対する「マーケティング」グループのアクセス権を付与するルールを作成します。*
* *マーケティング :segmentがEMEAに等しいアセットへのセールスグループのアクセス権を付与します。*
* *外部代理店*&#x200B;へのアクセス権を与えるすべてのルールを削除します
* *Content HubのABACとは何ですか。また、私のサポートを受けられますか？*

#### Assets Digital Rights Management {#assets-digital-rights-management}

Agentを使用すると、コンテンツエコシステム全体でAssetsのデジタル権限を管理できます。 これにより、権限と使用権限が詳細に管理され、アセットにアクセスして、定義されたコンプライアンス範囲内でのみ使用できるようになります。 これにより、安心して知的財産を保護し、規制リスクを低減して、ブランドの整合性を維持できます。 権限の適用を自動化することで、チームは安全かつ自信を持ってコラボレーションでき、セキュリティやコンプライアンスを犠牲にすることなくコンテンツ配信を加速できます。

![DRM管理の概要](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**プロンプトの例：**

* *アセットの有効期限がまもなく切れますか？*
* *先月有効期限が切れた自転車アセットをすべて検索します。*
* *最近期限切れになったアセットはどれですか？*
* *有効期限のないアセットを検索*
* *今後14日間で期限切れとなる/content/dam/productsのすべてのアセットを表示*
