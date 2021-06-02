---
title: Cloud Managerについて説明します
description: このページでは、Cloud Manager、Cloud Managerのプログラム、環境について説明します。
source-git-commit: 185a933e12ad81689168ad88574019ed219db06d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 20%

---


# Cloud Manager の概要 {#intro-cloud-manager}

Cloud Managerは、AEMのCloud Serviceとしての不可欠なコンポーネントで、チームの単一のエントリポイントとして機能します。

エンタープライズ開発の設定をおこなうお客様をサポートするために、AEM as aCloud ServiceはCloud Managerとその専用に構築されたCI/CDパイプラインに完全に統合され、優れたエクスペリエンスを提供するための徹底的なテストと最高のコード品質を保証します。

お客様がAEM as aCloud Serviceをすぐに使い始められるように、Cloud Managerは、クラウドのリソースや環境を作成する機能など、セルフサービス方式で開始するために必要なすべての機能を備えています。 この方法で、AEM開発者はCloud Managerを使用してGitリポジトリにアクセスできます。 開発チームは、Cloud Managerを使用して、セルフサービス方式で頻繁に変更をコミットするよう取り組むことができます。

システム管理者は、クラウドリソースおよび開発者を作成する個人を含むCloud Managerチームの設定を担当します。 エンタープライズチーム開発設定でのCloud Managerのサポート方法については、 AEM as aCloud Service向けの[エンタープライズチーム開発設定](/help/implementing/cloud-manager/enterprise-team-dev-setup.md)を参照してください。

## Cloud Manager プログラム {#cloud-manager-programs}

Cloud Managerプログラムは、通常、購入したサービスレベル契約(SLA)に対応する、ビジネスイニシアチブの論理的なセットをサポートするCloud Manager環境のセットを表します。 例えば、あるプログラムは、グローバルなパブリックWebサイトをサポートするAEMリソースを表し、別のプログラムは、内部のCentral DAMを表します。 Cloud Managerプログラムの使用について詳しくは、この[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)をご覧ください。

ユーザーは、**ｻサンドボックス**&#x200B;または&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* *実稼動プログラム*&#x200B;が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。詳しくは、[実稼動プログラムの概要](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。

* *サンドボックスプログラム*は、通常、トレーニング、デモの実行、イネーブルメント、POC、ドキュメントの実行の目的で作成されます。ライブトラフィックを運ぶことを目的としたものではなく、実稼動プログラムにはない制限が課されます。Sites と Assets が含まれ、サンプルコード、開発環境、非実稼動パイプラインを含む Git ブランチが自動生成されて配信されます。
詳しくは、[サンドボックスプログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。

## Cloud Manager環境{#cloud-manager-environments}

クラウド環境は、Cloud Managerを使用して作成、アクセスおよび表示されます。 実稼動環境、ステージ環境、または開発環境を指定できます。 環境が異なれば、サポートする目的も異なり、様々なCI/CDパイプラインを使用して関与できます。 環境は、次のようなサービスで構成されます。

* [AEMオーサーサービス](#author-services)
* [AEMパブリッシュサービス](#publish-services)
* [Dispatcherサービス](#dispatcher-services)

   >[!NOTE]
   > 使用可能な環境の詳細については、ビデオ[Using Using Cloud Manager Environments](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager)を参照してください。 さらに、[環境の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)を参照して、ユーザーが作成できる環境のタイプと、ユーザーが環境を作成する方法について詳しく知ってください。

### AEMオーサーサービス{#author-services}

AEMオーサーサービスは、サイトコンテンツとデジタルアセットが作成、管理、更新される環境に含まれています。 通常、オーサーサービスにアクセスできるのは内部ユーザーのみで、ログイン画面の後ろにあります。 オーサリングサービスは、オーサリング環境とプレビュー環境の両方として設計されています。

### AEMパブリッシュサービス{#publish-services}

AEMパブリッシュサービスは、Webサイトなどのエンドユーザーエクスペリエンスをホストする環境に含まれます。 これは、サイト訪問者が表示し、操作するサービスです。 通常、パブリッシュサービスは公開されています。

### AEM Dispatcherサービス{#dispatcher-services}

Dispatcherは、AEMパブリッシュサービスの前に配置されるセキュリティとパフォーマンスのレイヤーを提供する`Apache HTTP Web server`モジュールです。