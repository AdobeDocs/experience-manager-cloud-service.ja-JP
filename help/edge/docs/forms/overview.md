---
title: AEM Forms Edge Delivery Service の概要
description: AEM Forms Edge Delivery Service は、効率化されたデータ収集とユーザーエンゲージメントの将来を想定できるように、最高のパフォーマンス向けに構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 2%

---


# AEM Forms Edge Delivery Service

AdobeのAEM Forms Edge Delivery Service を使用して、フォームの作成を合理化し、完了率を高めます。 この強力で合成可能なサービスにより、優れたパフォーマンスと視覚的な魅力を備えたエンタープライズクラスのフォームを構築できます。 AEMは、ユーザーエクスペリエンスとビジネス目標の両方を優先し、超高速読み込み時間とフォームの完了を確保します。

サービスを使用して以下のことが行えます。

* **見事なフォームを持つCaptivateユーザー**：事前に作成されたコンポーネントのライブラリを使用して、複雑で魅力的なフォームを簡単に作成できます。 reCAPTCHA の統合、電子メールへの直接の送信、シームレスなファイルアップロードを可能にし、SharePoint、Azure Storage、Amazon S3 などのセキュリティで保護されたストレージソリューションを実現します。 独自のカスタムフォームコンポーネントを作成して、独自のビジョンを生み出すこともできます。

* **お好みのツールでデジタル登録エクスペリエンスを作成**：コンテンツソースを分離することで、オーサリングの効率を向上させます。 標準では、ドキュメントベースのオーサリング (Microsoft 365 およびGoogle Workspace) とAEMのオーサリング (AEMエディター ) の両方を使用できます。 そのため、同じ Web サイト上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、アダプティブFormsエディターなどの好みのオーサリングツールを使用できます。

* **完璧な Lighthouse スコアを持つフォームの作成**：低速なインターネット接続でも、すばやく読み込んでレンダリングするフォームを構築します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスは、フォームの完了率の向上とコンバージョン率の向上に貢献します。

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 70%; /* Set image width to 70% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Formsの主な機能">
    </div>


</div>
&lt;!— &gt; * **見事なフォームを使用したCaptivateユーザー**：事前にビルドされたコンポーネントのライブラリを使用して、複雑で魅力的なフォームを簡単に構築できます。 reCAPTCHA の統合、電子メールへの直接の送信、シームレスなファイルアップロードを可能にし、SharePoint、Azure Storage、Amazon S3 などのセキュリティで保護されたストレージソリューションを実現します。 独自のカスタムフォームコンポーネントを作成して、独自のビジョンを生み出すこともできます。

    ![ 登録フォーム ](/help/edge/assets/enrollment-form.png)

* **完璧な Lighthouse スコアを持つフォームの作成**：低速なインターネット接続でも、すばやく読み込んでレンダリングするフォームを構築します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスは、フォームの完了率の向上とコンバージョン率の向上に貢献します。

  ![フォームに最適な Lighthouse スコア](/help/edge/assets/lighthouse-forms.png)

* **お好みのツールでデジタル登録エクスペリエンスを作成**：コンテンツソースを分離することで、オーサリングの効率を向上させます。 標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。そのため、同じ Web サイト上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、AEMエディターなどの好みのオーサリングツールを使用できます。

  ![Edge 配信フォームオーサリングツール](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 主な機能

* **HTML5 ベースのフォームフィールドコンポーネント**:AEM Forms Edge Delivery Service を使用すると、有効なHTML5 に基づいたフォームフィールドを使用して、使いやすくインタラクティブなフォームを作成できます。 [入力タイプ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選択</a>、および <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  コンポーネント。 これらのコンポーネントは、様々なタイプのデータ収集に対応し、特定のニーズに合わせて容易にカスタマイズできます。

* **アクセシビリティ**：フォームブロック内のフィールドにアクセスできます。 各ラベルはそれぞれの入力要素にリンクされ、ID はリンク用に自動生成されます。 フィールドに関連付けられている説明は、 aria-describbedby 属性でリンクされます。 標準の Tab/Shift + Tab キーを使用したキーボードナビゲーションがサポートされています。

* **フォームルール**：ユーザー入力または事前定義された条件に基づいてフィールドの表示、検証および動作を調整するロジックを作成します。 ルールは、フォームにインテリジェンスを追加する柔軟で直感的な方法を提供し、ユーザーの入力に基づいてシームレスに適応させます。

* **ファイルのアップロード**：シームレスなファイル添付機能でフォームを拡張します。 ユーザーからドキュメント、画像、その他のファイルを収集する必要がある場合でも、アダプティブフォームブロックを使用すれば、ファイルのアップロード機能を簡単に統合できます。 カスタム処理オプションを使用できるので、特定の要件に合わせてファイルのアップロードプロセスを調整できます。

* **フォームの検証**：送信前にフォームは検証され、無効なフィールドにはユーザーに表示されるエラーメッセージが適切にマークされます。 これらのエラーの表示には、様々なパターンを使用できます。

* **スタイル設定Forms**：各フォームフィールドは固定のHTML構造を持ち、カスタム CSS または JavaScript ファイルを使用してさらに装飾できます。 CSS/JS のターゲティングフィールドのセレクターは、タイプと名前に基づいて提供されます。


## フォームの作成を開始

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="eds フォームを使用したフォームの作成" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Google Sheet またはMicrosoft Excel を使用したフォームの作成</b>
        </a>
        <p>モバイルデバイスで読み込んで自動的にレンダリングするフォームを作成します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="フォームを送信" alt="EDS フォームでのフォームフラグメントの使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームをスプレッドシートに送信</b>
        </a>
        <p>フォームをMicrosoft Excel またはGoogleシートに直接送信する。</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="スタイルまたはテーマを eds フォームに適用する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">テーマのカスタマイズ</b>
        </a>
        <p>同じテーマを複数のフォームに適用して、一貫したブランドイメージを作成します。</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="フォームフィールドに検証機能を追加する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フィールド検証を適用</b>
        </a>
        <p>フォーム入力で適切な形式を確認することで、エラーと不満を減らすことができます。</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="ルールを使用してフォームに動的な動作を追加する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">ルールを使用してフォームに動的な動作を追加する</b>
        </a>
        <p>複数のフォーム間で事前設定済みのフラグメントを再利用する。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="EDS フォームの翻訳" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームの翻訳</b>
        </a>
        <p>コストを抑えながら、フォームのリーチを拡大します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="EDS フォームに繰り返し可能なセクションを追加" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">繰り返し可能なセクションの追加</b>
        </a>
        <p>繰り返し可能なセクションを容易に作成し、フォームに追加できます。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="標準の JavaScript と CSS を使用したカスタムフォームコンポーネントの作成"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">カスタムコンポーネントの作成</b>
        </a>
        <p>標準の JavaScript と CSS を使用して、コンポーネントとテーマを作成します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="EDS フォームでの reCAPTCHA の使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">reCAPTCHA を使用</b>
        </a>
        <p>堅牢なスパムとボット保護に、OOTB reCAPTCHA 統合を使用します。</p>
    </div>


</div>


</br>









