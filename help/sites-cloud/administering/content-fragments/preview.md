---
title: コンテンツフラグメントのプレビュー
description: 様々な方法でコンテンツフラグメントをプレビューする方法について説明します。
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: 40c02806-76a2-43ed-982c-0410c2125a36
source-git-commit: 5413e173ac159015f224845e238779c5dc997ee5
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 37%

---

# コンテンツフラグメントのプレビュー {#previewing-content-fragments}

コンテンツフラグメントは、ヘッドレス配信とページオーサリングの両方に使用できます。 フラグメントはコンテンツのみで、フォーマットが設定されていないため、レビューがより困難になる可能性があります。 そのため、様々なシナリオで、フラグメントをプレビューする複数の方法が用意されています。

コンテンツフラグメントには、コンソールフラグメントコンソールとエディターからアクセスできる複数の方法があります。 この節で説明するコンソールとエディターは、ヘッドレスコンテンツ配信用に開発されました（ただし、すべてのシナリオで使用できます）。

フラグメントをプレビューするには、次の操作を行います。

* [&#x200B; プレビューインスタンス &#x200B;](#preview-instance)に公開して、から非公開にする

* [外部アプリケーション &#x200B;](#preview-url-pattern)で、[&#x200B; プレビューURL パターン &#x200B;](#preview-url-pattern)を使用しています

* [&#x200B; ビジュアライゼーション （HTML） テンプレートを使用](#preview-with-visualization-html-templates)

もちろん、[&#x200B; コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/authoring.md)でフラグメントを表示することもできます。

>[!IMPORTANT]
>
>コンテンツフラグメントには、**コンテンツフラグメント**&#x200B;と **Assets** の 2 つのコンソールからアクセスできます。
>
>また、コンテンツフラグメントをオーサリングするエディターは 2 つあります。基本機能は同じですが、いくつか違いがあります。 両方のエディターは、両方のコンソールからアクセスできます。
>
>この節では、**コンテンツフラグメント**&#x200B;コンソールと&#x200B;*新しい*&#x200B;コンテンツフラグメントエディターについて説明します。 これらはヘッドレスコンテンツ配信用に開発されています（ただし、すべてのシナリオで使用できます）。
>
>詳しくは、次のセクションを参照してください。
>
>* [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)のための **Assets** コンソールの使用
>* [*元の*&#x200B;コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)の使用
>* [ページオーサリング用のコンテンツフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)の使用

## プレビューインスタンス {#preview-instance}

フラグメントを&#x200B;**[プレビューサービス](/help/headless/deployment/architecture.md)** （およびパブリッシュインスタンス）に&#x200B;**公開**&#x200B;および&#x200B;**非公開**&#x200B;できます。

フラグメントは、エディターまたはコンソールから公開できます。

以下を参照してください。

* 詳細については、[&#x200B; フラグメントの公開とプレビュー](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)を参照してください。

* 詳細については、[&#x200B; フラグメント &#x200B;](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment)を非公開にします。

## 外部アプリケーションでのプレビュー {#preview-in-an-external-application}

コンテンツフラグメントエディターは、編集内容を外部フロントエンドアプリケーションでプレビューするオプションを作成者に提供します。

### プレビュー URL パターン {#preview-url-pattern}

この機能を使用するには、まず次の操作が必要です。

* IT チームと協力して、JSON 出力を使用してコンテンツフラグメントをレンダリングする外部フロントエンドアプリケーションを設定します。

* 外部フロントエンドアプリケーションが設定されると、**デフォルトのプレビュー URL パターン**&#x200B;は、[適切なコンテンツフラグメントモデルのプロパティ](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties)として定義される必要があります。

プレビューURLは、次のパターンに従う必要があります。

    `https://<preview_url>?param=${expression}`

使用できる式は次のとおりです。

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

URLが定義されると、**[プレビュー](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)** ボタンがエディターの上部ツールバーでアクティブになります。 このボタンを選択すると、（別のタブで）外部アプリケーションを起動して、コンテンツフラグメントをレンダリングできます。

### 外部アプリケーションでのプレビュー {#preview-in-the-external-application}

コンテンツフラグメントは、外部アプリケーションでプレビューできます。

>[!NOTE]
>
>このオプションには、[&#x200B; プレビューURL パターン &#x200B;](#preview-url-pattern)を設定する必要があります。

1. コンテンツフラグメントコンソールで、フラグメントの場所に移動します。
1. エディターでフラグメントを開きます
1. 上部のツールバーから「**プレビュー**」を選択します。
1. **アプリケーション**&#x200B;を選択して、外部アプリケーションでフラグメントを開きます（例：[&#x200B; ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)）。

## ビジュアライゼーション（HTML）テンプレートを使用したプレビュー {#preview-with-visualization-html-templates}

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>ビジュアルコンテンツフラグメントは現在、限定的でご利用いただけます。
>
>参加を希望される場合は、公式メールアドレスから[experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com)にリクエストを送信してください。

AEMでは、HTML テンプレートに基づいたビジュアルレイアウトを使用して、コンテンツフラグメントをプレビューできます。

テンプレート [&#128279;](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md#preview-your-template-with-a-template)を使用してフラグメントを プレビューする方法について詳しくは、[&#x200B; ビジュアルコンテンツフラグメント &#x200B;](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)を参照してください。

>[!NOTE]
>
>独自のHTML テンプレートを作成、カスタマイズ、アップロードする方法について詳しくは、[&#x200B; ビジュアルコンテンツフラグメント – テンプレート &#x200B;](/help/implementing/developing/extending/content-fragments-visualization-templates.md)を参照してください。

