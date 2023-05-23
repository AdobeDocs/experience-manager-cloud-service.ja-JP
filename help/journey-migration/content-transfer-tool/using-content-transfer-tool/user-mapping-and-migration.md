---
title: ユーザーマッピングとプリンシパルの移行
description: ユーザーマッピングとプリンシパル移行の概要
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 25bfcd521e9bbc54bff3b87d17cdeb0f99a68511
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 96%

---

# ユーザーマッピングとプリンシパルの移行 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピング"
>abstract="コンテンツ転送ツールは、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移動する際に役に立ちます。既存のユーザーは、Cloud Service オーサーインスタンス上で重複しないように、IMS ID にマッピングする必要があります。"

>[!NOTE]
>以前のバージョンのユーザーマッピングツールについては、[レガシードキュメント](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。これには、コンテンツ転送ツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーの重複を避けるために、既存のユーザーを IMS ID にマッピングする必要があります。従来の AEM のグループは IMS のグループとは基本的に異なるので、グループはマッピングされませんが、移行が完了した後で 2 つのグループセットを調整する必要があります。

## ユーザーマッピングと移行の詳細 {#user-mapping-detail}

コンテンツ転送ツールおよび Cloud Acceleration Manager では、移行されるコンテンツに関連付けられているすべてのユーザーが移行されます。このマッピングは自動的に行われ、実行するかどうかは、抽出が開始される前に切り替えで制御できます。抽出を開始する際に、ユーザーが切り替えのデフォルト設定を上書きできます。

* ソースシステムがオーサーインスタンスの場合、デフォルトでは、マッピングを行う選択は&#x200B;_オン_&#x200B;になっています。これは、推奨されるプロセスです。
* ソースシステムがパブリッシュインスタンスの場合、デフォルトでは、マッピングを行う選択は&#x200B;_オフ_&#x200B;になっています。ユーザーは通常、パブリッシュインスタンスで移行されたり使用されたりしないためです。

## ユーザーをマッピングおよび移行する際の重要な考慮事項 {#important-considerations}


### 例外的な状況 {#exceptional-cases}

次の特定のケースがログに記録されます。

1. ユーザーの *jcr* ノードの `profile/email` フィールドにメールアドレスがない場合、該当するユーザーまたはグループは移行されますが、マッピングされません。これは、メールアドレスがログイン時にユーザー名として使用されている場合でも同じです。

1. ユーザーが現在無効になっている場合は、無効になっていない場合と同じように扱われます。通常どおりマッピングおよび移行され、クラウドインスタンス上では無効のままになります。

1. ソース AEM インスタンスのいずれかのユーザーと同じユーザー名（rep:principalName）のユーザーがターゲット AEM Cloud Service インスタンスに存在する場合、該当するユーザーまたはグループは移行されません。

1. ユーザーが最初にユーザーマッピング経由で移行されずに移行された場合、またはメールアドレスが IMS へのログインに使用されるメールアドレスと一致しない場合、ターゲットクラウドシステムでは、IMS ID を使用してログインできません。従来の AEM 方式でログインできる場合もありますが、通常はこの方法が望ましいものや期待されるものではないことに注意してください。


## その他の考慮事項 {#additional-considerations}

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが設定されている場合は、Cloud Service インスタンス上の転送済みユーザーと既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。また、これにより、ターゲット Cloud Service インスタンスに対する権限を含むすべての設定もリセットされます。これは、**administrators** グループに追加された管理者ユーザーに対しても当てはまります。CTT のアクセストークンを取得するには、管理者ユーザーを&#x200B;**管理者**&#x200B;グループに再度追加する必要があります。
* コンテンツ追加が実行されるときに、前回の転送以降変更がないのでコンテンツが転送されない場合は、そのコンテンツに関連付けられたユーザーやグループは、その間にユーザーやグループが変更されたとしても転送されません。これは、ユーザーやグループの移行が、ユーザーやグループが関連付けられているコンテンツと共に行われるからです。
* ユーザー名は異なるものの、ソース AEM インスタンスのいずれかのユーザーと同じメールアドレスを持つユーザーが、ターゲット AEM Cloud Service インスタンスに存在し、かつ、ユーザーマッピングが有効な場合、エラーメッセージがログに書き込まれ、ソース AEM ユーザーは転送されません。ターゲットシステムでは、任意のメールアドレスは 1 人のユーザーのみに許可されるからです。

## 最終概要とレポート {#final-report}

抽出と取り込みが正常に完了すると、主要な移行の詳細を示すレポートが生成されます。 詳しくは、 [プリンシパルの移行を検証する方法](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) を参照してください。
