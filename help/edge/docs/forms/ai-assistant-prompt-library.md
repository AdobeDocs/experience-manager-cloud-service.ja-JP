---
title: Forms Experience Builder - プロンプトライブラリ
description: Forms Management UI、アダプティブフォームエディター、ユニバーサルエディターで、AI を利用してフォームを作成するための実証済みのプロンプトパターンと例のコレクション。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---


# Forms Experience Builder - プロンプトライブラリ

Forms Experience Builder 用に最適化された、再利用可能なプロンプトパターンと例のコレクション。 この合理化されたライブラリは、2 つのコア作成方法に焦点を当てています。ゼロからの作成および読み込みと変換。LLM を利用したスマートフィールドの強化サポートおよびブランド一貫性を備えています。

>[!NOTE]
>
> Forms Experience Builder は、早期導入プログラムで利用できます。 勤務先のアドレスから `aem-forms-ea@adobe.com` にメールを送信して、アクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このプロンプトライブラリは現在製品に対してテスト中であり、更新および改訂される可能性があります。Forms Experience Builder は、早期導入プログラム中に進化し続けるため、プロンプト、例、ベストプラクティスが変わる可能性があります。

## このプロンプトライブラリの使用

このライブラリは、一般的なフォーム作成シナリオに対して、再利用可能なプロンプトパターンを提供します。 包括的なベストプラクティスについては、[Forms Experience Builder 入門ガイド ](forms-ai-assistant-getting-started.md#best-practices) を参照してください。

### このライブラリのクイックヒント

- **例から開始** – 提供されたプロンプトをテンプレートとして使用し、ニーズに合わせて調整します
- **2 つの作成方法** - 「ゼロから作成」または「インポートして変換」アプローチを選択します。
- **具体的** – 一般的な例に独自の詳細を追加します。
- **徹底的にテスト** – 常に特定の環境で結果を検証します

### ブランドのテンプレートとスタイル

**一貫したフォーム作成のために、事前にブランドアセットを準備：**

- **ブランドテンプレート** – 組織のカラー、フォント、レイアウトパターンを使用して標準化されたフォームテンプレートを作成します
- **スタイルガイドライン** – 一貫したフィールドのスタイル設定、ボタンのデザイン、間隔の標準を定義します
- **コンポーネントライブラリ** - ブランド ID に一致する、再利用可能なフォームコンポーネントを作成します
- **ビジュアルAssets** - フォームを統合するためのロゴ、アイコン、背景要素を準備します

**ブランドテンプレートプロンプトの例：**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**カスタムコンポーネント**：カスタムブランド要素を実装する前に、組織固有のコンポーネントの使用とそのForms Experience Builder との互換性について開発チームに確認してください。

>[!NOTE]
>
> このプロンプトライブラリが更新され、合理化されたForms Experience Builder 機能が反映されました。 例に示した一部の高度な統合およびテスト機能には、追加の設定が必要な場合があります。



## 漸進型開発の例

これらの例では、最初は簡単なものから始めて徐々に複雑なものを追加し、段階的にフォームを作成する方法を示しています。

### 例 1：連絡先フォームを漸進的に作成する

**手順 1 - シンプルに開始：**

```
Create a basic contact form with name, email, and message fields
```

**手順 2 - 検証の追加：**

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

### 例 2：登録フォームの段階的作成

**手順 1 - 基本構造：**

```
Create a user registration form with personal information panel
```

**手順 2 – 必須フィールドを追加：**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**手順 3 - ビジネスロジックの追加：**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**手順 4 – 環境設定を使用した機能強化：**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**手順 5 - ファイルのアップロードの追加：**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## フォームの作成と管理

**用途：** 新しいフォームを作成する必要がある場合や、既存のフォームを変更する必要がある場合。

**使用方法：** 2 つの方法から 1 つ選択します。「ゼロから作成」または「読み込んで変換」（『 [ はじめる前に ](forms-ai-assistant-getting-started.md#two-ways-to-create-forms) を参照）。

**プロンプトの例 – フォームの簡単な作成：**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**プロンプトの例 – 複雑なフォームの作成：**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**フォーム管理プロンプト：**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## フィールド管理と設定

**用途：** フォームフィールドを追加、変更、設定する必要がある場合。

**使用方法：** フィールドタイプ、検証ルールおよびユーザーエクスペリエンスの要件に関して具体的に説明します。

**プロンプトの例 – 基本フィールドの追加：**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**プロンプトの例 – 詳細フィールドの設定：**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**フィールド設定プロンプト：**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## LLM 拡張スマートフィールド

**使用するタイミング：** AI のナレッジベースを活用するオプションが事前入力されたフィールドが必要な場合。

**使用方法：** 包括的なデータセットが必要なリクエストフィールド - AI は、組み込みの知識を使用してオプションを自動的に入力できます。

### 「地理的および場所」フィールド

**空港・輸送機関：**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**行政区域：**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### ビジネスおよび業界データ

**会社の分類：**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**プロフェッショナルな分類：**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### 標準と規制

**財務および法務：**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**技術基準：**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### ヘルスケア・医療

**医療分類：**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### 時間とカレンダーインテリジェンス

**日付および時刻フィールド：**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### 製品およびサービスのカテゴリ

**E コマース分類：**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**スマートフィールドプロンプトの例：**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## ルールの作成とビジネスロジック

**用途：** 条件付きロジック、検証ルールまたはビジネスプロセスを実装する必要がある場合。

**使用方法：** 条件とアクションを指定して、ビジネスロジックを明確に説明します。

**プロンプトの例 – 単純な条件付きロジック：**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**プロンプトの例 – 複雑なビジネス・ルール：**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
```

## データ統合と送信

**用途：**&#x200B;バックエンドシステム、データベース、または外部サービスにフォームを接続する必要がある場合。

**使用方法：**&#x200B;基本的な送信設定から始めて、段階的に統合を追加します。統合タイプ、データ形式要件、エラー処理の環境設定を指定します。

**プロンプトの例 - 基本送信から開始：**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**次に、二次的なアクションを段階的に追加：**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**プロンプトの例 – 標準のマルチチャネル送信：**

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
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## 既存のFormsの読み込みと変換

**用途：** 既存のフォーム、ドキュメントまたはデザインを最新のAEM フォームに変換する場合。

**使用方法：** ソースファイルをアップロードし、変換要件を説明します（『 [ 読み込みガイド ](forms-ai-assistant-getting-started.md#2-import-and-convert) を参照）。

**プロンプトの例 - PDF フォームの変換：**

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**デザインの読み込みプロンプト：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
```

## モバイルの最適化と応答性

**用途：**&#x200B;あらゆるデバイスタイプや画面サイズにわたってシームレスにフォームを操作する必要がある場合。

**使用方法：**&#x200B;基本的なモバイル最適化から始めて、高度な機能で強化します。モバイルファーストのアプローチを重視し、ブレークポイントの動作を段階的に指定します。

**プロンプトの例 - 基本的なモバイル最適化から開始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**次に、高度なモバイル機能の追加：**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**プロンプトの例 - 包括的なモバイルファーストの最適化：**

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
```

**モバイル固有のプロンプト：**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## アクセシビリティとコンプライアンス

**使用するタイミング：** フォームがアクセシビリティ標準（WCAG）またはコンプライアンスの要件を満たす必要がある場合。

**使用方法：** 必要なコンプライアンスレベルと、必要な特定のアクセシビリティ機能を指定します。

**プロンプトの例 – 基本アクセシビリティ：**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**プロンプトの例 – 高度なアクセシビリティ：**

```
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
```

**アクセシビリティ固有のプロンプト：**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## パフォーマンスの最適化

**用途：** フォームを素早く読み込み、様々な条件下で適切に実行する必要がある場合。

**使用方法：** パフォーマンス要件と最適化戦略を指定します。

**プロンプトの例 – 基本パフォーマンス：**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**プロンプトの例 – 高度なパフォーマンス：**

```
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
```

**パフォーマンス固有のプロンプト：**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## テストと品質保証

**用途：** 信頼性とユーザー満足度を確保するために包括的なテストが必要な場合。

**使用方法：** テストシナリオ、検証要件および品質指標を指定します。

**プロンプトの例 – 基本テスト：**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**プロンプトの例 – 詳細テスト：**

```
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
```

**テスト固有のプロンプト：**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## トラブルシューティング

Forms Experience Builder の一般的な問題に対するクイックソリューション：

| 問題 | 簡易修正 |
|-------|-----------|
| フォームが送信されない | 送信アクションの設定と検証ルールの確認 |
| 検証エラーが表示されない | フィールド検証設定とエラーメッセージ配置の検証 |
| モバイルレイアウトの問題 | レスポンシブデザイン設定とフィールドサイズのレビュー |
| フィールドが表示されない | 条件付きロジックおよび表示ルールの確認 |
| 読み込み失敗 | ファイル形式の互換性とサイズ制限の検証 |
| 統合エラー | API エンドポイントと認証資格情報の検証 |
| パフォーマンスの問題 | フィールド数を最適化し、不要な検証を削除 |
| アクセシビリティの問題 | フィールドラベル、ARIA 属性、タブ順序の確認 |

**デバッグモードのプロンプト：**

```
Enable debug mode to identify issues with form submission and field validation
```

**エラー分析プロンプト：**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## 高度な分析とインサイト

**用途：** フォームのパフォーマンスとユーザーの行動を理解する必要がある場合。

**使用方法：** 必要な分析要件とインサイトを指定します。

**プロンプトの例 – 基本分析：**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**プロンプトの例 – 詳細分析：**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Analytics 固有のプロンプト：**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## セキュリティとデータ保護

**使用するタイミング：** フォームが機密データを処理し、セキュリティ対策が必要なタイミング。

**使用方法：** セキュリティ要件とデータ保護対策を指定します。

**プロンプトの例 – 基本セキュリティ：**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**プロンプトの例 – 高度なセキュリティ：**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**セキュリティ固有のプロンプト：**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

## コマンドリファレンス

### 基本コマンド

| コマンド | ベストユースケース | 例 |
|---------|---------------|---------|
| `/create-form` | 新しいフォームの開始 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | ページへのフォームの追加 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | フォーム構造の変更 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | フィールドプロパティの変更 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 動的動作の追加 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | フォームセクションの整理 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | デザインの変換 | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | データ処理の設定 | `/configure-submit to CRM and send confirmation email` |
| `/help` | ヘルプ | `/help how to implement multi-step validation?` |

### フィールド参照

`@fieldName` 構文を使用して、プロンプト内の既存のフィールドを参照します。

- `@email` – 参照メールフィールド
- `@firstName` – 参照の名フィールド
- `@maritalStatus` – 参照の配偶者の有無フィールド

### コンポーネントタイプ

**入力コンポーネント：**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**コンテナコンポーネント：**

- `fieldset`、`panel`、`repeatable`、`wizard`

### コンポーネントのプロパティ

**ユニバーサルプロパティ（すべてのコンポーネント）:**

- **タイプ**：コンポーネントの種類
- **Name**：フォーム送信用のフィールド ID
- **Labe**：フィールドのテキストを表示します
- **Description**：フィールドのヘルプテキスト
- **Visible**：最初の表示のブール値
- **Mandatory**：必須フィールドのブール値

**入力フィールドのプロパティ：**

- **Value**：デフォルト/初期値
- **Placeholder**：入力フィールドのヒントテキスト
- **Min**：最小値（数値/日付）
- **Max**：最大値（数値/日付）

**ファイル アップロードのプロパティ：**

- **Accept**：ファイル形式（.pdf、.doc、.docx、.jpg、.png など）
- **Multiple**：複数のファイルを選択する場合はブール値

**選択コントロール プロパティ：**

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
- クラウドストレージ （Azure、SharePoint）
- ワークフローの自動処理（Power Automate、Workfront Fusion）
- マーケティングプラットフォーム（Marketo）
- CRM 統合

### プロンプト構文ガイドライン

- **フィールド参照**：既存のフィールドに `@fieldName` を使用します
- **コマンド**：特定のアクションに `/command` を使用する
- **自然言語**：要件を明確かつ具体的に記述する

### 検証チェックリスト

包括的なベストプラクティスと検証のガイドラインについては、[Forms Experience Builder 入門ガイド ](forms-ai-assistant-getting-started.md#best-practices) を参照してください。

*このプロンプトライブラリは、ユーザーからのフィードバックと新しいForms Experience Builder 機能に基づいて、継続的に更新されています。 最新の機能と例については、[AEM Forms のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja)を参照してください。*
