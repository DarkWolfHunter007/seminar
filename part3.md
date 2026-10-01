
# PART 3 — SUPPORTING STUDIES AND COMPARATIVE ANALYSIS

## Chapter 5 — Review of Supporting Studies

### 5.1 Ghadi and Török (2020): Spatial and Environmental Factors

Ghadi and Török studied the relationship between spatial and environmental accident factors and severity patterns of road segments. Their methodology had three connected stages: spatial segmentation, black-spot identification/severity ranking, and decision-rule extraction.

The study analyzed approximately 1965 km of the Hungarian expressway network using accident and roadway data from 2013–2015. The accident records included severity, accident type, time, month, day, hour, weather, visibility and coordinates. Roadway variables included horizontal and vertical curvature, roadside hazards, median type and pavement condition. Traffic variables included speed limit, AADT and truck percentage. The analysis considered road segments without intersections. A total of 2155 fatal, serious and slight injury accidents were recorded.

The authors used linear referencing to locate accidents and K-means clustering to form spatially homogeneous accident segments. The method produced 181 segments. The clustered dataset included 1926 accidents because isolated observations that did not form an appropriate cluster were excluded. Segment length ranged from 0.23 km to 12.32 km, with a mean of about 6.76 km.

After segmentation, an empirical Bayesian procedure was used to rank the segments. A Safety Performance Function was developed using AADT, speed and degree of horizontal curve as explanatory variables. Reported calibration values included alpha = -3.577, beta1 = 0.674, beta2 = -0.465, beta3 = 1.059 and over-dispersion k = 1.179. The paper reports PCC = 0.768 for the relationship between observed and predicted accident data.

The 181 segments were divided into four severity groups, B1 to B4, with B1 representing the highest-risk group and B4 the lowest. CART was then used to derive decision rules. Twelve predictors covering environmental, temporal and accident characteristics were considered. AADT, path shape and speed limit were the principal splitters, with AADT appearing at the top of the tree. The paper reports that BS1 segments contained about one-third of the accidents and had an accident density of about 2.98 accidents/km. About 40% of BS1 accidents occurred under AADT greater than 10,000.

The study is important for this seminar because it demonstrates that spatial aggregation can expose roadway-environment patterns that are less visible when every accident is treated independently. It also provides a direct bridge between traditional black-spot analysis and machine-learning decision rules.

Relation to the base paper: Ghadi and Török use flexible spatially clustered segments, whereas Fiorentini and Losa use fixed 500 m road sites. Ghadi and Török combine K-means, SPF and EB with CART; Fiorentini and Losa compare LR, CART, RF, KNN and Naïve Bayes. Both studies nevertheless emphasize AADT and roadway geometry as important explanatory information.

### 5.2 Yan and Shen (2022): Bayesian-Optimized Random Forest

Yan and Shen proposed BO-RF, a hybrid model combining Random Forest with Bayesian Optimization for traffic accident severity prediction. The objective was to improve prediction while retaining interpretability through RF feature importance and partial dependence analysis.

The study used the US-Accidents dataset and obtained 30,426 records after preprocessing. Severity was represented by three ordered levels: Level 1 slight, Level 2 serious and Level 3 fatal. The reported distribution was highly imbalanced: 91.56% slight, 7.70% serious and 0.73% fatal.

The predictor set included location, distance, temporal, weather and point-of-interest variables. Important examples were Start_lat, Start_lng, Distance, Month, Day, Hour, Weekday, Pressure, Temperature, Humidity, Visibility, Traffic_signal, Junction, Crossing and Stop. Features with more than 10% missingness, including wind chill, wind speed and precipitation, were removed. Remaining missing values were imputed and categorical variables were converted to dummy variables.

Random Forest was optimized over three hyperparameters: n_estimators, max_depth and max_features. Ten-fold cross-validation was used, with mean F1 as the optimization objective. Bayesian Optimization used a Tree-structured Parzen Estimator and Expected Improvement. The search ranges and optimal values were:

| Hyperparameter | Search range | Optimal value |
|---|---:|---:|
| n_estimators | 1–1000 | 359 |
| max_depth | 1–50 | 42 |
| max_features | 1–15 | 12 |

