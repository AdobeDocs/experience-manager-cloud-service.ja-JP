---
title: ページプロパティの編集
description: ページに必要なプロパティを定義します
translation-type: tm+mt
source-git-commit: 0dc1e8d2d9e26473f97ce2606f26e97445501136

---


# ページプロパティの編集 {#editing-page-properties}

ページに必要なプロパティを定義できます。これらはページの特性に応じて異なることがあります。例えば、ページによってはライブコピーに接続されていたり、接続されずにライブコピー情報が必要に応じて利用可能な場合があります。

## ページのプロパティ {#page-properties}

プロパティは次のタブに分散しています。

### 基本 {#basic}

* **タイトル**

   * ページのタイトルは様々な場所に表示されます。例えば、「**Web サイト**」タブリストや「**サイト**」カードビュー／リストビューに表示されます。
   * このフィールドは必須です。

* **タグ**

   * ここでは、選択ボックス内のリストを更新することで、ページにタグを追加または削除できます。
   * タグを選択すると、選択ボックスの下のリストに表示されます。このリストからタグを削除するには、x を使用します。
   * 空の選択ボックスに名前を入力して、新しいタグを入力できます。
      * Enter キーを押すと、新しいタグが作成されます。
      * 新しいタグが表示され、その右側にタグが新規であることを示す小さな星が表示されます。
   * ドロップダウン機能を使用して、既存のタグを選択できます。
   * 選択ボックスのタグエントリの上にマウスポインターを合わせると、x が表示されます。これをクリックすると、対象のタグをこのページから削除できます。
   * タグについて詳しくは、[タグの使用](/help/sites-cloud/authoring/features/tags.md)を参照してください。

* **ナビゲーション内で非表示にする**

   * 使用されるサイトでページがページのナビゲーションに表示されるかどうかを示します。

* **ページタイトル**

   * ページで使用されるタイトルです。通常はタイトルコンポーネントで使用されます。空にすると、「**タイトル**」が使用されます。

* **ナビゲーションタイトル**

   * ナビゲーション内で使用するタイトルを別途指定できます（もっと簡潔にする場合など）。空にすると、「**タイトル**」が使用されます。

* **サブタイトル**

   * ページで使用されるサブタイトルです。

* **説明**

   * ページの説明です。ページの目的やその他の必要な追記事項を入力します。

* **オンタイム**

   * 公開されたページがアクティベートされる日付と時間です。公開されると、このページは指定された時間まで休止状態になります。
   * ページを即座に公開する場合（通常のシナリオの場合）、これらのフィールドは空白のままにします。

* **オフタイム**

   * 公開されたページのアクティベートが解除される時間です。
   * すぐにアクションを実行するには、これらのフィールドを空のままにします。

* **バニティ URL**

   * このページのバニティ URL を入力でき、短くより表現力のある URL にすることができます。
   * For example, if the Vanity URL is set to `welcome` to the page identified by the path `/v1.0/startpage` for the website `http://example.com`, then `http://example.com/welcome` would be the vanity URL of `http://example.com/content/v1.0/startpage`
   >[!CAUTION]
   >
   >バニティ URL は次のような特性があります。
   >
   >* 一意である必要があるので、別のページで同じ値が使用されないように注意してください。
   >* regex パターンはサポートされていません。
   >* 既存のページに設定しないでください。


* **バニティ URL をリダイレクト**

   * ページにバニティ URL を使用するかどうかを示します。

### アドバンス {#advanced}

* **言葉遣い**

   * ページの言語です。

* **言語ルート**

   * ページが言語コピーのルートの場合にオンにする必要があります。

* **リダイレクト**

   * このページが自動的にリダイレクトするページを示します。

