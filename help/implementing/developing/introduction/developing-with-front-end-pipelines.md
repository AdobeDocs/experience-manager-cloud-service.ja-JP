---
title: フロントエンドパイプラインを使用したサイトの開発
description: フロントエンドパイプラインを使用すると、開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。この記事では、最適なパフォーマンスと効率を確保するフロントエンドビルドプロセスに関する主な考慮事項の概要について説明します。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '1126'
ht-degree: 100%

---


# フロントエンドパイプラインを使用したサイトの開発 {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

[フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)を使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発を大幅に速めることができます。この記事では、プロセスの仕組みについて説明し、プロセスを最大限に活用できるように主な考慮事項に焦点を当てます。

>[!TIP]
>
>フロントエンドパイプラインの使用方法とそのメリットをまだ習熟していない場合は、[クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)ガイドを参照してください。バックエンド開発とは無関係に、新しいサイトを素早くデプロイし、そのテーマをカスタマイズする方法の例を示します。

## AEM Cloud Manager のフロントエンドパイプラインの設定およびビルドプロセスについて {#front-end-build-contract}

[フルスタックビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)と同様に、フロントエンドパイプラインには独自の環境があります。開発者はフロントエンドビルドコントラクトに従っている限り、このパイプラインにある程度の柔軟性があります。

フロントエンドパイプラインでは、フロントエンド `Node.js` プロジェクトでデプロイするビルドを生成するのに、`build` スクリプトディレクティブを使用する必要があります。この要件が存在するのは、Cloud Manager がコマンド `npm run build` を使用して、フロントエンドビルドに対してデプロイ可能なプロジェクトを生成するからです。

`dist` フォルダーの結果のコンテンツは、最終的には Cloud Manager によってデプロイされ、静的ファイルとして提供されます。これらのファイルは AEM の外部でホストされますが、デプロイ済み環境の `/content/...` URL 経由で使用可能になります。

## サポートされている Node.js バージョン {#node-versions}

フロントエンドビルド環境は、次の `Node.js` バージョンをサポートしています。

* 23
* 22
* 20
* 18
* 16
* 14（デフォルト）
* 12

`NODE_VERSION` [環境変数](/help/implementing/cloud-manager/environment-variables.md)を使用して、目的のバージョンを設定できます。

## AEM のフロントエンドパイプラインの命名と管理のベストプラクティス {#single-source-of-truth}

AEM のデプロイメントのベストプラクティスは、唯一の明確な情報源を維持することです。Cloud Manager はこの原則を強化するように設計されています。ただし、フロントエンドパイプラインではコードの一部を分離できるので、適切な設定が不可欠です。競合を回避するために、複数のフロントエンドパイプラインを同じ環境内の同じサイトにデプロイしないでください。

このため、特に複数のフロントエンドパイプラインを作成する場合、アドビでは体系的な命名規則を維持することをお勧めします。次の推奨事項を使用できます。

* `package.json` ファイルの `name` プロパティで定義されるフロントエンドモジュールの名前には、適用先のサイトの名前を含める必要があります。例えば、`/content/wknd` の場所にあるサイトの場合、フロントエンドモジュールの名前は `wknd-theme` のようになります。
* フロントエンドモジュールが他のモジュールと同じ Git リポジトリを共有する場合、そのフォルダーの名前はフロントエンドモジュールと同じにするか、同じ名前を含める必要があります。例えば、フロントエンドモジュールの名前が `wknd-theme` の場合、そのモジュールを含むフォルダー名は `wknd-theme-sources` のようになります。
* Cloud Manager フロントエンドパイプラインの名前には、フロントエンドモジュールの名前も含め、デプロイ先の環境（実稼動または開発）を追加する必要があります。 例えば、`wknd-theme` という名前のフロントエンドモジュールの場合、パイプラインに `wknd-theme-prod` のような名前を付けることができます。

このような規則により、次のデプロイメントエラーを防ぐことができます。

* フロントエンドモジュールを間違ったサイトに適用する。
* 同じサイトを適用する複数のフロントエンドモジュールを作成すると、相互に上書きされる。
* 同じソースに対して複数のフロントエンドパイプラインを作成すると、競合状態が発生する可能性があり、デプロイメントの順序は保証されない。

