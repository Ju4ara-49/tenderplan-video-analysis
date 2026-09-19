# TenderPlan-derived UX specification for Tender Intelligence Agent

## Status

Derived from the actual 57-frame extraction of the TenderPlan instruction video.
This is an original UX specification for the user's Tender Intelligence Agent, not a copy of TenderPlan.

Evidence pipeline:
- 57 frames extracted from the local source video.
- GitHub Actions OCR reconstruction completed successfully.
- OCR report artifact: `tenderplan-ux-reconstruction`.
- Reconstruction run: 35433236795.
- Commit analyzed: `d28257f7ba99ce17bfdc47aad075c061d8205eba`.

## 1. Product principle

The search interface must help a non-technical user describe a procurement need in progressively more detail without forcing the user to understand every procurement filter.

Three levels are recommended:

1. Quick Search
2. Advanced Search
3. Expert Search

A saved search profile must preserve the complete configuration and be editable later.

## 2. Quick Search

The first screen should contain only the highest-value filters:

- Search phrase / keywords
- Excluded words
- Region
- Minimum price
- Maximum price
- Advance payment
- Bid/application security
- Contract security
- Minimum days remaining before deadline
- Procurement platforms
- Search button

Primary action:

`НАЙТИ ТЕНДЕРЫ`

Secondary action:

`СОХРАНИТЬ ПОИСК`

## 3. Advanced Search

Advanced Search expands the form into logical groups.

### Search logic
- Any keyword
- All keywords
- Exact phrase
- Excluded words
- Search in procurement documentation
- Morphology / word forms
- Proximity where technically supported

### Classification
- OKPD2
- KTRU
- Industry / category
- Procurement type
- Procurement procedure

### Geography
- Region
- Delivery region
- Delivery location

### Customer
- Customer name
- INN
- Customer group
- Excluded customers
- Competitors / reference customers

### Financial
- Initial contract price
- Minimum price
- Maximum price
- Advance
- Bid/application security
- Contract security

### Dates
- Publication date
- Application start
- Application deadline
- Minimum days remaining

## 4. Expert Search

Expert Search exposes the full procurement-domain filter set without hiding advanced conditions.

It must support, where the source data permits:

- Exact procurement placement/procedure type
- Electronic / non-electronic placement
- Procurement law / regulatory regime
- Procurement method
- Advantages / participant preferences
- Special procurement attributes
- Detailed classification filters
- Detailed customer restrictions
- Detailed financial security conditions
- Detailed delivery geography
- Date/time conditions

The UI must clearly distinguish:
- user-entered criteria;
- derived criteria;
- criteria unavailable for a particular platform.

## 5. Saved search profiles

A saved profile has:

- Name
- Description
- Complete filter state
- Enabled platforms
- Created/updated timestamps
- Active/inactive status

Example:

`Запчасти ЖД — СЗФО`

Saved profiles appear in a left-side or top-level navigation area and can be:
- opened;
- duplicated;
- edited;
- disabled;
- deleted;
- executed immediately.

## 6. Results list

The result list should not merely reproduce raw procurement cards.

Every result should expose:

- Tender title
- Platform
- Procurement number
- Customer
- Initial price
- Application deadline
- Days remaining
- Delivery region/location
- Advance
- Bid security
- Contract security
- Matching criteria
- Risk summary
- Direct source link

The interface should show why the tender matched the saved search.

Example:

`Подходит: ключевые слова + ОКПД2 + регион + цена`

and separately:

`Риски: короткий срок / обеспечение заявки / отсутствие аванса`

## 7. Risk Engine integration

Risk Engine must not replace search filtering.

Pipeline:

Search criteria
→ collector results
→ normalization
→ hard filters
→ deduplication
→ Risk Engine
→ AI explanation
→ result presentation.

Hard filters answer:

`Подходит ли тендер под заданные условия?`

Risk Engine answers:

`Насколько рискованно участие?`

AI explains the result in human-readable language.

## 8. Platform-specific availability

The UI must not promise a filter that a platform cannot reliably provide.

Each filter should have one of:

- Supported
- Partially supported
- Derived
- Not available

For unsupported filters, the system must not silently pretend the filter was applied.

## 9. Result explanation

Each tender should provide a compact explanation:

### Почему найден
- matched keyword
- matched exclusion check
- region match
- price match
- classification match
- deadline match

### Что проверить
- customer
- delivery conditions
- advance/payment terms
- bid security
- contract security
- documentation
- deadline

### Risk
Risk Engine output with explicit factors, not an unexplained score alone.

## 10. UX rule

Do not copy TenderPlan's visual design, text layout, branding, colors, or proprietary presentation.

Reuse only generic interaction concepts that are useful:
- progressive disclosure;
- saved search keys/profiles;
- grouped procurement filters;
- expert mode;
- editable saved searches;
- visible filter state.

The Tender Intelligence Agent should have its own visual identity and a clearer explanation of matching and risk.

## 11. Implementation order

Do not implement the entire UI at once.

Phase A:
- Search data model
- Saved search model
- Quick Search UI
- Existing collector/filter integration

Phase B:
- Advanced Search
- classification/customer/geography filters
- platform capability matrix

Phase C:
- Expert Search
- detailed procurement conditions

Phase D:
- Result explanations
- Risk Engine integration
- AI explanation

Phase E:
- saved profiles
- duplicate/edit/disable
- regression tests

## 12. Acceptance criteria

A user must be able to:

1. Enter a procurement need in plain language.
2. Add include/exclude words.
3. Set price limits.
4. Set region.
5. Set advance/security/deadline conditions.
6. Select platforms.
7. Execute the search.
8. Save the configuration.
9. Reopen and edit it.
10. See why each result matched.
11. See separate risk factors.
12. Open the original procurement source.

No filter may be displayed as active unless it is actually enforced by the backend or explicitly marked as derived/partial.

## 13. Important conclusion from the video analysis

The source video confirms that the useful concept is not simply a large search form. The important UX pattern is progressive disclosure: start with a small set of high-value conditions and expose increasingly specialized procurement filters only when the user needs them.

For our product, the differentiator should be the combination:

Search profile
→ multi-platform collection
→ transparent matching
→ deduplication
→ Risk Engine
→ AI explanation
→ actionable tender result.
