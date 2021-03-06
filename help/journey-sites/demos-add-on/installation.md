---
title: 参照デモのアドオンのインストールについて
description: Cloud Manager と、それを使用してアドオンをインストールする方法を説明します。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 100%

---

# 参照デモのアドオンのインストールについて {#understand-installation}

Cloud Manager と、それを使用してアドオンをインストールする方法を説明します。

>[!TIP]
>
>Cloud Manager の使用経験がある場合や、アドオンの設定と使用に直接アクセスしたい場合は、スキップして [プログラムとパイプラインの作成](create-program.md) に進んでも構いません。
>
>Cloud Manager と AEM が連携してデモ環境を作成する方法、および独自のデモ環境を設定して使用する方法については、このドキュメントを引き続き参照してください。

## 目的 {#objective}

このドキュメントは、参照デモのアドオンのインストールプロセスの仕組みを理解するのに役立ち、様々な部分がどのように連携するかを示しています。読み終えると、次のことができるようになります。

* Cloud Manager の基本を理解しました。
* パイプラインで AEM にコンテンツと設定を配信する方法を理解しました。
* 数回クリックするだけで、デモコンテンツがあらかじめ登録された新しいサイトをテンプレートで作成できることがわかりました。

このドキュメントでは、ジャーニーの次のステップに進んでインストールを開始する前に、AEM 参照デモのアドオンのこれらの基本的な部分を理解することに焦点を当てています。

このジャーニーを順を追って進めることをお勧めしますが、Cloud Manager の使用経験がある場合や、アドオンの設定と使用に直接アクセスしたい場合は、スキップして [プログラムとパイプラインの作成](create-program.md) に進んでも構いません。

## 担当する役割 {#responsible-role}

このジャーニーは、組織の Cloud Manager で **ビジネスオーナー** の役割を持つメンバーであるシステム管理者に適用されます。

## 要件と前提条件 {#requirements-prerequisites}

参照デモのアドオンについて学び、使用を開始するための最小要件があります。

### 知識 {#knowledge}

* Cloud Manager の基本知識

### ツール {#tools}

* 組織の Cloud Manager で **ビジネスオーナー** の役割を持つメンバーになる

## Cloud Manager について {#cloud-manager}

Cloud Manager は、AEM as a Cloud Service の必須コンポーネントであり、プラットフォームへの単一のエントリポイントとして機能します。

Cloud Manager を使用すると、必要な環境やツールなど、AEM プロジェクトをサポートするクラウドリソースを管理できます。このジャーニーのために、Cloud Manager を完全に理解する必要ありません。ただし、いくつかの基本概念に精通している必要があります。

>[!TIP]
>
>Cloud Manager について詳しく知るには、この記事の [その他のリソース](#additional-resources) の節を参照して、詳細情報へのリンクを確認してください。

### プログラム {#programs}

Cloud Manager にログインすると、1 つ以上の **プログラム** にアクセスできます。プログラムは様々な方法で定義できますが、1 つのブランドアイデンティティに結び付くサイトやエクスペリエンスに関連付けられたものと考えるのが簡単です。

**WKND トラベル＆アドベンチャーエンタープライズ** の代表として Cloud Manager にログインすると、 **WKND ナイトライフ** プログラムと **WKND 裏庭プロジェクト** プログラムを作成するかもしれません。これらのプログラムは両方とも、関連するサイトを管理するための AEM 環境を持つことになります。

### サンドボックス {#sandboxes}

プログラムは、実稼動プログラムまたはサンドボックスプログラムにすることができます。

* **実稼動プログラム** は、プログラムの運用を開始する準備が整えば、最終的には本番のトラフィックを受け入れるために作成します。
* **サンドボックスプログラム** は、トレーニング、デモの実施、有効化、POC などのために作成します。また、ライブトラフィック向けではありません。

AEM 参照デモのアドオンをインストールするには、新しいサンドボックスプログラムを作成する必要があります。

>[!NOTE]
>
>AEM 参照デモのアドオンは、サンドボックスプログラムでのみ使用できます。

## インストールと使用のフロー {#installation-flow}

これで、Cloud Manager の基本的な概念を理解できたので、AEM 参照デモのアドオンをインストールする概念はシンプルです。

1. Cloud Manager にログインします。
1. 新しいサンドボックス AEM プログラムを作成し、プログラムのオプションとして AEM 参照デモのアドオンを有効にします。
1. デモのコンテンツと設定がプログラムにデプロイされます。デモのコンテンツには次が含まれます。
   * AEM の機能を利用した様々な AEM サイトを作成するために使用したサイトテンプレート。ベストプラクティスの事例があらかじめ入力されています。
   * デモコンテンツを管理するための設定ツール。
1. 新しいサンドボックスプログラムで AEM にログインし、クイックサイト作成ツールを使用して、テンプレートに基づいてデモサイトを作成します。
1. 設定ツールを使用してデモサイトとテンプレートを管理します（不要になったら削除するなど）。

## AEM サイトテンプレート {#site-templates}

AEM サイトテンプレートは、サイト用に事前定義されたコンテンツと構造を含むパッケージです。サイトテンプレートは特定のプロジェクトニーズに合わせてカスタマイズできるので、AEM 管理者は新しいサイトを作成するとき、自社のビジネスケースに応じてテンプレートを選択することができます。

AEM 参照デモのアドオンには、様々なテストやデモのニーズに対応できる複数のテンプレートが含まれています。プログラムを作成し、パイプラインをデプロイしてアドオンをインストールしたら、AEM にログインして、多くのデモテンプレートに基づいてサイトを作成できます。

## 次の手順 {#what-is-next}

AEM 参照デモのアドオンジャーニーのこのパートを終了したので、次のことができるようになりました。

* Cloud Manager の基本を理解しました。
* パイプラインで AEM にコンテンツと設定を配信する方法を理解しました。
* 数回クリックするだけで、デモコンテンツがあらかじめ登録された新しいサイトをテンプレートで作成できることがわかりました。

この知識に基づいて、次は [プログラムとパイプラインの作成](create-program.md) のドキュメントを確認して、AEM クイックサイト作成ジャーニーを続行してください。そこでは、アドオンをデプロイするための新しいプログラムとパイプラインを設定する方法を習得します。

## その他のリソース {#additional-resources}

[プログラムとパイプラインの作成](create-program.md) のドキュメントを確認して、クイックサイト作成ジャーニーの次のパートに進むことをお勧めしますが、以下のリソースではこのドキュメントで取り上げた概念についてより詳しく説明しています。追加的なオプションであり、ジャーニーを続ける上で必須のリソースではありません。

* [プログラムとプログラムの種類について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html?lang=ja) - ライブプログラムとサンドボックスプログラムの違いについて知るには、ここから始めてください。
* [サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md) - サイトテンプレートの構造と、サイトテンプレートがサイトの作成にどのように使用されるかについて詳しくは、このドキュメントを参照してください。
* [Cloud Manager ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=ja) - Cloud Manager の機能について詳しくは、詳細な技術ドキュメントを直接参照してください。