The optimization step can be represented by the acquisition-function update:
x(n+1) = argmax alpha(x; Dn).

For interpretation, the paper defines RF variable importance using the contribution of a feature to tree splitting and averages that contribution across the forest. It also uses partial dependence to investigate how selected variables affect predicted severity.

Because of class imbalance, the authors evaluated precision, recall, F1 and AUC rather than relying on accuracy alone. The BO-RF model achieved macro precision 0.66, macro recall 0.53, macro F1 0.57 and AUC 0.9625. The default RF benchmark achieved precision 0.70, recall 0.47, F1 0.54 and AUC 0.958.

The reported feature importance showed that Start_latitude and Start_longitude contributed 24.37% and 24.20%, respectively, while Distance contributed 20.32%. Hour, pressure, temperature and humidity were also influential. Partial-dependence analysis indicated nonlinear relationships for several important variables.

Relation to the base paper: this study extends Fiorentini and Losa through systematic hyperparameter optimization and direct multiclass severity prediction. The common element is Random Forest with interpretable feature analysis.

### 5.3 Khan and Hussain (2024): GIS and Machine Learning in an Urban Environment

Khan and Hussain integrated GIS hotspot analysis with machine learning for traffic accident prediction in Faisalabad, Pakistan. Their objectives were to analyze urban accidents, identify accident hotspots and determine significant contributing factors.

Accident records came from Rescue 1122 Emergency Services for 2022 and contained location, date, day and time. Records outside the study area, duplicates and missing observations were removed. The study then used ArcGIS for spatial analysis.

Local Moran’s I was applied to identify statistically significant spatial clusters. The study identified 140 hotspots: 117 at the 99% confidence level, 16 at 95% and 7 at 90%. It also identified 62 coldspots. Many hotspots were concentrated around the General Transport Stand area. The temporal analysis reported the largest number of accidents during 1–2 p.m., with 1330 accidents.

After hotspot identification, field investigation and traffic-data collection were used to construct ML predictors. The study considered road geometric characteristics, road furniture and traffic information. Computer vision was used to extract traffic data from recorded videos.

Three models were developed: Random Forest, Linear Regression and Decision Tree. The reported maximum accuracy was 84.4% for the Decision Tree. The paper also reports that road measurements had the greatest effect among the investigated contributing variables.

The workflow can be summarized as:

Accident data → cleaning → ArcGIS → Local Moran’s I → hotspot identification → field survey/traffic extraction → ML prediction.

This paper complements Fiorentini and Losa because it uses GIS to discover spatial clusters before machine learning. The base paper instead defines uniform 500 m sites before classification.

### 5.4 Hamdan and Sipos (2025): Segment-Level Injury Counts

Hamdan and Sipos developed a machine-learning framework for predicting segment-level counts of fatalities, serious injuries and slight injuries on Hungarian roads. The models were Random Forest, Gradient Boosting and K-Nearest Neighbors.

The dataset was compiled from the Hungarian national road network for 2023. Road segments were defined using road number and precise start/end locations. Crash severity followed the Hungarian national database and CARE definitions: fatal crashes involve death within 30 days, serious injury involves hospital treatment exceeding 24 hours, and slight injury involves medical attention with less than 24 hours of hospitalization.

The predictors covered roadway geometry, traffic volume, traffic composition and road classification. Important variables included direction and radius of horizontal alignment, section type, number of lanes, slope, vertical-curve characteristics, capacity utilization, heavy-truck flow, light-truck flow, trailer combinations, bus flow, motorcycle/moped flow and bicycle flow.

SMOTE was used to address class imbalance. Grid-search cross-validation was used for hyperparameter tuning.

For serious-injury prediction, the optimal RF configuration used 300 trees, maximum depth 20, sqrt maximum features, minimum leaf size 3 and minimum split size 5. The reported test results were:

| Metric | RF | KNN | GB |
|---|---:|---:|---:|
| Accuracy | 0.9377 | 0.8815 | 0.8976 |
| Precision | 0.9428 | 0.8858 | 0.9022 |
| F1 | 0.9385 | 0.8830 | 0.8967 |
| MCC | 0.9294 | 0.8648 | 0.8839 |
| G-Mean | 0.9641 | 0.9309 | 0.9404 |
| MSE | 0.1859 | 0.5784 | 0.2890 |
| RMSE | 0.4311 | 0.7605 | 0.5376 |
| R2 | 0.9823 | 0.9449 | 0.9725 |

