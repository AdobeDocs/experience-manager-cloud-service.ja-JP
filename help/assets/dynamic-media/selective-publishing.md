---
title: Dynamic Media での選択的公開の操作
description: Dynamic Mediaでの選択的公開の操作方法を説明します。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '2939'
ht-degree: 44%

---

# Dynamic Media のフォルダーレベルでの選択的公開の設定 {#selective-publish-configure-folder}

Adobe Experience ManagerまたはDynamic Mediaに対して、またはからアセットを公開または非公開にすることができます。 これは、**[!UICONTROL 「公開を管理」]**&#x200B;または&#x200B;**[!UICONTROL 「クイック公開」]**&#x200B;を使用して、フォルダーレベルでおこなえます。 この公開方法は、Dynamic Mediaインスタンス内のすべてのフォルダーでグローバルな設定を持つ&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;にのみ依存しないので便利です。

例えば、選択的公開を使用して、まだ実行されていない製品のアセットを操作できます。その場合、マーケティングチームは、Dynamic Mediaに同期されたスマート切り抜き画像と動的レンディションにアクセスできます。プロモーション用の資料を作成できますが、グローバル配信のためにDynamic Mediaに公開する必要はありません。

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

後でフォルダー内の「**[!UICONTROL 選択的公開]**」設定を変更すると、その変更の影響を受けるのは、その時点からそのフォルダーにアップロードする新しいアセットだけです。フォルダー内の既存のアセットの公開状態は、**[!UICONTROL クイック公開]**&#x200B;または&#x200B;**[!UICONTROL 公開を管理]**&#x200B;ダイアログボックスから手動で変更するまで、そのままになります。

「フォルダーレベル&#x200B;**[!UICONTROL Dynamic Media公開モード]**」オプションでは、常に、**[!UICONTROL Dynamic Media設定]**&#x200B;の「**[!UICONTROL アセットを公開]**」設定にある値がデフォルト値になります。 ただし、このトピックの次の手順では、フォルダーレベルで手動でこのデフォルト値を変更して、**[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きする方法を示します（次の手順で説明します）。

次の項目に依存しているかどうかに関係なく、

* **[!UICONTROL Dynamic Media設定]**&#x200B;に設定された&#x200B;**[!UICONTROL Publish Assets]**&#x200B;値
* または、フォルダーレベルのプロパティで設定された&#x200B;**[!UICONTROL Dynamic Mediaパブリッシュモード]**&#x200B;値

