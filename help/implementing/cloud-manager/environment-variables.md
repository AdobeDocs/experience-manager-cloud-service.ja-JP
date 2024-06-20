---
title: Cloud Manager 環境変数
description: 標準環境変数は、Cloud Manager を介して設定および管理でき、ランタイム環境に提供され、OSGi 設定で使用できます。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ed166aa753d4fb5c6fb1573032186e3e14f375df
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 98%

---


# Cloud Manager 環境変数 {#environment-variables}

標準環境変数は、Cloud Manager を介して設定および管理できます。これらは実行時環境に提供され、OSGi 設定で使用できます。環境変数には、環境固有の値または環境シークレットを変更内容に応じて指定できます。

## 概要 {#overview}

環境変数は、AEM as a Cloud Service のユーザーに次のような多くの利点を提供します。

* コードやアプリケーションの動作を、コンテキストや環境に応じて変化させることができます。例えば、実稼動環境やステージング環境と比較して開発環境で異なる設定を有効にして、コストのかかるミスを避けることができます。
* 設定とセットアップは 1 回だけで済み、必要に応じて更新や削除が可能です。
* 値は任意の時点で更新でき、コードの変更やデプロイメントを行う必要なく、即座に有効になります。
* 設定からコードを分離でき、バージョン管理に機密情報を含める必要がありません。
* コードの外部に存在するので、AEM as a Cloud Service アプリケーションのセキュリティが向上します。

環境変数を使用した一般的なユースケースを次に示します。

* 別の外部エンドポイントを使用した AEM アプリケーションの接続
* パスワードをコードベースに直接格納する代わりに、参照を使用する場合
* 1 つのプログラムに開発環境が複数あり、環境によって一部の設定が異なる場合

## 環境変数の追加 {#add-variables}

>[!NOTE]
>
>環境変数を追加または変更するには、[**デプロイメントマネージャー**&#x200B;の役割を持つ](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)メンバーである必要があります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Adobe Cloud Manager にログインします。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、管理する項目を選択します。
1. サイドナビゲーションバーから、選択したプログラムの&#x200B;**環境**&#x200B;ウィンドウを選択し、環境変数を作成する環境を選択します。
1. 環境の詳細で「**設定**」タブを選択し、「**追加**」を選択して **環境設定** ダイアログを開きます。
   * 初めて環境変数を追加する場合、ページの中央に「**設定を追加**」ボタンが表示されます。このボタンまたは「**追加**」を使用して、**環境設定**&#x200B;ダイアログを開くことができます。

   ![「設定」タブ](assets/configuration-tab.png)

1. 変数の詳細を入力します。
   * **名前**
   * **値**
   * **適用されるサービス**  – 変数をどのサービス（オーサー/Publish/プレビュー）に適用するか、またはすべてのサービスに適用するかを定義します
   * **種類** - 変数が通常の変数かシークレットかを定義します

   ![変数の追加](assets/add-variable.png)

1. 新しい変数を入力した後、新しい変数を含む行の最後の列で「**追加**」を選択する必要があります。
   * 新しい行を入力して「**追加**」を選択すると、一度に複数の変数を入力できます。

   ![変数の保存](assets/save-variables.png)

1. 「**保存**」を選択して、変数を保持します。

表の上部と新しく追加された変数の横に、ステータスが **更新中** のインジケーターが表示され、環境が設定で更新されていることを示します。完了すると、新しい環境変数が表に表示されます。

![変数の更新](assets/updating-variables.png)

>[!TIP]
>
>複数の変数を追加する場合は、最初の変数を追加してから、**環境設定**&#x200B;ダイアログの「**追加**」ボタンを使用してその他の変数を追加することをお勧めします。これにより、1 回の更新で環境に追加できます。

## 環境変数の更新 {#update-variables}

環境変数を作成したら、「**追加／更新**」ボタンを使用して環境変数を更新すると、**環境設定**&#x200B;ダイアログを起動できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Adobe Cloud Manager にログインします。
1. Cloud Manager に、使用可能な様々なプログラムのリストが表示されます。管理するものを選択します。
1. ナビゲーションパネルで、選択したプログラムの&#x200B;**環境**&#x200B;ウィンドウを選択し、環境変数を変更する環境を選択します。
1. 環境の詳細で「**設定**」タブを選択し、右上の「**追加／更新**」を選択して **環境設定** ダイアログを開きます。
1. 変更する変数の行の最後の列にある省略記号ボタンを使用して、「**編集**」または「**削除**」を選択します。

   ![変数を編集または削除](assets/edit-delete-variable.png)

1. 必要に応じて環境変数を編集します。
   * 編集時には、省略記号ボタンが、元の値に戻すか、変更を確定するかの選択ボタンに変わります。
   * シークレットを編集する場合、値は更新のみ可能で、表示はできません。

   ![変数の編集](assets/edit-variable.png)

1. 必要な設定の変更を行ったら、「**保存**」を選択します。

[変数を追加する場合と同様に、](#add-variables) ステータスが **更新中** のインジケーターがテーブルの上部と新しく更新された変数の横に表示され、環境が設定で更新されていることを示します。完了すると、更新された環境変数がテーブルに表示されます。

>[!TIP]
>
>複数の変数を更新する場合は、**環境設定**&#x200B;ダイアログを使用して、必要なすべての変数を一度に更新してから、「**保存**」をタップまたはクリックすることをお勧めします。これにより、1 回の更新で環境に追加できます。

## 環境変数の使用 {#using}

環境変数を使用すると、`pom.xml` 設定の安全性と柔軟性を高めることができます。例えば、パスワードをハードコードする必要はなく、環境変数の値に基づいて設定を適応させることができます。

次のように、XML を使用して環境変数とシークレットにアクセスできます。

* `${env.VARIABLE_NAME}`

`pom.xml` ファイルで両方のタイプの変数を使用する方法の例については、[プロジェクトの設定](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)を参照してください。

詳しくは、[Maven の公式ドキュメント](https://maven.apache.org/settings.html#quick-overview)を参照してください。

## 環境変数の可用性 {#availability}

環境変数は複数の場所で使用できます。

### オーサー、プレビュー、パブリッシュ {#author-preview-publish}

オーサー、プレビュー、パブリッシュの各環境では、通常の環境変数とシークレットの両方を使用できます。

### Dispatcher {#dispatcher}

通常の環境変数のみが、[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) シークレットは使用できません。

ただし、環境変数は `IfDefine` ディレクティブでは使用できません。

>[!TIP]
>
>デプロイする前に、[Dispatcher をローカルで](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=ja)使用して、環境変数の使用を検証する必要があります。

### OSGi 設定 {#osgi}

[OSGi 設定](/help/implementing/deploying/configuring-osgi.md)では、通常の環境変数とシークレットの両方を使用できます。

### パイプライン変数 {#pipeline}

環境変数に加えて、ビルドフェーズで公開されるパイプライン変数もあります。[パイプライン変数について詳しくは、こちらを参照してください](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)。