For slight-injury prediction, the reported test results were:

| Metric | RF | KNN | GB |
|---|---:|---:|---:|
| Accuracy | 0.9064 | 0.8391 | 0.7155 |
| Precision | 0.9108 | 0.8374 | 0.7041 |
| F1 | 0.9068 | 0.8352 | 0.7003 |
| MCC | 0.8983 | 0.8252 | 0.6917 |
| G-Mean | 0.9480 | 0.9093 | 0.8349 |
| MSE | 0.6024 | 1.8831 | 3.3148 |
| RMSE | 0.7761 | 1.3723 | 1.8207 |
| R2 | 0.9494 | 0.8419 | 0.7218 |

For fatality counts, the paper reports that Gradient Boosting achieved the highest accuracy, approximately 0.95, with R2 greater than 0.87.

The paper used:
R2 = 1 - sum((yi - yhat_i)^2) / sum((yi - ybar)^2)

and evaluated imbalance using G-Mean and Matthews Correlation Coefficient.

Feature-importance analysis showed that horizontal alignment was particularly influential for fatal crashes, while capacity utilization was more important for slight and serious injuries. Heavy-vehicle flows were consistently important across severity categories.

This paper extends the base study from binary accident-site screening to a richer prediction target: the number or level of injury outcomes associated with a road segment.

### 5.5 Golestani et al. (2025): Telematics, Weather and Explainable ML

Golestani et al. examined whether driving errors recorded by telematics occurred within previously identified accident hotspots. The study used telematics data from 1673 intercity buses across Iran during 2020 and merged these records with weather data.

After cleaning, 1,583,811 error records were available. Only 29,618, or approximately 1.87%, occurred in identified accident hotspots. The five error types were harsh braking, harsh acceleration, harsh turning, overspeed and fatigue.

The study defined an accident-density index:
l = x + 3y + 9z

where x is the number of property-damage-only accidents, y is the number of injury accidents and z is the number of fatal accidents. Locations above the mean index were treated as high-density accident locations.

A Haversine-distance procedure was then used to determine whether a telematics error occurred within 150 m of a hotspot.

The feature set included province, road type, error type, weather condition, dew point, hour, average wind speed and relative humidity. The final modeling data were highly imbalanced, so the authors used Balanced Random Forest, Easy Ensemble and Balanced Bagging approaches rather than ordinary sampling.

The data were split 70% for training and 30% for testing. Feature selection used Balanced Random Forest and permutation importance.

The final model comparison was:

| Model | AUC |
|---|---:|
| XGBoost | 91.70% |
| Random Forest | 91.14% |
| KNN | 90.09% |
| Logistic Regression | 85.73% |
| Naïve Bayes | 84.77% |
| SVM | 82.03% |

The selected XGBoost model achieved balanced accuracy of 84.70%.

SHAP was used for interpretation. Important mean absolute SHAP values included Tehran province 0.74, trunk roads 0.36, fatigue 0.33, Hamadan province 0.32 and dew point 0.14.

This study represents an important extension of the base paper because it combines static spatial context with dynamic behavioral and environmental observations. It also illustrates a modern explainable-AI workflow in which permutation importance is used for feature selection and SHAP is used for model interpretation.

## 5.6 Synthesis of the Supporting Studies

The five supporting papers expand the base-paper framework in five major directions.

1. Spatial aggregation: Ghadi and Török show how clustering can form flexible homogeneous road segments.
2. Hyperparameter optimization: Yan and Shen demonstrate Bayesian optimization of Random Forest.
3. GIS integration: Khan and Hussain combine Local Moran’s I with machine learning.
4. Injury-count prediction: Hamdan and Sipos extend the target from occurrence/severity classification to segment-level injury outcomes.
5. Dynamic behavioral data: Golestani et al. introduce telematics, weather and explainable ML.

The overall progression is:

Road geometry and traffic exposure → spatial severity → optimized severity classification → GIS hotspot prediction → injury-count prediction → dynamic behavioral-risk analysis.

# Chapter 6 — Comparative Analysis of the Six Studies

