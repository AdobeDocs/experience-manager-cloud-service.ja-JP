---
title: コアコンポーネントに基づくアダプティブフォームのカスタム送信アクションの作成方法
description: カスタマイズされた送信アクションを使用して送信する前にデータを処理する、アダプティブ Formsのカスタム送信アクションを作成する方法について説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 28%

---

# アダプティブForms（コアコンポーネント）のカスタム送信アクションの作成

送信アクションを使用すると、ユーザーはフォームから取得したデータの送信先を選択したり、フォームの送信時に実行する追加機能を定義したりできます。 AEM フォームは、メールの送信やSharePointまたは OneDrive へのデータの保存など、複数の [ 標準の送信アクション （OOTB） ](/help/forms/configure-submit-actions-core-components.md) をサポートしています。

また、カスタム送信アクションを作成して、[ 標準のオプション ](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action) に含まれない機能を追加することもできます。 例えば、フォームデータをサードパーティのアプリケーションと統合したり、ユーザー入力に基づいてパーソナライズされた SMS 通知をトリガーにしたりします。

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## 前提条件

アダプティブForms用の最初のカスタム送信アクションを作成する前に、次のことを確認してください。

* **プレーンテキストエディター（IDE）**：どのプレーンテキストエディターでも機能しますが、Microsoft Visual Studio Code などの統合開発環境（IDE）では、編集を簡単にする高度な機能が提供されます。

* **Git**：このバージョン管理システムは、コードの変更を管理するために必要です。 インストール済みでない場合は、https://git-scm.com からダウンロードしてください。

## フォーム用の最初のカスタム送信アクションの作成

次の図は、アダプティブフォームのカスタム送信アクションを作成する手順を示しています。

