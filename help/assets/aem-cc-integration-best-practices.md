---
title: ' [!DNL Adobe Creative Cloud] との統合のベストプラクティス'
description: Experience Manager デプロイメントを Adobe Creative Cloud と統合して、アセット転送ワークフローを効率化し、効率を最大限に高めるためのベストプラクティス。
contentOwner: AG
mini-toc-levels: 1
feature: 共同作業、アドビのアセットリンク、デスクトップアプリ
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 09aecfac8bab0377e9e777b80e7db986d7aa4914
workflow-type: tm+mt
source-wordcount: '3451'
ht-degree: 57%

---

#  Experience Manager と Adobe Creative Cloud の統合のベストプラクティス {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager Assetsは、Adobe Creative Cloudと統合して、DAMユーザーがクリエイティブチームと連携し、コンテンツ作成プロセスでのコラボレーションを合理化する、デジタルアセット管理(DAM)ソリューションです。

Adobe Creative Cloud は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。これには、デスクトップおよびモバイルアプリケーション、デスクトップ同期や Web エクスペリエンスを備えたストレージなどのクラウドサービス、および Adobe Stock などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>Creative Cloudフォルダー共有のExperience Managerは廃止され、以下では扱われなくなりました。 Adobeは、Adobeで管理されたアセットへのアクセス権をクリエイティブユーザーに与える、Experience ManagerアセットリンクやExperience Managerデスクトップアプリケーションなどの新しい機能を推奨します。

