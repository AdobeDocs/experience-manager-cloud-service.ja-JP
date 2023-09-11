---
title: ユーザーマッピングとプリンシパルの移行
description: AEM as a Cloud Serviceでのユーザーマッピングとプリンシパル移行の概要です。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 2fdfb65543fa2942e809aa5d379f4000e40bd517
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 16%

---

# ユーザーマッピングとプリンシパルの移行 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピング"
>abstract="コンテンツ転送ツールは、ユーザーとグループを既存の Adobe Experience Manager（AEM）システムから AEM as a Cloud Service に移動する際に役に立ちます。既存のユーザーは、Cloud Service オーサーインスタンス上で重複しないように、IMS ID にマッピングする必要があります。"

>[!NOTE]
>以前のバージョンのユーザーマッピングツールについては、[レガシードキュメント](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager(AEM)as a Cloud Serviceへの移行プロセスの一環として、ユーザーとグループ（または「プリンシパル」）を既存のAEMシステムからAEMas a Cloud Serviceに移行する必要があります。 このタスクはコンテンツ転送ツールで実行されます。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。このプロセスでは、 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) ユーザーとユーザーグループを管理するための ユーザープロファイル情報は、すべてのAdobeクラウドアプリケーションに対してシングルサインオンを提供するAdobeIdentity Management System(IMS) で一元化されます。 詳しくは、 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). この変更により、Cloud Serviceオーサーインスタンスでの重複ユーザーの作成を避けるために、既存のユーザーをその IMS ID にマッピングする必要があります。 従来の AEM のグループは IMS のグループとは基本的に異なるので、グループはマッピングされませんが、移行が完了した後で 2 つのグループセットを調整する必要があります。

## プリンシパル移行の詳細 {#principal-migration-detail}

コンテンツ転送ツールおよび Cloud Acceleration Manager は、移行されるコンテンツに関連付けられたプリンシパルをクラウドシステムに移行します。  コンテンツ転送ツールは、抽出プロセス中にソースAEMシステムからすべてのプリンシパルをコピーすることで、これをおこないます。  次に、CAM 取り込みは、取り込まれるコンテンツに関連付けられたプリンシパルのみを選択して移行します。

## ユーザーマッピングの詳細 {#user-mapping-detail}

AEMユーザーは、同じ E メールアドレスを持つ対応するAdobe IMSユーザーにマッピングできます。  このマッピングは、CTT で（抽出ステップ中に）自動的におこなうことができ、抽出が開始される前に切り替えで制御できます。 抽出を開始する際に、ユーザーが切り替えのデフォルト設定を上書きできます。

* ソースシステムがオーサーインスタンスの場合、デフォルトでは、マッピングを行う選択はです。 _オン_&#x200B;を選択します。これは、推奨されるプロセスなのでです。
* ソースシステムがパブリッシュインスタンスの場合、デフォルトでは、マッピングを行う選択はです。 _オフ_&#x200B;ユーザーは通常、パブリッシュインスタンスで移行または使用されないので、または使用する場合は、通常、異なる認証システム（IMS ではなく）が使用されます。

抽出時にユーザーがマッピングされているかどうかに関わらず、移行されるコンテンツに関連付けられている場合、ユーザーはグループと共に取得時にクラウドシステムに移行されます。

## ユーザーをマッピングおよび移行する際の重要な考慮事項 {#important-considerations}

### 例外的な状況 {#exceptional-cases}

次の特定のケースがログに記録されます。

1. ユーザーのメールアドレスが `profile/email` 彼らの分野 *jcr* ノード、問題のユーザーまたはグループは移行される可能性がありますが、マッピングされません。 このシナリオでは、電子メールアドレスがログイン時のユーザー名として使用されている場合でも同様です。
2. ユーザーが無効になっている場合、他のユーザーと同じように扱われ、通常どおりにマッピングおよび移行され、クラウドインスタンス上では無効のままになります。
3. ソースAEMインスタンスとターゲットAEM Cloud Serviceインスタンスの両方に同じ名前 (rep:principalName) のプリンシパルが存在する場合、問題のプリンシパルは移行されず、クラウドシステム上の既存のプリンシパルは変更されません。
4. ユーザーマッピングを使用してマッピングされずにユーザーが移行された場合、ターゲットクラウドシステムでは、ユーザーは IMS ID を使用してログインできません。 また、電子メールアドレスが IMS へのログインに使用された電子メールアドレスと一致しない場合、Target Cloud システムでも、IMS ID を使用してログインすることはできません。 従来のAEM方式（ローカルログイン）を使用してログオンできる場合がありますが、通常、この方式は望ましいものや期待されるものではありません。

## その他の考慮事項 {#additional-considerations}

* 設定が **取り込み前にクラウドインスタンス上の既存のコンテンツを消去** が設定され、Cloud Serviceインスタンスで既に転送されたユーザーは、既存のリポジトリ全体と共に削除されます。新しいリポジトリが作成され、そのリポジトリにコンテンツが取り込まれます。 このプロセスは、ターゲットCloud Serviceインスタンスに対する権限を含むすべての設定もリセットし、に追加された管理者ユーザーに対して true になります。 **管理者** グループ化します。 管理者ユーザーは、 **管理者** グループを使用して、CTT/CAM 取り込み用のアクセストークンを取得します。
* コンテンツ追加を行う際に、前回の転送以降に変更が加えられていないためにコンテンツが転送されなかった場合、そのコンテンツに関連付けられたユーザーやグループも転送されません。 このルールは、ユーザーとグループがソースシステム上で変更された場合でも当てはまります。 移行の理由は、ユーザーとグループが、関連付けられているコンテンツと共に移行されるだけです。
* ターゲットのAEM Cloud Serviceインスタンスに、ユーザー名が異なり、ソースのAEMインスタンスのユーザーの 1 人と同じ E メールアドレスを持つユーザーが存在し、「ユーザーマッピング」が有効な場合、ログにエラーメッセージが記録されます。 また、ターゲットシステムでは、指定された E メールアドレスを持つ 1 人のユーザーのみが許可されるので、ソースAEMユーザーは転送されません。
* 詳しくは、 [閉じられたユーザーグループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) 閉じられたユーザーグループ (CUG) ポリシーで使用されるプリンシパルに関するその他の考慮事項については、を参照してください。

## 最終概要とレポート {#final-report}

抽出と取り込みが正常に完了すると、主要な移行の詳細を示すレポートが生成されます。 詳しくは、 [プリンシパルの移行を検証する方法](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) を参照してください。
