---
title: Cloud Manager の Edge Delivery Services の概要
description: Edge Delivery Services を使用して Cloud Manager プロジェクトを配信する方法について説明します。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '823'
ht-degree: 100%

---


# Cloud Manager の Edge Delivery Services の概要 {#edge-delivery-services}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、合成可能なサービスセットです。この機能では、次の操作を実行できます。

* 完璧な Lighthouse スコアで高速なサイトを作成する。
* 運用テレメトリを通じて、パフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させる。

ユニバーサルエディターを使用した AEM コンテンツ管理および WYSIWYG オーサリングと、ドキュメントベースのオーサリングの両方を使用できます。

AEM as a Cloud Service の Cloud Manager を使用すると、プロジェクトで Edge Delivery Service を有効にできます。

>[!TIP]
>
>Edge Delivery Services の概要と、AEM で使用する方法について詳しくは、[Edge Delivery Services の概要](/help/edge/overview.md)を参照してください。

## Cloud Manager の Edge Delivery Services について {#edge-in-cloud-manager}

Adobe Experience Manager Sites の一部として Edge Delivery Services のライセンスを取得している場合は、Cloud Manager で Edge Delivery Services を使用してサイトを直接オンボードし、[ガイド付きのセルフサービスエクスペリエンスを使用](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)して運用開始できます。

さらに、主要なワークフロー全体の一貫性を確保しながら、すべての AEM プロパティを管理するための統合されたエクスペリエンスにアクセスできます。これらのワークフローには、ドメイン名管理、SSL 証明書管理、CDN マッピングが含まれます。

## アドビが推奨する Edge Delivery Services のパスを使用するメリット {#recommended-path-eds}

Cloud Manager を通じて Edge Delivery Services ライセンスにアクセスして使用することで、アドビのメリットを最大限に活用できます。これにより、いくつかの主なメリットを活用できます。

* [選択したプログラムのライセンスを消費](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)、[他のプログラムを更新](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)、またはその両方を実行します。
* CRUD（作成、読み取り、更新、削除）操作を実行するための [API ファースト](https://developer.adobe.com/experience-cloud/experience-manager-apis/)のメリットを活用します。
* [SLA レポートへのアクセス](/help/implementing/cloud-manager/sla-reporting.md)（*近日公開予定*）
* 登録済みの実稼動プログラムに関する[アドビサポートにアクセス](/help/edge/overview.md#support-ticket)できます。

Edge Delivery Services（EDS）ライセンスをお持ちの場合、Edge Delivery サイトで[アドビが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) を使用し、セルフサービス CDN 管理や、DV 証明書の 3 か月ごとの自動更新（削除された場合を除く）機能を利用できます。

または、自分の CDN （アドビが管理する CDN 以外の CDN）を使用する場合は、Edge Delivery Services　のライセンスに関係なく、CDN を `aem.live` プラットフォームで設定する必要があります。[BYO CDN 設定](https://www.aem.live/docs/byo-cdn-setup)を参照してください。


## 実稼動プログラムまたはサンドボックスプログラムへの Edge Delivery Services の追加について

Edge Delivery Services は、プロジェクトの開始方法やサイトを作成するタイミングに応じて、様々な方法で追加できます。

| ユースケース | 説明 |
| --- | --- |
| 新しい実稼動プログラムに Edge Delivery Services を追加したい。 | [実稼動プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)を参照してください。<br>ウィザードの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| 既存の実稼動プログラムに Edge Delivery Services を追加したい。 | [プログラムの編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)を参照してください。<br>**プログラムを編集**&#x200B;ダイアログボックスの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| Cloud Manager に Edge Delivery サイトを追加したい | [Edge Delivery サイトの追加](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)を参照してください。 |
| 今すぐ Edge Delivery サイトを作成したい | [ボタンをクリックするだけで Cloud Manager で Edge Delivery サイトをすばやく作成](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)を参照してください。 |
| 新規または既存のサンドボックスプログラムに Edge Delivery Services を追加したい。 | [サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)を参照してください。<br>サンドボックスプログラムを作成すると、Edge Delivery Services がデフォルトでプログラムに追加されるので、これを選択する必要はありません。<br>Edge Delivery が一般提供される前の既存のサンドボックスプログラムは、Edge Delivery Services を自動的に継承します。 |

>[!NOTE]
>
>* プログラムを追加または編集するには、**ビジネス所有者**&#x200B;の役割のメンバーであるか、これらの操作を行う権限が付与されている必要があります。
>* 実稼動プログラムに適用する前に、組織に未使用の Edge Delivery Services ライセンスが必要です。
>* Edge Delivery Services ライセンスがプログラムに適用または削除されると、パイプラインを実行しなくても、変更がすぐに有効になります。


## Cloud Manager の Edge Delivery の TODO リストについて {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Manager の **Edge Delivery の TODO リスト**&#x200B;は、オンボーディング、Edge Delivery サイトの管理から[運用開始](/help/journey-onboarding/go-live-checklist.md)までガイドすることを目的としたオンボーディングタスクチェックリストです。

![Cloud Manager の Edge Delivery サイトの TODO リスト。](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | タスク | 説明 |
| --- | --- | --- |
| 1 | 製品コラボレーションチャネルに参加 | 「**今すぐリクエストを送信**」をクリックすると、会社のチャネルを作成するためのリクエストがアドビに送信されます。チャネルが既に存在する場合は、会社のチャネルに転送されます。 |
| 2 | 前提条件を完了 | [基本を学ぶチュートリアルを表示](https://www.aem.live/developer/tutorial)を参照してください。 |
| 3 | Edge Delivery サイトを追加または<br>今すぐサイトを作成 | [Edge Delivery サイトの追加](#eds-add-site)を参照してください。<br>[Cloud Manager での Edge Delivery サイトの作成](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)を参照してください。 |
| 4 | 外部 Git リポジトリを使用するために Edge Delivery サイトを設定 | [外部 Git リポジトリを使用するための Edge Delivery サイトの設定](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md)を参照してください。 |
| 5 | ドメインを追加 | [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。 |
| 6 | SSL 証明書を追加 | [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。 |
| 7 | Edge Delivery サイトの CDN を設定 | [ドメインマッピングの追加](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)を参照してください。 |
| 8 | プッシュ検証を設定 | [Edge Delivery サイト用のプッシュ検証の設定](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md)を参照してください。 |
| 9 | 運用開始 | [運用開始チェックリスト](https://www.aem.live/docs/go-live-checklist)を参照してください。 |

>[!VIDEO](https://video.tv.adobe.com/v/3441562?learn=on&captions=jpn)

## サポートチケットのログ {#eds-support-ticket}

{{support-ticket}}



