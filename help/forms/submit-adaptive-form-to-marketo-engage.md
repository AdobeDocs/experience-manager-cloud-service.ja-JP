---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 20%

---

# 既存のフォーム用の Marketo Engage に対する送信アクションの設定

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

![ワークフロー](/help/forms/assets/workflow-marketo-3.png)

アダプティブFormsエディターには、アダプティブFormsデータをAdobe Marketo Engageに送信して処理するための **送信Marketo Engage** 送信アクションが用意されています。 送信時にデータを [Adobe Marketo Engage](https://experienceleague.adobe.com/ja/docs/marketo/using/home) に送信するように、既存のアダプティブフォームを設定できます。

フォームの送信を処理するための、すぐに使用できる様々な送信アクションを使用できます。 これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事を参照してください。

## フォームのMarketo Engageへの送信アクションを設定する際の考慮事項

* フォーム送信時にMarketo Engageにデータを送信するように、アダプティブフォームがMarketo Engageデータソースで設定されていることを確認します。 ただし、フォームがMarketo Engageデータスキーマで設定されている場合でも、送信アクションを代替アクション（**OneDrive に送信** や **SharePointに送信** などに変更することができます。

## 既存のフォームをMarketo Engageするための送信アクションを設定するための前提条件

Marketo Engageへの送信アクションを設定するための前提条件は次のとおりです。

* アダプティブフォームの [Marketo Engageデータソースを設定し ](/help/forms/use-marketo-engage-data-source-in-form.md) フォーム要素をMarketo Engageフィールドにバインドします。

## 既存のフォームをMarketo Engageに送信する方法を教えてください。

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

アダプティブフォームの送信アクションを、Adobe Marketo Engageにデータを送信するように設定できます。 Marketo Engageに対する送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
2. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
3. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。送信アクションを設定するための「アダプティブフォームコンテナ」ダイアログボックスが開きます。
4. 「**[!UICONTROL 送信]**」タブを開き、送信アクションを「**Marketo Engageに送信** として選択します。
5. 「**[!UICONTROL 完了]**」をクリックします。

![Marketo送信操作 ](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}


アダプティブフォームの送信アクションを **Marketo Engageに送信** に設定すると、Adobe Marketo Engageにデータを送信して処理できます。 このデータを使用して、マーケティングキャンペーンの分析と最適化、フォローアップメールの自動化、フォーム送信に基づくワークフローのトリガーを行うことができます。

## よくある質問（FAQ）

**Q:Marketo Engageスキーマに接続するように設定されたフォームの送信アクションを変更できますか？**
**A:** デフォルトでは、Marketo Engageスキーマと接続するようにフォームが設定されている場合、**Marketoに送信** アクションが選択されています。 ただし、必要に応じて、フォームの送信アクションを変更できます。

## 次の手順

また、アダプティブフォームを [Munchkin ライブラリ ](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/setup/munchkin) に接続して、訪問数、クリック数、フォーム送信数をトラッキングすることもできます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
