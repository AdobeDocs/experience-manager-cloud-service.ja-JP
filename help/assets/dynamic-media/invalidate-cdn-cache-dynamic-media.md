---
title: ダイナミックメディアを使用したCDNキャッシュの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
translation-type: tm+mt
source-git-commit: 262867ff19c373905b71b9099d1062705cfbf9cf
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 4%

---


# ダイナミックメディアを使用したCDNキャッシュの無効化 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Mediaアセットは、顧客との配信を高速化するために、CDN(コンテンツ配信ネットワーク)によってキャッシュされます。 ただし、これらのアセットを更新する場合は、その変更をWebサイトに即座に反映させることができます。 CDNキャッシュの削除または無効化を行うと、ダイナミックメディアによって配信されるアセットをすばやく更新できます。 TTL(Time To Live)値（デフォルトは10時間）を使用してキャッシュの有効期限が切れるのを待つ代わりに、ダイナミックメディアユーザーインターフェイスから要求を送信し、キャッシュの有効期限を数分で設定できます。

>[!IMPORTANT]
>
>次の手順は、Cloud ServiceとしてAEM上のダイナミックメディアにのみ適用されます。 また、この機能を使用するには、AEMダイナミックメディアに組み込まれている標準搭載のCDNを使用する必要があります。その他のカスタムCDNはサポートされていません。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

