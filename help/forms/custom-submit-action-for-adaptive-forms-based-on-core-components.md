---
title: コアコンポーネントに基づいてアダプティブフォームのカスタム送信アクションを作成する方法
description: カスタマイズされた送信アクションを使用してデータを送信する前に、アダプティブ Formsのカスタム送信アクションを作成してデータを処理する方法について説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 26%

---

# アダプティブ Forms（コアコンポーネント）用のカスタム送信アクションの作成

送信アクションを使用すると、ユーザーはフォームから取得したデータの宛先を選択し、フォーム送信時に実行する追加機能を定義できます。 AEM フォームでは、電子メールの送信やデータのSharePointやOneDriveへの保存など、複数の[送信アクションをすぐに実行できる（OOTB） &#x200B;](/help/forms/configure-submit-actions-core-components.md)がサポートされています。

カスタム送信アクションを作成して、[標準提供オプション &#x200B;](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action)に含まれていない機能を追加することもできます。 たとえば、フォームデータをサードパーティのアプリケーションと統合したり、顧客の入力にもとづいてパーソナライズされたSMS通知をトリガーしたりできます。

<!--
 ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## 前提条件

アダプティブ Formsの最初のカスタム送信アクションの作成を開始する前に、次の点を確認してください。

* **プレーンテキストエディター（IDE）**：どのプレーンテキストエディターでも機能しますが、Microsoft Visual Studio Code などの統合開発環境（IDE）では、編集を簡単にする高度な機能が提供されます。

* **Git**: コード変更の管理には、このバージョン管理システムが必要です。 インストール済みでない場合は、https://git-scm.com からダウンロードしてください。

## フォームの最初のカスタム送信アクションの作成

次の図は、アダプティブフォームのカスタム送信アクションを作成する手順を示しています。

![&#x200B; カスタム送信アクションのワークフロー](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### AEM as a Cloud Service Git リポジトリを複製します。

1. コマンドラインを開き、AEM as a Cloud Service リポジトリを保存するディレクトリ（例：`/cloud-service-repository/`）を選択します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **この情報はどこにありますか？**

   これらの詳細を見つける手順について詳しくは、Adobe Experience League の記事「[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」を参照してください。

   **プロジェクトの準備が整いました。**

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。このフォルダーは、アプリケーション（app-idなど）にちなんで名前が付けられます。 このフォルダーには、AEM as a Cloud Service Git リポジトリーからダウンロードされたすべてのファイルとコードが含まれます。 AEM プロジェクトの `<appid>` は `archetype.properties` ファイルにあります。

   ![アーキタイププロパティ](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   このガイドでは、このフォルダーを `[AEMaaCS project directory]` と呼びます。

## 新しい送信アクションを追加

1. エディターでリポジトリフォルダーを開きます。

   ![&#x200B; クローン済みリポジトリ &#x200B;](/help/forms/assets/custom-submit-action-clone-repo.png)

1. `[AEMaaCS project directory]`内の次のディレクトリに移動します。

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **重要**：`<app-id>` を実際のアプリケーション ID に置き換えます。

1. カスタム送信アクション用に新しいフォルダーを作成し、任意の名前を付けます。 例えば、フォルダーに`customsubmitaction`という名前を付けます。

   ![&#x200B; カスタム送信アクションフォルダーを作成](/help/forms/assets/custom-submit-action-create-folder.png)

1. 追加されたカスタム送信アクションディレクトリに移動します。

   `[AEMaaCS project directory]` 内で、次のパスに移動します。

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: `<app-id>`を実際のアプリケーション IDに置き換えます。

1. 新しい設定ファイルを作成します。
`customsubmitaction` フォルダー内に、`.content.xml`という名前の新しいファイルを作成します。

   ![構成ファイルの作成](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. このファイルを開き、次のコンテンツを貼り付け、`[customsubmitaction]`を送信アクションの名前に置き換えます

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   例えば、`[customsubmitaction]`をカスタマイズした送信アクション名`Custom Submit Action`に置き換えます。

   ![&#x200B; カスタム送信アクション設定ファイルを作成](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > フォームのオーサリング中に[ ドロップダウンリストに同じ名前が表示されるため、]customsubmitaction`Submit action`の名前を覚えておいてください。


**新しいフォルダーを`filter.xml`**&#x200B;に含める

1. [AEMaaCS プロジェクトディレクトリ]内の `/ui.apps/src/main/content/META-INF/vault/filter.xml` ファイルに移動します。

1. ファイルを開き、最後に次の行を追加します。

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   例えば、次のコード行を追加して、`customsubmitaction` ファイルに`filter.xml` フォルダーを追加します。

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![作成したフォルダーをfilter.xml](/help/forms/assets/custom-submit-action-filter-xml.png)に追加します

1. 変更を保存します。

### 追加された送信アクションのサービスを実装します。

1. `[AEMaaCS project directory]`内の次のディレクトリに移動します。
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: `<app-id>`を実際のアプリケーション IDに置き換えます。
1. 新しいJava ファイルを作成して、追加された送信アクションのサービスを実装します。 例えば、新しいJava ファイルを`CustomSubmitService.java`として追加します。

   ![&#x200B; カスタム送信アクション フォルダー](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. このファイルを開き、カスタム送信アクション実装用のコードを追加します。

   例えば、以下のJava コードは、送信されたデータをログに記録してフォーム送信を処理し、ステータス `OK`を返すOSGi サービスです。 次のコードを`CustomSubmitService.java` ファイルに追加します。

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data]
       -->
       " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![&#x200B; カスタム送信アクションサービス &#x200B;](/help/forms/assets/custom-submit-action-service.png)

1. 変更を保存します。

### コードをデプロイします。

**ローカル開発環境のコードをデプロイ**

* AEM as a Cloud Service `[AEMaaCS project directory]`をローカル開発環境にデプロイして、新しい送信アクションをローカルマシンで試してください。 ローカル開発環境にデプロイするには：

   1. ローカル開発環境が起動および実行されていることを確認します。ローカル開発環境をまだ設定していない場合は、[AEM Formsのローカル開発環境の設定](/help/forms/setup-local-development-environment.md)に関するガイドを参照してください。

   1. ターミナルウィンドウまたはコマンドプロンプトを開きます。

   1. `[AEMaaCS project directory]`に移動します。

   1. 次のコマンドを実行します。

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![&#x200B; ローカル展開](/help/forms/assets/custom-submit-action-local-deployment.png)

**Cloud Service環境のコードをデプロイ**

* AEM as a Cloud Service `[AEMaaCS project directory]`をCloud Service環境にデプロイします。 Cloud Service 環境にデプロイするには：

   1. 変更を確定：

      新しいカスタム送信アクション設定を追加したら、変更をコミットして明確なGit メッセージを表示します。 （例：「新しいカスタム送信アクションを追加しました」）。

   1. 更新されたコードをデプロイします。

      [既存のフルスタックパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)を通じてコードのデプロイメントをトリガーします。新しいカスタム m送信アクションのサポートを使用して、更新されたコードが自動的にビルドおよびデプロイされます。

      パイプラインをまだ設定していない場合は、[AEM Forms as a Cloud Service のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)のガイドを参照してください。

      ![&#x200B; クラウド展開](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **インストールの確認方法を教えてください。**

      プロジェクトが正常に構築されると、フォームのオーサリング中にカスタム送信アクションが`Submit action` ドロップダウンリストに表示されます。

      ![&#x200B; カスタム送信アクション ドロップダウンリスト &#x200B;](/help/forms/assets/custom-submit-action-drop-down-list.png)

  これで、環境でフォームのオーサリング時に追加されたカスタム送信アクションを使用する準備が整いました。

### 新しく追加された送信アクションを含むアダプティブフォームのプレビュー

1. AEM Forms as a Cloud Service インスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。

   ![Formsとドキュメント &#x200B;](/help/forms/assets/custom-submit-action-fnd.png)

1. アダプティブフォームを選択し、**編集**&#x200B;をクリックします。 フォームが編集モードで開きます。

   ![&#x200B; フォームを編集](/help/forms/assets/custom-submit-action-edit-af.png)

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、送信アクションを選択します。 例えば、送信アクションを`Custom Submit Action`として選択します。

   ![&#x200B; カスタム送信フォーム &#x200B;](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. フォームに記入して送信してください。

   ![&#x200B; フォームを送信](/help/forms/assets/custom-submit-action-submit-form.png)

   ![感謝メッセージ &#x200B;](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   フォームが正常に送信されたら、**Adobe Experience Manager Web コンソール設定**&#x200B;を確認して、ローカル開発環境でのカスタム送信アクションの動作を確認できます。
1. `http://<host>:<port>/system/console/configMgr` にアクセスします。

1. **の** Adobe Experience Manager Web Console Log Support`http://<host>:<port>/system/console/slinglog`に移動します。

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. 「`logs/error.log`」オプションをクリックします。
   ![error.log ファイルを開く](/help/forms/assets/custom-submit-action-error-log.png)

1. `error.log` ファイルを開いて、データが追加されていることを確認します。

   ![error.log ファイル &#x200B;](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > * AEM as a Cloud Service環境でエラーログを確認するには、Splunkを使用します。
   > * カスタム送信アクションサービスで未処理のエラーが発生した場合、AEM as a Cloud Serviceは502 エラーページ HTMLを返します。


## よくある質問

**Q：送信後にアダプティブフォームに5.x.x エラーページが表示されるのはなぜですか？**
カスタム送信アクションサービスは、処理できないエラーで失敗しました。 AEM Cloud Serviceは、デフォルトのエラーページを返します。

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## 関連記事

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
