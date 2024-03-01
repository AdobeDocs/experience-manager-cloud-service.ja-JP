---
title: EDS Formsの「ありがとうございます」ページの設定
description: EDS Formsがユーザーエクスペリエンスを最適化し、ユーザージャーニーを合理化するための、ありがとうページとリダイレクトの設定方法を説明します。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# アダプティブFormsブロックでの「ありがとうございます」ページとリダイレクトの設定

ありがとうページとリダイレクトは、ユーザーエクスペリエンスの強化の重要な側面であり、フォーム送信後の確認、明確なコミュニケーション、スムーズなナビゲーションをユーザーに提供します。

## 「ありがとうございます」ページの設定

ありがとうページは、ユーザーに対する安心感を与え、組織がブランドアイデンティティを強化しながら重要な情報を伝えるのを可能にします。 EDS Formsの「ありがとうございます」ページを設定するには、次の手順に従います。

1. Microsoft SharePointまたはGoogle Workspace のAEM Edge Delivery プロジェクトフォルダーにアクセスします。
1. プロジェクトディレクトリ内に、「thankyou」という名前のMicrosoft Word またはGoogle Docs ファイルを作成します。
1. 「thankyou」ファイルに感謝のメッセージを追加します。
   ![「ありがとうございます」ページの例](/help/edge/assets/sample-thankyou-page.png)
1. AEM Sidekickを利用して「thankyou」ファイルをプレビューし、公開します。

## 送信後にユーザーをリダイレクト

リダイレクトは、ユーザーを関連する宛先に誘導し、エンゲージメントを最適化し、コンバージョン率を高めることで、シームレスなユーザージャーニーを容易にします。

デフォルトでは、アダプティブFormsブロックはユーザーを「感謝祭」ページにリダイレクトします。 デフォルトの「thankyou」ページ以外のページにユーザーをリダイレクトするには、次の 2 つのオプションがあります。

* 既存の「ありがとうございます」ページを別のページに置き換えるか、
* 「thankyou」ページを別のページにリダイレクトします。

### 既存の「thankyou」ページを置き換える

1. を開きます。[EDS プロジェクト]/blocks/form/form.js&quot;ファイルを編集します。
1. 次を変更： `thankyou` ページを次の行から選択したページに移動します。

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Microsoft SharePointまたはGoogle Workspace の Edge Delivery Service プロジェクトフォルダーに同じ名前のページが存在することを確認します。 ページが存在しない場合は、作成して公開します。

1. 更新された「form.js」フォルダーとその基になるファイルを、GitHub の Edge 配信サービスプロジェクトにチェックインします。 この更新により、フォームは、指定したとおりに更新されたページにリダイレクトされるようになります。

1. EDS プロジェクトフォルダーにページが存在することを確認し、公開します。


### Web サイトのリダイレクトを使用

Web サイトのリダイレクトを設定して、「感謝状」ページを別のページにリダイレクトします。 詳しくは、 [リダイレクトに関するドキュメント](https://www.aem.live/docs/redirects) を参照してください。