![ カスタム送信アクションワークフロー ](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### AEM as a Cloud Service Git リポジトリのクローンを作成します。

1. コマンドラインを開き、AEM as a Cloud Service リポジトリを保存するディレクトリ（例：`/cloud-service-repository/`）を選択します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **この情報はどこにありますか？**

   これらの詳細を見つける手順について詳しくは、Adobe Experience League の記事「[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」を参照してください。

   **プロジェクトの準備が整いました。**

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。このフォルダーには、アプリケーションの名前を付けます（例えば、app-id）。 このフォルダーには、AEM as a Cloud Service Git リポジトリからダウンロードしたすべてのファイルとコードが含まれています。 AEM プロジェクトの `<appid>` は `archetype.properties` ファイルにあります。

   ![アーキタイププロパティ](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   このガイドでは、このフォルダーを `[AEMaaCS project directory]` と呼びます。

## 新しい送信アクションを追加

1. エディターでリポジトリフォルダーを開きます。

   ![ クローンリポジトリ ](/help/forms/assets/custom-submit-action-clone-repo.png)

1. `[AEMaaCS project directory]` ージ内の次のディレクトリに移動します。

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **重要**：`<app-id>` を実際のアプリケーション ID に置き換えます。

1. カスタム送信アクション用の新しいフォルダーを作成し、任意の名前を付けます。 例えば、フォルダーに `customsubmitaction` という名前を付けます。

   ![ カスタム送信アクションフォルダーの作成 ](/help/forms/assets/custom-submit-action-create-folder.png)

1. 追加したカスタム送信アクションディレクトリに移動します。

   `[AEMaaCS project directory]` 内で、次のパスに移動します。

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: `<app-id>` を実際のアプリケーション ID に置き換えます。

1. 新しい設定ファイルを作成します。
`customsubmitaction` フォルダー内に、`.content.xml` という名前の新しいファイルを作成します。

   ![ 設定ファイルを作成 ](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. このファイルを開き、次の内容を貼り付けます。`[customsubmitaction]` は、送信アクションの名前に置き換えます

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   例えば、`[customsubmitaction]` をカスタマイズした送信アクション名に置き換え `Custom Submit Action` す。

   ![ カスタム送信アクション設定ファイルの作成 ](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > [customsubmitaction] の名前は、フォームのオーサリング時に「`Submit action`」ドロップダウンリストに表示される名前と同じであるため、覚えておいてください。


**新しいフォルダーを`filter.xml`** に含める

1. [AEMaaCS プロジェクトディレクトリ]内の `/ui.apps/src/main/content/META-INF/vault/filter.xml` ファイルに移動します。

1. ファイルを開き、最後に次の行を追加します。

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   例えば、次のコード行を追加して、`customsubmitaction` ファイルに `filter.xml` フォルダーを追加します。

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![ 作成したフォルダーを filter.xml に追加 ](/help/forms/assets/custom-submit-action-filter-xml.png)

1. 変更を保存します。

### 追加した送信アクションのサービスを実装します。

1. `[AEMaaCS project directory]` ージ内の次のディレクトリに移動します。
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: `<app-id>` を実際のアプリケーション ID に置き換えます。
1. 新しい Java ファイルを作成して、追加した送信アクションのサービスを実装します。 例えば、`CustomSubmitService.java` のように新しい Java ファイルを追加します。

   ![ カスタム送信アクションフォルダー ](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. このファイルを開き、カスタム送信アクション実装のコードを追加します。

   例えば、次の Java コードは、送信されたデータをログに記録してフォーム送信を処理し、ステータス `OK` ータを返す OSGi サービスです。 `CustomSubmitService.java` ファイルに次のコードを追加します。

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
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![ カスタム送信アクションサービス ](/help/forms/assets/custom-submit-action-service.png)

1. 変更を保存します。

### コードをデプロイします。

**ローカル開発環境用のコードのデプロイ**

* AEM as a Cloud Service、`[AEMaaCS project directory]` をローカル開発環境にデプロイして、ローカルマシンで新しい送信アクションを試します。 ローカル開発環境にデプロイするには：

   1. ローカル開発環境が起動および実行されていることを確認します。ローカル開発環境をまだ設定していない場合は、[AEM Formsのローカル開発環境の設定 ](/help/forms/setup-local-development-environment.md) に関するガイドを参照してください。

   1. ターミナルウィンドウまたはコマンドプロンプトを開きます。

   1. `[AEMaaCS project directory]` に移動します。

   1. 次のコマンドを実行します。

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![ ローカルデプロイメント ](/help/forms/assets/custom-submit-action-local-deployment.png)

**Cloud Service環境用のコードのデプロイ**

* AEM as a Cloud Service、`[AEMaaCS project directory]` をCloud Service環境にデプロイします。 Cloud Service 環境にデプロイするには：

   1. 変更内容をコミットします。

      新しいカスタム送信アクション設定を追加したら、明確な Git メッセージを使用して変更をコミットします。 （例：「新しいカスタム送信アクションを追加」）。

   1. 更新されたコードをデプロイします。

      [既存のフルスタックパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)を通じてコードのデプロイメントをトリガーします。新しいカスタム m 送信アクションのサポートを使用して、更新されたコードを自動的にビルドおよびデプロイします。

      パイプラインをまだ設定していない場合は、[AEM Forms as a Cloud Service のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)のガイドを参照してください。

      ![ クラウドデプロイメント ](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **インストールを確認するにはどうすればよいですか？**

      プロジェクトが正常に作成されると、フォームのオーサリング中にカスタム送信アクションが `Submit action` ドロップダウンリストに表示されます。

      ![ カスタム送信アクションドロップダウンリスト ](/help/forms/assets/custom-submit-action-drop-down-list.png)

  これで、環境でフォームをオーサリングする際に、追加されたカスタム送信アクションを使用する準備が整いました。

### 新しく送信アクションが追加されたアダプティブフォームをプレビューする

1. AEM Forms as a Cloud Service インスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。

   ![Formsとドキュメント ](/help/forms/assets/custom-submit-action-fnd.png)

1. アダプティブフォームを選択し、「**編集**」をクリックします。 フォームが編集モードで開きます。

   ![ フォームを編集 ](/help/forms/assets/custom-submit-action-edit-af.png)

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、送信アクションを選択します。 例えば、送信アクションを `Custom Submit Action` のように選択します。

   ![ カスタム送信フォーム ](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. フォームに入力して送信します。

   ![ 送信フォーム ](/help/forms/assets/custom-submit-action-submit-form.png)

   ![ 感謝のメッセージ ](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   フォームが正常に送信されたら、**Adobe Experience Manager Web コンソールローカル開発** を調べて、設定環境でのカスタム送信アクションのアクションを確認できます。
1. `http://<host>:<port>/system/console/configMgr` にアクセスします。

1. **Adobe Experience Manager Web コンソールのログサポート** （`http://<host>:<port>/system/console/slinglog`）に移動します。

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. `logs/error.log` オプションをクリックします。
   ![error.log ファイルを開く ](/help/forms/assets/custom-submit-action-error-log.png)

1. `error.log` ファイルを開いて、データが追加されていることを確認します。

   ![error.log ファイル ](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > AEM as a Cloud Service環境でエラーログを表示するには、Splunk を使用します。

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## 関連記事

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
