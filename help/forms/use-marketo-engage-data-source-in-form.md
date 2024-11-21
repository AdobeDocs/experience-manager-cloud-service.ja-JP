---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 15%

---


# 既存のアダプティブFormsのMarketo Engageデータソースを設定する

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

![ワークフロー](/help/forms/assets/workflow-marketo-2.png)

Marketo Engageを既存のAEM Formsと統合するためのクラウドサービス設定を作成したら、フォームのデータソースを設定できます。

データ統合を設定すると、ユーザーは様々なデータソースやスキーマに接続できます。 Marketo Engageのデータソースと統合し、異なるフォームで使用すると、そのデータに対する操作が容易になります。 アダプティブフォームでサポートされる標準提供データソースを調べるには、[ データソースの設定 ](/help/forms/configure-data-sources.md) の記事を参照してください。

## フォームのMarketo Engageデータソースを設定する際の考慮事項

フォーム用のMarketo Engageデータソースを設定する際の考慮事項は次のとおりです。

* Edge Delivery Services FormsをMarketo Engageと接続することはできません。

## フォームにMarketo Engageデータソースを使用するための前提条件

フォームでMarketo Engageデータソースを使用するための前提条件は次のとおりです。

* Marketo Engageをフォームと統合するための [ クラウドサービス設定を作成します ](/help/forms/integrate-form-to-marketo-engage.md)。

## 既存のアダプティブフォームをMarketo Engageデータソース用に設定する方法

アダプティブフォームにMarketo Engageデータソースを設定するには、次の手順を実行します。
1. [!DNL Experience Manager Forms] オーサーインスタンスにログインします。

1. アダプティブフォームを編集用に開きます。
1. コンテンツツリーを開き、「**[!UICONTROL ガイドコンテナ]**」を選択します。
1. アダプティブフォームコンテナのプロパティ（![アダプティブフォームコンテナのプロパティ](/help/forms/assets/configure-icon.svg) アイコン）をクリックします。データソースを設定するための「アダプティブフォームコンテナ」ダイアログボックスが開きます。
1. 「**[!UICONTROL データモデル]**」タブを開き、フォームモデルを「**コネクタ**」として選択します。
1. ドロップダウンリストから **[!UICONTROL コネクタ]** を選択します。

1. **[!UICONTROL コネクタ]** を選択したら、クラウド設定を選択できます。

   ![Marketo コネクタの選択 ](/help/forms/assets/select-marketo-connector.png)

   選択したMarketo Engage設定に基づいて、フォーム要素がサイドバーの **[!UICONTROL コンテンツブラウザー]** の **[!UICONTROL データモデルオブジェクト]** タブに表示されます。 これらの要素をドラッグ&amp;ドロップして、アダプティブフォームを作成できます。

   ![Marketo データSource](/help/forms/assets/marketo-engage-data-source.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

これで、接続されたMarketo Engageインスタンスからのデータソースでアダプティブフォームが設定されました。 次に、データをAdobe Marketo Engageに送信するように設定します。

## よくある質問（FAQ）

**Q：フォームのコネクタを変更するとどうなりますか？**\
**A:** フォームのコネクタを変更すると、既存の連結が無効になります。

**Q:Marketo Engageと統合されたフォームのルールエディターの呼び出しサービスで使用できる 3 つの操作を教えてください。**\
**A:** Marketo Engageと統合されたフォームの場合、**サービスの呼び出し** で使用できる、以下の 3 つの標準の操作を以下に示します。
* リードを同期
* リードを ID で取得
* フィルタータイプでリードを取得

## 次の手順

これで、アダプティブFormsのMarketo Engageデータソースを設定しました。 次に、[ アダプティブフォームを設定してMarketo Engageにデータを送信する ](/help/forms/submit-adaptive-form-to-marketo-engage.md) ことができます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}


