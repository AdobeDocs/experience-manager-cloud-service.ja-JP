---
title: パーソナライゼーションとコンテンツのターゲティング
description: AEMを使用して、パーソナライズされたターゲットコンテンツを作成する方法を説明します
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: f2466cb5cda759f0c97cd69810d208d47fb73b98
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 12%

---


# パーソナライゼーションとコンテンツのターゲティング {#personalization-and-content-targeting}

顧客に提供する Web コンテンツのパーソナライゼーションとは、顧客の興味やニーズに合わせてエクスペリエンスを調整することを意味します。 これは、顧客に関する情報に基づいて行うことができます。例：買い物の概要、年齢、性別、地域など。

Adobe Experience Manager as a Cloud Service(AEM) では、選択したコンテンツを作成し、個々のエクスペリエンスを表示するオーディエンス（エンドユーザーのグループ）を指定できます。 つまり、特定のオーディエンスでパーソナライズされたエクスペリエンスをターゲットに設定しています。

読者がオンラインになると、ターゲティングエンジンは、エンドユーザーに関する利用可能な情報を確認し、エクスペリエンスの定義と比較します。 その後、エンジンが *&quot;decifies&quot;* どのパーソナライズされたエクスペリエンスを表示するか。

AEMは、次のツールのフレームワークを提供します。

* 利用可能な顧客情報に応じて、様々なオーディエンスに適したターゲットコンテンツをオーサリングします。
* 既知のユーザー情報をオーディエンス定義に対して解決するために使用するルールを定義する。
* ターゲットを絞り込んでパーソナライズされたエクスペリエンスを表示するためのページの設定を使用して、特定のコンテンツを現在のエンドユーザーに適用できます。

次の概要では、AEM as a Cloud Serviceのパーソナライゼーションに使用される用語の一部を示し、推奨されるアクション順を示します。

## Experience {#experience}

エクスペリエンスとは、エンドユーザーに表示するコンテンツです。

## Personalized Experience {#personalized-experience}

パーソナライズされたエクスペリエンスとは、限られたオーディエンスに対して表示されるエクスペリエンスです。 オーディエンスはユーザーによって定義され、コンテンツは、現在のエンドユーザーに関する既知の情報がそのオーディエンス定義に対応する場合にのみ表示されます。

ページを作成する際に、複数のエクスペリエンスを定義し、各エクスペリエンスを 1 つ以上のオーディエンスに解決します。 オーディエンスが解決されない場合は、デフォルトのエクスペリエンスが表示されます。

### オファー {#offer}

オファーは、パーソナライズされたエクスペリエンスで、多くの場合、期間を限定して利用できます。

例えば、サンプル Web サイトのページでは、オファーをティーザー画像として使用して、ページの上部に表示することができます。 30 歳以上の人と 30 歳未満の人は、異なるオファーをエクスペリエンスティーザーとして表示します。

## 対象読者 {#audience}

オーディエンスは、パーソナライズされたコンテンツでターゲットに設定するエンドユーザーのグループです。 訪問者が Web ページを開く際、ページロジックは既知の情報に基づいて、訪問者が属するオーディエンスを決定します。 この評価に基づいて、そのオーディエンス用に作成したコンテンツがAEMに表示されます。

オーディエンスは、マーケティングセグメントに基づいています。 これらは、AEMまたはAdobe Targetで作成されます。オーディエンスコンソールを使用して、AEMで直接Adobe Targetオーディエンスを作成できます。

### セグメント {#segment}

AEM ContextHub 内では、オーディエンスは、ルール（条件）に基づくセグメントとして定義されます。 その後、これらは解決され、必要なコンテンツがレンダリングされます。

## アクティビティ {#activity}

アクティビティ：

