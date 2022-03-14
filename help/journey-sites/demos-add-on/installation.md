---
title: 参照デモアドオンのインストールについて
description: Cloud Manager と、Cloud Manager を使用してアドオンをインストールする方法について説明します。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# 参照デモアドオンのインストールについて {#understand-installation}

Cloud Manager と、Cloud Manager を使用してアドオンをインストールする方法について説明します。

>[!TIP]
>
>既に Cloud Manager の使用経験がある場合や、アドオンの設定と使用に直接アクセスしたい場合は、次に進むことができます： [プログラムとパイプラインの作成](create-program.md)
>
>Cloud Manager とAEMが連携してデモ環境を作成する方法、および独自のデモ環境をセットアップして使用する方法を学びたい場合は、現在のドキュメントを引き続きお読みください。

## 目的 {#objective}

このドキュメントでは、参照デモアドオンのインストールプロセスの仕組みを理解し、異なる要素がどのように連携するかを示します。 ドキュメントを読めば、以下が可能です。

* Cloud Manager の基本を理解している。
* パイプラインがAEMにコンテンツと設定を配信する方法を説明します。
* 数回のクリックでデモコンテンツが事前入力された新しいサイトをテンプレートで作成する方法をご覧ください。

このドキュメントでは、インストールを開始するジャーニーの次のステップに進む前に、AEM Reference Demo Add-On のこれらの基本的な部分を理解することに焦点を当てています。

このジャーニーを順を追って進めることをお勧めしますが、Cloud Manager の使用経験が既にある場合や、アドオンの設定と使用に直接アクセスしたい場合は、スキップしてかまいません [プログラムとパイプラインの作成](create-program.md)

## 担当ロール {#responsible-role}

このジャーニーは、 **ビジネスオーナー** 組織の Cloud Manager での役割。

## 要件と前提条件 {#requirements-prerequisites}

参照デモのアドオンについて学び、使用を開始するための最小要件があります。

### 知識 {#knowledge}

* Cloud Manager の基本知識

### ツール {#tools}

* メンバーになる **ビジネスオーナー** 組織の Cloud Manager での役割

## Cloud Manager について {#cloud-manager}

Cloud Manager は、AEM as a Cloud Serviceの必須コンポーネントで、プラットフォームの単一のエントリポイントとして機能します。

Cloud Manager は、必要な環境やツールなど、AEMプロジェクトをサポートするクラウドリソースの管理に使用します。 このジャーニーの目的上、Cloud Manager に関する完全な理解は必要ありません。 ただし、いくつかの基本概念に精通している必要があります。

>[!TIP]
>
>Cloud Manager について詳しくは、 [その他のリソース](#additional-resources) この記事の節を参照してください。

### プログラム {#programs}

Cloud Manager にログインすると、1 つ以上の **プログラム**. プログラムは様々な方法で定義できますが、1 つのブランドアイデンティティに関連付けられたサイトやエクスペリエンスに関連付けられていると考えるのが最も簡単です。

次の Cloud Manager にサインインしている場合： **WKND Travel and Adventure Enterprises**&#x200B;を使用する場合、 **WKND Nightlife** プログラムと **WKND Backyard プロジェクト** プログラム。 これらの両方のプログラムには、関連するサイトを管理するAEM環境があります。

### サンドボックス {#sandboxes}

プログラムは、実稼動プログラムまたはサンドボックスプログラムにすることができます。

* **実稼働プログラム** は、プログラムの運用開始準備が整った時点で、最終的にライブトラフィックを許可するように作成されます。
* **サンドボックスプログラム** は、トレーニング、実行デモ、有効化、POC などに対して作成されます。 およびは、ライブトラフィック向けではありません。

AEM Reference Demos Add-On をインストールするには、新しいサンドボックスプログラムを作成する必要があります。

>[!NOTE]
>
>AEM Reference Demos Add-On は、サンドボックスプログラムでのみ使用できます。

## インストールおよび使用フロー {#installation-flow}

これで、AEM Manager の基本的な概念を理解できたので、Cloud Reference Demos Add-On のインストールは概念的にシンプルです。

1. Cloud Manager にログインします。
1. 新しいサンドボックスAEMプログラムを作成し、プログラムのオプションとしてAEM Reference Demos Add-On をアクティブ化します。
1. デモコンテンツと設定がプログラムにデプロイされます。 デモコンテンツには次が含まれます。
   * AEMの機能を使用して様々なAEMサイトを作成するために使用されるサイトテンプレートには、ベストプラクティスの例があらかじめ入力されています。
   * デモコンテンツを管理する設定ツール。
1. 新しいサンドボックスプログラムでAEMにログインし、クイックサイト作成ツールを使用して、テンプレートに基づいてデモサイトを作成します。
1. 設定ツールを使用して、不要になった場合に削除するなど、これらのデモサイトとテンプレートを管理します。

## AEM Site Templates {#site-templates}

AEM Site Templates は、サイト用の事前定義済みのコンテンツと構造を含むパッケージです。 サイトテンプレートは、特定のプロジェクトのニーズに合わせてカスタマイズできるので、AEM管理者が新しいサイトを作成する際に、自社のビジネスケースに適用されるテンプレートから選択できます。

AEM Reference Demos Add-On には、様々なテストおよびデモのニーズに対応する複数のテンプレートが含まれています。 プログラムを作成し、パイプラインをデプロイしてアドオンをインストールしたら、AEMにログインして、多くのデモテンプレートに基づいてサイトを作成できます

## 次のステップ {#what-is-next}

これで、AEM Reference Demos アドオンのジャーニーのこの部分が完了しました。完了したら、次の手順を実行します。

* Cloud Manager の基本を理解している。
* パイプラインがAEMにコンテンツと設定を配信する方法を説明します。
* 数回のクリックでデモコンテンツが事前入力された新しいサイトをテンプレートで作成する方法をご覧ください。

この知識に基づいてドキュメントを次に確認し、AEMクイックサイト作成のジャーニーを続行します [プログラムとパイプラインの作成](create-program.md) ここでは、新しいプログラムとパイプラインを設定してアドオンをデプロイする方法について説明します。

## その他のリソース {#additional-resources}

クイックサイト作成ジャーニーの次の部分に進むことをお勧めしますが、ドキュメントを確認してください [プログラムとパイプラインの作成](create-program.md) 以下に、このドキュメントで取り上げたいくつかの概念について詳しく説明する、その他のオプションのリソースを示します。ただし、このジャーニーを続行する必要はありません。

* [プログラムとプログラムの種類について](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html)  — ライブプログラムとサンドボックスプログラムの違いについては、ここから始めてください。
* [サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)  — サイトテンプレートの構造と、サイトの作成にどのように使用されるかについて詳しく知りたい場合は、このドキュメントを参照してください。
* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Cloud Manager の機能の詳細については、詳細な技術ドキュメントを直接お問い合わせください。
