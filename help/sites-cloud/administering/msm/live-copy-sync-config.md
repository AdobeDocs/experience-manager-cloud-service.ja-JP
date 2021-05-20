---
title: ライブコピーの同期の設定
description: 使用可能な強力なライブコピー同期オプションと、プロジェクトのニーズに合わせてライブコピーを設定およびカスタマイズする方法について説明します。
feature: マルチサイトマネージャー
role: Administrator
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 32%

---

# ライブコピーの同期の設定 {#configuring-live-copy-synchronization}

Adobe Experience Managerには、すぐに使用できる多数の同期設定が用意されています。 ライブコピーを使用する前に、次の点を考慮して、ライブコピーとソースコンテンツの同期方法と同期のタイミングを定義する必要があります。

1. 既存のロールアウト設定が要件を満たしているかどうかを判断する
1. 既存のロールアウト設定がない場合は、独自のロールアウト設定を作成する必要があるかどうかを決定します。
1. ライブコピーに使用するロールアウト設定を指定します。

## インストールされるロールアウト設定とカスタムロールアウト設定 {#installed-and-custom-rollout-configurations}

ここでは、インストールされるロールアウト設定、それらの設定で使用する同期アクションおよびカスタム設定の作成方法（必要な場合）に関する情報を示します。

>[!CAUTION]
>
>標準のロールアウト設定を更新または変更することは、**お勧めしません**。 カスタムライブアクションの要件がある場合は、カスタムロールアウト設定に追加する必要があります。

### ロールアウトトリガー {#rollout-triggers}

各ロールアウト設定では、ロールアウトトリガーを使用してロールアウトを発生させます。ロールアウト設定では、以下のいずれかのトリガーを使用できます。

* **ロールアウト時**:Rolloutコ **** マンドは、青い印刷ページで使用するか、ライブコピ **** ーページで同期コマンドを使用します。
* **変更時**:ソースページが変更されました。
* **アクティベート時**：ソースページがアクティベートされます。
* **アクティベート解除時**：ソースページがアクティベート解除されます。

>[!NOTE]
>
>**変更時**&#x200B;トリガーの使用は、パフォーマンスに影響を与える可能性があります。 詳しくは、[MSM のベストプラクティス](best-practices.md#onmodify)を参照してください。

### ロールアウト設定 {#rollout-configurations}

