---
title: AEM Forms AI アシスタント – プロンプトライブラリ
description: Forms Management UI、アダプティブFormsエディター、ユニバーサルエディターをまたいで、AI を利用してフォームを作成するための実証済みのプロンプトパターンと例を集めました。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# AEM Forms AI アシスタント – プロンプトライブラリ

再利用可能なプロンプトパターンと、一般的なフォーム作成シナリオの例のコレクション。 特定のニーズに合わせて調整できるテンプレートと考えてください。 各セクションでは、特定のユースケースと、それを使用するタイミング、実証済みの例について説明します。

>[!NOTE]
>
> AEM Formsの AI アシスタントは、早期導入プログラムで利用できます。 勤務先のアドレスからmailto:aem-forms-ea@adobe.comにメールを送信して、アクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このプロンプトライブラリは現在製品に対してテスト中であり、更新および改訂される可能性があります。 早期導入プログラム中にAEM Forms用 AI アシスタントが進化し続けると、プロンプト、例、ベストプラクティスが変わる可能性があります。

## 最適な結果を得るためのベストプラクティス

AI アシスタントを最大限に活用するには、次のヒントに留意してください。

### シンプルなビルドから開始し、段階的にビルドする

最初は過度に複雑な複数ステップのリクエストではなく、小さく具体的なコマンド（「名」のテキスト入力の追加など）から始めます。 このアプローチは、精度を確保するのに役立ち、何かが期待どおりに動作しない場合のトラブルシューティングが容易になります。

**シンプルな開始の例：**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**さらにビルドします：**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### AEM Formsの用語の使用

「パネル」、「テキスト入力フィールド」、「チェックボックスグループ」、「送信アクション」、「ルール」などの用語を使用して、アシスタントの理解を深めます。 これにより、AI がAEM Forms コンテキスト内でリクエストを正しく解釈します。

**優先用語：**

- 「テキストボックス」ではなく「テキスト入力フィールド」
- 「チェックボックス」ではなく「チェックボックスグループ」
- 「リストを選択」ではなく「ドロップダウン」
- 「セクション」や「コンテナ」ではなく「パネル」
- 「フォーム送信」ではなく「送信アクション」
- 「論理」や「条件」ではなく「ルール」

### フィールドを明確に参照

既存のフィールドを設定する場合は、@fieldName の表記を使用します（例：「Make @firstName mandatory」）。 これは、特に、多くのフィールドを含む複雑なフォームで、AI が参照しているフィールドを正確に識別するのに役立ちます。

**例：**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### 計画を常に確認する

ユニバーサルエディターでアシスタントが提案した変更については、常に慎重に計画を確認してから、「適用」をクリックしてください。 AI は、計画内容を示します。この情報が期待に沿っていることを確認してください。

### 手動で検証

アシスタントが変更を加えた後は、常にフォームをプレビューおよびテストして、動作が期待どおりに表示されることを確認します。 AI は強力なツールですが、最終的な検証は品質を確保するための鍵です。

**検証チェックリスト：**

- プレビューモードでのフォーム機能のテスト
- 条件付きロジックが正しく機能することを検証
- モバイルの応答性の確認
- フォーム送信のテスト
- アクセシビリティ機能の検証

### 繰り返して調整

最初のプロンプトで正確な結果が得られない場合は、リクエストを言い換えるか、小さな手順に分割してみてください。 AI はコンテキストから学習するので、より具体的な詳細を提供すると結果が向上する場合が多いです。

**イテレーションの例：**

1. 1 回目：「フォームをモバイル対応にする」
2. 改善：「1 列レイアウトで大きなタッチターゲットを使用し、768 px 未満のモバイル画面用のフォームレイアウトを最適化」

### Provide Feedback

組み込みのフィードバックメカニズムを使用して、アシスタントが学習したり改善したりできるようにします。 フィードバックは、すべてのユーザーの AI をより良いものにするのに役立ちます。


## 増分開発の例

これらの例では、シンプルなフォームから徐々に複雑さを増しながら、フォームを順を追って作成する方法を示しています。

### 例 1：連絡先フォームを増分的に作成する

**手順 1 - シンプルなワークフローの開始：**

```
Create a basic contact form with name, email, and message fields
```

**手順 2 – 検証を追加：**

```
Make @name and @email mandatory fields with appropriate validation
```

**手順 3 - ユーザーエクスペリエンスの向上：**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**手順 4 – 高度な機能の追加：**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**手順 5 – 条件付きロジックの実装：**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### 例 2：登録フォームの増分作成

**手順 1 – 基本構造：**

```
Create a user registration form with personal information panel
```

**手順 2 - コアフィールドを追加：**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**手順 3 – 検証を追加：**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**手順 4 - アカウント情報の追加：**

```
Create a new panel "Account Information" with @username and @password fields
```

**手順 5 - セキュリティの強化：**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**手順 6 – 環境設定を追加：**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

