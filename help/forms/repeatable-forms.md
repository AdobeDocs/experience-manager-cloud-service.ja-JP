---
description: このチュートリアルでは、フォームのセクションを繰り返し可能にする手順を説明します
title: 繰り返し可能なセクション (Edge Delivery Services)
feature: Edge Delivery Services
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# エッジ配信の繰り返し可能なセクション

繰り返し可能なセクションとは、同じデータに関する複数のオカレンスの情報を収集するために、複製または複製されたフォームのコンポーネントです。

例えば、ローン申し込みを行うユーザーから情報を収集するために使用するフォームについて考えてみましょう。 フォームを使用すると、ユーザーは共同閲覧者の詳細を含む個人情報を提供できます。 ユーザーは共同申込者の詳細を入力できます。このセクションは繰り返し可能です。

![フォーム内の繰り返し可能なセクション](/help/forms/assets/eds-repeatable.png)

## 前提条件

AEMボイラープレートを使用して Edge Delivery Service(EDS)GitHub プロジェクトを設定し、対応する GitHub リポジトリのクローンをローカルマシンに作成します。 詳しくは、 [開発者向けチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) 」を参照してください。

## エッジ配信の繰り返し可能なセクション

次に、ローン申し込みフォームの例を見てみましょう。 このフォームを使用して、ユーザーは個人情報を送信できます。 繰り返し可能なセクションを使用して、共同申込者の詳細を含めることができます。オプションで、同意申込者のセクションを最小 3 つまで追加できます。

>[!NOTE]
>
> * SharePoint Site またはGoogle Drive 上でMicrosoft Excel を作成して、フィールドセットをフォーム内で繰り返し可能にすることができます。
> * ここでは、マイクロソフトSharePointの例を示します。 SharePointフォルダーをコンテンツソースとして設定するには、 [SharePoint の使用方法](https://www.aem.live/docs/setup-customer-sharepoint).


Edge 配信に繰り返し可能なセクションを追加するには：

1. [Microsoft Excel を使用したフォームの作成](#author-form)
2. [フォームのプレビューと発行](#preview-form)

### Microsoft Excel を使用したフォームの作成 {#author-form}

1. Microsoft SharePointアカウントに移動し、 AEM Edge Delivery プロジェクトディレクトリを開くか作成します。
2. 既存のMicrosoft Excel ファイルを開くか、新規作成します。
この例では、という名前の Excel シートを使用します。 `loan-application.xlsx` Microsoft SharePoint Site で作成済み。
3. 次のラベルの付いた新しい列を追加 `Repeatable`, `Min`、および `Max` をMicrosoft Excel ファイルに追加します。
4. の値を指定します。 `Repeatable` 列の形式 `True` を繰り返し可能にするフィールドセット用に使用します。
5. 次の項目の値を指定します。 `Min` および `Max` 列。 The `Min` 値は、パネルが繰り返される最小回数を表し、 `Max` 値は、パネルが繰り返される回数の最大値を表します。
6. Microsoft Excel ファイルを保存します。

>[!NOTE]
>
> こちらが [ローン申し込み](/help/forms/assets/loan-application.xlsx) 参照用の excel シート。

### Edge 配信サービスを使用したフォームのプレビュー/パブリッシュ

1. Microsoft SharePoint Site で新しいドキュメントファイルを開くか作成し、 `Form Block`. 例えば、 `index` ファイルを作成し、 `Form Block`.
2. コマンドプロンプトを開き、ローカルマシン上のAEM Edge Delivery プロジェクトディレクトリに移動し、次のようにコマンドを実行します。 `aem up`.

フォームは次の場所でアクセスできます。 `https://localhost:3000`をクリックし、 `Add` 「 」ボタンをクリックすると、同意申込者の詳細を入力するための繰り返し可能なセクションが新しく追加されます。 繰り返し可能なセクションを削除するには、 `Delete` 」ボタンをクリックします。

>[!NOTE]
>
> localhost でのフォームへのアクセス中に「ページが見つかりません」エラーが発生した場合は、フォームの場所の URL の前に、Microsoft SharePointサイトのディレクトリ名を追加します。 例：`http://localhost:3000/<dir-name>/`