次の表に、AEMに標準で用意されているロールアウト設定を示します。 表には各ロールアウト設定のトリガーと同期アクションが含まれます。

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| 名前 | 説明 | トリガー | [同期アクション](#synchronization-actions) |
|---|---|---|---|
| 標準のロールアウト設定 | ロールアウト設定時にロールアウトプロセスを開始し、アクションを実行する標準のトリガーコンテンツの作成、更新、削除、子ノードの並べ替え | ロールアウト時 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| ブループリントのアクティベート時にアクティベート | ソースが公開されたときにライブコピーを公開します | アクティベート時 | `targetActivate` |
| ブループリントのアクティベート解除時にアクティベート解除 | ソースが非アクティブ化された場合にライブコピーを非アクティブ化します | 非アクティブ化時 | `targetDeactivate` |
| 変更時にプッシュ | ソースが変更されたときに、コンテンツをライブコピーにプッシュします。<br>このロールアウト設定は、変更時トリガーを使用するので、慎重に使用してください。 | 変更時 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| 変更時にプッシュ (シャロー) | 参照を更新する（シャローコピーの場合など）ことなく、ブループリントページが変更されたときに、ライブコピーにコンテンツをプッシュします。<br>このロールアウト設定は、「変更時」トリガーを使用するので、慎重に使用します。 | 変更時 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| ローンチを昇格 | ローンチページを昇格するための標準のロールアウト設定。 | ロールアウト時 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### 同期アクション{#synchronization-actions}  

次の表に、AEMに標準で用意されている同期アクションを示します。

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| アクション名 | 説明 | プロパティ |
|---|---|---|
| `contentCopy` | ソースのノードがライブコピーに存在しない場合、このアクションはノードをライブコピーにコピーします。 [ **CQ MSM Content Copy Actionserviceを設定** ](#excluding-properties-and-node-types-from-synchronization) して、除外するノードタイプ、段落項目およびページプロパティを指定します。 |  |
| `contentDelete` | このアクションは、ソースに存在しないライブコピーのノードを削除します。 [ **CQ MSM Content Delete Actionserviceを設定** ](#excluding-properties-and-node-types-from-synchronization) して、除外するノードタイプ、段落項目およびページプロパティを指定します。 |  |
| `contentUpdate` | この操作により、ライブコピーのコンテンツがソースの変更で更新されます。 [ **CQ MSM Content Update Actionserviceを設定** ](#excluding-properties-and-node-types-from-synchronization) して、除外するノードタイプ、段落項目およびページプロパティを指定します。 |  |
| `editProperties` | このアクションは、ライブコピーのプロパティを編集します。 `editMap`プロパティは、編集するプロパティとその値を決定します。 `editMap`プロパティの値は、<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value`と`new_value`の形式を使用する必要があります。`n`は増分された整数です。<br>例えば、次の値を考えてみま `editMap`す。<br>`sling:resourceType#/(contentpage`この値では、ライブコピーノードのプロパティを次のように編集します。`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>またはに設定され<br>るプロパティは、 `sling:resourceType` に設定されま `contentpage`  `homepage`  `mobilecontentpage`す。<br>に設 `cq:template` 定するプロパティ `contentpage` はに設定されま `mobilecontentpage`す。 | `editMap: (String)` プロパティ、現在の値、新しい値を識別します。詳しくは、説明を参照してください。 |
| `notify` | このアクションは、ページがロールアウトされたページイベントを送信します。 通知が送信されるようにするには、最初にロールアウトイベントを購読する必要があります。 |  |
| `orderChildren` | このアクションは、ブループリントの順序に基づいて子ノードを並べ替えます。 |  |
| `referencesUpdate` | この同期アクションは、ライブコピー上の参照を更新します。<br>ライブコピーページ内で、ブループリント内のリソースを指すパスを検索します。見つかると、ライブコピー内の関連リソースを指すようにパスが更新されます。 ブループリント外のターゲットを持つ参照は変更されません。<br>[CQ MSM References Update Actionserviceを設 **定して、除外** ](#excluding-properties-and-node-types-from-synchronization) するノードタイプ、段落項目およびページプロパティを指定します。 |  |
| `targetVersion` | この操作により、ライブコピーのバージョンが作成されます。<br>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。 |  |
| `targetActivate` | この操作により、ライブコピーがアクティベートされます。<br>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。 |  |
| `targetDeactivate` | この操作により、ライブコピーが非アクティブ化されます。<br>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。 |  |
| `workflow` | このアクションは、ターゲットプロパティで定義されたワークフローを開始し（ページの場合のみ）、ライブコピーをペイロードとして取ります。<br>ターゲットパスは、モデルノードのパスです。 | `target: (String)` は、ワークフローモデルへのパスです。 |
| `mandatory` | このアクションは、ライブコピーページ上の複数のACLの権限を、特定のユーザーグループに対して読み取り専用に設定します。 次のACLが設定されています。<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>このアクションはページに対してのみ使用します。 | `target: (String)` は、権限を設定するグループのIDです。 |
| `mandatoryContent` | このアクションは、ライブコピーページ上の複数のACLの権限を、特定のユーザーグループに対して読み取り専用に設定します。 次のACLが設定されています。<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>このアクションはページに対してのみ使用します。 | `target: (String)` は、権限を設定するグループのIDです。 |
| `mandatoryStructure` | このアクションは、ライブコピーページ上の`ActionSet.ACTION_NAME_REMOVE` ACLの権限を、特定のユーザーグループに対して読み取り専用に設定します。<br>このアクションはページにのみ使用してください。 | `target: (String)` は、権限を設定するグループのIDです。 |
| `VersionCopyAction` | ブループリント/ソースページが少なくとも1回公開されている場合、このアクションは、公開されているバージョンを使用してライブコピーページを作成します。 注意：このアクションは、公開されたソースページに基づくライブコピーページの作成にのみ使用でき、既存のライブコピーページの更新には使用できません。 |  |
| `PageMoveAction` | `PageMoveAction`は、ページがブループリント内に移動された場合に適用されます。<br>アクションは、（関連する）ライブコピーページを移動前の場所から移動後の場所に移動するのではなく、コピーします。<br>は、 `PageMoveAction` 移動前の場所にあるライブコピーページを変更しません。したがって、連続したロールアウト設定の場合、ブループリントのないライブ関係のステータスになります。<br>[**** CQ MSM Page Move Action サービスを設定](#excluding-properties-and-node-types-from-synchronization)して、除外するノードタイプ、段落項目およびページプロパティを指定してください。<br>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。 | `prop_referenceUpdate: (Boolean)`をtrue（デフォルト）に設定すると、参照が更新されます。 |
| `markLiveRelationship` | このアクションローンチが作成したコンテンツにライブ関係が存在することを示します。 |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### プロパティとノードタイプの同期からの除外 {#excluding-properties-and-node-types-from-synchronization}

対応する同期アクションをサポートする複数のOSGiサービスを設定して、特定のノードタイプやプロパティに影響を与えないようにすることができます。例えば、AEMの内部機能に関連する多くのプロパティやサブノードを、ライブコピーに含めないでください。 ページのユーザーに関連するコンテンツのみをコピーする必要があります。

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳細および推奨事項については、[OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。

以下の表は、除外するノードを指定できる同期アクションを示しています。この表には、Web コンソールを使用して設定する場合のサービスの名前とリポジトリノードを使用して設定する場合の PID が示されています。

| 同期アクション | Web コンソールでのサービス名 | サービス PID |
|---|---|---|
| `contentCopy` | CQ MSM Content Copy Action | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM Content Delete Action | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM Content Update Action | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM Page Move Action | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM References Update Action | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

次の表は、設定可能なプロパティを示しています。

| Web コンソールのプロパティ | OSGi のプロパティ | 説明 |
|---|---|---|
| 除外されたノードタイプ | `cq.wcm.msm.action.excludednodetypes` | 同期アクションから除外するノードタイプに一致する正規表現 |
| Excluded Paragraph Items | `cq.wcm.msm.action.excludedparagraphitems` | 同期アクションから除外する段落項目に一致する正規表現 |
| Excluded Page Properties | `cq.wcm.msm.action.excludedprops` | 同期アクションから除外するページプロパティに一致する正規表現 |
| Ignored Mixin NodeTypes | `cq.wcm.msm.action.ignoredMixin` | 同期アクションから除外するmixinノードタイプの名前に一致する正規表現（`contentUpdate`アクションでのみ使用可能） |

#### CQ MSM Content Update Action - 除外 {#cq-msm-content-update-action-exclusions}

いくつかのプロパティやノードタイプはデフォルトで除外されています。これらは **CQ MSM Content Update Action** の OSGi の設定の、**Excluded Page Properties** の下に定義されています。

デフォルトでは、次の正規表現に一致するプロパティがロールアウト時に除外されます（更新されません）。

![ライブコピーの除外範囲](../assets/live-copy-exclude.png)

必要に応じて、除外リストを定義する表現を変更できます。

例えば、ロールアウトで考慮される変更にページ&#x200B;**タイトル**&#x200B;を含めるには、除外から `jcr:title` を削除します。正規表現は次のようになります。

`jcr:(?!(title)$).*`

### 参照を更新するための同期の設定 {#configuring-synchronization-for-updating-references}

参照の更新に関連する、対応する同期アクションをサポートする複数の OSGi サービスを設定できます。

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳細および推奨事項については、[OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。

次の表は、参照の更新を指定できる同期アクションを示します。この表には、Web コンソールを使用して設定する場合のサービスの名前とリポジトリノードを使用して設定する場合の PID が示されています。

| Web コンソールのプロパティ | OSGi のプロパティ | 説明 |
|---|---|---|
| Update Reference across nested LiveCopies | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Webコンソールでこのオプションを選択するか、リポジトリ設定を使用して`true`に設定し、最上位のライブコピーのブランチ内にあるリソースをターゲットとする参照を置き換えます。 `referencesUpdate`アクションでのみ使用できます。 |
| Update Referencing Pages | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Webコンソールでこのオプションを選択するか、リポジトリ設定を使用してこのブール値プロパティを`true`に設定し、元のページを使用する参照を更新して、ライブコピーページを参照します。 `PageMoveAction`でのみ使用できます。 |

## 使用するロールアウト設定の指定 {#specifying-the-rollout-configurations-to-use}

MSMを使用すると、一般に使用されるロールアウト設定のセットを指定でき、必要に応じて、特定のライブコピー用にそれらを上書きできます。MSMには、使用するロールアウト設定を指定する場所が複数用意されています。場所によって、設定が特定のライブコピーに適用されるかどうかが決まります。

使用するロールアウト設定を指定できる場所を以下に示します。ここでは、MSMがライブコピーに使用するロールアウト設定を決定する方法について説明します。

* **[ライブコピーページのプロパティ](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** 1つ以上のロールアウト設定を使用するようにライブコピーページが設定されている場合、MSMはそれらのロールアウト設定を使用します。
* **[ブループリントページのプロパティ](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** ライブコピーがブループリントに基づいており、ライブコピーページがロールアウト設定で設定されていない場合は、ブループリントソースページに関連付けられているロールアウト設定が使用されます。
* **ライブコピーの親ページのプロパティ：** ライブコピーページもブループリントソースページもロールアウト設定で設定されていない場合は、ライブコピーページの親ページに適用されるロールアウト設定が使用されます。
* **[システムのデフォルト](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** ライブコピーの親ページのロールアウト設定を判断できない場合は、システムのデフォルトのロールアウト設定が使用されます。

例えば、ブループリントでは、[WKNDチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)サイトをソースコンテンツとして使用します。 サイトはブループリントから作成されます。次のリスト内の各項目は、ロールアウト設定の使用に関する様々なシナリオを示しています。

* ロールアウト設定を使用するようにブループリントページやライブコピーページが設定されていない。MSMでは、すべてのライブコピーページに対してシステムのデフォルトのロールアウト設定を使用します。
* WKNDサイトのルートページは、複数のロールアウト設定を使用して設定します。 MSMは、すべてのライブコピーページに対してこれらのロールアウト設定を使用します。
* WKNDサイトのルートページは複数のロールアウト設定で設定され、ライブコピーサイトのルートページは別のロールアウト設定で設定されます。 MSMは、ライブコピーサイトのルートページで設定されたロールアウト設定を使用します。

### ライブコピーページ用のロールアウト設定の指定 {#setting-the-rollout-configurations-for-a-live-copy-page}

ソースページがロールアウトされたときに使用するロールアウト設定を含むライブコピーページを設定します。 デフォルトでは、子ページは設定を継承します。使用するロールアウト設定を指定する際に、ライブコピーページが親から継承する設定を上書きします。

[ライブコピー](creating-live-copies.md#creating-a-live-copy-of-a-page)の作成時に、ライブコピーページのロールアウト設定を指定することもできます。

1. **サイト**&#x200B;コンソールを使用して、ライブコピーページを選択します。
1. ツールバーの「**プロパティ**」を選択します。
1. 「**ライブコピー**」タブを開きます。

   「**設定**」セクションには、ページが継承するロールアウト設定が表示されます。

   ![親ページからのライブコピーの継承](../assets/live-copy-inherit.png)

1. 必要に応じて、「**ライブコピーの継承**」フラグを変更します。オンにすると、ライブコピー設定がすべての子に対して有効になります。

1. 「**ロールアウト設定を親から継承**」プロパティをオフにして、1 つ以上のロールアウト設定をリストから選択します。

   選択したロールアウト設定がドロップダウンリストの下に表示されます。

   ![ライブコピー設定の継承の上書き](../assets/live-copy-inherit-override.png)

1. 「**保存して閉じる**」をクリックまたはタップします。

### ブループリントページ用のロールアウト設定の指定 {#setting-the-rollout-configuration-for-a-blueprint-page}

ブループリントページがロールアウトされる場合に使用するロールアウト設定を使用してブループリントページを設定します。

ブループリントページの子ページがその設定を継承します。使用するロールアウト設定を指定する場合は、ページがその親から継承する設定を上書きできます。

1. **サイト**&#x200B;コンソールを使用して、ブループリントのルートページを選択します。
1. ツールバーの「**プロパティ**」を選択します。
1. 「**ブループリント**」タブを開きます。
1. ドロップダウンセレクターを使用して&#x200B;**ロールアウト設定**&#x200B;を 1 つ以上選択します。
1. 「**保存**」を選択して更新内容を保持します。

### システムのデフォルトのロールアウト設定の指定 {#setting-the-system-default-rollout-configuration}

システムのデフォルトとして使用するロールアウト設定を指定するには、次のOSGiサービスを設定します。

* **Day CQ WCM Live Relationship Manager(サ** ービスPIDを使用)  `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

[Webコンソール](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または[リポジトリノード](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を使用して、サービスを設定します。

* Webコンソールでは、設定するプロパティの名前は&#x200B;**デフォルトのロールアウト設定**&#x200B;です。
* リポジトリノードを使用する場合、設定するプロパティの名前は`liverelationshipmgr.relationsconfig.default`です。

このプロパティの値を、システムのデフォルトとして使用するロールアウト設定のパスに指定します。デフォルト値は`/libs/msm/wcm/rolloutconfigs/default`で、**標準のロールアウト設定**&#x200B;です。
