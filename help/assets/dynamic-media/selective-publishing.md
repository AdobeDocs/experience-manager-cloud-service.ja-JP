---
title: Dynamic Media での選択的公開の操作
description: Dynamic Media での選択的公開の操作方法について説明します。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Publishing,Dynamic Media
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2946'
ht-degree: 100%

---

# Dynamic Media のフォルダーレベルでの選択的公開の設定 {#selective-publish-configure-folder}

Adobe Experience Manager または Dynamic Media との間でアセットを公開または非公開にすることができます。これは、「**[!UICONTROL 公開を管理]**」または「**[!UICONTROL クイック公開]**」を使用して、フォルダーレベルで行えます。この公開方法は、Dynamic Media インスタンス内のすべてのフォルダーに適用される **[!UICONTROL Dynamic Media 設定]**&#x200B;のみに依存してはいないので便利です。

例えば、選択的公開を使用して、まだ実行されていない製品のアセットを操作できます。その場合、マーケティングチームは Dynamic Media に同期されたスマート切り抜き画像や動的レンディションにアクセスできます。アセットをグローバル配信用に Dynamic Media に公開しなくても、販促用のマテリアルを作成できます。

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

後でフォルダー内の「**[!UICONTROL 選択的公開]**」設定を変更すると、その変更の影響を受けるのは、その時点からそのフォルダーにアップロードする新しいアセットだけです。フォルダー内の既存のアセットの公開状態は、**[!UICONTROL クイック公開]**&#x200B;または&#x200B;**[!UICONTROL 公開を管理]**&#x200B;ダイアログボックスから手動で変更するまで、そのままになります。

「**[!UICONTROL Dynamic Media 公開モード]**」フォルダーレベルのオプションでは、**[!UICONTROL Dynamic Media 設定の「]**&#x200B;アセットを&#x200B;**[!UICONTROL 公開」設定にある値が常にデフォルト値になります。]**&#x200B;ただし、このトピックの次の手順では、フォルダーレベルで手動でこのデフォルト値を変更して、**[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きする方法を示します（次の手順で説明します）。

次の項目に依存しているかどうかに関係なく、

* **[!UICONTROL Dynamic Media 設定]**&#x200B;で指定された「**[!UICONTROL アセットを公開]**」の値
* フォルダーレベルのプロパティで設定された「**[!UICONTROL Dynamic Media 公開モード]**」の値

引き続き、「**[!UICONTROL 即時]**」、「**[!UICONTROL アクティベーション時]**」、「**[!UICONTROL 選択的公開]**」のいずれかを選択できます。例えば、**[!UICONTROL Dynamic Media 設定]**&#x200B;の「**[!UICONTROL アセットを公開]**」の値を「**[!UICONTROL アクティベーション時]**」に設定できます。また、**[!UICONTROL Dynamic Media 公開]**&#x200B;モードの値をフォルダーレベルで&#x200B;**[!UICONTROL 選択的公開]**&#x200B;に設定することも、その逆に設定することなども可能です。

フォルダーで選択的公開を設定した後、次の操作を行うことができます。

