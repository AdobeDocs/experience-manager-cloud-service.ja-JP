---
title: パーソナライズとコンテンツのターゲティング
description: AEMがパーソナライズされたコンテンツを作成する方法を説明します。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# パーソナライズとコンテンツのターゲティング {#personalization}

## パーソナライズとコンテンツのターゲティング {#personalization-and-content-targeting}

AEM には、ターゲットとなるコンテンツをオーサリングして、パーソナライズされたエクスペリエンスを提供するためのツールのフレームワークが用意されています。

## ターゲットモード {#targeting-mode}

[AEM のターゲットモードを使用してターゲットコンテンツをオーサリングします。](/help/sites-cloud/authoring/personalization/targeted-content.md)ターゲットモードと Target コンポーネントは、マーケティングアクティビティのエクスペリエンス用コンテンツを作成するためのツールを提供します。

## アクティビティ {#activities}

アクティビティは、マーケティング戦略を定義し、整理するためのものです。アクティビティは、ターゲットとするオーディエンスと、そのターゲット設定の適用期間から構成されます。

例えば、商品カタログに季節の商品に注目するティーザーを含めることができます。 Summer Sports アクティビティは、このティーザーが夏季のターゲットとするマーケティングセグメントを定義します。

アクティビティは、ページが使用する[ターゲティングエンジン](#targeting-engine)も識別します。

Use the [Activities console](/help/sites-cloud/authoring/personalization/activities.md) to create and manage the activities for your brands. You can also create activities as you [author targeted content](/help/sites-cloud/authoring/personalization/targeted-content.md).

## エクスペリエンス {#experiences}

アクティビティごとに、ターゲットとするオーディエンスを識別する 1 つ以上のエクスペリエンスを定義します。AEMでは、各エクスペリエンスを構成するコンテンツを制御できます。

オーディエンスは、AEM または Adobe Target で作成されたマーケティングセグメントをベースとします。訪問者が Web ページを開くと、そのページのロジックによってオーディエンスが判断され、そのオーディエンス向けに作成されたコンテンツが表示されます。

例えば、あるアクティビティが「30 歳以上の女性」と「30 歳未満の女性」という 2 つの異なるオーディエンス用のエクスペリエンスを定義するものとします。Webサイトの女性用ページには、エクスペリエンスごとに異なる製品が表示される場合があります。

1 つのアクティビティに複数のエクスペリエンスを定義できます。[アクティビティコンソール](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console)または[ターゲットモード](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode)を使用して、アクティビティにエクスペリエンスを追加できます。

## オファー {#offers}

オファーは、それぞれのエクスペリエンスでページ上に表示されるコンテンツです。オーディエンス向けコンテンツの効果を最大限に高めるには、異なるエクスペリエンスに異なるオファーを使用します。

例えば、サンプルWebサイトの女性用ページでは、ページの上部に表示されるティーザー画像としてオファーを使用できます。 30 歳以上の女性向けエクスペリエンスと、30 歳未満の女性向けエクスペリエンスには、それぞれ異なるオファーをティーザーとして使用します。

複数のエクスペリエンスで使用できるオファーを作成するには、[オファーコンソール](/help/sites-cloud/authoring/personalization/offers.md)を使用します。[ターゲットコンテンツをオーサリング](/help/sites-cloud/authoring/personalization/targeted-content.md)するときは、単一エクスペリエンス用のオファーを作成するか、オファーライブラリからオファーを追加します。

## ターゲティングエンジン {#targeting-engine}

ターゲティングエンジンは、ターゲットコンテンツ用のロジックを動かすメカニズムです。使用可能なターゲティングエンジンには AEM と Adobe Targeting の 2 種類があり、どちらを使用するかは[アクティビティ](/help/sites-cloud/authoring/personalization/activities.md)で設定します。

### AEM {#aem}

AEM は、ページリクエストの処理や、表示コンテンツの判断をおこなう組み込みのターゲティングエンジンを備えています。AEM ターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義に使用できるセグメントは、AEM で作成されるセグメントのみとなります。

### Adobe Target {#adobe-target}

Adobe Target ターゲティングエンジンを使用すると、ページの訪問から収集された情報が Adobe Target で追跡されます。

* このターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には Adobe Target から読み込んだセグメントを使用します。
* Adobe Target エンジンを使用するアクティビティは、[Target と同期](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)します。

You can use this engine when you have integrated with Adobe Target. <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
