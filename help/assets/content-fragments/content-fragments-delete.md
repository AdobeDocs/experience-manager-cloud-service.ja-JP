---
title: コンテンツフラグメント - 削除に関する考慮事項
description: コンテンツフラグメント - 削除に関する考慮事項
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# コンテンツフラグメント - 削除に関する考慮事項{#content-fragments-delete-considerations}

## 権限 - 削除または削除禁止 {#permissions-delete-or-not-delete}

コンテンツを削除する機能は強力ですが、この権限の割り当て方法を制限および管理する必要がある多くの業界では、慎重な取り扱いが求められる可能性があります。

削除権限に関しては、コンテンツフラグメントは次の2つのレベルで考慮する必要があります。

1. **単一のエンティティとしてのコンテンツフラグメント**。

   * **使用例**：コンテンツフラグメントの編集または更新を必要とするユーザーが&#x200B;**フラグメント全体を削除できる**&#x200B;場合。
   * **権限**:削除権限は、ユーザー管理またはグループ管理を通じて割り当てることができます。 <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **コンテンツフラグメントを構成する複数のサブエンティティ（例：バリエーション、サブノードなど）。**

   コンテンツフラグメントエディターの基本操作を使用するには、そうした一時的なサブ要素を削除できる必要があります。例えば、バリエーションの操作、メタデータの編集、関連コンテンツの管理などをおこなう場合です。

   * **使用例**：コンテンツフラグメントの編集または更新を必要とするユーザーが&#x200B;**フラグメント全体を削除できない**&#x200B;場合。
   * **権限**:「エディター機能にのみ必要な権限」を参照してください。 <!-- See [Permissions Required for Editor Functionality Only](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only). -->

>[!NOTE]
>
>When a user does not have any Delete permissions, the Content Fragment editor operates in *read-only* mode. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>See also How to Audit User Management Operations in AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## エディター機能のみに必要な権限 {#permissions-required-for-editor-functionality-only}

コンテンツフラグメントを編集または更新する必要があっても&#x200B;**フラグメント全体を削除できない**&#x200B;ユーザーの場合は、特定の権限を割り当てる必要があります。コンテンツフラグメントエディターの基本操作を使用するには、一時的なサブ要素を削除できる必要があるからです。

例えば、バリエーションの操作、メタデータの編集、関連コンテンツの管理などをおこなう場合です。

>[!NOTE]
>
>The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission assigned through User and/or Group Management. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

The permissions needed to edit/update a fragment need to be applied to either the node containing the content fragment, or an appropriate parent node (at any level under `/content/dam`). このような親ノードに割り当てられた権限は、そのブランチ内のすべてのノードに適用されます。

例えば、すべてのコンテンツフラグメントが格納される次のようなフォルダーです。

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Setting the permissions on `/content/dam` is also possible, as all content fragments are stored here.
>
>ただし、その場合は、他の&#x200B;*すべての*&#x200B;アセットタイプにも同じ削除権限が適用されます。

特定のユーザーまたはグループにコンテンツフラグメントの編集または更新を許可するうえであらかじめ必要な権限は次のとおりです。

>[!NOTE]
>
>この一覧には、削除権限だけでなく、必要なすべての権限が含まれています。

* コンテンツフラグメントノードまたはフォルダーの場合：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* For the `jcr:content`node of all Content Fragments:

   * `jcr:addChildNodes`, `jcr:modifyProperties` および `jcr:removeChildNodes`

* For all nodes below `jcr:content` of all Content Fragments:

   * `jcr:addChildNodes`, `jcr:modifyProperties` および `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