* [「公開を管理」を使用して、Dynamic Media または Experience Manager にアセットを選択的に公開する](#selective-publish-manage-publication)
* [「公開を管理」を使用して、Dynamic Media または Experience Manager からアセットを選択的に非公開にする](#selective-unpublish-manage-publication)
* [「クイック公開」を使用して、Dynamic Media または Experience Manager にアセットを公開する](#quick-publish-aem-dm)
* [検索結果を使用して、アセットを選択的に公開または非公開にする](#selective-publish-unpublish-search-results)

**Dynamic Media のフォルダーレベルで選択的公開を設定するには：**

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. 次のいずれかの操作を行います。
   * 既存フォルダーのプロパティの編集 - **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、プロパティを編集するフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL プロパティ]**」を選択します。
   * 新しいフォルダーのプロパティを編集します。**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、**[!UICONTROL リスト表示]**&#x200B;の中で、ページの右上隅付近の&#x200B;**[!UICONTROL 作成]**／**[!UICONTROL フォルダー]**&#x200B;に移動します。**[!UICONTROL フォルダーの作成]**&#x200B;ダイアログボックスで、フォルダーのタイトル（必須）を入力し、「**[!UICONTROL 作成]**」を選択します。フォルダーを選択し、ツールバーで「**[!UICONTROL プロパティ]**」を選択します。

1. 「**[!UICONTROL 同期モード]**」ドロップダウンリストで、次のいずれかを選択します。

   | 同期モード | 説明 |
   | --- | --- |
   | **[!UICONTROL 継承]** | フォルダーに明示的な同期値はなく、代わりに、上位フォルダーの 1 つ、または **[!UICONTROL Dynamic Media 設定]**&#x200B;のデフォルトモードから同期値を継承します。**[!UICONTROL 継承]**&#x200B;の詳細なステータスは、ツールチップで表示されます。 |
   | **[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media に同期]** | Dynamic Media への公開を続行するには、アセットを Dynamic Media と同期する必要があります。このオプションを選択すると、このサブツリー内のすべてのアセットが Dynamic Media と同期されます。フォルダー固有の設定は、**[!UICONTROL Dynamic Media 設定]**&#x200B;のデフォルト設定よりも優先します。 |
   | **[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media との同期から除外]** | このサブツリー内のすべてのアセットを、Dynamic Media との同期から除外します。 |

   ![フォルダーレベルの選択的公開](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 「**[!UICONTROL Dynamic Media 公開モード]**」ドロップダウンリストで、オプションを選択します。「**[!UICONTROL Dynamic Media 公開モード]**」オプションのデフォルト値は、常に **[!UICONTROL Dynamic Media 設定]**&#x200B;の値になります。ただし、次のいずれかのオプションを使用して、手動でこのデフォルトの **[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きできます。

   >[!IMPORTANT]
   >
   >選択した「Dynamic Media 公開モード」オプションに関係なく、*既に*&#x200B;公開されているアセットに対して後で更新を加えた場合、その更新は、それ以上のユーザー操作なしに即時に公開されます。

   | Dynamic Media 公開モードのオプション | 説明 |
   | --- | --- |
   | **[!UICONTROL 即時]** | アセットがこのフォルダーにアップロードされると、システムはアセットを Experience Manager に取り込み、URL／埋め込みを即座に提供します。このオプションは Experience Manager の公開のみに関連しており、アセットの公開にユーザーが介入する必要はありません。<br>前の手順の&#x200B;**[!UICONTROL 同期モード]**&#x200B;で、「**[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media との同期から除外]**」を選択した場合は、このオプションは使用&#x200B;*できません*。 |
   | **[!UICONTROL アクティベーション時]** | アセットがこのフォルダーにアップロードされる場合は、URL／埋め込みリンクを指定する前に、まずアセットを明示的に公開する必要があります。このオプションは Experience Manager の公開にのみ関連付けられています。<br>前の手順の&#x200B;**[!UICONTROL 同期モード]**&#x200B;で、「**[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media との同期から除外]**」を選択した場合は、このオプションは使用&#x200B;*できません*。 |
   | **[!UICONTROL 選択的公開]** | アセットは、Experience Manager または Dynamic Media のいずれかを選択して公開され、パブリックドメインで配信されます。どちらの公開方法も相互に排他的です。つまり、アセットを DMS7 に公開して、スマート切り抜きや動的レンディションなどの機能を使用できます。または、アセットを安全なプレビュー用に Experience Manager にのみ公開することもできます。これらの同じアセットは、パブリックドメインでの配信のために DMS7 には公開&#x200B;*されません*。前の手順の&#x200B;**[!UICONTROL 同期モード]**&#x200B;で、「**[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media との同期から除外]**」を選択した場合は、このオプションは使用できません。 |

1. ページの右上隅にある「**[!UICONTROL 保存して閉じる]**」を選択したあと、「**[!UICONTROL OK]**」を選択して Experience Manager Assets に戻ります。

## 「公開を管理」を使用した、Dynamic Media または Experience Manager as a Cloud Service へのアセットの選択的公開{#selective-publish-manage-publication}

「**[!UICONTROL 公開を管理]**」を使用して Dynamic Media または Experience Manager にアセットを選択的に公開するには、まず、次のいずれかの操作を完了している必要があります。

* **[!UICONTROL Dynamic Media 設定]**&#x200B;の「**[!UICONTROL アセットを公開]**」オプションを「**[!UICONTROL 選択的公開]**」に設定する。
* フォルダーレベルで選択的公開を設定する。

詳しくは、[Dynamic Media 設定の作成](#configuring-dynamic-media-cloud-services)、または [Dynamic Media のフォルダーレベルでの選択的公開の設定](#selective-publish-configure-folder)を参照してください。

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

**「公開を管理」を使用して、Dynamic Media または Experience Manager as a Cloud Service にアセットを選択的に公開するには：**

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作を行います。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーの「**[!UICONTROL 公開を管理]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

     >[!NOTE]
     >
     >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンを選択し、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、目的のアクティベーションの種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 公開]**（Experience Manager に対して） | 安全にプレビューするために Experience Manager にアセットを公開するには、このオプションを選択します。 |
   | **[!UICONTROL Dynamic Media に公開]** | パブリックドメインで配信するためにアセットを Dynamic Media に公開する場合、またはスマート切り抜きや動的レンディションなどの機能を使用する場合には、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、投稿のタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに公開する場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを公開する場合に選択します。 |

1. **[!UICONTROL 公開を管理]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」を選択します。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作を行います。
   * 必要に応じて、公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 - 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 公開]**」または「**[!UICONTROL Dynamic Media に公開]**」を選択します。
1. 「**[!UICONTROL OK]**」を選択します。

### 「公開を管理」を使用した、Dynamic Media または Experience Manager からのアセットの選択的非公開  {#selective-unpublish-manage-publication}

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作を行います。
   * アセットを非公開にするフォルダーに移動します。フォルダーを選択し、ツールバーの「**[!UICONTROL 公開を管理]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを非公開にするフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

     >[!NOTE]
     >
     >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンを選択し、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、アクティベーションを解除する種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 非公開]**（Experience Manager から） | Experience Manager からアセットを非公開にするには、このオプションを選択します。 |
   | **[!UICONTROL Dynamic Media から非公開]** | Dynamic Media からアセットを非公開にするには、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに非公開にする場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを非公開にする場合に選択します。 |

1. **[!UICONTROL 公開を管理]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」を選択します。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作を行います。
   * 非公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 - 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 非公開]**」または「**[!UICONTROL Dynamic Media から非公開]**」を選択します。
1. 「**[!UICONTROL OK]**」を選択します。

## 「クイック公開」を使用した、Dynamic Media または Experience Manager へのアセットの公開 {#quick-publish-aem-dm}

簡単なアセットアクティベーションの場合は、**[!UICONTROL クイック公開]**&#x200B;を使用できます。**[!UICONTROL クイック公開]**：選択したアセットを直ちに公開し、ユーザー操作は不要です。未公開の参照も自動的に公開されます。

>[!NOTE]
>
>**[!UICONTROL クイック公開]**&#x200B;を使用してアセットを Dynamic Media または Experience Manager に公開するには、**[!UICONTROL Dynamic Media 設定]**&#x200B;または選択したフォルダーのフォルダープロパティで「**[!UICONTROL 選択的公開]**」が有効になっていることを確認します。

**「クイック公開」を使用して Dynamic Media または Experience Manager にアセットを公開するには：**

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。ページの左側で、（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、ページの右側で、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作を行います。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL クイック公開]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL クイック公開]**」を選択します。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

     >[!NOTE]
     >
     >ツールバーに「**[!UICONTROL クイック公開]**」が表示されない場合は、省略記号ボタンを選択し、リストメニューから「**[!UICONTROL クイック公開]**」を選択します。

     ![Dynamic Media に対するフォルダーレベルのクイック公開](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 「**[!UICONTROL クイック公開]**」メニューリストから、次のいずれかのオプションを選択します。

   | クイック公開オプション | 動作 |
   | --- | --- |
   | Experience Manager に公開 | 選択したアセットを直ちに Experience Manager に公開します。 |
   | Brand Portal に公開 | 選択したアセットを直ちに **[!UICONTROL Brand Portal]** に公開します。<br> このオプションは、Experience Manager Assets インスタンスで **[!UICONTROL Brand Portal]** が既に設定されている場合にのみ使用できます。 |
   | Dynamic Media に公開 | 選択したアセットを直ちに Dynamic Media に公開します。<br>アセットは、既に Dynamic Media と同期している必要があります。必要に応じて、フォルダーのプロパティの&#x200B;**[!UICONTROL 同期モード]**&#x200B;が既に「**[!UICONTROL このフォルダーサブツリー内のすべてを Dynamic Media に同期]**」に設定されていることを確認します。 |

1. 「**[!UICONTROL OK]**」を選択したあと、「**[!UICONTROL 閉じる]**」を選択します。

## 検索結果を使用して、アセットを選択的に公開または非公開にする {#selective-publish-unpublish-search-results}

検索結果には、異なる Dynamic Media 公開設定を持つ複数のアセットフォルダーのアセットが表示される場合があります。検索結果から 1 つ以上のアセットを選択し、そのアセットに異なる Dynamic Media 公開モードの設定がある場合は、ツールバーから「**[!UICONTROL 公開を管理]**」をトリガーして、公開または非公開にできます。

[Experience Manager でのアセットの検索](/help/assets/search-assets.md)も参照してください。

**検索結果を使用してアセットを選択的に公開または非公開にするには：**

1. Experience Manager で、ページの左上隅にある Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。ページの左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. ページ右上隅近くにある、ツールバーの検索アイコン（虫めがね）を選択します。
1. 「**[!UICONTROL 検索キーワードを入力]**」フィールドにキーワードを入力し、**[!UICONTROL Enter]** キーを押します。
1. ページの左上隅付近にある&#x200B;**[!UICONTROL リスト表示]**&#x200B;アイコンを選択します。
1. ページの左上隅付近にある「**[!UICONTROL フィルター]**」アイコンを選択します。

   ![検索結果のリスト表示とフィルター](/help/assets/assets-dm/select-publish-search-result.png)

1. 左のパネルで、「**[!UICONTROL ステータス]**」を展開し、**[!UICONTROL Dynamic Media]** の検索述語を展開します。
1. 「**[!UICONTROL 公開済み]**」および「**[!UICONTROL 未公開]**」のチェックボックスを使用して、Dynamic Media アセットの公開状態に基づいて検索結果を絞り込みます。
必要に応じて、これらのチェックボックスを「**[!UICONTROL 公開]**」検索述語と組み合わせて使用し、「**[!UICONTROL 公開済み]**」と「**[!UICONTROL 未公開]**」の Experience Manager アセットの検索結果を絞り込むことができます。
1. 次のいずれかの操作を行います。
   * 公開または非公開にする 1 つ以上のアセットを選択します。
   * **[!UICONTROL 検索結果]**&#x200B;ページの右上隅近くにある「**[!UICONTROL すべてを選択]**」を選択します。
1. ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。必要に応じて、ツールバーの省略記号アイコンを選択して、**[!UICONTROL 公開を管理]**&#x200B;を表示します。
1. **[!UICONTROL 公開を管理 -オプション]**&#x200B;ページで、目的のアクションを選択します。

   | 選択したアクション | Dynamic Media 設定の「アセットを公開」設定 | アセットは |
   | --- | --- | --- |
   | 公開 | 即時またはアクティベーション時 | Experience Manager と Dynamic Media に公開 |
   | 公開 | 選択的公開 | Experience Manager のみに公開 |
   | 非公開 | 即時またはアクティベーション時 | Experience Manager と Dynamic Media から非公開 |
   | 非公開 | 選択的公開 | Experience Manager のみから非公開 |
   | Dynamic Media に公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方に非公開 |
   | Dynamic Media に公開 | 選択的公開 | Dynamic Media のみに公開 |
   | Dynamic Media から非公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方から非公開にならない |
   | Dynamic Media から非公開 | 選択的公開 | Dynamic Media のみから非公開 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | 選択したスケジュール | 結果 |
   | --- | --- |
   | 今すぐ | 選択したアクションは直ちに実行されます。 |
   | 後で | 選択したアクションは、選択した特定の日時に実行されます。 |

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」を選択します。
1. （オプション）**[!UICONTROL 公開を管理 - オプション]**&#x200B;ページで、選択したアセットに関する表の「**[!UICONTROL 公開ターゲット]**」列を確認します。

   | Dynamic Media 設定の「アセットを公開」設定 | 選択したアクション | 公開ターゲット |
   | --- | --- | --- |
   | 即時または<br>アクティベーション時 | 公開 | Experience Manager と Dynamic Media |
   | 即時または<br>アクティベーション時 | Dynamic Media に公開 | なし |
   | 選択的公開 | 公開 | Experience Manager |
   | 選択的公開 | Dynamic Media に公開 | Dynamic Media |
   | 即時または<br>アクティベーション時 | 非公開 | Experience Manager と Dynamic Media |
   | 即時または<br>アクティベーション時 | Dynamic Media から非公開 | なし |
   | 選択的公開 | 非公開 | Experience Manager |
   | 選択的公開 | Dynamic Media から非公開 | Dynamic Media |

1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作を行います。
   * 公開または非公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 - 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 公開]**」または「**[!UICONTROL 非公開]**」を選択してアクションを開始します。
