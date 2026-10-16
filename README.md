# E-Commerce Funnel Analysis — View to Purchase

## Project Overview

This project analyzes e-commerce user behavior using event-level data from January and February 2020. The goal is to understand how users interact with products, identify conversion drop-off points, compare monthly performance, and discover opportunities to improve purchasing behavior.

The project combines exploratory data analysis, funnel analysis, product segmentation, statistical techniques, and data visualization to transform raw event data into actionable business insights.

## Project Objectives

- Build an e-commerce conversion funnel from event-level data.
- Measure user activity across product views, cart additions, and purchases.
- Calculate conversion rates and identify potential drop-off points.
- Compare funnel performance between January and February 2020.
- Analyze conversion performance across product categories and brands.
- Identify products with high views but low purchase counts.
- Detect price outliers using the Interquartile Range (IQR) method.
- Provide data-driven recommendations for conversion optimization.

## Dataset

The project uses two original datasets containing e-commerce events:

- `2020-Jan.csv` — January 2020 event data.
- `2020-Feb.csv` — February 2020 event data.

The combined dataset contains **8,421,434 event records and 10 columns**.

The data includes event types, timestamps, user identifiers, product identifiers, product categories, brands, prices, and user-session information.

The original datasets are stored in the `data/` directory. The `outputs/` directory contains selected analysis results exported as CSV files.

## Tools and Technologies

- **Python** — data analysis and processing
- **Pandas** — data cleaning, manipulation, and aggregation
- **NumPy** — numerical calculations
- **Matplotlib** — data visualization
- **Seaborn** — statistical visualization
- **Jupyter Notebook** — interactive analysis

## Methodology

### 1. Data Preparation

- Loaded the January and February datasets.
- Combined the datasets for analysis.
- Inspected dataset dimensions, data types, and missing values.
- Examined event distributions and prepared the data for further analysis.

### 2. Funnel Analysis

The main customer journey focuses on three stages:

**Product View → Add to Cart → Purchase**

The analysis examines unique users at each stage and calculates:

- **View-to-Cart Rate:** Unique users who added products to their carts divided by unique viewers.
- **Cart-to-Purchase Rate:** Unique purchasers divided by unique users who added products to their carts.
- **View-to-Purchase Rate:** Unique purchasers divided by unique viewers.

A separate sequential funnel summary is also exported to the `outputs/` directory.

### 3. Monthly Performance Comparison

January and February were compared to identify changes in user engagement, purchase activity, and conversion rates.

### 4. Category and Brand Analysis

Product categories and brands were compared to identify differences in purchase volume and conversion performance.

### 5. High-View, Low-Purchase Product Analysis

Products with relatively high view counts but low purchase counts were identified for further investigation.

### 6. Price Outlier Detection

The Interquartile Range (IQR) method was used to identify unusually high or low product prices.

\[
IQR = Q3 - Q1
\]

The outlier boundaries were calculated using:

- Lower bound: \(Q1 - 1.5 \times IQR\)
- Upper bound: \(Q3 + 1.5 \times IQR\)

### 7. Data Visualization

Visualizations were created to communicate funnel performance, monthly trends, and differences across product categories and brands.

## Key Findings

### Event Distribution

| Event Type | Share of Events |
|---|---:|
| View | 47.39% |
| Cart | 27.28% |
| Remove from Cart | 19.32% |
| Purchase | 6.01% |

Product views represent the largest share of recorded events, while purchases account for a smaller proportion.

## Interactive Visualizations

Click the links below to open the charts directly in your browser, with no download required:

| Visualization | Description | Link |
|---|---|---|
| E-Commerce Conversion Funnel | Overall conversion funnel analysis | [Open](https://kerimovaayse80-ui.github.io/E-Commerce-Funnel-Analysis/visual/ecommerce_conversion_funnel.html) |
| Sequential Funnel | Step-by-step (sequential) funnel analysis | [Open](https://kerimovaayse80-ui.github.io/E-Commerce-Funnel-Analysis/visual/sequential_funnel.html) |

> **Note:** The charts are interactive. Hover over them to see exact values. Because the files are large, the first load may take a few seconds.

### Overall Funnel Metrics

| Metric | Result |
|---|---:|
| Unique viewers | 716,987 |
| Unique users adding to cart | 162,035 |
| Unique purchasers | 49,473 |
| View-to-cart rate | 22.60% |
| Cart-to-purchase rate | 30.53% |
| View-to-purchase rate | 6.90% |

These stage-level rates are calculated from independently aggregated unique-user counts and do not necessarily represent a strictly sequential funnel.

### Monthly Performance

| Metric | January 2020 | February 2020 |
|---|---:|---:|
| Unique viewers | 397,775 | 379,246 |
| Unique users adding to cart | 92,653 | 89,269 |
| Unique purchasers | 28,220 | 25,759 |
| View-to-cart rate | 23.29% | 23.54% |
| Cart-to-purchase rate | 30.46% | 28.86% |
| View-to-purchase rate | 7.09% | 6.79% |

The view-to-purchase rate decreased by approximately **0.30 percentage points** from January to February. The cart-to-purchase rate also declined, while the view-to-cart rate increased slightly.

This suggests that the later stages of the purchasing journey deserve further investigation.

### Category Performance

- `apparel.glove` recorded a view-to-purchase rate of 38.91%.
- `accessories.bag` recorded a view-to-purchase rate of 1.43%.

These results highlight differences in observed conversion performance across product categories. Traffic volume and sample size should also be considered when interpreting these rates.

### Brand Performance

The brands with the highest purchase-event counts included:

| Brand | Purchase Events |
|---|---:|
| runail | 45,274 |
| irisk | 31,210 |
| grattol | 21,320 |
| masura | 19,929 |
| ingarden | 10,276 |

Purchase volume and conversion rate measure different aspects of performance and should be evaluated separately.

### Price Outlier Analysis

The IQR analysis produced the following statistics:

- Q1: 1.59
- Q3: 5.56
- IQR: 3.97
- Lower bound: −4.37
- Upper bound: 11.52
- Outlier events: 34,947 (approximately 6.91%)

Flagged prices may represent legitimate products or data-quality issues and should be reviewed before taking action.

## Business Recommendations

1. **Investigate cart abandonment:** Review checkout friction, shipping costs, payment issues, and unexpected fees.
2. **Analyze cart removals:** Identify products or categories with frequent removals and investigate potential pricing or product-information issues.
3. **Monitor monthly conversion trends:** Investigate the February decline alongside traffic sources, product availability, and promotions.
4. **Study high-converting categories:** Explore product selection, pricing, and customer demand in stronger-performing categories.
5. **Evaluate brands using multiple metrics:** Compare purchase counts, conversion rates, traffic, and average order value.
6. **Review high-view, low-purchase products:** Examine product descriptions, pricing, availability, images, and customer feedback.

## Repository Structure

```text
E-Commerce-Funnel-Analysis/
│
├── README.md
├── note.md
├── ecommerce_funnel_analysis.ipynb
│
├── data/
│   ├── 2020-Jan.csv
│   └── 2020-Feb.csv
│
├── outputs/
│   ├── brand_funnel.csv
│   ├── category_funnel.csv
│   ├── high_view_low_purchase.csv
│   ├── monthly_funnel.csv
│   └── sequential_funnel_summary.csv
│
└── visuals/
    └── [your visualization files]
```

## How to Run the Project

1. Clone or download this repository.
2. Install the required Python libraries.
3. Ensure the original CSV datasets are placed in the `data/` directory.
4. Open `ecommerce_funnel_analysis.ipynb` in Jupyter Notebook.
5. Run the notebook cells in order to reproduce the analysis.

Install the main dependencies using:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Make sure the file paths used in the notebook match the repository structure.

## Limitations

- The analysis covers January and February 2020 only.
- Independently calculated unique-user ratios may not represent a strict sequential funnel.
- Event counts and unique-user counts measure different things.
- Observed patterns do not establish causation.
- User journeys may extend beyond the available data period.
- Outlier detection flags unusual prices but does not establish that they are errors.

## Conclusion

This project demonstrates how e-commerce event data can be used to understand user behavior, evaluate conversion performance, and identify potential opportunities for business improvement.

The findings highlight differences across funnel stages, a decline in view-to-purchase conversion in February, variation in category and brand performance, and products that receive views without generating many purchases.

The analysis provides a foundation for further investigation into checkout optimization, product performance, and customer conversion.

