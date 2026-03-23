---
title: ユニバーサルエディター 2026.03.19 リリースノート
description: ユニバーサルエディターの 2026.03.19 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 048e86fe7930173bb33de9252607e2910520b575
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 34%

---


# ユニバーサルエディター 2026.03.19 リリースノート {#release-notes}

これらは、ユニバーサルエディターの2026年3月19日リリースのリリースノートです。

>[!TIP]
>
>ユニバーサルエディターの&#x200B;**今後の**&#x200B;機能をリリース前にテストしたい場合は、[ユニバーサルエディターのプレビューリリースノート](/help/release-notes/universal-editor/preview.md)を参照してください。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* ホーム画面[に戻ると、プロパティ内の項目が折りたたまれるようになりました。](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [ アセットセレクター](/help/implementing/universal-editor/configure-assets-selector.md)は、[ フィルター定義をサポートするようになりました。](/help/implementing/universal-editor/filtering.md)
* 選択した項目に対して使用可能なアクションがない場合、[ コンテキストメニュー](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu)には、そのアクションを示すメッセージが表示されるようになりました。

## その他の改善点 {#other-improvements}

* モデル/フィルター/コンポーネントの定義がある場合、エディターでアプリからアプリに切り替えると、その定義がリフェッチされます。
* DAをバックエンドとして使用する際に、画像を削除しても空の画像タグが残らなくなりました。
* DAをバックエンドとして使用する場合、ブロック内のクラスが適切に処理されるようになりました。
* Open APIが、リモートアセットをオブジェクトとして適切に保存するようになりました。

## 改ページ {#breaking-change}

* 安定性を向上させるために、すべての拡張機能を`@adobe/uix-guest` >= `1.1.7`に更新してください。
