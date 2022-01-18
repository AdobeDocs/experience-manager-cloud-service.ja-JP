---
title: ' [!DNL Adobe Creative Cloud] との統合のベストプラクティス'
description: Experience Manager デプロイメントを Adobe Creative Cloud と統合して、アセット転送ワークフローを効率化し、効率を最大限に高めるためのベストプラクティス。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: ht
source-wordcount: '3443'
ht-degree: 100%

---

# Experience Manager と Adobe Creative Cloud の統合のベストプラクティス {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager Assets は、Adobe Creative Cloud と統合できるデジタルアセット管理（DAM）ソリューションです。DAM ユーザーがクリエイティブチームと協力してコンテンツ作成プロセスでのコラボレーションを効率化できるようにサポートします。

Adobe Creative Cloud は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。これには、デスクトップおよびモバイルアプリケーション、デスクトップ同期や Web エクスペリエンスを備えたストレージなどのクラウドサービス、および Adobe Stock などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>Experience Manager／Creative Cloud フォルダー共有機能は非推奨（廃止予定）となったので、以下では扱われなくなりました。Experience Manager で管理されたアセットへのアクセス権をクリエイティブユーザーに与える方法としては、Adobe Asset Link や Experience Manager デスクトップアプリケーションなどの新しい機能をお勧めします。

