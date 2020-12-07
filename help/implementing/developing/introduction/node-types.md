---
title: AEMノードタイプ
description: AEMはSlingに基づいており、両方から提供されるノードタイプを持つJCRリポジトリを使用しますが、AEMは独自のノードタイプも提供します。
translation-type: tm+mt
source-git-commit: 020cebfa714c098f032df963b7105503c741e748
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 15%

---


# AEMノードタイプ{#aem-node-types}

AEMはSlingに基づいており、JCRリポジトリを使用するので、AEMでは、次の両方の標準で提供されるノードタイプを使用できます。

* [JCR ノードタイプ](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling ノードタイプ](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

これらに加えて、AEMには、様々なカスタムノードタイプが用意されています。 すべての関連プロパティを持つ最新のリストの場合、[CRXDE](/help/implementing/developing/tools/crxde.md)を使用してAEMリポジトリ内の次のパスを参照します。

`/jcr:system/jcr:nodeTypes`
