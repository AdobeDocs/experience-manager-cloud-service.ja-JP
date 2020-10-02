---
title: アクセシビリティ [!DNL Experience Manager Assets]
description: 障害を持つユーザーにとって、Cloud Service [!DNL Adobe Experience Manager] のアクセシビリティ機能がどのように役立つかを知る。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bd27bb5da82c9997f4c562a3d1efad77df66728f
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 2%

---


<!--
Original scope of this article for Core Assets for all a11y topics is around the following topics. This has changed since then but keeping this list of topics for posterity's sake.

* Convert the absolute doc links to relative links.
* Add an overview
* Compile a list of enhancements done in the last ~1 year.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.)
* Specific user tasks supported, such as, download assets, datepicker, editing metadata, etc.
* Support matrix of user tasks with browsers and screen readers + OSes combinations
* Exceptions that users should be aware of.
* CTA – what is next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Examples of other a11y DX Docs from Elle.
  * Link to a11y-specific channels to report issues, seek support, or request enhancements, if any. Available info from Elle.
-->

# Accessibility in [!DNL Adobe Experience Manager Assets] as a Cloud Service {#accessibility-in-aem-assets}

Adobeは、障害を持つユーザーを含むすべてのユーザー向けの商品作成に取り組んでいます。 [!DNL Adobe Experience Manager] は、すべてのタイプのユーザーのニーズに合わせて継続的に拡張されます。 [!DNL Experience Manager] 規格に準拠する詳細な規格に関する準拠情報を公開し、製品のアクセシビリティ機能の概要を示し、準拠レベルを説明します。 これは、ユーザーが遵守の程度を理解するのに役立ちます。

[!DNL Adobe Experience Manager] は、次の標準に対する様々なレベルのサポートを提供します。

