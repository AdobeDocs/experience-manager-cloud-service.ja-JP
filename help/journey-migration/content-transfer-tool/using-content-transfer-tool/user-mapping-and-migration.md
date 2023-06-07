---
title: ユーザーマッピングとプリンシパルの移行
description: ユーザーマッピングとプリンシパル移行の概要
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: caa04391077d594a828a42a1a5a6a03daa107168
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 24%

---

# ユーザーマッピングとプリンシパルの移行 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピング"
>abstract="コンテンツ転送ツールは、ユーザーとグループを既存の Adobe Experience Manager（AEM）システムから AEM as a Cloud Service に移動する際に役に立ちます。既存のユーザーは、Cloud Service オーサーインスタンス上で重複しないように、IMS ID にマッピングする必要があります。"

>[!NOTE]
>以前のバージョンのユーザーマッピングツールについては、[レガシードキュメント](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager(AEM)as a Cloud Serviceへの移行プロセスの一環として、ユーザーとグループを既存のAEMシステムからAEM as a Cloud Serviceに移行する必要があります。 このタスクはコンテンツ転送ツールで実行されます。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。このプロセスでは、 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) ユーザーとユーザーグループを管理するための ユーザープロファイル情報は、すべてのAdobeクラウドアプリケーションに対してシングルサインオンを提供するAdobeIdentity Management System(IMS) で一元化されます。 詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management) を参照してください。この変更により、Cloud Serviceオーサーインスタンスでの重複ユーザーを避けるために、既存のユーザーをそれぞれの IMS ID にマッピングする必要があります。 従来の AEM のグループは IMS のグループとは基本的に異なるので、グループはマッピングされませんが、移行が完了した後で 2 つのグループセットを調整する必要があります。

## ユーザー移行の詳細 {#user-migration-detail}

コンテンツ転送ツールおよび Cloud Acceleration Manager は、移行されるコンテンツに関連付けられているすべてのユーザーをクラウドシステムに移行します。

## ユーザーマッピングの詳細 {#user-mapping-detail}

AEMユーザーは、同じ E メールアドレスを持つ対応するAdobe IMSユーザーにマッピングできます。  このマッピングは CTT で自動的におこなえ、実行するかどうかは抽出を開始する前に切り替えで制御できます。 抽出を開始する際に、ユーザーが切り替えのデフォルト設定を上書きできます。

* ソースシステムがオーサーインスタンスの場合、デフォルトでは、マッピングを行う選択はです _オン_&#x200B;を選択します。これは、推奨されるプロセスなのでです。
* ソースシステムがパブリッシュインスタンスの場合、デフォルトでは、マッピングを行う選択はです _オフ_&#x200B;ユーザーは通常、パブリッシュインスタンスで移行されたり使用されたりしないので、

## ユーザーをマッピングおよび移行する際の重要な考慮事項 {#important-considerations}


### 例外的な状況 {#exceptional-cases}

次の特定のケースがログに記録されます。

1. ユーザーのメールアドレスが `profile/email` 彼らの分野 *jcr* ノード、問題のユーザーまたはグループは移行される可能性がありますが、マッピングされません。 このシナリオでは、電子メールアドレスがログイン時のユーザー名として使用されている場合でも同様です。

1. ユーザーが現在無効になっている場合は、無効になっていない場合と同じように扱われます。通常どおりマッピングおよび移行され、クラウドインスタンス上では無効のままになります。

1. ターゲットのAEM Cloud Serviceインスタンス上に、ソースのAEMインスタンス上のユーザーと同じユーザー名 (rep:principalName) を持つユーザーが存在する場合、問題のユーザーは移行されません。

1. ユーザーマッピングを通じてマッピングされずにユーザーが移行された場合、ターゲットクラウドシステムでは、その IMS ID を使用してログオンできません。 また、電子メールアドレスが IMS へのログインに使用された電子メールアドレスと一致しない場合、Target Cloud システムでは、IMS ID を使用してログオンすることもできません。 従来のAEM方式を使用してログオンできる場合がありますが、通常、この方法は望ましいものや期待されるものではありません。


## その他の考慮事項 {#additional-considerations}

* 設定が **取り込み前にクラウドインスタンス上の既存のコンテンツを消去** が設定されると、既にCloud Serviceインスタンスで転送されたユーザーは、既存のリポジトリ全体と共に削除されます。 また、コンテンツの取り込み先となる新しいリポジトリが作成されます。 このプロセスは、ターゲットCloud Serviceインスタンスに対する権限を含むすべての設定もリセットし、に追加された管理者ユーザーに対して true になります。 **管理者** グループ化します。 管理者ユーザーは、 **管理者** グループを使用して、CTT のアクセストークンを取得します。
* コンテンツ追加を行う際に、前回の転送以降に変更が加えられていないためにコンテンツが転送されなかった場合、そのコンテンツに関連付けられたユーザーやグループも転送されません。 このルールは、ユーザーとグループがその間に変更を加えた場合でも当てはまります。 これは、ユーザーとグループが、関連付けられているコンテンツと共に移行されるからです。
* ターゲットのAEM Cloud Serviceインスタンスに、ユーザー名が異なり、ソースのAEMインスタンスのユーザーの 1 人と同じ E メールアドレスを持つユーザーが存在し、「ユーザーマッピング」が有効な場合、ログにエラーメッセージが記録されます。 また、ターゲットシステムでは、指定された E メールアドレスを持つ 1 人のユーザーのみが許可されるので、ソースAEMユーザーは転送されません。

## 最終概要とレポート {#final-report}

抽出と取り込みが正常に完了すると、主要な移行の詳細を示すレポートが生成されます。 詳しくは、 [プリンシパルの移行を検証する方法](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) を参照してください。
