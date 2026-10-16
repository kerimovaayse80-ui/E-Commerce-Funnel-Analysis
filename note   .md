# E-Commerce Funnel Analysis – View to Purchase

## 1. Project Overview

### Business Problem

In e-commerce, attracting visitors is only the first step toward generating sales. Users may view products without adding them to their carts, or add products to their carts without completing a purchase. Understanding these behaviors helps businesses identify friction points, improve the customer journey, and make better product and marketing decisions.

This project analyzes e-commerce event data from January and February 2020 to evaluate user activity throughout the shopping journey. It examines conversion rates, compares monthly performance, identifies category and brand differences, detects unusual purchase prices, and highlights products that receive many views but few purchases.

### Objectives

- Combine January and February event datasets.
- Analyze the distribution of e-commerce event types.
- Build a funnel using unique users at the view, cart, and purchase stages.
- Calculate view-to-cart, cart-to-purchase, and view-to-purchase ratios.
- Compare funnel performance between January and February.
- Analyze conversion metrics for the top eight product categories.
- Identify the top ten brands by purchase-event count and evaluate their view-to-purchase ratios.
- Detect purchase-price outliers using the Interquartile Range (IQR) method.
- Explore time from product view to purchase.
- Identify high-view, low-purchase products.
- Develop actionable recommendations for product and growth teams.