* **エイリアス**

   * このページで使用されるエイリアスを指定します。
   >[!NOTE]
   >
   >「Alias」は、リソ `sling:alias` ースのエイリアス名を定義するプロパティーを設定します（これは、パスではなく、リソースにのみ影響します）。
   >
   >例：ノードノードのエイリアスを `latin-lang` 定義した場合 `/content/we-retail/spanish` 、このページは、 `/content/we-retail/latin-language`
   >
   >詳しくは、「SEOとURL管理のベストプラクティス」の「ローカライズされたページ名」を参照してください。
   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **&lt;*path*> から継承**

   * ページが継承されるかどうか、およびどこから継承するかを示します。

* **クラウド設定**

   * 設定のパスです。

* **許可されたテンプレート**

   * このサブブランチ内で[使用できるテンプレートのリストを定義](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)します。

* **有効化**（認証要件）

   * ページにアクセスするための認証を有効（または無効）にします。
   >[!NOTE]
   >
   >ページにアクセスできるユーザーグループは、「**[権限](#permissions)**」タブで定義します。

* **ログインページ**

   * ログインに使用されるページです。

* **設定を書き出し**

   * 書き出し設定を指定します。

### サムネイル {#thumbnail}

ページサムネイル画像が表示されます。以下の操作を実行できます。

* **プレビューを生成**

   * サムネイルとして使用するページのプレビューを生成します。

* **画像をアップロード**

   * サムネイルとして使用する画像をアップロードします。

* **画像を選択**

   * サムネールとして使用する既存のアセットを選択します。

* **revert**

   * このオプションは、サムネールを変更した後で使用できるようになります。変更を維持しない場合は、保存前にその変更を元に戻すことができます。

### ソーシャルメディア {#social-media}

* **ソーシャルメディア共有**

   ページで使用可能な共有オプションを定義します。使用可能なオプションを[コアコンポーネントの共有](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/sharing.html)に公開します。

   * **Facebook に対してユーザー共有を有効にする**
   * **Pinterest に対してユーザー共有を有効にする**
   * **優先 XF バリエーション**
      * ページのメタデータの生成に使用するエクスペリエンスフラグメントのバリエーションの定義

### クラウドサービス {#cloud-services}

* **クラウドサービス**

   * Define properties for cloud services. <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).-->

### パーソナライゼーション {#personalization}

* **ContextHub 設定**

   * Select the ContextHub Configuration and Segments Path. <!--Select the [ContextHub Configuration](/help/sites-administering/contexthub-config.md) and [Segments Path](/help/sites-administering/segmentation.md).-->

* **ターゲティング設定**

   * [ブランドを選択してターゲット設定の範囲を指定](/help/sites-cloud/authoring/personalization/targeted-content.md)します。
   >[!NOTE]
   >このオプションを使用するには、ユーザーアカウントがグループに属している必要 `Target Adminstrators`があります。

### 権限 {#permissions}

* **権限**

   * 権限を追加 <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->
   * 閉じられたユーザーグループを編集 <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->
   * 有効な権限<!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->を表示 

### ブループリント {#blueprint}

* **ブループリント**

   * Define properties for a Blueprint page within multi-site management. <!--Define properties for a Blueprint page within [multi-site management](/help/sites-administering/msm.md).-->
   * 変更がライブコピーに適用される条件を制御します。

### ライブコピー {#live-copy}

* **Livecopy**

   * Define properties for a Live Copy page within multi-site management. <!--Define properties for a Live Copy page within [multi-site management](/help/sites-administering/msm.md).-->
   * ブループリントからの変更が適用される条件を制御します。

### サイト構造 {#site-structure}

* **サインアップページ**、**オフラインページ**&#x200B;など、サイト全体にわたる機能を提供するページへのリンクを指定します。

## ページプロパティの編集 {#editing-page-properties-1}

* **サイト**&#x200B;コンソールから：
   * [新しいページを作成](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)します（プロパティのサブセット）
   * Clicking or tapping **Properties**
      * 単一のページ
      * 複数のページ（まとめて編集する場合は、プロパティのサブセットのみを使用できます）
* ページエディターから、次の操作をおこないます。
   * 「**ページ情報**」を使用します（その後、「**プロパティを開く**」をクリック）

### サイトコンソールから - 単一のページ {#from-the-sites-console-single-page}

