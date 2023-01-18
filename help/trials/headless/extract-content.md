---
title: GraphQL API を使用したコンテンツの抽出
description: コンテンツフラグメントと GraphQL API をヘッドレスコンテンツ管理システムとして使用する方法を説明します。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---


# GraphQL API を使用したコンテンツの抽出 {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="GraphQL API を使用したコンテンツの抽出"
>abstract="このモジュールでは、コンテンツフラグメントとGraphQL API をヘッドレスコンテンツ管理システムとして使用する方法を学びます。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="GraphQL Explorer を起動します。"
>abstract="GraphQLはクエリベースの API を提供し、1 回の API 呼び出しを使用して、外部のクライアントアプリケーションが必要なコンテンツに対してのみAEMをクエリできるようにします。 このモジュールでは、2 つの異なるタイプのクエリを実行する方法について説明します。 次に、前のモジュールで作成したコンテンツフラグメントからコンテンツを取得する方法を説明します。<br><br>以下をクリックして、新しいタブでこのモジュールを起動します。"
>additional-url="https://video.tv.adobe.com/v/328618" text="コンテンツの抽出の導入ビデオ"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="お疲れさまでした。 ここでは、2 つの基本的なタイプのクエリと、独自のコンテンツに対するクエリ方法について説明します。 AEM GraphQL API を使用して、アプリが想定する形式でコンテンツを配信する効率的なクエリを作成する方法を理解しました。"
>abstract=""

## サンプルコンテンツのリストのクエリ {#list-query}

クリック **GraphQL Explorer を起動します。** 上のボタンをクリックすると、GraphQL Explorer が新しいタブで開きます。

![GraphQL Query Editor](assets/extract-content/query-editor.png)

GraphQL Explorer を使用すると、ヘッドレスコンテンツを使用してアプリまたは Web サイトのコンテンツを強化する前に、ヘッドレスコンテンツに対するクエリを作成および検証できます。 それがどのように行われたかを見てみましょう。

1. AEMヘッドレス体験版には、テスト用にコンテンツを抽出できるコンテンツフラグメントがプリロードされたエンドポイントが付属しています。 を選択します。 **AEMデモアセット** エンドポイント **エンドポイント** エディターの右上隅にあるドロップダウンメニュー。

   ![エンドポイントを選択](assets/extract-content/select-endpoint.png)

1. 次のコードスニペットをコピーして、プリロードされたのリストクエリを実行します。 **AEMデモアセット** endpoint. リストクエリは、特定のコンテンツフラグメントモデルを使用するすべてのコンテンツのリストを返します。 在庫ページとカテゴリページでは、通常、このクエリ形式を使用します。

   ```text
   {
       adventureList {
         items {
            _path
            adventureTitle
            adventurePrice
            adventureTripLength
            adventurePrimaryImage {
              ... on ImageRef {
               _path
               mimeType
               width
               height
             }
           }
         }
      }
    }
   ```

1. クエリエディターで既存のコンテンツを置き換えるには、コピーしたコードを貼り付けます。

   ![リストクエリ](assets/extract-content/list-query.png)

1. 貼り付けたら、 **再生** ボタンをクリックしてクエリを実行します。

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。 クエリが正しくない場合は、右側のパネルにエラーが表示されます。

   ![クエリ結果のリスト](assets/extract-content/list-query-results.png)

すべてのコンテンツフラグメントの完全なリストのリストクエリを検証しました。 このプロセスは、応答がアプリが期待するものであることを確認するのに役立ちます。その結果、アプリや Web サイトがAEMで作成されたコンテンツを取得する方法が示されます。

## サンプルコンテンツの特定の部分のクエリ {#bypath-query}

byPath クエリを実行すると、特定のコンテンツフラグメントのコンテンツを取得できます。 特定のコンテンツのセットに焦点を当てる製品の詳細ページやページには、通常、このタイプのクエリが必要です。 仕組みを見てみましょう。

1. プリロードされたの byPath クエリに対して、次のコードスニペットをコピーします。 **AEMデモアセット** endpoint.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         adventureTitle
         adventureDescription {
           json
         }
         adventurePrimaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. クエリエディターで既存のコンテンツを置き換えるには、コピーしたコードを貼り付けます。

   ![byPath クエリ](assets/extract-content/bypath-query.png)

1. 貼り付けたら、 **再生** ボタンをクリックしてクエリを実行します。

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。 クエリが正しくない場合は、右側のパネルにエラーが表示されます。

   ![byPath クエリの結果](assets/extract-content/bypath-query-results.png)

byPath クエリを検証し、そのフラグメントのパスで識別される特定のコンテンツフラグメントを取得しました。

## 独自のコンテンツのクエリ {#own-queries}

これで、2 つの主なタイプのクエリを実行したので、独自のコンテンツに対してクエリを実行する準備が整いました。

1. 独自のコンテンツフラグメントに対してクエリを実行するには、エンドポイントを **AEMデモアセット** フォルダーを **プロジェクト** フォルダー。

   ![独自のエンドポイントを選択](assets/extract-content/select-endpoint.png)

1. クエリエディターで既存のコンテンツをすべて削除します。 次に、開き角括弧を入力します `{` をクリックし、 Ctrl+Space キーまたは Option+Space キーを押して、エンドポイントで定義されたモデルのオートコンプリートリストを表示します。 作成したで終わるモデルを選択します。 `List` を選択します。

   ![クエリエディターでのモデルの自動完了](assets/extract-content/auto-complete-models.png)

1. 選択したコンテンツフラグメントモデルに対してクエリに含める必要がある項目を定義します。 繰り返しに、開き角括弧を入力します。 `{`をクリックし、Ctrl +スペースキーまたは Option +スペースキーを押してオートコンプリートリストを表示します。 選択 `items` を選択します。

   ![クエリエディターでの項目のオートコンプリート](assets/extract-content/auto-complete-items.png)

1. 選択したコンテンツフラグメントモデルに対してクエリに含める必要があるフィールドを定義します。 もう一度、開き角括弧を入力します。 `{`をクリックし、 Ctrl + Space キーまたは Option + Space キーを押して、コンテンツフラグメントモデル内の使用可能フィールドのオートコンプリートリストを表示します。 リストから、モデルから必要なフィールドを選択します。

   ![クエリエディターのフィールドを自動入力](assets/extract-content/auto-complete-fields.png)

1. 複数のフィールドをコンマ (`,`) または Space キーを押しながら Ctrl + Space キーまたは Option + Space キーを押して、追加のフィールドを選択します。

1. 作業中に、 **事前設定** ボタンを使用して、読みやすくするためのコードの書式を自動的に設定します。

   ![事前設定](assets/extract-content/prettify.png)

1. 完了したら、 **再生** ボタンをクリックして、クエリを実行します。

   ![独自のクエリの結果](assets/extract-content/custom-query-results.png)

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。

コンテンツをオムニチャネルのデジタルエクスペリエンスに配信する方法は次のとおりです。
