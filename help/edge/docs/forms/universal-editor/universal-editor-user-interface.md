---
title: ユニバーサルエディターについて
description: このチュートリアルは、ユニバーサルエディターのインターフェイスを起動および実行するのに役立ちます。ユニバーサルエディターで独自の Edge Delivery Services フォームを作成するユーザーインターフェイスを理解できます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 11%

---


# ユニバーサルエディター（WYSIWYG）インターフェイスの詳細

[ユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)は、Adobe Edge Delivery Services Forms 用のシンプルで視覚的かつ直感的な WYSIWYG（見たままが得られる）インターフェイスを提供します。ドラッグ＆ドロップ機能を備えた最新のインターフェイスで、効率的なフォームオーサリングを実現します。

![ユニバーサルエディターのユーザーインターフェイス](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 学習内容

このチュートリアルを終了すると、次のことができるようになります。

- ユニバーサルエディターインターフェイスの主なコンポーネントについて
- 様々なインターフェイスセクションを自信を持って移動します
- フォーム作成に不可欠なツールへのアクセス方法と使用方法を理解する
- 生産性を向上させるキーボードショートカットについて理解する

## ユニバーサルエディターインターフェイスについて

ユニバーサルエディターを使用してフォームを編集すると、コンソールが開き、すぐに編集を開始できるインタラクティブなWYSIWYG インターフェイスが表示されます。 このインターフェイスは、作業時に視覚的なフィードバックをリアルタイムで提供し、エンドユーザーに対してフォームがどのように表示されるかを正確に示します。

>[!NOTE]
>
> ユニバーサルエディターを使用してフォームを作成する方法について詳しくは、[ユニバーサルエディター（WYSIWYG）での AEM Forms の Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)を参照してください。

![ユニバーサルエディターのユーザーインターフェイス](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

ユニバーサルエディターのインターフェイスは、次の 4 つの論理部分に分かれています。

- **[A：Experience Cloud ヘッダー](#experience-cloud-header)**
- **[B：ユニバーサルエディターのツールバー](#universal-editor-toolbar)**
- **[C: プロパティパネル](#properties-panel)**
- **[D：エディター](#editor)**

それぞれのセクションを詳しく見ていきましょう。

### Experience Cloud ヘッダー

Experience Cloud ヘッダーは、コンソールの上部に表示され、より広範なAdobe Experience Cloud エコシステム内のナビゲーションコンテキストを提供します。 現在の場所が表示され、他のExperience Cloud アプリケーションにすばやくアクセスできます。

![ユニバーサルエディターの Experience Cloud ヘッダー](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

次に、各コンポーネントについて説明します。

- **Adobe Experience Cloud**

  画面左側の **Adobe Experience Cloud** リンクをクリックすると、Experience Manager ソリューションのルートに移動できます。 ここから、Experience Manager Sites、Experience Manager Assets、Experience Manager Guidesなどの他のツールにアクセスできます。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **組織名**

  **組織名** には、現在ログインしているIdentity Management System （IMS）組織の名前が表示されます。 複数の組織にアクセスできる場合は、このドロップダウンメニューを使用して組織を切り替えることができます。 例えば、スクリーンショットでは、現在選択されている IMS 組織は「AEM Forms Internal01」です。

  ![ 組織 ](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **ヘルプ**

  ヘルプアイコンを使用すると、学習リソースやサポートリソースにすばやくアクセスできます。 これは、課題が発生した場合や、特定の機能に関するガイダンスが必要な場合に特に役立ちます。 また、この節を通じてフィードバックを送信することもできます。

  ![ヘルプ](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **通知**

  「**通知**」セクションには、IMS 組織で現在割り当てられている未完了の通知、リクエストおよび現在のタスクの数が表示されます。 このセクションを監視することで、ワークフローを常に把握することができます。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **ソリューション**

  **ソリューション** メニューを使用すると、他のAdobe Experience Cloud ソリューションに切り替えることができ、ワークフロー内の様々なツールを簡単に移動できます。

  ![ソリューション](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **ユーザープロファイル**

  このアイコンは、プロファイル情報と、現在ログインしている IMS 組織の名前を表示します。 アカウント設定とサインアウトオプションにアクセスするには、このアイコンをクリックします。

  ![作成者](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### ユニバーサルエディターのツールバー

ツールバーには、基本的なナビゲーションおよび編集ツールが用意されています。 これを使用すると、フォーム間の移動、フォームの公開または非公開、フォームプロパティの編集、動的な動作を追加するためのルールエディターへのアクセスを行うことができます。

![ユニバーサルエディターのツールバー](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

各コンポーネントの機能は次のとおりです。

- **ホームボタン**

  「ホーム」ボタンをクリックすると、ユニバーサルエディターの開始ページに戻ります。 これは、別のフォームで作業を開始する必要がある場合に役立ちます。 また、ロケーションバーに URL を直接入力して、編集する任意のフォームに移動することもできます。

  ![ユニバーサルエディターのホーム](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **ロケーション バー**

  **ロケーションバー** には、現在編集中のフォームのアドレスが表示されます。 別のフォームに切り替えるには、ロケーションバーをクリックして URL を入力します。 ロケーションバーにフォーカスするためのキーボードショートカットが `l` です。

  ![ ロケーション バー ](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **ルールエディター**

  **ルールエディター** を使用すると、直感的なビジュアルインターフェイスを通じて、フォームに動的な動作を追加できます。 これを使用すると、ユーザーの入力に応答する条件、検証、アクションを作成して、フォームをインタラクティブかつインテリジェントにすることができます。

  ![ルールエディター](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - ユニバーサルエディターでは、ルールエディター拡張機能はデフォルトでは有効になっていません。 この強力な機能を有効にするには、公式メールアドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にお問い合わせください。
  > - ルールの作成および管理方法については、[WYSIWYG オーサリングでのルールエディターの概要 ](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) を参照してください。

- **フォームプロパティを編集**

  **フォームプロパティを編集** オプションを使用すると、フォームデータモデル（FDM）や公開日などの重要なフォーム設定を設定できます。 これらのプロパティは、フォームの動作およびバックエンドシステムとの統合の方法に影響します。

  ![フォームプロパティを編集](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **認証ヘッダー設定**

  「**Authentication Header Settings**」オプションを使用すると、ローカル開発用のカスタム認証ヘッダーを設定できます。 これは、認証資格情報を必要とするフォームをテストする場合に特に便利です。

  ![ 認証ヘッダー ](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **レスポンシブモード**

  **レスポンシブモード** 機能を使用すると、様々なデバイスでのフォームの表示方法をテストできます。 デフォルトでは、エディターはデスクトップレイアウトで開きますが、モバイルビューに切り替えて、フォームをより小さな画面で引き続き使用できて魅力的なものにすることができます。

  ![ レスポンシブモード ](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **プレビューモード**

  **プレビューモード** では、公開時に表示されるとおりにフォームを表示します。 これにより、ユーザーと同様に、リンクやボタンをクリックしてフォームを操作できます。 これは、公開する前に、すべてが期待どおりに動作することを確認するための不可欠な手順です。 キーボードショートカットキーを使用して、編集モードとプレビューモードを切り替 `p` ます。

  ![プレビュー](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **ページを開く**

  **ページを開く** ボタンをクリックすると、フォームがプレビュー用の新しいブラウザータブで開きます。 これにより、エディターインターフェイスを使用せずにフォームを全画面表示できます。 このアクションのキーボードショートカットは `o` です。

  ![ページを開く](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **公開**

  ユーザーがフォームを使用できる状態になったら、「**公開** ボタンを使用すると、フォームをライブにして、オーディエンスから使用できます。 これは、フォーム作成ワークフローの最後のステップです。

  ![公開](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **省略記号メニュー**

  省略記号（...）をクリックすると、現在ライブになっているフォームの **非公開** 機能など、追加のオプションが表示されます。 これは、フォームを一時的に公開アクセスから削除する必要がある場合や、フォームを更新バージョンに置き換える必要がある場合に便利です。

  ![ 省略記号 ](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### プロパティパネル

**プロパティパネル** は、インターフェイスの右側に表示され、フォームで選択した内容に基づいてコンテキスト情報を表示します。 コンポーネントが選択されていない場合、フォーム構造全体が表示されます。

![ プロパティパネル ](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

その主要なコンポーネントを見てみましょう。

- **プロパティモード**

  **プロパティ** モードには、現在選択しているコンポーネントの設定とオプションが表示されます。 ここで、特定の要件に合わせてフォームの個々の要素をカスタマイズします。 選択したコンポーネントのプロパティを開くためのキーボードショートカットが `d` きます。

  ![プロパティ](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **コンテンツツリー**

  **コンテンツツリー** には、フォームの階層構造が表示されます。 この視覚的表現は、コンポーネントが相互にどのようにネストされているかを理解するのに役立ちます。 ツリー内の項目をクリックすると、エディター内でその項目が選択され、スクロールしてその場所に移動します。 これは、特に複雑なフォームで役立ちます。 キーボードショートカット `f` ーを使用してコンテンツツリー表示を切り替えます。

  ![コンテンツツリー](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **バリエーションを生成**

  **バリエーションの生成** 機能は、人工知能を利用して、特定のプロンプトに基づいてフォームの様々なバージョンを作成します。 これにより、各バリエーションを手動で作成することなく、様々なアプローチやデザインを試すことができます。 プロンプトは、Adobeから提供することも、ユーザーがカスタマイズすることもできます。

  ![バリエーションを生成](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > フォームのバリエーションを生成するを使用する手順について詳しくは、[ バリエーションの生成 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/generative-ai/generate-variations) の記事を参照してください。

- **実験**

  **実験** 機能を使用すると、様々なフォームデザインとレイアウトを比較する制御されたテストを実行できます。 ユーザーが各バリアントとどのようにやり取りするかを分析することで、コンバージョン率とユーザーエクスペリエンスを最適化するためのデータに基づく意思決定を行うことができます。

  ![ 実験 ](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **パーソナライズ機能**

  **Personalization** 設定を使用すると、フォームをAdobe Experience Platform（AEP）または外部アプリケーションと接続できます。 この接続により、ユーザーデータと行動に基づいてカスタマイズされたフォームエクスペリエンスを作成でき、関連性とエンゲージメントを高めることができます。

  ![パーソナライズ機能](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **A/B テスト**

  **A/B テスト** は、フォームの特定のバリエーションを比較して、パフォーマンスが優れたフォームを判断するのに役立ちます。 より広範な実験とは異なり、A/B テストは通常、特定の要素や変更の比較に焦点を当て、最も効果的なオプションを特定します。

  ![A/B テスト](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **タスクの管理**

  **タスク管理** 機能を使用すると、チームがフォームの作成と最適化に関連するタスクを整理、追跡、完了するのに役立つことで、共同作業が効率化されます。 これにより、明確な説明責任を持って効率的にプロジェクトを進めることができます。

  ![ タスクの管理 ](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **コンテンツドラフト**

  **コンテンツドラフト** 機能を使用すると、フォームのテキスト要素の予備バージョンを作成して保存できます。 既存のフォームテキストを使用してドラフトを作成することも、最初からドラフトを作成することもできます。その後、必要に応じてドラフトを編集または削除します。 デフォルトでは 3 つのドラフトが表示されますが、「**すべて表示**」をクリックすると、追加のドラフトが表示されます。

  ![コンテンツドラフト](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **データソース**

  「**データSource**」オプションを使用すると、フォームデータモデル（FDM）のデータソースを設定および選択できます。 この統合により、選択したソースのすべてのデータモデルオブジェクト、プロパティ、サービスをフォーム内で使用できるようになり、動的なデータ取得と送信が可能になります。

  ![データソース](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **追加**

  **追加** ボタンをクリックすると、現在選択しているコンテナに追加できるコンポーネントのドロップダウンリストが表示されます。 例えば、アダプティブフォーム セクションを選択すると、そのセクションに追加できるすべてのコンポーネントがこのリストに表示されます。 このコンポーネントリストを開くためのキーボードショートカットは `a` です。

  ![ アイコンを追加 ](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **複製**

  「**複製** オプションは、選択したコンポーネントの正確なコピーを作成します。 これにより、最初から作成するのではなく、複製してから変更できるので、複数の類似要素が必要な場合に時間を節約できます。

  ![ 複製アイコン ](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **削除**

  **削除** オプションは、選択したコンポーネントをフォームから削除します。 このオプションを使用する場合は、確認プロンプトが表示されずに要素がすぐに削除されるので、注意が必要です。

  ![削除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### エディター

エディターは、フォームを作成および変更する中心的なワークスペースです。 場所バーで指定されたフォームが表示され、フォームがユーザーにどのように表示されるかを正確に示すWYSIWYG エクスペリエンスが提供されます。 プレビューモードでは、ボタンやリンクを介したナビゲーションをテストして、ユーザーと同じようにフォームを操作できます。

![エディター](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

エディターでは、コンポーネントの追加、プロパティの設定および整理を行い、直感的で効果的なフォームエクスペリエンスを作成して、ほとんどの時間を費やすことができます。

## キーボードショートカットの概要

生産性を高めるために、次の重要なキーボードショートカットに注意してください。

- `l` - ロケーションバーをフォーカスします
- `p` – 編集モードとプレビューモードを切り替えます
- `o` - フォームを新しいタブで開く
- `d` – 選択したコンポーネントのプロパティを開く
- `f` - コンテンツツリー表示を切り替えます
- `a` – 追加するコンポーネントのリストを開きます


