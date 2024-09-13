---
title: Cloud Manager での Edge Delivery Services のサポート
description: Edge Delivery Servicesを使用してCloud Manager プロジェクトを配信する方法を説明します。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bc9aa376a402a55191e153f662262ff65df32f5e
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 6%

---

# Cloud Manager での Edge Delivery Services のサポート {#edge-delivery-services}

Edge Delivery Services ライセンスを使用してEdge Delivery Servicesサイトを作成する方法を説明します。

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->

## 概要のEdge Delivery Services {#edge-overview}

Edge Delivery Services は、web サイト上のコンテンツの柔軟なオーサリングを実現する、構成可能なサービスセットです。この機能を使用すると、次のことが可能です。

* 完璧な Lighthouse スコアで高速サイトを作成します。
* RUM （Real Use Monitoring）を通じてパフォーマンスを継続的に監視します。
* コンテンツソースを分離することでオーサリング効率を向上させます。

ユニバーサルエディターとドキュメントベースのオーサリングを使用して、AEM コンテンツ管理と WYSIWYG オーサリングの両方を使用できます。

AEM as a Cloud ServiceのCloud Managerを使用すると、プロジェクトのEdge Delivery サービスを有効にできます。

>[!TIP]
>
>Edge Delivery Servicesの詳細とAEMでの使用方法については、[Edge Delivery Servicesの概要 ](/help/edge/overview.md) を参照してください。

## Cloud ManagerのEdge Delivery Services {#edge-in-cloud-manager}

Adobe Experience Manager Sitesの一部としてライセンスをEdge Delivery Servicesしている場合は、Cloud Managerで直接Edge Delivery Servicesを使用してサイトをオンボーディングし、[ ガイド付きのセルフサービスエクスペリエンスを使用して ](/help/implementing/cloud-manager/managing-code/private-repositories.md) 運用を開始できます。

さらに、主要なワークフロー間の一貫性を確保しながら、すべてのAEM プロパティを管理できる統一されたエクスペリエンスにアクセスできます。 これには、ドメイン名の管理、SSL 証明書の管理、CDN マッピングが含まれます。

## 実稼動プログラムまたはサンドボックスプログラムへのEdge Delivery Servicesの追加

プログラムを追加または編集するには、**ビジネスオーナー** の役割のメンバーであるか、その権限が付与されている必要があります。
実稼動プログラムに適用するには、未使用のEdge Delivery Services ライセンスが必要です。

>[!NOTE]
>
>Edge Delivery Servicesライセンスがプログラムに適用またはプログラムから削除されると、変更はパイプラインを実行しなくても、直ちに有効になります。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

ユースケースに応じて、次のいずれかの操作を行います。

| ユースケース | 説明 |
| --- | --- |
| 新しい実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ 実稼動プログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) を参照してください。<br> ウィザードの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| 既存の実稼動プログラムにEdge Delivery Servicesを追加したいのですが、 | [ プログラムの編集 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) を参照してください。<br>**プログラムを編集** ダイアログボックスの「**ソリューションとアドオン**」タブで、「**Edge Delivery Services**」を選択します。 |
| 新規または既存のサンドボックスプログラムにEdge Delivery Servicesを追加したいのですが、 | [ サンドボックスプログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) を参照してください。<br> サンドボックスプログラムを作成すると、デフォルトでEdge Delivery Servicesがプログラムに追加されるので、選択する必要はありません。<br> 既存のサンドボックスプログラムは、Edge Delivery Servicesを自動的に継承します。 |

## 契約済みのお客様に対するAdobeの推奨パス {#recommended-path-eds}

契約先のお客様は、Cloud Managerを通じてEdge Delivery Servicesライセンスにアクセスして利用することで、Adobeから最大限のメリットを得ることができます。 このアプローチを使用すると、[Adobe管理による CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) を使用して、DV 証明書の設定や追加など、セルフサービス CDN 管理などの主なメリットを活用できます。 さらに、DV 証明書を作成した後、Adobeは、削除されない限り、3 か月ごとに自動的に更新します。 AdobeのEdge Delivery Services ライセンスを持っておらず、これらの利点を回避する場合は、お客様が管理する CDN のみを使用できます。 この設定は、`aem.live` プラットフォーム上に存在する必要があります。

AEM as a Cloud Service Sites Edge Delivery Servicesライセンスを契約している場合は、Cloud Managerにログインして、以下を実行できるようにします。

* 選択したプログラムでライセンスを使用します。
* [API ファースト ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) の利点を活用して、CRUD （作成、読み取り、更新、削除）操作を実行します。
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* SLA レポートへのアクセス （*近日公開*） <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Adobeのサポートを得る。 Adobeから適切に認識され、サポートを受けるために、Edge Delivery ServicesサイトがCloud Managerの実稼動プログラムを通じて登録されていることを確認します。

## Edge Delivery サイトを追加 {#eds-add-site}

実稼動プログラムにEdge Delivery Servicesを追加すると、そのプログラムにEdge Delivery Servicesライセンスが適用されます。

概要ページに、**Edge Delivery** というクリック可能なタブが表示されます。 タブをクリックすると、追加した各Edge Delivery サイトを一覧表示するテーブルが表示されます。 左側のナビゲーションパネルの **サービス** グループの下に、**Edge Delivery Sites** という名前のメニューオプションがあります。

