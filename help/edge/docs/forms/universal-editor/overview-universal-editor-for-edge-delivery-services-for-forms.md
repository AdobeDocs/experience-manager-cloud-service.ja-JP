---
title: Forms の Edge Delivery Services のユニバーサルエディター
description: Forms の Edge Delivery Services のユニバーサルエディターを使用して、アダプティブフォームを作成します。
feature: Edge Delivery Services
role: Admin, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 100%

---


# Forms の Edge Delivery Services のユニバーサルエディター

ユニバーサルエディターは、シンプルで視覚的かつ直感的な WYSIWYG（見たままが得られる）インターフェイスを提供することで、Adobe Edge Delivery Services のフォーム作成に革命をもたらします。コンテンツ作成者とフォーム作成者向けに設計されており、従来のフォーム作成プロセスの複雑さを排除し、技術に詳しくないユーザーでもアクセスできます。

ユニバーサルエディターを使用すると、テキストフィールド、チェックボックス、ラジオボタンなどの事前定義済みコンポーネントを使用して、レスポンシブでインタラクティブなフォームをすばやく設計できます。その堅牢な機能セットは、動的なルール、シームレスなデータ統合、高度なパーソナライゼーションをサポートし、すべてのフォームをニーズに合わせて調整します。

軽量のクライアントサイドレンダリングの管理、ブラウザー間の互換性の確保、または厳密なアクセシビリティ標準の準拠のいずれであっても、ユニバーサルエディターはフォームの作成と管理の効率化されたソリューションを提供します。

