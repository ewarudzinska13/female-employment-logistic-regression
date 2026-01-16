# female-employment-logistic-regression
Logistic regression analysis of female labor force participation determinants, comparing Maximum Likelihood Estimation (MLE) with Method of Moments (MM) approaches

# Determinants of Female Employment - Logistic Regression Analysis

Advanced econometric analysis comparing Maximum Likelihood Estimation (MLE) and Method of Moments (MM) approaches in logistic regression modeling. Project completed for "Analytical Tools Programming II" course at the University of Warsaw (February 2025).

## Project Overview

This study analyzes determinants of female labor force participation using logistic regression with two estimation methods: classical MLE and the more flexible Method of Moments approach. The comparison demonstrates how both methods handle binary outcome variables and validates the robustness of findings across different estimation techniques.

## Research Questions & Hypotheses

### Hypothesis 1: Young Children Effect
**Having children aged 0-6 negatively impacts the probability of female employment.**

Based on Bruce (1978) and Euwals et al. (2011), young children significantly reduce female labor force participation due to childcare responsibilities and costs.

**Result**: **CONFIRMED** - Strong negative effect (β₄ ≈ -1.40, p < 0.001)

### Hypothesis 2: Older Children Effect  
**Having children aged 6-18 negatively impacts employment probability, but less severely than younger children.**

Following Euwals et al. (2011), the negative effect should decrease as children reach school age.

**Result**:  **REJECTED** - Effect statistically insignificant (β₅ ≈ 0.044, p > 0.5)

### Hypothesis 3: Education Effect
**More years of education increase the probability of female employment.**

Consistent with Euwals et al. (2011) and Osundina (2019), higher education correlates with increased female labor force participation.

**Result**:  **CONFIRMED** - Positive effect (β₁ ≈ 0.162, p < 0.001)

## Data

### Source
**Mroz (1987)** dataset - widely used for binary choice modeling in econometrics
- Cross-sectional data from the United States
- **Sample size**: 753 observations
- **Dependent variable**: Binary employment status (1 = employed, 0 = not working)

### Variables

| Variable | Type | Description |
|----------|------|-------------|
| `inlf` | Binary | Employment status (1 = employed, 0 = not working) |
| `educ` | Discrete | Years of education |
| `exper` | Discrete | Years of work experience |
| `age` | Discrete | Age in years |
| `kidslt6` | Discrete | Number of children under age 6 |
| `kidsge6` | Discrete | Number of children aged 6-18 |
| `faminc` | Continuous | Family income |
| `city` | Binary | Place of residence (0 = rural, 1 = urban) |

## Methodology

### Model Specification

**Logistic regression model**:
```
P(inlf = 1) = 1 / (1 + e^-(β₀ + β₁·educ + β₂·exper + β₃·age + β₄·kidslt6 + β₅·kidsge6 + β₆·faminc + β₇·city))
```

### Estimation Methods

#### 1. Maximum Likelihood Estimation (MLE)
Classical approach providing asymptotically efficient estimators for logistic regression.

**Model diagnostics performed**:
- **Link test**: Verified functional form specification (p < 2e-16 for linear term, p = 0.887 for quadratic)
- **Hosmer-Lemeshow test**: Assessed goodness-of-fit in subgroups (p = 0.181)
- **Osius-Rojek test**: Overall fit assessment (p = 0.739)
- **Stukel test**: Alternative fit assessment (p = 0.987)
- **Likelihood Ratio test**: Joint significance of variables (p < 2e-16)

**Conclusion**: Model is correctly specified and well-fitted to the data.

#### 2. Method of Moments (MM)
Alternative estimation approach using moment conditions:

**Moment conditions**:
```
R₁: Σ[inlf - p] = 0
R₂: Σ[(inlf - p) × educ] = 0
R₃: Σ[(inlf - p) × exper] = 0
R₄: Σ[(inlf - p) × age] = 0
R₅: Σ[(inlf - p) × kidslt6] = 0
R₆: Σ[(inlf - p) × kidsge6] = 0
R₇: Σ[(inlf - p) × faminc] = 0
R₈: Σ[(inlf - p) × city] = 0
```

where `p = 1/(1 + e^-(X'β))` is the predicted probability.

Variance-covariance matrix calculated to obtain standard errors for hypothesis testing.

## Results

### Estimation Comparison

| Variable | MLE Estimate | MLE Std. Error | MLE p-value | MM Estimate | MM Std. Error | MM p-value |
|----------|--------------|----------------|-------------|-------------|---------------|------------|
| Intercept | 1.198 | 0.834 | 0.151 | 1.198 | 0.016 | < 2e-16* |
| `educ` | 0.162 | 0.043 | 0.0002 | 0.162 | 0.035 | 4.39e-06 |
| `exper` | 0.128 | 0.014 | < 2e-16 | 0.128 | 0.014 | < 2e-16 |
| `age` | -0.099 | 0.014 | 5.16e-12 | -0.099 | 0.009 | < 2e-16 |
| `kidslt6` | **-1.403** | 0.199 | 1.88e-12 | **-1.403** | 0.186 | 4.88e-14 |
| `kidsge6` | 0.044 | 0.073 | 0.548 | 0.044 | 0.066 | 0.507 |
| `faminc` | 0.00002 | 0.00001 | 0.038* | 0.00002 | 0.00001 | 0.062 |
| `city` | -0.171 | 0.188 | 0.364 | -0.171 | 0.188 | 0.362 |

**Key observations**:
- **Identical parameter estimates** across both methods
- **Different standard errors** leading to slight variations in statistical significance
- Both methods confirm key hypotheses (H1 and H3)

### Additional Hypothesis Test

**H₀: β₄ (kidslt6) = -1.7**  
Test statistic z = 1.597 → p-value outside critical region at α = 0.05

**Conclusion**: No statistical grounds to reject H₀; the effect of young children could be as strong as -1.7.

### Main Findings

1. **Young children (< 6 years)**: Strongest negative effect on employment probability (β ≈ -1.40)
2. **Education**: Positive effect - each additional year increases employment probability (β ≈ 0.16)
3. **Work experience**: Significant positive effect (β ≈ 0.13)
4. **Age**: Negative effect - older women less likely to be employed (β ≈ -0.10)
5. **Older children (6-18)**: No statistically significant effect
6. **Family income**: Borderline significance - MLE suggests slight positive effect, MM is inconclusive at α = 0.05
7. **Urban residence**: No significant effect

## Interpretation

### Economic Significance

The negative coefficient for young children (kidslt6) of approximately -1.40 indicates that having one additional child under age 6 **decreases the log-odds of employment by 1.40**, which translates to a substantial reduction in employment probability. This confirms that childcare responsibilities for young children are the primary barrier to female labor force participation.

The positive education coefficient (0.162) suggests that each additional year of schooling increases employment probability, supporting the human capital theory that education improves labor market outcomes.

### Method Comparison

Both MLE and MM produced identical point estimates, validating the robustness of findings. The slight differences in standard errors are expected and demonstrate that:
- **MLE** is asymptotically efficient under correct model specification
- **MM** provides consistent estimates with greater flexibility regarding distributional assumptions

The family income variable showed the only meaningful difference: significant at 5% level under MLE (p = 0.038) but not under MM (p = 0.062), suggesting marginal evidence of an income effect.

## Tools & Technologies

- **R** for statistical analysis
- **Libraries**:
  - `stats::glm()` - MLE logistic regression
  - `rootSolve::multiroot()` - Solving MM equation system
  - `lmtest` - Diagnostic tests
  - `generalhoslem` - Hosmer-Lemeshow test


