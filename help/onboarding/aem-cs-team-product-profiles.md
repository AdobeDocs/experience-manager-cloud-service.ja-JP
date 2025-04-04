---
title: AEM as a Cloud Service チームおよび製品プロファイル
description: AEM as a Cloud Service チームおよび製品プロファイルでライセンス取得済みアドビソリューションへのアクセスを許可および制限する方法について説明します。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 86bb2e020a003fd418f8b1cf7bdf55987a2eaf3d
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 98%

---


# AEM as a Cloud Service チームおよび製品プロファイル {#product-profiles}

AEM as a Cloud Service チームおよび製品プロファイルでライセンス取得済みアドビソリューションへのアクセスを許可および制限する方法について説明します。

## 製品プロファイル {#profiles}

特定のアドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、ソリューションごとに独自のユーザー権限を設定できます。これらのプロファイルは、[ Admin Console](/help/journey-onboarding/admin-console.md) を通じて使用でき、アクセスできます。

Adobe Admin Console には、製品、製品インスタンス、製品プロファイルの構造化された階層があり、組織の内部ユーザーにメンバーシップを割り当てて、ライセンス済みソリューションや機能にアクセスできます。

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service 製品プロファイル {#aem-product-profiles}

AEM as a Cloud Service は、AEM をサービスとして提供する、完全にクラウドネイティブな製品です。常時稼動で、常に最新、常に安全、常にスケーラブルといった新しい属性を備えた AEM をクラウドネイティブな方法で提供します。それと同時に、カスタマイズ可能なプラットフォームとしての AEM の価値を維持し、エンタープライズクラスのチームが開発および配信の手順に統合することができます。AEM as a Cloud Service について詳しくは、[Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)を参照してください。

### 組織レベルの製品インスタンス {#org-level-product-instances}

>[!NOTE]
>
> この記事で説明する製品インスタンスと製品プロファイルの一部は、新しく作成した環境にのみ表示される場合があります。環境を最新化する方法については、[ 既存環境の製品プロファイルの追加 ](#adding-product-profiles-for-existing-environments) の節を参照してください。

アドビが初めて AEM ソリューションのライセンスを処理すると、Adobe Admin Console の Adobe Experience Manager as a Cloud Service 製品の下に次の 2 つの製品インスタンスが表示されます。

* **AEM 組織レベル** - 1 つの AEM 環境だけでなく、すべての AEM 環境に適用される機能へのアクセスを表す 1 つ以上の製品プロファイルが含まれます。
* **Cloud Manager** - Cloud Manager 機能への様々なアクセスレベルに対応する製品プロファイルが含まれます。

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![組織レベルの製品インスタンス](/help/onboarding/assets/orglevel.png)

AEM 組織レベルの製品インスタンス内には、AEM 組織レベルのレポーターという名前の製品プロファイルがあります。これは、現時点では使用されていませんが、今後 AEM 製品ライセンスに関する情報を取得するアクセスを表すのに使用される可能性があります。

Forms コミュニケーションソリューションのライセンスが付与されると、対応する製品プロファイルが AEM 組織レベルの製品インスタンスの下にも表示されます。

![レポーターの製品プロファイル](/help/onboarding/assets/org-level-reporters.png)

### 環境および階層レベルの製品インスタンス {#environment-and-tier-level-product-instances}

1 つ以上の AEM 環境で新しいプログラムをプロビジョニングすると、環境ごとに 2 つの製品インスタンスが表示され、それぞれにオーサー用とパブリッシュ用の製品プロファイルが含まれます。

![環境の製品インスタンス](/help/onboarding/assets/env-productinstances.png)

AEM Sites を含むプログラムで環境をプロビジョニングした組織のオーサー製品インスタンス内の製品プロファイルを以下に示します。

![Sites の製品インスタンス](/help/onboarding/assets/sites-product-instances.png)

次の表に、環境層固有の製品インスタンスの下にある使用可能な製品プロファイルのリストを示します。

<table style="table-layout:auto">
    <tr>
        <th>製品インスタンス</th>
        <th>命名規則</th>
        <th>デフォルトのサービス</th>
        <th>説明</th>
    </tr>
    <tr>
        <td>AEM オーサー</td>
        <td>AEM Sites コンテンツマネージャー - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Sites コンテンツマネージャー</td>
        <td>
            <ul>
                <li>この環境上の AEM Sites オーサー機能への制御されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM Sites コンテンツ作成者 AEM グループのメンバーになります。AEM グループの権限は、目的のアクセスレベルを使用して AEM で設定する必要があります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM Sites コンテンツマネージャー - サービス」AEM グループのメンバーにもなります。</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 管理者 - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 管理者</td>
        <td>
            <ul>
                <li>AEM オーサーおよびパブリッシュ環境機能への無制限のアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM 管理者作成者 AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM 管理者 - サービス」AEM グループのメンバーにもなります</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM ユーザー - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM ユーザー</td>
        <td>
            <ul>
                <li>AEM オーサー環境機能への非常に限定されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される「寄稿者」AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM ユーザー - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM レポーター - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM レポーター</td>
        <td>
            <ul>
                <li>現在は使用されていませんが、今後、この環境のオーサー層に関するレポート情報へのアクセスが提供される可能性があります。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets 共同作業者 - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Assets 共同作業者ユーザー</td>
        <td>
        <ul>
                <li>DAM への読み取り専用アクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される「寄稿者」AEM グループのメンバーになります。
                </li>
                <li>
                また、アセットのバリエーションを作成する Adobe Express 権限も提供します。
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets パワーユーザー - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Assets パワーユーザー</td>
<td>
        <ul>
                <li>DAM への読み取り専用アクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される「寄稿者」AEM グループのメンバーになります。
                </li>
                <li>
                また、アセットのバリエーションを作成する Adobe Express 権限も提供します。
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms コンテンツマネージャー - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms コンテンツマネージャー</td>
        <td>
            <ul>
                <li>この環境上の AEM Forms オーサー機能への制御されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM Forms forms-users AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM Forms コンテンツマネージャー - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 開発者 - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms 開発者</td>
        <td>
            <ul>
                <li>この環境上の AEM Forms オーサー機能への制御されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM Forms forms-power-users AEM グループのメンバーになります。これらのユーザーには、通常のフォーム作成タスクに加えて、XDP をアップロードし、フォームデータモデルを作成する権限もあります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM Forms 開発者 - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms コミュニケーションサービスユーザー - オーサー - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms コミュニケーションサービスユーザー</td>
        <td>
            <ul>
                <li>この環境上の AEM Forms コミュニケーションサービス機能への制御されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM Forms forms-users AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM Forms コミュニケーションサービスユーザー - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM パブリッシュ</td>
        <td>AEM ユーザー - パブリッシュ - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM ユーザー</td>
        <td>
            <ul>
                <li>AEM オーサー環境機能への非常に限定されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される「寄稿者」AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM ユーザー - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM レポーター - パブリッシュ - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM レポーター</td>
        <td>
            <ul>
                <li>現在は使用されていませんが、今後、この環境のパブリッシュ層に関するレポート情報へのアクセスが提供される可能性があります。</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms コミュニケーションサービスユーザー - パブリッシュ - プログラム <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms コミュニケーションサービスユーザー</td>
        <td>
            <ul>
                <li>この環境上の AEM Forms コミュニケーションサービス機能への制御されたアクセスを目的としています。この製品プロファイルのユーザーは、AEM で自動的に作成される AEM Forms forms-users AEM グループのメンバーになります。</li><br>
                <li>デフォルトのサービスが選択されたままの場合
                    <ul>
                        <li>この製品プロファイルのユーザーは、「AEM Forms コミュニケーションサービスユーザー - サービス」AEM グループのメンバーにもなります。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

各製品プロファイルには、関連付けられた製品プロファイルサービスがデフォルトで有効になっています。複雑なアクセス要件がない限り、デフォルトのサービスのみを選択したままにしておくことをお勧めします。対応する AEM グループが、命名規則 `<Product Profile Prefix> - Service`（例：**AEM Sites コンテンツマネージャー - サービス**）を使用して AEM 内に作成され、親製品プロファイル内のユーザーは自動的にその対応する AEM グループのメンバーになります。

サービスに関連付けられた AEM 内の AEM グループには、その環境と層の組み合わせに対して、そのサービスに関連付けられたすべての製品プロファイルに存在するユーザーの集計セットが含まれます。

![サービス](/help/onboarding/assets/services.png)

次の画像は、AEM Sites コンテンツマネージャーのオーサー層の製品プロファイルとサービスを反映した AEM グループを表しています。

![AEM グループからサービスへのマッピング](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>AEM as a Cloud Service の製品プロファイルに割り当てられたすべてのユーザーは、**Cloud Manager ユーザー**&#x200B;の役割を介して Cloud Manager に読み取り専用でアクセスできます。
>
>**Cloud Manager ユーザー**&#x200B;の役割のみを持つユーザーは、Cloud Manager にログインし、**プログラム**&#x200B;メニューオプションを使用して AEM オーサー環境（存在する場合）に移動できます。**Cloud Manager ユーザー**&#x200B;の役割では、プログラムの詳細にアクセスするのに十分ではありません。 そのようなアクセスが必要な場合は、システム管理者から追加の役割を付与してもらう必要があります。

>[!WARNING]
>
>**AEM 管理者**&#x200B;の製品プロファイル名は変更しないでください。**AEM 管理者**&#x200B;製品プロファイルの名前を変更すると、そのプロファイルに割り当てられているすべてのユーザーから管理者権限が削除されます。

>[!TIP]
>
>* AEM 製品プロファイルについて詳しくは、[AEM 製品プロファイルの割り当て](/help/journey-onboarding/assign-profiles-aem.md)を参照してください。
>* オンボーディングプロセスについて詳しくは、[オンボーディングジャーニー](/help/journey-onboarding/overview.md)を参照してください。

### 既存の環境に対する製品プロファイルの追加 {#adding-product-profiles-for-existing-environments}

2024 年 4 月上旬より前に作成された環境では、上記の節で説明した組織レベルの製品インスタンスおよび特定の製品プロファイルが欠落している可能性があります。 また、既存の製品プロファイルの場合はサービス切替スイッチもありません。今後の API にアクセスするための前提条件となる、これらの製品プロファイルを更新することをお勧めします。

プログラム内の 1 つ以上の環境で製品プロファイルを更新する必要がある場合、Cloud Manager に以下の通知が表示されます。製品プロファイルを更新する前に、環境を最新の AEM バージョンにする必要があります。

![製品プロファイルの最新化](/help/onboarding/assets/modernize-product-profiles.png)

「**製品プロファイルを追加**」ボタンをクリックすると、プログラムで使用可能なすべての環境または個別の環境に新しい製品プロファイルを追加するオプションを表示するメニューが開きます。

![環境の置換](/help/onboarding/assets/choose-env-r.png)

「**すべての環境**」をクリックして、プログラム内のすべての環境に新しい製品プロファイルを追加します。または、「**個別の環境**」をクリックして、選択した新しい製品プロファイルを環境に追加します。これにより、ユーザーは環境リストページに移動し、**その他のオプション**&#x200B;アイコンから「**製品プロファイルを追加**」アクションを選択できます。

![個別の環境](/help/onboarding/assets/individual-environments.png)

また、製品概要ページの「環境」セクションに移動し、環境に対応するその他のオプションアイコンをクリックし、「製品プロファイルを追加」を選択して、選択した環境に製品プロファイルを追加することもできます。

新しい製品プロファイルが追加されている間は、環境のステータスに「製品プロファイルを追加中」、プロセスが完了すると「実行中」と表示されます。


## Cloud Manager 製品プロファイル {#cloud-manager-product-profiles}

Cloud Manager には、役割ベースの権限と考えられる事前設定済み製品プロファイルがあります。 Cloud Manager チームをこれらの製品プロファイルに割り当てて設定するのは、システム管理者の仕事です。

>[!TIP]
>
>詳しくは、[Cloud Manager での役割に基づく権限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)を参照してください。

それぞれの製品プロファイルには、固有の権限が関連付けられています。

* **ビジネスオーナー**
   * この役割には、新しいプログラムの追加、プログラムの編集、環境の追加または更新、AEM 環境へのコードのデプロイ、コード品質チェックの実行などを行う権限があります。
   * このユーザーは、KPI の定義、実稼動デプロイメントの承認および必要に応じて重要な 3 層エラーの上書きを担当します。
* **デプロイメントマネージャー**
   * この役割には、環境の追加または更新、任意のパイプラインの実行、AEM 環境へのコードのデプロイ、コード品質チェックの実行などを行う権限があります。
   * このユーザーは、デプロイメント操作を管理、Cloud Manager を使用してステージング環境または実稼動環境のデプロイメントを実行、CI／CD パイプラインを編集、必要に応じて重要な 3 層エラーを承認、Git リポジトリにアクセスできます。
* **開発者**
   * この役割には、Git にアクセスするための個人用アクセストークンを生成する権限があります。
   * このユーザーは、カスタムアプリケーションコードの開発およびテストを担当し、主に Cloud Manager を使用してデプロイメントステータスを表示し、コードコミットの Git リポジトリにアクセスできます。
* **プログラムマネージャー**
   * この役割には、パイプラインのスケジュール設定、3 層品質ゲートのオーバーライド、実稼動の承認などを行う権限があります。
   * このユーザーは Cloud Manager を使用して、チームの設定を実行、ステータスを確認、KPI を表示し、必要に応じて重大な 3 層エラーを承認できます。

1 人のユーザーを複数の製品プロファイルに割り当てることができます。例えば、**ビジネスオーナー**&#x200B;と&#x200B;**デプロイメントマネージャー**&#x200B;の両方の役割を 1 人のユーザーに割り当てると、これらの権限の組み合わせ（総和）が付与されます。

Cloud Manager チームには、少なくとも次の役割が含まれています。

* 1 人の&#x200B;**ビジネスオーナー**。通常はシステム管理者も兼ねており、Cloud Manager にログインしてアクセスする最初のユーザーでなければなりません
* 1 人の&#x200B;**デプロイメントマネージャー**
* 1 人の&#x200B;**デベロッパー**

>[!NOTE]
>
>ユーザーに AEM as a Cloud Service へのアクセスを許可するには、ユーザーが「`AEM Users`」または「`AEM Administrators`」のどちらかの製品プロファイルに属している必要があります。Cloud Manager を管理する権限では不十分です。

>[!TIP]
>
>* Cloud Manager 製品プロファイルについて詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/assign-profiles-cloud-manager.md)を参照してください。
>* オンボーディングプロセスについて詳しくは、[オンボーディングジャーニー](/help/journey-onboarding/overview.md)を参照してください。