* [Web Content Accessibility Guidelines（WCAG）2.1](https://www.w3.org/TR/WCAG/).
* [第508条を改訂](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [WAI-ARIA](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

準拠レベルの詳細を示すレポートにアクセスするには、すべてのAdobeソリューションの [アクセシビリティ準拠レポート ](https://www.adobe.com/accessibility/compliance.html) (ACR)ページを参照してください。

## 支援テクノロジー {#at-support}

障害を持つユーザーは、Webコンテンツにアクセスする際に、ハードウェアとソフトウェアを頻繁に使用します。 これらのツールは、支援テクノロジーと呼ばれます。 [!DNL Adobe Experience Manager Assets] 次の種類の支援テクノロジーを使用して、ソフトウェアの主要機能を使用するユーザーにサポートを提供します。

* スクリーンリーダー
* 音声認識ソフトウェア
* キーボードの使用 — ナビゲーションとショートカット。
* スイッチコントロール、更新可能な点字ディスプレイ、その他のコンピュータ入力デバイスを含む支援ハードウェア。
* UI虫めがねツール

## [!DNL Experience Manager Assets] アクセシブルな使用例 {#accessible-assets-use-cases}

では、アクセシビリティ機能 [!DNL Experience Manager]は、ユーザーとそのお客様の2つの主要な要件に対応し [!DNL Experience Manager] ています。

コンテンツデザイナーや制作者にとって、アクセシブルなコンテンツを作成して公開する機能は、顧客やWebサイト訪問者の間でも使用されます。 コンテンツは、支援テクノロジーの支援を受けて障害を持つユーザーが使用できます。 詳しくは、「 [Webアクセシビリティガイドライン](/help/onboarding/accessibility/web-accessibility.md)」を参照してください。

また、障害を持つユーザー [!DNL Experience Manager] や管理者は、コンテンツの作成と管理を行うためのユーザーインターフェイスやコントロールにアクセスできます。 障害を持つユーザーは、支援テクノロジーを使用して、この [!DNL Assets] 機能をナビゲート、使用、管理できます。

の主な機能 [!DNL Assets] は以前よりもアクセスしやすく、定期的に更新され、グローバル標準への準拠が改善されています。 アセットのCRUD操作には、ある程度のアクセシビリティが組み込まれています。 アセットの追加、管理、検索、配布などのDAMワークフローには、キーボードショートカット、スクリーンリーダーテキスト、カラーコントラストなどの支援を受けてアクセスできます。

## キーボードの使用のサポート {#keyboard-use}

クリック可能なユーザーインターフェイス要素や、ポインターを使用したアクションが可能なユーザーインターフェイス要素の多くは、キーボードを使用して操作することもできます。 キーボードを使用すると、UI要素に焦点を当て、適切なアクションを実行できます。 ユーザーは、キーボードショートカットを使用して、UI要素にフォーカスしなくても、コマンドやアクションを直接トリガーできます。 例えば、ユーザーは、キーボードを使用してUIコントロールに移動し、Returnキーを押し、キーボードショートカットを押すことで、左側にアセットのタイムラインを開くことができ `alt + 2` ます。

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### アセットのキーボードショートカット {#keyboard-shortcuts}

<!-- TBD: Add here only those keyboard shortcuts that work for/with Assets. Do with Oct release.
-->

| ユーザーインターフェイスまたはシナリオ | キーボードショートカット | アクション |
|---|---|---|
| アセットユーザーインターフェイスの列表示 | 上向き矢印キーと下向き矢印キー | 同じ階層内のファイルやフォルダーに移動します。 |
| アセットユーザーインターフェイスの列表示 | 左向き矢印キーと右向き矢印キー | 現在のフォルダーの上または下のファイルとフォルダーに移動します。 |
| アセット内のフォルダの参照 | `/` | Omnisearchボックスを開いて検索を呼び出します。 |
| アセットコンソール | ` | サイドレールを切り替え |
| アセットコンソール | Alt + 1 | コンテンツツリーを開きます。 |
| アセットコンソール | Alt + 2 | 「 [!UICONTROL ナビゲーション] 」(Navigation)を参照してください。 |
| アセットコンソール | Alt + 3 | 選択したアセットの [!UICONTROL タイムラインを表示] 。 |
| アセットコンソール | Alt + 4 | 選択したアセットのライブコピーの参照を開きます。 |
| アセットコンソール | Alt + 5 | 検索を呼び出して、選択したフォルダー内で検索を行います。 |
| アセットまたはフォルダが選択されている | Backspace | 選択したアセットまたはフォルダーを削除します。 |
| アセットまたはフォルダが選択されている | `p` | 選択したアセットのプロパティページを開きます。 |
| アセットまたはフォルダが選択されている | `e` | 選択したアセットを編集します。 |
| アセットまたはフォルダが選択されている | `m` | 選択したアセットを移動します。 |
| アセットまたはフォルダが選択されている | Ctrl + C | 選択したアセットをコピーします。 |
| アセットまたはフォルダが選択されている | Esc | 選択を解除します。 |
| ダイアログボックスが開き、フォーカスがある | Esc | ダイアログボックスを閉じます。 |
| DAM内のフォルダー内 | Ctrl + V | コピーしたアセットを貼り付けます。 |
| アセットコンソール | Ctrl + A | すべてのアセットを選択します。 |
| アセットプロパティページ | Ctrl + S | 変更を保存します。 |
| アセットコンソール | `?` | キーボードショートカットのリストを参照してください。 |

コンソールに適用されるほとんどのキーボードショートカットは、 [!DNL Experience Manager] アセットにも適用されます。 See [Keyboard Shortcuts for Consoles](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/essentials/keyboard-shortcuts.html). キーボードショートカットを [有効または無効にする方法を参照してください](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)。

## サインインとユーザーインター [!DNL Assets] フェイスの操作 {#login}

ユーザーは、キーボードを使用してログイン先に移動し、ログインフィールドに入力することができます。 ログインページのユーザ名とパスワードの組み合わせが正しくないことに起因するエラーメッセージは、エラーが発生するたびにスクリーンリーダーによって通知されます。

ログイン後、DAMユーザーは、キーボードを使用してユーザーインター [!DNL Assets] フェイスに移動できます。 キーボードのナビゲーション順序は、左から右、上から下です。 キーボードを使用してナビゲーションを行う場合、焦点を合わせた操作可能なオプションは、カラーコントラストが高くハイライト表示され、スクリーンリーダーによってナレーションが行われます。 メニュー内のフォーカスされたオプションの状態（展開または折りたたみ）が、スクリーンリーダーによってアナウンスされます。

ユーザーがメニューからヘルプまたはユーザープロファイルのオプションを展開すると、スクリーンリーダーから適切なオプションまたはステータスが通知されます。 ユーザーがユーザープロファイルオプションを展開すると、キーボードを使用して使用可能なオプションを選択できます。 例えば、ユーザーが別のユーザーを装うことができます。 ユーザーインターフェイスオプションとエラーメッセージ

![Experience Managerユーザーインターフェイスでのトップオプションのキーボードナビゲーション](assets/keyboard-navigation-in-aem.gif)

*図：Experience Managerユーザーインターフェイスの上部にあるオプションを、`Tab`keyを使用して移動します。*

ユーザーが [!UICONTROL ヘルプ] オプションから文字列を検索した場合、ナレーターが「ヘルプの検索」を通知して、検索が進行中であることを示します。

## 既存のアセットと表示関連情報の参照 {#browse}

ユーザーインターフェイスでは、キーボードを使用してDAMリポジトリ内の既存のデジタルアセットのリスト、プレビューまたはダウンロード、生成されたレンディションの表示、表示の切り替え、生成されたレンディションの表示、タイムラインとバージョンの履歴の表示、コメントと参照の表示、メタデータの管理を行えます。 [!DNL Assets]

<!-- TBD: Not sure about the following list items mean:

In Experience Manager header section, when navigating in browse mode, screen reader now announces,
  
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
* キーを使用して移動する際のユーザーフォーカスは、バージョンプレビューの閉じるオプションに移動できます。 `Tab`
* キーボードを使用して参照する場合、強調表示された操作可能なユーザーインターフェイスオプションは、コントラストを強化し、より目立つ視覚的な焦点を持ちます。 これにより、焦点を絞った領域をユーザーがより識別しやすくなります。
* サムネール表示からクイックアクションアイコンを削除する `Esc` ためにキーを使用しても、最後にフォーカスされたアイテムからはキーボードフォーカスが削除されません。
* アセットを選択した状態で、Alt + 4キーボードショートカットを押すと、参照リストが開きます。 キーを使用して、ゼロ以外の参照エントリ間を移動でき `Tab` ます。
* アセットに対するコメントは、アセットタイムラインで使用できます。 キーボードでアクセスできます。
* Experience Managerの表示設定には、キーボードからアクセスできます。 ユーザーは、矢印キーを使用してカードの使用可能なサイズ間を移動し、選択してTabキーで移動し、既存の表示設定表示ー内の他の要素を設定できます。

<!-- TBD: Gradually,  as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?

-->

## Manage digital assets {#manage-assets}

CRUD操作、アセットのダウンロード、メタデータの追加など、多くのアセット管理タスクには、様々なアクセスが可能です。 アセットを使用すると、様々な支援テクノロジー（特にスクリーンリーダーやキーボード）を使用してタスクを実行できます。

キーボードを使用してリポジトリを [参照し、アセットをダウンロードする方法を示すビデオデモを参照してください](https://youtu.be/K3dgqMRQJys)。

通常、マーケターや管理者などの役割が行うメタデータ操作では、次の機能によりアクセシビリティが向上します。

* [!UICONTROL アセットのプロパティページの「保存して閉じる] 」オプションが、キーボードを使用してアクセスできるようになりました。
* スクリーンリーダーは、アセットのプロパティボタンの「基本」タブで選択したタグを削除し、選択したタグを削除するオプションを読み上げます。
* 日付選択ポップアップダイアログは、キーボードを使用して使用できます。 日付選択は、オン時間とオフ時間を設定するために使用します。
* キーボードを使用したドラッグ機能は、スクリーンリーダーの参照モードのメタデータスキーマエディターで正しく機能します。
* ユーザーは、キーボードを使用して、フォルダープロパティの「権限」タブにある「閉じたユーザーグループ」の下の追加ユーザーまたはグループフィールドにフォーカスを移動できます。

## デジタルアセットの検索 {#search-assets}

すばやくシームレスなアセット検索の経験により、コンテンツの速度が向上します。 コンテンツ速度の使用例は、主な [!DNL Assets] 機能の一部です。 Omnisearchバーから検索を開始するには、キーボードショートカットを使用する `/` か、スクリーンリーダーと共に使用し `Tab` て、検索オプションをすばやく見つけることができます。 スクリーンリーダーは、検索オプションの検索オプションにフォーカスがある場合、 [!UICONTROL 検索ボタン] (Search Button ![)としてオプション名をナレートします](assets/do-not-localize/search_icon.png)。 ユーザーが押すと、「Omnisearch」ボックス `Return` が開きます。 スクリーンリーダーは、検索ボックスに入力されたキーワードのナレーションだけでなく、提供されるオートコンプリート候補のナレーションも行い [!DNL Experience Manager Assets]ます。 矢印キーと `Return`、を組み合わせて使用し、様々なオプション `Tab` にアクセスして検索をトリガーできます。

検索機能は、次の機能によりさらにアクセスできるようになりました。

* ページタイトルはスクリーンリーダーが使用できるので、ページをアセットの検索ページとして識別するのに役立ちます。
* ユーザーはOmnisearchバー内でアセットを検索します。 Omnisearchバーにアクセスするには、キーボードのキーまたはキーボードのショートカット `/` を使用します。
* 開始が検索キーワードを入力し、キーボードを使用して自動サーチクエリを選択する。 Returnキーを押して、自動推奨文字列を受け入れ、そのアセットを検索します。
* スクリーンリーダーは、検索結果をフィルタリングする際に、フィルターパネルで混合状態のチェックボックス（ネストされた述語のすべてを選択しない限り、第1レベルのチェックボックスは選択されず、完全に選択されます）を識別し、読み上げることができます。
* 「全検索」ボックスを閉じると、ユーザーのフォーカスが検索オプションに移動します。

検索結果をフィルタする場合：

* 検索結果ページには、スクリーンリーダーユーザーの理解を深めるための情報タイトルが表示されます。
* スクリーンリーダーは、検索フィルターのオプションを拡大可能なアコーディオンとして通知します。
* 状態が混在するボタンを持つ述部は、スクリーンリーダーによって通知されます。

## アセットの共有 {#share-assets}

<!-- TBD: Accessibility in DA, BP, AAL? Asked CCE team for AAL content?
-->

アセットを共有する場合、次の機能によってアクセシビリティが向上します。

* ユーザーは、リンクの共有ダイアログの「検索と電子メールアドレス」フィールド内のキーボードを使用して、フォーカスを移動す追加ることができます。

* リンクの共有ダイアログで、参照モードで移動するときに、スクリーンリーダー、

   * ダイアログが読み込まれた後は、直ちに表の情報を読み込まないでください。
   * リストに表示されているすべての自動提案に移動できます。
   * 「電子メールアドレス」フィールドと「検索」フィールドに追加対して、自動提案として表示されます。

## アクセシビリティ [!DNL Dynamic Media] {#dynamic-media-accessibility}

ダイナミックメディアを使用する場合、次の機能を使用するとアクセスしやすくなります。

* ユーザは、キーアセット内 `Flyout`の詳細ビューアを使用して、 、 、 、 、 、 、 `InlineZoom`、 `Shoppable_Banner`、および `Zoom_dark``Zoom_light``ZoomVertical_dark``ZoomVertical_light``Tab`[!DNL Dynamic Media]オプションにフォーカスできます。

## アクセス可能なドキュメント {#accessible-docs}

[!DNL Experience Manager] には、障害を持つユーザーが利用できる、アクセシブルなドキュメントが用意されています。 以下は、コンテンツオファーを今すぐアクセシブルにするのに役立ちますが、Adobeはテンプレートとコンテンツの改善に努め続けます。

* スクリーンリーダーはテキストを読み上げることができます。
* 画像や図には代替テキストが用意されています。
* キーボードナビゲーションが可能です。
* コントラスト比は、ドキュメントWebサイトの一部を強調表示するのに役立ちます。

<!-- 
## More resources for accessibility {#a11y-resources}

TBD: If anyone is aware of AEM-specific resources that help users leverage any accessibility features or use any assistive technology with AEM, please share or leave a link here.
-->

## リリースの機能強化 [!DNL Experience Manager Assets] {#rn-fixes}

個々のリリースで行われた個々の拡張機能のリストについては、各リリースの [リリースノート](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/release-notes/home.html) を参照してください。

>[!MORELIKETHIS]
>
>* [AEMアクセシビリティガイダンス](/help/onboarding/accessibility/web-accessibility.md)
>* [Adobeソリューションの準拠レポート](https://www.adobe.com/accessibility/compliance.html)

