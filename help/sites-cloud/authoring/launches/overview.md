---
title: ページのローンチ
description: Adobe Experience Manager as a Cloud Serviceでページにローンチを使用する方法を説明します。 ローンチを使用すると、現在のページを維持しながら、将来のリリース向けにコンテンツを効率的に開発できます。
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 3859393b94680ac1c786bfe31950e6073650167f
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 85%

---

# ページのローンチ {#launches-for-pages}

Adobe Experience Manager（AEM）as a Cloud Serviceでは、ローンチを使用すると、将来のリリース向けにコンテンツを効率的に開発できます。

*ローンチ* が作成され、現在のコンテンツを維持しながら、今後の公開に備えて変更を加えることができます。 AEM ページの場合は、現在公開されているページと、今後公開されるページのバージョンの 2 つを同時に効果的に編集することになります。 その時間が来たら、元のページを置き換えて、新しいバージョンを公開できます。

<!--
>[!NOTE]
>
>Launches are also available for Content Fragments. The basic concepts are the same, but there are differences in how to manage them in AEM. 
>
>For full details see [Launches for Content Fragments](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).
-->

*ローンチ*&#x200B;を作成し、*ローンチ*&#x200B;ページを編集および更新した後、*ソース*&#x200B;に&#x200B;*昇格*&#x200B;して戻します。その後、これらの&#x200B;*ソース*&#x200B;ページ（上位レベル）をアクティブ化できます。昇格により、ローンチコンテンツを複製してソースページに戻します。これは、手動または自動で行うことができます（ローンチを作成および編集するときに設定されるフィールドに依存します）。

例えば、オンラインストアの季節商品のページを四半期ごとに更新し、現在の季節に合わせて目玉商品を表示します。次の四半期の更新に備えて、適切な web ページのローンチを作成できます。四半期中、次のような変更がローンチコピーに蓄積されます。

* ソースページに対して、通常の管理タスクの結果として行われた変更。これらの変更内容は、ローンチページに自動的に複製されます。
* 次の四半期に備えて、ローンチページで直接行われた編集。

また、次のことを実行できます。

* ローンチブランチのコンテンツをナビゲートします。必要に応じて、ページを追加または削除します。
* 公開済みのコンテンツが将来の特定の日付にどのように表示されるかをプレビューします。

次の四半期が始まるとき、ローンチページを昇格させて（更新されたコンテンツを保持している）ソースページを公開できます。すべてのページを昇格させるか、変更したページのみを昇格させることができます。

ローンチで次のアクションを実行することもできます。

* ローンチを複数のルート分岐に対して作成します。サイト全体のローンチを作成（してそこで変更を加えることが）できますが、サイト全体をコピーする必要があるので、これは実用的ではありません。何百何千ものページが関与すると、コピーアクションや後の昇格タスクで必要な比較の両方により、システム要件とパフォーマンスが影響を受けます。
* ローンチをネスト（ローンチをローンチ内に作成）して、既存のローンチからローンチを作成できます。これにより、作成者は各ローンチで同じ変更を複数回加えることなく、既に加えられた変更を利用できます。

