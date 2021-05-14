---
title: Dynamic Media での選択的公開の操作
description: Dynamic Mediaの一部のみの発行を使用する方法について説明します。
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

Adobe Experience ManagerまたはDynamic Mediaに対して、またはから、アセットの公開と非公開を選択できます。 これは、**[!UICONTROL パブリケーションの管理]**&#x200B;または&#x200B;**[!UICONTROL クイック発行]**&#x200B;を使用して、フォルダーレベルで行うことができます。 この発行方法は、Dynamic Mediaインスタンス内のすべてのフォルダに対してグローバルな設定を持つ&#x200B;**[!UICONTROL Dynamic Mediaの設定]**&#x200B;だけに依存しないので便利です。

例えば、選択的公開を使用して、まだ実行されていない製品のアセットを操作できます。その場合、マーケティングチームは、Dynamic Mediaと同期されたスマートな切り抜き画像と動的なレンディションにアクセスできます。プロモーション用の資料を作れるので、Dynamic Mediaに資産を発行しなくてもグローバル配信が可能です。

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

後でフォルダー内の「**[!UICONTROL 選択的公開]**」設定を変更すると、その変更の影響を受けるのは、その時点からそのフォルダーにアップロードする新しいアセットだけです。フォルダー内の既存のアセットの公開状態は、**[!UICONTROL クイック公開]**&#x200B;または&#x200B;**[!UICONTROL 公開を管理]**&#x200B;ダイアログボックスから手動で変更するまで、そのままになります。

フォルダーレベル&#x200B;**[!UICONTROL Dynamic Media発行モード]**&#x200B;オプションは、常に、**[!UICONTROL Dynamic Media構成]**&#x200B;の&#x200B;**[!UICONTROL 発行アセット]**&#x200B;設定にある値にデフォルト設定されます。 ただし、このトピックの次の手順では、フォルダーレベルで手動でこのデフォルト値を変更して、**[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きする方法を示します（次の手順で説明します）。

信頼できるかどうかに関係なく、次の処理を行います。

* **[!UICONTROL Dynamic Media設定]**&#x200B;に設定された&#x200B;**[!UICONTROL アセットを発行]**&#x200B;値
* または、フォルダーレベルのプロパティで設定された&#x200B;**[!UICONTROL Dynamic Media公開モード]**&#x200B;値

「**[!UICONTROL すぐに]**」、「**[!UICONTROL アクティベーション]**」、または「**[!UICONTROL 一部のみの発行]**」を選択できます。 例えば、**[!UICONTROL Dynamic Media設定]**&#x200B;の&#x200B;**[!UICONTROL アセットを発行]**&#x200B;の値を&#x200B;**[!UICONTROL アクティベーション]**&#x200B;に設定できます。 また、**[!UICONTROL Dynamic Media発行]**&#x200B;モードの値をフォルダーレベルで&#x200B;**[!UICONTROL 一部の発行]**&#x200B;に設定したり、逆に設定したりできます。

フォルダーで選択的公開を設定した後、次の操作をおこなうことができます。

