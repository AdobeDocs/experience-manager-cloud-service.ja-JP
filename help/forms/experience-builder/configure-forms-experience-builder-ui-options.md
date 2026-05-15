---
title: Forms Experience Builder UI オプションの設定
description: 最適なユーザーエクスペリエンスを実現するために、Forms Experience Builderのインターフェイスのオプションと設定を設定およびカスタマイズする方法について説明します。
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: d481e705-62bf-47f7-a832-1a005ec5ec59
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---

# Forms Experience Builder UI オプションの設定

>[!NOTE]
>
> Forms Experience Builderは、早期アクセスプログラムで利用できます。 開始する前に、アクセスをリクエストし、許可されていることを確認してください。

Forms Experience Builderには、ワークフローの環境設定や組織のニーズに応じてインターフェイスをカスタマイズするための様々なUI設定オプションが用意されています。

## インターフェイスのカスタマイズオプション

### 会話を削除

Forms Experience Builderの履歴から特定の会話スレッドを削除します。

**使用するタイミング：**

- 機密情報や機密情報を含む会話を削除する
- 古い会話スレッドや無関係な会話スレッドのクリーンアップ
- プライバシーとデータのセキュリティを維持

**削除方法：**

1. 会話履歴パネルに移動します
2. 削除する会話を探します
3. 会話の横にある削除アイコンをクリックします
4. ポップアップダイアログで削除を確認する

**重要なメモ：**

- 削除された会話は復元できません
- このアクションは、ローカルの履歴からのみ会話を削除します
- 会話で作成されたフォームデータと設定は変更されません

### 新しい会話を開始

Forms Experience Builderで新しい会話スレッドを開始します。

**使用するタイミング：**

- 新しいフォームプロジェクトの作業を開始
- 異なるフォーム作成タスク間の切り替え
- 作業を分割された会話スレッドに整理
- 新しいフォーム作成セッションのコンテキストをクリア

**開始方法：**

1. インターフェイスの「新規会話」ボタンをクリックします
2. または、キーボードショートカット（Ctrl+NまたはCmd+N）を使用します
3. 新しい会話スレッドが作成されます
4. 新しいフォーム要件の説明を開始する

**メリット：**

- 様々なフォームプロジェクトを整理します
- 新しいフォームの作成に最適な状態を提供
- 各プロジェクトの会話履歴を管理します
- AIによるコンテキストと応答精度の向上

### チャットをクリア

会話スレッドを維持しながら、現在の会話をクリアします。

**使用するタイミング：**

- 現在の会話からすべてのメッセージを削除
- 同じ会話スレッド内で新たに開始します
- スレッドを失うことなく、乱雑な会話をクリーンアップ
- スレッドのメンテナンス中に会話コンテキストをリセットする

**消去する方法：**

1. 消去する会話を開きます
2. 会話メニューの「チャットをクリア」オプションをクリックします
3. ポップアップダイアログでアクションを確認する
4. 会話スレッドは残りますが、すべてのメッセージが削除されます

**削除との違い：**

- **チャットをクリア**: メッセージを削除しますが、会話スレッドを維持します
- **会話を削除**：会話スレッド全体を削除します
- **新しい会話を開始**：まったく新しい会話スレッドを作成します

### ヘルプの取得

UI設定の追加サポートについて：

- [Forms Experience Builder FAQ](forms-experience-builder-frequently-asked-questions.md)を確認します
- [はじめにガイド ](forms-experience-builder-getting-started.md)を確認する
- テクニカルサポートについては、システム管理者にお問い合わせください

## 関連記事

- [Forms Experience Builderの概要](product-overview.md)
- [Forms Experience Builderの基本を学ぶ](forms-experience-builder-getting-started.md)
- [Forms Experience Builderのデプロイと設定](deploy-forms-experience-builder.md)
- [よくある質問](forms-experience-builder-frequently-asked-questions.md)
