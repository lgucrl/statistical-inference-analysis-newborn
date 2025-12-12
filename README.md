# Statistical Inference Analysis to predict newborn weight

This repository contains an inferential statistics project in **R** with the goal of building, validating, and interpreting a statistical model capable of **predicting newborn weight** from collected clinical variables, such as maternal, pregnancy, and newborn measurements. The analysis combines classical hypothesis testing with multiple linear regression, model selection, diagnostics, and scenario-based prediction. The full project is contained in the R Markdown document and the HTML output can be visulized in this [Github Page](https://lgucrl.github.io/statistical-inference-analysis-newborn/).



## Dataset

The dataset (`newborns.csv`) contains **2,500 newborns** observed across **three hospitals**. It is structured with **one row per newborn** and includes the following variables:

- **Mother.age**: mother’s age
- **Pregnancies.n**: number of the mother's previous pregnancies
- **Smoker**: mother smoking status (0 = non-smoker, 1 = smoker)
- **Gestation.w**: gestational age in weeks
- **Weight**: newborn weight in grams (**response variable**) 
- **Length**: newborn length in millimeters
- **Cranium**: newborn cranium diameter in millimeters
- **Birth.type**: delivery mode (Natural or Cesarean)
- **Hospital**: hospital identifier (1, 2, or 3)
- **Sex**: newborn sex (Male or Female)



## Analytical workflow

1. **Exploratory data analysis**  
   The analysis starts by loading the required R packages (for data manipulation, visualization, modeling and diagnostics), importing the CSV dataset and verifying (head/summary) column types and ranges. Next, a descriptive analysis of each variable (central tendency, variability and potential anomalies) is produced. Since `Weight` is the target, its shape is inspected using density plots and normality tests (e.g., Shapiro–Wilk), motivating later choices about parametric vs. non-parametric procedures and highlighting whether normality of residuals must be assessed after modeling.

3. **Overview of variable relationship**  
   To understand how predictors relate to each other and to `Weight`, the analysis computes a correlation matrix for continuous variables and visualizes it to check for potential multicollinearity. A scatterplot matrix (pair plot) complements this by showing functional forms, such as non-linear relationships. For categorical predictors (`Sex`, `Smoker`, `Birth.type`), boxplots provide an initial view of between-group differences.

4. **Hypothesis testing to answer specific questions**  
   Before fitting predictive models, targeted hypothesis tests address some questions: (1) whether `Birth.type` differs by `Hospital` (Chi-square test on a contingency table), (2) whether sample means (`Weight`, `Length`) align with reference population values (one-sample tests, switching to Wilcoxon when normality is violated), and (3) whether anthropometric measures differ by `Sex (two-sample Wilcoxon when appropriate). These tests establish evidence-backed context for later modeling.

5. **Baseline multiple regression**  
   A first multiple linear regression including all available predictors is fit to quantify marginal effects on `Weight`. Coefficient estimates and p-values provide intuitions about which variables matter most, while multicollinearity is checked using VIF to confirm whether any predictors should be excluded due to redundancy.

6. **Model selection and feature engineering**  
   A stepwise selection using an information criterion (BIC) is performed to retain only predictors that significantly improve fit. Possible interaction terms are tested (such as `Length` × `Cranium`) and compared through BIC and ANOVA tests. Quadratic terms are added based on observed curvature in pair plots (e.g., `Length`² and `Gestation.w`²), allowing the final model to capture non-linear effects.

7. **Model validation, diagnostics, and prediction**  
   All created models are compared using BIC, adjusted R² and RMSE to balance fit, complexity, and predictive accuracy. Diagnostics then assess residual behavior (normality, homoscedasticity, autocorrelation) and identify influential observations via leverage, studentized residuals, and Cook’s distance. Lastly, the selected model is used to generate estimates of newborn weight under specified clinical scenarios, supported by clear 2D/3D visualizations.