![ 左側のナビゲーションパネルに「Edge Delivery Sites」を表示し、「Edge Delivery配信」タブの右側にある「Publish」タブを表示する概要ページ ](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Edge Delivery サイトを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されているプログラムを選択します。このプログラムに、Edge Delivery サイトを追加します。
1. 次のいずれかの操作を行います。
   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 次に、ページの右下隅付近にある「**Edge Delivery サイトを追加**」をクリックします。

     ![ 「Edge Delivery」タブからEdge Delivery サイトを追加する ](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     上の画像に示すように、**Edge Delivery to-do リスト** は、Edge Deliveryの使用を開始する際に役立つオプションのオンボーディングチェックリストガイドです。 [Edge Delivery To Do リストについて ](#ed-todo-list) を参照してください。

   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。 ページの右上隅付近にある「**サイトを追加**」をクリックします。

     ![ 「Edge Delivery サイト」ボタンから「Edge Delivery サイトを追加」 ](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. **Edge Delivery サイトを追加** ダイアログボックスで、次の操作を行います。

   | テキストフィールド | 実行内容 |
   | --- | --- |
   | サイト名 | 追加するEdge Delivery サイトの名前を入力します。 名前は、Cloud Manager内のサイトの一意の ID として機能します。 |
   | リポジトリ URL | このフィールドは、web サイトのコードが保存されている Git リポジトリーを参照します。<br>Edge Delivery サイトに必要なファイルおよびリソース（HTML、CSS、JavaScript、その他の web アセットなど）を含む Git リポジトリの URL を入力します。 この配置により、Cloud Managerはデプロイメントプロセス中にそのリポジトリからコードを取り込むことができます。 |
   | サイトの説明 (オプション) | 追加するEdge Delivery サイトの簡単な説明を入力します。<br> この説明は、サイトを識別して区別するのに役立ち、追加した他のサイトの管理と認識を容易にします。 サイトの目的、コンテンツ、またはその機能や範囲を明確にするのに役立つその他の関連情報に関する詳細を含めることをお勧めします。 |

1. ダイアログボックスの右下隅にある「**追加**」をクリックします。

1. **リポジトリの所有権を確認** ダイアログボックスで、次の各操作を行います。

   | 手順 | 説明 |
   | --- | --- |
   | 1 | 「**リポジトリ URL**」フィールドにリストされている Git リポジトリの `main` ブランチへのロケーションパスを持つファイルを追加します。 必要に応じて、コピーアイコンをクリックして、パスをクリップボードにコピーします。<br> 場所のパスは <br>`well-known/adobe/cloudmanager-challenge.txt` です。場所のパスの先頭にピリオドを追加する <br><br>*しないでください* は次の場所にあります：<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | 生成されたコードを手順 1 で作成したファイルに追加します。 必要に応じて、「コピー」アイコンをクリックして、コードをクリップボードにコピーします。 |
   | 3 | Git リポジトリでプルリクエストを作成し、それを結合してコードをコミットします。 |

1. **確認** をクリックします。 リポジトリが検証されると、Edge配信サイト テーブル内のステータスが緑色の円に変わり、その内側に白いチェックマークが付きます。

## Edge Delivery To Do リストについて {#ed-todo-list}

**Edge Delivery To-Do リスト** はオンボーディングタスクのチェックリストで、オンボーディング、Edge Delivery サイトの管理を [ 運用開始 ](/help/journey-onboarding/go-live-checklist.md) までガイドすることを目的としています。

|  | タスク | 説明 |
| --- | --- | --- |
| 1 | 製品コラボレーションチャネルに参加 | **リクエストを今すぐ送信** をクリックすると、会社のチャネルを作成するためのリクエストがAdobeに送信されます。 チャネルが既に存在する場合は、会社のチャネルに転送されます。 |
| 2 | 前提条件を完了 | **入門チュートリアルを表示** をクリックすると、[ 入門 – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) に移動します。 |
| 3 | Edge Delivery サイトを追加 | [Edge Delivery サイトの追加 ](#eds-add-site) を参照してください。 |
| 4 | ドメインを追加 | [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。 |
| 5 | SSL 証明書を追加 | [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。 |
| 6 | Edge Delivery サイトの CDN の設定 | [CDN 設定の追加 ](#add-cdn) を参照してください。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Edge Delivery サイトに CDN 設定を追加します。 {#add-cdn}

[CDN 設定の追加 ](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) を参照してください。

## Edge Delivery サイトを削除する {#eds-site-delete}

>[!IMPORTANT]
>
>Edge Delivery Servicesサイトを削除すると、関連する CDN 設定もすべて削除されます。 このアクションにより、カスタムドメインとサイトの間の接続が切断されます。 詳しくは、CDN 設定を参照してください。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Edge Delivery サイトを削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されているプログラムを選択します。このプログラムに、Edge Delivery サイトを追加します。
1. 次のいずれかの操作を行います。
   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 Edge Deliveryのサイトテーブルで、サイトを削除する行の最後にある省略記号をクリックします。 **削除** をクリックし、もう一度 **削除** をクリックしてサイトの削除を確認します。

     ![ 「Edge Delivery」タブからEdge Delivery サイトを追加する ](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。 Edge Deliveryのサイトテーブルで、サイトを削除する行の最後にある省略記号をクリックします。 **削除** をクリックし、もう一度 **削除** をクリックしてサイトの削除を確認します。


     ![ 「Edge Delivery サイト」ボタンから「Edge Delivery サイトを追加」 ](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)


<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
