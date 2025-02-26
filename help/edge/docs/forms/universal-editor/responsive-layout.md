---
title: ユニバーサルエディターについて – レスポンシブモード
description: この記事では、ユニバーサルエディターで様々なエミュレーターを使用してフォームをプレビューし、オーサリング中のルックアンドフィールを視覚化する方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

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

## 関連トピック

{{universal-editor-see-also}}