ここでは、サイトコンソール内または[ローンチコンソール](#the-launches-console)内からローンチページを作成、編集、昇格（必要に応じて[削除](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)）する方法について説明します。

* [ローンチの作成](/help/sites-cloud/authoring/launches/creating.md)
* [ローンチの編集](/help/sites-cloud/authoring/launches/editing.md)
* [ローンチ内でのページの管理](/help/sites-cloud/authoring/launches/managing-pages.md)
* [タイムワープを使用したローンチに基づくコンテンツのプレビュー](/help/sites-cloud/authoring/launches/preview.md)
* [ローンチの昇格](/help/sites-cloud/authoring/launches/promoting.md)

## ローンチ - イベントの順序 {#launches-the-order-of-events}

ローンチを使用すると、アクティベートされた 1 つ以上の web ページの今後のリリース用にコンテンツを効率的に開発できます。

ローンチでは、次のことを実行できます。

* ソースページのコピーを作成できます。
   * コピーがローンチになります。
   * トップレベルのソースページは、「**実稼働**」と呼ばれます。
      * ソースページは複数の（別個の）分岐から取得できます。

  ![ローンチの操作の順序](/help/sites-cloud/authoring/assets/launches-order.png)

* ローンチの設定を編集できます。
   * ローンチに対してページや分岐を追加または削除できます。
   * 「**タイトル**」、「**ローンチ日**」、「**実稼動準備完了**」フラグなどのローンチプロパティを編集します。
* コンテンツの昇格や公開は、手動または自動で行えます。
   * 手動:
      * 公開する準備ができたら、ローンチを&#x200B;**ターゲット**（ソースページ）に戻して昇格させます。
      * （戻して昇格させた後に）ソースページからコンテンツを公開します。
      * すべてのページまたは変更したページのみを昇格させます。
   * 自動 - これには次の要素が関与します。
      * 「**ローンチ日**（**ライブ日付**）」**フィールド**：ローンチを作成または編集するときに設定できます。
      * 「**実稼動準備完了**」フラグ：ローンチを編集するときにのみ設定できます。
      * 「**実稼動準備完了**」フラグが設定されると、ローンチは指定の「**ローンチ**&#x200B;**日**（**開始日**）」に実稼動ページに自動的に昇格されます。昇格後、実稼働ページは自動的に公開されます。\
        日付が設定されていない場合、フラグの効果はありません。
* ソースの更新とページのローンチを並行して行うことができます。
   * ソースページに対する変更は、ローンチコピーに自動的に反映されます（ライブコピーなど、継承するように設定されている場合）。
   * ローンチコピーに対する変更は、ソースコピーの自動更新を中断することなく行うことができます。

  ![並行実行されるアクション](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [ネストされたローンチの作成](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - ローンチ内でのローンチの作成：
   * ソースは既存のローンチです。
   * [ネストされたローンチを任意のターゲットに昇格できます](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)。親ローンチや最上位のソースページ（実稼働）を指定することもできます。

  ![ネストされたローンチ](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >ローンチを削除すると、ローンチ自体およびネストされているすべてのローンチが削除されます。

>[!NOTE]
>
>ローンチを作成および編集するには、デフォルトグループ `content-authors` と同様に、`/content/launches` へのアクセス権限が必要です。
>
>問題が発生している場合は、システム管理者にお問い合わせください。

## 「参照」のローンチ（サイトコンソール） {#launches-in-references-sites-console}

1. **Sites** のコンソールで、ローンチのソースに移動します。
1. **参照**&#x200B;パネルを開き、ソースページを選択します。
1. 「**ローンチ**」を選択すると、既存のローンチが一覧表示され、**ローンチコンソール**&#x200B;にアクセスできます。

   ![サイトコンソールでのローンチの参照](/help/sites-cloud/authoring/assets/launches-references.png)

1. 適切なローンチを選択すると、使用可能なアクションのリストが表示されます。

   ![サイトコンソールでローンチに対して実行可能なアクション](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## ローンチコンソール {#the-launches-console}

<!--
>[!NOTE]
>
>This console is only for Launches for Pages. 
>
>To manage your Content Fragments see [Launches for Content Fragments](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).
-->

ローンチコンソールを使用すると、ローンチの概要を確認し、リストされたローンチに対して処理を実行できます。

![ローンチコンソール - コンテンツを管理](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

コンソールは次の方法でアクセスできます。

* **ツール**&#x200B;コンソールで、**ツール**／**一般**／**ローンチ**&#x200B;と選択します。

* Sites コンソールでソースコンテンツをナビゲートする際に、**参照**&#x200B;パネルの「**ローンチ**」セクションの下部にある「**ローンチコンソール**」をクリックします。

  ![Sites コンソールのローンチの「参照」にあるローンチコンソール](/help/sites-cloud/authoring/assets/launches-references.png)

* 右上の「**ローンチ**」ボタン（Sites コンソールでローンチコンテンツをナビゲーションする場合）。

  ![Sites コンソールのローンチオプション](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
