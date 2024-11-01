---
title: ユニバーサルエディター 2024.08.13 リリースノート
description: ユニバーサルエディターの 2024.08.13 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c66621eb336b8e6eb5ceb1056c089c190fcd1c34
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# ユニバーサルエディター 2024.08.13 リリースノート {#release-notes}

ユニバーサルエディターの 2024 年 8 月 13 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Serviceの最新のリリースノートについては、[ このページ ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## 新機能 {#what-is-new}

* **カスタムデータタイプ**：プロパティパネル内にカスタムフィールドを作成 [ できるので、独自のデータニーズに合わせてエディターをカスタマイズできます。](https://developer.adobe.com/uix/docs/services/aem-universal-editor/api/item-types-renderers/)
   * コマースのユースケース用にカスタム製品ピッカーを開発する場合でも、ドロップダウンリストにバックエンドの値を入力する場合でも、この機能を使用すると、作成者がコンテンツの作成に使用するデータを制御できます。
* **クロスコンテナのドラッグ&amp;ドロップ**:[ コンテンツツリーパネル内で [ ドラッグ&amp;ドロップを使用して異なるコンテナ間でコンポーネントを移動 ](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) でき、レイアウト構成の柔軟性が向上します。](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **最適化された GitHub 統合**:GitHub 応答のキャッシュが導入され、タグと `universal-editor-cors-library` の取得が大幅に高速化され、ユーザーエクスペリエンスが高速でスムーズになりました。
* **設定可能な IMS トークン検証**：トークン管理の柔軟性を高めるために、[IMS トークン検証がオプションになりました。](/help/implementing/universal-editor/local-dev.md#setting-up-service)
   * この設定オプションを使用すると、必要に応じて検証を無効にして、クラウドゲートウェイの設定を簡素化できます。
* **Splunk 統合**:Splunk ログは、モニタリングと診断を強化し、ローカル開発のために [ ユニバーサルエディターサービスに統合され ](/help/implementing/universal-editor/local-dev.md#setting-up-service) した。
   * この統合により、効率的なログトラッキング、よりスムーズな操作、迅速なトラブルシューティングが保証されます。

## バグ修正 {#bug-fixes}

* **公開フィードバックの強化**：権限が不十分なために公開が失敗した場合、公開中のユーザーへのフィードバックが改善されて、単に失敗を示すのではなく、明確な警告が表示されるようになりました。
* **URL 処理の改善**：誤った URL エンコーディング/デコードが原因で公開に失敗していた問題を修正しました。
* **正確なデータ処理**：浮動小数が誤って整数として保存される問題に対処し、コンテンツ全体で正確なデータ処理を確保しました。
* **セキュリティと安定性**:Docker イメージのセキュリティの脆弱性を修正し、コンポーネントピッカーやパンくずリストなどの重要なコンポーネントのカバレッジをテストし、より安全で安定した信頼性の高いエディターエクスペリエンスを実現しました。
