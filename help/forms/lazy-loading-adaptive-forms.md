---
title: 遅延読み込みによる大きなフォームのパフォーマンスの向上させる方法
description: 遅延読み込みを使用して大きなフォームのパフォーマンスを向上させる方法について説明します。遅延読み込みを使用すると、フォームのフラグメントが表示されるまでそれらの初期化と読み込みを延期することにより、大きく複雑なアダプティブフォームのパフォーマンスを向上できます。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 0cd38edb-2201-4ca6-8b84-6b5b7f76bd90
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: ht
source-wordcount: '1063'
ht-degree: 100%

---

# 遅延読み込みによる大きなフォームのパフォーマンスの向上 {#improve-performance-of-large-forms-with-lazy-loading}

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/lazy-loading-adaptive-forms.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


## 遅延読み込みの概要 {#introduction-to-lazy-loading}

フォームが数百以上のフィールドを持ち、大きく複雑になると、エンドユーザーはフォームがレンダリングされる際に長時間待たされることになります。応答時間を最小にするために、アダプティブフォームでは、フォームを複数の論理的なフラグメントに分解し、これらのフラグメントを表示する必要が生じるまで、それらの初期化や読み込みを遅延するように設定できます。これを遅延読み込みと呼びます。さらに、遅延読み込みが設定されたフラグメントは、ユーザーがフォーム内の他のセクションに移動するとアンロードされ、フラグメントは表示されなくなります。

まず最初に、遅延読み込みを設定する前に、要件と準備手順を説明します。

## 遅延読み込みを設定するための準備 {#preparing-to-configure-lazy-loading}

アダプティブフォーム内のフラグメントの遅延読み込みを設定する前に、フラグメントを作成し、スクリプトで使用されたり他のフラグメントで参照されたりする値を特定し、遅延読み込みされたフラグメントの表示をコントロールするためのルールを定義するといった、戦略を定義することが重要です。

* **フラグメントの特定と作成**
遅延読み込みを設定できるのは、アダプティブフォームのフラグメントのみです。フラグメントとは、アダプティブフォームの外側にある独立したセグメントで、フォーム間で再利用できます。したがって、遅延読み込みを実装するための最初の手順は、フォーム内の論理的なセクションを特定し、それらをフラグメントに変換することです。フラグメントは、最初から作成することも、または既存のフォームパネルをフラグメントとして保存することもできます。

  <!--For more information about creating fragments, see [Adaptive Form Fragments](adaptive-form-fragments.md).-->

* **グローバルな値の特定とマーク付け**
フォームベースのトランザクションには、ユーザーからの適切なデータを取得し、それを処理してフォーム入力エクスペリエンスを簡素化するための動的な要素が含まれます。例えば、フォームのフラグメント X 内にフィールド A があり、その値が別のフラグメント内のフィールド B の有効性を決定するとします。この場合、フラグメント X が遅延読み込みに対してマーク付けされた場合、フィールド A の値は、フラグメント X が読み込まれていないときでも、フィールド B を検証するために利用できる必要があります。これを実現するには、フィールド A をグローバルとしてマーク付けします。これにより、その値が、フラグメント X が読み込まれていないときでもフィールド B の検証のために使用できるようになります。

  フィールド値をグローバルにする方法については、[遅延読み込みの設定](lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p)を参照してください。

* **フィールドの表示をコントロールするルールの記述**
フォームには、必ずしもすべてのユーザーや条件に適用されないフィールドやセクションがいくつか含まれます。フォームの作成者や開発者は、ユーザーの入力に基づいてその表示をコントロールするために表示／非表示ルールを使用します。例えば、会社住所フィールドは、フォームの職業ステータスで無職を選択したユーザーには表示されません。ルールの作成について詳しくは、[ルールエディターの使用](rule-editor.md)を参照してください。

  遅延読み込みされたフラグメント内で表示ルールを使用して、必要な場合にのみ条件付きフィールドを表示させることができます。また、条件付きフィールドをグローバルとしてマーク付けして、遅延読み込みフラグメントの表示式内でそれを参照することもできます。

## 遅延読み込みの設定 {#configuring-lazy-loading}

