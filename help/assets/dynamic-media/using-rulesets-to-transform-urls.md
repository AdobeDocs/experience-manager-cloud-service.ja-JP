---
title: ルールセットを使用した URL の変換
description: Dynamic Media でルールセットをデプロイして、URL を変換する方法を説明します。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 75%

---

# ルールセットを使用した URL の変換 {#using-rulesets-to-transform-urls}

Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。各ルールは、1 つ以上の条件と 1 つ以上のアクションで構成されます。ルールは XML データを条件に対して評価し、条件を満たしている場合は適切なアクションを実行します。ルールセットの例としては、次のようなものがあります。

* MIME タイプのサフィックスの付加。多くのサービスや Web サイトでは、`.jpg` を URL に付加するなど、画像のサフィックスが必要です。
* SEO（検索エンジン最適化）のための URL へのフォルダーパスの作成。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* SEO（検索エンジン最適化）のための URL へのメタデータの付加。

   「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* ダウンロードを開始するためのコンテンツ処理方法の設定。
* パーソナライゼーションのための画像サービングテンプレーティング URL の簡略化。例えば、`rgb{XX,YY,ZZ}` を RTF 対応の `\redXX\greenYY\blueZZ` に変換します。

* `$`、`{`、`}` などの特定の文字のエンコードと、ImageServer への特定の文字のデコードのリクエスト。例えば、Facebook は特殊文字を含む URL では正しく機能しません。

   [URL から特殊文字を削除する ](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html) を参照してください。

Dynamic Media のコンテキストで、XML ベースのシステムを使用してアセット情報を管理する Web サイトは、XML ファイルを Dynamic Media にアップロードできます。これらのファイルのいずれかを、Dynamic Media のアセットを処理するための前処理ルールセットファイルとして指定できます。このファイルは、Dynamic Media と統合するシステムの会社ロジックを満たすよう、標準 URL プロトコル形式を再構成します。XML ファイルをルールセット定義ファイルのパスとして指定します。

>[!CAUTION]
>
>ルールセットを使用する場合は、Dynamic Media のコンテンツが Web サイトに表示されなくなる可能性があるので、注意してください。

独自のルールセットの作成に役立つサンプルルールセットを利用できます。
[ルールセットのリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html?lang=ja)を参照してください。

すべてのルールセットの作成と同様に、xmlvalid などの XML バリデータープログラムを使用して、XML ファイルが有効であることを確認してからアップロードしてください。[ ルールセットのトラブルシューティング ](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html) も参照してください。

また、最初は実稼動環境に影響を与えないステージング環境でルールセットをテストしてください。通常、実稼動環境とステージング環境では異なるログイン情報が必要となります。

ログイン情報については、[Adobe Dynamic Media Classicデスクトップアプリケーション ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#sign-in-dmc-app) を参照してください。

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

[ルールセットでの &#39;is&#39; イメージに代わる &#39;asset&#39; の使用](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)も参照してください。

## XML ルールセットのデプロイ {#deploy-xml-rule-sets}

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、カスタマーサポートにお問い合わせください。

1. 次の手順を実行して、ルールセットファイルをアップロードします。

   * グローバルナビゲーションバーで、「**[!UICONTROL アップロード]**」を選択します。
   * **[!UICONTROL アップロード]** ページの左上隅付近で、「**[!UICONTROL 参照]**」を選択します。
   * **[!UICONTROL 開く]**&#x200B;ダイアログボックスで、ルールセットファイル（XML）を参照します。
   * ファイルを選択し、「**[!UICONTROL 開く]**」を選択します。
   * **[!UICONTROL アップロード]**&#x200B;ページの右側で、ルールセットファイルの公開先フォルダーを選択します。
   * ページ下部付近の「アップロード後に公開」が選択されていることを確認します。
   * ページの右下隅で、「**[!UICONTROL アップロードを送信]**」を選択します。
   * グローバルナビゲーションバーで、「**[!UICONTROL ジョブ]**」を選択して、アップロードジョブのステータスを確認します。 **[!UICONTROL ジョブ]**&#x200B;ページの「**[!UICONTROL ステータス]**」列に「アップロード完了」と表示されたら、次のステップに進みます。

1. ページの上付近にあるナビゲーションバーで、**[!UICONTROL 設定]** / **[!UICONTROL アプリケーション設定]** / **[!UICONTROL 公開設定]** / **[!UICONTROL Image Server]** に移動します。
1. **[!UICONTROL Image Server 公開]** ページの「**[!UICONTROL カタログ管理]**」グループで、「**[!UICONTROL ルールセット定義ファイルのパス]**」を探し、「**[!UICONTROL 選択]**」を選択します。
1. **[!UICONTROL ルールセット定義ファイル (XML)]** を選択ページでルールセットファイルを参照し、ページ右下隅の「**** を選択します。
1. 設定ページの右下隅で、「**[!UICONTROL 閉じる]**」を選択します。
1. Image Server 公開ジョブを実行します。

   ルールセットの条件が現在の Dynamic Media の Image Server へのリクエストに適用されます。

   ルールセットファイルを変更した場合、変更したルールセットファイルを再アップロードして再公開すると、変更内容が直ちに適用されます。