* [「パブリケーションの管理](#selective-publish-manage-publication)」を使用して、Dynamic MediaまたはExperience Managerにアセットを選択して公開する。
* [「パブリケーションの管理](#selective-unpublish-manage-publication)」を使用して、Dynamic MediaまたはExperience Managerからアセットを選択して非公開にします。
* [クイック公開を使用したDynamic MediaまたはExperience Managerへのアセットの公開](#quick-publish-aem-dm)。
* [検索結果を使用して、アセットを選択して公開または非公開にする](#selective-publish-unpublish-search-results)。

**Dynamic Media のフォルダーレベルで選択的公開を設定するには:**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側で、（ツールアイコンの真上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. 次のいずれかの操作をおこないます。
   * 既存フォルダーのプロパティの編集 - **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、プロパティを編集するフォルダーに移動します。フォルダーを選択し、ツールバーで&#x200B;**[!UICONTROL プロパティ]**&#x200B;をタップします。
   * 新しいフォルダーのプロパティを編集します。**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、ページ右上隅近くの&#x200B;**[!UICONTROL 作成/フォルダー]**&#x200B;をタップします。 **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログボックスで、フォルダーのタイトル（必須）を入力し、「**[!UICONTROL 作成]**」をタップします。 フォルダーを選択し、ツールバーで&#x200B;**[!UICONTROL プロパティ]**&#x200B;をタップします。

1. 「**[!UICONTROL 同期モード]**」ドロップダウンリストで、次のいずれかを選択します。

   | 同期モード | 説明 |
   | --- | --- |
   | **[!UICONTROL 継承]** | フォルダーに明示的な同期値がありません。代わりに、フォルダーは、その上位フォルダーの1つ、または&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;で設定されているデフォルトモードから同期値を継承します。 **[!UICONTROL 継承]**&#x200B;の詳細なステータスは、ツールチップを介して表示されます。 |
   | **[!UICONTROL このフォルダーサブツリーのすべてをDynamic Mediaに同期]** | Dynamic Media への公開を続行するには、アセットを Dynamic Media と同期する必要があります。このオプションを選択すると、このサブツリー内のすべてのアセットが含まれ、Dynamic Mediaと同期されます。 フォルダー固有の設定は、**[!UICONTROL Dynamic Media構成]**&#x200B;のデフォルト設定に優先します。 |
   | **[!UICONTROL このフォルダーサブツリー内のすべてをDynamic Media同期から除外する]** | このサブツリー内のすべてのアセットを、Dynamic Mediaとの同期から除外します。 |

   ![フォルダーレベルの選択的公開](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 「**[!UICONTROL Dynamic Media 公開モード]**」ドロップダウンリストで、オプションを選択します。**[!UICONTROL Dynamic Media公開モード]**&#x200B;オプションは、常に&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;で設定された値にデフォルト設定されます。 ただし、次のいずれかのオプションを使用して、手動でこのデフォルトの **[!UICONTROL Dynamic Media 設定]**&#x200B;値を上書きできます。

   >[!IMPORTANT]
   >
   >選択したDynamic Media公開モードのオプションに関係なく、後で&#x200B;*既に*&#x200B;公開されているアセットに対して行った更新はすべて、ユーザーの操作を必要とせずに直ちに公開されます。

   | Dynamic Media 公開モードのオプション | 説明 |
   | --- | --- |
   | **[!UICONTROL 即時]** | アセットがこのフォルダーにアップロードされると、アセットがExperience Managerーに取り込まれ、URL/埋め込みが即座に提供されます。 このオプションはExperience Managerの公開のみに関連しており、アセットの公開にユーザーが介入する必要はありません。<br>前の手順で「このフォルダーサブツリー内のすべてを ** 除外する」を選択した場合、このオプションは使用できま **[!UICONTROL せん。前の手順では、Dynamic Media]** 同期 **[!UICONTROL モ]** ードから同期します。 |
   | **[!UICONTROL アクティベーション時]** | アセットがこのフォルダーにアップロードされる場合は、URL/埋め込みリンクを指定する前に、最初にアセットを明示的に公開する必要があります。 このオプションは、Experience Managerの公開にのみ関連付けられます。<br>前の手順で「このフォルダーサブツリー内のすべてを ** 除外する」を選択した場合、このオプションは使用できま **[!UICONTROL せん。前の手順では、Dynamic Media]** 同期 **[!UICONTROL モ]** ードから同期します。 |
   | **[!UICONTROL 選択的公開]** | アセットは、パブリックドメインでの配信のために、Experience ManagerまたはDynamic Mediaのどちらかを選択して発行されます。 どちらの公開方法も相互に排他的です。つまり、アセットを DMS7 に公開して、スマート切り抜きや動的レンディションなどの機能を使用できます。または、アセットをExperience Managerのみに公開して、安全なプレビューを実現することもできます。これらの同じアセットは、パブリックドメインでの配信のためにDMS7に公開&#x200B;*され*&#x200B;ません。 前の手順で&#x200B;**[!UICONTROL 同期モード]**&#x200B;で、「**[!UICONTROL Dynamic Media同期]**&#x200B;からこのフォルダーサブツリー内のすべてを除外する」を選択した場合は、このオプションを使用できません。 |

1. ページの右上隅にある「**[!UICONTROL 保存して閉じる]**」をタップし、「**[!UICONTROL OK]**」をタップしてExperience Managerアセットに戻ります。

## パブリケーションの管理{#selective-publish-manage-publication}を使用して、アセットを選択してDynamic MediaまたはExperience ManagerにCloud Serviceとして発行

**[!UICONTROL パブリケーションの管理]**&#x200B;を使用して、アセットを選択的にDynamic MediaまたはExperience Managerに発行する前に、次のいずれかの操作を行ったことを確認してください。

* **[!UICONTROL Dynamic Media設定]**&#x200B;の「アセットを発行&#x200B;]**」オプションを**[!UICONTROL &#x200B;一部の発行&#x200B;]**に設定します。**[!UICONTROL 
* または、フォルダーレベルで選択的発行を設定します。

詳しくは、[Dynamic Media 設定の作成](#configuring-dynamic-media-cloud-services)、または [Dynamic Media のフォルダーレベルでの選択的公開の設定](#selective-publish-configure-folder)を参照してください。

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>フォルダー間でアセットを&#x200B;*コピー*&#x200B;すると、これらのアセットの公開状態がクリアされます。ただし、フォルダープロパティが「**[!UICONTROL 選択的公開]**」に設定されているフォルダー間でアセットを&#x200B;*移動*&#x200B;すると、それらのアセットの公開状態は維持されます。

**「パブリケーションの管理」を使用して、アセットを選択してDynamic MediaまたはExperience ManagerにCloud Serviceとして発行するには：**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側で、（ツールアイコンの真上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーで&#x200B;**[!UICONTROL パブリケーションの管理]**&#x200B;をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスを簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーで、**[!UICONTROL パブリケーションの管理]**&#x200B;をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスを簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、目的のアクティベーションの種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 発行]** (Experience Managerへ) | プレビューを保護するために、Experience Managerにアセットを公開するには、このオプションを選択します。 |
   | **[!UICONTROL Dynamic Media に公開]** | パブリックドメインで配信するためにアセットをDynamic Mediaに公開する場合、またはスマート切り抜きや動的レンディションなどの機能を使用する場合は、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、投稿のタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに公開する場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを公開する場合に選択します。 |

1. **[!UICONTROL パブリケーションの管理]**&#x200B;ページの右上隅にある&#x200B;**[!UICONTROL 「次へ]**」をタップします。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作をおこないます。
   * 必要に応じて、公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL パブリケーションの管理 — スコープ]**&#x200B;ページの右上隅にある&#x200B;**[!UICONTROL 発行]**&#x200B;または&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;に発行をタップします。
1. 「**[!UICONTROL OK]**」をタップします。

### パブリケーションの管理{#selective-unpublish-manage-publication}を使用して、Dynamic MediaまたはExperience Managerからアセットを選択して非公開にする

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 左側で、（ツールアイコンの真上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを非公開にするフォルダーに移動します。フォルダーを選択し、ツールバーで&#x200B;**[!UICONTROL パブリケーションの管理]**&#x200B;をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスを簡単に確認できます。
   * アセットを非公開にするフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーで、**[!UICONTROL パブリケーションの管理]**&#x200B;をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスを簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL 公開を管理]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理 - オプション]**&#x200B;ページの「**[!UICONTROL アクション]**」で、アクティベーションを解除する種類を選択します。

   | アクション | 説明 |
   | --- | --- |
   | **[!UICONTROL 非公開]** (Experience Managerから) | Experience Managerからアセットを非公開にするには、このオプションを選択します。 |
   | **[!UICONTROL Dynamic Media から非公開]** | Dynamic Mediaからアセットを非公開にするには、このオプションを選択します。<br>このオプションは、フォルダーのプロパティで「**[!UICONTROL Dynamic Media 公開モード]**」が「**[!UICONTROL 選択的公開]**」に設定されている場合にのみ使用できます。 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | スケジュール | 説明 |
   | --- | --- |
   | **[!UICONTROL 今すぐ]** | アセットを直ちに非公開にする場合に選択します。 |
   | **[!UICONTROL 後で]** | 特定の日時にアセットを非公開にする場合に選択します。 |

1. **[!UICONTROL パブリケーションの管理]**&#x200B;ページの右上隅にある&#x200B;**[!UICONTROL 「次へ]**」をタップします。
1. **[!UICONTROL 公開を管理 -範囲]**&#x200B;ページで、次のいずれかの操作をおこないます。
   * 非公開から削除する 1 つ以上のアセットを選択します。
   * **[!UICONTROL パブリケーションの管理 — スコープ]**&#x200B;ページの右上隅にある&#x200B;**[!UICONTROL 非公開]**&#x200B;または&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;から非公開をタップします。
1. 「**[!UICONTROL OK]**」をタップします。

## クイック発行を使用したDynamic MediaまたはExperience Managerへのアセットの発行{#quick-publish-aem-dm}

簡単なアセットアクティベーションの場合は、**[!UICONTROL クイック公開]**&#x200B;を使用できます。**[!UICONTROL クイック公開]**：選択したアセットを直ちに公開し、ユーザー操作は不要です。非公開の参照も自動的に公開されます。

>[!NOTE]
>
>**[!UICONTROL クイック発行]**&#x200B;を使用して、アセットをDynamic MediaまたはExperience Managerに発行するには、**[!UICONTROL Dynamic Media設定]**&#x200B;または選択したフォルダーのフォルダープロパティで、**[!UICONTROL 一部の発行]**&#x200B;を有効にします。

**クイック公開を使用してDynamic MediaまたはExperience Managerにアセットを公開するには：**

1. Experience Managerで、Experience Managerのロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側で、（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、ページの右側で&#x200B;**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**&#x200B;または&#x200B;**[!UICONTROL リスト表示]**&#x200B;で、次のいずれかの操作をおこないます。
   * アセットを公開するフォルダーに移動します。フォルダーを選択し、ツールバーで&#x200B;**[!UICONTROL クイック発行]**&#x200B;をタップします。 **[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のフォルダーの公開ステータスを簡単に確認できます。
   * アセットを公開するフォルダーに移動します。フォルダーを開き、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL クイック公開]**」をタップします。**[!UICONTROL リスト表示]**&#x200B;を使用すると、特定のアセットの公開ステータスを簡単に確認できます。

      >[!NOTE]
      >
      >ツールバーに「**[!UICONTROL クイック公開]**」が表示されない場合は、省略記号ボタンをタップし、リストメニューから「**[!UICONTROL クイック公開]**」を選択します。

      ![Dynamic Media に対するフォルダーレベルのクイック公開](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 「**[!UICONTROL クイック公開]**」メニューリストから、次のいずれかのオプションを選択します。

   | クイック公開オプション | 動作 |
   | --- | --- | 
   | Experience Managerに発行 | 選択したアセットを直ちにExperience Managerに公開します。 |
   | Brand Portal に公開 | 選択したアセットをすぐに&#x200B;**[!UICONTROL ブランドポータル]**&#x200B;に公開します。<br>このオプションは、Experience Managerアセットインスタンスで **[!UICONTROL ブランドポータルが既に設定されている場合にのみ使用]** できます。 |
   | Dynamic Media に公開 | 選択したアセットを直ちに Dynamic Media に公開します。<br>アセットは既にDynamic Mediaに同期されている必要があります。必要に応じて、フォルダーのプロパティ内の&#x200B;**[!UICONTROL 同期モード]**&#x200B;が既に&#x200B;**[!UICONTROL 同期されていることを確認します。このフォルダーサブツリー内のすべてをDynamic Media]**&#x200B;に同期します。 |

1. 「**[!UICONTROL OK]**」をタップし、「**[!UICONTROL 閉じる]**」をタップします。

## 検索結果を使用して、アセットを選択的に公開または非公開にする{#selective-publish-unpublish-search-results}

検索結果には、異なる Dynamic Media 公開設定を持つ複数のアセットフォルダーのアセットが表示される場合があります。検索結果から1つ以上のアセットを選択し、アセットに異なるDynamic Media発行モードの設定がある場合は、ツールバーの&#x200B;**[!UICONTROL パブリケーションを管理]**&#x200B;をトリガーして、公開または非公開にできます。

[Experience Manager](/help/assets/search-assets.md)内のアセットの検索も参照してください。

**検索結果を使用して、アセットを選択的に公開または非公開にするには:**

1. Experience Managerで、ページの左上隅にあるExperience Managerロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側で、（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. ページ右上隅近くにある、ツールバーの検索アイコン（虫めがね）をタップします。
1. 「**[!UICONTROL 検索するタイプ]**」テキストフィールドにキーワードを入力し、**[!UICONTROL Enter]**&#x200B;キーを押します。
1. ページの左上隅付近にある「**[!UICONTROL リスト表示]**」をタップします。
1. ページの左上隅付近にある&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。

   ![検索結果のリスト表示とフィルター](/help/assets/assets-dm/select-publish-search-result.png)

1. 左のパネルで、「**[!UICONTROL ステータス]**」を展開し、**[!UICONTROL Dynamic Media]** の検索述語を展開します。
1. 「**[!UICONTROL 公開済み]**」および「**[!UICONTROL 未公開]**」のチェックボックスを使用して、Dynamic Media アセットの公開状態に基づいて検索結果を絞り込みます。
必要に応じて、これらのチェックボックスを**[!UICONTROL 検索述語の発行]**&#x200B;と共に使用し、**[!UICONTROL 発行済み]**&#x200B;と&#x200B;**[!UICONTROL 未発行]**&#x200B;のExperience Managerアセットの検索結果を絞り込むことができます。
1. 次のいずれかの操作をおこないます。
   * 公開または非公開にする 1 つ以上のアセットを選択します。
   * **[!UICONTROL 検索結果]**&#x200B;ページの右上隅近くにある「**[!UICONTROL すべて選択]**」をタップします。
1. ツールバーで、**[!UICONTROL パブリケーションの管理]**&#x200B;をタップします。 必要に応じて、ツールバーの省略記号アイコンをタップし、「**[!UICONTROL パブリケーションの管理]**」を表示します。
1. **[!UICONTROL 公開を管理 -オプション]**&#x200B;ページで、目的のアクションを選択します。

   | 選択したアクション | Dynamic Media 設定の「アセットを公開」設定 | アセットは |
   | --- | --- | --- |
   | 公開 | 即時またはアクティベーション時 | Experience ManagerとDynamic Mediaに発行。 |
   | 公開 | 選択的公開 | Experience Managerにのみ公開済み。 |
   | 非公開 | 即時またはアクティベーション時 | Experience ManagerとDynamic Mediaから非公開。 |
   | 非公開 | 選択的公開 | Experience Managerのみ非公開。 |
   | Dynamic Media に公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方には投稿されていません。 |
   | Dynamic Media に公開 | 選択的公開 | Dynamic Media のみに公開される。 |
   | Dynamic Media から非公開 | 即時またはアクティベーション時 | Experience Manager、Dynamic Media、またはその両方から非公開にしない。 |
   | Dynamic Media から非公開 | 選択的公開 | Dynamic Media のみから非公開になる。 |

1. 「**[!UICONTROL スケジュール]**」で、アクティベーションを解除するタイミングを設定します。

   | 選択したスケジュール | 結果 |
   | --- | --- |
   | 今すぐ | 選択したアクションは直ちに実行されます。 |
   | 後で | 選択したアクションは、選択した特定の日時に実行されます。 |

1. **[!UICONTROL パブリケーションの管理 — オプション]**&#x200B;ページの右上隅にある&#x200B;**[!UICONTROL 「次へ]**」をタップします。
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

Experience Managerで&#x200B;**[!UICONTROL タイムライン]**&#x200B;と&#x200B;**[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**&#x200B;を使用して、アセットの公開状態をすばやく確認できます。

**アセットの公開ステータスを確認するには:**

1. Experience Managerで、ページの左上隅にあるExperience Managerロゴをタップして、グローバルナビゲーションコンソールにアクセスします。 ページの左側で、（ツールアイコンのすぐ上にある）ナビゲーションアイコンをタップし、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;をタップします。
1. **[!UICONTROL カード表示]**、**[!UICONTROL 列表示]**、または&#x200B;**[!UICONTROL リスト表示]**（下のスクリーンショットは&#x200B;**[!UICONTROL リスト表示]**&#x200B;のアセットを示しています）で、公開または非公開にしたアセットを含むフォルダーを開きます。
1. チェックマークが付くようにアセットを選択します。例については、下のスクリーンショットを参照してください。
1. ページの左上隅近くにあるドロップダウンメニューで、「**[!UICONTROL タイムライン]**」を選択します。 左側のパネルの「**[!UICONTROL ステータス]**」領域には、選択したアセットの公開状態が表示されます。
**[!UICONTROL リスト表示]**&#x200B;を使用すると、**[!UICONTROL Dynamic Media]**&#x200B;の公開状態に余分な列が表示されます。
   * Dynamic Mediaと同期するように構成されたフォルダーには、デフォルトで&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;列が表示されます。
   * **がDynamic Mediaと同期するように構成されていないフォルダーは、Dynamic Media列を表示しません。
      ![リスト表示とタイムライン](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 選択的公開のトラブルシューティング {#selective-publish-troubleshoot}

Dynamic Media に同期されず、Dynamic Media の公開アクションがトリガーされたアセットは、次のエラーメッセージとソリューションが発生します。

![選択的公開エラー](/help/assets/assets-dm/selective-publish-error.png)