以下の手順を実行して、アダプティブフォームフラグメントに対して遅延読み込みを有効にします。

1. 遅延読み込みを有効にしたいフラグメントを含むアダプティブフォームをオーサリングモードで開きます。
1. アダプティブフォームフラグメント、「![設定](assets/configure-icon.svg)」の順に選択します。
1. サイドバーで、「**[!UICONTROL フラグメントを緩慢に読み込む]**」を有効にして、「**完了**」を選択します。

   ![アダプティブフォームフラグメントに対する遅延読み込みの有効化](assets/lazy-loading-fragment.png)

   フラグメントの遅延読み込みが有効になりました。

遅延読み込みフラグメント内のオブジェクトの値をグローバルとしてマーク付けすることで、これらの値は、そのフラグメントが読み込まれていなくてもスクリプトで使用できるようになります。以下の操作を実行します。

1. アダプティブフォームフラグメントをオーサリングモードで開きます。
1. グローバルとしてマークしたい値のフィールド、「![設定](assets/configure-icon.svg)」の順に選択します。
1. サイドバーで、**[!UICONTROL 遅延読み込み中に値を使用]**&#x200B;を有効にします。

   ![サイドバーの遅延読み込みフィールド](assets/enable-lazy-loading.png)

   この値は、グローバルとしてマーク付けされ、そのフラグメントが読み込まれていないときでもスクリプト内で使用できます。

## 遅延読み込みを設定するための注意点とベストプラクティス {#considerations-and-best-practices-for-configuring-lazy-loading}

遅延読み込みを使用する際に留意しておかなければならない制限事項、レコメンデーションおよび重要な点を以下に示します。

* 大きなフォームに対して遅延読み込みを設定する場合は、XFA ベースのアダプティブフォームよりも XSD スキーマベースのアダプティブフォームを使用することをお勧めします。XFA ベースのアダプティブフォームでの遅延読み込みの実装によるパフォーマンスの向上は、XSD ベースのアダプティブフォームでの向上に比べて、相対的に小さくなります。
* ルートパネルの&#x200B;**[!UICONTROL レスポンシブ - ナビゲーションを使用せず、すべてを 1 ページに集約]**&#x200B;レイアウトを使用するアダプティブフォームのフラグメントに遅延読み込みを設定しないでください。レスポンシブレイアウト設定の結果、すべてのフラグメントがアダプティブフォームに同時に読み込まれます。パフォーマンスが低下する可能性もあります。
* アダプティブフォームの読み込み時に表示する最初のパネル内のフラグメントに対しては遅延読み込みを設定しないことをお勧めします。
* 遅延読み込みは、フラグメント階層の最大 2 レベルまでサポートされます。
* グローバルとしてマークされたフィールドがアダプティブフォーム内で一意であることを確認してください。
* 条件に基づいて表示または非表示する必要があるフラグメントに対して、フラグメントの表示ルールを記述することを検討します。例えば、配偶者情報フラグメントは、ユーザーによって指定された婚姻ステータスに基づいて表示または非表示にできます。
* ファイル添付および利用条件コンポーネントは、遅延読み込みフラグメントではサポートされません。

### 遅延読み込みを設定するためのスクリプトに関するベストプラクティス {#scripting-best-practices-for-configuring-lazy-loading}

遅延読み込みパネル用のスクリプトの作成時に留意しておく必要のある重要な点を以下に示します。

* 遅延読み込みが設定されたフラグメントで使用される初期化および計算スクリプトは、べき等になるようにしてください。べき等のスクリプトとは、何度実行しても同じ結果になるスクリプトです。
* フィールドのグローバルに使用できるプロパティを使用して、遅延読み込みパネル内にあるフィールドの値をフォームのその他のすべてのパネルで使用できるようにしてください。
* フィールドがフラグメント間でグローバルとしてマークされているかどうかにかかわらず、遅延パネル内部のフィールドの参照値を転送しないでください。
* パネルリセット機能を使用して、パネル上で表示されているすべてのものを、以下のクリック式を使用してリセットしてください。\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;})).resetData()


## 関連トピック {#see-also}

{{see-also}}