* 特定のエクスペリエンスと特定のオーディエンス（セグメント）のマッピングを定義します
* ターゲティングが適用される期間を定義します。
* を識別します。 [ターゲティングエンジン](#targeting-engine) ページが使用する

「 」アクティビティは、パーソナライゼーションアクティビティか、「 A/B テスト」アクティビティ (AEMとAdobe Targetのパーソナライゼーションワークフローの場合 ) のどちらかです。

例えば、1 つのアクティビティで、2 つの異なるオーディエンス用のエクスペリエンスを定義できます。30 歳以上の人々と 30 歳未満の人々です。 その後、Web サイトの 1 ページに、閲覧者ごとに異なる製品が表示される場合があります。

また、季節商品に注目を集めたティーザーが商品カタログに含まれている場合もあります。 したがって、サマースポーツアクティビティは、ティーザーが夏季のターゲットとするオーディエンスを定義する場合があります。

以下を使用： [アクティビティコンソール](/help/sites-cloud/authoring/personalization/activities.md) のアクティビティを作成および管理するには、以下を実行します。 [ブランド](#brand). また、 [ターゲットコンテンツ](/help/sites-cloud/authoring/personalization/targeted-content.md) と [ターゲットモード](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Brand  {#brand}

ブランドには、様々なマーケティングアクティビティや領域が含まれます。

アクティビティコンソールを使用してブランドを作成すると、そのブランドがオファーコンソールにも表示されます。

### 領域 {#area}

領域は、ブランドの下位区分です。

## ターゲットモード {#targeting-mode}

オーサリング時に、パーソナライゼーション用のコンポーネントをアクティベートおよび設定するために使用される編集モードです。

以下が可能です。 [ターゲットコンテンツのオーサリング](/help/sites-cloud/authoring/personalization/targeted-content.md) AEMのターゲットモードを使用して ターゲットモードと Target コンポーネントは、マーケティングアクティビティのエクスペリエンス用コンテンツを作成するためのツールを提供します。

## エクスペリエンスフラグメント {#experience-fragments}

エクスペリエンスを構成するコンポーネントのグループセット。

[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) は、エクスペリエンスを作成するためのコンテンツと情報（スタイル設定など）で構成されます。ページのオーサリング時に直接使用できます。 これらは、AEMページのサブセットと考えることができます。 コンテンツ作成者は、Sites ページやサードパーティ製システムを含む複数のチャネルをまたいでコンテンツを再利用できます。

パーソナライゼーションの例では、タイトル、画像、説明およびコールトゥアクションボタンを組み合わせて、ティーザーエクスペリエンスを形成できます。 エクスペリエンスフラグメントの使用は、Adobe Targetのパーソナライゼーションの主な要素です。

## ターゲティングエンジン {#targeting-engine}

ターゲティングエンジンは、ターゲットコンテンツのロジックを解決するメカニズムです。 使用可能なターゲティングエンジンには AEM と Adobe Target の 2 種類があり、どちらを使用するかは[アクティビティ](/help/sites-cloud/authoring/personalization/activities.md)で設定します。

ターゲティングエンジンは、使用するパーソナライゼーションシステムを決定するプラットフォームまたはメカニズムです。

現在、AEMは次を使用できます。

* [AEM ContextHub](#aem-contexthub) ( 標準AEM)
* の [Adobe Target](#adobe-target) パーソナライゼーションエンジン

>[!CAUTION]
>
>1 つのAEMページで、両方のエンジンを同時に使用することはできません。
>
>同じサイト内の別のページで、両方のエンジンを使用できます。

### AEM ContextHub {#aem-contexthub}

AEMには、組み込みのターゲティングエンジンが用意されています。 [ContextHub](/help/implementing/developing/personalization/contexthub.md) はページリクエストを処理し、表示するコンテンツを決定します。 AEM ターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義に使用できるセグメントは、AEM で作成されるセグメントのみとなります。

### Adobe Target {#adobe-target}

この [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) ターゲティングエンジンによって、ページ訪問から収集された情報がAdobe Targetで追跡されます。

* このターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には Adobe Target から読み込んだセグメントを使用します。
* Adobe Target エンジンを使用するアクティビティは、[Target と同期](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target)します。

このエンジンを使用できるのは、[Adobe Target と統合](/help/sites-cloud/integrating/integrating-adobe-target.md)している場合のみです。

## パーソナライズされたコンテンツの設定方法 {#how-to-setup-personalized-content}

パーソナライズされたコンテンツを配信するには、次のように様々な手順と定義が必要です。

1. 次のいずれかの方法でターゲティングエンジンを設定します。

   1. 設定 [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. との統合 [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. オーディエンスを設定します。

   1. ターゲティングエンジンに応じて、 [ターゲットオーディエンス](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) または [ContextHub セグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)とルールを組み合わせて使用します。

1. を [ブランドとアクティビティ](/help/sites-cloud/authoring/personalization/activities.md).

1. 様々なオーディエンスに表示するエクスペリエンスの選択を作成します。

1. これらのエクスペリエンスをパーソナライズするには、 [ターゲット](/help/sites-cloud/authoring/personalization/targeted-content.md) 特定のオーディエンス（セグメント）に割り当てられます。