---
title: Experience Hub について
description: Adobe Experience Hub のページについて説明します。
landing-page-description: すべての AEM 機能にアクセスする一元的な出発点である Experience Hub について説明します。
solution: Experience Manager
feature: Authoring, AI Assistant, Central Interface Components, Getting Started, Onboarding, Programs, Workflows
feature-set: Experience Cloud,Experience Manager Sites,Experience Cloud Services
role: Admin, Developer, User
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: a1b0eed7-b74c-4e72-8399-c473bbda9245
source-git-commit: 4ae77b2c9cff253749578127827a12e8483aaf7f
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 65%

---

# Experience Hub について {#aem-experience-hub}

Experience Hub は、Adobe Experience Manager 内のコンテンツ、アセット、サイトを一元管理する出発点となります。 パーソナライズされたエクスペリエンスを提供するように設計された Experience Hub を使用すると、役割と目標に応じて AEM エコシステムをシームレスに操作できます。 目標を効率的に達成するための重要なインサイトと推奨されるアクションを提供します。 Experience Hub は、わかりやすいペルソナ主導型のレイアウトにより、重要なツールにすばやくアクセスでき、すべての AEM 機能をまたいで、合理化された効果的なエクスペリエンスをサポートします。

[AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/)も参照してください。

AEM Experience Hub ワークスペースの概要を表示します（2分40秒）。

