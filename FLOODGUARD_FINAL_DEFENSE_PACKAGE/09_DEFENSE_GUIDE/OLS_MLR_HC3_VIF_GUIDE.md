# Statistical Methodology Guide: OLS, MLR, HC3, and VIF

---

## Part 1: Plain Language Panel Answers

### 1. What is Multiple Linear Regression (MLR)?
MLR models the mathematical relationship between a target variable (e.g. tomorrow's maximum water level) and two or more explanatory predictors (e.g. yesterday's water level, water level 3 days ago, and upstream rainfall).

### 2. How are the model coefficients calculated?
Coefficients are calculated using **Ordinary Least Squares (OLS)**, which computes the unique set of weights that minimizes the sum of squared differences between observed water levels and predicted water levels:
$$\hat{\beta} = (X^T X)^{-1} X^T y$$

### 3. What is HC3 and why is it necessary?
Standard regression standard errors assume that variance of error terms is constant across all river heights (homoskedasticity). In river modeling, error variance is naturally higher during severe storms than during calm dry days (heteroskedasticity). **HC3 (Heteroskedasticity-Consistent Standard Errors)** adjusts the variance-covariance matrix to provide honest, trustworthy $p$-values and confidence intervals without being distorted by high-leverage storm outliers.
> **Critical Defense Fact:** HC3 changes hypothesis testing and standard errors ONLY. It strictly DOES NOT change model coefficients ($\beta$) or predicted water levels ($\hat{y}$).

### 4. What is VIF and how did you verify multicollinearity?
**Variance Inflation Factor (VIF)** measures how much the variance of an estimated regression coefficient increases due to correlation among predictor variables. A VIF below 5.0 indicates that multicollinearity is within safe statistical limits and does not destabilize coefficient estimates.
- **Sto. Niño C9:** Max VIF = **`2.0610`** (2.060977) $\le 5.0$ (PASS)
- **Nangka C4:** Max VIF = **`1.5957`** $\le 5.0$ (PASS)
- **Tumana C8:** Max VIF = **`1.1212`** $\le 5.0$ (PASS)

---

## Part 2: Mathematical Formulations & Exact Proofs

### OLS Parameter Estimation
Given design matrix $X \in \mathbb{R}^{n \times p}$ and observation vector $y \in \mathbb{R}^n$:
$$\hat{\beta} = (X^T X)^{-1} X^T y$$

### HC3 Covariance Estimator (MacKinnon & White, 1985)
Let $H = X(X^T X)^{-1} X^T$ be the hat matrix, with diagonal leverage values $h_{ii} = H_{ii}$. Let $e_i = y_i - \hat{y}_i$ be the OLS residuals.
The HC3 covariance matrix is defined as:
$$\text{Cov}_{\text{HC3}}(\hat{\beta}) = (X^T X)^{-1} X^T \Omega_{\text{HC3}} X (X^T X)^{-1}$$
where $\Omega_{\text{HC3}} = \text{diag}\left( \frac{e_i^2}{(1 - h_{ii})^2} \right)$.
The robust standard error for coefficient $\beta_j$ is:
$$\text{SE}_{\text{HC3}}(\hat{\beta}_j) = \sqrt{\left[ \text{Cov}_{\text{HC3}}(\hat{\beta}) \right]_{jj}}$$

### Variance Inflation Factor (VIF)
For predictor $X_j$, let $R_j^2$ be the coefficient of determination when regressing $X_j$ against all other predictors $X_{-j}$:
$$\text{VIF}_j = \frac{1}{1 - R_j^2}$$
- $\text{VIF} < 5.0$: Low to moderate collinearity (Certified PASS).
- $\text{VIF} \ge 10.0$: Severe collinearity (Prohibited).