引き続き、「**[!UICONTROL 即時]**」、「**[!UICONTROL アクティベーション時]**」、「**[!UICONTROL 選択的公開]**」のいずれかを選択できます。 例えば、**[!UICONTROL Dynamic Media設定の「**[!UICONTROL &#x200B;アセットを公開&#x200B;]**」の値を「]**」の「**[!UICONTROL アクティベーション時]**」に設定できます。 また、**[!UICONTROL Dynamic Media公開]**&#x200B;モードの値をフォルダーレベルで&#x200B;**[!UICONTROL 選択的公開]**&#x200B;に設定することも、逆に設定することもできます。

フォルダーで選択的公開を設定した後、次の操作をおこなうことができます。

* [「公開を管理」を使用して、Dynamic MediaまたはExperience Managerにアセットを選択的に公開する](#selective-publish-manage-publication)。
* [「公開を管理」を使用して、Dynamic MediaまたはExperience Managerからアセットを選択的に非公開にする](#selective-unpublish-manage-publication)。
* [クイック公開を使用したDynamic MediaまたはExperience Managerへのアセットの公開](#quick-publish-aem-dm)
* [検索結果を使用して、アセットを選択的に公開または非公開にする](#selective-publish-unpublish-search-results)。

**Dynamic Media のフォルダーレベルで選択的公開を設定するには:**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]** /**[!UICONTROL ファイル]**&#x200B;をタップします。
1. 次のいずれかの操作をおこないます。
   * 既存フォルダーのプロパティの編集 - **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、プロパティを編集するフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL プロパティ]**」をタップします。
   * 新しいフォルダーのプロパティを編集します。**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、ページの右上隅付近にある&#x200B;**[!UICONTROL 作成/フォルダー]**&#x200B;をタップします。 **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログボックスで、フォルダーのタイトル（必須）を入力し、「**[!UICONTROL 作成]**」をタップします。 フォルダーを選択し、ツールバーで「**[!UICONTROL プロパティ]**」をタップします。

1. 「**[!UICONTROL 同期モード]**」ドロップダウンリストで、次のいずれかを選択します。

   | 同期モード | 説明 |
   | --- | --- |
   | **[!UICONTROL 継承]** | フォルダーに明示的な同期値はありません。代わりに、上位フォルダーの1つ、または&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;に設定されたデフォルトモードから同期値を継承します。 **[!UICONTROL 継承]**&#x200B;の詳細なステータスは、ツールチップで表示されます。 |
   | **[!UICONTROL このフォルダーサブツリー内のすべてをDynamic Mediaに同期]** | Dynamic Media への公開を続行するには、アセットを Dynamic Media と同期する必要があります。このオプションを選択すると、このサブツリー内のすべてのアセットが含まれ、Dynamic Mediaと同期されます。 フォルダー固有の設定は、**[!UICONTROL Dynamic Media設定]**&#x200B;のデフォルト設定よりも優先されます。 |
   | **[!UICONTROL このフォルダーサブツリー内のすべてをDynamic Media同期から除外]** | このサブツリー内のすべてのアセットを、Dynamic Mediaとの同期から除外します。 |

   ![フォルダーレベルの選択的公開](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 「**[!UICONTROL Dynamic Media 公開モード]**」ドロップダウンリストで、オプションを選択します。「**[!UICONTROL Dynamic Media公開モード]**」オプションは、常に&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;で設定された値にデフォルト設定されます。 ただし、次のいずれかのオプションを使用して、手動でこのデフォルトの **[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きできます。

   >[!IMPORTANT]
   >
   >選択する「Dynamic Media公開モード」オプションに関係なく、既に&#x200B;**&#x200B;公開されているアセットに対して後でおこなった更新は、ユーザーの操作を必要とせずに即座に公開されます。

   | Dynamic Media 公開モードのオプション | 説明 |
   | --- | --- |
   | **[!UICONTROL 即時]** | アセットがこのフォルダーにアップロードされると、システムはアセットをExperience Managerに取り込み、URL/埋め込みをすぐに提供します。 このオプションはExperience Managerの公開のみに関連しており、アセットの公開にユーザーが介入する必要はありません。<br>前の手順で「 Dynamic Media同期モ ** ードからこのフォルダー **[!UICONTROL のサブツリー内のすべてを除外」を選択し]** た場合、このオ **[!UICONTROL プションは使]** 用できません。 |
   | **[!UICONTROL アクティベーション時]** | アセットがこのフォルダーにアップロードされる場合は、URL/埋め込みリンクが提供される前に、最初にアセットを明示的に公開する必要があります。 このオプションは、Experience Managerの公開のみに関連付けられます。<br>前の手順で「 Dynamic Media同期モ ** ードからこのフォルダー **[!UICONTROL のサブツリー内のすべてを除外」を選択し]** た場合、このオ **[!UICONTROL プションは使]** 用できません。 |
   | **[!UICONTROL 選択的公開]** | アセットは、Experience ManagerまたはDynamic Mediaに公開され、パブリックドメインで配信されます。 どちらの公開方法も相互に排他的です。つまり、アセットを DMS7 に公開して、スマート切り抜きや動的レンディションなどの機能を使用できます。または、安全なプレビュー用に、Experience Managerのみにアセットを公開することもできます。これらの同じアセットは、パブリックドメインでの配信のためにDMS7に&#x200B;*公開されて*&#x200B;いません。 前の手順の&#x200B;**[!UICONTROL 同期モード]**&#x200B;で、「このフォルダーのサブツリー内のすべてをDynamic Media同期&#x200B;]**から除外する」を選択した場合は、このオプションは使用できません。**[!UICONTROL  |

1. ページの右上隅にある「**[!UICONTROL 保存して閉じる]**」をタップし、「**[!UICONTROL OK]**」をタップしてExperience Managerアセットに戻ります。

## 「公開を管理」を使用して、Dynamic MediaまたはExperience ManagerをCloud Serviceとして選択的に公開する{#selective-publish-manage-publication}

「**[!UICONTROL 公開を管理]**」を使用して、Dynamic MediaまたはExperience Managerにアセットを選択的に公開する前に、次のいずれかの操作を行っていることを確認してください。

* **[!UICONTROL Dynamic Media設定]**&#x200B;の「**[!UICONTROL アセットを公開]**」オプションを「**[!UICONTROL 選択的公開]**」に設定します。
* または、フォルダーレベルで選択的公開を設定します。

詳しくは、[Dynamic Media 設定の作成](#configuring-dynamic-media-cloud-services)、または [Dynamic Media のフォルダーレベルでの選択的公開の設定](#selective-publish-configure-folder)を参照してください。

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

**「公開を管理」を使用して、Dynamic MediaまたはExperience ManagerをCloud Serviceとして選択的に公開するには：**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]** /**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL 公開を管理]**」をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL 公開を管理]**」をタップします。 **[!UICONTROL リストビュー]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、目的のアクティベーションの種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 公開]** (Experience Manager) | 安全にプレビューするためにExperience Managerにアセットを公開するには、このオプションを選択します。 |
   | **[!UICONTROL Dynamic Media に公開]** | パブリックドメインで配信するためにDynamic Mediaにアセットを公開する場合や、スマート切り抜きや動的レンディションなどの機能を使用する場合は、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、投稿のタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに公開する場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを公開する場合に選択します。 |

1. **[!UICONTROL 公開を管理]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」をタップします。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作をおこないます。
   * 必要に応じて、公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 — 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 公開]**」または「**[!UICONTROL Dynamic Mediaに公開]**」をタップします。
1. 「**[!UICONTROL OK]**」をタップします。

### 「公開を管理」を使用して、Dynamic MediaまたはExperience Managerからアセットを選択的に非公開にする{#selective-unpublish-manage-publication}

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側の（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]** /**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを非公開にするフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL 公開を管理]**」をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを非公開にするフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL 公開を管理]**」をタップします。 **[!UICONTROL リストビュー]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、アクティベーションを解除する種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 非公開]** (Experience Manager) | アセットの公開を取り消すには、このExperience Managerを選択します。 |
   | **[!UICONTROL Dynamic Media から非公開]** | Dynamic Mediaのアセットを非公開にするには、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに非公開にする場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを非公開にする場合に選択します。 |

1. **[!UICONTROL 公開を管理]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」をタップします。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作をおこないます。
   * 非公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 — 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 非公開]**」または「**[!UICONTROL Dynamic Mediaから非公開]**」をタップします。
1. 「**[!UICONTROL OK]**」をタップします。

## クイック公開を使用したDynamic MediaまたはExperience Managerへのアセットの公開{#quick-publish-aem-dm}

簡単なアセットアクティベーションの場合は、**[!UICONTROL クイック公開]**&#x200B;を使用できます。**[!UICONTROL クイック公開]**：選択したアセットを直ちに公開し、ユーザー操作は不要です。非公開の参照も自動的に公開されます。

>[!NOTE]
>
>**[!UICONTROL クイック公開]**&#x200B;を使用してDynamic MediaまたはExperience Managerにアセットを公開するには、**[!UICONTROL Dynamic Media設定]**&#x200B;または選択したフォルダーのフォルダープロパティで&#x200B;**[!UICONTROL 選択的公開]**&#x200B;が有効になっていることを確認します。

**クイック公開を使用してDynamic MediaまたはExperience Managerにアセットを公開するには：**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側で、（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、ページの右側で&#x200B;**[!UICONTROL Assets]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーで「**[!UICONTROL クイック公開]**」をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスをより簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL クイック公開]**」をタップします。**[!UICONTROL リストビュー]**&#x200B;を使用すると、特定のアセットの公開ステータスをより簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL クイック公開]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL クイック公開]**」を選択します。

      ![Dynamic Media に対するフォルダーレベルのクイック公開](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 「**[!UICONTROL クイック公開]**」メニューリストから、次のいずれかのオプションを選択します。

   | クイック公開オプション | 動作 |
   | --- | --- | 
   | Experience Managerに公開 | 選択したアセットを直ちにExperience Managerに公開します。 |
   | Brand Portal に公開 | 選択したアセットを直ちに&#x200B;**[!UICONTROL Brand Portal]**&#x200B;に公開します。<br>このオプションは、AssetsインスタンスでBrand Portalが既に設定されてい **[!UICONTROL る場合に]** のみ使用できます。 |
   | Dynamic Media に公開 | 選択したアセットを直ちに Dynamic Media に公開します。<br>アセットは、既にDynamic Mediaと同期している必要があります。必要に応じて、フォルダーのプロパティの&#x200B;**[!UICONTROL 同期モード]**&#x200B;が既に&#x200B;**[!UICONTROL 「このフォルダーのサブツリー内のすべてをDynamic Media]**&#x200B;に同期」に設定されていることを確認します。 |

1. 「**[!UICONTROL OK]**」をタップし、「**[!UICONTROL 閉じる]**」をタップします。

## 検索結果を使用して、アセットを選択的に公開または非公開にする{#selective-publish-unpublish-search-results}

検索結果には、異なる Dynamic Media 公開設定を持つ複数のアセットフォルダーのアセットが表示される場合があります。検索結果から1つ以上のアセットを選択し、そのアセットに異なるDynamic Media公開モードの設定がある場合は、ツールバーの「**[!UICONTROL 公開を管理]**」をトリガーして、公開または非公開にできます。

[Experience Manager](/help/assets/search-assets.md)でのアセットの検索も参照してください。

**検索結果を使用して、アセットを選択的に公開または非公開にするには:**

1. Experience Managerで、ページの左上隅にあるExperience Managerロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側にある（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]** / **[!UICONTROL ファイル]**&#x200B;をタップします。
1. ページ右上隅近くにある、ツールバーの検索アイコン（虫めがね）をタップします。
1. **[!UICONTROL 検索する]**&#x200B;テキストフィールドにキーワードを入力し、**[!UICONTROL Enter]**&#x200B;キーを押します。
1. ページの左上隅付近にある「**[!UICONTROL リスト表示]**」をタップします。
1. ページの左上隅付近にある&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。

   ![検索結果のリスト表示とフィルター](/help/assets/assets-dm/select-publish-search-result.png)

1. 左のパネルで、「**[!UICONTROL ステータス]**」を展開し、**[!UICONTROL Dynamic Media]** の検索述語を展開します。
1. 「**[!UICONTROL 公開済み]**」および「**[!UICONTROL 未公開]**」のチェックボックスを使用して、Dynamic Media アセットの公開状態に基づいて検索結果を絞り込みます。
必要に応じて、「**[!UICONTROL 公開]**」検索述語でこれらのチェックボックスを使用して、「**[!UICONTROL 公開済み]**」と「**[!UICONTROL 未公開]**」のExperience Managerアセットの検索結果を絞り込むことができます。
1. 次のいずれかの操作をおこないます。
   * 公開または非公開にする 1 つ以上のアセットを選択します。
   * **[!UICONTROL 検索結果]**&#x200B;ページの右上隅付近にある「**[!UICONTROL すべて]**&#x200B;を選択」をタップします。
1. ツールバーの「**[!UICONTROL 公開を管理]**」をタップします。 必要に応じて、ツールバーの省略記号アイコンをタップし、「**[!UICONTROL 公開を管理]**」を表示します。
1. **[!UICONTROL 公開を管理 -オプション]**&#x200B;ページで、目的のアクションを選択します。

   | 選択したアクション | Dynamic Media 設定の「アセットを公開」設定 | アセットは |
   | --- | --- | --- |
   | 公開 | 即時またはアクティベーション時 | Experience ManagerとDynamic Mediaに公開。 |
   | 公開 | 選択的公開 | Experience Managerのみに公開。 |
   | 非公開 | 即時またはアクティベーション時 | Experience ManagerとDynamic Mediaから非公開にする。 |
   | 非公開 | 選択的公開 | Experience Managerのみから非公開。 |
   | Dynamic Media に公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方には公開されていない。 |
   | Dynamic Media に公開 | 選択的公開 | Dynamic Media のみに公開される。 |
   | Dynamic Media から非公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方から非公開にしない。 |
   | Dynamic Media から非公開 | 選択的公開 | Dynamic Media のみから非公開になる。 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | 選択したスケジュール | 結果 |
   | --- | --- |
   | 今すぐ | 選択したアクションは直ちに実行されます。 |
   | 後で | 選択したアクションは、選択した特定の日時に実行されます。 |

1. **[!UICONTROL 公開を管理 — オプション]**&#x200B;ページの右上隅にある「**[!UICONTROL 次へ]**」をタップします。
1. （オプション）公開を管理 - オプション&#x200B;****&#x200B;ページで、選択したアセットに関する表の「**[!UICONTROL 公開ターゲット]**」列を確認します。

   | Dynamic Media 設定の「アセットを公開」設定 | 選択したアクション | 公開ターゲット |
   | --- | --- | --- |
   | 即時または<br>アクティベーション時 | 公開 | Experience ManagerとDynamic Media |
   | 即時または<br>アクティベーション時 | Dynamic Media に公開 | なし |
   | 選択的公開 | 公開 | Experience Manager |
   | 選択的公開 | Dynamic Media に公開 | Dynamic Media |
   | 即時または<br>アクティベーション時 | 非公開 | Experience ManagerとDynamic Media |
   | 即時または<br>アクティベーション時 | Dynamic Media から非公開 | なし |
   | 選択的公開 | 非公開 | Experience Manager |
   | 選択的公開 | Dynamic Media から非公開 | Dynamic Media |

1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作をおこないます。
   * 公開または非公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL 公開を管理 - 範囲]**&#x200B;ページの右上隅にある「**[!UICONTROL 公開]**」または「**[!UICONTROL 非公開]**」をタップしてアクションを開始します。
1. 「**[!UICONTROL OK]**」をタップします。

## アセットの公開ステータスの確認 {#check-publish-status-of-asset}

Experience Managerで&#x200B;**[!UICONTROL タイムライン]**&#x200B;を&#x200B;**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、**[!UICONTROL リスト表示]**&#x200B;と共に使用して、アセットの公開状態をすばやく確認できます。

**アセットの公開ステータスを確認するには:**

1. Experience Managerで、ページの左上隅にあるExperience Managerロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側にある（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]** / **[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**（下のスクリーンショットは&#x200B;**[!UICONTROL リスト表示]**&#x200B;のアセットを示しています）で、公開または非公開にしたアセットを含むフォルダーを開きます。
1. チェックマークが付くようにアセットを選択します。例については、下のスクリーンショットを参照してください。
1. ページの左上隅付近にあるドロップダウンメニューで、「**[!UICONTROL タイムライン]**」を選択します。 左側のパネルの「**[!UICONTROL ステータス]**」領域には、選択したアセットの公開状態が表示されます。
**[!UICONTROL リスト表示]**&#x200B;を使用すると、**[!UICONTROL Dynamic Media]**&#x200B;の公開状態の追加の列が表示されます。
   * Dynamic Mediaと同期するように設定されたフォルダーには、デフォルトで&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;列が表示されます。
   * Dynamic Mediaと同期するように設定されている&#x200B;**でないフォルダーには、Dynamic Media列は表示されません。
      ![リスト表示とタイムライン](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 選択的公開のトラブルシューティング {#selective-publish-troubleshoot}

Dynamic Media に同期されず、Dynamic Media の公開アクションがトリガーされたアセットは、次のエラーメッセージとソリューションが発生します。

![選択的公開エラー](/help/assets/assets-dm/selective-publish-error.png)
