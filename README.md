# Clickstream Customer Behaviour & Conversion Analytics

**R | Customer Analytics | Statistical Testing | Regression | Sequence Analysis | Markov Chains**

An individual Digital Marketing Analytics project analysing e-commerce clickstream behaviour to understand **review influence, purchase activity and customer journeys**.

The project combines clickstream feed data, product/review metadata and registered-user information. The analysis moves from data preparation and descriptive customer behaviour through statistical inference and regression into user-level journey and sequence analysis.

> **Portfolio note:** The original source dataset is not included in this repository. The R Markdown is structured so the analysis can be reproduced when the three source TSV files are available locally.

## Business questions

1. Which product-review format receives the greatest exposure?
2. Are celebrity recommendations more influential than customer reviews in observed purchasing activity?
3. How do celebrity, video and customer reviews compare with one another?
4. What is the relationship between review exposure and purchase activity?
5. Which pages and navigation sequences characterise customer journeys?
6. How does browsing behaviour differ between buyers and non-buyers and between male and female users?
7. Where could the business intervene to improve customer experience and conversion?

## Data

The project uses three source datasets:

- **Clickstream feed** — user/session identifiers, URLs, timestamps and purchase indicators.
- **Products and reviews** — page/review identifiers used to classify review and product interactions.
- **Registered users** — user-level demographic information.

The analysed sample contains approximately **16,123 unique users**, **5 selling products**, **16 URL types**, and activity from the **first 15 days of March 2012**. Approximately **51.6% of users are recorded as buyers**.

## Analytical workflow

### 1. Data preparation
- Import and validate source files.
- Standardise the user/session identifier.
- Classify raw review/page identifiers into business-facing categories.
- Join clickstream and registered-user data.
- Construct user-level purchase and review-exposure measures.

### 2. Customer behaviour
- Buyer-rate analysis.
- Browsing depth by buyer status.
- Browsing behaviour by gender.
- Most-visited pages.

### 3. Statistical analysis
- Pairwise comparison of review-type conversion proportions.
- User-level regression relating purchase activity to review exposure.
- Interpretation of coefficients as **observational associations**, not causal effects.

### 4. Customer journey analysis
- Reconstruct user-level page sequences using timestamp ordering.
- Examine common sequence patterns.
- Fit a **second-order Markov chain** to model transitions conditional on recent browsing history.
- Use sequence distances and hierarchical clustering to explore journey archetypes.
- Derive journey-level features for purchase-association analysis.

## Selected findings

### Review exposure

| Review type | Approx. sessions |
|---|---:|
| Customer review | 68,074 |
| Video review | 41,974 |
| Celebrity recommendation | 27,592 |

Customer reviews had the highest observed visibility in the sample.

### Review comparisons

The original analysis reported:

- Celebrity vs customer: **z = -145.03, right-tailed p ≈ 1**
- Celebrity vs video: **z = -58.63, right-tailed p ≈ 1**
- Customer vs video: **z = 88.71, p < 0.05**

The results do **not** support the claim that celebrity recommendations outperform customer reviews or video reviews in the tested comparisons. Customer reviews showed the strongest observed relationship among the formats examined.

### Customer journeys

| Segment | Average distinct pages visited |
|---|---:|
| Buyers | ~1.65 |
| Non-buyers | ~8.52 |
| Male users | ~10.38 |
| Female users | ~10.73 |

The buyer/non-buyer difference is particularly notable: buyers tend to have substantially shorter observed browsing paths.

## Business implications

The findings suggest several areas for experimentation:

- Prioritise high-quality customer-generated reviews on relevant product pages.
- Test the placement and presentation of video and celebrity content rather than assuming that greater exposure will improve conversion.
- Investigate unnecessary navigation between product discovery, evaluation and purchase.
- Monitor common paths and exit pages using sequence analysis.
- Use controlled A/B tests to evaluate review placement, calls to action and product-page design.
- Extend the analysis into purchase-propensity modelling using behavioural features such as page depth, review exposure, product interactions and journey sequence.

## Important limitations

This is an observational clickstream analysis. The project therefore identifies **associations rather than causal effects**. In particular, shorter buyer journeys do not prove that reducing page visits would itself increase conversion; underlying purchase intent may influence both browsing behaviour and conversion.

The observation period covers only the first 15 days of March 2012, and review availability differs across products. These factors should be considered before generalising the findings or using them to make causal business decisions.

## Repository structure

```text
Clickstream-Customer-Behaviour-Analytics/
│
├── README.md
├── clickstream_analysis.Rmd       # Application-ready R Markdown analysis
│
├── docs/
│   ├── Clickstream_Business_Report.pdf
│   ├── Clickstream_Business_Report.docx
│   ├── Clickstream_Presentation.pdf
│   └── Clickstream_Presentation.pptx
│
├── notebooks/
│   └── original_notebook.html     # Original rendered notebook
│
└── data/
    └── README.md                  # Instructions for local source data
```

## Reproducing the analysis

Install the required R packages:

```r
install.packages(c("dplyr", "tidyr", "TraMineR", "clickstream"))
```

Place the three source TSV files under `data/`:

```text
data/
├── clickstream-feed-generated.tsv
├── products (2).tsv
└── regusers (1).tsv
```

The R Markdown uses a `data_dir` parameter and defaults to `run_analysis = FALSE` so that the document can be reviewed as a portfolio artifact without the original data. Set `run_analysis = TRUE` when the source files are available.

## Outputs

- [Business report](docs/Clickstream_Business_Report.pdf)
- [Presentation](docs/Clickstream_Presentation.pdf)
- [Editable presentation](docs/Clickstream_Presentation.pptx)
- [R Markdown analysis](clickstream_analysis.Rmd)

## Presentation recording

The original project recording is available here:

https://drive.google.com/file/d/1Ke8dqnkjL5S8KGGkhVakl2kvyej1jV6f/view?usp=sharing

## Author

**Chhavi Wadhera**  
Digital Marketing Analytics | Statistics | Customer Analytics | Data Science
