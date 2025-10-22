---
title: Experience Hub について
description: Adobe Experience Hub のページについて説明します。
landing-page-description: すべての AEM 機能にアクセスする一元的な出発点である Experience Hub について説明します。
solution: Experience Manager
feature: Authoring, AI Assistant, Central Interface Components, Getting Started, Onboarding, Programs, Workflows
feature-set: Experience Cloud,Experience Manager Sites,Experience Cloud Services
role: Admin, Architect, Developer, User
exl-id: a1b0eed7-b74c-4e72-8399-c473bbda9245
source-git-commit: e317db6747b6a47e2245c2816659188686ca7820
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 9%

---

# Experience Hub について {#aem-experience-hub}

Experience Hubは、Adobe Experience Manager内のコンテンツ、アセット、サイトを一元的に管理するための出発点となります。 Experience Hubはパーソナライズされたエクスペリエンスを提供するように設計されており、ユーザーの役割と目標に応じてAEM エコシステムをシームレスに移動できます。 ガイドとして機能し、目的を効率的に達成するのに役立つ重要なインサイトと推奨されるアクションを提供します。明確なペルソナ駆動型のレイアウトにより、Experience Hubは重要なツールにすばやくアクセスでき、すべてのAEM機能で合理化された効果的なエクスペリエンスをサポートします。

再考されたAEM Experience Hub Workspace のクイックツアー（2 分 40 秒）をご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3475190/?learn=on&enablevpops)

<!--
Available as a private beta, Experience Hub offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence Experience Hub's development by providing feedback that helps shape its future and enhances its value for the entire AEM community. -->

