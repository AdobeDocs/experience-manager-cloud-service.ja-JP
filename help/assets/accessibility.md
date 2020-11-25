---
title: アクセシビリティ [!DNL Experience Manager Assets]
description: 障害を持つユーザーにとって、Cloud Service [!DNL Adobe Experience Manager] のアクセシビリティ機能がどのように役立つかを知る。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1dc278c85a1dabdd3e6ac4c0de95271d9da3260c
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 2%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Cloud Serviceとしてのアクセシビリティ機能 [!DNL Adobe Experience Manager Assets] の使用 {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] コンテンツ作成者や発行者は、素晴らしいエクスペリエンスをWeb上で提供できます。 Adobeは、のアクセシビリティを向上させ、障害を持つクリエイターを対象に取り組んでい [!DNL Experience Manager]ます。 このソフトウェアは、あらゆる種類のユーザーのニーズを満たすように継続的に拡張され、視覚、聴覚、運動、または他の障害を持つ個人を含む世界的な標準に準拠しています。

[!DNL Experience Manager] 準拠する規格を説明する準拠情報を公開し、製品のアクセシビリティ機能の概要を示し、準拠レベルを説明します。 アクセシビリティ準拠レポートは、 [!DNL Experience Manager] ユーザーが様々な標準への準拠レベルを理解するのに役立ちます。 で行った機能強化により、すべてのユーザーは、キーボード、スクリーンリーダー、拡大鏡、その他の支援テクノロジーを使用して、簡単にインターフェイスを使用できます。 [!DNL Assets]

[!DNL Experience Manager] は、次の標準に対する様々なレベルのサポートを提供します。

