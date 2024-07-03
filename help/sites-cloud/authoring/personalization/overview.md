---
title: パーソナライゼーションとコンテンツのターゲティング
description: パーソナライズされたターゲットコンテンツを AEM で作成する方法について説明します。
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '1054'
ht-degree: 100%

---


# パーソナライゼーションとコンテンツのターゲティング {#personalization-and-content-targeting}

顧客に提供する web コンテンツのパーソナライゼーションとは、顧客の関心やニーズに合わせてエクスペリエンスを調整することです。これは、買い物の概要、年齢、性別、地域など、顧客に関する情報に基づいて行うことができます。

Adobe Experience Manager as a Cloud Service（AEM）では、様々なコンテンツを作成して、個々のエクスペリエンスを提供するオーディエンス（エンドユーザーのグループ）を指定することができます。つまり、パーソナライズしたエクスペリエンスのターゲットを特定のオーディエンスに設定しています。

読者がオンラインになると、ターゲティングエンジンは、エンドユーザーに関する入手可能な情報を精査して、エクスペリエンスの定義と比較します。次に、エンジンは、パーソナライズされたどのエクスペリエンスを表示するかを「*決定*」します。

AEM には、次の用途に使用できるツールのフレームワークが用意されています。

* 入手可能な顧客情報に応じて、様々なオーディエンスに適したターゲットコンテンツをオーサリングします。
* オーディエンス定義に照らして既知のユーザー情報を解決するためのルールを定義します。
* ターゲットを絞ったパーソナライズされたエクスペリエンスを提示する（現在のエンドユーザーに適用可能な特定のコンテンツをレンダリングする）ようにページを設定します。

次の概要では、AEM as a Cloud Service でのパーソナライゼーションに使用する一部の用語と、アクションの推奨される順序について紹介します。

## エクスペリエンス {#experience}

エクスペリエンスとは、エンドユーザーに表示するコンテンツです。

## パーソナライズされたエクスペリエンス {#personalized-experience}

パーソナライズされたエクスペリエンスとは、限られたオーディエンスに表示するエクスペリエンスです。オーディエンスは開発者によって定義され、コンテンツは、現在のエンドユーザーに関する既知の情報がそのオーディエンスの定義に対応する場合にのみ表示されます。

ページを作成する際は、複数のエクスペリエンスを定義し、各エクスペリエンスが 1 つ（または複数）のオーディエンスに対応するようにします。オーディエンスに対応するエクスペリエンスが見つからない場合は、デフォルトのエクスペリエンスが表示されます。

### オファー {#offer}

オファーは、パーソナライズされたエクスペリエンスであり、多くの場合、期間限定で利用できます。

例えば、サンプルの web サイトのページでは、上部に表示されるティーザー画像としてオファーを使用することができます。また、30 歳以上のユーザーと 30 歳未満のユーザーに、エクスペリエンスティーザーとして異なるオファーを表示します。

## オーディエンス {#audience}

オーディエンスとは、パーソナライズされたコンテンツのターゲットとして設定するエンドユーザーのグループです。訪問者が web ページを開くと、そのページのロジックが既知の情報に基づいて、訪問者が属するオーディエンスを決定します。その評価に基づいて、そのオーディエンス向けに作成したコンテンツが AEM によって表示されます。

オーディエンスは、マーケティングセグメントに基づいています。これらは AEM または Adobe Target で作成されます。オーディエンスコンソールを使用して、AEM で直接 Adobe Target オーディエンスを作成できます。

### セグメント {#segment}

AEM ContextHub 内では、オーディエンスはルール（条件）に基づいてセグメントとして定義されます。その後、これらが解決されて、必要なコンテンツがレンダリングされます。

## アクティビティ {#activity}

アクティビティは、