## 6.1 Research objectives

| Study | Main objective |
|---|---|
| Fiorentini & Losa (2020) | Long-term accident/non-accident road-site screening |
| Ghadi & Török (2020) | Spatial/environmental characterization of severity groups |
| Yan & Shen (2022) | Optimized RF prediction of accident severity |
| Khan & Hussain (2024) | GIS hotspot identification plus ML prediction |
| Hamdan & Sipos (2025) | Segment-level fatality and injury-count prediction |
| Golestani et al. (2025) | Telematics-error prediction within accident hotspots |

The base paper is primarily a road-site screening study. The supporting studies broaden the problem toward severity, spatial clustering, injury outcomes and dynamic behavior.

## 6.2 Dataset comparison

| Study | Location | Period | Observation unit |
|---|---|---|---|
| Fiorentini & Losa | Tuscany, Italy | 2012–2016 | 500 m road site |
| Ghadi & Török | Hungary | 2013–2015 | clustered road segment |
| Yan & Shen | US-Accidents | dataset period | geocoded accident |
| Khan & Hussain | Faisalabad, Pakistan | 2022 | urban accident/hotspot |
| Hamdan & Sipos | Hungary | 2023 | national road segment |
| Golestani et al. | Iran | 2020 | telematics event |

The data volumes also vary greatly. The base paper contains 1990 balanced road sites, Ghadi and Török analyze 181 clustered segments, Yan and Shen use 30,426 records after preprocessing, Hamdan and Sipos use national segment data, and Golestani et al. analyze more than 1.58 million telematics error records.

These differences mean that reported accuracy, AUC or R2 values must not be treated as results from a common benchmark.

## 6.3 Spatial representation

The studies use several spatial representations:

- Fiorentini and Losa: fixed 500 m road sites.
- Ghadi and Török: K-means-derived flexible accident segments.
- Yan and Shen: geocoded accident locations.
- Khan and Hussain: Local Moran’s I hotspots.
- Hamdan and Sipos: predefined national road segments.
- Golestani et al.: telematics points linked to hotspot locations.

Thus, spatial scale is a methodological decision, not simply a data-format choice.

## 6.4 Predictor-variable comparison

| Predictor group | F&L | G&T | Y&S | K&H | H&S | G et al. |
|---|---|---|---|---|---|---|
| Traffic volume/AADT | ✓ | ✓ | — | ✓ | ✓ | — |
| Road geometry | ✓ | ✓ | limited | ✓ | ✓ | — |
| Speed | ✓/related | ✓ | — | ✓ | ✓ | ✓ |
| Weather | — | ✓ | ✓ | limited | — | ✓ |
| Time | — | ✓ | ✓ | ✓ | — | ✓ |
| Spatial location | site | segment | ✓ | ✓ | segment | ✓ |
| POI | — | — | ✓ | — | — | — |
| Vehicle composition | — | trucks | — | ✓ | ✓ | — |
| Behavioral data | — | — | — | — | — | ✓ |
| Telematics | — | — | — | — | — | ✓ |

The trend is toward progressively richer and more heterogeneous predictors.

## 6.5 Prediction-target comparison

The target variable evolves substantially:

Accident/non-accident site → segment severity group → individual accident severity → urban hotspot occurrence → injury count → behavioral error in hotspot.

This is important because a road-safety ML system should be designed around the operational question it is intended to answer. Screening, severity prediction and injury forecasting are related but distinct tasks.

## 6.6 Machine-learning comparison

The papers use Logistic Regression, CART/Decision Tree, Random Forest, KNN, Naïve Bayes, Gradient Boosting, XGBoost, Linear Regression and optimized/imbalanced ensemble methods.

Tree-based ensembles appear repeatedly because they can model nonlinear interactions among roadway, traffic and environmental variables. Random Forest is particularly common across the corpus and is the central ML method in the base paper.

Optimization is also becoming more systematic. Fiorentini and Losa use a specified RF configuration, Yan and Shen use Bayesian Optimization, Hamdan and Sipos use grid-search cross-validation, and Golestani et al. use model comparison with imbalance-aware ensembles.

## 6.7 Class imbalance

Class imbalance is a recurring methodological issue.

