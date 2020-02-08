---
title: ビデオプロファイル
description: Dynamic Media には、事前定義済みのアダプティブビデオエンコーディングプロファイルが最初から付属しています。この標準提供プロファイルの設定は、ユーザーができる限り最高の閲覧エクスペリエンスを得られるように最適化されています。また、ビデオにスマートな切り抜きを追加することもできます。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# ビデオプロファイル{#video-profiles}

Dynamic Media には、事前定義済みのアダプティブビデオエンコーディングプロファイルが最初から付属しています。この標準提供プロファイルの設定は、ユーザーができる限り最高の閲覧エクスペリエンスを得られるように最適化されています。アダプティブビデオエンコーディングプロファイルを使用してマスタービデオをエンコーディングすると、再生中にビデオプレーヤーによって、顧客のインターネット接続速度に応じてビデオストリームの品質が自動調整されます。これがアダプティブストリーミングと呼ばれるものです。

ビデオの品質を決めるその他の要因には、次のようなものがあります。

* **アップロードされたマスタービデオの解像度**

   MP4ビデオが240pや360pなど低い解像度で録画された場合、高解像度でストリーミングすることはできません。

* **ビデオプレーヤーのサイズ**

   デフォルトでは、アダプティブビデオエンコーディングプロファイルの「幅」は「自動」に設定されています。再生中は、プレーヤーのサイズに応じた最適な品質が使用されます。

