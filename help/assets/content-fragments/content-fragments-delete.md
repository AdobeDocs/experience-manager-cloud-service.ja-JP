---
title: コンテンツフラグメント - 削除に関する考慮事項（アセット - コンテンツフラグメント）
description: AEM でコンテンツフラグメント削除ポリシーを定義する前に、以下の重要な考慮事項を確認してください。コンテンツフラグメントはヘッドレスコンテンツを配信する強力なツールです。削除する際は、影響を慎重に考慮する必要があります。
exl-id: 69c08f2f-4d51-4aea-957e-ee81c4604377
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 80%

---

# コンテンツフラグメント - 削除に関する考慮事項 {#content-fragments-delete-considerations}

AEM でコンテンツフラグメント削除ポリシーを定義する前に、以下の重要な考慮事項を確認してください。コンテンツフラグメントはヘッドレスコンテンツを配信する強力なツールです。削除する際は、影響を慎重に考慮する必要があります。

## 権限 - 削除または削除禁止 {#permissions-delete-or-not-delete}

コンテンツを削除する機能は強力ですが、この特権の割り当て方法を制限および管理する必要がある多くの業界では、慎重な取り扱いが求められる可能性があります。

削除権限に関しては、コンテンツフラグメントを次の 2 つのレベルで考える必要があります。

1. **単一のエンティティとしてのコンテンツフラグメント**。

   * **使用例**：コンテンツフラグメントの編集または更新を必要とするユーザーが&#x200B;**フラグメント全体を削除できる**&#x200B;場合。
   * **権限**：削除権限はユーザー管理やグループ管理で割り当てることができます。<!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **コンテンツフラグメントを構成する複数のサブエンティティ例えば、バリエーション、サブノードなどです。**

   コンテンツフラグメントエディターの基本的な操作では、このような一時的なサブ要素を削除できる必要があります。 例えば、バリエーションの操作、メタデータの編集、関連コンテンツの管理などをおこなう場合です。

   * **使用例**：コンテンツフラグメントの編集または更新を必要とするユーザーが&#x200B;**フラグメント全体を削除できない**&#x200B;場合。
   * **権限**：[エディター機能のみに必要な権限](#permissions-required-for-editor-functionality-only)を参照してください。

>[!NOTE]
>
>ユーザーに削除権限がない場合、コンテンツフラグメントエディターは&#x200B;*読み取り専用*&#x200B;モードで動作します。<!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>AEM でのユーザー管理操作を監査する方法も参照してください。<!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## エディター機能のみに必要な権限 {#permissions-required-for-editor-functionality-only}

コンテンツフラグメントを編集または更新する必要があっても&#x200B;**フラグメント全体を削除できない**&#x200B;ユーザーの場合は、特定の権限を割り当てる必要があります。コンテンツフラグメントエディターの基本操作を使用するには、一時的なサブ要素を削除できる必要があるからです。

例えば、バリエーションの操作、メタデータの編集、関連コンテンツの管理などをおこなう場合です。

>[!NOTE]
>
>コンテンツフラグメントの編集または更新に必要な削除権限は、ユーザー管理やグループ管理で割り当てられた削除権限に含まれています。<!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

フラグメントの編集または更新に必要な権限は、コンテンツフラグメントを含んでいるノードまたは適切な親ノード（`/content/dam` 下の任意のレベル）のどちらかに適用する必要があります。このような親ノードに割り当てられると、権限はそのブランチ内のすべてのノードに適用されます。

例えば、次のようなすべてのコンテンツフラグメントを格納するフォルダーです。

* `/content/dam/contentfragments`

>[!CAUTION]
>
>`/content/dam` に権限を設定することもできます。すべてのコンテンツフラグメントがそこに格納されているからです。
>
>ただし、この操作により、同じ削除権限が *すべて* その他のアセットタイプも同様です。

特定のユーザーやグループに対し、コンテンツフラグメントの編集や更新を許可するための権限の前提条件は次のとおりです。

>[!NOTE]
>
>このリストには、削除特権だけでなく、必要なすべての特権が含まれています。

* コンテンツフラグメントノードまたはフォルダーの場合：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* すべてのコンテンツフラグメントの `jcr:content` ノードの場合：

   * `jcr:addChildNodes`、`jcr:modifyProperties`、`jcr:removeChildNodes`

* すべてのコンテンツフラグメントの `jcr:content` 下にあるすべてのノードの場合：

   * `jcr:addChildNodes`、`jcr:modifyProperties`、`jcr:removeChildNodes`、`jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
