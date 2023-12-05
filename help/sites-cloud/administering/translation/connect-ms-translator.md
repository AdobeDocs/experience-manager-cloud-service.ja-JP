---
title: Microsoft Translator への接続
description: AEM を Microsoft Translator に接続して翻訳ワークフローを自動化する方法を説明します。
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 81%

---

# Microsoft Translator への接続 {#connecting-to-microsoft-translator}

AEM ページのコンテンツまたはアセットの翻訳に Microsoft Translation アカウントを使用するには、[Microsoft Translator](https://www.microsoft.com/ja-jp/translator/business/) クラウドサービスの設定を作成します。

>[!TIP]
>
>コンテンツの翻訳を初めて行う場合は、[AEM Sites 翻訳ジャーニー](/help/journey-sites/translation/overview.md)を参照してください。これは、AEM の強力な翻訳ツールを使用して AEM Sites コンテンツを翻訳する手順を示すガイドです。AEM や翻訳の経験がないユーザーに最適です。

>[!NOTE]
>
>AEM には、毎月最大 2,000,000 文字の無料翻訳を利用できる体験版の Microsoft Translation アカウントが用意されています。実稼動システムに適したアカウントサブスクリプションを取得するには、[Microsoft Translator 体験版ライセンス設定のアップグレード](#upgrading-the-microsoft-translator-trial-license-configuration)を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合、翻訳されたテキストの横に表示されるアトリビューション。例： `Translations by Microsoft` |
| ワークスペース ID | （オプション）使用するカスタム Microsoft Translator エンジンの ID |
| サブスクリプションキー | Microsoft Translator の Microsoft サブスクリプションキー |

設定を作成したら、その[設定をアクティベートする](#activating-the-translator-service-configurations)必要があります。

Microsoft Translator 設定を作成するには、次の手順に従います。

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 選択 **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 設定を作成する場所に移動します。 通常は、これはサイトのルートにあります。また、グローバルなデフォルト設定にすることもできます。
1. 「**作成**」ボタンを選択します。
1. 設定を定義します。
   1. ドロップダウンで **Microsoft Translator** を選択します。
   1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。
   1. オプションとして、設定を格納するリポジトリーノードに使用する名前を入力します。

   ![翻訳設定の作成](../assets/create-translation-config.png)

1. 「**作成**」をクリックします。
1. **設定を編集**&#x200B;ウィンドウで、前述の表で説明した翻訳サービスの値を指定します。

   ![翻訳設定の編集](../assets/edit-translation-config.png)

1. 選択 **接続** 接続を確認します。
1. 「**保存して閉じる**」を選択します。

## Microsoft Translator 体験版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得する場合に役立つ、Microsoft web サイトへのリンクが表示されます。

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 選択 **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 既存のMicrosoft Translator 設定を選択します。
1. 「**編集**」を選択します。
1. Adobe Analytics の **設定を編集** ウィンドウ、「 」を選択します。 **配信登録のアップグレード**. サービスの詳細を表示する Microsoft Web ページが開きます。

## Microsoft Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft Translation 設定ページには、Microsoft Translator エンジンをカスタマイズする場合に役立つ、Microsoft Web サイトへのリンクが表示されます

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 選択 **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 既存のMicrosoft Translator 設定を選択します。
1. 「**編集**」を選択します。
1. Adobe Analytics の **設定を編集** ウィンドウ、「 」を選択します。 **Translator をカスタマイズ**. 表示された Microsoft の web ページを使用して、サービスをカスタマイズします。

## Translator サービス設定のアクティベート {#activating-the-translator-service-configurations}

パブリッシュインスタンスでレプリケートされる翻訳コンテンツをサポートするには、クラウドサービス設定をアクティベートする必要があります。[ツリーの公開](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree)方法を使用して、Microsoft Translator 設定を格納するリポジトリーノードをアクティベートします。このノードは以下に示す親ノードの下にあります。

* `/libs/settings/cloudconfigs/translation/msft-translation`