「**プロパティ**」をクリックまたはタップして、ページのプロパティを定義します。

1. **サイト**&#x200B;コンソールを使用して、プロパティを表示および編集するページの場所に移動します。
1. Select the **Properties** option for the required page using either:
   * [クイックアクション](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * ページのプロパティが該当するタブに表示されます。
1. 必要に応じてプロパティを表示または編集します。
1. その後、「**保存**」を使用して更新内容を保存し、「**閉じる**」を使用してコンソールに戻ります。

### ページの編集中 {#when-editing-a-page}

ページの編集中は、**ページ情報**&#x200B;を使用してページプロパティを定義できます。

1. プロパティを編集するページを開きます。
1. **ページ情報**&#x200B;アイコンを選択して選択メニューを開きます。
1. 「**プロパティを開く**」を選択すると、プロパティを編集するためのダイアログが開きます。プロパティは適切なタブに分類されています。ツールバーの右側にある次のボタンも使用できます。
   * **キャンセル**
   * **保存して閉じる**
1. 「**保存して閉じる**」ボタンを使用して、変更を保存します。

### サイトコンソールから - 複数のページ {#from-the-sites-console-multiple-pages}

**Sites** コンソールから、複数のページを選択し、「**プロパティを表示**」を使用してページのプロパティを表示および編集することができます。これは、ページプロパティの一括編集と呼ばれます。

>[!NOTE]
>
>プロパティの一括編集はアセットに対しても使用できます。操作はよく似ていますが、次の点が異なります。詳しくは、複数のアセットのプロパティの編集を参照してください。
>
>また、バルクエディターも用意されています。このエディターでは、GQL（Google Query Language）を使用して、複数のページからコンテンツを検索できます。コンテンツをバルクエディターで直接編集してから、変更を元のページに保存できます。
<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

次の方法を含む様々な方法で、複数のページを一括編集用に選択することができます。

* **サイト**&#x200B;コンソールの参照時
* **検索**&#x200B;によって複数のページを特定した後

ページを選択して「**プロパティ**」オプションをクリックまたはタップすると、一括プロパティが表示されます。

![ページプロパティの一括編集](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

一括編集ができるのは、次のようなページに限られます。

* 同じリソースタイプを共有する
* ライブコピーの一部ではない
   * いずれかのページがライブコピー中である場合、プロパティを開くときにメッセージが表示されます。

一括編集を開始すると、次の操作をおこなうことができます。

* **表示**

   * 影響を受けるページのリスト
      * 必要に応じて、選択／選択解除できます。
      * タブ
         * 単一ページのプロパティを表示する場合と同様に、プロパティがタブの下で順に並べられます。
   * プロパティのサブセット
      * 選択したすべてのページで使用できるプロパティ（および一括編集で使用できると明示的に定義されたプロパティ）が表示されます。
      * 選択するページを 1 つに減らすと、すべてのプロパティが表示されます。
   * 共通の値を持つ共通のプロパティ
      * 表示モードで表示されるのは、共通の値を持つプロパティのみです。
      * フィールドが複数値（タグなど）の場合は、すべての値が共通の場合に限り、値が表示されます。**&#x200B;一部の値のみが共通の場合は、それらの値は編集時にのみ表示されます。
      * 一般的な値を含むプロパティがない場合は、メッセージが表示されます。

* **編集**

   * 利用可能なフィールドの値を更新できます。
      * 新しい値は、「**完了**」を選択したときに、選択したすべてのページに適用されます。
      * フィールドが複数値（タグなど）の場合は、新しい値を追加するか、共通の値を削除できます。
   * Fields that are common, but have different values across the various pages will be indicated with a special value such as the text `<Mixed Entries>`. そのようなフィールドを編集する際は、データが失われないように、慎重におこなう必要があります。

>[!NOTE]
>
>ページコンポーネントを設定して、一括編集が可能なフィールドを指定できます。ページプロパティの一括編集のためのページの設定を参照してください。
<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
