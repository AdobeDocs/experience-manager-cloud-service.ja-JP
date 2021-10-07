---
title: AEM ノードタイプ
description: AEM は、Sling をベースにして JCR リポジトリーを使用し、両方から提供されるノードタイプを使用しますが、様々な独自ノードタイプも提供しています。
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 92%

---

# AEM ノードタイプ {#aem-node-types}

AEM は Sling ベースであり JCR リポジトリーを使用しているので、これらの標準規格が提供する次のようなノードタイプを AEM で利用できます。

* [JCR ノードタイプ](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling ノードタイプ](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

これらに加えて、AEM では様々なカスタムノードタイプも提供しています。すべての関連プロパティの最新リストについては、[CRXDE](/help/implementing/developing/tools/crxde.md) を使用して AEM リポジトリー内の次のパスを参照してください。

`/jcr:system/jcr:nodeTypes`
