---
title: タグの使用
description: タグを使用すると、Web サイト内のコンテンツをすばやく簡単に分類できます。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# タグの使用 {#using-tags}

タグを使用すると、Web サイト内のコンテンツをすばやく簡単に分類できます。タグはキーワードやラベルとしてページ、アセット、その他のコンテンツに添付し、コンテンツや関連コンテンツを検索できます。

* See Administering Tags for information about creating and managing tags, as well as to which content tags have been applied. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* See Tagging for Developers for information about the tagging framework as well as including and extending tags in custom applications. <!-- See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.-->

## タグを使用する 10 の理由 {#ten-reasons-to-use-tagging}

1. **コンテンツの整理** — タグ付けを行うと、作成者は手間をかけずにコンテンツをすばやく整理できるので、作業が容易になります。
1. **タグの整理** — タグはコンテンツ、階層的な分類法、名前空間はタグを整理します。
1. **詳細に整理されたタグ** — タグとサブタグを作成できるので、用語、サブキーワード、その関係をカバーする分類システム全体を表すことが可能になりました。 これにより、正式な階層に合わせてコンテンツの二次（または三次）階層を作成できます。
1. **管理タグ** — タグの作成とアプリケーションを制御するために、タグや名前空間に権限を適用することで、タグを制御できます。
1. **柔軟なタグ付け** — タグには多数の名前と顔が含まれます。タグ、分類用語、カテゴリ、ラベルなど。 タグのコンテンツモデルや使用方法は自由です。例えば、ターゲット層に説明を付けたり、コンテンツの分類や評価をおこなうとき、またはコンテンツの二次階層を作成するために使用できます。
1. **検索機能の強化** - AEMのデフォルトの検索コンポーネントには、様々な形で作成されたタグと適用されたタグが含まれており、このタグにフィルターを適用して、関連する結果に絞り込むことができます。
1. **SEOの有効化** — ページのプロパティとして適用したタグは、ページのメタタグに自動的に表示され、検索エンジンに表示されます。
1. **シンプルな洗練** — 単語やボタンのタッチからタグを簡単に作成できます。 その後、タイトルや説明のほか、ラベルを制限なく追加してタグにセマンティクスをさらに追加できます。
1. **コアの一貫性** — タグ付けシステムはAEMのコアコンポーネントで、すべてのAEM機能でコンテンツの分類に使用されます。 さらに、開発者はタグ付け API を使用して、同じ分類にアクセス可能な、タグ付けが有効化されたアプリケーションを作成できます。
1. **構造と柔軟性を組み合わせ** — ページとパスのネストにより、AEMは構造化された情報を扱うのに最適です。 フルテキスト検索機能が組み込まれているので、非構造化の情報の処理する際にも力を発揮します。タグ付けは構造化と柔軟性の両方の利点を結び付けます。

サイトのコンテンツ構造やアセットのメタデータスキーマを設計する際には、タグ付け機能が提供する軽量でアクセス可能なアプローチを検討してください。

## タグの適用 {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply pre-defined tags, in the **Page Properties** window use the **Tags** field and the **Select Tags** window. The **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![複数のタグの選択](/help/sites-cloud/authoring/assets/tags-select.png)

## タグの公開 {#publishing-tags}

ページの公開と非公開の方法と同様に、タグと名前空間に対して次の操作を実行できます。

### Activate {#activate}

* 個別のタグをアクティベートします。

   ページと同様、新しく作成されたタグは、発行環境で使用可能となる前にアクティベートする必要があります。

>[!NOTE]
>
>ページをアクティブ化すると、ダイアログが自動的に開き、そのページに属する非アクティブ化されたタグをアクティブ化できます。

### アクティベートを解除 {#deactivate}

* 選択したタグのアクティベートを解除します。
