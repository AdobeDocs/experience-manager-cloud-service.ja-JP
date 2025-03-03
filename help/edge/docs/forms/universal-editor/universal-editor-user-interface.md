---
title: ユニバーサルエディターについて - 開発者向けチュートリアル
description: このチュートリアルは、ユニバーサルエディターのインターフェイスを起動および実行するのに役立ちます。ユニバーサルエディターで独自の Edge Delivery Services フォームを作成するユーザーインターフェイスを理解できます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 96%

---

# ユニバーサルエディター（WYSIWYG）インターフェイスの詳細

[ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) は、Adobe Edge 配信サービスForms用のシンプルで視覚的かつ直感的なWhat You See Is What You Get（WYSIWYG）インターフェイスを提供します。 ドラッグ＆ドロップ機能を備えた最新のインターフェイスで、効率的なフォームオーサリングを実現します。

![ユニバーサルエディターのユーザーインターフェイス](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## ユニバーサルエディターのインターフェイスについて

フォーム作成者がユニバーサルエディターを使用してフォームを編集すると、コンソールはインタラクティブな WYSIWYG インターフェイスを開き、ユーザーがフォームの編集を開始できます。

>[!NOTE]
>
> ユニバーサルエディターを使用してフォームを作成する方法について詳しくは、[ユニバーサルエディター（WYSIWYG）での AEM Forms の Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)を参照してください。

![ユニバーサルエディターのユーザーインターフェイス](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

ユニバーサルエディターのインターフェイスは、次の 4 つの部分に分かれています。

* **[A：Experience Cloud ヘッダー](#experience-cloud-header)**
* **[B：ユニバーサルエディターのツールバー](#universal-editor-toolbar)**
* **[C: プロパティパネル](#properties-panel)**
* **[D：エディター](#editor)**

### Experience Cloud ヘッダー

Experience Cloud ヘッダーは、コンソールの上部にあります。Experience Cloud 内の現在の場所に関する情報を提供します。また、他の Experience Cloud アプリケーションに移動することもできます。

![ユニバーサルエディターの Experience Cloud ヘッダー](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


それぞれのコンポーネントについて説明します。

* **Adobe Experience Cloud**

  画面の左側にある **Adobe Experience Cloud** リンクをクリックすると、Experience Manager ソリューションのルートに移動し、Experience Manager Sites、Experience Manager Assets、Experience Manager Guides などのツールにアクセスできます。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **組織名**

  **組織名**&#x200B;には、現在ログインしている IMS 組織の名前が表示されます。他の組織へのアクセス権がある場合は、ドロップダウンリストから選択して、別の IMS 組織に切り替えることができます。例えば、現在選択されている IMS 組織名は `AEM Forms Internal01` です。

  ![組織](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **ヘルプ**

  ヘルプアイコンを使用すると、学習リソースやサポートリソースにクイックアクセスできます。フォーム作成者は、「**ヘルプ**」セクションにフィードバックを追加することもできます。
  ![ヘルプ](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **通知**

  「**通知**」セクションには、現在割り当てられている未完了の通知の数、リクエストおよび IMS 組織内の現在のタスクが表示されます。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **ソリューション**

  **ソリューション**リンクを使用して、他の Experience Cloud ソリューションに切り替えることができます。
  ![ソリューション](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **作成者**
アイコンは、フォーム作成者の詳細と、作成者が現在ログインしている IMS 組織の名前を表します。
  ![作成者](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### ユニバーサルエディターのツールバー

ツールバーを使用すると、他のフォームに移動して編集できます。また、フォームを公開または非公開にしたり、フォームのプロパティを編集したり、ルールエディターにアクセスしたりすることもできます。
![ユニバーサルエディターのツールバー](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

それぞれのコンポーネントについて説明します。

* **「ホーム」ボタン**
「ホーム」ボタンを使用すると、ユニバーサルエディターの開始ページに移動できます。また、ユニバーサルエディターを使用して、編集するフォームの URL を直接入力することもできます。
  ![ユニバーサルエディターのホーム](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **ロケーションバー**
**ロケーションバー**&#x200B;には、作成者が編集しているフォームのアドレスが表示されます。また、ロケーションバーをクリックして、別のフォーム URL を入力することもできます。ロケーションバーを開くショートカットキーは `l` キーです。
  ![ロケーションバー](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **ルールエディター**

  **ルールエディター**&#x200B;には、ルールを作成および管理する直感的で視覚的なインターフェイスが用意されています。ルールエディターを使用して、動的なフォーム動作を追加できます。

  ![ルールエディター](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * ユニバーサルエディターでは、ルールエディター拡張機能はデフォルトで有効になっていません。ルールエディター拡張機能を有効にするには、公式メール ID から [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) までご連絡ください。
  > * ルールの作成方法について詳しくは、[WYSIWYG オーサリングのルールエディターの概要](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)の記事を参照してください。

* **フォームプロパティを編集**
「**フォームプロパティを編集**」オプションをクリックすると、フォームデータモデルや公開日などのフォームプロパティを編集できます。
  ![フォームプロパティを編集](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **認証ヘッダー設定**
**認証ヘッダー設定**を使用すると、作成者はローカル開発目的でカスタム認証ヘッダーを設定できます。
  ![認証ヘッダー](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **レスポンシブモード**
  「**レスポンシブモード**」オプションを使用すると、ユニバーサルエディターによるフォームのレンダリング方法を定義できます。デフォルトでは、エディターはデスクトップレイアウトで開き、高さと幅はブラウザーで自動的に決定されます。または、モバイルデバイスをエミュレートして、フォームがモバイルデバイス上でどのように表示されるかを確認することもできます。

  ![レスポンシブモード](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **プレビューモード**
プレビューモードでは、フォームは公開されるときとまったく同じようにエディターに表示されます。これにより、作成者は、リンクやボタンをクリックしてフォーム内を移動できます。編集が完了したら、作成者はフォームをライブユーザー向けに公開できます。編集モードとプレビューモードを切り替えるショートカットキーは `p` です。
  ![プレビュー](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **ページを開く**
「**ページを開く**」オプションを選択すると、フォームがプレビュー用の新しいタブで開きます。新しいタブでプレビューモードでフォームを開くショートカットキーは `o` です。
  ![ページを開く](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **公開**

  「**公開**」ボタンを使用すると、フォームをライブユーザーが使用できます。
  ![公開](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **省略記号**
作成者が（...）省略記号オプションをクリックすると、「**非公開**」オプションが表示されます。フォームを非公開にするには、「**非公開**」オプションを使用します。
  ![省略記号](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### プロパティパネル

**プロパティパネル**は、エディターの右側にあります。フォームの階層で選択したコンポーネントの詳細が表示されます。これは、コンポーネントが選択されていない場合のデフォルトの構造です。
![UE プロパティパネル](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


それぞれのコンポーネントについて説明します。


* **プロパティモード**
「**プロパティ**」オプションでは、エディターで選択したコンポーネントのプロパティが表示されます。例えば、画像には、選択した数値入力コンポーネントのプロパティが表示されます。このオプションを使用して、コンポーネントのプロパティを変更できます。コンポーネントのプロパティを開くショートカット キーは `d` です。

  ![UE プロパティ](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **コンテンツツリー**
「**コンテンツツリー**」オプションには、フォームの階層が表示されます。 作成者がコンテンツツリー内の項目をクリックすると、エディターはその項目を選択し、そのコンポーネントまでスクロールします。コンテンツツリービューを切り替えるショートカットキーは、`f` キーです。

  ![コンテンツツリー](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **バリエーションを生成**
  **バリエーションを生成**&#x200B;は、人工知能を使用して、特定のプロンプトに基づいて様々なバージョンのフォームを生成します。これらのプロンプトは、アドビが提供するか、フォーム作成者が作成および管理できます。

  ![バリエーション](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > フォームのバリエーションを生成を使用する手順について詳しくは、[バリエーションを生成](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)の記事を参照してください

* **実験**：

  **実験**とは、ユーザーエクスペリエンスとパフォーマンスを最適化することを目的に、フォームやレイアウトの様々なバリエーションのテストに使用されるテクニックを指します。
  ![実験](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **パーソナライゼーション**
「**パーソナライゼーション**」オプションは、Adobe エコシステムまたは外部アプリケーションの一部であるフォームと Adobe Experience Platform（AEP）間の接続を確立する設定を指定します。
  ![パーソナライゼーション](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **A/B テスト**：
  **A/B テスト**とは、ユーザーエクスペリエンスとパフォーマンスを最適化することを目的に、フォームとレイアウトの様々なバリエーションのテストに使用されるテクニックを指します。
  ![A/B テスト](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **タスク管理**：
**タスク管理**機能を使用すると、チームがフォームのカスタマイズと最適化に関連するタスクを管理、追跡、実行できるようにすることで、ワークフローを効率化し、共同作業を強化できます。
  ![タスク管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

。
* **コンテンツドラフト**

  「**コンテンツドラフト**」オプションを使用すると、リッチテキスト要素のドラフトを作成できます。ドラフトは、既存のフォームテキストを使用して作成することも、ゼロから作成することもできます。必要に応じて、ドラフトを編集または削除できます。デフォルトでは 3 つのドラフトのみが表示されますが、「**すべて表示**」をクリックすると残りが表示されます。

  ![タスク管理](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **データソース**

  「**データソース**」オプションを使用すると、フォームデータモデル（FDM）を作成する際に、データソースを設定および選択できます。この方法の場合、選択したデータソースのすべてのデータモデルオブジェクト、プロパティ、サービスを、フォームデータモデル内で使用できます。
  ![データソース](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **追加**

  「**追加**」オプションを選択すると、選択したコンテナに追加できるコンポーネントのドロップダウンリストが開きます。例えば、「アダプティブフォーム」セクションでは、フォームに追加できる使用できるコンポーネントがリストに表示されます。コンポーネントのリストを開くショートカットキーは `a` です。
  ![追加アイコン](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **複製**

  「**複製**」オプションを選択すると、コンテンツツリーまたはエディターで選択したコンポーネントのコピーが作成されます。
  ![複製アイコン](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **削除**
「**削除**」オプションを選択すると、コンテンツツリーまたはエディターで選択したコンポーネントが削除されます。

  ![削除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### エディター

エディターを使用すると、フォームを編集でき、ロケーションバーで指定したフォームが編集領域にレンダリングされます。エディターがプレビューモードの場合、使用可能なボタンとリンクを使用してフォームを移動できます。
![エディター](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## 関連トピック

{{universal-editor-see-also}}