See [Best Practices for Video Encoding](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

[処理プロファイルを使用するためのデジタルアセットの編成のベストプラクティス](/help/assets/dynamic-media/best-practices-for-file-management.md)を参照してください。

>[!NOTE]
>
>ビデオのメタデータと関連するビデオ画像サムネールを生成するには、ビデオ自体がダイナミックメディアでのエンコード処理を経る必要があります。 In AEM, the **[!UICONTROL Dynamic Media Encode Video]** workflow encodes video if you have enabled dynamic media and set up video cloud services. このワークフローは、ワークフローの処理履歴およびエラー情報を捕捉します。詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](/help/assets/dynamic-media/video.md#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。Dynamic Media を有効にし、ビデオクラウドサービスを設定済みの場合、ビデオをアップロードすると、**[!UICONTROL Dynamic Media エンコードビデオ]**&#x200B;ワークフローが自動的に有効になります（Dynamic Media を使用していない場合は、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローが有効になります）。
>
>メタデータは、アセットの検索時に役に立ちます。サムネールは、エンコード中に生成される静的なビデオ画像です。 これらはAEMシステムで必須で、カードビュー、検索結果ビューおよびアセットリストビューでビデオを視覚的に識別するのに役立つユーザーインターフェイスで使用されます。 生成されたサムネールは、エンコードされたビデオのレンディションアイコン（ペインターのパレット）をタップすると表示されます。

ビデオプロファイルの作成が完了したら、そのプロファイルをフォルダーまたは複数のフォルダーに適用します。 See [Applying a video profile to folders.](#applying-a-video-profile-to-folders)

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing)を参照してください。

See also [Profiles for Processing Metadata, Images, and Videos](/help/assets/dynamic-media/processing-profiles.md).

## Adaptive video encoding presets {#adaptive-video-encoding-presets}

次の表に、モバイルデバイス、タブレットデバイスおよびデスクトップコンピューターへのアダプティブビデオストリーミングにおけるベストプラクティスとなるエンコーディングプロファイルを示します。これらのプリセットは、任意の縦横比のビデオで使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>ビデオ形式のコーデック</strong></td>
   <td><strong>ビデオサイズ - 幅（px）</strong></td>
   <td><strong>ビデオサイズ - 高さ（px）</strong></td>
   <td><strong>縦横比を保持</strong></td>
   <td><strong>ビデオビットレート（Kbps）</strong></td>
   <td><strong>ビデオフレームレート（Fps）</strong></td>
   <td><strong>オーディオコーデック</strong></td>
   <td><strong>オーディオビットレート (Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264（mp4）</p> </td>
   <td>自動</td>
   <td>360</td>
   <td>はい</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264（mp4）</p> </td>
   <td>自動</td>
   <td>540</td>
   <td>はい</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264（mp4）</p> </td>
   <td>自動</td>
   <td>720<br /> </td>
   <td>はい</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## ビデオプロファイルでのスマート切り抜きの使用について {#about-smart-crop-video}

ビデオのスマート切り抜き — ビデオプロファイルで使用できるオプションの機能 — Adobe Senseiの人工知能機能を使用して、サイズに関係なく、アップロードしたアダプティブビデオやプログレッシブビデオの焦点を自動的に検出し、切り抜くツールです。

スマート切り抜きでサポートされるビデオ形式には、MP4、MKV、MOV、AVI、FLV、WMVがあります。

スマート切り抜きでサポートされるビデオファイルの最大サイズは、次の条件です。

* 5分間。
* 30フレーム/秒(FPS)。
* 300 MBのファイルサイズ。

現在、Adobe Senseiは9,000フレームに制限されています。 つまり、30 FPSで5分です。 ビデオのFPSが高いと、サポートされるビデオの最大時間が短くなります。 例えば、60 fpsのビデオは、Adobe Sensaiとスマート切り抜きでサポートされるまで2分半の長さにする必要があります。

![ビデオのスマート切り抜き](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>ビデオスマート切り抜きを機能させるには、ビデオプロファイルに1つ以上のビデオエンコーディングプリセットを含める必要があります。

ビデオにスマート切り抜きを使用するには、アダプティブビデオエンコーディングプロファイルまたはプログレッシブビデオエンコーディングプロファイルを作成します。 プロファイルの一部として、スマート切り抜き **[!UICONTROL 比率ツールを使用し]** 、事前に定義された縦横比を選択します。 例えば、ビデオエンコーディングプリセットを定義した後、縦横比が16 x 9の「モバイル用横置き」定義と、縦横比が9 x 16の「モバイル用縦置き」定義を追加できます。 1x1、4x3、4x5の縦横比も選択できます。

![スマート切り抜きによるビデオエンコーディングプロファイルの編集](assets/edit-smart-crop-video2.png)

ユーザインターフェイスの「スマート切り抜き率」の右端にあるスライダを使用して、ビデオプロファイルのビデオスマート切り抜きのオン/オフを切り替えるこ **[!UICONTROL とができ]** 、注意してください。

ビデオプロファイルを作成して保存した後、目的のフォルダーに適用できます。

詳しくは、特 [定のフォルダーへのビデオプロファイルの適用](#applying-video-profiles-to-specific-folders) 、またはビデ [オプロファイルのグローバルな適用を参照してくださ](#applying-a-video-profile-globally)い。

画像のスマート [切り抜きも参照してください](image-profiles.md)。

## Creating a video profile for adaptive streaming {#creating-a-video-encoding-profile-for-adaptive-streaming}

ダイナミックメディアには、定義済みのアダプティブビデオエンコーディングプロファイルが既に付属しています。これは、最適な視聴環境に最適化されたMP4 H.264用のビデオアップロード設定のグループです。このプロファイルは、ビデオのアップロード時に使用できます。

この事前定義済みプロファイルがニーズに合わない場合は、独自のアダプティブビデオエンコーディングプロファイルを作成することもできます。When you use the setting **[!UICONTROL Encode for adaptive streaming]**–as a best practice–all encoding presets that you add to the profile are validated to ensure that all videos have the same aspect ratio. さらに、エンコーディングされたビデオは、ストリーミング向けの複数ビットレート設定として扱われます。

ビデオエンコーディングプロファイルの作成時に、ユーザー補助の目的で、ほとんどのエンコーディングオプションに対して推奨されるデフォルト設定があらかじめ入力されます。ただし、推奨されるデフォルト値以外の値を選択する場合は、再生中にビデオ品質が低下したり、その他のパフォーマンス問題が発生したりする可能性があることに注意してください。

プロファイル内のすべての MP4 H.264 ビデオエンコーディングプリセットで、次の値について、プロファイル内の個々のエンコーディングプリセットで同じ値が使用され、アダプティブストリーミングを実行できることが検証されます。

* ビデオ形式のコーデック - MP4 H.264（.mp4）
* オーディオコーデック
* オーディオビットレート
* 縦横比を保持
* 2 パスエンコーディング
* 固定ビットレート
* H264 プロファイル
* オーディオのサンプリングレート

値が異なる場合も、プロファイルの作成をそのまま続行できますが、アダプティブストリーミングは実行できなくなることに注意してください。ユーザーには単一ビットレートのストリーミングが示されます。プロファイル内の個々のエンコーディングプリセットで同じ値を使用するようにエンコーディング設定を編集することをお勧めします（「アダプティブストリーミング用にエンコーディング」が有効になっている場合、ビデオプロファイル／プリセットエディターでアダプティブビデオエンコーディング設定のパリティを適用する必要があります）。

[プログレッシブストリーミング用のビデオエンコーディングプロファイルの作成](#creating-a-video-encoding-profile-for-progressive-streaming)も参照してください。

[ビデオエンコーディングのベストプラクティス](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos)も参照してください。

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing)を参照してください。

**アダプティブストリーミング用のビデオプロファイルを作成するには**、

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. Click or tap **[!UICONTROL Create]** to add a new video profile.

1. プロファイルの名前と説明を入力します。
1. ビデオエンコーディングプリセットを作成/編集ページで、「ビデオエンコーディングプ **[!UICONTROL リセットを追加」をタップしま]**&#x200B;す。
1. 「**[!UICONTROL 基本]**」タブで、ビデオとオーディオのオプションを設定します。各オプションの横にある情報アイコンをタップすると、追加の説明や、選択したビデオ形式のコーデックに応じた推奨設定が表示されます。
1. 「ビデオサイズ」ヘッダーの下で、「**[!UICONTROL 縦横比を保持]**」チェックボックスがオンになっていることを確認します。
1. ビデオフレームサイズの解像度をピクセル単位で設定します。]**auto**[!UICONTROL  値を使用すると、ソースの縦横比（幅と高さの比率）に合わせて自動的に拡大／縮小されます。例えば、「auto x 480」や「640 x auto」のようになります。

1. 次のいずれかの操作をおこないます。

   * 「**[!UICONTROL 幅]**」フィールドに「**[!UICONTROL auto]**」と入力します。「**[!UICONTROL 高さ]**」フィールドに値をピクセル単位で入力します。

   * ビデオのサイズを目で確認できるようにするには、「**[!UICONTROL 高さ]**」の右にある情報アイコン（「i」）をタップして、サイズ計算ツールページを開きます。**[!UICONTROL サイズ計算ツール]**&#x200B;を使用して、必要なビデオサイズ（青のボックスで表示）を設定します。完了したら、右上隅の「**[!UICONTROL X]**」をタップします。

1. (Optional) Tap the **[!UICONTROL Advanced]** tab and ensure the **[!UICONTROL Use Default Values]** check box is selected (recommended). または、ビデオおよびオーディオの詳細設定を変更します。
1. ページの右上隅の「**[!UICONTROL 保存]**」をタップして、プリセットを保存します。
1. 次のいずれかの操作をおこないます。
   * 手順 4～10 を繰り返して、その他のエンコーディングプリセットを作成します。（アダプティブビデオストリーミングの場合は、複数のビデオプリセットが必要です）。
   * 次の手順に進みます。

1. （オプション）このプロファイルを適用するビデオにビデオスマート切り抜きを追加するには、次の操作を行います。
   * ビデオプロファイルを編集ページの「スマート切り抜き率」の見出しの右側で、「新規追加」をタ **[!UICONTROL ップします]**。
   * 「名前」フィールドに、切り抜き率を簡単に識別できるように、切り抜き率の名前を入力します。
   * 切り抜き **[!UICONTROL 率ドロップダウンリスト]** で、使用する比率を選択します。

1. 次のいずれかの操作をおこないます。

   * 必要に応じて、新しい切り抜き比率の追加を続けます。
   * 次の手順に進みます。

1. ページの右上隅の「**[!UICONTROL 保存]**」をもう一度タップして、プロファイルを保存します。

これで、ビデオを含むフォルダーにプロファイルを適用できるようになりました。 詳しくは、フ [ォルダーへのビデオプロファイルの適用](#applying-a-video-profile-to-folders) 、またはビデオプ [ロファイルのグローバルな適用を参照してくださ](#applying-a-video-profile-globally)い。

## Creating a video profile for progressive streaming {#creating-a-video-encoding-profile-for-progressive-streaming}

「**[!UICONTROL アダプティブストリーミング用にエンコーディング]**」オプションを使用しない場合は、プロファイルに追加されるすべてのエンコーディングプリセットが、単一ビットレートのストリーミングまたはプログレッシブビデオ配信用の個々のビデオレンディションとして扱われることに注意してください。また、すべてのビデオレンディションが同じ縦横比であることを確認するための検証は実行されません。

サポートされるビデオ形式のコーデックはH.264(.mp4)およびWebMです。

[アダプティブストリーミング用のビデオエンコーディングプロファイルの作成](#creating-a-video-encoding-profile-for-adaptive-streaming)も参照してください。

[ビデオエンコーディングのベストプラクティス](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos)も参照してください。

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing)を参照してください。

**プログレッシブストリーミング用のビデオプロファイルを作成するには：**

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. Tap **[!UICONTROL Create]** to add a new video profile.
1. プロファイルの名前と説明を入力します。
1. ビデオエンコーディングプリセットを作成/編集ページで、「ビデオエンコーディングプ **[!UICONTROL リセットを追加」をタップしま]**&#x200B;す。
1. 「**[!UICONTROL 基本]**」タブで、ビデオとオーディオのオプションを設定します。各オプションの横にある情報アイコンをタップすると、追加の説明や、選択したビデオ形式のコーデックに応じた推奨設定が表示されます。
1. （オプション）「ビデオサイズ」ヘッダーの下で、「**[!UICONTROL 縦横比を保持]**」チェックボックスをオフにします。
1. 以下の操作を実行してください。
   * 「**[!UICONTROL 幅]**」フィールドに「**[!UICONTROL auto]**」と入力します。
   * 「**[!UICONTROL 高さ]**」フィールドに値をピクセル単位で入力します。ビデオのサイズを視覚化するには、高さの情報アイコンをタップして、サイズ計算ペ **[!UICONTROL ージを開きます]** 。 **[!UICONTROL サイズ計算ツール]**&#x200B;ページを使用して、必要なビデオのサイズ（青いボックス）を設定します。完了したら、ダイアログボックスの右上隅にある「 **[!UICONTROL X」をタップします]**。
1. （オプション）次のいずれかの操作をおこないます。

   * Tap the **[!UICONTROL Advanced]** tab, and make sure the **[!UICONTROL Use Default Values]** check box is selected (recommended).

   * Clear the **[!UICONTROL Use Default Values]** check box and specify the video settings and audio settings you want.
各オプションの横にある情報アイコンをタップすると、追加の説明や、選択したビデオ形式のコーデックに応じた推奨設定が表示されます。

1. ページの右上隅の「**[!UICONTROL 保存]**」をタップして、プリセットを保存します。
1. 次のいずれかの操作をおこないます。

   * 手順 4～9 を繰り返して、その他のエンコーディングプリセットを作成します
   * 次の手順に進みます。

1. （オプション）このプロファイルを適用するビデオにビデオスマート切り抜きを追加するには、次の操作を行います。

   * ビデオプロファイルを編集ページの「スマート切り抜き率」の見出しの右側で、「新規追加」をタ **[!UICONTROL ップします]**。
   * 「名前」フィールドに、切り抜き率を簡単に識別できるように、切り抜き率の名前を入力します。
   * 切り抜き **[!UICONTROL 率ドロップダウンリスト]** で、使用する比率を選択します。

1. 次のいずれかの操作をおこないます。

   * 必要に応じて、新しい切り抜き比率の追加を続けます。
   * 次の手順に進みます。

1. ページの右上隅の「**[!UICONTROL 保存]**」をタップして、プロファイルを保存します。

これで、ビデオを含むフォルダーにプロファイルを適用できるようになりました。 詳しくは、フ [ォルダーへのビデオプロファイルの適用](#applying-a-video-profile-to-folders) 、またはビデオプ [ロファイルのグローバルな適用を参照してくださ](#applying-a-video-profile-globally)い。

## カスタムで追加するビデオエンコーディングパラメーターの使用 {#using-custom-added-video-encoding-parameters}

AEM でビデオプロファイルを作成または編集する際にはユーザーインターフェイスに表示されない、高度なビデオエンコーディングパラメーターを利用して、既存のビデオエンコーディングプロファイルを編集できます。既存のプロファイルに、minBitrate や maxBitrate などの 1 つ以上の高度なパラメーターをカスタムで追加できます。

**カスタムで追加するビデオエンコーディングパラメーターを使用するには**：

1. Tap the AEM logo, then navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. CRXDE Lite ページの左側にあるエクスプローラーパネルで、以下の場所に移動します。

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. ページの右下にあるパネルの「プロパティ」タブで、使用するパラメーターの「**[!UICONTROL 名前]**」、「**[!UICONTROL タイプ]**」および「**[!UICONTROL 値]**」を指定します。

   以下の高度なパラメーターを使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>説明</strong><br /> </td>
   <td><strong>タイプ</strong><br /> </td>
   <td><strong>値</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>エンコードに使用するH.264レベル。 通常、この値は、使用しているエンコーディング設定に基づいて自動的に決定されます。</td>
   <td><code>String</code></td>
   <td><p>10 * h264レベル</p> <p>例：3.0 = 30、1.3 = 13)</p> <p>デフォルト値はありません。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>キーフレーム間のターゲットフレーム数。 2～10 秒ごとにキーフレームが生成されるようにこの値を計算します。例えば、1 秒あたり 30 フレームの場合、キーフレーム間隔は 60～300 にします。<br /> キーフ <br /> レーム間隔を小さくすると、アダプティブビデオエンコーディングのストリームシークとストリーム切り替えの動作が改善され、動きの多いビデオの画質も向上します。 ただし、キーフレームが増えるとファイルのサイズも増えるので、通常、キーフレーム間隔を短くすると、特定のビットレートでの全体的なビデオの画質は低下します。</td>
   <td><code>String</code></td>
   <td><p>正の数。</p> <p>初期設定は 300 です。</p> <p>HLS（HTTPライブストリーミング）の推奨値は60 ～ 90です。</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>可変ビットレートエンコーディングを可能にする最小ビットレート(Kbps)。</p> <p>This parameter only applies when<strong> Use Constant Bitrate</strong> is deselected in the Advanced tab when you create or edit a video encoding profile.</p> <p>ビットレートも参 <a href="/help/assets/dynamic-media/video.md#bitrate">照してくださ</a>い。</p> </td>
   <td><code>String</code></td>
   <td><p>正の数(Kbps)。</p> <p>デフォルト値はありません。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>可変ビットレートエンコーディングを許可する最大ビットレート(Kbps)。</p> <p>This parameter only applies when<strong> Use Constant Bitrate</strong> is deselected in the Advanced tab when you create or edit a video encoding profile.</p> <p>ビットレートも参 <a href="/help/assets/dynamic-media/video.md#bitrate">照してくださ</a>い。</p> </td>
   <td><code>String</code></td>
   <td><p>正の数(Kbps)。</p> <p>デフォルト値はありません。ただし、推奨値は、エンコーディングのビットレートの最大 2 倍です。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>オーディオコーデッ <code>true</code> クでサポートされている場合、オーディオストリームの固定ビットレートを強制するには、値をに設定します。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>デフォルトは <code>false</code> です。</p> <p>Recommended value for HLS (HTTP Live Streaming) is <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. ページの右下隅付近にある「**[!UICONTROL 追加]**」をタップします。
1. 次のいずれかの操作をおこないます。

   * 手順 3 および 4 を繰り返して、ビデオエンコーディングプロファイルに別のパラメーターを追加します。
   * ページの左上隅付近にある「**[!UICONTROL すべて保存]**」をタップします。

1. CRXDE Lite ページの左上隅にある「**[!UICONTROL ホームに戻る]**」アイコンをタップして、AEM に戻ります。

### Editing a video profile {#editing-a-video-encoding-profile}

作成した任意のビデオプロファイルを編集して、そのプロファイル内のビデオプリセットを追加、編集または削除できます。

デフォルトでは、Dynamic Media に付属している定義済みの既製&#x200B;**[!UICONTROL アダプティブビデオエンコーディング]**&#x200B;プロファイルを編集することはできません。代わりに、プロファイルを手軽にコピーし、新しい名前で保存することができます。その後、コピーしたプロファイルで目的のプリセットを編集できます。

[ビデオエンコーディングのベストプラクティス](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos)も参照してください。

他のアセットタイプへの高度な処理パラメーターの定義については、[アセット処理の設定](/help/assets/dynamic-media/config-dm.md#configuring-asset-processing)を参照してください。

**ビデオプロファイルを編集するには**:

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. ビデオプロファイルページで、1 つのビデオプロファイル名のチェックボックスをオンにします。
1. ツールバーの「**[!UICONTROL 編集]**」をタップします。
1. ビデオエンコーディングプロファイルページで、必要に応じて名前と説明を編集します。
1. As a best practice, ensure that the **[!UICONTROL Encode for adaptive streaming]** check box is selected.
情報アイコンをタップすると、アダプティブストリーミングの説明が表示されます。 （プログレッシブビデオプロファイルを編集する場合は、このチェックボックスをオンにしないでください）。
1. 「ビデオエンコーディングプリセット」ヘッダーの下で、プロファイルを構成するビデオエンコーディングプリセットを追加、編集または削除します。

   Tap the information icon next to each option on the **[!UICONTROL Basic]** and **[!UICONTROL Advanced]** tabs for additional descriptions or recommended settings based on the selected video format codec.

1. ページの右上隅にある「保存」をタップし **[!UICONTROL ます]**。

### Copying a video profile {#copying-a-video-encoding-profile}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. ビデオプロファイルページで、1 つのビデオプロファイル名のチェックボックスをオンにします。
1. On the toolbar, tap **[!UICONTROL Copy]**.
1. ビデオエンコーディングプロファイルページで、プロファイルの新しい名前を入力します。
1. As a best practice, ensure that the **[!UICONTROL Encode for adaptive streaming]** check box is selected. 情報アイコンをタップすると、アダプティブストリーミングの説明が表示されます。 （プログレッシブビデオプロファイルをコピーする場合は、このチェックボックスをオンにしないでください）。

   Dynamic Media（ハイブリッドモード）では、WebM ビデオプリセットがビデオプロファイルに含まれている場合は、すべてのプリセットを MP4 にする必要があるので、**[!UICONTROL アダプティブストリーミング用にエンコーディング]**&#x200B;をオンにすることはできません。
1. 「ビデオエンコーディングプリセット」ヘッダーの下で、プロファイルを構成するビデオエンコーディングプリセットを追加、編集または削除します。

   「基本」タブと「詳細」タブで、各オプションの横にある情報アイコンをタップして、推奨設定と説明を表示します。

1. ページの右上隅にある「保存」をタップし **[!UICONTROL ます]**。

### Deleting a video profile {#deleting-a-video-encoding-profile}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. ビデオプロファイルページで、1 つ以上のビデオプロファイル名のチェックボックスをオンにします。
1. ツールバーの「**[!UICONTROL 削除]**」をタップします。
1. 「**[!UICONTROL OK]**」をタップします。

## ビデオプロファイルのフォルダーへの適用 {#applying-a-video-profile-to-folders}

フォルダーにビデオプロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。つまり、フォルダーに 1 つのビデオプロファイルのみを適用すればよいことになります。そのため、アセットをアップロード、保存、使用およびアーカイブする場所のフォルダー構造については入念に検討してください。

フォルダーに異なるビデオプロファイルを割り当てた場合、新しいプロファイルが以前のプロファイルよりも優先されます。以前に存在していたフォルダーのアセットは変更されずに維持されます。新しいプロファイルは、その後にフォルダーに追加されるアセットに対して適用されます。

プロファイルが割り当てられているフォルダーは、ユーザーインターフェイスでカード名にプロファイルの名前が表示されます。

![chlimage_1-517](assets/chlimage_1-517.png)

ビデオプロファイルは、特定のフォルダーに適用することも、すべてのアセットに全体的に適用することもできます。

後で変更した既存のビデオプロファイルが既に存在するフォルダー内のアセットを再処理できます。 フォルダー [内のアセットの再処理を参照してくださ](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets)い。

### Applying a video profile to specific folders {#applying-video-profiles-to-specific-folders}

**[!UICONTROL ツール]**&#x200B;メニュー内からフォルダーにビデオプロファイルを適用するか、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から適用します。この節では、フォルダーにビデオプロファイルを適用するこれら両方の方法について説明します。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

See also [Reprocessing assets in a folder after you have edited its processing profile](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets).

#### Applying a video profile to folders by way of the Profiles user interface {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. 1 つまたは複数のフォルダーに適用するビデオプロファイルを選択します。
1. Tap **[!UICONTROL Apply Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Apply]**. Folders that have a profile already assigned to it are indicated by the display of the profile&#39;s name directly below the folder name while in **[!UICONTROL Card View]**.
ビデオプロ [ファイル処理ジョブの進行状況を監視できます](#monitoring-the-progress-of-an-encoding-job)。

#### プロパティからフォルダーへのビデオプロファイルの適用 {#applying-video-profiles-to-folders-from-properties}

1. Tap or click the AEM logo and navigate to **[!UICONTROL Assets]** and then to the folder that you want to apply a video profile to.
1. On the folder, tap the check mark to select it and then tap **[!UICONTROL Properties]**.
1. 「**[!UICONTROL ビデオプロファイル]**」タブを選択し、ドロップダウンメニューからプロファイルを選択して、「**[!UICONTROL 保存して閉じる]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

   ![chlimage_1-518ビデオプ](assets/chlimage_1-518.png)ロフ [ァイル処理ジョブの進行状況を監視できます](#monitoring-the-progress-of-an-encoding-job)。

### ビデオプロファイルの全体的な適用 {#applying-a-video-profile-globally}

特定のフォルダーにプロファイルを適用できるだけでなく、グローバルにプロファイルを適用することもできます。これにより、AEM アセットにアップロードされている、すべてのフォルダー内にあるすべてのコンテンツに、選択したプロファイルを適用できます。

フォルダー内のア [セットの再処理も参照してくださ](/help/assets/dynamic-media/processing-profiles.md#reprocessing-assets)い。

**ビデオプロファイルをグローバルに適用するには**、

* Navigate to CRXDE Lite to the following node: `/content/dam/jcr:content`. プロパティを追加し、「す `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` べて保存」 **[!UICONTROL をタップしま]**&#x200B;す。

   ![chlimage_1-519](assets/chlimage_1-519.png)
* ビデオプロ [ファイル処理ジョブの進行状況を監視できます](#monitoring-the-progress-of-an-encoding-job)。

## ビデオプロファイル処理ジョブの進行状況の監視 {#monitoring-the-progress-of-an-encoding-job}

処理インジケーター（またはプログレスバー）が表示され、ビデオプロファイル処理ジョブの進行状況を視覚的に監視できます。

You can also view the `error.log` file to monitor the progress of an encoding job, to see if encoding is finished, or to see any job errors. The `error.log` is found in the `logs` folder where your instance of AEM is installed.

## フォルダーからのビデオプロファイルの削除 {#removing-a-video-profile-from-folders}

フォルダーからビデオプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

You can remove a video profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from the **[!UICONTROL Folder Settings]**. This section describes how to remove video profiles from folders both ways.

### Removing a video profile from folders by way of the Profiles user interface {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]**.
1. 1 つまたは複数のフォルダーから削除するビデオプロファイルを選択します。
1. Tap **[!UICONTROL Remove Profile from Folders]** and select the folder or multiple folders you want use to remove the profile from and tap **[!UICONTROL Remove]**.

   名前がフォルダー名の下に表示されなくなっていることで、ビデオプロファイルがフォルダーに適用されていないことを確認できます。

### Removing a video profile from folders by way of Properties {#removing-video-profiles-from-folders-by-way-of-properties}

1. Tap or click the AEM logo and navigate to **[!UICONTROL Assets]** and then to the folder that you want to remove a video profile from.
1. On the folder, tap or click the check mark to select it and then tap or click **Properties]**.
1. 「**[!UICONTROL ビデオプロファイル]**」タブを選択し、ドロップダウンメニューから「**[!UICONTROL なし]**」を選択して、「**[!UICONTROL 保存して閉じる]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

