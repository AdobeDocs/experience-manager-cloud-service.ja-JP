---
title: コンテンツフラグメントのプレビュー
description: 様々な方法でコンテンツフラグメントをプレビューする方法について説明します。
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: 40c02806-76a2-43ed-982c-0410c2125a36
source-git-commit: 19931f7cc911376f5096903a2d99d6ff11f928ac
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 39%

---

# コンテンツフラグメントのプレビュー {#previewing-content-fragments}

コンテンツフラグメントは、ヘッドレス配信とページオーサリングの両方に使用できます。 フラグメントはコンテンツのみで、フォーマットが設定されていないため、レビューがより困難になる可能性があります。 そのため、様々なシナリオで、フラグメントをプレビューする複数の方法が用意されています。

コンテンツフラグメントには、コンソールフラグメントコンソールとエディターからアクセスできる複数の方法があります。 この節で説明するコンソールとエディターは、ヘッドレスコンテンツ配信用に開発されました（ただし、すべてのシナリオで使用できます）。

フラグメントをプレビューするには、次の操作を行います。

* [ プレビューインスタンス ](#preview-instance)に公開して、から非公開にする

* [外部アプリケーション ](#preview-url-pattern)で、[ プレビューURL パターン ](#preview-url-pattern)を使用しています

* [ ビジュアライゼーション （HTML） テンプレートを使用](#preview-with-visualization-html-templates)

もちろん、[ コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/authoring.md)でフラグメントを表示することもできます。

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

* 詳細については、[ フラグメントの公開とプレビュー](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)を参照してください。

* 詳細については、[ フラグメント ](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment)を非公開にします。

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
>このオプションには、[ プレビューURL パターン ](#preview-url-pattern)を設定する必要があります。

1. コンテンツフラグメントコンソールで、フラグメントの場所に移動します。
1. エディターでフラグメントを開きます
1. 上部のツールバーから「**プレビュー**」を選択します。
1. **アプリケーション**&#x200B;を選択して、外部アプリケーションでフラグメントを開きます（例：[ ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)）。

## ビジュアライゼーション（HTML）テンプレートを使用したプレビュー {#preview-with-visualization-html-templates}

AEMでは、HTML テンプレートに基づいたビジュアルレイアウトを使用して、コンテンツフラグメントをプレビューできます。

テンプレート ](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md#preview-your-template-with-a-template)を使用してフラグメントを[ プレビューする方法について詳しくは、[ ビジュアルコンテンツフラグメント ](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)を参照してください。

>[!NOTE]
>
>独自のHTML テンプレートを作成、カスタマイズ、アップロードする方法について詳しくは、[ ビジュアルコンテンツフラグメント – テンプレート ](/help/implementing/developing/extending/content-fragments-visualization-templates.md)を参照してください。
