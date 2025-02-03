---
title: アダプティブフォームのメタデータプロパティを再利用する方法を教えてください。
description: 既存のアダプティブフォームを効率的に再利用して新しいアダプティブフォームを作成する方法を説明します。
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
feature: Adaptive Forms, Foundation Components
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: ht
source-wordcount: '601'
ht-degree: 100%

---

# アダプティブフォームのメタデータプロパティの再利用 {#reusing-adaptive-forms}

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#) |
| AEM as a Cloud Service | この記事 |

既存のアダプティブフォームの一部のプロパティを使用して新しいアダプティブフォームを生成する場合は、単純にコピーと貼り付けの機能を使用できます。さらに、新しいアダプティブフォームを希望のフォルダーパスに貼り付けることもできます。すべてのメタデータプロパティが複製され、XFA ベースのアダプティブフォームの XFA と XSD ベースのアダプティブフォームの XSD もコピーされます。

>[!NOTE]
>
>ステータスとレビューの詳細はコピーされません。例えば、アダプティブフォームが公開され、その後にそのアダプティブフォームをコピーした場合、貼り付けられるアダプティブフォームは未公開の状態になります。同様に、コピーされたアセットがレビュー中の場合、貼り付けられたアセットは同じレビュー中とはなりません。

## アダプティブフォームのコピー {#copy-an-adaptive-form}

次のいずれかの方法を使用して、アダプティブフォームをコピーします。

1. クイックアクションからコピー ![aem6forms_copy](assets/aem6forms_copy.png) アイコンをクリックします。

   >[!NOTE]
   >
   >クイックアクションは、マウスのカーソルを合わせたときにサムネール上に表示されるアクション項目です。

1. アダプティブフォームを選択します。選択方法はビューによって異なります。

   カードビューの場合は、選択 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) アイコンをクリックして選択モードに移行し、コピーするすべてのアダプティブフォームをクリックします。

   リスト表示の場合は、選択するすべてのアダプティブフォームのチェックボックスをオンにします。

   >[!NOTE]
   >
   >コピーと貼り付けの機能はアダプティブフォームのみをサポートしていますので、選択したアセットはすべてアダプティブフォームである必要があります。また、選択したすべてのアセットは同じフォルダー内のものである必要があります。

   アセットを選択したら、ツールバーにあるコピー ![aem6forms_copy](assets/aem6forms_copy.png) アイコンをクリックして、選択したアダプティブフォームをコピーします。

## アダプティブフォームの貼り付け {#paste-an-adaptive-form}

コピーアクションをクリックすると、選択モードが自動的に終了し、貼り付け![貼り付け](assets/Smock_Paste_18_N.svg)アイコンが表示されます。必要なフォルダーパスに移動して貼り付け![貼り付け](assets/Smock_Paste_18_N.svg)アイコンをクリックし、コピーしたアダプティブフォームを貼り付けます。

同じフォルダー内に貼り付ける場合、または貼り付け先のフォルダー内に同じノード名（CRX リポジトリへの保存に使用される名前）の別のファイルがある場合は、接尾辞に 1 が追加されます（例えば、myaf は myaf1 となり、同じ場所に myaf1 がある場合は myaf が myaf2 になります）。その他のプロパティはすべて元のアダプティブフォームと同じになります。

貼り付け![貼り付け](assets/Smock_Paste_18_N.svg)アイコンをクリックすると、アイコンは再び非表示になります。一度に行える貼り付け操作は一回だけです。同じアセットのコピーを再び作成するには、再度アセットをコピーします。

## 新しいアダプティブフォームのコンテンツの変更 {#change-contents-of-new-adaptive-form}

貼り付けたアダプティブフォームのコンテンツは、次の方法を用いて変更し、コピー元のフォームとは別のフォームにすることができます。

1. **メタデータプロパティの変更：**

   タイトルや説明など、アダプティブフォームのメタデータプロパティを変更できます。メタデータプロパティとその変更方法について詳しくは、 [フォームメタデータの管理](manage-form-metadata.md) を参照してください。

1. **XFA/XSD ベースのアダプティブフォームの XFA/XSD の変更：**

   アダプティブフォームで使用する XFA/XSD を変更できます。これらのアダプティブフォームの変更方法について詳しくは、[フォームメタデータの管理](manage-form-metadata.md)を参照してください。

1. **再公開：**

   ペーストしたアセットはコピー元のアセットとは別のものになります。エンドユーザーが使用できるように、新しいアセットとして公開することができます。アセットの公開方法を理解するには、<!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->


## 関連トピック {#see-also}

{{see-also}}