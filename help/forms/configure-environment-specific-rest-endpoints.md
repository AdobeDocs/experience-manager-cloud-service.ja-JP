---
title: 同じアダプティブフォームに対する環境固有のREST エンドポイントの設定| Adobe Experience Manager as a Cloud Service
description: 同じアダプティブフォームを、開発、ステージング、実稼動環境全体の異なるREST送信エンドポイントにフォームを変更せずにルーティングする方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 40410875-96d0-4728-8cbd-b1e1dfa438c4
source-git-commit: 8d60f09ffd3912f4a14df01baccf1c368a518a91
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 4%

---


# 同じアダプティブフォームに対する環境固有のREST エンドポイントの設定

アダプティブフォームを開発からステージングから実稼動に昇格させる場合、フォーム自体は同じままですが、通常、各環境の&#x200B;*different* REST エンドポイントにフォームを送信する必要があります。 フォームの送信アクションでエンドポイント URLをハードコーディングすると、同じURLがフォームとともにあらゆる環境に移動するため、これを壊します。

この記事では、ポータブルな単一のアダプティブフォームを保持し、その[REST エンドポイントに送信](/help/forms/configure-submit-action-restpoint.md) アクションを各環境の正しいエンドポイントに解決する方法について説明します。 フォームはURLではなく名前&#x200B;*でREST設定*&#x200B;を参照し、各環境はその設定に独自の値を提供します。

## 前提条件 {#prerequisites}

