---
title: クローズドユーザーグループの移行
description: コンテンツを Adobe Experience Manager as a Cloud Service に移行した後でクローズドユーザーグループを有効にするために必要な特別な考慮事項について説明します。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---


# クローズドユーザーグループの移行 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="クローズドユーザーグループの移行"
>abstract="クローズドユーザーグループ（CUG）の移行では、現在、移行後に運用を確認および実行するいくつかの手順が必要です。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=ja" text="AEM のクローズドユーザーグループ"

現在、クローズドユーザーグループ（CUG）を移行の宛先環境で機能させるには、追加の手順が必要です。このドキュメントでは、シナリオと、ノードを意図した方法で保護するために必要な手順について説明します。

## クローズドユーザーグループ（CUG）の移行

そのコンテンツの ACL または CUG ポリシーノードを使用して移行されたコンテンツに関連付けられている場合、グループは Adobe Experience Manager as a Cloud Service への CTT/CAM 移行に自動的に含まれます。グループとそのメンバーが存在することを、運用開始前に確認する必要があります。CUG ポリシーで参照されるグループを、ここでは「CUG グループ」と呼びます。

AEM as a Cloud Service で CUG を使用するには、ユーザーがオーサーインスタンスに存在し、関連する CUG グループのメンバーである必要があります。これは、パッケージを使用して実行できます。または、CUG ユーザーが IMS ユーザーの場合は、既に存在している可能性があります。CUG ユーザーを、AEM CUG グループのメンバーにする必要があります。

パブリッシュインスタンスで CUG の動作を有効にする手順は次のとおりです。

1. CUG グループをアクティベートする必要があります（CUG グループとそのメンバーがパブリッシュインスタンスにレプリケートされます）。
1. CUG ポリシーで保護された&#x200B;*すべて*&#x200B;のページを非公開にする必要があります（グローバル CUG カウントをクリアするため）。
1. 次に、CUG ポリシーで保護されたページを公開する必要があります（これにより、パブリッシュインスタンスが有効になり、ポリシーを追跡できます）。
1. すべてのページが公開されたら、CUG で保護された各ページの機能を確認します。

詳しくは、[クローズドユーザーグループ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=ja)を参照してください。