* [Web Content Accessibility Guidelines（WCAG）2.1](https://www.w3.org/TR/WCAG/).
* [再生法第508条を改正](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) by W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

準拠レベルの詳細を含むレポートを読み取るには、 [アクセシビリティ準拠レポート](https://www.adobe.com/accessibility/compliance.html) (ACR)ページを参照してください。

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](/). -->

## 支援テクノロジー {#at-support}

障害を持つユーザーは、頻繁にハードウェアとソフトウェアを利用してWebコンテンツにアクセスし、ソフトウェア製品を使用します。 これらのツールは、支援テクノロジーと呼ばれます。 [!DNL Experience Manager Assets] ソフトウェアの主要機能を使用する場合、次の種類の支援テクノロジー(AT)を使用できます。

* スクリーンリーダーとスクリーン虫めがね。
* 音声認識ソフトウェア
* キーボードの使用 — ナビゲーションとショートカット。
* スイッチコントロール、更新可能な点字ディスプレイ、その他のコンピュータ入力デバイスを含む支援ハードウェア。
* UI虫めがねツール

## [!DNL Experience Manager Assets] アクセシブルな使用例 {#accessible-assets-use-cases}

では、アクセシビリティ機能 [!DNL Experience Manager]は、ユーザーとそのお客様の2つの主要な要件に対応し [!DNL Experience Manager] ています。

* コンテンツデザイナーや制作者にとって、アクセシブルなコンテンツを作成して公開する機能は、顧客やWebサイト訪問者の間でも使用されます。 コンテンツは、支援テクノロジーの支援を受けて障害を持つユーザーが使用できます。 詳しくは、「 [Webアクセシビリティガイドライン](/help/onboarding/accessibility/web-accessibility.md)」を参照してください。
* [!DNL Experience Manager] また、障害を持つユーザーや管理者は、ユーザーインターフェイスやコントロールにアクセスして、コンテンツの作成と管理を行うこともできます。 障害を持つユーザーは、支援テクノロジーを使用して、この [!DNL Assets] 機能をナビゲート、使用、管理できます。

の主な機能 [!DNL Assets] は以前よりもアクセスしやすく、定期的に更新され、グローバル標準への準拠が改善されています。 のCRUD操作には、ある程度のアクセシビリティが組み込ま [!DNL Assets] れています。 アセットの追加、管理、検索、配布などのDAMワークフローには、キーボードショートカット、スクリーンリーダーテキスト、カラーコントラストなどの支援を受けてアクセスできます。

## キーボードの使用のサポート {#keyboard-use}

クリック可能なユーザーインターフェイス要素や、ポインターを使用したアクションが可能なユーザーインターフェイス要素の多くは、キーボードを使用して操作することもできます。 キーボードを使用すると、UI要素に焦点を当て、適切なアクションを実行できます。 ユーザーは、キーボードショートカットを使用して、UI要素にフォーカスしなくても、コマンドやアクションを直接トリガーできます。 例えば、ユーザーは、キーボードを使用してユーザーインターフェイスコントロールに移動し、キーボードショートカットを選択することで、左側にアセットのタイムラインを開くこ `Return`とができ `Alt + 2` ます。

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### のキーボードショートカット [!DNL Assets] {#keyboard-shortcuts}

の次の操作は、リストに表示されているキーボードショートカット [!DNL Assets] を使用して実行します。 コンソールに適用されるほとんどのキーボードショートカットは、 [!DNL Experience Manager] にも適用され [!DNL Assets]ます。 See [keyboard shortcuts for Consoles](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md). キーボードショートカットを [有効または無効にする方法を参照してください](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)。

| ユーザーインターフェイスまたはシナリオ | キーボードショートカット | アクション |
|---|---|---|
| ユーザーインター [!DNL Assets] フェイスの列表示 | 上向き矢印キーと下向き矢印キー | 同じ階層内のファイルやフォルダーに移動します。 |
| ユーザーインター [!DNL Assets] フェイスの列表示 | 左向き矢印キーと右向き矢印キー | 現在のフォルダーの上または下のファイルとフォルダーに移動します。 |
| フォルダの参照 [!DNL Assets] | `/` | Omnisearchボックスを開いて検索を呼び出します。 |
| [!DNL Assets] コンソール | ` | サイドレールを切り替え |
| [!DNL Assets] コンソール | `Alt + 1` | コンテンツツリーを開きます。 |
| [!DNL Assets] コンソール | `Alt + 2` | 左側の [!UICONTROL ナビゲーション] (Navigation)パネルを開きます。 |
| [!DNL Assets] コンソール | `Alt + 3` | 選択したアセットの [!UICONTROL タイムラインを表示] 。 |
| [!DNL Assets] コンソール | `Alt + 4` | 選択したアセットのライブコピーの参照を開きます。 |
| [!DNL Assets] コンソール | `Alt + 5` | 検索を呼び出して、選択したフォルダー内で検索を行います。 |
| アセットまたはフォルダが選択されている | Backspace | 選択したアセットまたはフォルダーを削除します。 |
| アセットまたはフォルダが選択されている | `p` | 選択したアセットのプロパティページを開きます。 |
| アセットまたはフォルダが選択されている | `e` | 選択したアセットを編集します。 |
| アセットまたはフォルダが選択されている | `m` | 選択したアセットを移動します。 |
| アセットまたはフォルダが選択されている | `Ctrl + c` | 選択したアセットをコピーします。 |
| アセットまたはフォルダが選択されている | `Esc` | 選択を解除します。 |
| ダイアログボックスが開き、フォーカスがある | `Esc` | ダイアログボックスを閉じます。 |
| DAM内のフォルダー内 | `Ctrl + v` | コピーしたアセットを貼り付けます。 |
| [!DNL Assets] コンソール | `Ctrl + A` | すべてのアセットを選択します。 |
| アセットプロパティページ | `Ctrl + S` | 変更を保存します。 |
| [!DNL Assets] コンソール | `?` | キーボードショートカットのリストを参照してください。 |

## サインインとユーザーインター [!DNL Assets] フェイスの操作 {#login}

ユーザーは、キーボードを使用してログイン先に移動し、サインインフィールドに入力することができます。 ログインページのユーザ名とパスワードの組み合わせが正しくないことに起因するエラーメッセージは、エラーが発生するたびにスクリーンリーダーによって通知されます。

ログイン後、DAMユーザーは、キーボードを使用してユーザーインター [!DNL Assets] フェイス内を移動できます。 左側のパネル、メニュー、ユーザープロファイル、検索バー、ファイルとフォルダー、管理および設定などのユーザーインターフェイス要素は、キーボードを使用して移動できます。 キーボードのナビゲーション順序は、左から右、上から下です。 キーボードを使用してナビゲーションを行う場合、フォーカス時にアクション可能なオプションが、カラーコントラストの高いハイライトで表示され、スクリーンリーダーによってナレーションされます。 メニュー内のフォーカスされたオプションの状態（展開、折りたたみ、混在など）は、必要に応じて、スクリーンリーダーによって通知されます。 また、アクション可能なオプションの目的は、外観やUIの配置などではなく、スクリーンリーダーによって通知されます。

ユーザーがメニューからヘルプまたはユーザープロファイルのオプションを展開すると、スクリーンリーダーから適切なオプションまたはステータスが通知されます。 ユーザーがユーザープロファイルオプションを展開すると、キーボードを使用して使用可能なオプションを選択できます。 例えば、管理者は別のユーザーを装うことができます。 ユーザーが [!UICONTROL ヘルプ] ・オプションから文字列を検索した場合、ナレータは検索が進行中であることを示す「ヘルプの検索」を通知します。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## アセットの参照と関連表示 {#browse}

ユーザーインターフェイスでは、キーボードを使用してDAMリポジトリ内の既存のデジタルアセットのリスト、プレビューまたはダウンロード、生成されたレンディションの表示、表示の切り替え、生成されたレンディションの表示、タイムラインとバージョンの履歴の表示、コメントと参照の表示、メタデータの管理を行えます。 [!DNL Assets]

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

アセットリポジトリを参照する際、次の機能によりアクセシビリティが向上します。

* スクリーンリーダーは、アイコン名の代わりにアイコンの目的や機能を表現する代替テキストを表示します。
* ユーザーは、キーボードキーを使用して、アセットの参照リストのインタラクティブユーザーインターフェイスオプションにアクセスし、焦点を合わせることができます。
* リスト表示の各行の要素は、スクリーンリーダーによって同じ行の要素として通知されます。
* キーを使用して移動する場合、フォーカスはバージョンプレビューの閉じるオプションに移動できます。 `Tab`
* キーボードを使用して参照する場合、強調表示された操作可能なユーザーインターフェイスオプションは、コントラストを強化し、より目立つ視覚的な焦点を持ちます。 これにより、焦点を絞った領域をユーザーがより識別しやすくなります。
* サムネール表示からクイックアクションアイコンを削除する `Esc` ためにキーを使用しても、最後にフォーカスされたアイテムからはキーボードフォーカスが削除されません。
* アセットを選択した状態で、キーボードショートカットを選択すると、左側のレールに `Alt + 4` 参照  リストが開きます。 キーを使用して、ゼロ以外の参照エントリ間を移動でき `Tab` ます。 ゼロ以外の参照エントリを参照するだけで、作業やキー操作を省力化できます。
* アセットに対するコメントは、アセットタイムラインで使用できます。 キーボードまたはキーボードショートカットを使用して左側のレールにアクセスすると、アクセスできます。
* [!UICONTROL の表示設定][!DNL Experience Manager] は、キーボードを使用してアクセスできます。 ユーザーは、矢印キーを使用して使用可能なカードのサイズ間を移動し、選択してTabキーで移動し、既存の表示設定表示ー内の他の要素を設定できます。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Manage digital assets {#manage-assets}

CRUD操作、アセットのダウンロード、メタデータの追加など、多くのアセット管理タスクには、様々な角度からアクセスできます。 [!DNL Assets] 様々な支援テクノロジー（特にスクリーンリーダーやキーボード）を使用してタスクを行うことができます。

キーボードを使用してリポジトリを [参照し、アセットをダウンロードする方法を示すビデオデモを参照してください](https://youtu.be/K3dgqMRQJys)。

通常、マーケターや管理者などの役割が行うメタデータ操作では、次の機能によりアクセシビリティが向上します。

* [!UICONTROL アセットの] プロパティ [!UICONTROL ページの「保存して閉じる] 」オプションは、キーボードを使用してアクセスできるようになりました。
* スクリーンリーダーは、アセットの [!UICONTROL プロパティの「] 基本 [!UICONTROL 」タブで選択したタグを削除するオプションを読み上げます]。
* ユーザーは、日付選択ポップアップダイアログをキーボードと共に使用できます。 日付選択ユーザーインターフェイス要素を使用して、オン時間とオフ時間を設定し、「日付」を選択します。
* キーボードを使用したドラッグ機能は、スクリーンリーダーの [!UICONTROL 参照モードのメタデータスキーマエディタ] (MDE)で正しく機能します。
* ユーザーは、キーボードを使用して、フォルダーのプ [!UICONTROL ロパティの「] 権限 [!UICONTROL 」タブにある「] 閉じたユーザーグループ」の下の「ユーザーまたはグループ」フィールドにフォーカスを移動でき ます。

## デジタルアセットの検索 {#search-assets}

すばやくシームレスなアセット検索の経験により、コンテンツの速度が向上します。 コンテンツ速度の使用例は、主な [!DNL Assets] 機能の一部です。 Omnisearchバーから検索を開始するには、キーボードショートカットを使用する `/` か、スクリーンリーダーと共に使用し `Tab` て、検索オプションをすばやく見つけることができます。 スクリーンリーダーは、検索オプションの検索オプションにフォーカスがある場合、オプション名を「検索ボタン」として ![ナレーションします](assets/do-not-localize/search_icon.png)。 ユーザーは「Omnisearch」ボックス `Return` を開くことを選択できます。 スクリーンリーダーは、検索ボックスに入力されたキーワードのナレーションだけでなく、提供された提案のナレーションも行い [!DNL Experience Manager Assets]ます。 矢印キーと `Return`、を組み合わせて使用し、様々なオプション `Tab` にアクセスして検索をトリガーできます。

検索機能は、次の機能でアクセスできます。

* ページタイトルはスクリーンリーダーが使用できるので、ページをアセットの検索ページとして識別するのに役立ちます。
* ユーザーは、Omnisearchフィールド内からアセットを検索します。 ユーザーは、キーボードナビゲーションまたはキーボードショートカットを使用して開くことができ `/`ます。
* 開始が検索キーワードを入力し、矢印キーを使用して自動サーチクエリを選択できます。 ハイライトされた提案はキーを使用して選択でき、選択した提案はアセットで検索されます。 `Return`
* スクリーンリーダーは、検索結果をフィルタリングする際に、フィルターパネルで混在状態のチェックボックス（ネストされた述語のすべてを選択しない限り、第1レベルのチェックボックスは選択されず、完全に選択されます）を識別し、読み上げることができます。
* 「全検索」ボックスを閉じると、ユーザーのフォーカスが検索オプションに移動します。

検索結果をフィルタする場合：

* 検索結果ページには、スクリーンリーダーユーザーをより深く理解するための情報のタイトルが表示されます。
* スクリーンリーダーは、検索フィルターのオプションを拡大可能なアコーディオンとして通知します。
* 状態が混在するオプションを持つ述語は、スクリーンリーダーによって通知されます。

## アセットの共有 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

アセットを共有する場合、次の機能によってアクセシビリティが向上します。

* ユーザーは、リンクの共有ダイアログの「検索と電子メールアドレス」フィールド内のキーボードを使用して、フォーカスを移動す追加ることができます。

* リンクの共有ダイアログで、参照モードで移動するときに、スクリーンリーダー、

   * ダイアログが読み込まれた後は、直ちに表の情報を読み込まないでください。
   * リストに表示されているすべての提案に移動できます。
   * 「電子メールアドレス」フィールドと「検索」フィ追加ールドに対して表示された提案の説明

## アクセス可能なドキュメント {#accessible-docs}

[!DNL Experience Manager] には、障害を持つユーザーが使用できる、アクセシブルなドキュメントが用意されています。 以下は、コンテンツオファーを今すぐアクセシブルにするのに役立ちますが、Adobeはテンプレートとコンテンツの改善に努め続けます。

* スクリーンリーダーはテキストを読み上げることができます。
* 画像や図には代替テキストが用意されています。
* キーボードナビゲーションが可能です。
* コントラスト比は、ドキュメントWebサイトの一部を強調表示するのに役立ちます。

## フィードバックの提供 {#a11y-feedback}

アクセシビリティに関するフィードバックを提供し、質問をし、製品の改良点をリクエストするには、次の方法を使用します。

* フォームにwww.adobe.com/accessibility/feedback.htmlで入力し [ます](https://www.adobe.com/accessibility/feedback.html)。
* access@adobe.comまで電子メールでお問い合わせください。

>[!MORELIKETHIS]
>
>* [各リリースで行われた機能強化のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)。
>* [[!DNL Adobe Experience Manager] アクセシビリティガイダンス](/help/onboarding/accessibility/web-accessibility.md)。
>* [Adobeソリューションの準拠レポート(ACR)およびVPATリスト](https://www.adobe.com/accessibility/compliance.html)。