## クリエイティブプロフェッショナル、マーケティング担当者、DAM ユーザーのコラボレーションニーズ {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル、またはネイティブのアセット作成アプリケーションで作業するデスクトップユーザー向けに、DAM([!DNL Assets])からのアセットへのアクセスを合理化します。 Experience Managerの検出、使用（開く）、編集、変更の保存、新しいファイルのアップロードを簡単かつ簡単におこなう方法が必要です。 | Windows または Mac デスクトップ、Creative Cloud アプリ |
| [!DNL Adobe Stock]から高品質で使いやすいアセットを提供する | マーケティング担当者は、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Assets]; [!DNL Adobe Stock] marketplace;メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| アップロードしたアセットの事前定義済みバリエーションを自動的に生成する | 事前に定義されたアクションに対して、Adobe固有のメディア処理および変換テクノロジーを利用してアセットを自動的に処理します。 カスタムロジックを作成し、APIとアセットマイクロサービスを使用して独自のアクションを定義します。 | [!DNL Assets] ユーザーインターフェイス |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Experience Manager]からアセットを検出し、開いて使用し、[!DNL Experience Manager]に変更を編集してアップロードし、[!DNL Creative Cloud]アプリを離れることなく[!DNL Experience Manager]に新しいファイルをアップロードします。 | [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator、InDesign. |
| ビジネスユーザーは、アセットの開封と使用、編集と[!DNL Experience Manager]への変更のアップロード、デスクトップ環境から[!DNL Experience Manager]への新しいファイルのアップロードを簡単におこなえます。 汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) | WindowsおよびMac OSデスクトップ上のExperience Managerデスクトップアプリケーション |
| マーケターとビジネスユーザーは、Adobe Analytics内からAdobe Stockアセットを検出、プレビュー、ライセンス、保存およびExperience Managerします。 ライセンスを取得し保存したアセットは、限定された Adobe Stock メタデータを提供してガバナンスの強化に役立ちます。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] webインターフェイス |
| デジタル製品デザイナーとマーケターのコラボレーションを強化 Adobe XDキャンバス上のデザインとワイヤフレームモデルで、デザイナーがデジタルアセットを使用できるようにします。 | [[!DNL Adobe Asset Link] （ [!DNL Adobe XD] 用）](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| マーケターは、アップロードされたアセットと、カスタマイズを使用して作成された事前定義済みのアクションに基づいて、バリエーションと派生物を自動的に作成できます。 この自動化機能を使用して、コンテンツの速度を向上させ、手作業を軽減します。 | [コンテンツの自動化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] webインターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。代替ソリューション([Experience ManagerAssets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)、[Asset Share Commons](https://opensource.adobe.com/asset-share-commons/)コンポーネントに基づいて構築できるソリューション、[リンク共有](share-assets.md)、[Experience ManagerアセットWeb UI](/help/assets/manage-digital-assets.md)を使用するソリューションなど)については、それぞれ固有の要件に基づいて検討する必要があります。

![Creative CloudのExperience Manager:使用する機能の決定](assets/creative-connections-aem.png)

使用する機能の決定

### 使用例とアドビソリューションの対応関係 {#mapping-of-use-cases-and-adobe-solutions}

| 使用例 | Adobe Asset Link | Experience Manager デスクトップアプリ | 備考または代替手段 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 検出 — フォルダーの参照 | ○ | Experience ManagerWeb UI +デスクトップアクション | ネットワーク共有を参照する場合は、アセットのバイナリファイルをダウンロードしないように、サムネールをオフにします。 |
| Discover — コレクションへのアクセス | ○ | Experience ManagerWeb UI +デスクトップアクション |  |
| Discover — アセットの検索 | ○ | Experience ManagerWeb UI +デスクトップアクション |  |
| 使用 - アセットを開く | 対応 | 対応 - 任意のアプリに対して | 「[Web インターフェイスから開く](/help/assets/manage-digital-assets.md#previewing-assets)」またはファインダーから開く |
| 使用 — アセットからドキュメントへのExperience Managerの配置 | 対応 - 埋め込み | 対応 - リンクまたは埋め込み | Experience Managerデスクトップアプリケーションでは、ローカルファイルシステム上のファイルとしてアセットにアクセスできます。 ネイティブアプリでは、これらのリンクはローカルパスで表されます。 |
| 編集 - 編集用に開く | 対応 - チェックアウトアクション | 対応 - 「開く」アクション（ネットワーク共有内） | 「[AAL でチェックアウト](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)」の場合は、デフォルトでは、アセットをユーザーの Creative Cloud ストレージアカウント（Creative Cloud アプリで同期）に保存します。 |
| 編集 —Experience Manager外で作業中 | 対応 - デスクトップに同期しているユーザーの Creative Cloud ストレージアカウントでアセットが入手可能です。 | 対応 |  |
| 編集 - 変更をアップロードする | 対応 - [チェックインアクション](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)（オプションコメント付き） | 対応 |  |
| アップロード - 単一ファイル | 対応 - 現在のアクティブなドキュメントをアップロードします | 対応 | [Web インターフェイスを使用してアップロード](/help/assets/manage-digital-assets.md#uploading-assets) |
| アップロード - 複数ファイル／階層フォルダー構造 | 非対応 | 対応 | [Web インターフェイスを使用してアップロード](/help/assets/manage-digital-assets.md#uploading-assets)。カスタムスクリプティングまたはツール |
| その他 - ユーザーとログイン | Creative Cloud デスクトップアプリケーションにログインした Creative Cloud ユーザーが認識されます（SSO） | Experience Managerユーザー/ログイン | 両方のソリューションのユーザーは、Experience Manager・ユーザー・クォータに対してカウントされます。 |
| その他 - ネットワークとアクセス | ネットワークを介してユーザーのデスクトップからExperience Managerの導入にアクセスする必要がある | ネットワークを介してユーザーのデスクトップからExperience Managerの導入にアクセスする必要がある | Adobe Asset Link はネットワークプロキシ環境を共有しません。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

アセット配布の使用例をサポートするには、次のオプションを検討します。

* [Experience ManagerAssets Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal ：アセットを公開するための、Assetsへの設定可能なアドオン。

* カスタムソリューションは [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) のコードベースに基づいて作成される。
* Experience Manager[リンク共有](/help/assets/share-assets.md)を使用して、リンクを使用してアセットをアドホックで共有します。
* [Experience Managerのア](/help/assets/manage-digital-assets.md) クセス制御の設定で保護される外部の関係者向けのAssets Webインターフェイスと、必要なIT/ネットワーク設定の調整機能を備え、外部ユーザーがExperience Managerにアクセスできるようにします。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更がおこなわれている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：**&#x200B;より広範なチームと共有するための準備ができているアセット。または、マーケティングチームもしくは LOB チームと共有するためにクリエイティブチームによって選択／承認されているアセット。

* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての    承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。

* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するためにおこなわれます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り、Adobe Experience Manager（）Assets と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成はおこなわないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### Experience ManagerとCreative Cloudの統合を使用する際の考慮事項 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Experience ManagerとCreative Cloudの統合のベストプラクティスの概要です。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesignまたはIllustratorで作業しているクリエイティブユーザーの場合：** Adobeアセットリンクは、Experience Managerからチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：** Experience Managerデスクトップアプリケーションを使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### Adobe Stock AssetsからのExperience Managerへのアクセス {#access-to-adobe-stock-assets-from-aem-assets}

[Experience ManagerとAdobe Stockの統](/help/assets/aem-assets-adobe-stock.md) 合により、Experience ManagerユーザーはAdobe StockからExperience Managerにアセットを検索、プレビュー、ライセンス、保存できます。ライセンス取得され保存された Adobe Stock アセットには、限定された Stock メタデータが付いており、このメタデータを使用してアセットをさらに絞り込むことができます。

この統合に関するいくつかの重要な点を以下に示します。

* AdobeストックのアセットをExperience Managerに保存すると、アセットは通常のExperience Managerアセットになり、バイナリがExperience Managerリポジトリに保存されます。 Adobe Stockに関連する一部のメタデータは、Experience Manager内のアセット用に保存されます。それ以外の場合、取り込みプロセスは、他のファイルの場合と同じように見えます。 例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* Experience Managerに保存されたアセットは、Adobe Stockへのリンクではなく、コピーです。

**Adobe StockからCreative Cloud内のExperience Managerに保存されたアセットの操作**この統合は Adobe Asset Link とは無関係ですが、Adobe Asset Link では Stock から保存されたこれらのアセットをそのように認識し、Photoshop、Illustrator、InDesign の Adobe Asset Link 拡張 UI でこれらのアセットに追加のメタデータと Stock アイコンを表示します。ファイルは、Experience Managerに保存する際の通常のExperience Managerアセットなので、参照や開くなどに使用できます。
AdobeのAsset Link拡張機能が存在するCreative Cloudアプリで作業するクリエイティブユーザーは、Adobe StockからExperience Managerにライセンスが必要なアセットにアクセスできるほか、Creative Cloudライブラリパネルを使用してAdobe Stockアセットを検索、プレビュー、ライセンス取得できます。
Adobe Stockのアセットがライセンスされ、Experience Managerに保存された場合、Experience ManagerAssetsのデプロイメントにアクセスする広範なチームが利用できます。一方、Creative Cloudライブラリパネルを介してAdobe Stockのアセットをクリエイティブにライセンスする場合は、デフォルトでCreative Cloudアカウントでのみ利用できます。

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、ダウンストリームのマーケティング/LOBプロセスに関連するアセットのみを保存します(Experience Managerサイトや、Adobe Experience Cloud(Marketing Cloud、Advertising Cloud)が提供する他のチャネル、Analytics Cloudが提供するやパートナーなどに公開)。 また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

また、アセットを保存する場合、技術上およびリソース使用上でも考慮すべき点があります。DAM では、保存されたアセット関連の追加サービスが用意されています（メタデータの抽出、バージョン管理、プレビュー／トランスコーディングの生成、参照の管理およびアクセス制御情報の追加など）。これらのサービスを使用すると、追加の時間リソースおよびインフラストラクチャリソースが消費されます。

多くの場合、アセットおよび更新をすべて保存することは推奨されません。例えば、特定のアセットの更新の質が低く、大量のリソースを消費するような場合、そのアセットは DAM に保存しないようにします。

#### アセットを DAM に保存するタイミング {#when-assets-are-stored-in-dam}

クリエイティブチーム（および組織）は、通常、アセットのライフサイクルのステージごとにアセットを保存しようとは考えません。例えば、以下のような場合、アセットは保存されません。

* アセットがまだ最終決定されていない、またはテストが予定されている場合
* アセットがクリエイティブ／内部チームのレビューサイクルで不合格になった場合
* 問題のアセットに比べ、外部チームへの作業の説明に、より適したアセットがある場合

通常、以下のクラスのアセットが DAM に保存されます。

* 一定の成熟度に到達し、共有する準備ができたと判断されたアセット
* クリエイティブチームが事前に選択したアセット
* マーケティング部門が使用できる、または特定の契約や合意に応じて同部門から要求された、特定の形式のアセット（例えば、RAW ファイルから変換した JPG ファイル、PSD ファイルから作成した TIFF／画像ファイルなど）

#### アセットの更新を DAM に保存するタイミング {#when-updates-to-assets-are-stored-in-dam}

原則として、より広範な DAM ユーザーに関連するアセットの更新のみを DAM に保存するようにしてください。それにより、（マーケティングおよび類似の部門の）ユーザーの DAM アセットのタイムラインには、関連するバージョンのみが表示されます。

代表的な例としては、アセットのライフサイクルで主要なマイルストーンに関連する変更があります。例えば、最初のマーケティング用アセットや、クリエイティブチームからの要求／レビューに基づいた公式の更新などは、DAM に保存してバージョン管理する必要があります。

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームがおこなった更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備が完了する前に、アセットの最終版以外のバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームおよびマーケティングチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

Experience Managerアセットは、Assetsデプロイメントへのアクセス権に基づいて、2種類のExperience Managerをサポートします。 通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM に直接アクセスできます。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセスすることはできません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内のクリエイティブチームや、社内ネットワークに 内部ネットワークに転送された場合、Experience Managerログインを含むDAMインスタンスにアクセスできます。 Experience Managerとネットワークインフラストラクチャは、外部の関係者（通常、クライアントで作業するエージェンシーなどの信頼できる組織）に直接アクセスし、VPNやIP許可リストなどを介してネットワーク経由でExperience Managerにアクセスできるように設定できます。

このような場合、AdobeアセットリンクまたはExperience Managerデスクトップアプリケーションを使用すると、最終/承認済みアセットに簡単にアクセスし、クリエイティブレディアセットをDAMに保存できます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM インスタンスへの直接アクセス権を持たない外部のエージェンシーやフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

以下の戦略で最終／承認済みアセットへのアクセスを提供します。

* Asset Link が機能しない場合は、デスクトップアプリケーションを使用します。
* 外部パートナーに安全にExperience Managerを配布するには、[アセットAssets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)を使用します。
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) に基づいた、配布および調達用ポータルのカスタム実装を使用します。
* Experience Managerで設定されたアクセス制御と必要なネットワークインフラストラクチャ（VPNやIPの許可リストなど）を使用して、外部の関係者がDAM内のコンテンツの専用領域にアクセスできるようにします。 Experience ManagerのWeb UIを使用して、アセットを取得し、新しいコンテンツをDAMにアップロードできます。

#### Experience Manager {#work-in-progress-on-assets-from-aem}

このドキュメントで説明したように、ローカルファイルに保存したすべての編集内容を変更としてExperience Managerにアップロードすることなく、アセット（「作業中」とも呼ばれる）に対して大幅な更新を実行することをお勧めします。 これにより、デスクトップユーザーの作業がはかどり、使用されるネットワーク帯域幅が制限され、アセットのタイムラインが適切な状態に保たれ、管理された大規模な更新に集中するようになります。

Adobe Asset Link は、この使用例を適切にサポートしています。

* Photoshop、InDesign、Illustrator のいずれかでユーザーがファイルを編集しようとすると、指定されたアセットに対してチェックアウト操作が実行されます。
* アセットはバックグラウンドでダウンロードされ、Creative CloudのデスクトップアプリケーションによってCreative Cloudに同期されたユーザーExperience Managerアカウントに入れられ、編集上の競合を最小限に抑えるためにアセットのチェックアウトフラグが切り替えられます
* それ以降、ユーザーは、同期した場所にローカルに保存されているファイルで作業をおこない、必要な変更を必要な頻度で継続的に作業し保存することができます。
* さらに、アセットは Creative Cloud アカウントにあるので、ユーザーが所有している他のデバイスでも使用でき（例えば、専用の Creative Cloud モバイルアプリで開いたり編集したりできます）、コラボレーション目的で他の Creative Cloud ユーザーと共有することもできます。
* クリエイティブユーザーが変更を完了すると、使用中の Creative Cloud アプリケーションで、そのファイルに対してチェックイン操作を実行できます。その際に、オプションでコメントを付けることもできます。対応するアセットのExperience Managerが、新しいバイナリでに更新されます。 マーケターやLOBユーザーなどのExperience Managerユーザーは、Experience ManagerアセットタイムラインUIを使用して、アセットの大きな変更やマイルストーンにアクセスできます。

Experience Managerデスクトップアプリケーションは、ネイティブアプリで開かれたアセットのネットワーク共有を提供します。 デフォルトでは、ローカルでおこなわれたすべての変更は、しばらくすると自動的にExperience Managerにアップロードされます。 このような構成を使用すると、作業中の段階で頻繁に保存がすべてExperience Managerにアップロードされ、Experience Managerで不要なバージョンを除き、多くのネットワークトラフィックと潜在的な拡張性の課題が発生します。

ここで推奨されるアプローチは、Experience Managerデスクトップアプリケーションのオプションを使用して自動更新をオフにし、デスクトップアプリケーションのAsset Status UIのアップロードアクションを利用して、Experience Managerに変更を手動でアップロードすることです。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や大規模なプロジェクトのアップロード
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットセットから選択したアセットのアップロード（選択が DAM の外部でおこなわれた場合）

これは、デスクトップユーザーの通常のワークフローの一部として、一定のルールに従って（例：毎週、    撮影するたびに毎回）ファイルをアップロードする場合についての説明です。大規模なアセット移行については、ここでは説明しません。

次のアップロード機能を利用できます。

* 大きなフォルダーや階層フォルダーを一括でアップロードするには、[フォルダーアップロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets)機能を提供するExperience Managerデスクトップアプリケーションを使用します。 フォルダーの階層構造もアップロードできます。アセットはバックグラウンドでアップロードされます。そのため、アセットは Web ブラウザーのセッションに拘束されません。
* 1つのフォルダーから少数のファイルをアップロードするには、ファイルを直接Webインターフェイスにドラッグするか、Experience ManagerAssets Webインターフェイスの「作成」オプションを使用します。
* ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップから直接実行するデジタルアセット管理 {#managing-digital-assets-directly-from-desktop}

Experience Managerファイル共有を使用してデジタルアセットを管理する場合、ネットワークデスクトップアプリケーションでマッピングされたネットワーク共有を使用するだけで、便利な方法と見なされます。 Experience ManagerのWebインターフェイスは、ネットワーク共有（検索、コレクション、メタデータ、コラボレーション、プレビューなど）で可能な限り多くのデジタルアセット管理機能を提供し、Experience Managerデスクトップアプリケーションは、サーバー側DAMリポジトリをデスクトップ上の作業と接続します。

Experience Managerデスクトップアプリケーションを使用してアセットアセットのネットワーク共有で直接Experience Managerを管理することは避けてください。 例えば、Experience Managerデスクトップアプリケーションを使用して複数のファイルを移動またはコピーしないでください。 代わりに、Experience ManagerアセットWeb UIを使用して、Finder/エクスプローラーからExperience Managerーをネットワーク共有にドラッグするか、アセットフォルダーのアップロード機能を使用します。
