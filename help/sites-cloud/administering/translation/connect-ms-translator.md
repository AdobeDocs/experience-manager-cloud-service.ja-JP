---
title: Microsoft Translator への接続
description: AEMをMicrosoft Translatorに接続して、すぐに使用できる状態で翻訳ワークフローを自動化する方法を説明します。
feature: 言語コピー
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 36%

---


# Microsoft Translator への接続 {#connecting-to-microsoft-translator}

AEMページのコンテンツやアセットの翻訳にMicrosoft Translationアカウントを使用するための[Microsoft Translator](https://hub.microsofttranslator.com)クラウドサービスの設定を作成します。

>[!NOTE]
>
>AEMは、月に最大2,000,000文字の無料翻訳文字を使用できる試用版のMicrosoft翻訳アカウントを提供しています。 実稼働システムに適したアカウント購読を入手するには、[『Microsoft Translator体験版ライセンス設定のアップグレード](#upgrading-the-microsoft-translator-trial-license-configuration)』を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合、翻訳済みテキストの横に表示されるアトリビューション（例：`Translations by Microsoft`） |
| ワークスペース ID | （オプション）使用するカスタマイズされたMicrosoft TranslatorエンジンのID |
| サブスクリプションキー | Microsoft TranslatorのMicrosoft購読キー |

設定を作成したら、[アクティブ化](#activating-the-translator-service-configurations)する必要があります。

次の手順では、Microsoft Translatorの設定を作成します。

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)「**ツール** -> **Cloud Services** -> **翻訳Cloud Services**」をクリックまたはタップします。
1. 設定を作成する場所に移動します。 通常は、これはサイトのルートにあります。また、グローバルでデフォルトの設定にすることもできます。
1. 「**作成**」ボタンをタップまたはクリックします。
1. 設定を定義します。
   1. ドロップダウンで[**Microsoft Translator**]を選択します。
   1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。
   1. オプションとして、設定を格納するリポジトリノードに使用する名前を入力します。

   ![翻訳設定の作成](../assets/create-translation-config.png)

1. 「**作成**」をクリックします。
1. **設定を編集**&#x200B;ウィンドウで、前の表で説明した変換サービスの値を指定します。

   ![翻訳設定の編集](../assets/edit-translation-config.png)

1. 「**接続**」をタップまたはクリックして接続を確認します。
1. 「**保存して閉じる**」をタップまたはクリックします。

## Microsoft Translator 試用版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation の設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得する場合に役立つ、Microsoft Web サイトへのリンクが表示されます。

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)**ツール** -> **Cloud Services** -> **翻訳Cloud Services**&#x200B;をタップまたはクリックします。
1. 既存のMicrosoft Translator設定をタップまたはクリックします。
1. 「**編集**」をタップまたはクリックします。
1. **設定を編集**&#x200B;ウィンドウで、**アップグレード購読**&#x200B;をタップまたはクリックします。 サービスの詳細を含むMicrosoftのWebページが開きます。

## Microsoft Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft Translation の設定ページには、Microsoft Translator エンジンをカスタマイズする場合に役立つ、Microsoft Web サイトへのリンクが表示されます

1. [ナビゲーションパネルで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)**ツール** -> **Cloud Services** -> **翻訳Cloud Services**&#x200B;をタップまたはクリックします。
1. 既存のMicrosoft Translator設定をタップまたはクリックします。
1. 「**編集**」をタップまたはクリックします。
1. **設定を編集**&#x200B;ウィンドウで、**Translatorをカスタマイズ**&#x200B;をタップまたはクリックします。 表示された Microsoft の Web ページを使用して、サービスをカスタマイズします。

## 翻訳サービス設定のアクティベート  {#activating-the-translator-service-configurations}

パブリッシュインスタンスでレプリケーションされる翻訳コンテンツをサポートするには、クラウドサービス設定をアクティベートする必要があります。[ツリー](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree)を発行する方法を使用して、Microsoft Translatorの設定を保存するリポジトリノードをアクティブにします。 このノードは以下に示す親ノードの下にあります。

* `/libs/settings/cloudconfigs/translation/msft-translation`