>[!VIDEO](https://video.tv.adobe.com/v/3475193/?captions=jpn&learn=on&enablevpops)

<!--
Available as a private beta, Experience Hub offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence Experience Hub's development by providing feedback that helps shape its future and enhances its value for the entire AEM community.
-->

## Experience Hubの概要 {#aem-experience-hub-about}

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックしてホームページを開きます。

   ![Adobe Experience Cloud のホームページ](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. **クイックアクセス**&#x200B;のグループ化で、「[**Experience Manager**](https://experience.adobe.com)」をクリックします。
1. 初回アクセス時に、システムは&#x200B;**コンテンツ作成者**&#x200B;プリセット（ページの右上隅付近に表示）を割り当てます。 これにより、表示されるウィジェット、ナビゲーション項目、コンテンツが制御されます。

   このプリセットはいつでも変更できます。

   ![&#x200B; コンテンツ作成者プリセットを表示するドロップダウンリストが選択されています](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

Adobe Experience Manager ページが更新され、強化されたナビゲーションとインタラクティブウィジェットが使用できるようになりました。 以前のソリューションカードのコレクションでは、次のようなツールにアクセスできました。

* ユニバーサルエディター
* Cloud Manager
* Cloud Acceleration Manager
* ソフトウェア配布
* Adobe Extension Manager
* Brand Portal

>[!IMPORTANT]
>
>表示されるウィジェット、ツール、アーティファクトは、ユーザーペルソナ、使用権限、AEM デプロイメントタイプ（AEM as a Cloud Service または Managed Services 6.5/6.5 LTS）によって異なります。

これらのソリューションは、**ツール**&#x200B;または&#x200B;**サービス**&#x200B;の下のメインナビゲーションに移動しました。 新しいナビゲーション要素により、有効なソリューションに関連付けられたAEM機能にすばやくアクセスできます。 Assets、Adobe Experience Manager Sites、Forms、コンテンツフラグメント、Adobe Cloud Platform Launchなど、さまざまな製品を利用できます。

![Experience Hub 環境](/help/implementing/cloud-manager/assets/experience-hub-author-environments.png)

これらの機能は、主要な本番環境で使用できます。 複数のAEM インスタンスにアクセスできる場合は、対象となる環境を選択します。

![本番環境とステージ環境](/help/implementing/cloud-manager/assets/experience-hub-prod-stage.png)

Experience Hubは、Adobe Experience Managerの中央ハブとして機能し、各ユーザーロール（プリセット）に合わせたウィジェットやアクションを追加する機能へと拡張されています。 自由にカスタマイズでき、このページでは画面に最適なレイアウトを選択できます。 ウィジェットをフィルタリングして、選択したウィジェットだけをメインページに表示するようにすることで、パーソナライズされたエクスペリエンスを実現できます。

![Experience Hub のカスタマイズ](/help/implementing/cloud-manager/assets/experience-hub-custom.png)

ウィジェットは、ニーズや好みに合わせて、ページ上でサイズを変更したり、再配置したりすることもできます。

![Experience Hub のウィジェット](/help/implementing/cloud-manager/assets/experience-hub-widgets.png)

「**オーサリング環境**」セクションには、アクセス可能なすべてのAEM環境が一覧表示され、ソリューションとページへのショートカットが含まれています。 特定の環境をリストの最上部に表示するには、固定します。

下の画像に表示されている「**最近使用したもの**」セクションには、最近 AEM にアクセスしたページが一覧表示されます。 テナントのライセンスに応じて、ウィジェットにはプログラム、パイプライン実行、様々なエディターなどの項目が含まれます。

ページの左上隅付近の&#x200B;**クイックショートカット**&#x200B;には、毎日のタスクを開始するのに役立つ、設定可能なショートカットのリストが用意されています。 リストはカスタマイズ可能で、各アクションは選択した AEM 環境を対象としています。

![オーサリング環境](/help/implementing/cloud-manager/assets/experience-hub-recents.png)

![Experience Hub クイックショートカット](/help/implementing/cloud-manager/assets/experience-hub-quick-shortcuts.png)

実稼動環境のAEM Cloud ServiceまたはManaged Services環境が存在しない場合、選択オプションはグレー表示され、使用できません。

![Experience Hub（本番環境なし）](/help/implementing/cloud-manager/assets/experience-hub-no-prod-environs.png)

## よくある質問（FAQ） {#faq}

+++**Experience HubからCustomer Managed Keysを設定するにはどうすればよいですか？**

プログラムでCMKが有効になっている場合、Experience HubはCMK設定ページへの直接リンクを提供します。 プログラムカードから&#x200B;**Configure CMK**&#x200B;を選択するか、
クイックショートカット。 完全な設定手順については、を参照してください。
AEM as a Cloud Service[&#128279;](/help/security/customer-managed-keys.md)の カスタマー管理キー設定。

+++

+++**Adobe Experience Manager 内の Adobe Experience Hub の主な目的は何ですか？**

Adobe Experience Hub は、Adobe Experience Manager 内のコンテンツ、アセット、サイトを一元管理する出発点として機能し、ユーザーの役割と目標に応じてパーソナライズされた体験を提供します。

+++

+++**Experience Hub は様々なユーザーの役割にどのように対応していますか？**

Experience Hubでは、作成者、アセットライブラリ管理者、IT担当者に対して、ロールベースのビューとクイックアクションが表示されます。 各役割は、必要なツールや機能にすばやくアクセスできます。

+++

+++**Experience Hub のナビゲーションとレイアウトには、どのような機能がありますか？**

Experience Hub では、統合された左ナビゲーションにより、AEM の主要な機能やカスタマイズ可能なウィジェット、クイックアクションが整理されています。 このレイアウトにより、整理整頓された効率的なワークスペースを作成できます。

+++

+++**Experience Hub ワークスペースをパーソナライズする方法を教えてください。**

ユーザーは、ウィジェットの追加、削除、サイズ変更、並べ替えが可能で、クイックアクションをカスタマイズして、ニーズや好みに合わせてワークスペースをカスタマイズできます。

+++

+++**Experience Hub を使用して、どの種類のアクションをすばやく実行できますか？**

Experience Hubでは、ユーザーの役割に合わせてカスタマイズされた、一般的なタスクのワンクリックショートカットを提供しています。

+++

+++**Experience Hub では、AEM のさまざまな機能へのナビゲーションが容易になりますか？**

**ツール**&#x200B;または&#x200B;**サービス**&#x200B;の下にある Experience Hub のメインナビゲーションでは、Assets、Sites、Forms、コンテンツフラグメント、ローンチなどの AEM 機能にすばやくアクセスできます。

+++

+++**Experience Hub でのウィジェットの重要性は何ですか？**

Experience Hub のウィジェットは、ユーザーが作業を効率的に管理できるカスタマイズ可能な要素であり、最近のアクティビティの追跡や製品更新の把握などに役立ちます。

+++

+++**Experience Hub を使用して複数の AEM 環境を管理するにはどうすればよいですか？**

ユーザーは、対象とする環境を選択し、お気に入りをピン留めして上位に固定することができます。 ショートカットを使用すると、これらの環境内のソリューションとページが開きます。

+++

+++**AEM で AI アシスタントはどのような役割を果たしますか？**

AEM の AI アシスタントは、前提条件を満たしたユーザーが利用でき、組織内でのさらなるサポートとインサイトを提供します。

+++

+++**AEM Cloud Service または Managed Services の本番環境が存在しない場合はどうなりますか？**

本番環境が存在しない場合、Experience Hub の選択オプションはグレー表示になり、使用できなくなります。

+++

## AEM の AI アシスタント

前提条件の条件[&#128279;](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)を完了したお客様の場合、AEMのAI アシスタントは、お客様の組織のユーザーが利用できます。 [AEM の AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)を参照してください。
