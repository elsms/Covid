[![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-orange)](Project.ipynb)
[![Bloomberg Terminal](https://img.shields.io/badge/Bloomberg%20Terminal-Data%20Source-yellow)](https://www.bloomberg.com/professional/products/bloomberg-terminal/#overview)

# Introduction 
This notebook explores whether COVID-19 affected the Hong Kong MSCI Index returns. It was developed as part of the [Econometrics Analysis for Finance](https://www.reading.ac.uk/modules/documents?acyear=2025%252f6&modcode=ICM337&schoolcode=HBS%20DME%20G%7CHBS%20DME%20W%7CHBS%20FIN%20G%7CHBS%20FIN%20W%7CHBS%20IBS%20G%7CHBS%20IBS%20W%7CHBS%20LBR%20G%7CHBS%20LBR%20W%7CHBS%20MGM%20W%7CHBS%20REP%20G%7CHBS%20REP%20W&_ga=2.25857272.458363835.1771460903-1103066443.1771460903) module at [Henley Business School](https://www.henley.ac.uk/#).

The group assignment involved selecting one of two MSCI indexes (Hong Kong or South Korea) and addressing related research questions. This notebook presents my individual contribution, analyzing the impact of COVID-19 on the chosen index’s returns and comparing the findings with existing literature.

# Data 
The [data](Data) used in this analysis was sourced from the [Bloomberg Terminal](https://www.bloomberg.com/professional/products/bloomberg-terminal/), [LSEG](https://www.lseg.com/en) and a [website curated by the Hong Kong Government](https://data.gov.hk/en-data/dataset/hk-dh-chpsebcddr-novel-infectious-agent). 

# Methodology 

### Dataset Description 
The dataset used in the analysis entails the following variables. 
| Variable | Meaning |
|----------|--------------------|
| HK MSCI Returns | Monthly logarithmic HK MSCI returns over 2015-2023, used as the model’s dependent variable.  |
| Stringency Index | Government response tracker developed by the Blavatnik School of Government at the University of Oxford and sourced from London Stock Exchange Group (LSEG). It compiles policy responses to COVID-19 and is included because containment and economic measures (e.g., lockdowns, social distancing) have been shown to mitigate market impacts and support stock returns (Beer, Maniora, and Pott, 2023; Deng, Xu, and Lee, 2022; Guven et al., 2022; Jiang et al., 2022).  |
| Hang Seng Returns | Monthly logarithmic returns of the Hang Seng Index. Included because Hong Kong’s equity market was negatively affected by the outbreak, and prior research shows stock returns interact significantly with developing pandemics (Al-Awadhi, 2020; Jin, Lu, and Zhang, 2022). |
| Number of death cases related to COVID-19 | Daily deaths aggregated to monthly totals. Included as confirmed cases and deaths negatively impact stock returns and volatility (Ashraf, 2020; Guven et al., 2022; Harjoto et al., 2021). |
| Outbreak Severity | Sum of hospitalized cases in critical condition and the ratio of deaths to confirmed cases. Included due to evidence that higher severity negatively affects stock returns and volatility (Ashraf, 2020; Guven et al., 2022; Harjoto et al., 2021). |
| Spread | Ratio of confirmed cases to total monthly tests. Included as higher case rates negatively impact stock returns (Ashraf, 2020; Guven et al., 2022; Harjoto et al., 2021).  |
| Recovery | Sum of discharged cases and the ratio of ruled-out cases to confirmed cases. Included because recoveries have been shown to influence stock returns, though the effect is weaker than cases or deaths (Basuony, 2021).  |
| Time Dummy | Time dummy defined as follows: 1 = from January 1st, 2020, to December 31st, 2022, and 0 = from January 1st, 2015, to December 31st , 2019. Adopted to differentiate between pre-pandemic and pandemic periods, as in prior studies (Basuony et al., 2021; Khan, Fifield, and Power, 2024).  |
| MSCI COVID-19 | Interaction term specified as the product of MSCI Returns and the Time Dummy variable to capture potential changes in market sensitivity during the pandemic period, as stock markets exhibited intensified reactions during this period (Ashraf, 2020; Bai et al., 2023).  |

### Model Specification 

To test for a COVID-19 effect on the dependent variable, the following models are specified:

* A **simple linear regression** with the *time dummy* variable as the only explanatory variable.
* A **multiple linear regression** including all previously listed variables.
* **ARCH** and **GARCH** models to capture volatility dynamics. 

# Key Findings 

### Simple Linear Regression 
The *p*-value on the time dummy exceeds the 5% significance level, indicating it's not statistically significant. Consequently, the test fails to reject the null hypothesis that MSCI Hong Kong Index performance is the same in the pre-COVID and COVID-19 preiods, suggesting no no significant relationship between the time dummy and index returns.

### Multiple Linear Regression 
The time dummy is statistically insignificant. In contrast, Hang Seng Index returns, COVID-19 deaths, the Spread Index, and the MSCI COVID-19 indicator are significant determinants of MSCI Hong Kong Index returns. Hang Seng Index returns and the MSCI COVID-19 indicator are positively associated with returns, whereas COVID-19 deaths and the Spread Index have negative effects.

Moreover, the **Fitted vs. Actual Values plot** shows that MSCI Hong Kong returns experienced frequent fluctuations during 2020, which are largely captured by the first multiple linear regression model. From 2021 onward, MSCI performance declined more persistently, with reduced volatility for much of the period, followed by sharp movements toward the end of 2022, contrasting with the more cyclical pattern observed from 2015 to 2020. Overall, the model captures broad trends over the sample period; however, it performs less accurately during certain sub-periods, particularly between mid-2021 and late 2022. Additionally, the fitted values tend to follow minor fluctuations in the data too closely, suggesting potential in-sample overfitting.

<div align="center">
<img width="587" height="455" alt="image" src="https://github.com/user-attachments/assets/88168c8c-d1f6-4752-a815-966154b45467" />
</div>

Variance inflation factor (VIF) diagnostics indicate that the time dummy may contribute to multicollinearity. Given its insignificance, it was excluded from the model. However, the reduced specification produces identical results, confirming its lack of explanatory power.

### ARCH and GARCH models


# Conclusion 
The final results of the estimated models are presented in the table below.
| Variable | Meaning |
|----------|--------------------|
| Stringency Index | Positive but statistically non-significant. This contrasts with prior studies that found government measures, such as lockdowns and social distancing, mitigated pandemic impacts or positively influenced stock markets (Beer, Maniora, and Pott, 2023; Deng, Xu, and Lee, 2022; Guven et al., 2022; Jiang et al., 2022).  |
| Hang Seng Returns | Highly significant and positive, confirming that Hong Kong's market strongly influenced MSCI returns. This aligns with literature documenting regional market co-movement and spillover effects during the pandemic (Al-Awadhi, 2020; Jin, Lu, and Zhang, 2022).  |
| Number of death cases related to COVID-19 | Highly significant and negatively associated with MSCI returns, consistent with prior research showing that rising COVID-19 cases and deaths negatively affected stock markets (Ashraf, 2020; Harjoto et al., 2021). |
| Outbreak Severity | Statistically non-significant, despite expectations from the literature that more severe outbreaks would depress stock returns (Ashraf, 2020; Harjoto et al., 2021).  |
| Spread | Statistically significant and negative, confirming that higher infection rates adversely impacted MSCI returns, consistent with previous findings (Ashraf, 2020;Harjoto et al., 2021).  |
| Recovery | Statistically non-significant, contrary to literature suggesting that recoveries positively influence markets, albeit with weaker effects than deaths or cases (Basuony et al., 2021).   |
| Time Dummy | Not statistically significant, indicating MSCI returns did not differ systematically between pre-COVID and pandemic periods. This contrasts with studies reporting negative shifts in market performance during the pandemic (Harjoto, Rossi, and Paglia, 2021; Liu et al., 2020; Shehzad, Xiaoxing, and Kazouz, 2020).   |
| MSCI COVID-19 | Highly significant and positive, suggesting that MSCI returns became more sensitive during the pandemic. This is consistent with studies documenting increased responsiveness of MSCI and other global equity indices to pandemic-related shocks (Ashraf, 2020; Bai et al., 2023).   |
