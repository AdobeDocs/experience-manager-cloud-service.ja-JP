---
title: Dynamic Mediaを使用したCDN（コンテンツ配信ネットワーク）キャッシュの無効化
description: 「CDN（コンテンツ配信ネットワーク）にキャッシュされたコンテンツを無効にして、Dynamic Mediaから配信されるアセットをすばやく更新する方法を説明します。キャッシュの期限が切れるのを待つ必要はありません。」
feature: アセット管理
role: Administrator,Business Practitioner
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 57%

---

# Dynamic Media を使用した CDN キャッシュの無効化 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media アセットは、顧客との配信を高速化するために、CDN（コンテンツ配信ネットワーク）によってキャッシュされます。ただし、これらのアセットを更新する場合は、その変更をWebサイトで直ちに有効にする必要があります。 CDN キャッシュの削除または無効化をおこなうと、Dynamic Media によって配信されるアセットをすばやく更新できます。TTL(Time To Live)値（デフォルトは10時間）を使用して、キャッシュの有効期限が切れるのを待つ必要がなくなりました。 代わりに、Dynamic Mediaユーザーインターフェイス内からリクエストを送信して、キャッシュの有効期限を数分で切れます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。 その他のカスタムCDNは、この機能ではサポートされません。

[Dynamic Media のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**Dynamic Media を使用して CDN キャッシュを無効にするには:**

*パート 1 / 2：CDN 無効化テンプレートの作成*

1. Adobe Experience Manager as aCloud Serviceで、**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL CDN無効化テンプレート]**&#x200B;をタップします。

   ![CDN 検証機能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. **[!UICONTROL CDN 無効化テンプレート]**&#x200B;ページで、シナリオに応じて次のいずれかのオプションを実行します。

   | シナリオ | オプション |
   | --- | --- |
   | Dynamic Media Classic を使用して、以前に CDN 無効化テンプレートを作成したことがある。 | 「**[!UICONTROL テンプレートを作成]**」テキストフィールドに、テンプレートデータが事前に入力されています。この場合は、テンプレートを編集するか、続行して次の手順に進みます。 |
   | テンプレートを作成する必要があります。 入力する値 | 「**[!UICONTROL テンプレートを作成]**」テキストフィールドに、特定の画像IDではなく`<ID>`を参照する画像URL（画像プリセットまたは修飾子を含む）を入力します。<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>テンプレートに`<ID>`が含まれる場合は、`https://<publishserver_name>/is/image/<company_name>/<ID>`に入力します。`<publishserver_name>`はDynamic Media Classicの一般設定。 `<company_name>`は、このExperience Managerインスタンスに関連付けられている会社のルートの名前で、`<ID>`は、無効化するアセットピッカーを使用して選択されたアセットです。<br>その後に続くプリセット/ `<ID>` 修飾子は、そのままURL定義にコピーされます。<br>テンプレートに基づいて自動形成できるのは画像のみ、すなわち `/is/image` のみです。<br>`/is/content/` の場合、アセットピッカーを使用してビデオや PDF などのアセットを追加しても、URL は自動生成されません。代わりに、CDN 無効化テンプレートでそのようなアセットを指定するか、*パート 2 / 2 CDN 無効化オプションの設定*&#x200B;で、URL を手動で追加する必要があります。<br>**例：**<br>&#x200B;最初の例では、無効化テンプレートに `<ID>` と、`/is/content` を持つアセット URL が含まれます。例えば、`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>` のようになります。Dynamic Mediaは、このパスに基づいてURLを形成します。`<ID>`は、アセットピッカーを使用して選択された、無効化するアセットです。<br>2 つ目の例では、無効化テンプレートに、`/is/content` が用いられ、Web プロパティで使用されるアセットの完全な URL が含まれます（アセットピッカーに依存しません）。例えば、`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` の backpack はアセット ID です。<br>Dynamic Media でサポートされているアセット形式は、無効化の対象となります。CDNの無効化で&#x200B;*サポートされていない*&#x200B;アセットファイルタイプには、PostScript®、Encapsulated PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft® Powerpoint、Microsoft® Excel、Microsoft® Wordおよびリッチテキスト形式が含まれます。<br>テンプレートを作成する際は、構文と入力ミスに注意する必要があります。Dynamic Media では、テンプレートの検証はおこなわれません。<br>画像スマートトリミングのURLは、このCDN無効化テンプレート、またはパート2の「 URLを追 **[!UICONTROL 加」テキ]** ストフィールドのい *ずれかで指定します。CDN無効化オプションの設定。*<br>**重要：** CDN 無効化テンプレートの各エントリは、それぞれ別の行にする必要があります。<br>*次のテンプレートの例は、説明の目的でのみ使用します。* |

   ![CDN 無効化テンプレート - 作成](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. **[!UICONTROL CDN無効化テンプレート]**&#x200B;ページの右上隅にある「**[!UICONTROL 保存]**」をタップし、「**[!UICONTROL OK]**」をタップします。<br>

   *パート 2 / 2：CDN 無効化オプションの設定*
   <br>

1. Experience Managerで、Cloud Serviceとして&#x200B;**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL CDN無効化]**&#x200B;をタップします。

   ![CDN 検証機能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. **[!UICONTROL CDN 無効化]** - **[!UICONTROL 追加詳細]**&#x200B;ページで、CDN を無効化にするアセットを選択します。

   ![CDN 無効化 - 追加詳細](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >「**[!UICONTROL CDN でアセット関連の画像プリセットを無効にする]**」*および*「**[!UICONTROL テンプレートに基づいて無効にする]**」をオフにしたままにすると、選択したアセットのベース URL が無効に設定されます。このオプションは、画像に対してのみ使用します。


   | オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL CDN でアセット関連の画像プリセットを無効化する]** | （オプション）このオプションを選択すると、選択したアセットとそれに関連するすべての画像プリセット URL が、キャッシュの無効化のために自動作成されます。<br>アセットと、それに関連付けられた事前定義のプリセット URL は、無効化のために自動作成されます。このオプションは、画像アセットに対してのみ機能します。 |
   | **[!UICONTROL テンプレートに基づいて無効化]** | （オプション）URL 作成に定義済みのテンプレートのみを使用する場合は、このオプションを選択します。 |
   | **[!UICONTROL アセットを追加]** | アセットピッカーを使用して、無効にするアセットを選択します。公開済みまたは非公開のアセットを選択できます。<br>CDN でのキャッシュは、アセットベースではなく URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。これらの URL を決定したら、テンプレートに追加できます。それから、アセットを選択して追加し、ワンステップで URL を無効にできます。<br>このオプションは、「CDNでアセ **[!UICONTROL ット関連の画像プリセットを無効にする」、「テンプレートに基づいて無効化」]**、またはその両方で使用します。 **** |
   | **[!UICONTROL URL を追加]** | CDN キャッシュを無効にする Dynamic Media セットに、完全な URL パスを手動で追加または貼り付けます。***パート 1 / 2：CDN 無効化テンプレートの作成***&#x200B;で CDN 無効化テンプレートを作成しておらず、無効にするアセットが数個の場合にこのオプションを使用します。<br>**重要：**&#x200B;追加する各 URL は、それぞれ別の行に記述する必要があります。<br>一度に 1000 個までの URL を無効にできます。「**[!UICONTROL URL を追加]**」テキストフィールドの URL 数が 1000 を超える場合、「**[!UICONTROL 次へ]**」をタップできません。その場合、選択したアセットの右側の **[!UICONTROL X]** をタップするか、手動で追加した URL をタップして、アセットを無効化リストから削除する必要があります。<br>画像スマート切り抜きのURLは、CDN無効化テンプレートまたはこのURLを追加テキストフィー **[!UICONTROL ルド]** で指定します。 |

1. ページの右上隅付近にある「**[!UICONTROL 次へ]**」をタップします。
1. **[!UICONTROL CDN無効化]** - **[!UICONTROL 確認]**&#x200B;ページの&#x200B;**[!UICONTROL URL]**&#x200B;リストボックスに、前に作成したCDN無効化テンプレートから生成された1つ以上のURLと、先ほど追加したアセットのリストが表示されます。

   例えば、前の手順で示した CDN 無効化テンプレートの例を使用して、`spinset` という名前のアセットを 1 つ追加したとします。**[!UICONTROL ツール/アセット/CDN無効化]**&#x200B;をタップすると、**[!UICONTROL CDN無効化 — 確認]**&#x200B;ユーザーインターフェイスで次の5つのURLが生成されます。

   ![CDN 無効化 - 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   必要に応じて、URL の右側の **X** をタップして、URL を無効化プロセスから削除します。

1. ページの右上隅近くにある「**[!UICONTROL 送信]**」をタップして、CDN 無効化プロセスを開始します。

## CDN 無効化エラーのトラブルシューティング

いずれの場合も、無効にするバッチ全体が処理されるか、バッチ全体が失敗します。

| エラー | 説明 |
| --- | --- |
| *選択されたアセットのURLを取得できませんでした。* | 次のいずれかのシナリオが満たされた場合に発生します：<br> - Dynamic Media 設定が見つかりません。<br>- Dynamic Media設定の読み取りに使用するサービスユーザーの取得中に例外が発生しました。<br> - URL の形成に使用するパブリッシュサーバーまたは会社ルートが Dynamic Media の設定にありません。 |
| *一部の URL が正しく定義されていません。修正して再送信します。* | IPS CDNキャッシュ無効化APIがエラーを返した場合に発生します。 エラーは、URLが別の会社を参照していること、またはIPS cdnCacheInvalidation APIが実行した検証に従ってURLが無効であることを示します。 |
| *CDN キャッシュを無効にできませんでした。* | CDN キャッシュの無効化リクエストがその他の理由で失敗した場合に発生します。 |
| *無効にするURLが入力されていません。* | **[!UICONTROL CDN無効化]** - **[!UICONTROL 確認]**&#x200B;ページにURLが存在せず、**[!UICONTROL 送信]**&#x200B;をタップした場合に発生します。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
