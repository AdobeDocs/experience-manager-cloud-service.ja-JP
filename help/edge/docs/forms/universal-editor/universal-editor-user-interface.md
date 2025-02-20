---
title: ユニバーサルエディターについて – 開発者チュートリアル
description: このチュートリアルは、ユニバーサルエディターのインターフェイスを使い始める際に役立ちます。 ガイドに従うと、ユニバーサルエディターで独自のEdge Delivery Services フォームを作成するためのユーザーインターフェイスを理解することができます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 1%

---

# ユニバーサルエディター（WYSIWYG）インターフェイスの詳細

[ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) は、Adobe Edge 配信サービス（EDS）Forms用のシンプルで視覚的で直感的なWhat You See Is What You Get（WYSIWYG）インターフェイスを提供します。 これは、効率的なフォームオーサリングを行うためのドラッグ&amp;ドロップ機能を備えた最新のインターフェイスを提供します。

![ ユニバーサルエディターのユーザーインターフェイス ](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## ユニバーサルエディターインターフェイスについて

フォーム作成者がユニバーサルエディターを使用してフォームを編集すると、コンソールがインタラクティブなWYSIWYG インターフェイスを開き、ユーザーがフォームの編集を開始できます。

>[!NOTE]
>
> ユニバーサルエディターを使用してフォームを作成する方法については、[ ユニバーサルエディターを使用したAEM FormsのEdge Delivery Servicesの概要（WYSIWYG） ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) を参照してください。

![ ユニバーサルエディターのユーザーインターフェイス ](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

ユニバーサルエディターのインターフェイスは、次の 4 つの部分に分かれています。

* **[A:Experience Cloud ヘッダー](#experience-cloud-header)**
* **[B：ユニバーサルエディターツールバー](#universal-editor-toolbar)**
* **[C: プロパティパネル](#properties-panel)**
* **[D：エディター](#editor)**

### Experience Cloud Header

Experience Cloud ヘッダーは、コンソールの上部にあります。 Experience Cloud内の現在の場所に関する情報が提供されます。 また、他のExperience Cloud アプリケーションに移動することもできます。

![ ユニバーサルエディターのExperience Cloudヘッダー ](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


それぞれのコンポーネントについて説明します。

* **Adobe Experience Cloud**

  画面左側の **Adobe Experience Cloud** リンクをクリックすると、Experience Manager ソリューションのルートに移動し、Experience Manager Sites、Experience Manager Assets、Experience Manager Guidesなどのツールにアクセスできます。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **組織名**

  **組織名** には、現在ログインしている IMS 組織の名前が表示されます。 他の組織へのアクセス権を持っている場合は、ドロップダウンリストから選択して別の IMS 組織に切り替えることができます。 例えば、現在選択されている IMS 組織名は `AEM Forms Internal01` です。

  ![ 組織 ](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **ヘルプ**

  ヘルプアイコンを使用すると、学習リソースやサポートリソースに素早くアクセスできます。 フォーム作成者は、「**ヘルプ**」セクションにフィードバックを追加することもできます。
  ![ ヘルプ ](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **通知**

  「**通知**」セクションには、現在割り当てられている未完了の通知の数、リクエストおよび IMS 組織の現在のタスクが表示されます。

  ![ 通知 ](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **ソリューション**

  **ソリューション** リンクを使用して、他のExperience Cloud ソリューションに切り替えることができます。
  ![ ソリューション ](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **作成者**
このアイコンは、フォーム作成者の詳細と、作成者が現在ログインしている IMS 組織の名前を表します。
  ![ 作成者 ](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### ユニバーサルエディターツールバー

ツールバーを使用すると、他のフォームに移動して編集できます。 また、フォームの公開または非公開、フォームのプロパティの編集、ルールエディターへのアクセスを行うこともできます。
![ ユニバーサルエディターツールバー ](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

それぞれのコンポーネントについて説明します。

* **ホームボタン**
「ホーム」ボタンを使用すると、ユニバーサルエディターの開始ページに移動できます。 ユニバーサルエディターを使用して、編集するフォームの URL を直接入力することもできます。
  ![ ユニバーサルエディターホーム ](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **ロケーション バー**
**ロケーションバー** には、作成者が編集しているフォームのアドレスが表示されます。 また、ロケーションバーをクリックして、別のフォーム URL を入力することもできます。 キー `l` は、ロケーションバーを開くためのショートカットキーです。
  ![ ロケーションバー ](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){ 幅=50%，高さ=50%}



* **ルールエディター**

  **ルールエディター** は、ルールを作成および管理するための直感的で視覚的なインターフェイスを提供します。 ルールエディターを使用して動的なフォームの動作を追加できます。

  ![ルールエディター](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * ユニバーサルエディターでは、ルールエディター拡張機能はデフォルトでは有効になっていません。 ルールエディター拡張機能を有効にするには、公式メール ID から [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) に書き込みます。
  > * ルールの作成方法については、「WYSIWYG オーサリングのルールエディターの概要 [ を参照してください ](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

* **フォームプロパティの編集**
「**フォームプロパティを編集**」オプションをクリックすると、フォームデータモデルや公開日などのフォームプロパティを編集できます。
  ![ フォームプロパティの編集 ](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **認証ヘッダー設定**
**認証ヘッダー設定** を使用すると、作成者は、ローカル開発目的でカスタム認証ヘッダーを設定できます。
  ![ 認証ヘッダー ](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **レスポンシブモード**
  **レスポンシブモード** オプションを使用すると、ユニバーサルエディターでのフォームのレンダリング方法を定義できます。 デフォルトでは、エディターはデスクトップレイアウトで開き、高さと幅はブラウザーによって自動的に決定されます。 または、モバイルデバイスをエミュレートし、モバイルデバイスでフォームがどのように表示されるかを確認することもできます。

  ![ レスポンシブモード ](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **プレビューモード**
プレビューモードでは、フォームは公開されるときとまったく同じようにエディターに表示されます。 これにより、作成者はリンクやボタンをクリックしてフォーム内を移動できます。 編集内容に満足したら、作成者はライブユーザー用のフォームを公開できます。 編集モードとプレビューモードを切り替えるためのショートカットキーが `p` まれています。
  ![プレビュー](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **ページを開く**
「**ページを開く**」オプションを選択すると、フォームがプレビュー用の新しいタブで開きます。 フォームをプレビューモードで新しいタブで開くためのショートカットキーは、`o` です。
  ![ ページを開く ](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **公開**

  「**公開** ボタンを使用して、ライブユーザーがフォームを使用できるようにします。
  ![ 公開 ](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **省略記号**
作成者が（...）省略記号オプションをクリックすると、「**非公開**」オプションが表示されます。 フォームを非公開にするには、「**非公開** オプションを使用します。
  ![ 省略記号 ](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### プロパティパネル

**プロパティパネル** は、エディターの右側にあります。 フォームの階層で選択したコンポーネントの詳細が表示されます。 これは、コンポーネントが選択されていない場合のデフォルトの構造です。
![ue-properties パネル ](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


それぞれのコンポーネントについて説明します。


* **プロパティモード**
**プロパティ** オプションに、エディターで選択したコンポーネントのプロパティが表示されます。 例えば、この画像には、選択した数値入力コンポーネントのプロパティが表示されます。 このオプションを使用して、コンポーネントのプロパティを変更できます。 コンポーネントのプロパティを開くためのショートカットキーは `d` です。

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **コンテンツツリー**
「**コンテンツツリー**」オプションには、フォームの階層が表示されます。 作成者がコンテンツツリーで項目をクリックすると、エディターはその項目を選択し、スクロールしてそのコンポーネントに移動します。 コンテンツツリー表示を切り替えるためのショートカットキーは、キー `f` です。

  ![ コンテンツツリー ](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **バリエーションを生成**
  **バリエーションを生成** 人工知能を使用して、特定のプロンプトに基づいて異なるバージョンのフォームを生成します。 これらのプロンプトは、Adobeが提供するか、フォーム作成者が作成および管理できます。

  ![ バリエーション ](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > フォームのバリエーションを生成を使用する手順については、「バリエーションの生成 [ の記事を参照し ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations) ください

* **実験**:

  **実験** とは、フォームとレイアウトの様々なバリエーションをテストして、ユーザーエクスペリエンスとパフォーマンスを最適化するために使用される手法を指します。
  ![ 実験 ](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalization**
「**Personalization**」オプションは、Adobe エコシステムまたは外部アプリケーションの一部である Forms とAdobe Experience Platform（AEP）の間の接続を確立するための設定を行います。
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **A/B テスト**:
  **A/B テスト** フォームやレイアウトの様々なバリエーションをテストして、ユーザーエクスペリエンスとパフォーマンスを最適化するために使用される手法を参照します。
  ![A/B テスト ](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **タスク管理**:
**タスク管理** 機能を使用すると、フォームのカスタマイズと最適化に関連するタスクをチームが管理、追跡、実行できるので、ワークフローを効率化し、コラボレーションを強化できます
  ![ タスク管理 ](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){ 幅=50%，高さ=50%}

。
* **コンテンツドラフト**

  「**コンテンツドラフト**」オプションを使用すると、リッチテキスト要素のドラフトを作成できます。 ドラフトは、既存のフォームテキストを使用して、またはゼロから作成できます。 必要に応じて、ドラフトを編集または削除できます。 デフォルトでは、3 つのドラフトのみが表示されますが、残りは **すべて表示** をクリックすると表示されます。

  ![ タスク管理 ](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){ 幅=50%，高さ=50%}


* **データSource**

  「**データSource**」オプションを使用すると、フォームデータモデル（FDM）の作成時にデータソースを設定および選択できます。 これにより、選択したデータソースのすべてのデータモデルオブジェクト、プロパティ、サービスを、フォームデータモデルで使用できるようになります。
  ![ データSource](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **追加**

  **追加** オプションを選択すると、選択したコンテナに追加できるコンポーネントのドロップダウンリストが開きます。 例えば、「アダプティブフォーム」セクションでは、フォームに追加できる使用可能なコンポーネントがリストに表示されます。 コンポーネントのリストを開くためのショートカットキーは `a` です。
  ![ アイコンを追加 ](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **複製**

  「**複製**」オプションを選択すると、コンテンツツリーまたはエディターで選択されたコンポーネントのコピーが作成されます。
  ![ アイコンを複製 ](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **削除**
**削除** オプションを選択すると、コンテンツツリーまたはエディターで選択されたコンポーネントが削除されます。

  ![ 削除 ](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### エディター

エディターを使用してフォームを編集でき、ロケーションバーで指定したフォームが編集領域にレンダリングされます。 エディターがプレビューモードの場合、使用可能なボタンとリンクを使用してフォーム内を移動できます。
![ エディター ](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## 関連トピック

{{universal-editor-see-also}}
