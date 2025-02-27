---
title: ユニバーサルエディターについて – レスポンシブモード
description: この記事では、ユニバーサルエディターで様々なエミュレーターを使用してフォームをプレビューし、オーサリング中のルックアンドフィールを視覚化する方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# WYSIWYG オーサリングのレスポンシブモード

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信します。 例えば、リポジトリ URL がhttps://github.com/adobe/abcの場合、組織名は adobe で、リポジトリ名は abc.</span> です


[ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) を使用すると、様々なエミュレーターでEdge Delivery Services Formsをプレビューして、オーサリング中のフォームのルックアンドフィールを確認できます。

レスポンシブモードを使用すると、開発者はデスクトップ、タブレット、モバイルデバイスなど、様々な画面サイズに自動的に適応するレイアウトをデザインできます。 ユニバーサルエディターは、デスクトップ、タブレットおよびモバイルデバイス用のエミュレーターをサポートします。 画面サイズに応じて高さと幅を設定し、次のアクションを実行できます。

* 向きの設定
* 幅と高さを指定
* 向きを変更する

## 様々なデバイスのレスポンシブモードでのFormsのプレビュー

ユニバーサルエディターでは、画面の右上隅にある **エミュレーター** アイコンを使用すると、様々なデバイスサイズでページをプレビューし、レスポンシブデザインの動作をテストして、ユーザーエクスペリエンスを向上させることができます。

ユニバーサルエディターが様々な画面サイズでフォームをレンダリングする方法を確認するには、次の手順を実行します。

1. フォームをユニバーサルエディターで編集用に開きます。
1. ユニバーサルエディターツールバーで使用可能な ![ エミュレーターアイコン ](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} を選択し、エミュレーターアイコンをクリックしてオプションを表示します。

   ![ レスポンシブモード ](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. 選択したデバイスのユニバーサルエディターでフォームをエミュレートするためのオプションを選択します（デスクトップ、タブレット、モバイル）。

   ![ レスポンシブモード ](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   デフォルトでは、エディターはデスクトップレイアウトで開き、高さと幅はブラウザーによって自動的に決定されます。 または、モバイルデバイスまたはタブレットデバイス上のフォームをエミュレートすることもできます。 また、カスタムデバイスの画面の幅と高さをカスタマイズすることもできます。

ユニバーサルエディターには、様々なデバイスでフォームをプレビューするための様々なエミュレーターが用意されています。 次の表に、使用可能なエミュレータタイプと、対応するデバイス表現を示します。

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">エミュレーターのタイプ</th>
        <th style="width: 80%">デバイスの画像</th>
    </tr>
    <tr>
        <td style="width: 20%">デスクトップ</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="デスクトップエミュレーター" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">タブレットなど）のアクティブマーカーを確認する。</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="タブレットエミュレーター" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">モバイル</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="モバイルエミュレーター" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">カスタムデバイス</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="カスタムデバイスエミュレーター" style="width: auto; height: auto"></td>
    </tr>
</table>

**スクリーンローテーター** アイコンを使用すると、異なるデバイスでフォームをプレビューする際に、縦向きと横向きを切り替えることができます。 これは、開発者が、レスポンシブデザインが様々なデバイスでの画面の回転にどのように適応するかをテストするのに役立ちます。

ユニバーサルエディターは、様々なフォームレイアウトをサポートしています。 様々なレイアウトを探索するには、[ レイアウトの機能 ](#layout-capabilities) の節を参照してください。

## レイアウト機能

ユニバーサルエディターを使用すると、簡単に使用できるフォームを作成して、エンドユーザーに動的なエクスペリエンスを提供できます。 フォームのレイアウトは、フォーム内での項目やコンポーネントの表示方法をコントロールします。

ユニバーサルエディターは、フォームに対して次のタイプのレイアウトをサポートします。
* [パネルレイアウト](#panel-layout)
* [ウィザードレイアウト](#wizard-layout)
* [アコーディオンレイアウト](#accordion-layout)

### パネルレイアウト

パネルレイアウトは、関連するフィールドを整理して、対応するコンテンツを簡単に移動および検索するのに役立ちます。 パネルレイアウトを使用すると、フォーム内の個別のパネル、セクションまたはパネル内にフォームコンポーネントを配置できます。

![ パネルレイアウト ](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

[ パネルコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) を使用して、パネルレイアウトをフォームに追加できます。 パネルコンポーネントの様々なプロパティを設定する方法について詳しくは、[ パネルコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) の記事を参照してください。

### ウィザード レイアウト


ウィザードレイアウトは、複雑なフォームを明確な手順に分割してシンプル化するのに役立ちます。 各手順はプロセスの異なる部分を表し、ユーザーは多くの場合、「次へ **や「戻る** ボタンを使用して手順を順番に移動し **す**。 ウィザードレイアウトを使用すると、複数のセクションや手順を含むフォームを作成できます。

![ ウィザードのレイアウト ](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

[ ウィザードコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) を使用して、フォームにウィザードレイアウトを追加できます。 ウィザードコンポーネントの様々なプロパティを設定する方法について詳しくは、[ ウィザードコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) の記事を参照してください。

### アコーディオンレイアウト

アコーディオンレイアウトでは、アダプティブフォーム内の折りたたみ可能なセクションまたはパネルにコンテンツが表示されます。 セクションを展開すると、内にコンテンツが表示されますが、その他のセクションは折りたたまれたままです。 大量の情報をコンパクトに表示する場合に最適です。

![ アコーディオンレイアウト ](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

[ アコーディオンコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) を使用して、フォームにアコーディオンレイアウトを追加できます。 アコーディオンコンポーネントの様々なプロパティを設定する方法について詳しくは、[ アコーディオンコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) の記事を参照してください。

### 適切なレイアウトを選択する方法

ユーザーエクスペリエンスとフォーム機能を最適化するには、適切なレイアウトを選択することが重要です。 この表を参照すると、使用可能な様々なレイアウトオプションを理解でき、特定のニーズやユースケースに基づいて最も適したレイアウトを選択する際に役立ちます。

| 機能 | パネルレイアウト | ウィザード レイアウト | アコーディオンレイアウト |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **目的** | 関連するコンテンツを個別のセクションにグループ化 | 複数の手順から成るプロセスまたはフォームのガイド | コンテンツを折りたたみ可能なセクションに整理します |
| **構造** | 個別セクション | 順次ステップ/ページ | 折りたたみ可能なパネル/セクション |
| **ナビゲーション** | パネルヘッダーをクリックして移動します |  – 進む：「次へ」ボタン <br> – 戻る：「戻る」ボタン <br>- オプションのスキップ手順 | ヘッダーをクリックしてセクションを展開/折りたたむ |
| **ユーザーエクスペリエンス** | 管理しやすい方法で大量のコンテンツを整理する | ステップバイステップのガイダンス、負担の軽減 | セクションを展開/折りたたんだ状態のコンパクト ビュー |
| **ユースケース** | セクションが分類された複雑なフォーム | セットアッププロセス、複雑なフォーム | FAQ、設定メニュー、詳細なコンテンツセクション |

## 関連トピック

{{universal-editor-see-also}}