![ユニバーサルエディター](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Forms 向け Edge Delivery Services のユニバーサルエディターの主な機能



| ![WYSIWYG インターフェイス](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![ルールエディター](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![送信アクション](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**WYSIWYG インターフェイス**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**ルールエディター**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**送信アクション**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| ユニバーサルエディターでは、事前定義済みのコンポーネントライブラリ、レスポンシブデザイン、テンプレートベースの作成、リアルタイムのフィールド変更を備えたフォームデザイン用の WYSIWYG インターフェイスを提供します。 | ルールエディターを使用すると、ユーザーは、イベント駆動型ルール、即時検証、軽量の JavaScript と JSON によるエラー処理を使用して、動的なフォームインタラクションを作成できます。 | 送信アクションは、バックエンド統合、条件付き送信ロジック、安全なエンドポイント、プリプロセッサーをサポートし、送信ワークフローを効率化します。 |

| ![公開／非公開](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![レスポンシブモード](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![カスタムコンポーネント](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**公開／非公開**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**レスポンシブモード**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**カスタムコンポーネント**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| フォームの表示を簡単に制御します。数回クリックするだけでエディターから直接フォームを公開または非公開にできます。 | デバイス（デスクトップ、タブレット、モバイル）間でシームレスに適応するフォームを設計します。レスポンシブモードを使用して、様々な画面サイズのフォームをプレビューおよびテストします。 | カスタムコンポーネントを使用すると、開発者は特定の組織のユースケースに合わせて独自の要素を作成して、フォームの機能を拡張できます。 |

| ![スタイル設定](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![事前入力サービス](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B テスト](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**スタイル設定**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **[事前入力フォーム](/help/edge/docs/forms/universal-editor/prefill-form.md)** | [**A/B テスト**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| CSS を使用したスタイル設定により、開発者はフォーム要素の外観をカスタマイズし、web サイトの美観に合った視覚的に魅力的なデザインを作成できます。 | 事前入力サービスでは、様々なソースから関連するユーザーデータを自動的にフォームフィールドに入力し、手動入力を減らしてユーザーエクスペリエンスを向上させることができます。 | A/B テストにより、組織は様々なフォームのデザイン、レイアウト、機能を試して、最もパフォーマンスの高いバリアントを特定できます。 |

| ![分析とトラッキング](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![フォームフラグメント](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![データバインディング](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**分析とトラッキング**](https://www.aem.live/developer/martech-integration) | **フォームフラグメント**（近日公開） | [**データバインディング**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| ビルトインの分析とトラッキングを使用して、ユーザーの行動、フォームのインタラクション、送信率に関するインサイトを獲得し、データ駆動型のフォーム最適化を実現します。 | フォームフラグメントを使用すると、よく使用するセクションを一度作成したら、複数のフォームで再利用できるので、一貫性が確保およびメンテナンス作業が軽減され、再利用性が高まります。 | データバインディングにより、フォームフィールドとバックエンドデータソース間の直接接続が可能になり、リアルタイムの更新と、高度なデータマッピングがサポートされます。 |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![埋め込みフォーム](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![「ありがとうございます」設定](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**CAPTCHA**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **埋め込みフォーム**（近日公開） | [**「ありがとうございます」設定**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| reCAPTCHA を使用すると、フォームを自動ボットから保護し、安全で信頼性の高いデータ収集を行うことができます。 | ユニバーサルエディターのビルトインの埋め込みコンポーネントを使用して、フォームを Edge Delivery Services サイトページに直接埋め込みます。 | フォームの送信が成功した後に、ユーザーに表示される感謝のメッセージまたはページを簡単にカスタマイズします。 |



## 事前定義済みフォームコンポーネント

ユニバーサルエディターには、次のフォームコンポーネントが標準搭載されています。

<table>
  <thead>
    <tr>
      <th></th> 
      <th>フォームコンポーネント</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="フォームコンポーネント" style="width: 100%;"></td> 
      <td><b>アコーディオン</b></td>
      <td>コンテンツを整理する折りたたみ可能なパネル構造。</td>
    </tr>
    <tr>
      <td><b>ボタン</b></td>
      <td>ナビゲーションやカスタムロジックなどのアクション用にインタラクティブ要素を追加します。</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Google reCaptcha または HCaptcha を使用して人間が行う検証タスクを完了するようにユーザーに求めることで、スパムを防止します。</td>
    </tr>
    <tr>
      <td><b>チェックボックス</b></td>
      <td>ユーザーがチェックボックスを設定できます。</td>
    </tr>
    <tr>
      <td><b>チェックボックスグループ</b></td>
      <td>ユーザーがグループから複数のオプションを選択できます。</td>
    </tr>
    <tr>
      <td><b>日付選択</b></td>
      <td>ユーザーがカレンダーインターフェイスを使用して日付を選択できます。</td>
    </tr>
    <tr>
      <td><b>ドロップダウンリスト</b></td>
      <td>定義済みのリストから 1 つまたは複数のオプションを選択できます。</td>
    </tr>
    <tr>
      <td><b>メール</b></td>
      <td>基本的な形式の検証でメールアドレスをキャプチャします。</td>
    </tr>
    <tr>
      <td><b>ファイル添付</b></td>
      <td>ドキュメント、画像、またはその他のファイルタイプのアップロードを有効にします。</td>
    </tr>
    <tr>
      <td><b>フォームフラグメント</b></td>
      <td>住所フィールドや連絡先詳細などのセクションに再利用可能なフォームコンポーネント。</td>
    </tr>
    <tr>
      <td><b>画像</b></td>
      <td>フォーム内での画像のアップロードと表示をサポートします。</td>
    </tr>
    <tr>
      <td><b>モーダル</b></td>
      <td>アラート、追加情報、または確認に使用されることが多いポップアップダイアログボックスを表示します。</td>
    </tr>
    <tr>
      <td><b>数値フィールド</b></td>
      <td>数値入力をキャプチャし、数値または範囲の検証を可能にします。</td>
    </tr>
    <tr>
      <td><b>パネル</b></td>
      <td>展開／折りたたみ可能なパネルを使用して、フォームのセクションを整理します。</td>
    </tr>
    <tr>
      <td><b>ラジオボタン</b></td>
      <td>オプションのグループからの単一選択を有効にします。</td>
    </tr>
    <tr>
      <td><b>レーティング</b></td>
      <td>ユーザーが星形ベースの評価を提供できます。</td>
    </tr>
    <tr>
      <td><b>リセットボタン</b></td>
      <td>フォームフィールドをデフォルトの状態にリセットします。</td>
    </tr>
    <tr>
      <td><b>送信ボタン</b></td>
      <td>フォームの送信をトリガーし、定義されたワークフローを開始します。</td>
    </tr>
    <tr>
      <td><b>電話番号フィールド</b></td>
      <td>国に基づく形式を使用して、電話番号をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>テキスト</b></td>
      <td>法的条件を表示し、チェックボックスを通じてユーザーの同意を収集するための専用セクションを提供します。</td>
    </tr>
    <tr>
      <td><b>テキストフィールド</b></td>
      <td>名前やメールアドレスなど、単一行の入力をキャプチャします。</td>
    </tr>
    <tr>
      <td><b>ウィザード</b></td>
      <td>複数のパートで構成されるフォームプロセスを段階的にユーザーに説明します。</td>
    </tr>
  </tbody>
</table>

## よくある質問（FAQ）

**Q. ユニバーサルエディターは、どのようなユーザーが使用できますか？**
ユニバーサルエディターは、次のような幅広いオーディエンス向けに設計されています。

- 視覚に訴えるフォームを作成するコンテンツ制作者。
- 高度なカスタマイズおよび統合機能を必要とする開発者。
- スケーラブルで安全、かつ規制に準拠したフォームソリューションを探している組織。

**Q：ユニバーサルエディターで作成したフォームを既存のシステムに統合できますか？**
もちろんです。ユニバーサルエディターは、バックエンドシステムとのシームレスなデータバインディングをサポートし、リアルタイムの更新と高度なデータマッピングを可能にします。また、タスク管理用の Adobe Workfront などのツールと統合し、データ送信ワークフローの安全なエンドポイントをサポートします。

**Q：フォームコンポーネントをカスタマイズできますか？**
はい、ユニバーサルエディターを使用すると、開発者は特定の組織のニーズに合わせて調整されたカスタムコンポーネントを作成できます。さらに、UI 拡張機能とカスタムワークフローを通じてエディターの機能を拡張できます。

**Q：フォームからどのような分析を取得できますか？**
ユニバーサルエディターには、ユーザーのインタラクション、フォーム送信率およびコンバージョン指標を監視するビルトインの分析およびトラッキングツールが含まれています。これらのインサイトは、フォームを最適化してパフォーマンスを向上させるのに役立ちます。

**Q：ユニバーサルエディターはアクセシビリティにどのように対応しますか？**
ユニバーサルエディターは、WCAG（Web コンテンツアクセシビリティガイドライン）を含むアクセシビリティ標準に厳密に準拠して設計されています。これにより、障がい者でもフォームを使用できるので、包括的なエクスペリエンスを提供できます。