**Dataset:** [E-Commerce Events History in Cosmetics Shop – Kaggle](https://www.kaggle.com/datasets/mkechinov/ecommerce-events-history-in-cosmetics-shop)

**Input files:** `2020-Jan.csv`, `2020-Feb.csv`

**Technologies:** Python, pandas, Matplotlib, Seaborn

---

## 2. Dataset Overview

The January and February datasets were combined into a single DataFrame containing **8,421,434 event records and 10 columns**.

The dataset records user interactions with products, including views, cart additions, cart removals, and purchases.

| Column | Description |
|---|---|
| `event_time` | Date and time when the event occurred |
| `event_type` | Type of interaction, such as view, cart, or purchase |
| `product_id` | Unique identifier of the product |
| `category_id` | Product category identifier |
| `category_code` | Product category code or hierarchy |
| `brand` | Product brand |
| `price` | Recorded product price |
| `user_id` | Identifier of the user |
| `user_session` | Identifier of the user's session |
| `month` | Month label used for monthly comparisons |

### Data Preparation

The following preparation steps were performed:

1. Loaded the January and February CSV files.
2. Added a month label to distinguish records from each month.
3. Concatenated both datasets into a single DataFrame.
4. Converted `event_time` to a datetime data type.
5. Inspected the dataset structure, column types, event types, and missing values.
6. Used unique user counts for funnel calculations.
7. Grouped data by category, brand, product, and month for the relevant analyses.

Missing values were particularly common in `category_code`, `brand`, and `user_session`. These missing values can limit category-level, brand-level, and session-level analysis. They should be considered when interpreting results rather than automatically treated as invalid records.

---

## 3. Event Distribution Analysis

The first step was to understand the frequency of each event type across the combined dataset.

| Event type | Number of events | Percentage |
|---|---:|---:|
| View | 3,991,194 | 47.39% |
| Cart | 2,297,017 | 27.28% |
| Remove from cart | 1,627,433 | 19.32% |
| Purchase | 505,790 | 6.01% |

### Interpretation

View events represent the largest share of recorded activity, while purchase events represent a smaller share. This is expected in many e-commerce environments because users can browse multiple products before deciding to buy.

Cart-removal events are also substantial. They may reflect users reconsidering their choices, changing product selections, or removing products before checkout. However, event counts alone cannot determine why a user removed a product.

**Business implication:** Event distribution provides an overview of customer activity, but it should not be confused with user conversion. A single user can generate multiple views, cart events, and purchases.

---

## 4. Funnel Construction and Conversion Analysis

### Funnel Definition

The main funnel consists of three stages:

1. **View:** A user viewed at least one product.
2. **Cart:** A user added at least one product to their cart.
3. **Purchase:** A user completed at least one purchase.

Unique users were counted separately at each stage.

| Funnel stage | Unique users |
|---|---:|
| View | 716,987 |
| Cart | 162,035 |
| Purchase | 49,473 |

### Conversion Rate Formulas

**View-to-cart rate**

\[
\text{View-to-Cart} =
\frac{\text{Unique Cart Users}}{\text{Unique View Users}} \times 100
\]

**Cart-to-purchase rate**

\[
\text{Cart-to-Purchase} =
\frac{\text{Unique Purchase Users}}{\text{Unique Cart Users}} \times 100
\]

**Overall view-to-purchase rate**

\[
\text{View-to-Purchase} =
\frac{\text{Unique Purchase Users}}{\text{Unique View Users}} \times 100
\]

### Results

| Conversion metric | Rate |
|---|---:|
| View → Cart | 22.60% |
| Cart → Purchase | 30.53% |
| View → Purchase | 6.90% |

### Interpretation

The view-to-cart ratio measures how often the view audience is represented among users who added products to a cart. The cart-to-purchase ratio measures the relationship between users with cart activity and users with purchase activity. The overall ratio compares unique purchase users with unique view users.

The overall view-to-purchase ratio is useful as a high-level performance indicator. However, the ratios above are based on independent unique-user counts at each stage.

**Important limitation:** These calculations do not establish that every user completed the stages in sequence or within the same session. A strict sequential funnel requires events to be ordered by timestamp and linked at the user or session level. The results should therefore be interpreted as stage-level ratios, not as a fully validated sequential customer journey.

---

## 5. Category-Level Conversion Analysis

The top eight product categories by view activity were selected for a category-level comparison. For each category, unique users with view, cart, and purchase events were counted, and the same conversion formulas were applied.

### Key Findings

- `apparel.glove` recorded the highest calculated view-to-purchase ratio among the examined categories: **38.91%**.
- `accessories.bag` recorded the lowest calculated view-to-purchase ratio among the examined categories: **1.43%**.

### Interpretation

The difference between category ratios suggests that user behavior varies across product categories. Some categories may attract users who are more likely to purchase, while others may receive more browsing activity without equivalent purchase activity.

Possible explanations include differences in product prices, product availability, customer intent, product-page quality, and the number of products within each category. These explanations are hypotheses for further investigation, not proven causes.

### Recommended Follow-Up

- Compare the number of unique viewers and purchasers behind each category ratio.
- Investigate low-converting categories for pricing, availability, and product-page issues.
- Examine whether high-converting categories share useful merchandising or presentation practices.
- Compare conversion alongside revenue and profit, if those measures are available.
- Avoid reallocating marketing budgets based on conversion percentages alone without checking sample sizes and category value.

---

## 6. Monthly Funnel Comparison

January and February were analyzed separately using the month label. Unique users were counted independently at each stage for each month.

### Monthly Results

| Metric | January | February |
|---|---:|---:|
| Unique users with views | 397,775 | 379,246 |
| Unique users with cart events | 92,653 | 89,269 |
| Unique users with purchase events | 28,220 | 25,759 |
| View → Cart | 23.29% | 23.54% |
| Cart → Purchase | 30.46% | 28.86% |
| View → Purchase | 7.09% | 6.79% |

### Month-over-Month Changes

| Metric | Change from January to February |
|---|---:|
| View → Cart | +0.25 percentage points |
| Cart → Purchase | −1.60 percentage points |
| View → Purchase | −0.30 percentage points |

The overall change was calculated as:

\[
6.79\% - 7.09\% = -0.30 \text{ percentage points}
\]

### Interpretation

The overall view-to-purchase ratio declined from **7.09% in January to 6.79% in February**. Therefore, the overall conversion ratio did not improve in February.

At the same time, the view-to-cart ratio increased slightly. The larger decline occurred in the cart-to-purchase ratio, which decreased by 1.60 percentage points.

This pattern suggests that the transition from cart activity to purchase activity should be investigated first. Possible factors include payment issues, delivery costs, checkout complexity, stock availability, or changes in traffic quality. The available results do not prove which factor, if any, caused the decline.

The analysis covers only two months, so it cannot establish a long-term trend or seasonal pattern.

---

## 7. Brand Performance Analysis

The ten brands with the highest purchase-event counts were identified. Their view-to-purchase ratios were then calculated using unique users with view and purchase events for each brand.

### Leading Brands by Purchase-Event Count

| Brand | Purchase events |
|---|---:|
| runail | 45,274 |
| irisk | 31,210 |
| grattol | 21,320 |
| masura | 19,929 |
| ingarden | 10,276 |

Among the selected top ten brands:

- **Highest calculated view-to-purchase ratio:** `bpw.style` — 22.95%.
- **Lowest calculated view-to-purchase ratio:** `kapous` — 7.14%.

### Interpretation

Purchase volume and conversion efficiency measure different aspects of brand performance. A brand may generate many purchases because it receives substantial traffic, while another brand may convert a larger share of its viewers but have fewer purchases overall.

### Recommended Follow-Up

- Evaluate purchase volume and conversion ratio together.
- Include the number of unique viewers when interpreting brand ratios.
- Compare brands within similar categories or price ranges where possible.
- Investigate whether low-converting brands have product availability, pricing, or product-page issues.
- Avoid concluding that a brand is more profitable based on conversion rate alone.

---

## 8. Purchase-Price Outlier Analysis

The Interquartile Range (IQR) method was applied to prices in purchase events to identify values outside the typical statistical range.

The calculation uses:

\[
IQR = Q3 - Q1
\]

\[
\text{Lower Bound} = Q1 - 1.5 \times IQR
\]

\[
\text{Upper Bound} = Q3 + 1.5 \times IQR
\]

### Results

| Statistic | Value |
|---|---:|
| First quartile (Q1) | $1.59 |
| Third quartile (Q3) | $5.56 |
| Interquartile range (IQR) | $3.97 |
| Lower bound | −$4.37 |
| Upper bound | $11.52 |
| Purchase events outside the bounds | 34,947 |
| Share of purchase events | 6.91% |

### Interpretation

The IQR method identifies statistically unusual prices, but an outlier is not automatically a data error. A high price may reflect a legitimate product or transaction, and the upper bound is a statistical threshold rather than a business rule.

Flagged records should be reviewed before removing or changing them. Negative or implausible prices should be checked against the dataset's definitions and business context.

---

## 9. Bonus Analysis: Time from View to Purchase

A supplementary analysis matched purchase events with available earlier view events.

| Metric | Result |
|---|---:|
| Matched purchase events | 182,151 |
| Median time to purchase | 34.20 minutes |
| Mean time to purchase | 2,068.42 minutes |
| First quartile | 9.65 minutes |
| Third quartile | 714.39 minutes |
| Purchases without a matching prior view in the available data | 323,639 |

### Interpretation

The mean time to purchase is much higher than the median. This indicates a right-skewed distribution: many matched purchases occur relatively quickly, while some have much longer delays.

A purchase without a matching earlier view does not necessarily mean that the customer never viewed the product. The view may have occurred outside the selected date range, or tracking and event matching may be incomplete.

These results should be interpreted in the context of the matching method and observation window. They do not represent a complete customer-level attribution model.

### Business Application

Time-to-purchase analysis can help teams understand how quickly users make decisions and whether certain categories require longer consideration periods. Additional segmentation by product, category, traffic source, or session could provide more actionable results if the data supports it.

---

## 10. Bonus Analysis: High-View, Low-Purchase Products

Products with at least 100 view events and no more than two purchase events were identified as candidates for further investigation.

| Product ID | View events | Purchase events |
|---|---:|---:|
| 5805511 | 1,302 | 2 |
| 5770135 | 1,157 | 2 |
| 5688835 | 1,135 | 1 |
| 27759 | 1,062 | 0 |
| 5394 | 930 | 2 |

### Interpretation

These products received substantial viewing activity but recorded very few purchase events in the selected data.

Possible explanations include uncompetitive pricing, unavailable variants, unclear product descriptions, insufficient product images, delivery constraints, or low purchase intent among visitors. The data alone cannot determine which explanation is correct.

These are event-based counts rather than unique-user conversion rates. Repeated views by the same user can contribute multiple events.

### Recommended Follow-Up

- Check product and variant availability.
- Review prices relative to comparable products.
- Improve product images and descriptions where necessary.
- Make delivery costs and timelines clear.
- Review traffic sources and device behavior.
- Recalculate product conversion using unique users and, where possible, a sequential session-level funnel.

---

## 11. Growth Insights and Recommendations

### Insight 1: Investigate the cart-to-purchase decline

The cart-to-purchase ratio declined from **30.46% in January to 28.86% in February**, while view-to-cart improved slightly.

**Why it matters:** The decline indicates that purchase activity did not keep pace with cart activity. Checkout completion is therefore a strong candidate for further investigation.

**Recommended actions:**
- Review payment failures and checkout error logs.
- Check whether delivery fees or other unexpected costs appear late in checkout.
- Test the checkout experience across mobile and desktop devices.
- Investigate stock availability and delivery restrictions.
- Build a strictly ordered session-level funnel to identify the exact stage where users abandon the process.

### Insight 2: Monitor the full funnel, not only cart additions

View-to-cart increased by 0.25 percentage points, but the overall view-to-purchase ratio fell by 0.30 percentage points.

**Why it matters:** Improving an early funnel stage does not guarantee more completed purchases. Cart additions should not be treated as the final measure of growth success.

**Recommended actions:**
- Report view-to-cart and cart-to-purchase together.
- Track completed purchases alongside cart additions.
- Segment performance by device, traffic source, and category where possible.
- Use consistent metric definitions in monthly reports.

### Insight 3: Use category differences to prioritize investigation

The calculated view-to-purchase ratios varied considerably across the examined categories, from 38.91% for `apparel.glove` to 1.43% for `accessories.bag`.

**Why it matters:** Category differences can reveal opportunities, but percentages may be influenced by category size, prices, and product mix.

**Recommended actions:**
- Validate the number of users behind each category ratio.
- Compare conversion with revenue and margin where available.
- Investigate low-converting categories for stock, pricing, and product-page issues.
- Study high-converting categories for practices worth testing elsewhere.
- Validate findings before changing marketing budgets.

### Insight 4: Separate brand scale from brand efficiency

Purchase-event counts and view-to-purchase ratios provide different perspectives on brand performance.

**Why it matters:** Ranking brands by purchases alone may favor high-traffic brands and overlook brands with stronger conversion ratios.

**Recommended actions:**
- Maintain separate rankings for purchase volume and conversion.
- Include unique viewer counts to provide context for each ratio.
- Compare similar brands within the same category or price range.
- Consider both metrics when evaluating promotions and merchandising.

### Insight 5: Audit products with many views but few purchases

The high-view, low-purchase product list identifies products that attract attention without recording many purchase events.

**Why it matters:** These products may have friction points that prevent interested users from buying, but low purchase activity can also reflect stock, pricing, or traffic quality.

**Recommended actions:**
- Review product images, descriptions, prices, and availability.
- Check delivery options and additional costs.
- Examine traffic sources and device types.
- Verify the pattern with unique-user and session-level conversion metrics before making product decisions.

---

## 12. Visualization Deliverables

The notebook should include the following four required visualizations and save them in the `visuals/` directory.

### 1. Funnel Bar Chart
Displays the number of unique users at the view, cart, and purchase stages. The chart should make the difference in audience size between stages easy to understand.

### 2. Category Conversion Chart
Compares view-to-cart, cart-to-purchase, and view-to-purchase ratios for the top eight categories. Percentage formatting and readable category labels should be used.

### 3. Monthly Conversion Comparison
Compares January and February funnel ratios. The overall view-to-purchase ratio should be clearly highlighted so the monthly change is easy to interpret.

### 4. Top 10 Brands Horizontal Bar Chart
Displays either purchase-event counts or view-to-purchase ratios for the ten leading brands. The chart title and axis labels should clearly identify the selected metric.

All charts should have meaningful titles, axis labels, readable tick labels, and consistent formatting. The files saved in `visuals/` should correspond to the figures presented in the notebook.

---

## 13. Limitations

- Independent unique-user stage ratios do not establish a sequential journey within the same session.
- Missing category, brand, and session values can limit some analyses.
- Event counts and unique-user counts are different measures and should not be mixed.
- IQR outliers are not necessarily incorrect records.
- Time-to-purchase results depend on the matching method and the observation window.
- High-view, low-purchase products are candidates for investigation, not proof of product defects.
- Only January and February are compared, so the analysis cannot establish a long-term seasonal trend.
- The analysis describes observed patterns but does not prove the cause of monthly changes.

## 14. Conclusion

This project combines January and February 2020 e-commerce event data to examine activity at the view, cart, and purchase stages. The calculated overall view-to-purchase ratio declined from **7.09% in January to 6.79% in February**, with a more substantial decline in the cart-to-purchase ratio.

Category and brand comparisons, purchase-price outlier detection, time-to-purchase analysis, and high-view/low-purchase product identification provide additional areas for investigation.

The main recommendation is to investigate checkout completion and validate the observed patterns using a strictly ordered, session-level funnel. These results provide a data-driven starting point for product and growth decisions, while further analysis is needed to confirm causes and measure the impact of any changes.