- Fiorentini and Losa construct a balanced binary dataset with 995 accident and 995 non-accident sites.
- Yan and Shen retain a highly imbalanced three-level severity target and emphasize F1/AUC.
- Hamdan and Sipos use SMOTE.
- Golestani et al. use balanced ensemble methods because only about 1.87% of telematics errors occurred in hotspots.

This shows that sampling and imbalance handling are part of model design, not merely preprocessing.

## 6.8 Interpretability comparison

| Study | Main interpretation method |
|---|---|
| Fiorentini & Losa | descriptive statistics, RF behavior and classification metrics |
| Ghadi & Török | CART decision rules |
| Yan & Shen | RF importance + partial dependence |
| Khan & Hussain | decision-tree rules and contributing-factor analysis |
| Hamdan & Sipos | feature importance |
| Golestani et al. | permutation importance + SHAP |

The progression is from directly readable decision rules toward model-agnostic explanation techniques such as SHAP.

## 6.9 Evaluation metrics

Fiorentini and Losa use accuracy, precision, recall, F1 and AUROC. Yan and Shen use precision, recall, F1 and AUC. Hamdan and Sipos additionally use MCC, G-Mean, MSE, RMSE and R2. Ghadi and Török use AIC and PCC for the SPF and spatial/decision analysis. Khan and Hussain report hotspot confidence levels and model accuracy. Golestani et al. use AUC, balanced accuracy and weighted F1.

The metrics therefore depend on the prediction target, class distribution and analytical purpose.

## 6.10 Selected reported results

| Study/model | Reported result |
|---|---|
| Fiorentini & Losa RF | 73.53% test accuracy; AUROC 0.795 |
| Ghadi & Török SPF | PCC 0.768 |
| Yan & Shen BO-RF | Macro F1 0.57; AUC 0.9625 |
| Khan & Hussain Decision Tree | 84.4% accuracy |
| Hamdan & Sipos RF, serious injury | 93.77% test accuracy; R2 0.9823 |
| Hamdan & Sipos RF, slight injury | 90.64% test accuracy; R2 0.9494 |
| Hamdan & Sipos GB, fatalities | approximately 95% accuracy; R2 > 0.87 |
| Golestani et al. XGBoost | AUC 91.70%; balanced accuracy 84.70% |

These figures are study-specific. They should not be interpreted as a ranking because the prediction targets, data, class structures and validation methods are different.

## 6.11 Evolution of the research problem

The six papers illustrate the following evolution:

1. Long-term blackspot screening.
2. Spatial severity characterization.
3. Individual accident-severity classification.
4. GIS-supported urban hotspot prediction.
5. Segment-level injury-count prediction.
6. Dynamic behavioral-risk prediction.

Conceptually:

Spatial road-site screening → severity modeling → injury prediction → dynamic behavioral risk.

This evolution changes the role of the model from identifying locations requiring attention to estimating increasingly specific outcomes associated with those locations.

## 6.12 Integrated literature framework

A unified framework emerging from the six studies is:

Road-safety data
→ roadway geometry, traffic exposure, accident history, weather, time and behavior
→ spatial processing
→ fixed segments, clustered segments or GIS hotspots
→ feature engineering and imbalance handling
→ ML models
→ evaluation
→ feature importance, partial dependence or SHAP
→ safety decision support.

GIS and ML therefore play complementary roles. GIS provides spatial structure and clustering; machine learning models nonlinear relationships among spatial, geometric, traffic, environmental and behavioral variables.

## 6.13 Research gaps

### 6.13.1 Generalizability

Each study is based on a particular road system. Differences in roadway standards, traffic composition, enforcement, reporting and driving behavior may limit transferability.

### 6.13.2 Static versus dynamic data

The base paper uses mainly stable roadway attributes. Later research introduces time, weather and telematics. A future model could combine static infrastructure variables with dynamic exposure and behavioral observations.

### 6.13.3 Spatial-scale selection

The papers use 500 m sites, flexible clusters, urban hotspots, national road segments and individual telematics observations. Multi-scale validation remains an important research opportunity.

### 6.13.4 Imbalanced severe outcomes

Fatal and severe crashes are comparatively rare. SMOTE, balanced forests and other ensemble approaches are useful, but their comparative behavior across a common dataset is not fully established by these six papers.

