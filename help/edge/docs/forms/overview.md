---
title: AEM Forms Edge Delivery Service の概要
description: AEM Forms Edge Delivery Service は、効率化されたデータ収集とユーザーエンゲージメントの将来を想定できるように、最高のパフォーマンス向けに構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service は、Adobeが提供する合成可能なサービスで、影響が大きく、パフォーマンスの高い Web フォームを作成して配信できます。 サービスを使用して以下のことが行えます。

* **視覚的に美しいフォームを作成**：ブランドアイデンティティを反映したダイナミックで最新のフォームを使用して、ブランド、cookie-cutter のデザインを見捨て、ユーザーを魅了します。 事前に作成されたコンポーネントを活用するか、独自のカスタムコンポーネントを作成して、ビジョンを迅速かつ簡単に実現します。

* **完璧な Lighthouse スコアを持つフォームの作成**：低速なインターネット接続でも、すばやく読み込んでレンダリングするフォームを構築します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスは、フォームの完了率の向上とコンバージョン率の向上に貢献します。

* **オーサリングと送信を簡素化**：従来のオーサリング環境ではなく、Microsoft Excel やGoogleシートなどの使い慣れたツールを使用してフォームを作成します。 フォームをMicrosoft Excel またはGoogleシートに直接送信し、そのエコシステムを使用して送信されたデータを簡単に処理できます。


この合成可能なサービスはコンテンツソースから切り離され、ユーザーが好みのオーサリングツールを使用できるようにすることで、柔軟にコンテンツを作成できます。

![Edge 配信フォームオーサリングツール](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

コンテンツ作成者は、Microsoft Excel やGoogleシート（ドキュメントベースのオーサリング）、JSON エディター、AEM Forms Adaptive Forms editor for WYSIWYG editing (AEM Formsプロジェクト ) など、使い慣れたツールを活用して、フォームをデザインおよび作成できます。

>[!NOTE]
>
>
> WYSIWYG 編集機能とクロスウォークは、アーリーアダプタープログラムの下で利用可能です。 アーリーアダプタープログラムに参加し、機能へのアクセス権をリクエストするには、公式のメール ID からaem-forms-early-adopter-program@adobe.comに書き込むことができます。

## 基本事項から始めます

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
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="フォームフィールドに検証機能を追加する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フィールド検証を適用</b>
        </a>
        <p>フォーム入力で適切な形式を確認することで、エラーと不満を減らすことができます。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="EDS フォームでのフォームフラグメントの使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームフラグメントの作成</b>
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
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="スタイルまたはテーマを eds フォームに適用する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">テーマのカスタマイズ</b>
        </a>
        <p>同じテーマを複数のフォームに適用して、一貫したブランドイメージを作成します。</p>
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
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="フォームを送信" alt="EDS フォームでのフォームフラグメントの使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームをスプレッドシートに送信</b>
        </a>
        <p>フォームをMicrosoft Excel またはGoogleシートに直接送信する。</p>
    </div>
</div>


</br>









