---
title: アセットマイクロサービスがクラウド内のデジタルアセットを処理する方法を知る
description: クラウドネイティブでスケーラブルなアセット処理マイクロサービスを使用して、デジタルアセットを処理します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 55dd497caaa25cf7c0d8da1c1400b74f7d265d29

---


# アセットマイクロサービスを使用したアセットの取り込みと処理の概要 {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.

-->

クラウドサービスとしてのAdobe Experience Managerは、Experience Managerのアプリケーションと機能をクラウドネイティブで活用する方法です。 この新しいアーキテクチャの主な要素の1つは、アセットの取り込みと処理で、アセットマイクロサービスを利用して行われます。

アセットマイクロサービスは、様々なアセットタイプや処理オプションを最適に処理するためにアドビが管理するクラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。 主なメリットは次のとおりです。

* リソースを大量に消費する操作にシームレスな処理を可能にする、拡張性の高いアーキテクチャ。
* Experience Manager環境のパフォーマンスに影響を与えない、効率的なインデックス作成とテキスト抽出。
* Experience Manager環境でアセット処理を処理するワークフローの必要性を最小限に抑えます。 これにより、リソースが解放され、Experience Managerの負荷が最小限に抑えられ、拡張性が向上します。
* アセット処理の回復力が向上しました。 破損したファイルや非常に大きなファイルなど、非定型的なファイルを処理する際に発生する可能性のある問題が、展開のパフォーマンスに影響を与えなくなりました。
* 管理者向けのアセット処理の設定の簡素化。
* アセット処理の設定はアドビが管理および管理し、様々なファイルタイプのレンディション、メタデータおよびテキスト抽出を処理するための最も既知の設定を提供します
* 適宜、ネイティブのアドビファイル処理サービスが使用され、アドビ独自の形式の高精度な出 [力と効率的な処理が可能です](file-format-support.md)。
* 後処理ワークフローを設定して、ユーザー固有のアクションと統合を追加できます。

アセットマイクロサービスは、サードパーティ製のレンダリングツール（ImageMagickなど）が不要になり、システムの設定がシンプルになると共に、一般的なファイルタイプに対してそのまま使用できる機能を提供します。

## ハイレベルアーキテクチャ {#asset-microservices-architecture}

アセットの取り込みと処理、およびシステム全体のアセットのフローの主要な要素が、高レベルのアーキテクチャ図で示されています。

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![アセットの取り込みと処理アセットのマイクロサ](assets/asset-microservices-overview.png "ービスを使用したアセットの取り込みと処理")

アセットマイクロサービスを使用した取り込みと処理の主な手順は次のとおりです。

* WebブラウザーやAdobe Asset linkなどのクライアントは、アップロードリクエストをExperience Managerに送信し、バイナリクラウドストレージへのバイナリの直接アップロードを開始します。
* バイナリの直接アップロードが完了すると、クライアントからExperience Managerに通知されます。
* Experience Managerは、処理リクエストをアセットマイクロサービスに送信します。 リクエストの内容は、生成する必要のあるレンディションを指定するExperience Managerの処理プロファイル設定によって異なります
* アセットマイクロサービスバックエンドは要求を受け取り、要求に基づいて1つ以上のマイクロサービスにその要求をディスパッチします。 各マイクロサービスは、バイナリクラウドストアから直接元のバイナリにアクセスします。
* レンディションなどの処理の結果は、バイナリクラウドストレージに保存されます。
* 生成されたバイナリ（レンディション）への直接ポインターと共に処理が完了したことがExperience Managerに通知され、Experience Managerでアップロードされたアセットに対して使用できます

これは、アセットの取り込みと処理の基本的なフローです。 設定した場合、Experience Managerは、顧客のワークフローモデルを起動して、アセットの後処理を実行することもできます。例えば、顧客のエンタープライズシステムから情報を取得してアセットのプロパティに追加するなど、顧客環境に固有のカスタマイズされた手順を実行できます。

インジェストと処理フローは、Experience Managerのアセットマイクロサービスアーキテクチャで活用されるいくつかの主要概念を示しています。

* **直接バイナリアクセス** - Experience Manager環境用に設定したアセットはCloud Binary storeに転送（およびアップロード）され、AEM、アセットマイクロサービス、最後にクライアントは直接アクセスして作業を行うことができます。 これにより、ネットワークへの負荷と保存されるバイナリの複製を最小限に抑えることができます。
* **外部化処理** — アセットの処理はAEM環境の外部で行われ、Digital Asset Managementの主要な機能を提供し、エンドユーザー向けにシステムとの対話的な作業をサポートするリソース（CPU、メモリ）が節約されます。

## 直接バイナリアクセスを使用したアセットのアップロード {#asset-upload-with-direct-binary-access}

製品の一部であるExperience Managerクライアントは、デフォルトでバイナリに直接アクセスできるアップロードをすべてサポートします。 これには、Webインターフェイスを使用したアップロード、Adobe Asset Link、AEMデスクトップアプリが含まれます。

AEM HTTP APIで直接機能するカスタムアップロードツールを使用できます。 これらのAPIを直接使用することも、アップロードプロトコルを実装する次のオープンソースプロジェクトを使用して拡張することもできます。

* [ソースアップロードライブラリを開く](https://github.com/adobe/aem-upload)
* [オープンソースのコマンドラインツール](https://github.com/adobe/aio-cli-plugin-aem)

For more information, see [uploading assets](add-assets.md).

## カスタムアセットの後処理の追加 {#add-custom-asset-post-processing}

ほとんどのお客様は、設定可能なアセットマイクロサービスからすべてのアセット処理のニーズを得る必要がありますが、追加のアセット処理が必要な場合もあります。 これは特に、統合を介して他のシステムからの情報に基づいてアセットを処理する必要がある場合に当てはまります。 そのような場合は、カスタムの後処理ワークフローを使用できます。

後処理ワークフローは、AEMワークフローエディターで作成および管理される、通常のAEMワークフローモデルです。 お客様は、あらかじめ用意されている使用可能なワークフロー手順やカスタムワークフローの使用など、アセットに対して追加の処理手順を実行するようにワークフローを設定できます。

Adobe Experience Managerは、アセット処理の完了後に後処理のワークフローを自動的にトリガーするように設定できます。

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスの概要](asset-microservices-configure-and-use.md)
>* [サポートされているファイル形式](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [AEM Desktop App](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)
>* [直接バイナリアクセスに関するApache Oakドキュメント](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