### 6.13.5 Interpretability versus causality

Feature importance, partial dependence and SHAP explain model behavior but do not establish causal relationships. Infrastructure decisions should therefore distinguish predictive association from causal evidence.

### 6.13.6 Temporal validation

Random train/test splitting is common. A stronger deployment-oriented design would also test a model trained on earlier years against later years.

### 6.13.7 Dynamic risk prediction

Telematics demonstrates the possibility of continuous behavioral-risk monitoring. Combining telematics with GIS hotspots and long-term road characteristics could move the field beyond periodic blackspot screening.

### 6.13.8 Common benchmarking

Because the studies use different datasets and targets, cross-paper performance comparisons are not directly valid. A standardized benchmark would require common spatial units, consistent severity definitions, explicit imbalance procedures and standardized evaluation metrics.

## 6.14 Overall synthesis

Fiorentini and Losa provide the methodological anchor for this seminar through long-term road-site screening using roadway and traffic characteristics. Ghadi and Török show how spatial clustering and empirical Bayesian ranking can reveal segment-level severity patterns. Yan and Shen demonstrate optimized Random Forest for multiclass severity prediction. Khan and Hussain connect GIS hotspot analysis with machine learning in an urban environment. Hamdan and Sipos extend the target to fatality and injury counts using detailed geometric and traffic-composition variables. Golestani et al. add telematics, weather, behavioral errors and SHAP-based interpretation.

The combined literature therefore supports a progression from static blackspot screening toward integrated, interpretable and increasingly dynamic road-safety analytics.

## References

1. Fiorentini, N.; Losa, M. Long-Term-Based Road Blackspot Screening Procedures by Machine Learning Algorithms. Sustainability, 2020, 12, 5972.
2. Ghadi, M.Q.; Török, Á. Evaluation of the Impact of Spatial and Environmental Accident Factors on Severity Patterns of Road Segments. Periodica Polytechnica Transportation Engineering, 2020. DOI: 10.3311/PPtr.14692.
3. Yan, M.; Shen, Y. Traffic Accident Severity Prediction Based on Random Forest. Sustainability, 2022, 14, 1729. DOI: 10.3390/su14031729.
4. Khan, A.A.; Hussain, J. Utilizing GIS and Machine Learning for Traffic Accident Prediction in Urban Environment. Civil Engineering Journal, 2024, 10(6), 1922–1935. DOI: 10.28991/CEJ-2024-010-06-013.
5. Hamdan, N.; Sipos, T. Predicting Segment-Level Road Traffic Injury Counts Using Machine Learning Models: A Data-Driven Analysis of Geometric Design and Traffic Flow Factors. Future Transportation, 2025, 5, 197. DOI: 10.3390/futuretransp5040197.
6. Golestani, A.; Rezaei, N.; Malekpour, M.-R.; Ahmadi, N.; Ataei, S.M.-N.; Khosravi, S.; Jafari, A.; Shahraz, S.; Farzadfar, F. Predicting errors in accident hotspots and investigating spatiotemporal, weather, and behavioral factors using interpretable machine learning: An analysis of telematics big data. PLOS ONE, 2025, 20(7), e0326483. DOI: 10.1371/journal.pone.0326483.

## Figure/Table insertion plan

Figure 5.1 — Ghadi and Török: spatial clustering → EB ranking → CART decision rules.
Figure 5.2 — Yan and Shen: BO-RF workflow.
Figure 5.3 — Khan and Hussain: GIS hotspot → field survey → ML workflow.
Figure 5.4 — Hamdan and Sipos: segment-level injury-count framework.
Figure 5.5 — Golestani et al.: telematics → hotspot matching → feature selection → XGBoost → SHAP.
Table 5.1 — Summary of supporting studies.
Table 6.1 — Research objectives and prediction targets.
Table 6.2 — Dataset and spatial-unit comparison.
Table 6.3 — Predictor-variable comparison.
Table 6.4 — ML algorithms and evaluation metrics.
Table 6.5 — Selected reported model results.
Figure 6.1 — Evolution from blackspot screening to dynamic behavioral-risk prediction.
Figure 6.2 — Integrated GIS–ML road-safety analytics framework.
