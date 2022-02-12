---
title: 'ヘッドレスコンテンツの権限に関する考慮事項 '
description: Adobe Experience Managerを使用したヘッドレス実装に関する様々な権限と ACL の考慮事項について説明します。 オーサー環境とパブリッシュ環境の両方で必要となる、様々なペルソナおよび潜在的な権限レベルを理解します。
feature: Content Fragments,GraphQL API
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# ヘッドレスコンテンツの権限に関する考慮事項

ヘッドレス実装では、対処する必要のあるセキュリティおよび権限の領域がいくつかあります。 権限とペルソナは、AEM環境に基づいて幅広く考慮できます **作成者** または **公開**. 各環境には、様々なペルソナが含まれ、様々なニーズを持ちます。

## オーサーサービスに関する考慮事項

オーサーサービスは、内部ユーザーがコンテンツを作成、管理および公開する場所です。 権限は、コンテンツを管理する様々なペルソナを中心に展開されます。

### グループレベルで権限を管理

ベストプラクティスとして、権限はAEMのグループに設定する必要があります。 ローカルグループとも呼ばれ、これらのグループはAEMオーサー環境内で管理できます。

グループメンバーシップを管理する最も簡単な方法は、AdobeIdentity Management System(IMS) グループを使用して割り当てることです [IMS グループからローカルAEMグループ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem).

![Admin Console 権限フロー](assets/admin-console-aem-group-permissions.png)

プロセスの概要は次のとおりです。

1. を使用して、IMS ユーザーを新規または既存の IMS ユーザーグループに追加します。 [Admin Console](https://adminconsole.adobe.com/)
1. IMS グループは、ユーザーがログインするとAEMと同期されます。
1. IMS グループをAEM Groups に割り当てます。
1. AEM Groups に権限を設定します。
1. ユーザーがAEMにログインし、IMS で認証されると、AEMグループの権限が継承されます。

>[!TIP]
>
> IMS およびAEMのユーザーとグループの管理に関する詳細なビデオチュートリアルが参照できます [ここ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html).

管理するには **グループ** AEMで、に移動します。 **ツール** > **セキュリティ** > **グループ**.

AEMでグループの権限を管理するには、次に移動します。 **ツール** > **セキュリティ** > **権限**.

### DAM ユーザー

このコンテキストでは、「DAM」は、デジタルアセット管理を表します。 この **DAM ユーザー** は、デジタルアセットやコンテンツフラグメントを管理する「毎日」のユーザーに使用できる、AEMの標準のグループです。 このグループは、 **表示**, **追加**, **更新**, **削除**、および **公開** コンテンツフラグメントと、AEM Assets内のその他すべてのファイル。

グループメンバーシップに IMS を使用する場合は、適切な IMS グループをのメンバーとして追加します。 **DAM ユーザー** グループ化します。 IMS グループのメンバーは、AEM環境にログインする際に、 DAM ユーザーグループの権限を継承します。

#### DAM ユーザーグループのカスタマイズ

標準のグループの権限を直接変更しないことをお勧めします。 代わりに、 **DAM ユーザー** グループ権限とアクセスをさらに制限 **フォルダー** AEM Assetsの

より詳細な権限については、 **権限** AEMのコンソールと、 `/content/dam` をより具体的なパスに追加すると、 `/content/dam/mycontentfragments`.

コンテンツフラグメントの作成と編集をおこなう権限をユーザーグループに与え、削除はしない方が望ましい場合があります。 編集用の権限を確認して割り当て（削除は除く）するには、 [コンテンツフラグメント — 削除に関する考慮事項](/help/assets/content-fragments/content-fragments-delete.md).

### モデルエディター

変更する機能 **コンテンツフラグメントモデル** 管理者または **小集団** 管理者権限を持つユーザーのみを対象としています。 コンテンツフラグメントモデルを変更すると、多くのダウンストリーム効果が生じます。

>[!CAUTION]
>
>コンテンツフラグメントモデルを変更すると、ヘッドレスアプリケーションが依存する基盤となる GraphQL API が変更されます。

コンテンツフラグメントモデルを管理するが、完全な管理者アクセス権を持たないグループを作成する場合は、次のアクセス制御エントリを持つグループを作成できます。

| パス | 権限 | 権限 |
|-----| -------------| ---------|
| `/conf` | **許可** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **許可** | `rep:write`、`crx:replicate` |

## 公開サービスの権限

パブリッシュサービスは「ライブ」環境と見なされ、通常、GraphQL API コンシューマーとのやり取りがおこなわれます。 コンテンツは、Author サービスで編集および承認された後、Publish サービスに公開されます。 ヘッドレスアプリケーションは、GraphQL API を介して公開サービスから承認済みコンテンツを使用します。

AEM パブリッシュサービスの GraphQL エンドポイントで公開されたデフォルトのコンテンツは、未認証ユーザーを含め、すべてのユーザーがアクセスできます。

### コンテンツの権限

AEM GraphQL API を使用して公開されるコンテンツは、 [閉じられたユーザーグループ (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) アセットフォルダーに対して設定します。このフォルダーは、AEMのユーザーグループ（およびそのメンバー）が Assets フォルダーのコンテンツにアクセスできるように指定します。

アセット CUG は次の方法で動作します。

* まず、フォルダーおよびサブフォルダーへのすべてのアクセスを拒否します。
* 次に、CUG のリストに一覧表示されているすべてのAEMユーザーグループのフォルダーとサブフォルダーへの読み取りアクセスを許可します

CUG は、GraphQL API を介して公開されるコンテンツを含むアセットフォルダーに設定できます。 AEM Publish 上のアセットフォルダーへのアクセスは、ユーザーが直接アクセスするのではなく、ユーザーグループを通じて制御する必要があります。 GraphQL API で公開されるコンテンツを含むアセットフォルダーへのアクセス権を付与するAEMユーザーグループを作成（または再利用）します。

#### 認証スキームを選択{#publish-permissions-users}

この [AEMヘッドレス SDK](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) は、次の 2 種類の認証をサポートしています。

* [トークンベースの認証](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 単一のテクニカルアカウントにバインドされたサービス資格情報を使用する。
* AEMユーザーを使用した基本認証。

### GraphQL API へのアクセス

HTTP リクエスト [適切な認証資格情報](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) AEM パブリッシュサービスの GraphQL API エンドポイントには、読み取る権限を持つコンテンツや匿名でアクセス可能なコンテンツが含まれます。 GraphQL API の他のコンシューマーは、CUG で保護されたフォルダー内のコンテンツを読み取ることができません。

