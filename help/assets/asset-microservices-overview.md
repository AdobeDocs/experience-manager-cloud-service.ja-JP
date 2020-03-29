---
title: アセットマイクロサービスがクラウド内のデジタルアセットを処理する方法を知る
description: クラウドネイティブでスケーラブルなアセット処理マイクロサービスを使用して、デジタルアセットを処理します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# アセットの取り込みとアセットのマイクロサービスによる処理の概要 {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.
-->

クラウドサービスとしてのAdobe Experience Managerは、Experience Managerのアプリケーションと機能をクラウドネイティブで活用する方法を提供します。 この新しいアーキテクチャの主な要素の1つは、アセットの取り込みと処理で、アセットのマイクロサービスを活用しています。

アセットマイクロサービスは、様々なアセットタイプや処理オプションを最適に処理するためにアドビが管理しているクラウドサービスを利用して、拡張性と耐障害性に優れたアセット処理をおこないます。主な利点は次のとおりです。

* リソースを大量に消費する操作に対してシームレスな処理を可能にする、拡張性の高いアーキテクチャ。
* Experience Managerのパフォーマンスに影響を与えない、効率的なインデックス作成抽出とテキスト環境。
* Experience Managerのワークフローでアセット処理を処理する必要を最小限に抑えます。 これにより、リソースが解放され、Experience Managerの負荷が最小限に抑えられ、スケーラビリティが向上します。
* アセット処理の回復力を改善。 破損したファイルや非常に大きなファイルなど、非定型的なファイルを処理する際に発生する可能性のある問題は、展開のパフォーマンスに影響を与えなくなりました。
* 管理者向けのアセット処理の設定の簡素化。
* アセット処理の設定は、様々なファイルタイプのレンディション、メタデータおよびテキスト抽出を処理するための最も既知の設定を提供するために、アドビが管理および管理します
* アドビの固有のファイル処理サービスが適宜使用され、アドビ独自の形式を高精度に出力し、効 [率的に処理することができます](file-format-support.md)。
* 後処理ワークフローを設定して、ユーザー固有のアクションと統合を追加する機能。

アセットマイクロサービスは、サードパーティのレンダリングツール（ImageMagickなど）が不要になり、システムの設定が簡単になると共に、一般的なファイルタイプに対してそのまま使用できる機能を提供します。

## ハイレベルアーキテクチャ {#asset-microservices-architecture}

高レベルのアーキテクチャ図は、システム全体のアセットの取り込みと処理、およびフローの主要な要素を示しています。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![アセットの取り込みと処理アセットのマイクロサ](assets/asset-microservices-overview.png "ービスを使用したアセットの取り込みと処理")

アセットマイクロサービスを使用した取り込みと処理の主な手順は、次のとおりです。

* WebブラウザーやAdobe Asset Linkなどのクライアントは、Experience Managerにアップロードリクエストを送信し、開始はバイナリクラウドストレージに直接バイナリをアップロードします。
* バイナリの直接アップロードが完了すると、クライアントからExperience Managerに通知されます。
* Experience Managerは、処理リクエストをアセットマイクロサービスに送信します。 リクエストの内容は、指定するExperience Managerの処理プロファイルの設定（生成するレンディション）によって異なります
* アセットマイクロサービスバックエンドは、要求を受け取り、要求に基づいて1つ以上のマイクロサービスにその要求をディスパッチします。 各マイクロサービスは、バイナリクラウドストアから直接元のバイナリにアクセスします。
* レンディションなどの処理の結果は、バイナリクラウドストレージに保存されます。
* 処理が完了したことと、生成されたバイナリ（レンディション）への直接ポインターがExperience Managerに通知されます。これらのバイナリは、アップロードされたアセットに対してExperience Managerで使用できます

これは、アセットの取り込みと処理の基本的なフローです。 設定した場合、Experience Managerでは、開始の顧客のワークフローモデルを使用して、顧客の環境に固有のカスタマイズされた手順を実行するなど、アセットの後処理を行うこともできます。例えば、顧客の企業システムから情報を取得して、アセットのプロパティに追加します。

取り込みと処理フローは、Experience Managerのアセットマイクロサービスアーキテクチャの主要な概念です。

* **直接バイナリアクセス**:Experience Manager環境用に設定したアセットはCloud Binary Storeに転送（およびアップロード）され、AEM、アセットマイクロサービス、最後にクライアントが直接アクセスして作業を行えるようになります。 これにより、ネットワークへの負荷と、保存されるバイナリの重複を最小限に抑えることができます。
* **外部化処理**:アセットの処理はAEM環境の外部で行われ、主要なDigital Asset Management機能を提供し、エンドユーザー向けのシステムとの対話型作業をサポートするリソース（CPU、メモリ）を節約します。

## 直接バイナリアクセスを使用したアセットのアップロード {#asset-upload-with-direct-binary-access}

製品の一部であるExperience Managerクライアントは、デフォルトでは、すべてのアップロードを直接バイナリアクセスでサポートします。 これには、Webインターフェイス、Adobe Asset Link、AEMデスクトップアプリを使用したアップロードが含まれます。

AEM HTTP APIで直接機能するカスタムアップロードツールを使用できます。 これらのAPIを直接使用するか、アップロードプロトコルを実装する次のオープンソースプロジェクトを使用して拡張できます。

* [オープンソースアップロードライブラリ](https://github.com/adobe/aem-upload)
* [オープンソースコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)

For more information, see [upload assets](add-assets.md).

## 追加カスタムアセットの後処理 {#add-custom-asset-post-processing}

ほとんどのお客様は、設定可能なアセットマイクロサービスからすべてのアセット処理のニーズを得る必要がありますが、追加のアセット処理が必要な場合もあります。 これは特に、統合を介して他のシステムからの情報に基づいてアセットを処理する必要がある場合に当てはまります。 そのような場合は、カスタムの後処理ワークフローを使用できます。

後処理ワークフローは、AEM Workflowエディターで作成および管理される、通常のAEMワークフローモデルです。 お客様は、利用可能なすぐに使用できるワークフロー手順やカスタムワークフローなど、アセットに対する追加の処理手順を実行するようにワークフローを設定できます。

Adobe Experience Managerは、アセットの処理が完了した後に後処理ワークフローを自動的にトリガーするように設定できます。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスの概要](asset-microservices-configure-and-use.md)
>* [サポートされているファイル形式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [AEM Desktop App](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)
>* [直接バイナリアクセスに関するApache Oakのドキュメント](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