## AEM の安定性を確保するのにフロントエンドとバックエンドの開発を調整する。 {#separation-of-concerns}

関心の分離に関する重要なベストプラクティスは、関心間の境界を定義する契約を慎重に設計および管理することです。フロントエンドパイプラインでは、この契約はサイトによってレンダリングされる HTML および JSON 出力です。この出力の安定性を維持することで、フロントエンドパイプラインが最大限の価値を提供し、フロントエンドチームが独立して作業できるようになります。

現在、フロントエンドパイプラインと同期してフルスタックパイプラインを実行する組み込みの機能はありません。したがって、フロントエンド開発をフルスタックパイプラインから分離する場合は、境界を定義する契約を慎重に管理することが重要です。この契約は、通常、Experience Manager がレンダリングする HTML や JSON、またはその両方で構成されます。この契約への変更は、スムーズな移行と更新の適切な順序を確保するために、異なるパイプラインを管理するチーム間で慎重に調整する必要があります。

HTML や JSON 出力に変更を行う場合、特に両方の領域に影響を与える場合は、通常、次の手順をお勧めします。

1. バックエンドチームは、まず、新しい HTML や JSON 出力を使用して開発環境を設定します。
   1. フルスタックパイプラインを介して、必要な新しい HTML や JSON 出力、またはその両方のレンダリングに必要なコードをデプロイします。
   1. フロントエンドチームが以前にアクセス権を持っていなかった環境の場合は、次の手順を実行する必要があります。
      1. URL：フロントエンドチームは、その開発環境の URL を知っておく必要があります。
      1. ACL：フロントエンドチームには、「寄稿者」権限と似た権限を持つローカル AEM ユーザーが割り当てられている必要があります。
      1. Git：フロントエンドチームには、その開発環境を具体的にターゲットとするフロントエンドモジュール用として、個別の Git の場所が必要です。

         一般的な方法は、開発環境で行われた変更を管理する `dev` 分岐を作成することです。この方法により、実稼動環境へのデプロイメントに使用される `main` 分岐に簡単に結合して戻すことができます。

      1. パイプライン：フロントエンドチームには、開発環境にデプロイする、フロントエンドパイプラインが必要です。そのパイプラインは、前のポイントで説明したように、通常は `dev` 分岐にあるフロントエンドモジュールをデプロイします。
1. 次に、フロントエンドチームは、古い出力と新しい出力の両方で CSS と JS コードを動作するようにします。
   1. 通常どおり、ローカルで開発するには、次の手順を実行します。
      1. `npx aem-site-theme-builder proxy` コマンドは、AEM 環境からコンテンツを取得するプロキシサーバーを起動します。フロントエンドモジュールの CSS ファイルと JS ファイルを、ローカルの `dist` フォルダーのファイルに置き換えます。
      1. 非表示の `.env` ファイルで `AEM_URL` 変数を設定すると、ローカルプロキシサーバーがコンテンツを使用する AEM 環境を制御できます。
      1. そのため、`AEM_URL` の値を変更すると、両方の環境に適合するように CSS と JS を調整するために、実稼動環境と開発環境を切り替えることができます。
      1. 新しい出力をレンダリングする開発環境と、古い出力をレンダリングする実稼動環境で動作する必要があります。
   1. フロントエンドの作業は、更新されたフロントエンドモジュールが両方の環境で動作し、両方にデプロイされた時点で完了します。
1. その後、バックエンドチームは、フルスタックパイプラインを介して新しい HTML や JSON 出力、またはその両方をレンダリングするコードをデプロイすることにより、実稼動環境を更新できます。
1. フロントエンドチームは、CSS と JS をクリーンアップして、古い出力でのみ必要だった要素を削除し、フロントエンドパイプラインを介して最終的な更新を実稼動環境にデプロイできます。

## その他のリソース {#additional-resources}

* AEM サイトテーマを使用して、サイトのスタイルやデザインをカスタマイズする方法を説明します。

  [サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)を参照してください。

* アドビは、新しいサイトテーマを作成するための一連のスクリプトとして AEM Site Theme Builder を提供します。

  [AEM Site Theme Builder](https://github.com/adobe/aem-site-theme-builder) を参照してください



