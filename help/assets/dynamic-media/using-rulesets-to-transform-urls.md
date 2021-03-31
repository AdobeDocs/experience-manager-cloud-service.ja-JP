---
title: ルールセットを使用した URL の変換
description: URLを変換するためにDynamic Mediaにルールセットをデプロイする方法について説明します。 ルールセットは、XMLデータを評価し、特定の条件を満たす場合に特定のアクションを実行するスクリプティング言語（JavaScript™など）で記述された一連の命令です。
topic: 業務担当者
role: 業務担当者
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 85%

---


# ルールセットを使用した URL の変換 {#using-rulesets-to-transform-urls}

Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットは、XMLデータを評価し、特定の条件を満たす場合に特定のアクションを実行するスクリプティング言語（JavaScript™など）で記述された一連の命令です。 各ルールは、1 つ以上の条件と 1 つ以上のアクションで構成されます。ルールは XML データを条件に対して評価し、条件を満たしている場合は適切なアクションを実行します。ルールセットの例としては、次のようなものがあります。

* MIME タイプのサフィックスの付加。多くのサービスや Web サイトでは、`.jpg` を URL に付加するなど、画像のサフィックスが必要です。
* SEO（検索エンジン最適化）のための URL へのフォルダーパスの作成。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* SEO（検索エンジン最適化）のための URL へのメタデータの付加。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* ダウンロードを開始するためのコンテンツ処理方法の設定。
* パーソナライゼーションのための画像サービングテンプレーティング URL の簡略化。例えば、`rgb{XX,YY,ZZ}` を RTF 対応の `\redXX\greenYY\blueZZ` に変換します。

* `$`、`{`、`}` などの特定の文字のエンコードと、ImageServer への特定の文字のデコードのリクエスト。例えば、Facebook は特殊文字を含む URL では正しく機能しません。

   [URL からの特殊文字の削除](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)を参照してください。

Dynamic Media のコンテキストで、XML ベースのシステムを使用してアセット情報を管理する Web サイトは、XML ファイルを Dynamic Media にアップロードできます。これらのファイルのいずれかを、Dynamic Media のアセットを処理するための前処理ルールセットファイルとして指定できます。このファイルは、Dynamic Media と統合するシステムのビジネスロジックを満たすよう、標準 URL プロトコル形式を再構成します。XML ファイルをルールセット定義ファイルのパスとして指定します。

>[!CAUTION]
>
>ルールセットを使用する場合は、Dynamic Media のコンテンツが Web サイトに表示されなくなる可能性があるので、注意してください。

用意されているサンプルルールセットを使用して、独自のルールセットを作成できます。[ルールセットのリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html?lang=ja)を参照してください。

すべてのルールセットの作成と同様に、xmlvalid などの XML バリデータープログラムを使用して、XML ファイルが有効であることを確認してからアップロードしてください。[ルールセットのトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)も参照してください。

また、最初は実稼動環境に影響を与えないステージング環境でルールセットをテストしてください。通常、実稼動環境とステージング環境では異なるログイン情報が必要となります。

ログイン情報については、「[Adobe Dynamic Media クラシックにサインイン](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#sign-in-dmc-app)」を参照してください。

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

[ルールセットでの &#39;is&#39; イメージに代わる &#39;asset&#39; の使用](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)も参照してください。

**XML ルールセットをデプロイするには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. 次の手順を実行して、ルールセットファイルをアップロードします。

   * グローバルナビゲーションバーの「**[!UICONTROL アップロード]**」をクリックします。
   * **[!UICONTROL アップロード]**&#x200B;ページで、左上隅付近の「**[!UICONTROL 参照]**」をクリックします。
   * **[!UICONTROL 開く]**&#x200B;ダイアログボックスで、ルールセットファイル（XML）を参照します。
   * ファイルを選択して、「**[!UICONTROL 開く]**」をクリックします。
   * **[!UICONTROL アップロード]**&#x200B;ページの右側で、ルールセットファイルの公開先フォルダーを選択します。
   * ページ下部近くにある「アップロード後に公開」がチェック済みであることを確認します。
   * ページ右下隅の「**[!UICONTROL アップロードを送信]**」をクリックします。
   * グローバルナビゲーションバーの「**[!UICONTROL ジョブ]**」をクリックして、アップロードジョブのステータスを確認します。**[!UICONTROL ジョブ]**&#x200B;ページの「**[!UICONTROL ステータス]**」列に「アップロード完了」と表示されたら、次のステップに進みます。

1. ページ上部付近のナビゲーションバーで、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。
1. **[!UICONTROL Image Server 公開]**&#x200B;ページの「**[!UICONTROL カタログ管理]**」グループで、**[!UICONTROL ルールセット定義ファイルのパス]**&#x200B;を探し、「**[!UICONTROL 選択]**」をクリックします。
1. **[!UICONTROL ルールセット定義ファイル（XML）を選択]**&#x200B;ページでルールセットファイルを参照し、ページ右下隅の「**[!UICONTROL 選択]**」をクリックします。
1. 設定ページの右下隅の「**[!UICONTROL 閉じる]**」をクリックします。
1. Image Server 公開ジョブを実行します。

   ルールセットの条件が現在の Dynamic Media の Image Server へのリクエストに適用されます。

   ルールセットファイルを変更すると、更新したルールセットファイルを再アップロードして再公開すると、変更が直ちに適用されます。