## クリエイティブプロフェッショナル、マーケター、DAM ユーザーのコラボレーションニーズ {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル（より広い意味では、ネイティブアセット作成アプリケーションで作業しているデスクトップユーザー）向けに、DAM（[!DNL Assets]）で管理されるアセットへのアクセスを効率化します。変更の検出、使用（開く）、編集、Experience Manager への保存のほか、新しいファイルのアップロードを容易にわかりやすく行える方法が必要です。 | Windows または Mac デスクトップ、Creative Cloud アプリ |
| すぐに使用できる高品質なアセットを [!DNL Adobe Stock] から提供する | マーケターは、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Assets]、[!DNL Adobe Stock] マーケットプレイス、メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| アップロードされたアセットの事前定義済みバリエーションを自動的に生成する | 事前に定義されたアクションに対してアドビ固有のメディア処理および変換テクノロジーを利用して、アセットを自動的に処理します。カスタムロジックを作成して、API とアセットマイクロサービスを使用して独自のアクションを定義します。 | [!DNL Assets] ユーザーインターフェイス |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Creative Cloud] アプリを使用しながら、[!DNL Experience Manager] からアセットを検出し、それらを開いて使用したり、編集して変更を [!DNL Experience Manager] にアップロードしたり、新しいファイルを [!DNL Experience Manager] にアップロードできます。 | [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator、InDesign. |
| ビジネスユーザーは、アセットのオープンと使用、編集と [!DNL Experience Manager] への変更内容のアップロード、[!DNL Experience Manager] への新しいファイルのアップロードをデスクトップ環境から簡単に行えます。汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) | Windows および Mac デスクトップ上の Experience Manager デスクトップアプリケーション |
| マーケターとビジネスユーザーは、Experience Manager 内から Adobe Stock アセットの検出、プレビュー、ライセンス取得と保存、管理を行えます。ライセンスを取得し保存したアセットは、限定された Adobe Stock メタデータを提供してガバナンスの強化に役立ちます。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web インターフェイス |
| デジタル製品デザイナーとマーケターとのコラボレーションを改善できます。デザイナーが Adobe XD キャンバス上のデザインとワイヤフレームモデルでデジタルアセットを使用できます。 | [[!DNL Adobe Asset Link] （ [!DNL Adobe XD] 用）](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| マーケターは、アップロードしたアセットと、カスタマイズを使用して作成した事前定義済みのアクションに基づいて、バリエーションと派生物を自動的に作成できます。この自動処理を使用すると、コンテンツベロシティが向上し、手作業が軽減されます。 | [コンテンツ自動化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] Web インターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。代替ソリューション（[Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja)、[Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) コンポーネントに基づいて構築できるソリューション、[リンク共有](share-assets.md)、[Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md) の使用など）については、それぞれ固有の要件に基づいた検討が必要です。

![Experience Manager 用の Creative Cloud 接続：使用する機能の決定](assets/creative-connections-aem.png)

使用する機能の決定

### 使用例とアドビソリューションの対応関係 {#mapping-of-use-cases-and-adobe-solutions}

| 使用例 | Adobe Asset Link | Experience Manager デスクトップアプリ | 備考または代替手段 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 検出 - フォルダーを参照する | 対応 | Experience Manager Web UI およびデスクトップアクション | ネットワーク共有を参照する場合は、アセットのバイナリファイルをダウンロードしないように、サムネールをオフにします。 |
| 検出 - コレクションにアクセスする | 対応 | Experience Manager Web UI およびデスクトップアクション |  |
| 検出 - アセットを検索する | 対応 | Experience Manager Web UI およびデスクトップアクション |  |
| 使用 - アセットを開く | 対応 | 対応 - 任意のアプリに対して | 「[Web インターフェイスから開く](/help/assets/manage-digital-assets.md#previewing-assets)」またはファインダーから開く |
| 使用 - Experience Manager からドキュメント内にアセットを配置する | 対応 - 埋め込み | 対応 - リンクまたは埋め込み | Experience Manager デスクトップアプリケーションでは、ローカルファイルシステム上のファイルとしてアセットにアクセスできます。ネイティブアプリでは、これらのリンクはローカルパスで表されます。 |
| 編集 - 編集用に開く | 対応 - チェックアウトアクション | 対応 - 「開く」アクション（ネットワーク共有内） | 「[AAL でチェックアウト](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)」の場合は、デフォルトでは、アセットをユーザーの Creative Cloud ストレージアカウント（Creative Cloud アプリで同期）に保存します。 |
| 編集 - Experience Manager の外部で作業する | 対応 - デスクトップに同期しているユーザーの Creative Cloud ストレージアカウントでアセットが入手可能です。 | 対応 |  |
| 編集 - 変更をアップロードする | 対応 - [チェックインアクション](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)（オプションコメント付き） | 対応 |  |
| アップロード - 単一ファイル | 対応 - 現在のアクティブなドキュメントをアップロードします | 対応 | [Web インターフェイスを使用してアップロード](/help/assets/manage-digital-assets.md#uploading-assets) |
| アップロード - 複数ファイル／階層フォルダー構造 | 非対応 | 対応 | [Web インターフェイスを使用してアップロード](/help/assets/manage-digital-assets.md#uploading-assets)。カスタムスクリプティングまたはツール |
| その他 - ユーザーとログイン | Creative Cloud デスクトップアプリケーションにログインした Creative Cloud ユーザーが認識されます（SSO） | Experience Manager ユーザー／ログイン | 両方のソリューションのユーザーが Experience Manager ユーザークォータに対してカウントされます。 |
| その他 - ネットワークとアクセス | ネットワークを介してユーザーのデスクトップから Experience Manager デプロイメントにアクセスできる必要があります | ネットワークを介してユーザーのデスクトップから Experience Manager デプロイメントにアクセスできる必要があります | Adobe Asset Link はネットワークプロキシ環境を共有しません。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

アセット配布のユースケースをサポートするには、次のオプションを考慮します。

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja)：Assets への設定可能なアドオンでアセットの公開に使用。

* カスタムソリューションは [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) のコードベースに基づいて作成される。
* Experience Manager [リンク共有](/help/assets/share-assets.md)：リンクを使用してアドホックでアセットを共有する。
* [ Assets Web インターフェイス](/help/assets/manage-digital-assets.md)：外部ユーザーが Experience Manager にアクセスできるようにする、Experience Manager アクセス制御の設定で保護されている外部関係者向けのエリア。必要な IT／ネットワーク設定の調整機能が備わっている。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更が行われている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：**&#x200B;より広範なチームと共有するための準備ができているアセット。または、マーケティングチームもしくは LOB チームと共有するためにクリエイティブチームによって選択／承認されているアセット。

* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。

* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するために行われます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り、Adobe Experience Manager（）Assets と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成は行わないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### Experience Manager と Creative Cloud の統合を使用する場合の考慮事項 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Experience Manager と Creative Cloud の統合に関するベストプラクティスの概要を説明します。以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesign、Illustrator のいずれかで作業しているクリエイティブユーザーの場合：** Adobe Asset Link は、Experience Manager からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：** Experience Manager デスクトップアプリケーションを使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### Experience Manager Assets からの Adobe Stock アセットへのアクセス {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager と Adobe Stock の統合](/help/assets/aem-assets-adobe-stock.md)により、Experience Manager ユーザーは、Adobe Stock 内のアセットを検索、プレビュー、ライセンス取得し、Experience Manager に保存できるようになります。ライセンス取得され保存された Adobe Stock アセットには、限定された Stock メタデータが付いており、このメタデータを使用してアセットをさらに絞り込むことができます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobe Stock 内のアセットが Experience Manager に保存されると、それらは通常の Experience Manager Assets になり、バイナリが Experience Manager リポジトリーに保存されます。Adobe Stock に関係する一部のメタデータが Experience Manager 内のアセットに保存されます。その他の点では、取り込みプロセスは他のあらゆるファイルの場合と同様です。例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* Experience Manager に保存されたアセットはコピーであり、Adobe Stock へのリンクではありません。

**Adobe Stock から Creative Cloud 内の Experience Manager に保存されたアセットの操作**。この統合は Adobe Asset Link とは無関係ですが、Adobe Asset Link では Stock から保存されたこれらのアセットをそのように認識し、Photoshop、Illustrator、InDesign の Adobe Asset Link 拡張 UI でこれらのアセットに追加のメタデータと Stock アイコンを表示します。Experience Manager に保存すると通常の Experience Manager アセットになるので、ファイルを閲覧したり開いたりすることができます。Adobe Asset Link 拡張機能を備えた Creative Cloud アプリで作業しているクリエイティブユーザーは、Adobe Stock から Experience Manager に保存したライセンス取得済みアセットにアクセスできるだけでなく、Creative Cloud ライブラリパネルを使用して Adobe Stock アセットを検索、プレビューし、ライセンスを取得することもできます。Adobe Stock からライセンスを取得して Experience Manager に保存したアセットは、Experience Manager Assets デプロイメントにアクセスする広範なチームで利用できるようになります。ただし、クリエイティブユーザーが Creative Cloud ライブラリパネル経由で Adobe Stock からアセットのライセンスを取得した場合、デフォルトでは、それらのアセットは自分の Creative Cloud アカウント内でしか使用できません。

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織では、ダウンストリームマーケティング／LOB プロセスに関連するアセットのみを保存するようにしています（例えば、Experience Manager Sites 経由での Web チャネルなどのチャネルへの公開、Adobe Experience Cloud（Experience Cloud、Advertising Cloud）により提供され、Analytics Cloud により測定される他のチャネルへの公開、ユーザー／パートナーへの提供などのプロセス）。また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

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

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームが行った更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備が完了する前に、アセットの最終版以外のバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームおよびマーケティングチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

Experience Manager Assets では、Experience Manager Assets デプロイメントに対するアクセス権に基づいて、2 つのタイプのユーザーがサポートされています。通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM に直接アクセスできます。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセスすることはできません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内のクリエイティブチームや、社内ネットワークにオンボーディングされたエージェンシー／クリエイティブプロフェッショナルは、（Experience Manager ログインを含む）DAM インスタンスへのアクセス権を持っています。外部の関係者（通常はクライアントのために働く代理店などの信頼できる組織）に直接アクセスを許可するように、Experience Manager とネットワークインフラストラクチャを設定できます。これにより、外部の関係者がネットワークを介して（例えば、VPN または IP の許可リスト経由で）Experience Manager にアクセスできるようになります。

このような場合、Adobe Asset Link または Experience Manager デスクトップアプリケーションを使用すると、最終／承認済みアセットに容易にアクセスしたり、クリエイティブレディアセットを DAM に保存したりできます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM インスタンスへの直接アクセス権を持たない外部のエージェンシーやフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

以下の戦略で最終／承認済みアセットへのアクセスを提供します。

* Asset Link が機能しない場合は、デスクトップアプリケーションを使用します。
* 外部パートナーに安全にアセットを配布するには、[Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja) を使用します。
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) に基づいた、配布および調達用ポータルのカスタム実装を使用します。
* Experience Manager に設定されたアクセス制御と必要なネットワークインフラストラクチャ（VPN や IP の許可リストなど）を使用して、DAM 内の専用のコンテンツ領域に外部の関係者がアクセスできるようにします。Experience Manager Web UI を使用してアセットを取得したり、新しいコンテンツを DAM にアップロードしたりできます。

#### Experience Manager 内のアセットの更新 {#work-in-progress-on-assets-from-aem}

このドキュメントで説明しているように、アセットの大規模な更新（処理中の作業と呼ばれることもあります）を実行する際には、ローカルファイルに保存したすべての編集内容も変更として Experience Manager にアップロードすることを避けるとよいでしょう。これにより、デスクトップユーザーの作業がはかどり、使用されるネットワーク帯域幅が制限され、アセットのタイムラインが適切な状態に保たれ、管理された大規模な更新に集中するようになります。

Adobe Asset Link は、この使用例を適切にサポートしています。

* Photoshop、InDesign、Illustrator のいずれかでユーザーがファイルを編集しようとすると、指定されたアセットに対してチェックアウト操作が実行されます。
* そのアセットはバックグラウンドでダウンロードされ、Creative Cloud デスクトップアプリケーションによりディスクに同期されたユーザーの Creative Cloud アカウントに格納されます。Experience Manager でアセットのチェックアウトフラグが切り替わり、編集の競合が最小限に抑えられます。
* それ以降、ユーザーは、同期した場所にローカルに保存されているファイルで作業を行い、必要な変更を必要な頻度で継続的に作業し保存することができます。
* さらに、アセットは Creative Cloud アカウントにあるので、ユーザーが所有している他のデバイスでも使用でき（例えば、専用の Creative Cloud モバイルアプリで開いたり編集したりできます）、コラボレーション目的で他の Creative Cloud ユーザーと共有することもできます。
* クリエイティブユーザーが変更を完了すると、使用中の Creative Cloud アプリケーションで、そのファイルに対してチェックイン操作を実行できます。その際に、オプションでコメントを付けることもできます。Experience Manager 内で対応するアセットの新しいバージョンが作成され、新しいバイナリで更新されます。マーケターや LOB ユーザーなどの Experience Manager ユーザーは、Experience Manager Assets のタイムライン UI を介して、アセットの大幅な変更やマイルストーンにアクセスできます。

Experience Manager デスクトップアプリケーションは、ネイティブアプリで開かれたアセットのネットワーク共有を提供します。デフォルトでは、ローカルで行われたすべての変更は、しばらくすると自動的に Experience Manager にアップロードされます。このような設定では、WIP フェーズでの頻繁な保存はすべて Experience Manager にアップロードされバージョン管理されるので、不要なバージョンが Experience Manager に生成されることは言うまでもなく、大量のネットワークトラフィックが発生し、スケーラビリティの重大な問題も生じる可能性があります。

ここでは、Experience Manager デスクトップアプリケーションのオプションを使用して自動更新をオフにし、アプリのアセットステータス UI で変更のアップロードアクションを利用して、アセットへの変更を手動で Experience Manager にアップロードすることをお勧めします。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や大規模なプロジェクトのアップロード
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットセットから選択したアセットのアップロード（選択が DAM の外部で行われた場合）

これは、デスクトップユーザーの通常のワークフローの一部として、一定のルールに従って（例：毎週、撮影するたびに毎回）ファイルをアップロードする場合についての説明です。大規模なアセット移行については、ここでは説明しません。

次のアップロード機能を利用できます。

* 大きなフォルダーや階層フォルダーをまとめてアップロードするには、[フォルダーアップロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#bulk-upload-assets)機能を提供する Experience Manager デスクトップアプリケーションを使用します。フォルダーの階層構造もアップロードできます。アセットはバックグラウンドでアップロードされます。そのため、アセットは Web ブラウザーのセッションに拘束されません。
* 1 つのフォルダーから少数のファイルをアップロードするには、ファイルを直接 Web インターフェイスにドラッグするか、Experience Manager Assets Web インターフェイスの「作成」オプションを使用します。
* ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップから直接実行するデジタルアセット管理 {#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理している場合、Experience Manager デスクトップアプリケーションでマップされたネットワーク共有を使用するだけで、より便利になる可能性があります。ネットワークファイル共有から切り替える場合は、ネットワーク共有で可能な機能（検索、収集、メタデータ、コラボレーション、プレビューなど）に勝る豊富なデジタルアセット管理（DAM）機能が Experience Manager Web インターフェイスに用意されています。また、Experience Manager デスクトップアプリケーションには、サーバー側の DAM リポジトリーとデスクトップの作業を連携させるための便利なリンクもあります。

Experience Manager デスクトップアプリケーションを使用して Experience Manager Assets のネットワーク共有でアセットを直接管理することは避けてください。例えば、Experience Manager デスクトップアプリケーションを使用して複数のファイルを移動またはコピーしないでください。この場合は、Experience Manager Assets Web UI を使用して、Finder／エクスプローラーからフォルダーをネットワーク共有にドラッグします。または、Experience Manager Assets のフォルダーアップロード機能を使用します。
