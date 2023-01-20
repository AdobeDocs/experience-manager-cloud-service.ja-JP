---
title: GraphQL API を使用したコンテンツの抽出
description: コンテンツフラグメントとGraphQL API をヘッドレスコンテンツ管理システムとして使用する方法について説明します。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: 741fadcffc496cb1c32d1943f7759e8d70cf92ff
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

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
>additional-url="https://video.tv.adobe.com/v/328618/?captions=jpn" text="コンテンツの抽出の導入ビデオ"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="お疲れさまでした。 ここでは、2 つの基本的なタイプのクエリと、独自のコンテンツに対するクエリ方法について説明します。 AEM GraphQL API を使用して、アプリが想定する形式でコンテンツを配信する効率的なクエリを作成する方法を理解しました。"
>abstract=""

## サンプルコンテンツのリストのクエリ {#list-query}

新しいタブで、GraphQL Explorer を起動します。 ここでは、ヘッドレスコンテンツを使用してアプリまたは Web サイトのコンテンツを強化する前に、ヘッドレスコンテンツに対するクエリを作成および検証できます。

1. AEMヘッドレス体験版には、テスト用にコンテンツを抽出できるコンテンツフラグメントがプリロードされたエンドポイントが付属しています。 必ず **AEMデモアセット** エンドポイントが **エンドポイント** エディターの右上隅にあるドロップダウンメニュー。

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

1. 貼り付けたら、 **再生** ボタンをクリックしてクエリを実行します。

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。 クエリが正しくない場合は、右側のパネルにエラーが表示されます。

   ![リストクエリ](assets/do-not-localize/list-query-1-3-4-5.png)

すべてのコンテンツフラグメントの完全なリストのリストクエリを検証しました。 このプロセスは、応答がアプリが期待するものであることを確認するのに役立ちます。その結果、アプリや Web サイトがAEMで作成されたコンテンツを取得する方法が示されます。

## サンプルコンテンツの特定の部分のクエリ {#bypath-query}

byPath クエリを実行すると、特定のコンテンツフラグメントのコンテンツを取得できます。 特定のコンテンツのセットに焦点を当てる製品の詳細ページやページには、通常、このタイプのクエリが必要です。

1. プリロードされたの byPath クエリに対して、次のコードスニペットをコピーします。 **AEMデモアセット** endpoint.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
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

1. 貼り付けたら、 **再生** ボタンをクリックしてクエリを実行します。

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。 クエリが正しくない場合は、右側のパネルにエラーが表示されます。

   ![byPath クエリの結果](assets/do-not-localize/bypath-query-2-3-4.png)

byPath クエリを検証し、そのフラグメントのパスで識別される特定のコンテンツフラグメントを取得しました。

## 独自のコンテンツのクエリ {#own-queries}

これで、2 つの主なタイプのクエリを実行したので、独自のコンテンツに対してクエリを実行する準備が整いました。

1. 独自のコンテンツフラグメントに対してクエリを実行するには、エンドポイントを **AEMデモアセット** フォルダーを **プロジェクト** フォルダー。

1. クエリエディターで既存のコンテンツをすべて削除します。 次に、開き角括弧を入力します `{` をクリックし、 Ctrl+Space キーまたは Option+Space キーを押して、エンドポイントで定義されたモデルのオートコンプリートリストを表示します。 作成したで終わるモデルを選択します。 `List` を選択します。

   ![カスタムクエリを開始](assets/do-not-localize/custom-query-1-2.png)

1. 選択したコンテンツフラグメントモデルに対してクエリに含める必要がある項目を定義します。 繰り返しに、開き角括弧を入力します。 `{`をクリックし、Ctrl +スペースキーまたは Option +スペースキーを押してオートコンプリートリストを表示します。 選択 `items` を選択します。

1. をタップまたはクリックします。 **事前設定** ボタンを使用して、読みやすくするためのコードの書式を自動的に設定します。

1. 完了したら、 **再生** ボタンをクリックして、クエリを実行します。 エディターは、 `items` クエリが実行されます。

1. 結果は、右側のパネルの、クエリエディターの横に表示されます。

   ![カスタムクエリの実行](assets/do-not-localize/custom-query-3-4-5-6.png)

コンテンツをオムニチャネルのデジタルエクスペリエンスに配信する方法は次のとおりです。