## Experience Hubアップを閉じる {#aem-experience-hub-about}

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックしてホームページを開きます。

   ![Adobe Experience Cloudのホームページ &#x200B;](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. **クイックアクセス** グループ化で、[**Experience Manager**](https://experience.adobe.com) をクリックします。
1. 初回アクセス時には、**コンテンツ作成者** プリセット（ページの右上隅付近に表示）が割り当てられます。 表示されるウィジェット、ナビゲーション項目およびコンテンツを制御します。

   このプリセットはいつでも変更できます。

   ![&#x200B; 「コンテンツ作成者」プリセットを表示するドロップダウンリストが選択されている &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

Adobe Experience Managerページが更新され、ナビゲーションが強化され、インタラクティブウィジェットが追加されました。 以前のソリューションカードのコレクションでは、次のようなツールへのアクセスが可能でした。

* ユニバーサルエディター
* Cloud Manager
* Cloud Acceleration Manager
* ソフトウェア配布
* Extension Manager
* Brand Portal

>[!IMPORTANT]
>
>表示されるウィジェット、ツールおよびアーティファクトは、ユーザーのペルソナ、使用権限およびAEM デプロイメントタイプ（AEM as a Cloud ServiceまたはManaged Services 6.5/6.5 LTS）によって異なります。

これらのソリューションは、**ツール** または **サービス** の下のメインナビゲーションに移動しました。 新しいナビゲーション要素により、対応するソリューションに関連するAEM機能にすばやくアクセスできます。 Assets、Sites、Forms、コンテンツフラグメント、ローンチなどに移動します。

![Experience Hub環境 &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-author-environments.png)

これらの機能をプライマリ実稼動環境で使用します。 複数のAEM インスタンスにアクセスできる場合は、ターゲットにする環境を選択します。

![&#x200B; 実稼動環境とステージ環境 &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-prod-stage.png)

Adobe Experience Managerの中央ハブとして機能するExperience Hub ページには、各ユーザーロール（プリセット）に合わせて調整された追加のウィジェットとアクションが用意されています。 ページは完全にカスタマイズ可能で、画面に最適なレイアウトを選択できます。 ウィジェットをフィルタリングして、選択したウィジェットのみをメインページに表示し、パーソナライズされたエクスペリエンスを提供できます。

![&#x200B; カスタマイズされたExperience Hub](/help/implementing/cloud-manager/assets/experience-hub-custom.png)

ウィジェットは、ニーズや環境設定に合わせてサイズを変更したり、ページ上で再配置したりすることもできます。

![Experience Hub ウィジェット &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-widgets.png)

「**オーサリング環境**」セクションには、アクセスしてソリューションやページへのショートカットを含めることができるすべてのAEM環境が一覧表示されます。 特定の環境をピン留めして、リストの上部に保持できます。

次の図に示す **最近** セクションには、AEMで最近アクセスしたページが一覧表示されます。 テナントのライセンスに応じて、プログラム、パイプライン実行、Assets、ページエディター、フォームエディターなどがウィジェットに含まれる場合があります。

ページの左上隅付近にある **クイックショートカット** には、日々のタスクの開始に役立つ、設定可能なショートカットのリストが用意されています。 このリストはカスタマイズ可能で、各アクションは選択したAEM環境をターゲットにします。

![&#x200B; オーサリング環境 &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-recents.png)

![Experience Hubのクイックショートカット &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-quick-shortcuts.png)

AEM Cloud Service またはManaged Servicesの実稼動環境が存在しない場合は、選択オプションがグレー表示され選択できません。

![Experience Hub実稼動環境がありません &#x200B;](/help/implementing/cloud-manager/assets/experience-hub-no-prod-environs.png)

## よくある質問（FAQ） {#faq}

+++**Adobe Experience ManagerにおけるAdobe Experience Hubの主な目的は何ですか？**

Adobe Experience Hubは、Adobe Experience Manager内のコンテンツ、アセット、サイトを一元的に管理し、ユーザーの役割と目標に基づいてパーソナライズされたエクスペリエンスを提供する出発点として機能します。

+++

+++**Experience Hubは様々なユーザーロールにどのように適応しますか？**

Experience Hubでは、作成者、アセットライブラリ担当者、管理者および IT 者向けのロールベースビューとクイックアクションを示します。 各役割は、必要なツールと機能にすばやくアクセスできます。

+++

+++**Experience Hubのナビゲーションとレイアウトの機能には何がありますか？**

Experience Hubでは、左側の統合ナビゲーションを使用して、AEMのコア機能、カスタマイズ可能なウィジェット、クイックアクションを整理します。 このレイアウトにより、整理された効率的なワークスペースが作成されます。

+++

+++**Experience Hub Workspace をパーソナライズするにはどうすればよいですか？**

ユーザーは、ウィジェットの追加、削除、サイズ変更、並べ替えを行ったり、クイックアクションをカスタマイズして必要や好みに応じてワークスペースをカスタマイズしたりできます。

+++

+++**Experience Hubを使用すると、どのようなアクションをすぐに実行できますか？**

Experience Hubでは、ユーザーのロールに合わせて、コンテンツの作成、アセットのアップロード、チームアクセスの管理などの重要なタスクを行うためのワンクリックショートカットが用意されています。

+++

+++**Experience Hubを使用すると、様々なAEM機能に簡単に移動できますか？**

**ツール** または **サービス** の下にあるExperience Hubのメインナビゲーションを使用すると、Assets、Sites、Forms、コンテンツフラグメント、ローンチなどのAEM機能にすばやくアクセスできます。

+++

+++**Experience Hubにおけるウィジェットの重要性は何ですか？**

Experience Hubのウィジェットはカスタマイズ可能な要素で、最近のアクティビティのトラッキングや商品のアップデートに関する情報の保持など、ユーザーが作業を効率的に管理するのに役立ちます。

+++

+++**Experience Hubを使用して複数のAEM環境を管理するにはどうすればよいですか？**

ユーザーは、ターゲットにする環境を選択し、お気に入りをピン留めして、上部に表示できます。 ショートカットを使用すると、これらの環境内のソリューションやページを開くことができます。

+++

+++**AI アシスタントはAEMでどのような役割を果たしますか？**

AEMの AI アシスタントは、前提条件を満たしたユーザーが利用できるので、組織内でさらにサポートやインサイトを得ることができます。

+++

+++**AEM Cloud Service またはManaged Servicesの実稼動環境が存在しない場合はどうなりますか？**

実稼動環境が存在しない場合は、Experience Hubの選択オプションがグレー表示され、使用できません。

+++

## AEM の AI アシスタント

[前提条件の基準を満たした](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)お客様の組織内のユーザーは、AEM の AI アシスタントを使用できます。[AEM の AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)を参照してください。
