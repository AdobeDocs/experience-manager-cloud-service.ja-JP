---
title: ユニバーサルエディター 2026.03.19 リリースノート
description: ユニバーサルエディターの 2026.03.19 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 34%

---


# ユニバーサルエディター 2026.03.19 リリースノート {#release-notes}

ユニバーサルエディターの 2026 年 3 月 19 日リリースのリリースノートです。

>[!TIP]
>
>ユニバーサルエディターの&#x200B;**今後の**&#x200B;機能をリリース前にテストしたい場合は、[ユニバーサルエディターのプレビューリリースノート](/help/release-notes/universal-editor/preview.md)を参照してください。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* [ ホーム画面 ](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button) に戻ったときにプロパティの項目が折りたたまれるようになりました。
* [ アセットセレクター ](/help/implementing/universal-editor/configure-assets-selector.md) で [ フィルター定義がサポートされるようになりました ](/help/implementing/universal-editor/filtering.md)。
* 選択した項目に使用可能なアクションがない場合、[ コンテキストメニュー ](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu) には、アクションにアクセスするための山形が表示されなくなります。

## その他の改善点 {#other-improvements}

* モデル/フィルター/コンポーネント定義がある場合、エディターでアプリを別のアプリに切り替えると、再取得されます。
* DA をバックエンドとして使用する場合、画像を削除しても空の画像タグが残なくなりました。
* DA をバックエンドとして使用する場合、ブロック内のクラスが適切に処理されるようになりました。
* Open API でリモートアセットをオブジェクトとして適切に保存できるようになりました。

## 重大な変更 {#breaking-change}

* 安定性を向上させるには、すべての拡張機能を `@adobe/uix-guest` >= `1.1.7` に更新する必要があります。