ダイナミックメディアの [キャッシュの概要も参照してください](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**ダイナミックメディアを使用してCDNキャッシュを無効にするには**

*パート1/2:CDN無効化テンプレートの作成*

1. AEMで、Cloud Serviceとして **[!UICONTROL ツール/アセット/CDN無効化テンプレートをタップします。]**

   ![CDN検証機能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 「 **[!UICONTROL CDN無効化テンプレート]** 」ページで、シナリオに応じて次のいずれかのオプションを実行します。

   | シナリオ | オプション |
   | --- | --- |
   | Dynamic Media Classicを使用して、以前にCDN無効化テンプレートを作成したことがあります。 | 「テンプレート **[!UICONTROL を作成]** 」テキストフィールドには、テンプレートデータが事前に入力されています。 この場合は、テンプレートを編集するか、次の手順に進むことができます。 |
   | テンプレートを作成する必要があります。 何を入れる？ | 「テンプレート **[!UICONTROL を作成]** 」テキストフィールドに、特定の画像IDではなく、を参照する画像URL（画像プリセットまたは修飾子を含む）を入力します。 `<ID>`テンプレートに単一の画像が含まれる場合<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>`<ID>``https://<publishserver_name>/is/image/<company_name>/<ID>``<publishserver_name>` 、はDynamic Media Classicの「一般設定」で定義されているPublish Serverの名前です。は、こ `<company_name>` のAEMインスタンスに関連付けられている会社ルートの名前で、無効にするアセット選択 `<ID>` を介して選択されたアセットです。<br>プリセット/修飾子の投稿 `<ID>` は、そのままURL定義内にコピーされます。<br>テンプレートに基づいて自動形成で `/is/image`きるのは、画像のみです。<br>例え `/is/content/`ば、アセットピッカーを使用してビデオやPDFなどのアセットを追加しても、URLが自動生成されません。 代わりに、CDN無効化テンプレートでそのようなアセットを指定するか、 *パート2/2でURLを手動で追加する必要があります。CDN無効化オプションの設定を参照*。<br>**例：最初**<br>&#x200B;の例では、無効化テンプレートに、が含まれ `<ID>` るアセットURLが含まれ `/is/content`ます。 例えば、`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>` のようになります。ダイナミックメディアは、これに基づいてURLをフォームし、無効にするアセットピッカー `<ID>` を使用して選択されたアセットとなります。<br>この2つ目の例では、無効化テンプレートに、Webプロパティで使用されるアセットの完全なURLが含まれます(アセット選択に依存し `/is/content` ません)。 例えば、 `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` backpackはアセットIDです。<br>ダイナミックメディアでサポートされているアセット形式は、無効化の対象となります。 CDNの無効化で *サポートされないアセットファイルタイプには* 、Postscript、Encapsulated Postscript、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word、リッチテキスト形式があります。<br>テンプレートを作成する際は、構文と入力ミスに注意する必要があります。ダイナミックメディアでは、テンプレートの検証は行われません。<br>画像スマートトリミングのURLは、このCDN無効化テンプレートまたは **[!UICONTROL パート2の「]** 追加URL *」テキストフィールドのいずれかで指定する必要があります。CDN無効化オプションの設定を参照してください。*<br>**重要：**CDN無効化テンプレートの各エントリは、それぞれ別の行に存在する必要があります。<br>*次のテンプレートの例は、説明用です。* |

   ![CDN無効化テンプレート — 作成](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 「 **[!UICONTROL CDN無効化テンプレート]** 」ページの右上隅にある「 **[!UICONTROL 保存]**」をタップし、「 **[!UICONTROL OK」をタップします。]**<br>   *パート2/2:CDN無効化オプションの設定*
   <br>

1. AEMで、Cloud Serviceとして **[!UICONTROL ツール/アセット/CDNの無効化をタップします。]**

   ![CDN検証機能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 「 **[!UICONTROL CDN無効化]** - **[!UICONTROL 追加詳細]** 」ページで、CDN無効化のアセットを選択します。

   ![CDNの無効化 —追加詳細](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >「CDN内のアセットに関連付けられた画像プリセットを **[!UICONTROL 無効にする]** 」 *および「テンプレートに基づいて無効にする***** 」をオフにしたままにすると、選択したアセットのベースURLが無効に設定されます。 このオプションは、画像に対してのみ使用してください。


   | オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL CDN でアセット関連の画像プリセットを無効化します]** | （オプション）このオプションを選択すると、選択したアセットとそれに関連するすべての画像プリセットURLが、キャッシュの無効化のために自動形成されます。<br>アセットと、それに関連付けられた事前定義のプリセットURLは、無効化のために自動形成されます。 このオプションは、画像アセットに対してのみ機能します。 |
   | **[!UICONTROL テンプレートに基づく無効化]** | （オプション）URL生成に定義済みのテンプレートのみを使用する場合は、このオプションを選択します。 |
   | **[!UICONTROL アセットを追加]** | アセット選択を使用して、無効にするアセットを選択します。 公開済みまたは非公開のアセットを選択できます。<br>CDNでのキャッシュは、アセットベースではなくURLベースです。 したがって、Webサイト上の完全なURLを認識する必要があります。 これらのURLを決定したら、それらをテンプレートに追加できます。 その後、これらのアセットを選択して追加し、URLを無効にする作業を1回で行うことができます。 <br>このオプションは、CDNのアセットに関連付けられた画像プリセットを **[!UICONTROL 無効にする、またはテンプレートに基づく]**&#x200B;無効化 ****、あるいはその両方と組み合わせて使用します。 |
   | **[!UICONTROL URL を追加]** | CDNキャッシュを無効にするダイナミックメディアアセットに、完全なURLパスを手動で追加または貼り付けます。 パート1でCDN無効化テンプレートを作成しなかった場合は、このオプションを使用し ***ます。CDN無効化テンプレートの操作***。無効にするアセットは数個だけです。<br>**重要：** 追加する各URLは、それぞれ別の行に記述する必要があります。<br>一度に1,000個までのURLを無効にできます。 「 **[!UICONTROL 追加URL]** 」テキストフィールドのURL数が1000を超える場合、「 **[!UICONTROL 次へ]**」をタップできません。 このような場合、選択したアセットの右側の **[!UICONTROL X]** をタップするか、手動で追加したURLをタップして、アセットを無効化リストから削除する必要があります。<br>画像スマートトリミングのURLは、CDN無効化テンプレートまたはこの **[!UICONTROL 追加URL]** テキストフィールドのいずれかで指定する必要があります。 |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. **[!UICONTROL CDN無効化]** - **[!UICONTROL 確認]** ページの「URL **** リスト」ボックスに、前の手順で作成したCDN無効化テンプレートから生成された1つ以上のURLと、先ほど追加したアセットのリストが表示されます。

   例えば、前の手順で示したCDN無効化テンプレートの例を使用して、という名前のアセットを1つ追加したとし `spinset`ます。 **[!UICONTROL ツール/アセット/CDNの無効化をタップすると]** 、 **[!UICONTROL CDNの無効化 — 確認]** ユーザーインターフェイスで以下の5つの生成されたURLが生成されます。

   ![CDNの無効化 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   必要に応じて、URLの右側の **X** をタップして、URLを無効化プロセスから削除します。

1. ページの右上隅近くにある「 **[!UICONTROL 送信]** 」をタップして、CDN無効化プロセスを開始します。

## CDN無効化エラーのトラブルシューティング

いずれの場合も、バッチ全体が無効化のために処理されるか、バッチ全体が失敗します。

| エラー | 説明 |
| --- | --- |
| *選択されたアセットのURLを取得できませんでした。* | 次のいずれかのシナリオが満たされた場合に発生します。<br>— ダイナミックメディア設定が見つかりません。<br>— ダイナミックメディア設定の読み取りに使用するサービスユーザーの取得中に例外が発生しました。<br>- URLの形成に使用する発行サーバまたは会社ルートがダイナミックメディアの設定にありません。 |
| *一部のURLが正しく定義されていません。 訂正して再送信してください。* | IPS CDNキャッシュ無効化APIが、URLが別の会社を参照しているというエラーを返す場合、またはIPS cdnCacheInvalidation APIが実行した検証に従ってURLが有効でない場合に発生します。 |
| *CDNキャッシュを無効にできませんでした。* | CDNキャッシュの無効化要求が他の理由で失敗した場合に発生します。 |
| *無効にするURLが入力されていません。* | CDN無効化 **[!UICONTROL -]** 確認 **[!UICONTROL ページにURLが存在せず、「]****[!UICONTROL 送信」をタップした場合に発生します。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
