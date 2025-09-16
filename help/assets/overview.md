---
title: AEM でのデジタルアセット管理の Assets as a Cloud Service の概要
description: AEM でのデジタルアセット管理の Assets as a Cloud Service の概要
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: f72f72e87dabe89cafc0a56feb35f58ae1a97dfb
workflow-type: ht
source-wordcount: '5078'
ht-degree: 100%

---

# AEM でのデジタルアセット管理の Assets as a Cloud Service の概要 {#assets-as-cloud-service-digital-asset-management-aem}

AEM Assets as a Cloud Service は、クラウドネイティブな PaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を行うだけでなく、AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。これらすべては、常に最新で常に可用性が高く常に学習可能なシステム内から行います。

アドビでは、デジタルアセットを最大限に活用する堅牢なデジタルアセット管理（DAM）ソリューションを提供しています。Adobe Experience Manager Assets には、要件に合わせて同じ Cloud Services リポジトリを使用する 2 つの異なるエクスペリエンスがあります。AEM Assets のペルソナベースのエクスペリエンスについて詳しくは、[デジタルアセット管理で使用可能なペルソナベースのエクスペリエンス](#persona-based-experiences)を参照してください。

AEM Assets Ultimate および AEM Assets Prime の製品について詳しくは、[Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) および [Assets as a Cloud Service Prime](/help/assets/assets-prime.md) を参照してください。

アドビのデジタルアセット管理の主な機能には、次のようなものがあります。

![add-tags](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB アセットの取り込み]

## アセットの取り込み {#asset-ingestion}

一括読み込み機能を使用すると、Azure、AWS、Google Cloud、Dropbox、OneDrive などのデータソースから多数のアセットを Assets as a Cloud Service に直接読み込むことができます。

管理ビューまたはアセットビューを使用して、一括読み込み操作を実行できます。アセットビューには、管理ビューと比較して、より多くのデータソースオプションが用意されています。

Adobe Experience Manager では、web ブラウザーユーザーインターフェイスに加えて、デスクトップ上の他のクライアントもサポートしています。Web ブラウザーを使用しなくても、これらのクライアントでアップロード操作を行うことができます。

* Adobe Asset Link を使用すると、Adobe Photoshop、Adobe Illustrator、Adobe InDesign の各デスクトップアプリケーションで Adobe Experience Manager 内のアセットにアクセスできます。開いているドキュメントを Experience Manager にアップロードできます。これらのデスクトップアプリケーションにある Adobe Asset Link インターフェイスを通じて直接アップロードできます。

* Adobe Experience Manager デスクトップアプリケーションを利用すると、アセットのファイルタイプやアセットを操作するネイティブアプリケーションによらず、デスクトップ上でアセットを簡単に操作できます。ブラウザーアップロードではフラットなファイルリストのアップロードのみサポートしているので、ネストされたフォルダー階層内のファイルをローカルファイルシステムからアップロードする際に便利です。

これらのアセット取り込みツールに関する詳細なドキュメントにアクセスするには、次のリンクを使用します。

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="一括読み込みツール" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong>一括読み込みツールの使用</strong>
      </a>
   </div>
   <p>
      <em>データソースから多数のアセットを直接読み込む方法の詳細情報</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/ja/docs/experience-manager-desktop-app/using/get-started">
   <img alt="AEM デスクトップアプリケーションの使用" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/ja/docs/experience-manager-desktop-app/using/get-started">
      <strong>AEM デスクトップアプリケーションの使用</strong>
      </a>
   </div>
   <p>
      <em>AEM デスクトップアプリケーションを使用して、ネストされたフォルダー階層内のファイルをローカルファイルシステムからアップロードする方法について説明します。</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html">
   <img alt="Adobe Asset Link の使用" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html">
      <strong>Adobe Asset Link の使用</strong>
      </a>
   </div>
   <p>
      <em>詳しくは、Creative Cloud アプリケーションを使用して、Adobe Experience Manager にアセットをアップロードする方法を参照してください。</em>
   </p>
</td>
</table>

>[!TAB AI を活用した機能]

**スマートタグ**：スマートタグは Adobe Sensei の人工知能フレームワークを使用して、タグ構造とビジネス上の分類に基づいて画像認識アルゴリズムのトレーニングを行います。その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。デフォルトでは、AEM は、アップロードされたアセットにスマートタグを自動的に適用します。

**インテリジェントなカラーベースのタグ付けと検索**：AEM Assets は、Adobe Sensei AI 機能を使用して画像内のカラーを識別し、取り込み時に自動的にこれらの特性をタグとして適用します。これらのタグを使用すると、画像のカラー構成に基づいて検索エクスペリエンスを強化できます。

**AI 生成のメタデータ**：AEM Assets では AI を使用して、タイトル、説明、キーワードなどのメタデータが自動生成されます。これらの AI で生成されたフィールドは、メタデータの精度を高め、アセットの検索、分類および推奨を容易にします。このアプローチでは、手動でのタグ付けが不要なために効率が向上するだけでなく、大量のデジタルコンテンツ間の一貫性とスケーラビリティも確保できます。

**AI を活用したアセットの一括名前変更**：[アセットビューでは、人工知能を使用して複数のアセットの名前を一度に変更できます](/help/assets/bulk-rename-assets-view.md)。 複数のファイルを一度に選択し、まとめて名前を変更できます。対話型の名前変更プロンプトの例には、*すべてのファイルを「my-file」に変更して増分番号を追加*&#x200B;や&#x200B;*ファイルに 001、002 などのプレフィックスを付けて。英語に翻訳*&#x200B;などが含まれます。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets のスマートタグ" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>アセットへの AI スマートタグの追加</strong>
      </a>
   </div>
   <p>
      <em>アップロードしたアセットにスマートタグを自動的に適用する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="インテリジェントカラーベースのタグの追加" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>インテリジェントカラーベースのタグの追加</strong>
      </a>
   </div>
   <p>
      <em>取り込み時にカラーベースのタグを自動的に適用する方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="AI 生成のメタデータ" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>AI 生成のメタデータ</strong>
      </a>
   </div>
   <p>
      <em>AI を使用して、タイトルや説明などのアセットメタデータを生成します。</em>
   </p>
</td>
</table>

**コンテキスト検索**：AEM Assets では、テキストプロンプトを定義して、リポジトリで使用可能なアセットを検索できます。Experience Manager Assets は、テキストプロンプトを検索フィルターに自動変換し、検索結果を表示します。フィルターパネルを使用して自動フィルターを表示および変更すると、検索結果をさらに絞り込むことができます。対話型テキストプロンプトの例を次に示します。

* *高さ 200 ピクセル、幅 100 ピクセル以上で、ビーチと澄んだ空の画像*。
* *高さが 1500 および 2500 ピクセルで、過去 1 か月以内に作成された、期限内の承認された青空の画像が必要です*。

**AEM 内で Adobe Firefly を使用してアセットを生成**：AEM Assets では、検索クエリで結果が返されない場合に、Adobe Firefly をリアルタイムで使用してアセットを生成できます。また、AEM Assets では、生成した画像を AEM Assets ユーザーインターフェイス内から AEM Assets リポジトリにアップロードすることもできます。

**Adobe Express との統合**：AEM Assets は Adobe Express とネイティブに統合されているので、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。また、Express 内で Adobe Firefly 人工知能を使用して、シンプルなテキストプロンプトを使用して画像を生成し、Express キャンバスに配置することもできます。その後、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="コンテキスト検索" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong>コンテキスト検索</strong>
      </a>
   </div>
   <p>
      <em>シンプルなテキストプロンプトを使用してアセットを検索する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="Adobe Firefly を使用したアセットの生成" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>Adobe Firefly を使用したアセットの生成</strong>
      </a>
   </div>
   <p>
      <em>Adobe Firefly を使用してリアルタイムでアセットを生成します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Adobe Express との統合" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Adobe Express との統合</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets ユーザーインターフェイス内で Adobe Express AI 機能を使用します。</em>
   </p>
</td>
</table>

**スマートイメージング**：スマートイメージングは、顧客のブラウザー機能に応じて画像の形式とファイルサイズを自動的に最適化することで、画像アセット配信のパフォーマンスをさらに向上させます。既存の画像プリセットと連携し、配信時にインテリジェンスを使用します。このインテリジェンスにより、ブラウザーとネットワーク接続速度に応じて、画像ファイルのサイズがさらに縮小されます。

**スマート切り抜き**：Adobe Sensei AI 機能を使用して、どのような画像やビデオでも重要な部分を自動的に検出し、切り抜いて維持管理します。画面サイズに関係なく、意図した目標地点をキャプチャして、面倒な手動タスクを排除し、あらゆるデバイスや画面で美しく表示される、高画質で読み込みが速い画像とビデオを配信します。

**AI 生成のビデオキャプション**：Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。この機能は、正確なキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。キャプションは、元のオーディオ、追加のオーディオトラック、またはビデオプロパティページの `Captions and Audio` タブで提供される追加のキャプションから生成されます。60 を超える言語がサポートされているので、ビデオを公開する前にキャプションを確認およびプレビューできます。
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="スマートイメージング" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>スマートイメージング</strong>
      </a>
   </div>
   <p>
      <em>ユーザーのブラウザーの機能とネットワーク速度に基づいて、画像の形式とファイルサイズを最適化します。</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
   <img alt="スマート切り抜き" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
      <strong>スマート切り抜き</strong>
      </a>
   </div>
   <p>
      <em>AI を使用して、どのような画像やビデオでも重要な部分を自動的に検出し、切り抜いて維持管理します</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="AI 生成のビデオキャプション" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>AI 生成のビデオキャプション</strong>
      </a>
   </div>
   <p>
      <em>人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。</em>
   </p>
</td>
</table>

>[!TAB アセット検出]

## アセット検出 {#asset-discovery}

アセットを AEM Assets に読み込んだ後、膨大なコレクションから適切なアセットをすばやく見つけることが課題となります。

AEM Assets には、適切なアセットをすばやく見つけるのに役立つ機能が用意されています。これらの機能には、AI 生成のタグ付け（スマートタグ）、カスタマイズされたメタデータ、強化された検索機能が含まれます。

**メタデータ管理**：メタデータは、アセットジャーニーを開始する際の最も重要な側面です。アセットがユーザーに配布されると、メタデータの管理は管理者の制御から完全に外れます。効果的なアセットメタデータにより、任意の DAM ツールの最終的な宛先である検索が向上します。


**メタデータフォーム**：Assets as a Cloud Service には、デフォルトで多数の標準メタデータフィールドが用意されています。追加のメタデータニーズがあり、ビジネス固有のメタデータを追加するには、さらに多くのメタデータフィールドが必要です。メタデータフォームを使用すると、ビジネスごとにアセットの詳細ページにカスタムメタデータフィールドを追加できます。ビジネス固有のメタデータにより、アセットのガバナンスと検出が向上します。フォームは、ゼロから作成することも、既存のフォームを再利用することもできます。

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="アセットビューでのメタデータの管理" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>アセットビューでのメタデータの管理</strong>
      </a>
   </div>
   <p>
      <em>アセットビューを使用したメタデータとメタデータフォームを管理する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
   <img alt="メタデータ管理のベストプラクティス" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
      <strong>メタデータ管理のベストプラクティス</strong>
      </a>
   </div>
   <p>
      <em>アセットを AEM に移行する前と後にメタデータを管理する方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="Adobe Asset Link の使用" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong>管理ビューでのメタデータの管理</strong>
      </a>
   </div>
   <p>
      <em>管理ビューを使用したメタデータとメタデータフォームを管理する方法の詳細情報。</em>
   </p>
</td>
</table>

**スマートタグ**：スマートタグは Adobe Sensei の人工知能フレームワークを使用して、タグ構造とビジネス上の分類に基づいて画像認識アルゴリズムのトレーニングを行います。その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。デフォルトでは、AEM は、アップロードされたアセットにスマートタグを自動的に適用します。

**アセットを検索**：適切なメタデータを用意すると、AEM Assets で様々な演算子、ワイルドカード、高度なクエリ、カスタムフィルターを使用して検索できます。

**コンテキスト検索**：AEM Assets には、テキストプロンプトを定義して、リポジトリで使用可能なアセットを検索できるコンテキスト検索機能も用意されています。Experience Manager Assets は、テキストプロンプトを検索フィルターに自動変換し、検索結果を表示します。フィルターパネルを使用して自動フィルターを表示および変更すると、検索結果をさらに絞り込むことができます。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets のスマートタグ" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>アセットへのスマートタグの追加</strong>
      </a>
   </div>
   <p>
      <em>アップロードしたアセットにスマートタグを自動的に適用する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="検索アセットビュー" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>アセットビューでのアセットの検索</strong>
      </a>
   </div>
   <p>
      <em>アセットビューでコンテキスト検索やその他の検索機能を効果的に使用する方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="検索のベストプラクティス" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong>検索のベストプラクティス</strong>
      </a>
   </div>
   <p>
      <em>AEM ユーザーが基本レベルから高度なレベルの検索を実行するのに役立つ様々なシナリオの詳細情報。</em>
   </p>
</td>
</table>

>[!TAB アセットのガバナンス]

## アセットの管理とガバナンス {#asset-management-governance}

アセットを AEM Assets にアップロードし、メタデータを設定して検出性を高めると、アセットビューの使いやすいインターフェイスを使用して、様々なデジタルアセット管理タスクを実行できます。

**アセット管理タスク**：一部の基本的なタスクには、検索、ダウンロード、移動、コピー、名前変更、削除、更新、編集などの操作が含まれます。

また、アセットのバージョンの管理、アセットのステータスの設定、アセットの有効期限の設定も行うことができます。

**マイワークスペース**：アセットビューには、ウィジェットを提供するカスタマイズ可能なワークスペースも含まれます。これらのウィジェットは、Assets ユーザーインターフェイスの主要な領域と、最も関連性の高い情報に簡単にアクセスできます。このページは、作業項目の概要を示し、主要なワークフローにすばやくアクセスできるワンストップソリューションとして機能します。

**Content Credentials**：AEM Assets がサポートするもう 1 つの強力な機能は、Content Credentialsです。ブランドは、コンテンツの透明性、AI の開示、アセットの改ざん防止について、これまで以上に関心を寄せています。アドビのコンテンツ認証イニシアチブ（CAI）は、Coalition for Content Provenance and Authenticity（C2PA）技術標準に準拠したツールを作成しています。新しい種類の暗号化された改ざん防止メタデータである Content Credentials は、閲覧者がコンテンツの系統を理解し、ブランドアセットの整合性を確保するのに役立ちます。これらには、デジタルアセットの履歴に関するインサイトを提供する様々な来歴データを含めることができます。

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="アセット管理タスク" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>アセット管理タスク</strong>
      </a>
   </div>
   <p>
      <em>基本的なアセット管理タスクと高度なアセット管理タスクを実行する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="マイワークスペース" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>マイワークスペース</strong>
      </a>
   </div>
   <p>
      <em>マイワークスペースを使用して、Assets ユーザーインターフェイスの主要な領域にすばやくアクセスする方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Content Credentials</strong>
      </a>
   </div>
   <p>
      <em>Content Credentials を使用して、デジタルアセットの履歴に関するインサイトを取得します。</em>
   </p>
</td>
</table>

**コレクション**：AEM Assets では、アセットをコレクションに整理することもできます。 コレクションとは、Adobe Experience Manager Assets ビュー内の一連のアセット、フォルダーまたはその他のコレクションのことです。コレクションを使用して、ユーザー間でアセットを共有します。フォルダーとは異なり、1 つのコレクションに異なる複数の場所のアセットを含めることができます。1 人のユーザーと複数のコレクションを共有できます。各コレクションには、アセットへの参照が含まれます。アセットの参照整合性はコレクション間で維持されます。

**通知**：アセットビュー通知を使用すると、リポジトリで使用可能なアセット、フォルダーまたはコレクションで実行された操作を監視できます。通知を送信するコンテンツを選択し、購読する必要があります。また、通知を受け取るカテゴリを設定することもできます。

**重複アセットを検出**：AEM Assets では、重複アセットの検出もサポートしています。DAM ユーザーがリポジトリに既に存在する 1 つ以上のアセットをアップロードした場合、Adobe Experience Manager は重複を検出し、ユーザーに通知します。



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="コレクションを管理" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>コレクションの管理</strong>
      </a>
   </div>
   <p>
      <em>アセットをコレクションに整理して、アセットを効率的に共有する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="通知の設定" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>通知の設定</strong>
      </a>
   </div>
   <p>
      <em>アセット、フォルダーまたはコレクションで実行された操作を監視する通知を設定する方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="重複アセットの検出" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>重複アセットの検出</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets にアップロードされた重複アセットを検出し、ユーザーに通知します。</em>
   </p>
</td>
</table>

>[!TAB 統合]

## アドビアプリケーションおよびアドビ以外のアプリケーションとの統合 {#integration-adobe-non-adode-apps}

AEM Assets は、様々な アドビアプリケーションおよびアドビ以外のアプリケーションとシームレスに統合できます。使用可能な統合の概要を次に示します。

+++**アドビアプリケーションおよびアドビ以外のアプリケーションとの統合**

* **OpenAPI 機能を備えた Dynamic Media**：[OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) は、[検索](/help/assets/search-assets-api.md)および[配信](/help/assets/deliver-assets-apis.md) API の包括的なセットを提供します。これにより、開発者は簡単にアセットの配信をアプリケーションと統合できます。アプリケーションには、アドビおよびサードパーティのアプリケーションが含まれます。承認済みアセットを検索および選択するマイクロフロントエンドのアセットセレクターのユーザーインターフェイスを提供します。セレクターは、React JS、Angular JS、Vanilla JS などの JavaScript フレームワークに基づくすべてのアプリケーションと簡単に統合できます。

* **マイクロフロントエンドアセットセレクター**：マイクロフロントエンドアセットセレクターは、Experience Manager Assets リポジトリと簡単に統合できるユーザーインターフェイスを提供します。ユーザーはこれにより、リポジトリで使用可能なデジタルアセットを参照または検索できます。その後、アプリケーションのオーサリングエクスペリエンスで使用できます。
アセットセレクターは、アドビアプリケーションまたはアドビ以外のアプリケーションと統合できます。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="OpenAPI 機能を備えた Dynamic Media の概要" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>OpenAPI 機能を備えた Dynamic Media の概要</strong>
      </a>
   </div>
   <p>
      <em>主なメリットと有効化の方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Experience Manager でのアセットへのアクセスの制限" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Experience Manager でのアセットへのアクセスの制限</strong>
      </a>
   </div>
   <p>
      <em>承認済みアセットへのアクセスを制限するために役割を設定します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="アセットセレクター" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>マイクロフロントエンドアセットセレクター</strong>
      </a>
   </div>
   <p>
      <em>マイクロフロントエンドアセットセレクターをアドビアプリケーションまたはアドビ以外のアプリケーションと統合する方法の詳細情報。</em>
   </p>
</td>
</table>

+++

+++**アドビアプリケーションとのネイティブ統合**

* **Adobe Workfront との統合**：[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] の統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上させ市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

  アドビでは、[ [!DNL Workfront]  と  [!DNL Adobe Experience Manager Assets]  をネイティブに統合](https://experienceleague.adobe.com/ja/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations)することを提案しています。

* **Figma との統合**：AEM Assets は Figma とネイティブに統合されているので、デザイナーは AEM Assets に保存されているアセットに Figma ユーザーインターフェイスから直接アクセスできます。AEM Assets で管理されているコンテンツを Figma キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。Figma コミュニティページで利用可能な AEM Assets コネクタにアクセスするには、[こちら](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)をクリックします。

* **Adobe Express とのネイティブ統合**：AEM Assets は Adobe Express とネイティブに統合されているので、Adobe Express ユーザーインターフェイス内から AEM Assets に保存されているアセットに直接アクセスできます。AEM Assets で管理されているコンテンツを Express キャンバスに配置し、新しいコンテンツや編集したコンテンツを AEM Assets リポジトリに保存できます。

* **AEM Assets を Creative Cloud に接続**：Experience Manager Assets には、別の IMS 組織にプロビジョニングされた Creative Cloud 権限に接続できます。この機能を使用すると、Express ライブラリや Creative Cloud ライブラリなどの最新の Creative Cloud 統合を AEM Assets で使用できます。Creative Cloud 製品と AEM Assets が別の IMS 組織にプロビジョニングされている場合は、異なる Creative Cloud 組織に接続して、2 つのソリューション間で統合されたワークフローを実行できます。

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="Adobe Workfront との統合" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>Adobe Workfront との統合</strong>
      </a>
   </div>
   <p>
      <em>Adobe Workfront と統合して、作業のライフサイクル全体を一元的に管理します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Figma との統合" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>Figma との統合</strong>
      </a>
   </div>
   <p>
      <em>Figma ユーザーインターフェイス内から AEM Assets に保存されているアセットにアクセスします </em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Adobe Express とのネイティブ統合" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Adobe Express とのネイティブ統合</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets 内で使用可能なアセットを Express キャンバスに配置し、更新したアセットを AEM に保存します。</em>
   </p>
</td>


</table>


* **Adobe Journey Optimizer との統合**：Adobe Experience Manager Assets を使用して、マーケティングワークフローとクリエイティブワークフローを統合します。Adobe Journey Optimizer とネイティブに統合され、Assets as a Cloud Service にアクセスして、デジタルアセットを保存、管理、検出、配布できます。 メッセージへの入力に使用できるアセットを一元管理した単一のリポジトリを提供します。

* **Commerce との統合**：Commerce の Adobe Experience Manager（AEM）Assets 統合では、デジタルアセット管理（DAM）システムとしての AEM の堅牢な機能と Adobe Commerce を組み合わせて、e コマースエクスペリエンスを強化します。これらの機能は、Commerce プロジェクトを AEM の強力なアセット管理環境に接続することで提供され、Commerce ストアフロントをまたいでアセットをシームレスでスケーラブルな、効率的な管理および配信する方法を提供します。
* **AEM Assets と Edge Delivery Services のドキュメントベースのオーサリングフローの統合**：[!DNL AEM Assets] を [!DNL Microsoft Word] や [!DNL Google Docs] などのドキュメントベースのオーサリングツールと統合すると、オーサリングツールにアセットセレクターが提供されます。 このアセットセレクターを使用して [!DNL AEM Assets] にアクセスし、承認済みのアセットをコンテンツに挿入します。
既に [!DNL Edge Delivery Services] web サイトを使用している場合は、[[!DNL AEM Assets]  プラグイン](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)のドキュメントを参照して、[!DNL AEM Assets] を既存の [!DNL AEM] プロジェクトに統合する方法を確認してください。

* **[!DNL Edge Delivery Services]** 用の [!DNL AEM Assets] と [!DNL Universal Editor] ベースのオーサリングフローの統合：[!DNL AEM Assets] と統合するように [!DNL Universal Editor] を設定します。この統合により、[!DNL Dynamic Media with OpenAPI capabilities] を使用してアセットを配信できます。

   * [!DNL Universal Editor] にカスタムアセットピッカー機能を追加する方法について詳しくは、[ [!DNL Edge Delivery]  サイトの設定](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)を参照してください。カスタムアセットピッカーを使用すると、[!DNL Universal Editor] コンテンツにアセットを直接挿入できます。
   * [!DNL Universal Editor] でオーサリング中に [!DNL AEM Assets] にアクセスしてアセットを挿入する方法について詳しくは、[拡張機能の概要](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)を参照してください。

<table>
<td>
   <a href="https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="Adobe Journey Optimizer との統合" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>Adobe Journey Optimizer との統合</strong>
      </a>
   </div>
   <p>
      <em>AJO との統合を使用してマーケティングワークフローとクリエイティブワークフローを統合します</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/overview">
   <img alt="Commerce との統合" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/overview">
      <strong>Commerce との統合</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets を Commerce と統合して、e コマースエクスペリエンスを強化します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="AEM Assets と EDS の統合" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>AEM Assets と EDSの統合</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets をドキュメントベースおよびユニバーサルエディターベースのオーサリングフローと統合します。</em>
   </p>
</td>
</table>

+++

>[!TAB アセットのアクティブ化]

## アセットのアクティブ化 {#asset-activation}

強力な OpenAPI 機能を含む、コンテンツハブから Dynamic Media まで、AEM Assets でデジタルアセットの可能性を最大限に引き出します。AEM Assets では、アセットの変換を効率化し、様々なチャネルをまたいで配信を最適化するように設計された包括的なソリューションスイートを提供します。

+++**コンテンツハブ**

コンテンツハブは、Experience Manager Assets as a Cloud Service の一部として使用でき、組織とそのビジネスパートナーがオンブランドのコンテンツに簡単にアクセスできます。これは、大規模なアクティベーション用のアセットの配布と、マーケティングの俊敏性を向上させるオンブランドのコンテンツバリアントの作成に焦点を当てています。

コンテンツハブには、次のような主なメリットがあります。

* **直感的なポータルで使用可能なすべてのブランド承認済みアセットを検索および共有**：AEM Assets は信頼できる唯一の情報源として機能し、承認済みのすべてのアセットはコンテンツハブでフラットな階層で自動的に使用できるので、検索エクスペリエンスが向上します。

* **設定可能なユーザーインターフェイス**：検索用のフィルター、アセットの追加または読み込み時に使用可能なフィールド、アセットのプロパティ、ブランディング用のバナーコンテンツなど、コンテンツハブ内の最も一般的なプロパティは設定可能で、管理者は要件に基づいてコンテンツハブのユーザーインターフェイスを簡単に設定できます。

* **クリエイティブ以外のユーザーがブランドを維持しながらコンテンツを編集およびリミックスできるようにする**：コンテンツハブを使用すると、Adobe Express を使用して新しいコンテンツを作成できます（Adobe Express の使用権限がある場合）。使いやすいツールを使用して既存のコンテンツを編集し、テンプレートとブランド要素を使用してオンブランドのバリエーションを作成し、Adobe Firefly の最新の生成 AI 機能を使用して新しいコンテンツを作成できます。

* **チームをまたいでコンテンツの使用状況に関するインサイトを取得**：[!DNL Content Hub] は、アセットに関する貴重なインサイトを提供し、マーケティング関係者が頻繁に直面する一般的な課題、つまりマーケティングキャンペーン、チャネル、様々な地域で使用されるアセットの使用状況統計に対処します。アセットのパフォーマンスと人気を明確に把握することで、ユーザーエクスペリエンスの向上に不可欠な実用的なインサイトが得られます。

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="コンテンツハブの概要" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>コンテンツハブの概要</strong>
      </a>
   </div>
   <p>
      <em>コンテンツハブ、その主なメリット、アクセス方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="コンテンツハブユーザーインターフェイスの設定" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>コンテンツハブユーザーインターフェイスの設定</strong>
      </a>
   </div>
   <p>
      <em>コンテンツハブユーザーインターフェイスで使用できるオプションの設定方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Adobe Express を使用した編集" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Adobe Express を使用した編集</strong>
      </a>
   </div>
   <p>
      <em>Adobe Express を使用してコンテンツハブで画像を編集する方法の詳細情報。</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

Dynamic Media は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するのに役立ちます。また、ズーム、360 度スピン、ビデオなどのインタラクティブな視聴エクスペリエンスの作成と提供にも役立ちます。アセットは、web サイト、モバイルサイトおよびソーシャルサイトでの利用に合わせて動的に拡大縮小されます。Dynamic Media では、画像、ビデオ、3D などの一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルな CDN（コンテンツ配信ネットワーク）経由で、リッチコンテンツの複数のバリエーションをリアルタイムで生成および配信します。

Dynamic Media には次の主な機能があります。

* **スマートイメージング**：スマートイメージングは、顧客のブラウザー機能に応じて画像の形式とファイルサイズを自動的に最適化することで、画像アセット配信のパフォーマンスをさらに向上させます。既存の画像プリセットと連携し、配信時にインテリジェンスを使用します。このインテリジェンスにより、ブラウザーとネットワーク接続速度に応じて、画像ファイルのサイズがさらに縮小されます。

* **アダプティブビデオセット**：アダプティブビデオセットは、同じビデオを様々なビットレートおよび形式でエンコードしたバージョンをグループ化したものです。まずオリジナルのプライマリビデオをシステムにアップロードします。Dynamic Media は、そのビデオを複数のビデオに自動的にサイジングつまりトランスコードします。次に、使用するビデオ画面、画質および形式を配信時にインテリジェントに決定し、携帯電話、タブレット、デスクトップコンピュータなどにビデオを配信します。

* **スマート切り抜き**：Adobe Sensei AI 機能を使用して、どのような画像やビデオでも重要な部分を自動的に検出し、切り抜いて維持管理します。画面サイズに関係なく、意図した目標地点をキャプチャして、面倒な手動タスクを排除し、あらゆるデバイスや画面で美しく表示される、高画質で読み込みが速い画像とビデオを配信します。

* **Dynamic Media テンプレート**：WYSIWYG テンプレートエディターである Dynamic Media テンプレートを使用して、リアルタイムでカスタマイズ可能なバナーやチラシ用テンプレートを作成します。Dynamic Media テンプレートを公開し、ダウンストリームアプリケーションで使用します。Dynamic Media テンプレートには、画像レイヤーとテキストレイヤーが含まれます。テンプレートの画像とテキストレイヤーにパラメーターを追加し、Dynamic Media URL を使用してレイヤーの位置とサイズを変更し、コンテンツをリアルタイムで更新します。

* **マルチオーディオとキャプション**：プライマリビデオに対し、複数のキャプションと複数のオーディオトラックを追加します。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからキャプションとオーディオトラックを管理することもできます。

* **HTTP での動的アダプティブストリーミング（DASH）のサポート**：Dynamic Media は、Dynamic Media ビデオ配信（CMAF が有効）でアダプティブストリーミングをサポートし、ビデオのユーザー視聴エクスペリエンスを向上させます。DASH はアダプティブビデオストリーミングの国際標準プロトコルであり、業界で広く採用されています。

* **AI 生成のビデオキャプション**：Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。60 を超える言語がサポートされているので、ビデオを公開する前にキャプションを確認およびプレビューできます。

使用可能な Dynamic Media 製品について詳しくは、[Dynamic Media Prime と Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) を参照してください。



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="Dynamic Media の操作" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>Dynamic Media の操作</strong>
      </a>
   </div>
   <p>
      <em>Dynamic Media を使用して、web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Dynamic Media ジャーニー" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Dynamic Media ジャーニー</strong>
      </a>
   </div>
   <p>
      <em>Dynamic Media を使用して作業に価値を生み出す方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="AEM Assets を Creative Cloud に接続" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Dynamic Media のベストプラクティス</strong>
      </a>
   </div>
   <p>
      <em>画像、ビデオ、ビューアを操作する際のベストプラクティス。</em>
   </p>
</td>
</table>

+++

+++**OpenAPI 機能を備えた Dynamic Media**

今日の急速に変化するデジタルの世界では、ブランドのデジタルアセットの潜在能力を最大限に引き出すことが、競争で優位に立つために不可欠です。総合的なデジタルアセット管理（DAM）ソリューションは、アセットガバナンスを容易にし、ブランドの一貫性を促進し、コンテンツ配信を高速化すると共に、ブランドの整合性と優れたカスタマーエクスペリエンスを確保します。

OpenAPI 機能を備えた Dynamic Media では、DAM をアジャイルで効率的なコンテンツサプライチェーンエコシステムのコアに置き、アセットのガバナンスと配信を確実に行います。

OpenAPI 機能を備えた Dynamic Media には、次のような主なメリットがあります。

* **シームレスな統合**：OpenAPI 機能を備えた Dynamic Media は、包括的な検索および配信 API セットを提供します。これにより、開発者は簡単に[アセットの配信をアプリケーションと統合](/help/assets/integrate-dynamic-media-open-apis.md)できます。アプリケーションには、アドビおよびサードパーティのアプリケーションが含まれます。承認済みアセットを検索および選択する[マイクロフロントエンドのアセットセレクターのユーザーインターフェイス](/help/assets/overview-asset-selector.md)を提供します。セレクターは、React JS、Angular JS、Vanilla JS などの JavaScript フレームワークに基づくすべてのアプリケーションと簡単に統合できます。

* **デジタルアセットの一元管理**：DAM は、すべてのデジタルアセットに対して信頼できる唯一の情報源です。デジタルアセットは AEM Assets で一元管理され、アセットバイナリをコピーすることなく、配信 URL を使用した参照によって消費アプリケーションに配信されます。

* **リアルタイムの更新**：バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに行われた変更は、配信 URL に自動的に反映されます。CDN 経由の OpenAPI 機能を備えた Dynamic Media に 10 分という短い有効期限（TTL）値を設定すると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。

* **ブランドの一貫性**：[ブランド承認済みアセット](/help/assets/approve-assets.md)のみがダウンストリームアプリケーションに公開されます。[ブランドマネージャーとマーケターは、ブランドアセットを厳密に管理します](/help/assets/restrict-assets-delivery.md)。承認済みの最新バージョンのアセットのみが使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

* **Web に最適化された配信**：デジタルアセットは、web に最適化された形式で配信され、デジタルエクスペリエンスのコア web バイタルを強化します。この最適化には、画像の WebP レンディション、ビデオの HLS または DASH プロトコルによるアダプティブストリーミング、ドキュメントの元のレンディションのサポートが含まれます。

* **動的アセット変換**：システムでは、画像修飾子と呼ばれる URL パラメーターを使用して、その場で画像を変換できます。[例えば、幅、高さ、回転、反転、画質、切り抜き、形式、スマート切り抜きなどです](/help/assets/deliver-assets-apis.md)。変換したレンディションは動的に生成され、CDN 経由でシームレスに配信されます。

* **アセットの安全な配信**：OpenAPI 機能を備えた Dynamic Media は、デジタルアセットへのアクセスを制御するメカニズムを提供します。セキュリティ保護対象のアセットのメタデータとしてユーザーの役割またはグループを指定し、[承認済みユーザーのみがこれらのアセットにアクセスできる](/help/assets/restrict-assets-delivery.md)定義済みの期間を設定できます。制限期間中、セキュリティ保護対象のアセットの配信 URL は、承認されていないユーザーに対しては解決されません。

使用可能な Dynamic Media 製品について詳しくは、[Dynamic Media Prime と Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) を参照してください。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="OpenAPI 機能を備えた Dynamic Media の概要" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>OpenAPI 機能を備えた Dynamic Media の概要</strong>
      </a>
   </div>
   <p>
      <em>主なメリットと有効化の方法の詳細情報。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Experience Manager でのアセットへのアクセスの制限" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Experience Manager でのアセットへのアクセスの制限</strong>
      </a>
   </div>
   <p>
      <em>承認済みアセットへのアクセスを制限するために役割を設定します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="リモート AEM Assets と AEM Sites の統合" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>リモート AEM Assets と AEM Sites の統合</strong>
      </a>
   </div>
   <p>
      <em>リモート AEM Assets と AEM Sites 環境を統合します。</em>
   </p>
</td>
</table>

+++

>[!TAB インサイト]

## アセットインサイト {#asset-insights}

アセットレポートを使用すると、管理者は Adobe Experience Manager Assets ビュー環境のアクティビティを視覚的に確認できます。このデータは、ユーザーがコンテンツや製品とどのようにやり取りするかについての有用な情報を提供します。すべてのユーザーが Insights ダッシュボードにアクセスでき、管理者の製品プロファイルに割り当てられたユーザーはユーザー定義レポートを作成できます。

アップロード、ダウンロード、Dynamic Media 配信など、様々なタイプのレポートを生成できます。

* **アセットビューのインサイト**：アセットビューを使用すると、アセットビュー環境のリアルタイムデータをインサイトダッシュボードで表示できます。過去 30 日間または過去 12 か月間のリアルタイムイベント指標を表示できます。イベントには、ダウンロード、アップロード、ストレージ使用状況、上位の検索、サイズ別のアセット数、アセットタイプ別のアセット数が含まれます。

* **管理ビューでの Adobe Analytics の統合**：アセットインサイトの機能を使用すると、サードパーティの web サイト、マーケティングキャンペーン、アドビのクリエイティブソリューションで使用される画像のユーザー評価と使用状況統計を追跡できます。これにより、画像のパフォーマンスと人気に関するインサイトが提供されます。アセットインサイトでは、画像の評価回数、クリック数、インプレッション数（画像が Web サイトに読み込まれた回数）など、ユーザーのアクティビティの詳細を取得します。これらの統計情報に基づいて画像にスコアを割り当てます。スコアとパフォーマンス統計を使用して、人気が高い画像を選び、カタログやマーケティングキャンペーンなどに含めることができます。このような統計に基づいて、アーカイブやライセンス更新のポリシーを策定することもできます。アセットインサイトでアセットの使用状況統計を表示するには、最初に Adobe Analytics からのレポートデータを取得するように機能を設定します。

* **コンテンツハブのインサイト**：コンテンツハブは、アセットに関する貴重なインサイトを提供し、マーケティング関係者が頻繁に直面する一般的な課題、つまりマーケティングキャンペーン、チャネル、様々な地域で使用されるアセットの使用状況統計に対処します。アセットのパフォーマンスと人気を明確に把握することで、ユーザーエクスペリエンスの向上に不可欠な実用的なインサイトが得られます。

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="アセットビューでのレポートの管理" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>アセットビューでのレポートの管理</strong>
      </a>
   </div>
   <p>
      <em>アセットビューを使用して、主な成功指標に関するインサイトを導き出します。</em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="管理ビューでのレポートの管理" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>管理ビューでのレポートの管理</strong>
      </a>
   </div>
   <p>
      <em>管理ビューで Adobe Analytics 統合レポートを管理する方法の詳細情報。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="コンテンツハブのアセットインサイト" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>コンテンツハブのアセットインサイト</strong>
      </a>
   </div>
   <p>
      <em>コンテンツハブでアセットインサイトを表示する方法の詳細情報。</em>
   </p>
</td>
</table>

>[!ENDTABS]

## デジタルアセット管理で使用可能なペルソナベースのエクスペリエンス {#persona-based-experiences}

アドビでは、デジタルアセットを最大限に活用する堅牢なデジタルアセット管理（DAM）ソリューションを提供しています。Adobe Experience Manager Assets には、同じ Cloud Services リポジトリを使用する 2 つの異なるエクスペリエンスがあります。

* **管理ビュー**：既存の Assets as a Cloud Service ユーザーインターフェイス。管理ビューは、統合、ワークフロー、コンテンツの自動化、公開など、すべての高度なデジタルアセット管理機能に使用できます。

* **アセットビュー**：アドビの軽量なアセット管理エクスペリエンスで、デジタルアセットの保存、管理、検出および使用が実現します。合理化されたユーザーインターフェイスには、重要なデジタルアセット管理機能が含まれます。アップロード、メタデータの管理、検索、ダウンロードおよび共有に重点を置いた軽量な DAM ユーザー向けに設計されています。

![add-tags](assets/newui-overview.svg)

管理ビューへのアクセス権を持つユーザーは、アセットビューにもアクセスできます。アセットビューにはシンプルなユーザーインターフェイスが用意されており、デジタルアセットの管理、検出、配布が容易になります。クリエイティブ、マーケティング、事業部門のチームなど、異なる部門をまたいだ幅広いユーザーが、アセットで共同作業を行い、必要に応じて適切な承認済みアセットにアクセスできます。多くの一般的な DAM ユーザーは、機能のサブセットのみを含むアセットビューを好みます。このエクスペリエンスの対象は、クリエイティブ、読み取り専用アセットの消費者、より軽量な DAM ユーザーです。

DAM ライブラリ担当者、開発者およびスーパーユーザーは、必要に応じて、引き続き管理ビューを使用したり、ユーザーインターフェイスを切り替えたりできます。自分の役割に最適なエクスペリエンスを選択できます。

アセットビューへのアクセス方法および管理ビューで提供される簡略化について詳しくは、[アセットビューの概要](/help/assets/assets-view-introduction.md)を参照してください。

## AEM の AI アシスタント

[前提条件の条件を満たした](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)お客様の組織では、AEM の AI アシスタントをユーザーが使用できます。[AEM の AI アシスタント](/help/implementing/cloud-manager/ai-assistant-in-aem.md)を参照してください。
