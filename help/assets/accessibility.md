---
title: ' [!DNL Experience Manager Assets] でのアクセシビリティ'
description: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 障害を持つユーザーに対しては、アクセシビリティ機能の使い方を知っておくこと。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 54%

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

# [!DNL Adobe Experience Manager Assets]の[!DNL Cloud Service] {#accessibility-in-aem-assets}のアクセシビリティ機能

[!DNL Adobe Experience Manager] コンテンツ作成者や発行者は、素晴らしいエクスペリエンスをWeb上で提供できます。Adobeは、[!DNL Experience Manager]のアクセシビリティを向上させ、障害を持つクリエイターを加えようと努めています。 このソフトウェアは、あらゆる種類のユーザーのニーズを満たすように継続的に拡張され、視覚、聴覚、運動、または他の障害を持つ個人を含む世界的な標準に準拠しています。

[!DNL Experience Manager] 準拠する規格を説明する準拠情報を公開し、製品のアクセシビリティ機能の概要を示し、準拠レベルを説明します。アクセシビリティ準拠レポートは、[!DNL Experience Manager]ユーザーが様々な基準の準拠レベルを理解するのに役立ちます。 [!DNL Assets]の改良点は、キーボード、スクリーンリーダー、拡大鏡、その他の支援技術を使って、すべてのユーザーが簡単にインターフェイスを使用できるようにするものです。

[!DNL Experience Manager] は、次の標準を様々なレベルでサポートしています。

* [Web Content Accessibility Guidelines（WCAG）2.1](https://www.w3.org/TR/WCAG/)
* [再生法第508条を改正](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) by W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)

準拠レベルの詳細を含むレポートを読むには、[アクセシビリティ準拠レポート](https://www.adobe.com/accessibility/compliance.html) (ACR)ページを参照してください。

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](/). -->

## 支援テクノロジー {#at-support}

障害を持つユーザーは、頻繁にハードウェアとソフトウェアを利用してWebコンテンツにアクセスし、ソフトウェア製品を使用します。 これらのツールは、支援テクノロジーと呼ばれます。[!DNL Experience Manager Assets] ソフトウェアの主要機能を使用する場合、次の種類の支援テクノロジー(AT)を使用できます。

* スクリーンリーダーとスクリーン虫めがね。
* 音声認識ソフトウェア
* キーボードの使用 - ナビゲーションとショートカット
* スイッチコントロール、更新可能な点字ディスプレイ、その他のコンピュータ入力デバイスを含む支援ハードウェア
* UI 拡大ツール

## アクセシブルな [!DNL Experience Manager Assets] の使用例 {#accessible-assets-use-cases}

[!DNL Experience Manager] のアクセシビリティ機能は、[!DNL Experience Manager] ユーザーとその顧客の 2 つの主要な要件に対応しています。

* コンテンツデザイナーやクリエーターには、アクセシブルなコンテンツを作成して公開する機能が提供されます。作成されたコンテンツは、顧客や Web サイト訪問者によって使用されます。障害を持つユーザーは、支援テクノロジーを使用してコンテンツを使用できます。詳しくは、「[Web アクセシビリティのガイドライン](/help/onboarding/accessibility/web-accessibility.md)」を参照してください。
* [!DNL Experience Manager] また、障害を持つユーザーや管理者は、ユーザーインターフェイスやコントロールにアクセスして、コンテンツの作成と管理を行うこともできます。障害を持つユーザーは、支援テクノロジーを使用して、[!DNL Assets] 機能をナビゲート、使用、管理できます。

[!DNL Assets] の主な機能は以前よりもアクセスしやすく、定期的にアップデートされており、グローバル標準への準拠が改善されています。[!DNL Assets]のCRUD操作には、ある程度のアクセシビリティが組み込まれています。 アセットの追加、管理、検索、配布などの DAM ワークフローには、キーボードショートカット、スクリーンリーダーテキスト、カラーコントラストなどの支援を受けてアクセスできます。

## キーボードの使用のサポート {#keyboard-use}