この増分的なアプローチにより、次のことができるようになります。

- 問題が発生する前に問題を早期に検出
- 各機能を徹底的にテスト
- ユーザーのフィードバックに基づいて調整を行う
- 開発プロセスをより適切に制御できる

## 新しいFormsの開始

**使用するタイミング：** フォームプロジェクトの開始時。 このプロンプトは、AI が要件を理解し、基盤構造を構築するのに役立ちます。

**使用方法：** 基本構造とコア要件から始めます。 フォームタイプ、ターゲットオーディエンス、および主な目的を指定します。 後続のプロンプトで複雑さを追加します。

**プロンプトの例 – シンプルな文字列の開始：**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**さらにビルドします：**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**代替のシンプルな開始プロンプト：**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## フォームの構造とレイアウト

**用途：** 複雑なフォームを整理する必要がある場合や、レイアウトデザインを改善してユーザーエクスペリエンスを向上させる必要がある場合。

**使用方法：** ユーザージャーニーと情報の論理的なグループ化に焦点を当てます。 レイアウトの環境設定とナビゲーションパターンを指定します。

**プロンプトの例 – 複数ステップのフォーム構造：**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**レイアウト最適化プロンプト：**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## フィールド管理と検証

**使用すべき状況：** 特定の検証ルールおよび動作を使用して、フォームフィールドを追加、変更、拡張する必要がある場合。

**使用方法：** フィールドのタイプ、検証要件およびユーザーエクスペリエンスの期待について、具体的に説明します。 @fieldName 構文を使用して既存のフィールドを参照します。

**プロンプトの例 – フィールドの機能強化：**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**フィールド固有のプロンプト：**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## 条件付きロジックとルール

**用途：** ユーザー入力またはビジネスルールに基づいて動的なフォームの動作が必要な場合。

**使用方法：** 条件と結果のアクションを明確に定義します。 特定のフィールド参照と論理演算子を使用します。

**プロンプトの例 – 複雑な条件付きロジック：**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**ルール固有のプロンプト：**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## データ統合と送信

**用途：** バックエンドシステム、データベース、または外部サービスにフォームを接続する必要がある場合。

**使用方法：** 基本的な送信設定から始めて、さらに統合を追加します。 統合タイプ、データ形式要件およびエラー処理の環境設定を指定します。

**プロンプトの例 – 基本送信から開始：**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**次に、セカンダリのアクションを増分的に追加します：**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**プロンプトの例 – 高度なマルチチャネル送信：**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**統合固有のプロンプト：**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## デザインインポートとコンバージョン

**用途：** 既存のフォームデザイン（PDF、Figma、画像）を機能的なAEM フォームに変換する必要がある場合。

**使用方法：** ソースデザインに関する明確なコンテキストを提供し、必要な変更や機能強化を指定します。

**プロンプトの例 – PDF フォームの変換：**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**設計の読み込みプロンプト：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## モバイルの最適化と応答性

**用途：** あらゆるデバイスタイプや画面サイズにわたってシームレスにフォームを操作する必要がある場合。

**使い方：** 基本的なモバイル最適化から始めて、高度な機能で強化します。 モバイルファーストのアプローチを重視し、ブレークポイントの動作を段階的に指定します。

**プロンプトの例 – 基本的なモバイル最適化で開始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**次に、高度なモバイル機能を追加します。**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**プロンプトの例 – 包括的なモバイルファーストの最適化：**

