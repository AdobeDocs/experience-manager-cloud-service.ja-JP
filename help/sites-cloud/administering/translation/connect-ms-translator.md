---
title: Microsoft Translator への接続
description: 標準搭載のAEMをMicrosoft Translatorに接続して、翻訳ワークフローを自動化する方法を説明します。
feature: 言語コピー
role: Administrator
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 36%

---

# Microsoft Translator への接続 {#connecting-to-microsoft-translator}

AEMページのコンテンツやアセットの翻訳にMicrosoft Translationアカウントを使用するために、[Microsoft Translator](https://hub.microsofttranslator.com)クラウドサービスの設定を作成します。

>[!NOTE]
>
>AEMは、1ヶ月に最大2,000,000文字の無料翻訳文字を使用できるMicrosoft翻訳の体験版アカウントを提供しています。 実稼動システムに適したアカウントサブスクリプションを入手するには、「[Microsoft Translator試用版ライセンス設定のアップグレード](#upgrading-the-microsoft-translator-trial-license-configuration)」を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合、翻訳済みテキストの横に表示されるアトリビューション（例：`Translations by Microsoft`） |
| ワークスペース ID | （オプション）使用するカスタマイズ済みのMicrosoft TranslatorエンジンのID |
| サブスクリプションキー | Microsoft TranslatorのMicrosoftサブスクリプションキー |

設定を作成したら、[有効化](#activating-the-translator-service-configurations)する必要があります。

次の手順では、Microsoft Translatorの設定を作成します。

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)**ツール** -> **Cloud Services** -> **翻訳Cloud Services**&#x200B;をクリックまたはタップします。
1. 設定を作成する場所に移動します。 通常、これはサイトのルートにあるか、グローバルなデフォルト設定にすることができます。
1. 「**作成**」ボタンをタップまたはクリックします。
1. 設定を定義します。
   1. ドロップダウンで「**Microsoft Translator**」を選択します。
   1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。
   1. オプションとして、設定を格納するリポジトリノードに使用する名前を入力します。

   ![翻訳設定の作成](../assets/create-translation-config.png)

1. 「**作成**」をクリックします。
1. **設定を編集**&#x200B;ウィンドウで、前の表で説明した翻訳サービスの値を指定します。

   ![翻訳設定の編集](../assets/edit-translation-config.png)

1. 「**接続**」をタップまたはクリックして接続を確認します。
1. 「**保存して閉じる**」をタップまたはクリックします。

## Microsoft Translator 試用版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation の設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得する場合に役立つ、Microsoft Web サイトへのリンクが表示されます。

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)**ツール** -> **Cloud Services** -> **翻訳Cloud Services**&#x200B;をタップまたはクリックします。
1. 既存のMicrosoft Translator設定をタップまたはクリックします。
1. 「**編集**」をタップまたはクリックします。
1. **設定を編集**&#x200B;ウィンドウで、「**購読をアップグレード**」をタップまたはクリックします。 サービスの詳細を示すMicrosoftのWebページが開きます。

## Microsoft Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft Translation の設定ページには、Microsoft Translator エンジンをカスタマイズする場合に役立つ、Microsoft Web サイトへのリンクが表示されます

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)**ツール** -> **Cloud Services** -> **翻訳Cloud Services**&#x200B;をタップまたはクリックします。
1. 既存のMicrosoft Translator設定をタップまたはクリックします。
1. 「**編集**」をタップまたはクリックします。
1. **設定を編集**&#x200B;ウィンドウで、「**トランスレーターをカスタマイズ**」をタップまたはクリックします。 表示された Microsoft の Web ページを使用して、サービスをカスタマイズします。

## 翻訳サービス設定のアクティベート  {#activating-the-translator-service-configurations}

パブリッシュインスタンスでレプリケーションされる翻訳コンテンツをサポートするには、クラウドサービス設定をアクティベートする必要があります。[ツリー](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree)の公開方法を使用して、Microsoft Translator設定を保存するリポジトリノードをアクティブ化します。 このノードは以下に示す親ノードの下にあります。

* `/libs/settings/cloudconfigs/translation/msft-translation`