クリックやポインターを使用するユーザーインターフェイス要素の多くは、キーボードを使用して操作することもできます。キーボードを使用して UI 要素にフォーカスし、適切なアクションを実行できます。キーボードショートカットを使用して、UI 要素にフォーカスせずに、コマンドやアクションを直接トリガーすることもできます。例えば、ユーザーは、キーボードを使用してユーザーインターフェイスコントロールに移動し、`Return`を選択し、`Alt + 2`キーボードショートカットを選択することで、左側のアセットのタイムラインを開くことができます。

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}のキーボードショートカット

[!DNL Assets]の次の操作は、一覧に示したキーボードショートカットで動作します。 [!DNL Experience Manager]コンソールに適用されるほとんどのキーボードショートカットは、[!DNL Assets]にも適用されます。 コンソールの[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を参照してください。 キーボードショートカットを[有効または無効にする方法](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を参照してください。

| ユーザーインターフェイスまたはシナリオ | キーボードショートカット | アクション |
|---|---|---|
| [!DNL Assets]ユーザーインターフェイスの列表示 | 上向き矢印キーと下向き矢印キー | 同じ階層内のファイルやフォルダーに移動します。 |
| [!DNL Assets]ユーザーインターフェイスの列表示 | 左向き矢印キーと右向き矢印キー | 現在のフォルダーの上または下のファイルとフォルダーに移動します。 |
| [!DNL Assets]内のフォルダの参照 | `/` | オムニサーチボックスを開いて検索を呼び出します。 |
| [!DNL Assets] コンソール | ` | サイドパネルを切り替えます。 |
| [!DNL Assets] コンソール | `Alt + 1` | コンテンツツリーを開きます。 |
| [!DNL Assets] コンソール | `Alt + 2` | [!UICONTROL ナビゲーション]左側のナビゲーションパネルを開きます。 |
| [!DNL Assets] コンソール | `Alt + 3` | 選択したアセットの[!UICONTROL タイムライン]を表示します。 |
| [!DNL Assets] コンソール | `Alt + 4` | 選択したアセットのライブコピーの参照を開きます。 |
| [!DNL Assets] コンソール | `Alt + 5` | 検索を呼び出して、選択したフォルダー内で検索をおこないます。 |
| アセットまたはフォルダーが選択されている | Backspace | 選択したアセットまたはフォルダーを削除します。 |
| アセットまたはフォルダーが選択されている | `p` | 選択したアセットのプロパティページを開きます。 |
| アセットまたはフォルダーが選択されている | `e` | 選択したアセットを編集します。 |
| アセットまたはフォルダーが選択されている | `m` | 選択したアセットを移動します。 |
| アセットまたはフォルダーが選択されている | `Ctrl + c` | 選択したアセットをコピーします。 |
| アセットまたはフォルダーが選択されている | `Esc` | 選択を解除します。 |
| ダイアログボックスが開き、フォーカスがある | `Esc` | ダイアログボックスを閉じます。 |
| DAM 内のフォルダー内 | `Ctrl + v` | コピーしたアセットを貼り付けます。 |
| [!DNL Assets] コンソール | `Ctrl + A` | すべてのアセットを選択します。 |
| アセットプロパティページ | `Ctrl + S` | 変更を保存します。 |
| [!DNL Assets] コンソール | `?` | キーボードショートカットのリストを表示します。 |

## サインインと [!DNL Assets] ユーザーインターフェイスの操作 {#login}

ユーザーは、キーボードを使用してログイン先に移動し、サインインフィールドに入力することができます。 ログインページのユーザ名とパスワードの組み合わせが正しくないことに起因するエラーメッセージは、エラーが発生するたびにスクリーンリーダーによって通知されます。

ログイン後、DAMユーザーはキーボードを使用して[!DNL Assets]ユーザーインターフェイス内を移動できます。 左側のパネル、メニュー、ユーザープロファイル、検索バー、ファイルとフォルダー、管理および設定などのユーザーインターフェイス要素は、キーボードを使用して移動できます。 キーボードのナビゲーション順序は、左から右、上から下です。キーボードを使用してナビゲーションを行う場合、フォーカス時にアクション可能なオプションが、カラーコントラストの高いハイライトで表示され、スクリーンリーダーによってナレーションされます。 メニュー内のフォーカスされたオプションの状態（展開、折りたたみ、混在など）は、必要に応じて、スクリーンリーダーによって通知されます。 また、アクション可能なオプションの目的は、外観やUIの配置などではなく、スクリーンリーダーによって通知されます。

メニューからヘルプまたはユーザープロファイルのオプションを展開すると、スクリーンリーダーから適切なオプションまたはステータスが通知されます。ユーザープロファイルオプションを展開すると、キーボードを使用して使用可能なオプションを選択できるようになりす。例えば、管理者は別のユーザーを装うことができます。 ユーザーが[!UICONTROL ヘルプ]オプションから文字列を検索すると、ナレーターが「ヘルプの検索」を通知し、検索が進行中であることを示します。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## アセットと表示を参照し、関連情報{#browse}

[!DNL Assets] ユーザーインターフェイスでは、キーボードを使用して DAM リポジトリー内の既存のデジタルアセットの一覧表示、プレビューまたはダウンロード、生成されたレンディションの表示、表示の切り替え、タイムラインとバージョンの履歴の表示、コメントと参照の表示、メタデータの管理をおこなうことができます。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

アセットリポジトリーを参照する際、次の機能によりアクセシビリティが向上します。

* アイコン名の代わりにアイコンの目的や機能を表現する代替テキストがスクリーンリーダーによってアナウウンスされる。
* キーボードキーを使用してアセットの参照リストのインタラクティブユーザーインターフェイスオプションにアクセスし、フォーカスすることができる。
* リスト表示の各行の要素は、スクリーンリーダーによって同じ行の要素としてアナウンスされる。
* `Tab`キーを使用して移動する場合、フォーカスはバージョンプレビューの閉じるオプションに移動できます。
* キーボードを使用して参照する場合、強調表示された操作可能なユーザーインターフェイスオプションのコントラストが強化され、より目立つ視覚的なフォーカスを持つようになる。これにより、フォーカスされた領域がより識別しやすくなる。
* サムネール表示からクイックアクションアイコンを削除するために `Esc` キーを使用しても、最後にフォーカスされたアイテムからはキーボードフォーカスが削除されない。
* アセットを選択した状態で、`Alt + 4`キーボードショートカットを選択すると、左側のレールに[!UICONTROL 参照]リストが開きます。 `Tab`キーを使用して、ゼロ以外の参照エントリ間を移動できます。 ゼロ以外の参照エントリを参照するだけで、作業やキー操作を省力化できます。
* アセットに対するコメントは、アセットタイムラインで使用でき、キーボードまたはキーボードショートカットを使用して左側のレールにアクセスすると、アクセスできます。
* [!UICONTROL 表示] 設定 [!DNL Experience Manager] には、キーボードを使用してアクセスできます。ユーザーは、矢印キーを使用して使用可能なカードのサイズ間を移動し、選択してTabキーで移動し、既存の表示設定表示ー内の他の要素を設定できます。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## デジタルアセットの管理{#manage-assets}

CRUD操作、アセットのダウンロード、メタデータの追加など、多くのアセット管理タスクには、様々な角度からアクセスできます。 [!DNL Assets] を使用すると、様々な支援テクノロジー（特にスクリーンリーダーやキーボード）を使用してタスクを実行できます。

キーボードを使用して[リポジトリーを参照し、アセットをダウンロードする](https://youtu.be/K3dgqMRQJys)方法を示すビデオデモを参照してください。

通常、マーケターや管理者などの役割でおこなうメタデータ操作では、次の機能によりアクセシビリティが向上します。

* アセットのプロパティページの「[!UICONTROL 保存して閉じる][!UICONTROL  」オプションが、キーボードを使用してアクセスできるようになりました。]
* スクリーンリーダーは、アセット]プロパティ[!UICONTROL の「基本[!UICONTROL 」タブで選択したタグを削除するオプションを読み上げます。]
* ユーザーは、日付選択ポップアップダイアログをキーボードと共に使用できます。 日付選択ユーザーインターフェイス要素を使用して、オン時間とオフ時間を設定し、「日付」を選択します。
* キーボードを使用したドラッグ機能は、スクリーンリーダーのブラウズモードの[!UICONTROL メタデータスキーマエディター]で正しく機能します。
* ユーザーは、キーボードを使用して、フォルダー[!UICONTROL 追加プロパティ]の[!UICONTROL 権限]タブにある[!UICONTROL 閉じたユーザーグループ]の下のユーザーまたはグループフィールドにフォーカスを移動できます。

## デジタルアセットの検索 {#search-assets}

すばやくシームレスなアセット検索の経験により、コンテンツの速度が向上します。コンテンツ速度の使用例は、主な [!DNL Assets] 機能の一部です。オムニサーチバーから検索を開始するには、キーボードショートカット `/` を使用するか、スクリーンリーダーと共に `Tab` を使用して、検索オプションをすばやく見つけることができます。スクリーンリーダーは、検索オプション![検索オプション](assets/do-not-localize/search_icon.png)にフォーカスがある場合、オプションの名前を「検索ボタン」としてナレートします。 ユーザーは`Return`を選択してOmnisearchボックスを開くことができます。 スクリーンリーダーは、検索ボックスに入力されたキーワードのナレーションだけでなく、[!DNL Experience Manager Assets] で提供される提案のナレーションもおこないます。矢印キー、`Return`、`Tab`を組み合わせて使用し、様々なオプションにアクセスして検索をトリガーできます。

検索機能は、次の機能でアクセスできます。

* ページタイトルはスクリーンリーダーが使用できるので、ページをアセットの検索ページとして識別するのに役立つ。
* ユーザーは、Omnisearchフィールド内からアセットを検索します。 ユーザーは、キーボードナビゲーションまたはキーボードショートカット`/`を使用して開くことができます。
* 開始が検索キーワードを入力し、矢印キーを使用して自動サーチクエリを選択できます。 ハイライト表示された提案は`Return`キーを使用して選択でき、選択された提案はアセットで検索されます。
* スクリーンリーダーは、検索結果をフィルタリングする際に、フィルターパネルで混在状態のチェックボックス（ネストされた述語のすべてを選択しない限り、第1レベルのチェックボックスは選択されず、完全に選択されます）を識別し、読み上げることができます。
* 「オムニサーチ」ボックスを閉じると、ユーザーのフォーカスが検索オプションに移動する。

検索結果をフィルターする場合：

* 検索結果ページには、スクリーンリーダーユーザーがより深く理解できるように分かりやすいタイトルが表示される。
* スクリーンリーダーは、検索フィルターのオプションを拡大可能なアコーディオンとして通知する。
* 状態が混在するオプションを持つ述語は、スクリーンリーダーによって通知されます。

## アセットの共有 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

アセットを共有する場合、次の機能によってアクセシビリティが向上します。

* ユーザーは、リンク共有ダイアログの「電子メールアドレスを検索／追加」フィールド内でキーボードを使用して、フォーカスを移動することができる。

* リンク共有ダイアログで、参照モードで移動するときに、スクリーンリーダーに次の現象が発生する。

   * ダイアログが読み込まれてすぐに、テーブル情報を読み上げない。
   * リストに表示されているすべての提案に移動できる。
   * 「電子メールアドレスを検索／追加」フィールドに対して表示された提案を読み上げる。

## アクセス可能なドキュメント {#accessible-docs}

[!DNL Experience Manager] には、障害を持つユーザーが使用できる、アクセシブルなドキュメントが用意されています。アドビはテンプレートとコンテンツの改善に努めています。現時点では以下の機能が、コンテンツをアクセシブルにするのに役立ちます。

* スクリーンリーダーはテキストを読み上げることができる。
* 画像や図には代替テキストが用意されている。
* キーボードナビゲーションが可能である。
* コントラスト比は、ドキュメント Web サイトの一部を強調表示するのに役立つ。

## フィードバックを提供{#a11y-feedback}

アクセシビリティに関するフィードバックを提供し、質問をし、製品の改良点をリクエストするには、次の方法を使用します。

* [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)のフォームに入力します。
* access@adobe.comまで電子メールでお問い合わせください。

>[!MORELIKETHIS]
>
>* [各リリースで行われた機能強化のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)。
>* [[!DNL Adobe Experience Manager] アクセシビリティガイダンス](/help/onboarding/accessibility/web-accessibility.md)。
>* [Adobeソリューションの準拠レポート(ACR)およびVPATリスト](https://www.adobe.com/accessibility/compliance.html)。