```
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

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**モバイル固有のシンプルなプロンプト：**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## アクセシビリティとコンプライアンス

**使用するタイミング：** フォームがアクセシビリティ標準（WCAG 2.1 AA）またはコンプライアンス要件を満たす必要がある場合。

**使用方法：** 満たす必要のあるアクセシビリティ要件とコンプライアンス標準を指定します。

**プロンプトの例 – アクセシビリティの実装：**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**コンプライアンス固有のプロンプト：**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## テストと品質のAssurance

**用途：** フォームの機能、ユーザーエクスペリエンス、技術的なパフォーマンスを検証する必要がある場合。

**使用方法：** 検証が必要なテストシナリオ、エッジケースおよび品質条件を指定します。

**プロンプトの例 – 包括的なフォームテスト：**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**テスト固有のプロンプト：**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## 高度な機能と統合

**用途：** AI 支援、高度なワークフロー、複雑な統合などの高度なフォーム機能が必要な場合。

**使用方法：** 高度な機能と統合要件を明確に定義します。

**プロンプトの例 – AI 拡張フォーム：**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**高度な統合プロンプト：**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## トラブルシューティングと最適化

**用途：** フォームのパフォーマンスやユーザーエクスペリエンスの問題、技術的な問題が発生した場合。

**使い方：** 具体的な問題と望ましい結果を明確に説明します。

**プロンプトの例 – パフォーマンスの最適化：**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**トラブルシューティングプロンプト：**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## 環境固有のベストプラクティス

### Forms Management UI

**用途：** フォームの作成および管理の大まかなタスクの場合。

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### アダプティブFormsエディター

**用途：** フォームの設定や複雑なルールの作成について詳しく説明します。

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### ユニバーサルエディター

**用途：** ビジュアルエディット機能を備えたEdge Delivery Services フォームの場合。

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## コマンド リファレンス クイック ガイド

| コマンド | 最適なユースケース | 例 |
|---------|---------------|---------|
| `/create-form` | 新しいフォームの開始 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | ページへのフォームの追加 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | フォーム構造の変更 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | フィールドプロパティの変更 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 動的動作の追加 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | フォームセクションの整理 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | デザインの変換 | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | データ処理の設定 | `/configure-submit to CRM and send confirmation email` |
| `/help` | お問い合わせ | `/help how to implement multi-step validation?` |

## サポートされるコンポーネントのプロパティリファレンス

### ユニバーサルプロパティ（すべてのコンポーネント）

- **タイプ**：コンポーネントタイプ（テキスト、メール、数値、電話、日付、チェックボックス、ラジオ、ドロップダウン、ファイルなど）
- **名前**：フォーム送信用のフィールド ID
- **ラベル**：フィールドのテキストを表示します
- **説明**: フィールドのヘルプテキスト
- **表示**：最初の表示のブール値
- **必須**：必須フィールドのブール値

### 入力フィールドのプロパティ

- **値**：デフォルト/初期値
- **プレースホルダー**：入力フィールドのヒントテキスト
- **Min**：最小値（数値/日付）
- **Max**：最大値（数値/日付用）

### ファイルのアップロードプロパティ

- **許可**：ファイルタイプ（.pdf、.doc、.docx、.jpg、.png など）
- **Multiple**：複数のファイルを選択する場合はブール値

### 選択コントロールのプロパティ

- **オプション**：ドロップダウンの選択肢（コンマ区切りリスト）
- **オン**：チェックボックス/ラジオのデフォルト選択

### コンテナプロパティ

- **Fieldset**：グループ化に関連するフィールド
- **Repeatable**：繰り返し可能なセクションのブール値

### 詳細プロパティ

- **表示式**：条件付き表示の数式（=数式）
- **値式**：計算値の数式（=数式）

## ベストプラクティスのまとめ

### 技術的ガイドライン

- 公式のAEM Forms コンポーネント仕様の **サポートされているプロパティのみを使用**
- フィールド参照（@fieldName）および式（=数式）の **正しい構文に従う**
- 変更のたびに **増分的にテスト** して、問題を早期に発見します
- 後で考えるのではなく、最初から **アクセシビリティのプラン** を立てます
- 設計のあらゆる決定において **モバイルユーザーを考慮**
- 今後のメンテナンスおよびチームの共同作業に備えた **複雑なルールの文書化**

### 戦略的アプローチ

- **ユーザニーズから始める** – 技術的な機能だけでなく、ユーザーが達成する必要があるものに焦点を当てます
- **完了に向けたデザイン** - フォームデザインでの摩擦と認知負荷を最小限に抑える
- **データフローの計画** 早期 – データの処理、保存および使用方法を検討します
- **規模に合わせた構築** – 予想されるユーザー数とデータの増加に対応できるフォームを設計します。
- **プログレッシブ拡張の実装** – 基本機能が機能することを確認してから、高度な機能を追加します

### 回避すべき一般的な落とし穴

- **過度に複雑な初期リクエスト** – 大規模なタスクをより小さく管理しやすいステップに分割する
- **サポートされていないプロパティを使用** AEM Formsの仕様にはない
- 開発プロセスの後半まで **モバイルエクスペリエンスを無視**
- 実際のシナリオとエッジケースでの **ユーザーテストをスキップ**
- **明確で具体的な指示を提供することなく** AI がコンテキストを理解していると仮定
- **アクセシビリティおよびコンプライアンス要件** 忘れる
- 次の手順に進む前に **変更を検証しない**

### 高品質のAssuranceのアプローチ

1. **頻繁にプレビューする** – 重要な変更が行われるたびに、プレビューモードで作業を確認します
2. **テストエッジケース** – 異常な入力、長いテキスト、特殊文字を試します
3. **デバイス間での検証** - モバイル、タブレット、デスクトップでテストします
4. **アクセシビリティの確認** - キーボードナビゲーションとスクリーンリーダーの互換性の確認
5. **パフォーマンステスト** - フォームの迅速な読み込みとスムーズな応答を実現
6. **ユーザー受け入れテスト** - デプロイメント前に、実際のユーザーにフォームをテストしてもらいます。


*このプロンプト ライブラリは、ユーザ フィードバックと新しい AI アシスタント機能に基づいて継続的に更新されます。 最新の機能と例については、[AEM Formsのドキュメント ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja).* を参照してください。
