# Marketing Campaign Performance Analysis

Analysis of 300,000 social media ad campaign records to identify which channel underperforms — and why — using Python, pandas, and matplotlib.

## Objective

This dataset contains social media ad campaign data across Facebook, Instagram, Pinterest, and Twitter — including spend, impressions, clicks, conversions, ROI, and demographic targeting. The goal was to compare channel performance, identify the underperforming channel, and investigate the cause rather than just report the surface-level number.

## Dataset

- **Source:** [Kaggle — Social Media Advertising Dataset](https://www.kaggle.com/datasets/jsonk11/social-media-advertising-dataset)
- **Size:** 300,000 rows, 16 columns
- **Fields:** Campaign_ID, Target_Audience, Campaign_Goal, Duration, Channel_Used, Conversion_Rate, Acquisition_Cost, ROI, Location, Language, Clicks, Impressions, Engagement_Score, Customer_Segment, Date, Company

## Data Quality Validation

ROI and Engagement_Score both showed evenly-spaced quartiles and hard value caps — a signature of randomly-generated data rather than real business metrics — so both were **excluded**. CTR showed a naturally skewed distribution and was used as the primary metric throughout.

## Key Findings

CTR's distribution showed most campaigns clustered at 30–33%, with a smaller tail dropping as low as 15%. To understand what was driving that tail, campaigns with CTR below 20% were isolated and compared against the overall dataset across five dimensions: Channel_Used, Campaign_Goal, Customer_Segment, Target_Audience, and Location/Language.

- **Pinterest disproportionately drives severe underperformance.** Its overall average CTR (29.2%) is only slightly below other channels (~32%), but it accounts for **38% of all campaigns with CTR below 20%**, despite representing only **25% of total campaigns**.
- **The cause is channel-specific, not audience or goal-related.** Campaign_Goal, Customer_Segment, Target_Audience, Location, and Language showed no meaningful concentration in the low-CTR group — only Channel_Used did.
- **Acquisition_Cost and Conversion_Rate stay flat across channels**, ruling out cost or conversion efficiency as the explanation — the issue is specific to click-through behavior on Pinterest.

**Takeaway:** most Pinterest campaigns perform normally, but the channel carries a meaningfully higher risk of severe underperformance than the other three — worth a targeted creative/targeting review.

## Visualizations

- Average CTR by channel (bar chart)
- Overall campaign share vs. share of low-CTR campaigns, by channel (grouped bar chart) — the core evidence for the Pinterest finding
- Distribution of CTR across all campaigns (histogram) — visual confirmation of the skewed, trustworthy shape referenced in the data quality section

*(See `Marketing_Campaign_Analysis.ipynb` for all charts and full code.)*

## Tools & Libraries

- Python
- pandas
- matplotlib

## How to Run

1. Download the dataset from the Kaggle link above and place the CSV in the same folder as the notebook.
2. Install dependencies: `pip install pandas matplotlib`
3. Open `Marketing_Campaign_Analysis.ipynb` in Jupyter and run all cells.
