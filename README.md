# Lab 6: Association Rule Mining with Apriori and FP-Growth

**Course:** Advanced Big Data and Data Mining (MSCS-634-B01)  
**Author:** Rajiv  
**Date:** April 10, 2026

---

## Purpose

This lab explores **association rule mining** using two classic algorithms — **Apriori** and **FP-Growth** — applied to real-world transactional retail data. The goal is to discover meaningful purchasing patterns, generate actionable association rules, and compare the efficiency of both algorithms.

---

## Dataset

**Online Retail Dataset** — UCI Machine Learning Repository  
- ~540,000 transactions from a UK-based online retailer (2010–2011)  
- Filtered to **United Kingdom** transactions for computational efficiency  
- Columns used: `InvoiceNo`, `Description`, `Quantity`, `CustomerID`

---

## Lab Structure

| Step | Description |
|------|-------------|
| **Step 1** | Data loading, cleaning, basket encoding, frequency visualizations |
| **Step 2** | Frequent itemset mining with Apriori (`min_support = 0.05`) |
| **Step 3** | Frequent itemset mining with FP-Growth (same threshold) |
| **Step 4** | Association rule generation (`min_confidence = 0.5`) with support/confidence/lift analysis |
| **Step 5** | Algorithmic comparison: runtime, itemset counts, rule quality |

---

## Key Insights

1. **FP-Growth is significantly faster** than Apriori on this dataset while producing identical frequent itemsets and association rules. FP-Growth avoids expensive candidate generation by using a compressed FP-tree structure.

2. **Top association rules** revealed strong product bundles in the decorative/gift items category — items with **lift > 5** indicate that customers buying one item are 5× more likely to also buy the associated item compared to random chance.

3. **High-confidence rules (confidence > 0.7)** are directly actionable for e-commerce recommendation engines: when a customer adds the antecedent to their cart, the consequent should be prominently recommended.

4. **Co-occurrence heatmap** highlighted tight clusters among seasonal/gift items, suggesting a distinct customer segment that purchases gift sets, particularly around the holiday season.

5. **Support threshold of 0.05** balanced discovery of meaningful patterns against noise — lower thresholds produced thousands of weak/spurious rules.

---

## Visualizations Produced

| File | Description |
|------|-------------|
| `top20_items.png` | Barplot of top 20 most purchased items |
| `cooccurrence_heatmap.png` | Heatmap of item co-occurrence for top 15 items |
| `apriori_top20_itemsets.png` | Top 20 frequent itemsets by support — Apriori |
| `fpgrowth_top20_itemsets.png` | Top 20 frequent itemsets by support — FP-Growth |
| `confidence_vs_lift.png` | Scatter plot of confidence vs lift for both algorithms |
| `top15_rules_lift.png` | Top 15 rules by lift with confidence and support annotations |
| `runtime_comparison.png` | Bar chart comparing algorithm execution time |
| `lift_distribution.png` | Distribution of lift values across all rules |

---

## Challenges and Decisions

- **Dataset size**: The full dataset (~540K rows) was filtered to UK transactions to reduce the basket matrix size while retaining the most representative segment.
- **Support threshold tuning**: Initial `min_support = 0.01` generated too many low-quality itemsets. Raised to `0.05` to focus on pratically significant patterns.
- **Sparse matrix memory**: Used binary encoding with `mlxtend`'s `apriori`/`fpgrowth` functions which handle sparse boolean DataFrames efficiently.
- **Rule interpretability**: Itemset labels were truncated for visualization readability while keeping the full labels in the notebook output.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
mlxtend
openpyxl
```

Install with:
```bash
pip install pandas numpy matplotlib seaborn mlxtend openpyxl
```

---

## Files

```
Lab 6/
├── Lab6_Association_Rule_Mining.ipynb   # Main Jupyter Notebook
└── README.md                            # This file
```
# Lab-6