1. 「**[!UICONTROL OK]**」を選択します。

## アセットの公開ステータスの確認 {#check-publish-status-of-asset}

Experience Manager の&#x200B;**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、**[!UICONTROL リスト表示]**&#x200B;のいずれかで&#x200B;**[!UICONTROL タイムライン]**&#x200B;を使用して、アセットの公開状態をすばやく確認することができます。

**アセットの公開ステータスを確認するには:**

1. Experience Manager で、ページの左上隅にある Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。ページの左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**（下のスクリーンショットは&#x200B;**[!UICONTROL リスト表示]**&#x200B;のアセットを示しています）で、公開または非公開にしたアセットを含むフォルダーを開きます。
1. チェックマークが付くようにアセットを選択します。例については、下のスクリーンショットを参照してください。
1. ページの左上隅付近にあるドロップダウンメニューで「**[!UICONTROL タイムライン]**」を選択します。左側のパネルの「**[!UICONTROL ステータス]**」領域には、選択したアセットの公開状態が表示されます。
**[!UICONTROL リスト表示]**&#x200B;を使用する場合、**[!UICONTROL Dynamic Media]** の公開状態に関する追加の列が表示されます。
   * Dynamic Media と同期するように設定されたフォルダーには、デフォルトで「**[!UICONTROL Dynamic Media]**」列が表示されます。
   * Dynamic Media と同期するように設定されて&#x200B;*いない*フォルダーには、「Dynamic Media」列は表示されません。
     ![リスト表示とタイムライン](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 選択的公開のトラブルシューティング {#selective-publish-troubleshoot}

Dynamic Media に同期されず、Dynamic Media の公開アクションがトリガーされたアセットは、次のエラーメッセージとソリューションが発生します。

![選択的公開エラー](/help/assets/assets-dm/selective-publish-error.png)