* 特定のオーディエンス（セグメント）と特定のエクスペリエンスのマッピングを定義します。
* ターゲティングが適用される期間を定義します。
* ページで使用される[ターゲティングエンジン](#targeting-engine)を識別します。

アクティビティは、パーソナライゼーションアクティビティか A/B テストアクティビティのいずれかです（AEM および Adobe Target パーソナライゼーションワークフローの場合）。

例えば、あるアクティビティが「30 歳以上のユーザー」と「30 歳未満のユーザー」という 2 つの異なるオーディエンス向けのエクスペリエンスを定義するものとします。その場合、web サイトのページには、オーディエンスごとに異なる製品が表示される可能性があります。

または、別の例として、商品カタログには、季節商品に焦点を絞ったティーザーが含まれる可能性があります。そのため、サマースポーツアクティビティでは、これらのティーザーが夏季にターゲットとするオーディエンスを定義できます。

[ブランド](#brand)のアクティビティを作成および管理するには、[アクティビティコンソール](/help/sites-cloud/authoring/personalization/activities.md)を使用します。また、[ターゲティングモード](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode)を使用して[ターゲットコンテンツ](/help/sites-cloud/authoring/personalization/targeted-content.md)を作成する際に、アクティビティを作成することもできます。

### ブランド {#brand}

ブランドには、様々なマーケティングアクティビティや領域が含まれます。

アクティビティコンソールを使用してブランドを作成すると、そのブランドがオファーコンソールにも表示されます。

### 領域 {#area}

領域は、ブランドの下位区分です。

## ターゲティングモード {#targeting-mode}

オーサリング時に、パーソナライゼーション用のコンポーネントをアクティブ化および設定するために使用する編集モードです。

AEM のターゲティングモードを使用して、[ターゲットコンテンツをオーサリング](/help/sites-cloud/authoring/personalization/targeted-content.md)できます。ターゲティングモードと Target コンポーネントは、マーケティングアクティビティのエクスペリエンス用コンテンツを作成するためのツールを提供します。

## エクスペリエンスフラグメント {#experience-fragments}

エクスペリエンスを構成するコンポーネントのグループセット。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md#personalization-experience-fragment)は、エクスペリエンスを作成するためのコンテンツと情報（スタイル設定など）で構成され、ページのオーサリング時に直接使用できます。これらは、AEM ページのサブセットと考えることができます。コンテンツ作成者は、Sites ページやサードパーティ製システムなどの複数のチャネルからコンテンツを再利用できます。

パーソナライゼーションの例では、タイトル、画像、説明およびコールトゥアクションボタンを組み合わせて、ティーザーエクスペリエンスを形成することができます。 エクスペリエンスフラグメントの使用は、Adobe Target パーソナライズ機能を利用する際の重要な部分を占めます。

## ターゲティングエンジン {#targeting-engine}

ターゲティングエンジンは、ターゲットコンテンツのロジックを動かすメカニズムです。使用可能なターゲティングエンジンには AEM と Adobe Target の 2 種類があり、どちらを使用するかは[アクティビティ](/help/sites-cloud/authoring/personalization/activities.md)で設定します。

ターゲティングエンジンは、使用するパーソナライゼーションシステムを決定するプラットフォームまたはメカニズムです。

現在、AEM では次のものを使用できます。

* [AEM ContextHub](#aem-contexthub)（標準 AEM）
* [Adobe Target](#adobe-target) パーソナライゼーションエンジン

>[!CAUTION]
>
>単一の AEM ページで両方のエンジンを同時に使用することはできません。
>
>同じサイト内の別々のページで両方のエンジンを使用することはできます。

### AEM ContextHub {#aem-contexthub}

AEM には、ページリクエストの処理や表示するコンテンツの決定を行う組み込みのターゲティングエンジン [ContextHub](/help/implementing/developing/personalization/contexthub.md) が用意されています。AEM ターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には、AEM で作成されるセグメントのみを使用できます。

### Adobe Target {#adobe-target}

[Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) ターゲティングエンジンを使用すると、ページへの訪問から収集された情報が Adobe Target で追跡されます。

* このターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には、Adobe Target から読み込んだセグメントを使用します。
* Adobe Target エンジンを使用するアクティビティは、[Target と同期](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)します。

このエンジンを使用できるのは、[Adobe Target と統合](/help/sites-cloud/integrating/integrating-adobe-target.md)している場合のみです。

## パーソナライズされたコンテンツの設定方法 {#how-to-setup-personalized-content}

パーソナライズされたコンテンツを配信するには、次のように様々な手順と定義が必要です。

1. 次のいずれかの方法でターゲティングエンジンを設定します。

   1. [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) の設定
   1. [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) との統合

1. オーディエンスを設定します。

   1. ターゲティングエンジンに応じて、[ターゲットオーディエンス](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=ja)または [ContextHub セグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)をルールとともに定義します。

1. [ブランドとアクティビティ](/help/sites-cloud/authoring/personalization/activities.md)を作成します。

1. 様々なオーディエンスに見せる、厳選したエクスペリエンスを作成します。

1. 特定のオーディエンス（セグメント）に[ターゲティング](/help/sites-cloud/authoring/personalization/targeted-content.md)することで、これらのエクスペリエンスをパーソナライズします。