---
title: グループの移行
description: AEM as a Cloud Service でのグループの移行についての概要です。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: bb041cf13d5e82fc4135f0849b03eeeed9a5d009
workflow-type: ht
source-wordcount: '1476'
ht-degree: 100%

---


# グループの移行 {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="グループの移行"
>abstract="コンテンツ転送ツールは、グループを既存の Adobe Experience Manager（AEM）システムから AEM as a Cloud Service にコピーする際に役に立ちます。"

>[!NOTE]
>以前のバージョンのユーザーマッピングツールについては、[レガシードキュメント](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。

## はじめに {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="ユーザーが移行されない"
>abstract="コンテンツ転送ツールでは、ユーザーは移行されなくなりました。ユーザーは Admin Console で管理する必要があります。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console ドキュメント"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

Adobe Experience Manager（AEM）as a Cloud Service への移行プロセスの一環として、グループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。このタスクは、コンテンツ転送ツールによって実行されます。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。このプロセスでは、ユーザーとユーザーグループを管理するために [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンを利用できます。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、IMS 経由で AEM に最初にログインしたときにユーザーが自動的に AEM に作成されます。そのため、CTT では、ユーザーはクラウドシステムに移行されません。IMS ユーザーは、IMS グループに配置する必要があります。IMS グループは、移行対象のグループや、移行中の AEM コンテンツにアクセスする権限が付与された AEM グループに配置される新しいグループにすることができます。この方法では、クラウドシステム上のユーザーは、ソース AEM システムと同じアクセス権を使用することになります。

## グループの移行の詳細 {#group-migration-detail}

コンテンツ転送ツールおよび Cloud Acceleration Manager では、移行されるコンテンツに関連付けられているすべてのグループがクラウドシステムに移行されます。コンテンツ転送ツールは、抽出プロセス中にソース AEM システムからすべてのグループをコピーすることで、これを行います。すると、CAM 取り込みは、特定のグループのみを選択して移行します。

* 移行されたコンテンツの ACL または CUG ポリシーにグループが含まれている場合、以下に示す例外を除いて、そのグループは移行されます。
* ターゲットのクラウドシステムに既にビルトインされているグループが多数ありますが、これらは移行されません。
   * 一部のビルトイングループには、ビルトイン&#x200B;_ではない_&#x200B;メンバーグループが含まれる場合があります。このようなメンバーグループ（直接のメンバーや、メンバーのメンバーなど）は、移行されたコンテンツの ACL または CUG ポリシーで参照されている場合に移行され、これらのグループのメンバーであるユーザーが（直接または間接的に）移行されたコンテンツへのアクセスを維持できるようになります。
* ACL または CUG ポリシーに見つからないグループ、宛先システムに既に存在するグループ、およびターゲットシステムに一意性制約のあるデータが既に存在するグループなどのその他のグループは移行されません。

あるグループについてログに記録／報告されるパスは、そのグループの移行をトリガーした最初のパスのみです。また、そのグループが他のコンテンツパス上に存在する場合もあります。

移行されるほとんどのグループは、IMS で管理されるように設定されています。つまり、IMS 内にある同じ名前のグループは AEM 内のグループにリンクされ、IMS グループ内のすべての IMS ユーザーは AEM ユーザーとなり、AEM 内のグループのメンバーになります。これにより、これらのユーザーはグループの ACL または CUG ポリシーに従って、コンテンツにアクセスできるようになります。

なお、移行されたグループは、AEM の「ローカルグループ」とは見なされなくなり、AEM では IMS 対応のグループですが、IMS にまだ存在していない場合もあります。AEMと IMS の間で同期できるように、IMS で別個に再作成する必要があります。グループは、IMS で Admin Console などの方法を使用して、個別または一括で作成できます。Admin Console でグループを個別または一括で作成する方法について詳しくは、[ユーザーグループの管理](https://helpx.adobe.com/jp/enterprise/using/user-groups.html)を参照してください。

この IMS 設定の例外は、アセットコレクションによって作成されたグループです。AEM でコレクションを作成すると、そのコレクションにアクセスするためのグループが作成されます。このようなグループはクラウドシステムに移行されますが、IMS によって管理されるようには設定されません。IMS ユーザーをこれらのグループに追加するには、アセット UI のグループプロパティページで、個別に、または別の IMS グループの一部としてまとめて追加する必要があります。


## グループの移行のオプトアウト {#group-migration-option}

CTT バージョン 3.0.20 以降には、グループの移行を無効にするオプションが含まれています。これは、OSGi コンソールで次のように設定されます。

* OSGi 設定 `(http://<server>/system/console/configMgr)` を開きます
* 「**コンテンツ転送ツール抽出サービス設定**」という設定をクリックします
* 「**移行にグループを含める**」をオフにして、グループの移行を無効にします
* 「**保存**」をクリックして、設定が保存され、サーバー上でアクティブになっていることを確認します

この設定を無効にすると、グループは移行されず、プリンシパル移行レポートやユーザーレポートは作成されません。

## ユーザーレポート {#user-report}

移行中、ユーザーは移行されませんが、何らかの方法で取得されない限り、ソースシステム上のユーザーグループの関係は失われます。ユーザーレポートは、この情報の一部をテキスト形式でユーザーレポートに取り込みます。ここでは、各ユーザーがそのメンバーであるグループのリストとともに（1 行につき 1 つ）報告されます（ただし、移行されていないグループはこのリストには含まれません）。ただし、グループのリストが空の場合は、ユーザーは表示されません。各ユーザーとともに報告されるグループは、ユーザーがソースシステムで直接または間接的にメンバーであるグループです。ソースシステムのグループは、ターゲットシステムではネストされないが、ソースシステムではネストされる場合があるので、このグループのリストは IMS で新しくフラット化されたグループ構造をサポートします。

ワイプとその後のワイプなしの取り込みの場合、ユーザーのリスト内のグループには、いずれかのフェーズで移行されたグループが含まれます。

レポートには、各ユーザーのグループのほかに、ユーザーのメモを追加できるフィールドがあります（メモの意味に関する詳細な説明もレポートにあります）。メモの例を次に示します。

* ACL 内で直接参照されるユーザーの「メモ」セクションには&#x200B;*メモ - A* が表示されます。これは、推奨されるユースケースやベストプラクティスではないからです。
* 組み込みのグループの直接メンバーであるユーザーの「メモ」セクションには&#x200B;*メモ - B* が表示されます。これもまた、推奨されるユースケースやベストプラクティスではありません。

これらのケースは同時に発生し、また以前のケースと同時に発生することもあります。

ユーザーレポートは、プリンシパル移行レポートの最後（その一部）に追加されます（以下の[最終的な概要とレポート](#final-summary-and-report)を参照）。このレポートの情報（各ユーザーに対してレポートされたグループを含む）を使用すると、Admin Console で IMS に多数のユーザーを一括して作成するために使用できる一括ユーザーアップロードファイルを作成できます。また、既存の IMS ユーザーも一括編集できます。

Admin Console を使用してユーザーを一括で作成または編集する方法について詳しくは、[複数のユーザーの管理 | 一括 CSV アップロード](https://helpx.adobe.com/jp/enterprise/using/bulk-upload-users.html)を参照してください。

## その他の考慮事項 {#additional-considerations}

* 「**取り込み前にクラウドインスタンス上の既存のコンテンツを消去**」が設定されている場合は、以前に Cloud Service インスタンスに転送されたグループと既存のリポジトリ全体が削除され、コンテンツの取り込み先となる新しいリポジトリが作成されます。このプロセスは、ターゲットの Cloud Service インスタンスの権限を含むすべての設定もリセットします。これは、**管理者**&#x200B;グループに追加されたすべてのユーザーに当てはまります。CTT/CAM 取り込みのアクセストークンを取得するには、管理者ユーザーを&#x200B;**管理者**&#x200B;グループに再度追加する必要があります。
* ワイプなしの取り込みを実行する場合（「**既存のコンテンツを消去**」が設定されていない場合）、前回の転送以降変更がないのでコンテンツが転送されない場合は、そのコンテンツに関連付けられたグループも転送されません。このルールは、グループがソースシステム上で変更された場合でも当てはまります。これは、グループの移行が、ユーザーやグループが関連付けられているコンテンツと共にのみ行われるからです。このため、この場合、ソースシステム上のグループのメンバーであるグループは、移行中の別のグループの一部であるか、移行中の別のコンテンツの ACL に含まれていない限り、移行されません。これらのグループを後で移行する場合は、パッケージの使用、ターゲットからのグループの削除と関連コンテンツの再移行、ワイプ取り込みを使用した再移行を行うことを検討してください。
* ワイプなし取り込み中に、ソース AEM インスタンスとターゲット AEM Cloud Service インスタンスの両方に、同じ一意性制約データ（rep:principalName、rep:authorizableId、jcr:uuid または rep:externalId）のグループが存在する場合、問題のグループは移行&#x200B;_されず_、クラウドシステム上の既存のグループは変更されません。これは、プリンシパル移行レポートに記録されます。
* クローズドユーザーグループ（CUG）ポリシーで使用されるグループに関するその他の考慮事項について詳しくは、[クローズドユーザーグループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)を参照してください。

## 最終概要とレポート

抽出と取り込みが正常に完了すると、グループ移行の詳細を示すレポートが生成されます。詳しくは、[グループの移行を検証する方法](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration)を参照してください。