* コアコンポーネントに基づくアダプティブフォーム。
* **クラウド設定**&#x200B;が有効になっている設定ブラウザー（**ツール** > **一般** > **設定ブラウザー**）を介して作成された[設定コンテナ ](/help/implementing/developing/introduction/configurations.md)。
* 各環境（または[Cloud Manager デプロイメントパイプライン ](/help/implementing/deploying/overview.md#deploying-content-packages-via-cloud-manager-and-package-manager)）で&#x200B;**ツール** > **Cloud Services**&#x200B;およびプロモーション用に[ パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)にアクセスするための権限。

## ステージングでのRESTful サービス設定の作成 {#create-rest-configuration}

>[!VIDEO](https://video.tv.adobe.com/v/3492383)

ステージング作成者インスタンスで、フォームが参照する名前付き設定を作成します。 **サービスエンドポイント URL**&#x200B;をステージング用のRESTまたはWebhook エンドポイントに設定します。

1. **ツール**／**クラウドサービス**／**データソース**&#x200B;に移動します。

1. 設定コンテナを選択し、**作成**&#x200B;を選択します。

1. 「**一般**」タブで、設定に「**名前**」を入力します（例：`restTest`）。 すべての環境で&#x200B;*same*&#x200B;の名前を使用して、プロモーション後にフォームが一貫して解決されるようにします。

1. 「**認証設定**」タブで、次の設定を行います。

   * **RESTful サービス**&#x200B;を選択：**サービスエンドポイント**。
   * **メソッドの種類**: **投稿**。
   * **サービス エンドポイント URL**: ステージング エンドポイント URL （ステージングからの送信をテストするために使用するWebhook URLなど）。
   * **コンテンツタイプ**：例：**複数部品フォームデータ**。
   * **認証タイプ**: エンドポイントで必要とされる場合（例：**なし**&#x200B;または&#x200B;**基本認証**）。

1. 「**保存して閉じる**」を選択します。

## アダプティブフォームを設定コンテナにポイントします {#set-configuration-container}

>[!VIDEO](https://video.tv.adobe.com/v/3492384)

ステージング時に、フォームをREST設定を保持する設定コンテナに関連付けます。

1. **Formsとドキュメント**&#x200B;で、アダプティブフォームを選択し、**プロパティ**&#x200B;を開きます。

1. 「**基本**」タブで、**設定コンテナ**&#x200B;を、RESTful サービス設定を保持するコンテナ（`/conf/restConfigTest`など）に設定します。

1. 「**保存して閉じる**」を選択します。

## REST エンドポイントに送信アクションの設定 {#configure-submit-action}

>[!VIDEO](https://video.tv.adobe.com/v/3492385)

ステージング時に、ハードコードされたURLではなく、名前付きREST設定を使用して送信するフォームを設定します。 完全な送信アクションのリファレンスについては、[REST エンドポイント送信アクション用のアダプティブフォームの設定](/help/forms/configure-submit-action-restpoint.md)を参照してください。

1. アダプティブフォームを編集用に開き、**ガイドコンテナ** コンポーネントを選択し、その&#x200B;**アダプティブフォームコンテナ** プロパティを開きます。

1. 「**送信**」タブを開き、**送信アクション** ドロップダウンリストから、**REST エンドポイントに送信**&#x200B;を選択します。

1. **アクション設定**&#x200B;で、**POST リクエストを有効にする**&#x200B;を選択します。

1. **オプションを選択**&#x200B;するには、**設定** （**URL**&#x200B;ではなく）を選択します。

1. リストから名前付き設定（例：`restTest`）を選択します。

1. 「**完了**」を選択します。

フォームは、固定URLではなく、名前付き設定を使用して送信エンドポイントを解決するようになりました。

## フォームをステージングから本番環境に宣伝します {#promote-across-environments}

ステージングで設定およびテストを行った後、同じフォームと設定コンテナを実稼動環境に移動します。 次のいずれかの方法を使用できます。

### オプション 1：オーサーとパッケージのアプローチ {#option-package}

>[!VIDEO](https://video.tv.adobe.com/v/3492386)

作成者が各環境でフォームと設定を直接管理する場合に使用します。

1. **ステージング** オーサーインスタンスで、フォームとその設定コンテナを含むコンテンツパッケージを[ パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)に作成します。次に例を示します。

   * `/content/dam/formsanddocuments/<your-form-path>`
   * `/content/forms/af/<your-form-path>`
   * `/conf/<your-config-container>` （`.../settings/cloudconfigs/fdm/<your-config>`を含む）

1. パッケージをダウンロードし、**本番** オーサーインスタンスにインストールします。

>[!IMPORTANT]
>
>パッケージは、ステージングから&#x200B;**サービスエンドポイント URL**&#x200B;を含め、実稼動環境に同じ設定をインストールします。 本番環境でそのステージング URLを残さないでください。 次の節で説明するように、インストール後に実稼動環境のエンドポイントを更新します。

### オプション 2：コンテキストに応じた上書きアプローチ（自動化に推奨） {#option-context-aware}

このオプションは、デプロイメント後に手動で編集することなく、エンドポイント、ユーザー名、パスワードが環境ごとに自動的に解決されるパッケージ構成を1つ使用する場合に使用します。 この方法では、Cloud Managerの環境変数を使用して、設定プロパティを上書きします。

REST設定の場合、通常、`serviceEndPoint`、`userName`、`password`のプロパティの環境変数を作成し、プロジェクトの`OsgiConfigurationOverrideProvider`設定ファイルからそれらを参照します。

完全な手順については、[ コンテキストに応じたクラウド設定](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/context-aware-fdm)を参照してください。

## 実稼動時のエンドポイント URLの更新 {#configure-endpoint-on-production}

>[!VIDEO](https://video.tv.adobe.com/v/3492387)

実稼動環境にパッケージをインストールすると、アダプティブフォームとREST設定&#x200B;**name** （例：`restTest`）がステージングと一致します。 この設定の&#x200B;**サービスエンドポイント URL**&#x200B;は、引き続きパッケージのステージングエンドポイントを指しています。 実稼動環境で設定を開き、実稼動環境のエンドポイント URLに置き換えます。

1. **本番** オーサーインスタンスで、**ツール** > **クラウドサービス** > **データソース**&#x200B;に移動します。

1. デプロイした設定コンテナ （例：`restConfigTest`）を選択し、名前付き設定（例：`restTest`）を開きます。

1. 「**認証設定**」タブで、**サービスエンドポイント URL**&#x200B;を実稼動RESTまたはWebhook エンドポイントに設定します。

1. 「**保存して閉じる**」を選択します。

テスト中に、Webhook キャプチャサービスなどのリクエストインスペクターによって環境ごとに一意のURLが提供されるため、各送信を受信するエンドポイントを確認できます。

## ルーティングの確認 {#verify}

>[!VIDEO](https://video.tv.adobe.com/v/3492388)

ステージング環境と実稼動環境から同じフォームを送信し、各環境が他の環境のURLではなく、独自のエンドポイントに投稿することを確認します。

1. **ステージング**&#x200B;作成者インスタンスで、アダプティブフォームを開き、テストデータを使用して送信します（例：テキストフィールドに`stagetest`と入力します）。 POST リクエストが、ステージング時に設定した&#x200B;**ステージング** **サービスエンドポイント URL**&#x200B;に届くことを確認します。

1. **本番** オーサーインスタンスで、同じアダプティブフォームを開き、テストデータを使用して送信します（例えば、テキストフィールドに`prodtest`と入力します）。 POST リクエストが、ステージング URLではなく、実稼動環境で設定した&#x200B;**実稼動** **サービスエンドポイント URL**&#x200B;に届くことを確認します。

1. 各リクエストが想定されるコンテンツタイプ（例：**複数部品フォームデータ**）を使用し、送信されたフォームデータを含んでいることを確認します。 本番環境では、実際のセキュアエンドポイント（HTTPS）を使用します。

## ベストプラクティス {#best-practices}

* すべての環境で同じ設定&#x200B;**name**&#x200B;を使用して、プロモーション後にフォームが一貫して解決されるようにします。
* エンドポイント **value**&#x200B;は環境固有のままにします。 フォームの送信アクションに単一の環境のURLをハードコーディングしないでください。
* 実稼動エンドポイントの場合は、URLがセキュア（HTTPS）であり、受信パスが認証モデルに応じてPOST リクエストを適切に処理するように設定されていることを確認します。
* デプロイメントを繰り返し可能にし、デプロイメント後に手動で編集する必要がない場合は、コンテクストに応じた上書きアプローチを選択します。

## 関連記事 {#related-articles}

* [REST エンドポイントへの送信アクションのアダプティブフォームの設定](/help/forms/configure-submit-action-restpoint.md)
* [データソースの設定](/help/forms/configure-data-sources.md)
* [コンテキスト対応のクラウド設定](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/context-aware-fdm)
* [アダプティブフォーム送信アクション](/help/forms/aem-forms-submit-action.md)

