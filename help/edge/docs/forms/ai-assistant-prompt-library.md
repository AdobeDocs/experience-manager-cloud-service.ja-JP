---
title: Forms Experience Builder - プロンプトライブラリ
description: Forms Management UI、アダプティブフォームエディター、ユニバーサルエディターで、AI を利用してフォームを作成する実証済みのプロンプトパターンと例のコレクション。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 39%

---


# Forms Experience Builder - プロンプトライブラリ

Forms Experience Builder 用に最適化された再利用可能なプロンプトパターンと例のコレクション。この効率化されたライブラリは、LLM を活用したスマートフィールドとブランドの一貫性のサポートが強化されている、ゼロから作成および読み込みと変換という 2 つのコア作成方法に焦点を当てています。

>[!NOTE]
>
> Forms Experience Builder は、早期導入プログラムで利用できます。勤務先のアドレスから `aem-forms-ea@adobe.com` にメールを送信して、アクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このプロンプトライブラリは現在製品に対してテスト中であり、更新および改訂される可能性があります。早期導入プログラム中に Forms Experience Builder が進化し続けると、プロンプト、例、ベストプラクティスが変わる可能性があります。

## このプロンプトライブラリの使用

このライブラリは、一般的なフォーム作成シナリオに再利用可能なプロンプトパターンを提供します。包括的なベストプラクティスについて詳しくは、[Forms Experience Builder 入門ガイド](forms-ai-assistant-getting-started.md#best-practices)を参照してください。

### このライブラリのクイックヒント

- **例から開始** - 提供されたプロンプトをテンプレートとして使用し、ニーズに合わせて調整します
- **2 つの作成方法** - 「ゼロから作成」アプローチまたは「読み込みと変換」アプローチを選択します
- **具体的に指定** - 一般的な例に独自の詳細を追加します
- **徹底的にテスト** - 常に特定の環境で結果を検証します

### ブランドのテンプレートとスタイル

**一貫性のあるフォーム作成のためにブランドアセットを事前に準備：**

- **ブランドテンプレート** – 組織のカラー、フォント、レイアウトパターンを使用して標準化されたフォームテンプレートを準備します
- **スタイルガイドライン** - Forms Experience Builder で適用できる一貫したフィールドのスタイル、ボタンのデザインおよび間隔標準を定義します
- **コンポーネントライブラリ** – 開発チームと協力して、ブランドアイデンティティに一致する再利用可能なフォームコンポーネントを準備します
- **ビジュアルアセット** - フォーム統合用のロゴ、アイコン、背景要素を準備します

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## 漸進型開発の例

これらの例では、最初は簡単なものから始めて徐々に複雑なものを追加し、段階的にフォームを作成する方法を示しています。

### 例 1：連絡先フォームを漸進的に作成する

**手順 1 - シンプルに開始：**

     名前、メール、メッセージのフィールドを含む基本的な連絡先フォームの作成 

**手順 2 - 検証の追加：**

     適切な検証を使用して、@name および@email 必須フィールドを設定する 

**手順 3 - ユーザーエクスペリエンスの向上：**

     プレースホルダーテキストを追加します：「Your full name」、「your.email@company.com」@email@message 「Tell us how we help （お手伝いできることをお聞かせください）」を@name リックします 

**手順 4 – 高度な機能の追加：**

     「一般的な質問」、「サポート依頼」、「セールスに関する質問」、「パートナーシップ」などのオプションを含むドロップダウン照会タイプを追加 

**手順 5 – 条件付きロジックの実装：**

    /create-rule が「Support Request」@urgencyLevel 等しい場合にのみ、ドロップダウン（低、Medium、高）@inquiryType 表示する 

### 例 2：登録フォームの段階的作成

**手順 1 - 基本構造：**

     個人情報パネルを使用したユーザー登録フォームの作成 

**手順 2 - 必要なフィールドの追加：**

    @firstName、@lastName、@email、@phoneNumber のフィールドを適切な検証で追加 

**手順 3 - ビジネスロジックの追加：**

     ルールを作成します：@age が 18 未満の場合は、親/ガーディアン情報セクションを表示します 

**手順 4 - 環境設定を使用した機能強化：**

    @newsletterSubscription、@marketingConsent、@termsAccepted を含む環境設定パネルの追加 

**手順 5 - ファイルのアップロードの追加：**

     サイズ制限が 5 MB の@profilePicture ーザーにはファイルアップロードフィールドを含める 

## フォームの作成と管理

**用途：**&#x200B;新規フォームを作成する必要がある場合や、既存のフォームを変更する必要がある場合。

**使用方法：**「ゼロから作成」または「読み込みと変換」の 2 つの方法のいずれかを選択します（[入門ガイド](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)を参照）。

**プロンプトの例 - フォームの簡単な作成：**

     次の情報を使用して、お客様のフィードバックフォームを作成します。
     – 製品評価（1～5 つ星） 
     – 詳細なフィードバックのコメントフィールド 
     – お客様のメール（オプション） 
    - メール通知に送信 

**プロンプトの例 - 複雑なフォームの作成：**

    
    
    **個人情報セクション：**
     – 姓名（名、ミドルネーム、姓） 
     – 生年月日（年齢確認） 
     – 連絡先情報（E メール、電話、住所） 
     – 緊急連絡先の詳細 
    
    **雇用情報：**
     – 職階および部署の選択 
     – 営業日の確認とともに開始日 
     – 機密保持の通知とともに給与情報 
     – 報告構造 
    
    **文書のアップロード：**
     – 履歴書のアップロード（PDF、DOC、DOCX） 
    -ID 確認書類 
     – 税金フォームおよび銀行情報 
     – 署名済み雇用契約 
    
    **環境設定：**
     – 費用計算ツールによる福利厚生選択 
     – 作業スケジュールの環境設定 
     – 研修要件 
     
    
     
     
     
     
     
     
    
     
     
     
     
     
 – 機器のニーズ&#x200B;**&#x200B;**&#x200B;検証ルール：**電話の番号形式検証は – Age must be 18or older の書類 – All required documents must be uploaded 必須 documents- Terms and conditions must be newer employee への電子メールの送信 – Employee record システム – スケジュールの向きの会議
**フォーム管理プロンプト：**

     このPDF アプリケーション フォームをインポートして、検証機能を強化したアダプティブ フォームに変換します 
    
     既存の連絡先フォームを更新して、ソーシャル メディア ハンドルおよび推奨の連絡方法を組み込みます 
    
     登録フォームを、個人情報、環境設定、確認の 3 ステップ ウィザードに再編成し 
 す。

## フィールドの管理と設定

**用途：**&#x200B;フォームフィールドを追加、変更、設定する必要がある場合。

**使用方法：**&#x200B;フィールドのタイプ、検証ルールおよびユーザーエクスペリエンスの期待について、具体的に指定します。

**プロンプトの例 - 基本フィールドの追加：**

     「会社名」のテキスト入力フィールドを「会社名を入力」プレースホルダーと共に追加する 

**プロンプトの例 - 高度なフィールドの設定：**

     次を含む包括的な住所セクションを追加します。
    
    **&#x200B;**&#x200B;番地：**
     – 住所 1 行目（必須、最大 100 文字） 
     – 住所 2 行目（オプション、最大 100 文字） 
     – 市区町村（必須、共通の市区町村を含むドロップダウン） 
     – 都道府県（必須、ドロップダウン） 
     – 郵便番号（必須、デフォルトで「米国」に設定） 
     – 国（必須、「州」選択と一致する） 
    
     
     – 住所 1 を空にすることはできません 
     
     – 選択に有効市区町村有効な有効な市区町村状態 
    
    **ユーザーエクスペリエンス：**
     – 住所フィールドのオートコンプリート 
    - ラベルとヘルプテキストのクリア 
    - モバイルに適した入力フィールド 
    - アクセシビリティコンプライアンス 

**フィールド設定プロンプト：**

     リアルタイム@email 検証およびカスタムエラーメッセージでフィールドを必須にする 
    
     米国、カナダ、英国、ドイツ、フランスおよび「その他」のオプションを使用した@country@phoneNumber ーザー用のドロップダウンを追加する 
    
     形式（XXX） XXX-XXXX および検証を使用してフィールドを設定する 
    
    PDFおよび DOC の制限を使用した@resume ーザー用のファイルアップロードフィールドを追加する（最大 5MB まで） 

## LLM 拡張スマートフィールド

**用途：** AI のナレッジベースを活用する事前入力済みオプションを持つフィールドが必要な場合。

**使用方法：**&#x200B;包括的なデータセットが必要なフィールドをリクエスト - AI は、組み込みの知識を使用してオプションを自動的に入力できます。

### 地理的と場所フィールド

**空港と輸送機関：**

     すべての主要な国際空港を含む出発空港のドロップダウンを追加 
    IATA コードとフルネームを含む到着空港フィールドを追加 
     ユーザーの場所に最も近い空港のフィールドを作成 
     ヨーロッパ都市用の鉄道駅の選択を追加 

**行政区域：**

     略語を含む米国の州の完全なリストを追加 
    ISO コードとフルネームを含む国ドロップダウンを作成 
     タイムゾーンを含む世界の主要都市のフィールドを追加 
     カナダの都道府県および地域のドロップダウンを含める 
     英国の郡と郵便地域用のフィールドを追加 

### ビジネスと業界データ

**会社分類：**

    NAICS コードを使用して業界を分類するフィールドを追加 
     ビジネスタイプ（LLC、Corporation、Partnership など）のドロップダウンを作成）
     会社サイズ カテゴリ （スタートアップ、SME、エンタープライズ）のフィールドを追加 
     大規模組織の部門選択を含める 
     プロフェッショナル サービス タイプのフィールドを追加する 

**プロフェッショナルな分類：**

     業界で共通の役割を持つ役職名のフィールドを追加 
     フィールド別の専門職認定のドロップダウンを作成 
     学位タイプの教育レベルを含める 
     長年の経験範囲のフィールドを追加 
     プログラミング言語およびフレームワークの選択項目を作成 

### 標準と規制

**財務と法務：**

     記号および為替レートを含む通貨コードのフィールドを追加 
     国別の税金 ID タイプのドロップダウンを作成 
     法的文書タイプのフィールドを含める 
     セキュリティ機能を含む支払方法オプションを追加 
     国別の銀行機関用の選択項目を作成 

**技術標準：**

     拡張子を含むファイル形式タイプのドロップダウンを追加します 
     ネットワークプロトコルオプションを含めます 
     データベースタイプとバージョンのフィールドを追加します 
    API 認証方法の選択項目を作成します 

### ヘルスケアと医療

**医療分類：**

     医療専門分野のフィールドを追加 
     一般名の一般的な薬のドロップダウンを作成 
     保険業者の種類のフィールドを含める 
     医療緊急連絡先の関係の選択を追加 
     食事制限およびアレルギーのフィールドを作成する 

### 時間とカレンダーインテリジェンス

**日付と時刻フィールド：**

     タイムゾーンの処理と共に業務時間のフィールドを追加 
     国別の祝日のドロップダウンを作成 
     日付範囲を含む季節ごとのオプションを含める 
     空き時間付きの会議室予約用のフィールドを追加 
     定期的な会議パターンの選択を作成する 

### 製品とサービスカテゴリ

**e コマース分類：**

     サブカテゴリを含む製品カテゴリのフィールドを追加 
     配信予測を含む発送方法のドロップダウンを作成 
     返品ポリシーオプションのフィールドを含める 
     顧客の優先度レベルの選択を追加 
     サブスクリプション請求サイクルのフィールドを作成 

**スマートフィールドプロンプトの例：**

     「IATA コードや都市名を含む、世界中のすべての主要空港を含む出発空港フィールドを追加する」 
    
     「技術サブカテゴリを含む標準 NAICS 分類を使用して包括的な業界フィールドを作成する」 
    
     「選択した職種に基づいて適応する専門認定ドロップダウンを含める」 
    
     「選択した国に基づいて書式設定する国際電話番号フィールドを追加する」 
    
     「国およびランキング別の主要機関をの大学選択フィールドを作成」 

## ルールの作成とビジネスロジック

**用途：**&#x200B;条件付きロジック、検証ルールまたはビジネスプロセスを実装する必要がある場合。

**使用方法：**&#x200B;条件とアクションを指定して、ビジネスロジックを明確に記述します。

**プロンプトの例 - シンプルな条件付きロジック：**

    @maritalStatus が「既婚」の場合にのみ、@spouseInformation パネルを表示するルールを作成する

**プロンプトの例 - 複雑なビジネスルール：**

     包括的なローン申し込み検証の実装：
    
    **所得検証：**
    -@annualIncome@annualIncome @age が 30000 未満の場合：
     – 警告メッセージを表示：「要求されたローン金額に対する収入が不十分な場合があります」 
     – 収入に関する追加ドキュメントが必要です」 
     – 表示メッセージ：「収入が 100000:
     – 有料サービスのオプションを表示します 
     – 優先処理チェックボックスを有効にします 
    
    
    **年齢に基づく検証：**
     
     – 親/ガーディアン情報セクションを表示 
     
     – 親署名ボタンを変更するレビュー用に送信 
    -@age が 65 歳以上の場合：
    - シニア割引オプションを表示 
    - アクセシビリティ環境設定セクションを追加 

**ルール固有のプロンプト：**

以前の回答に基づいて追加の質問が表示される      既婚**または「国内パートナーシップ」 
    
     追加&#x200B;**プログレッシブディスクロージャー**&#x200B;と等しい場合にのみ@spouseInformation@maritalStatus のパネルを表示する**表示ルールを作成します。 基本情報から開始して、関連するフォローアップを表示します 
    
    **スマートデフォルト**&#x200B;を実装し、選択@country 関連フィールドを自動設定します。 手動による上書きを許可する 

## データ統合と送信

**用途：**&#x200B;バックエンドシステム、データベース、または外部サービスにフォームを接続する必要がある場合。

**使用方法：**&#x200B;基本的な送信設定から始めて、段階的に統合を追加します。統合タイプ、データ形式要件、エラー処理の環境設定を指定します。

**プロンプトの例 - 基本送信から開始：**

    @applicationForm:
    
    **プライマリ送信：**
    - フォームデータを REST エンドポイントに送信：&#39;/api/v1/applications&#39;
    - データを JSON としてフォーマット 
     – 成功メッセージを表示：「Application submitted successfully」 
     – 送信に失敗した場合にエラーメッセージを表示：「Submission failed, please retry」 

**次に、二次的なアクションを段階的に追加：**

    @applicationForm へのメール通知の追加：確認メールを@email アドレスに送信し、アプリケーションの参照番号を設定します 
    
    @applicationForm に CRM 統合を追加します：@firstName、@lastName、@email を含む新しいリードレコードを作成し、ステータスを「新しいアプリケーション」に設定し 
 す。
**プロンプトの例 - 標準的なマルチチャネル送信：**

     複数のデータ送信先でのフォーム送信の設定：
    
    **プライマリ送信：**
    - REST エンドポイントへのフォームデータの送信：&#39;/api/v1/applications&#39;
    - API キーを使用して認証ヘッダーを含める 
    - アドレスと社員向けにネストされたオブジェクトで JSON としてデータをフォーマットする 
     – ありがとうメッセージを表示して成功のレスポンス（201）を処理する 
    
    **セカンダリアクション：**
     
    -@email アドレスにトリガーメールををを送信 
     – 承認プロセスのワークフロー 
    - リード「新規」 アプリケーション&quot;
    
    **エラー処理：**
    - プライマリ送信に失敗した場合は、データをローカルに保存して再試行します 
    - ユーザーにとってわかりやすいエラーメッセージを表示します：「送信が一時的に利用できません」 
    - フォームデータをバックアップとしてダウンロードするオプションを提供します 
     – 送信に失敗した場合の管理者チームへのアラートメールの送信 
    
    **成功フロー：**
    - アプリケーション参照番号を含む確認ページへのリダイレクト 
     – 次の手順メールを表示する 
     
&#x200B;-
**統合固有のプロンプト：**

     このフォームを&#x200B;**CRM システム**&#x200B;に接続して、新しいリードを作成します。 フォームの送信時に、@firstName を FirstName に、@email を Email に、LeadSource を「Web Form」に、Status を「New」 
    
     設定&#x200B;**ワークフロートリガー**&#x200B;にマッピングします。 Manager notification
    
    Configure **database integration**&#x200B;を使用して、すべてのフォームデータおよびトリガー承認ワークフローを渡し、フォーム送信をレコードとして保存します。 アップロードされたドキュメントを含む各送信用の新しいフォルダーを作成する 

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## コマンドリファレンス

### 必須コマンド

| コマンド | ベストユースケース | 例 |
|---------|---------------|---------|
| `/create-form` | 新しいフォームの開始 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | ページへのフォームの追加 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | フォーム構造の変更 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | フィールドプロパティの変更 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 動的動作の追加 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | フォームセクションの整理 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | デザインの変換 | `/add-panel from uploaded form image with field recognition` |
| `/help` | ヘルプ | `/help how to implement multi-step validation?` |

### フィールド参照

`@fieldName` 構文を使用して、プロンプト内の既存のフィールドを参照します。

- `@email` - 参照メールフィールド
- `@firstName` - 参照名フィールド
- `@maritalStatus` - 参照婚姻ステータスフィールド

### コンポーネントタイプ

**入力コンポーネント：**

- `text`、`email`、`number`、`tel`、`date`、`checkbox`、`radio`、、`dropdown`、`file`、`textarea`

**コンテナコンポーネント：**

- `fieldset`、`panel`、`repeatable`、`wizard`

### コンポーネントプロパティ

**ユニバーサルプロパティ（すべてのコンポーネント）：**

- **Type**：コンポーネントタイプ
- **Name**：フォーム送信用のフィールド ID
- **Labe**：フィールドのテキストを表示します
- **Description**：フィールドのヘルプテキスト
- **Visible**：最初の表示のブール値
- **Mandatory**：必須フィールドのブール値

**入力フィールドプロパティ：**

- **Value**：デフォルト/初期値
- **Placeholder**：入力フィールドのヒントテキスト
- **Min**：最小値（数値/日付）
- **Max**：最大値（数値/日付）

**ファイルアップロードプロパティ：**

- **Accept**：ファイル形式（.pdf、.doc、.docx、.jpg、.png など）
- **Multiple**：複数のファイルを選択する場合はブール値

**選択コントロールプロパティ：**

- **Options**：ドロップダウンの選択肢（コンマ区切りリスト）
- **Checked**：チェックボックス/ラジオのデフォルト選択

**コンテナプロパティ：**

- **Fieldset**：グループ化に関連するフィールド
- **Repeatable**：繰り返し可能なセクションのブール値

**詳細プロパティ：**

- **Visible Expression**：条件付き表示の数式（=数式）
- **Value Expression**：計算値の数式（=数式）

### 統合コマンド

**送信アクション：**

- メール通知
- REST API 送信
- クラウドストレージ（Azure、SharePoint）
- ワークフロー自動化（Power Automate、Workfront Fusion）
- マーケティングプラットフォーム（Marketo）
- CRM 統合

### プロンプト構文ガイドライン

- **フィールド参照**：既存のフィールドに `@fieldName` を使用します
- **コマンド**：特定のアクションに `/command` を使用します
- **自然言語**：要件を明確かつ具体的に記述します

### 検証チェックリスト

包括的なベストプラクティスと検証のガイドラインについて詳しくは、[Forms Experience Builder 入門ガイド](forms-ai-assistant-getting-started.md#best-practices)を参照してください。

*このプロンプトライブラリは、ユーザーフィードバックと新しい Forms Experience Builder 機能に基づいて継続的に更新されます。最新の機能と例について詳しくは、[AEM Forms のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja)を参照してください。*
