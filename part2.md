# Part 2 — Chapters 2, 3 and 4

# CHAPTER 2 — FUNDAMENTALS OF ROAD TRAFFIC ACCIDENT ANALYSIS

## 2.1 Road Traffic Accident Characteristics

Road traffic accidents are events that occur within a transportation system through the interaction of road users, vehicles, roadway characteristics, traffic conditions and the surrounding environment. For analytical purposes, an accident record is not only a description of an event; it is also a spatial and temporal observation that can be linked to a particular road location and to the characteristics of that location.

The six studies considered in this seminar illustrate why accident analysis is multidimensional. The Fiorentini and Losa study uses long-term accident history together with roadway geometry, traffic flow and built-up-area information [1]. The Random Forest severity study incorporates traffic, temporal, weather and point-of-interest variables [2]. The GIS and machine-learning study in Faisalabad combines accident location, date and time with road geometric features, road furniture and traffic data [3]. The segment-level injury-count study uses detailed roadway geometry and vehicle-type traffic flows [4]. These studies therefore treat the accident record as part of a wider dataset rather than as an isolated event.

For road-safety analysis, an accident dataset can contain several levels of information:

1. accident-level information, such as date, time, location, collision characteristics and severity;
2. road-site information, such as road width, curvature, slope and junction characteristics;
3. traffic information, such as traffic volume and vehicle composition;
4. environmental information, such as built-up-area context and weather;
5. spatial information, which allows accident records and roadway characteristics to be linked geographically.

The analytical objective depends on how these data are organized. A study may predict whether an accident occurs, estimate the number of injuries, classify accident severity, or identify spatial clusters of accidents.

## 2.2 Accident Frequency and Severity

Accident frequency refers to the number of accident events associated with a road location or road segment during a defined period. Accident severity describes the consequence level of an accident, commonly using categories such as slight injury, serious injury and fatality.

These concepts should not be treated as interchangeable. A road segment may experience a relatively large number of low-severity crashes, while another segment may experience fewer crashes but include fatal or serious-injury events. A safety-analysis system therefore needs to define its prediction target before selecting the model.

The Fiorentini and Losa base study uses a binary crash-occurrence susceptibility target. The road site is labelled according to whether at least one fatal or injury crash occurred during the five-year period from 2012 to 2016 [1]. Property-damage-only crashes were excluded from their dataset because they were not considered under the Italian road-safety standards used in the study.

The accident-severity study by Yan and Shen uses a different target. Its response variable contains three severity levels: Level 1 for slight accidents, Level 2 for serious accidents and Level 3 for fatal accidents [2]. The distinction is important because the same machine-learning algorithm can be applied to different response variables, but the meaning of the resulting prediction is different.

The 2025 segment-level study goes further by considering crash severity counts rather than simply assigning one severity label to an individual crash. It develops models for fatality, serious-injury and slight-injury outcomes at the road-segment level [4]. This represents a transition from binary blackspot classification towards quantitative injury prediction.

## 2.3 Road Segmentation

Road segmentation is the process of dividing a road network into analytical units so that accident observations and explanatory variables can be associated with defined locations.

The choice of segment length is important because it changes the spatial resolution of the analysis. A segment that is too long can combine sections with substantially different roadway and traffic characteristics. A segment that is too short can produce sparse accident observations and unstable estimates.

Fiorentini and Losa adopted a fixed-length criterion and divided the analysed network into 500 m road sites [1]. Each input factor was calculated for the corresponding road site. The network extended for 1190.136 km and consisted mainly of two-lane rural roads.

The resulting road-site definition was:

- 500 m fixed-length road unit;
- input variables calculated for each unit;
- at least one accident during 2012–2016 required for the Accident Case class;
- randomly selected zero-accident sites used to form the Non-Accident Case class.

This fixed-length approach is different from the spatial clustering approach described by Ghadi and Török. Their work investigates accident segmentation using linear referencing and K-means clustering, allowing the spatial distribution of accidents to influence the resulting segment length [5]. In their framework, a cluster can define a road section according to the locations of accidents rather than according to one predetermined physical length.

Therefore, road segmentation is itself a methodological decision. The fixed 500 m approach is convenient for systematic network-wide screening, whereas accident-based clustering can provide a variable spatial scale related to the observed distribution of accidents.

## 2.4 Roadway Geometric Factors

Road geometry describes the physical configuration of a road and can be represented by variables such as carriageway width, horizontal curvature, vertical curvature, slope and junction characteristics.

In the base study, the geometric database supplied by the Tuscany Region Road Administration included topology, curves and curve radii, slopes, lane width, and the type and location of junctions [1]. These data were converted into numerical or categorical input factors.

The principal geometric measures were:

- average carriageway width, Wc,j;
- average slope, Ij;
- horizontal tortuosity index, HTIj;
- vertical tortuosity index, VTIj;
- density of road junctions, DJj.

These variables attempt to transform physical roadway characteristics into numerical descriptors that can be processed by machine-learning algorithms.

The 2025 injury-count study provides another example of geometric representation. Its variables include section type, number of traffic lanes, radius and direction of horizontal alignment, slope or gradient, type of vertical curve and radius of vertical curve [4]. This demonstrates that road geometry can be represented at several levels of detail depending on the objective and data availability.

## 2.5 Traffic Flow Factors

Traffic exposure is an important component of road-safety analysis because the opportunity for accidents is related to the amount and composition of traffic using a road.

The base study uses Average Annual Daily Traffic (AADT) and driveway density as traffic-related inputs [1]. The five-year average AADT for road site j is defined in the paper as:

$$
AADT_j = \frac{1}{n}\sum_{i=1}^{n} AADT_{i,j}
$$

where n is the analysis period in years, equal to 5 in the study, and AADT_i,j is the annual average daily traffic for year i at road site j.

The 2025 injury-count study uses a much more detailed representation of traffic. Its variables include heavy-truck traffic, medium-heavy two-axle truck traffic, truck and semi-trailer traffic, tractor-trailer traffic, light-truck traffic, single and articulated bus traffic, motorcycle and moped traffic, bicycle traffic, and slow-vehicle or agricultural-tractor traffic [4].

This comparison illustrates an important principle: traffic volume can be represented by a single aggregate exposure measure such as AADT, or by a vehicle-composition vector containing several traffic streams.

## 2.6 Environmental and Spatial Factors

Environmental context can influence accident occurrence and can also explain why similar road geometries behave differently in different locations.

In the Fiorentini and Losa study, built-up-area information was used to classify each road site into three nominal area types [1]:

- RSO = Road Site Outside a built-up area;
- RSI = Road Site Inside a built-up area;
- RSB = Road Site at the administrative Boundary of a built-up area.

The area type was assigned values 1, 2 and 3 respectively.

The study therefore represents environmental context as a categorical input variable. This is significant because the same geometric condition may have a different operational environment depending on whether the road is inside an urban area, outside it, or at its boundary.

Other selected studies use environmental information differently. Yan and Shen include temperature, humidity, atmospheric pressure and visibility, together with traffic and point-of-interest variables [2]. The telematics-based study includes temporal, weather and behavioural information and uses interpretable machine learning to examine the contribution of these variables [6]. Thus, environmental variables may be static spatial descriptors, dynamic weather observations, or behavioural and temporal conditions.

## 2.7 Blackspots and Accident Hotspots

The terms blackspot and hotspot are related but should be used carefully.

A blackspot generally refers to a road location or section associated with an unusually high safety problem or elevated accident susceptibility. In the base study, the screening procedure is designed to identify road sites that are potentially susceptible to accident occurrence based on long-term accident history and explanatory variables [1].

A hotspot is more directly associated with spatial concentration or clustering of accident observations. GIS-based hotspot methods can determine whether high accident values are spatially clustered rather than randomly distributed.

The Faisalabad study demonstrates this spatial interpretation. The authors used Local Moran's I in ArcGIS to identify statistically significant clusters of accident observations. They reported 140 hotspots, with 117 at the 99% confidence level, 16 at the 95% level and 7 at the 90% level [3].

The distinction is useful for this seminar:

- blackspot screening emphasizes safety susceptibility of defined road sites;
- hotspot analysis emphasizes spatial clustering of accident observations;
- machine learning can be used to predict susceptibility or other accident-related outcomes;
- GIS can provide the spatial framework for locating and interpreting those outcomes.

## 2.8 Conventional Accident Analysis

Before machine-learning methods are introduced, accident analysis commonly relies on historical accident counts, rates, statistical models and engineering inspection.

Historical screening has an obvious advantage: it directly uses observed accident experience. However, it may be limited when a newly developed road site has little or no accident history. This issue motivates the base paper. Fiorentini and Losa seek to develop a screening procedure that can classify road sites according to their susceptibility using roadway, traffic and environmental characteristics, including sites that have not yet experienced a long-term crash history [1].

Another issue is regression to the mean and the dependence of observed accident counts on exposure. The supporting literature discussed by Fiorentini and Losa motivates the use of broader safety-analysis procedures rather than relying exclusively on raw accident frequency [1].

The machine-learning approach in the base paper therefore does not replace engineering judgement. It provides a screening layer that can reduce a large road network to a smaller set of sites requiring further investigation.

---

# CHAPTER 3 — MACHINE LEARNING AND GIS FOR ROAD SAFETY

## 3.1 Machine Learning in Transportation Engineering

Machine learning is used in the selected studies as a data-driven method for learning relationships between input variables and accident-related outcomes.

The general structure can be expressed as:

$$
X = (x_1,x_2,\ldots,x_m) \rightarrow f(X) \rightarrow \hat{Y}
$$

where X is the vector of input variables, f represents the trained model, and Ŷ is the predicted output.

The important point for road-safety analysis is that the output may have different meanings. In the base paper, Ŷ is a binary road-site class. In the Yan and Shen study it represents accident severity. In the segment-level study the response represents injury-count categories. In the Faisalabad study the output represents accident occurrence [1–4].

Consequently, model selection should follow the prediction problem rather than the other way around.

## 3.2 Supervised Learning

All five algorithms used in the Fiorentini and Losa base paper are supervised classification algorithms [1]. Supervised learning requires observations for which both input factors and output classes are known.

For a road-site dataset, one observation can be represented as:

$$
\mathbf{x}_j = [AT_j, AADT_j, W_{c,j}, I_j, HTI_j, VTI_j, DD_j, DJ_j]
$$

where the eight variables correspond to the eight input factors used in the base study.

The associated output class is:

$$
Y_j \in \{\text{Accident Case},\text{Non-Accident Case}\}
$$

The algorithm learns from labelled examples and then applies the learned relationship to previously unseen test observations.

This structure is different from unsupervised clustering. The Ghadi and Török study uses K-means to identify accident clusters without defining the final road segment solely through a pre-existing accident/non-accident label [5]. GIS hotspot analysis also has a different objective because it examines spatial association and clustering.

## 3.3 Classification and Regression

Classification assigns observations to discrete categories, while regression estimates a numerical outcome.

The Fiorentini and Losa paper is a classification study. Its output is binary. The Yan and Shen study is also a classification problem, although its target has three severity levels [1,2].

The segment-level injury-count paper demonstrates a different formulation in which machine-learning models are used to estimate severity-related counts [4]. Its evaluation includes MSE, RMSE and R² in addition to classification-oriented measures, illustrating the importance of matching evaluation metrics to the prediction task.

For this reason, accuracy alone is not sufficient for describing all machine-learning road-safety studies.

## 3.4 Logistic Regression

Logistic Regression (LR) is one of the five algorithms calibrated in the base paper.

The paper defines the logistic function as:

$$
P(z)=\frac{1}{1+e^{-z}}
$$

where P(z) represents the probability of the event.

The regression term is:

$$
z=b_0+b_1x_1+b_2x_2+\cdots+b_mx_m
$$

where b0 is the constant term, bi is the regression coefficient for input factor xi, and m is the number of independent variables [1].

The model converts a linear combination of inputs into a probability between 0 and 1. It is therefore useful for binary classification, but the paper notes limitations associated with a linear decision surface and possible overfitting.

## 3.5 Classification and Regression Tree

Classification and Regression Tree (CART) is a non-parametric tree-based method.

A CART model begins with a root node and repeatedly divides the dataset into more homogeneous groups using decision rules based on input variables. Terminal or leaf nodes contain the final class prediction.

The base paper reports that the initial CART developed during the study contained 256 decision rules and 257 leaf nodes. After pruning, the model was reduced to 7 decision rules and 8 leaf nodes [1].

Pruning is important because an excessively complex tree can fit the training data too closely and generalize poorly to unseen observations. The use of a pruned CART also provides a more directly interpretable decision structure than a large ensemble.

## 3.6 Random Forest

Random Forest (RF) is the central algorithm in the base paper and appears again in the supporting severity and injury-count studies.

The base paper describes RF as an ensemble of uncorrelated CART models. Two mechanisms are central:

1. bootstrap aggregation, in which different training samples are created through sampling with replacement;
2. feature randomness, in which a subset of input factors is considered as candidate split variables at each node [1].

For a classification problem, the final class is determined from the votes of the individual trees. Conceptually:

$$
\hat{Y}=\operatorname{mode}(\hat{Y}_1,\hat{Y}_2,\ldots,\hat{Y}_{N_t})
$$

where Nt is the number of trees and Ŷt is the class predicted by tree t.

In the base study, Nt was set to 500 because increasing the number of trees beyond this value did not produce a significant performance increase. The number of randomly selected candidate input factors, Nrs, was tested from 1 through 8, with Nrs = 8 selected in the study [1].

The appeal of RF in road-safety datasets is related to its ability to model nonlinear relationships, work with numerical and nominal variables, reduce sensitivity to individual-tree instability and provide an estimate of feature importance. The base paper also notes disadvantages: the ensemble is less directly interpretable than a single CART, training many trees can increase computational cost, and prediction is slower than for an individual classifier [1].

## 3.7 K-Nearest Neighbor

K-Nearest Neighbor (KNN) is an instance-based supervised classifier. Rather than deriving a separate discriminative function during training, KNN retains the training observations and classifies a new observation using its nearest neighbours.

The Euclidean distance between observations i and j in the feature space is defined in the base paper as:

$$
d_{ij}=\sqrt{\sum_{k=1}^{m}(x_{ik}-x_{jk})^2}
$$

where m is the number of independent variables. In the Fiorentini and Losa study, m = 8 [1].

The class of a new observation is determined from the majority class among its k nearest neighbours. The authors tested k values of 1, 2, 5, 10, 15, 20 and 25 and selected k = 10 according to the reported accuracy comparison [1].

The paper notes that KNN can become computationally expensive with large datasets and high-dimensional data, is sensitive to scaling, and can be affected by noise, missing values and outliers.

## 3.8 Naïve Bayes

Naïve Bayes (NB) is a probabilistic classifier based on Bayes' theorem.

The paper gives:

$$
P(C_k|x)=\frac{P(C_k)P(x|C_k)}{P(x)}
$$

where P(Ck|x) is the posterior probability of class Ck given the feature vector, P(Ck) is the prior probability, P(x|Ck) is the conditional probability of observing the feature vector given the class, and P(x) is the probability of observing the feature vector [1].

Under the Naïve Bayes independence assumption:

$$
P(C_k)P(x|C_k)=P(C_k)\prod_{i=1}^{n}P(x_i|C_k)
$$

The resulting maximum-a-posteriori decision rule is:

$$
\hat{z}=\arg\max_{k\in\{1,\ldots,K\}}
P(C_k)\prod_{i=1}^{n}P(x_i|C_k)
$$

The balanced dataset in the base study means that the prior probability for each of the two classes is 0.5 [1].

The authors identify several limitations, including the zero-frequency problem for unseen categorical combinations, the normal-distribution assumption for numerical variables, and the unrealistic nature of complete predictor independence.

## 3.9 Gradient Boosting

Gradient Boosting is not one of the five classifiers in the Fiorentini and Losa base study, but it appears in the 2025 segment-level injury-count study [4].

Gradient Boosting builds a sequence of weak learners, commonly shallow decision trees, with each successive learner improving the prediction made by the preceding ensemble.

Its inclusion in the supporting study is useful because it demonstrates that road-safety prediction is not restricted to the algorithms used in the base paper. The 2025 study compares Random Forest, KNN and Gradient Boosting for different injury-count outcomes [4].

## 3.10 XGBoost

XGBoost is another ensemble learning approach used in the telematics-based supporting study [6].

The study compared several classifiers and reported XGBoost as the model with the highest AUC in its model-evaluation stage, with an AUC of 91.70%. Random Forest and KNN were also reported as competitive, while Logistic Regression, Naïve Bayes and SVM produced lower AUC values in that study [6].

The importance of this result for the seminar is methodological rather than universal. A model that performs well on one dataset cannot automatically be assumed to perform equally well on another road network, time period or prediction target.

## 3.11 Bayesian Optimization

Bayesian optimization is discussed in the Yan and Shen study as a method for tuning Random Forest hyperparameters [2].

Random Forest performance depends partly on hyperparameter settings. Instead of manually selecting these values or conducting a large exhaustive grid search, Bayesian optimization can search the parameter space using information from previous evaluations.

Yan and Shen therefore developed a Bayesian-optimized Random Forest approach, referred to as BO-RF, for traffic-accident severity prediction [2].

This provides an important extension to the base study. Fiorentini and Losa use a trial-and-error approach for the key RF settings, while the later study applies a formal optimization strategy. The comparison illustrates how the model-development stage can evolve beyond simply choosing an algorithm.

## 3.12 Geographic Information Systems

GIS provides the spatial data-management and analysis framework required to associate accidents with physical road locations and environmental features.

In the base paper, GIS is used to match the accident, road, traffic and built-up-area information and to construct the machine-learning input database [1].

The basic GIS workflow can be represented as:

$$
\text{Accident data}
+
\text{Road network}
+
\text{Traffic data}
+
\text{Environmental data}
\rightarrow
\text{Spatially referenced road-site database}
$$

This database then becomes the input to the machine-learning workflow.

The Faisalabad study demonstrates a more explicit GIS hotspot workflow. Accident records from Rescue 1122 were screened, imported into ArcGIS and subjected to spatial analysis before field surveys and machine-learning prediction were undertaken [3].

## 3.13 Spatial Autocorrelation

Spatial autocorrelation describes the degree to which nearby observations are more similar or more dissimilar than would be expected under a random spatial arrangement.

It is particularly relevant to accident analysis because accidents occurring at nearby locations may not be independent. Traffic volume, road geometry, land use, intersections and other characteristics can create spatially related patterns.

The Faisalabad study used Local Moran's I to detect statistically significant clusters of accident observations [3]. This method enabled the researchers to distinguish hotspot and coldspot patterns instead of relying only on a visual map of accident points.

The study reported that the identified hotspots were concentrated around the General Transport Stand area and attributed this spatial pattern to high traffic and pedestrian activity around major bus facilities [3]. This interpretation is reported from the study and should not be treated as a universal causal rule.

## 3.14 Moran's I

Moran's I is a measure of spatial autocorrelation. In general form, global Moran's I can be expressed as:

$$
I=
\frac{N}{W}
\frac{\sum_i\sum_j w_{ij}(x_i-\bar{x})(x_j-\bar{x})}
{\sum_i(x_i-\bar{x})^2}
$$

where N is the number of spatial units, wij is the spatial-weight relationship between units i and j, W is the sum of spatial weights, xi is the observed value at location i, and x̄ is the mean value.

Local Moran's I applies the same spatial-association concept locally so that individual areas can be evaluated for cluster membership.

The selected GIS study uses Local Moran's I Static rather than relying on a simple accident-density map [3]. The output therefore contains a statistical interpretation of spatial clustering.

## 3.15 Integration of GIS and Machine Learning

The combination of GIS and machine learning creates a two-stage analytical framework.

Stage 1 is spatial preparation and analysis:

- collect accident locations;
- clean and geocode accident records;
- map the road network;
- assign accident records to road segments or spatial units;
- extract roadway and environmental characteristics;
- identify hotspots or clusters where required.

Stage 2 is machine-learning modelling:

- construct the input feature matrix;
- define the output variable;
- divide the dataset into training and testing portions;
- train one or more algorithms;
- validate and compare models;
- interpret the resulting predictions and important variables.

The base paper mainly integrates GIS into database preparation and road-site definition before classification [1]. The Faisalabad study places GIS hotspot identification before field investigation and machine-learning prediction [3]. The two approaches are complementary rather than identical.

A useful conceptual framework for the seminar is therefore:

$$
\text{Raw accident and road data}
\rightarrow
\text{GIS processing}
\rightarrow
\text{Road-site/feature database}
\rightarrow
\text{ML model}
\rightarrow
\text{Prediction}
\rightarrow
\text{Road-safety screening}
$$

This integrated structure is one of the main themes developed throughout the seminar.

---

# CHAPTER 4 — BASE PAPER: LONG-TERM ROAD BLACKSPOT SCREENING USING MACHINE LEARNING

## 4.1 Introduction to the Base Study

The principal base paper selected for this seminar is:

**Fiorentini, N. and Losa, M. (2020), “Long-Term-Based Road Blackspot Screening Procedures by Machine Learning Algorithms,” Sustainability, 12, 5972 [1].**

The study proposes a road blackspot screening procedure for two-lane rural roads using real long-term traffic and accident data and five supervised machine-learning algorithms.

The central objective is to determine whether road sites can be classified according to their susceptibility to accident occurrence using a combination of roadway, traffic and environmental variables.

The paper is particularly useful for this seminar because the methodology connects the complete chain of road-safety data processing:

$$
\text{Road network}
\rightarrow
\text{500 m road sites}
\rightarrow
\text{Accident and non-accident labels}
\rightarrow
\text{8 input factors}
\rightarrow
\text{ML classification}
\rightarrow
\text{validation}
\rightarrow
\text{blackspot screening}
$$

The study considers Logistic Regression, Classification and Regression Tree, Random Forest, K-Nearest Neighbor and Naïve Bayes. All five algorithms are trained and tested using the same training and test datasets so that their reported results can be compared on the same problem [1].

An important terminology point should be recorded. The methodology section of the paper clearly defines a road site with at least one accident as an “Accident Case” and a site with no accident as a “Non-Accident Case.” The abstract contains a parenthetical reversal of these labels when describing “likely safe” and “potentially susceptible” sites. In this seminar, the class definitions used in the methodology, data preparation and results are followed: Accident Case = at least one qualifying accident in 2012–2016; Non-Accident Case = no accident in that period [1].

## 4.2 Study Area

The study network is located in the Tuscany Region of central Italy and is managed by the Tuscany Region Road Administration (TRRA).

The network extends for approximately 1190.136 km and consists mainly of two-lane rural roads [1].

The accident database covers the five-year period from 2012 through 2016. Within the analysed network:

- 995 road sites experienced at least one accident;
- the recorded accidents at these sites totalled 5094;
- the accidents involved 7437 injuries;
- 113 deaths were reported;
- an equal number of 995 sites without accidents during the same period were randomly selected as Non-Accident Cases.

Thus, the final balanced dataset contains:

$$
995 + 995 = 1990\text{ road-site observations}
$$

The use of a balanced dataset is an explicit methodological decision. The authors state that an equal number of non-accident road sites were randomly selected to avoid potential class-imbalance issues that could affect machine-learning algorithms [1].

The study period also determines the temporal meaning of the prediction. The model does not predict whether an accident will occur tomorrow or next week. Instead, the classification represents susceptibility corresponding to the five-year accident-history framework used to create the labels.

## 4.3 Dataset Development

The dataset was constructed from four major categories of information [1]:

1. accident history;
2. roadway geometric data;
3. traffic-flow data;
4. built-up-area information.

Accident records included fatal and injury crashes occurring from 2012 to 2016. The paper notes that the crashes could include different accident types, occur during daytime or nighttime, occur on road segments or at junctions, involve one or more vehicles, and involve one or more casualties.

Property-damage-only crashes were excluded.

The roadway database contained topology, curves and curve radii, slopes, lane width, and junction information.

The traffic database contained AADT and driveway-density information.

The built-up-area database allowed the road network to be classified according to the relationship between the road site and built-up areas.

GIS was used to combine these datasets and create the independent variables for the machine-learning models [1].

### Table 4.1. Data categories used in the base study

| Data category | Information used |
|---|---|
| Accident history | Fatal and injury crashes, 2012–2016 |
| Road geometry | Topology, curves, radii, slopes, carriageway width, junctions |
| Traffic flow | AADT |
| Access characteristics | Driveway density |
| Environmental context | Built-up-area classification |
| Spatial processing | GIS-based matching and segmentation |

**Source:** Adapted from Fiorentini and Losa (2020) [1].

## 4.4 Road-Site Definition

The study uses a fixed-length road-site criterion.

The 1190.136 km network was divided into 500 m stretches, and each input factor was calculated for each road site [1].

The basic road-site representation can be written as:

$$
R_j=[x_{1,j},x_{2,j},\ldots,x_{8,j},Y_j]
$$

where j denotes the road site, x1 through x8 are the eight independent variables and Yj is the binary output class.

This segmentation has two important effects.

First, it creates a consistent spatial unit for the entire network. Each 500 m road site is represented by the same set of explanatory variables.

Second, it makes it possible to connect accident records to roadway characteristics. A GIS operation assigns the accidents recorded during the five-year period to their corresponding road sites.

The classification rule is:

$$
Y_j=
\begin{cases}
1, & \text{if at least one qualifying accident occurred at site }j\\
0, & \text{if no qualifying accident occurred at site }j
\end{cases}
$$

The labels are referred to in the paper as Accident Case and Non-Accident Case.

This is a screening classification rather than a direct accident-frequency model. The model does not estimate the number of accidents expected on a site; it estimates the class associated with the presence or absence of a long-term accident history.

## 4.5 Input Variables

The base paper uses eight input factors. They represent environmental context, traffic exposure, carriageway geometry, vertical alignment, horizontal alignment, access density and junction density.

### 4.5.1 Area Type

Area Type (AT) represents the relationship of the road site to a built-up area.

The three categories are:

- RSO = road site completely external to built-up areas, coded 1;
- RSI = road site completely inside built-up areas, coded 2;
- RSB = road site at the administrative boundary of built-up areas, coded 3 [1].

This is a nominal variable.

### 4.5.2 Average Annual Daily Traffic

The five-year average AADT is:

$$
AADT_j=
\frac{1}{n}\sum_{i=1}^{n}AADT_{i,j}
$$

For the base study:

$$
n=5
$$

Therefore, the variable represents the mean annual daily traffic associated with road site j over the five-year analysis period [1].

### 4.5.3 Average Carriageway Width

The average carriageway width is defined as:

$$
W_{c,j}=
\frac{\sum_{i=1}^{m}W_{c,i}L_i}{500}
$$

where Wc,i is the average carriageway width of segment i, Li is the segment length, m is the number of segments in the road site, and 500 m is the fixed road-site length [1].

The equation therefore produces a length-weighted average width for the 500 m road site.

### 4.5.4 Average Slope

The average slope is:

$$
I_j=
\frac{\sum_{i=1}^{m}i_iL_i}{500}
$$

where ii is the average slope of segment i and Li is its length [1].

Again, the calculation is length-weighted over the 500 m road site.

### 4.5.5 Horizontal Tortuosity Index

The Horizontal Tortuosity Index is defined as:

$$
HTI_j=
\frac{\sum_{i=1}^{r_p}\frac{1}{R_i}}
{\sum_{i=1}^{r_p}L_i}
$$

where Ri is the radius of the ith horizontal circular curve, rp is the number of circular-curve elements in the road site and Li is the associated segment length [1].

The variable provides a numerical representation of horizontal alignment complexity.

### 4.5.6 Vertical Tortuosity Index

The Vertical Tortuosity Index is:

$$
VTI_j=
\frac{\sum_{i=1}^{r_v}\frac{1}{R_{v,i}}}
{\sum_{i=1}^{r_v}L_i}
$$

where Rv,i is the radius of the ith vertical curve, rv is the number of vertical-curve elements and Li is the length of the corresponding segment [1].

This variable represents the vertical alignment characteristics of the road site.

### 4.5.7 Driveway Density

Driveway Density is defined as:

$$
DD_j=\frac{n_{d,j}}{500}
$$

where nd,j is the number of driveways in road site j [1].

The variable therefore represents the number of driveways per 500 m road site.

### 4.5.8 Density of Road Junctions

The Density of Road Junctions is:

$$
DJ_j=
\frac{\sum_{i=1}^{m}(\alpha_i n_{i,j})}{500}
$$

where ni,j is the number of junctions of type i in road site j and αi is a weighting factor associated with the junction type [1].

The paper states that α can be 5 for linear signalized and unsignalized intersections and 1 for roundabouts. The weighting values are related to Crash Modification Factors reported in the Highway Safety Manual [1].

### Table 4.2. Eight input factors in the base study

| Symbol | Input factor | Type/description |
|---|---|---|
| AT | Area Type | Nominal: RSO, RSI, RSB |
| AADTj | Average Annual Daily Traffic | Five-year average |
| Wc,j | Average carriageway width | Length-weighted average |
| Ij | Average slope | Length-weighted average |
| HTIj | Horizontal Tortuosity Index | Horizontal alignment measure |
| VTIj | Vertical Tortuosity Index | Vertical alignment measure |
| DDj | Driveway Density | Number of driveways per 500 m |
| DJj | Density of Road Junctions | Weighted junction density |

**Source:** Adapted from Fiorentini and Losa (2020) [1].

## 4.6 Descriptive Statistics of the Input Factors

The paper reports descriptive statistics for the training set, separated into Accident Case and Non-Accident Case observations.

### Table 4.3. Descriptive statistics reported for the training set

| Factor | Statistic | Accident Case | Non-Accident Case |
|---|---|---:|---:|
| DDj | Mean | 16.97 | 7.83 |
| DDj | Std. Dev. | 18.19 | 9.93 |
| DJj | Mean | 2.90 | 1.02 |
| DJj | Std. Dev. | 3.25 | 1.76 |
| VTIj | Mean | 74.54 | 73.65 |
| VTIj | Std. Dev. | 71.64 | 52.70 |
| Ij | Mean | 1.98 | 1.13 |
| Ij | Std. Dev. | 2.80 | 1.77 |
| HTIj | Mean | 284.35 | 384.25 |
| HTIj | Std. Dev. | 304.84 | 381.90 |
| Wc,j | Mean | 6.66 | 6.53 |
| Wc,j | Std. Dev. | 0.66 | 0.73 |
| AADTv | Mean | 8712 | 4334 |
| AADTv | Std. Dev. | 5378 | 3333 |

For Area Type, the training-set counts reported by the paper are:

| Area Type | Accident Case | Non-Accident Case |
|---|---:|---:|
| RSO–1 | 348 (38.3%) | 560 (61.7%) |
| RSI–2 | 180 (66.7%) | 90 (33.3%) |
| RSB–3 | 173 (78.3%) | 48 (21.7%) |

**Source:** Fiorentini and Losa (2020), Table 2 [1].

These descriptive values are not themselves causal effects. They show how the input variables were distributed between the two classes in the training data. For example, the mean AADT was higher in the Accident Case observations than in the Non-Accident Case observations in the reported training sample. Similarly, the mean driveway and junction densities were higher for the Accident Case class.

The tortuosity variables require more careful interpretation. The reported mean HTI is actually higher for the Non-Accident Case group than for the Accident Case group, while VTI is very similar between the two groups. These values demonstrate why individual-variable interpretation should not be confused with the performance of a multivariable classifier.

## 4.7 Output Classification

The response variable is binary crash-occurrence susceptibility.

The classification rule is based on the five-year accident history:

- Accident Case: at least one fatal or injury crash occurred in the 500 m site during 2012–2016;
- Non-Accident Case: no qualifying crash occurred during the same period.

The study therefore transforms a continuous road network into a labelled classification dataset.

### Table 4.4. Output classes

| Output class | Definition |
|---|---|
| Accident Case | At least one fatal or injury accident during 2012–2016 |
| Non-Accident Case | No qualifying accident during 2012–2016 |

Property-damage-only crashes were not included [1].

This distinction is important when interpreting the model. A prediction of Accident Case does not mean that an accident is certain to occur. It indicates that, based on the trained model and the selected input variables, the road site is classified in the susceptibility category associated with the accident-history class.

## 4.8 Balanced Dataset and Data Partitioning

The study initially identified 995 road sites with at least one qualifying accident. It then randomly selected 995 sites from the sites with no accident during the same five-year period [1].

The total balanced dataset is therefore:

$$
N=1990
$$

The dataset was randomly divided into:

$$
70\%\text{ training},\qquad 30\%\text{ testing}
$$

The reported test set contains 597 observations, while the training set contains 1393 observations.

The training set was used to develop and evaluate model goodness-of-fit through ten-fold cross-validation. The independent test set was reserved for evaluating predictive performance [1].

This separation is essential. If the same observations were used to both fit and assess the final model without a separate test set, the reported performance could overstate how well the model generalizes to new road sites.

## 4.9 Machine-Learning Algorithms Used

Five supervised classifiers were developed:

1. Logistic Regression (LR);
2. Classification and Regression Tree (CART);
3. Random Forest (RF);
4. K-Nearest Neighbor (KNN);
5. Naïve Bayes (NB).

### Table 4.5. Machine-learning algorithms in the base study

| Algorithm | Main category | Main principle in the study |
|---|---|---|
| LR | Parametric/probabilistic classifier | Logistic probability from linear combination of inputs |
| CART | Non-parametric tree classifier | Recursive partitioning |
| RF | Non-parametric ensemble | Bagged, randomized CART ensemble |
| KNN | Instance-based classifier | Majority class of nearest observations |
| NB | Probabilistic classifier | Bayes theorem with conditional-independence assumption |

The use of five algorithms allows the authors to compare different model structures on exactly the same road-site dataset.

## 4.10 Training Procedure and Hyperparameters

### Logistic Regression

LR uses the logistic function and linear predictor described earlier. It is relatively simple and provides a probabilistic interpretation, but the paper identifies the limitation that its decision surface is linear.

### CART

The initial CART contained 256 decision rules and 257 leaf nodes. Automatic pruning reduced the model to 7 decision rules and 8 leaf nodes [1].

This reduction illustrates the role of model complexity. The unpruned tree can represent highly specific relationships in the training data, while pruning removes lower-level structure to improve generalization.

### Random Forest

The base study identifies two main RF hyperparameters:

- Nt = number of CART models in the forest;
- Nrs = number of randomly selected input factors considered at each split.

The authors tested the values through a trial-and-error procedure. The final configuration used:

$$
N_t=500
$$

and:

$$
N_{rs}=8
$$

The choice of 500 trees was based on the observation that a higher number did not significantly improve RF performance. Nrs = 8 was selected after testing values from 1 to 8 [1].

### KNN

The paper tested:

$$
k\in\{1,2,5,10,15,20,25\}
$$

and selected:

$$
k=10
$$

based on the reported accuracy comparison [1].

The Euclidean distance was used.

### Naïve Bayes

No complex hyperparameter tuning is required in the formulation described by the paper. The model uses the posterior probability of each class and selects the class with the maximum posterior probability.

## 4.11 Ten-Fold Cross-Validation

The training dataset was evaluated using ten-fold cross-validation.

The procedure can be summarized as follows:

1. divide the training set into ten approximately equal folds;
2. use nine folds to train the classifier;
3. use the remaining fold for validation;
4. repeat the process until every fold has served as the validation fold;
5. combine the results to obtain a more representative assessment of model performance.

The study adopted ten-fold cross-validation following the approach described by the authors [1].

Cross-validation is particularly useful here because the training dataset is not extremely large. It allows all training observations to participate in both model fitting and validation, while preserving the separate 30% test set for the final predictive assessment.

## 4.12 Performance Evaluation

The base study uses a broad set of performance metrics:

- Accuracy;
- Precision;
- Recall;
- F1-Score;
- Confusion Matrix;
- Receiver Operating Characteristic (ROC);
- Area Under the ROC Curve (AUROC).

For binary classification:

### Accuracy

$$
Accuracy=
\frac{TP+TN}{TP+FP+TN+FN}
$$

### Precision

$$
Precision=
\frac{TP}{TP+FP}
$$

### Recall

$$
Recall=
\frac{TP}{TP+FN}
$$

### F1-Score

$$
F1=
\frac{2}{\frac{1}{Precision}+\frac{1}{Recall}}
$$

equivalently,

$$
F1=
\frac{2TP}{2TP+FP+FN}
$$

The paper defines TP as Accident Case observations correctly classified as Accident Case, TN as Non-Accident Case observations correctly classified as Non-Accident Case, FP as Non-Accident Case observations classified as Accident Case, and FN as Accident Case observations classified as Non-Accident Case [1].

For the ROC curve, the False Positive Rate is:

$$
FPR=
\frac{FP}{FP+TN}
$$

The ROC curve represents the relationship between True Positive Rate and False Positive Rate across classification thresholds.

AUROC ranges from 0 to 1 in the interpretation used by the paper. An AUROC of 0.5 corresponds to random-classifier performance, while an AUROC of 1 represents perfect discrimination [1].

## 4.13 Training-Phase Results

The paper reports Precision, Recall and F1-Score for each class and for the weighted average.

### Table 4.6. Precision, Recall and F1-Score in the training phase

| Model | Accident Case P | Accident Case R | Accident Case F1 | Non-Accident P | Non-Accident R | Non-Accident F1 | Weighted P | Weighted R | Weighted F1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| LR | 0.769 | 0.610 | 0.681 | 0.676 | 0.816 | 0.739 | 0.722 | 0.713 | 0.710 |
| CART | 0.747 | 0.672 | 0.707 | 0.701 | 0.771 | 0.734 | 0.724 | 0.721 | 0.721 |
| RF | 0.742 | 0.668 | 0.703 | 0.697 | 0.767 | 0.730 | 0.719 | 0.717 | 0.716 |
| KNN | 0.680 | 0.685 | 0.682 | 0.681 | 0.676 | 0.679 | 0.681 | 0.681 | 0.681 |
| NB | 0.786 | 0.532 | 0.634 | 0.645 | 0.855 | 0.735 | 0.716 | 0.693 | 0.685 |

**Source:** Fiorentini and Losa (2020), Table 3 [1].

The highest weighted-average F1-score in the training phase was reported for CART at 0.721. This does not determine the final model selection because the independent test phase is more important for assessing generalization.

## 4.14 Testing-Phase Results

The independent test set provides the principal evidence of predictive performance.

### Table 4.7. Precision, Recall and F1-Score in the testing phase

| Model | Accident Case P | Accident Case R | Accident Case F1 | Non-Accident P | Non-Accident R | Non-Accident F1 | Weighted P | Weighted R | Weighted F1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| LR | 0.731 | 0.650 | 0.688 | 0.688 | 0.763 | 0.724 | 0.709 | 0.707 | 0.706 |
| CART | 0.754 | 0.630 | 0.686 | 0.685 | 0.797 | 0.737 | 0.719 | 0.714 | 0.712 |
| RF | 0.746 | 0.710 | 0.728 | 0.726 | 0.760 | 0.743 | 0.736 | 0.735 | 0.735 |
| KNN | 0.680 | 0.667 | 0.673 | 0.676 | 0.690 | 0.683 | 0.678 | 0.678 | 0.678 |
| NB | 0.758 | 0.529 | 0.623 | 0.641 | 0.833 | 0.725 | 0.699 | 0.682 | 0.674 |

**Source:** Fiorentini and Losa (2020), Table 4 [1].

The weighted-average Precision, Recall and F1-Score of RF are all 0.736, 0.735 and 0.735 respectively. The paper therefore identifies RF as the strongest classifier in the reported test-phase comparison [1].

It is important to distinguish this source-specific result from a general statement that Random Forest will always outperform the other algorithms. The authors themselves note that the other classifiers can perform better in other research settings.

## 4.15 Confusion-Matrix Results

The confusion matrix gives the number of correct and incorrect classifications for each class.

### Table 4.8. Testing-phase confusion matrices

| Model | TP: Accident correctly classified | FN: Accident classified as Non-Accident | FP: Non-Accident classified as Accident | TN: Non-Accident correctly classified | Correctly classified | Accuracy |
|---|---:|---:|---:|---:|---:|---:|
| LR | 193 | 104 | 71 | 229 | 422 | 70.69% |
| CART | 187 | 110 | 61 | 239 | 426 | 71.35% |
| RF | 211 | 86 | 72 | 228 | 439 | 73.53% |
| KNN | 198 | 99 | 93 | 207 | 405 | 67.84% |
| NB | 157 | 140 | 50 | 250 | 407 | 68.17% |

**Source:** Fiorentini and Losa (2020), Table 6 [1].

For RF, the test confusion matrix is:

|  | Predicted Accident | Predicted Non-Accident |
|---|---:|---:|
| Observed Accident | 211 | 86 |
| Observed Non-Accident | 72 | 228 |

The total is:

$$
211+86+72+228=597
$$

and the number correctly classified is:

$$
211+228=439
$$

Therefore:

$$
Accuracy=\frac{439}{597}\times100=73.53\%
$$

This reproduces the reported RF test accuracy.

The matrix also shows that 86 of the 297 observed Accident Case observations in the test set were classified as Non-Accident, while 72 of the 300 observed Non-Accident observations were classified as Accident.

For a road-safety screening application, both types of error matter. A false negative means a site with the observed Accident Case label is classified as Non-Accident, while a false positive means a Non-Accident Case is flagged as Accident Case. The practical cost assigned to these errors would depend on the purpose and decision context of the road authority.

## 4.16 ROC and AUROC Results

The paper evaluates ROC curves for both training and testing phases.

### Table 4.9. AUROC values reported by the base study

| Model | Training AUROC | Test AUROC |
|---|---:|---:|
| LR | 0.766 | 0.773 |
| CART | 0.763 | 0.742 |
| RF | 0.783 | 0.795 |
| KNN | 0.757 | 0.740 |
| NB | 0.749 | 0.747 |

**Source:** Fiorentini and Losa (2020), Table 7 [1].

RF has a training AUROC of 0.783 and a test AUROC of 0.795.

The test AUROC is higher than the training AUROC in the reported values. More importantly, the training and test values are reasonably close for all five models. The authors interpret the similarity between training and test performance as evidence that the models do not suffer from significant overfitting in this study [1].

The AUROC values also show that the models are not perfect classifiers. The best reported test AUROC is 0.795, not 1.0. Thus, the model should be interpreted as a screening tool with useful discrimination rather than as a deterministic accident predictor.

## 4.17 Overall Model Comparison

The principal reported test-phase results are summarized below.

### Table 4.10. Comparison of test-phase performance

| Model | Accuracy | Weighted Precision | Weighted Recall | Weighted F1 | AUROC |
|---|---:|---:|---:|---:|---:|
| LR | 70.69% | 0.709 | 0.707 | 0.706 | 0.773 |
| CART | 71.35% | 0.719 | 0.714 | 0.712 | 0.742 |
| RF | 73.53% | 0.736 | 0.735 | 0.735 | 0.795 |
| KNN | 67.84% | 0.678 | 0.678 | 0.678 | 0.740 |
| NB | 68.17% | 0.699 | 0.682 | 0.674 | 0.747 |

**Source:** Compiled from Fiorentini and Losa (2020), Tables 4, 6 and 7 [1].

The table shows that RF has the highest reported test accuracy, weighted Precision, weighted Recall, weighted F1-Score and AUROC among the five algorithms in this particular dataset.

CART has the highest weighted F1-score in the training phase, but RF has the highest weighted F1-score in the independent test phase. This difference demonstrates why model selection should not be based only on training performance.

## 4.18 Why Random Forest Performed Strongly in the Base Study

The reported RF result can be understood in relation to the structure of the road-safety dataset.

First, the input variables contain both numerical and nominal information. Area Type is categorical, while AADT, carriageway width, slope, tortuosity and density measures are numerical. RF can accommodate this mixed feature structure.

Second, the relationships between road characteristics and accident susceptibility need not be linear. For example, the combined effect of traffic volume, road width and junction density may not be represented adequately by a single linear relationship.

Third, individual decision trees can be unstable. Random Forest reduces dependence on one tree by combining many trees developed using bootstrap samples and feature randomness.

Fourth, the dataset contains several roadway variables that can interact. The ensemble approach can represent complex combinations of input variables without requiring the analyst to specify every interaction explicitly.

The base paper also identifies RF's ability to provide feature-importance estimation through the Out-of-Bag Error and its relative resistance to overfitting through bagging and feature randomness [1].

These are methodological advantages, not guarantees of superior performance on all datasets.

## 4.19 Interpretation of the Input-Factor Statistics

The descriptive statistics provide useful context for understanding the classification problem.

The Accident Case training observations have a mean AADT of 8712 compared with 4334 for the Non-Accident Case group. The mean driveway density is 16.97 compared with 7.83, and the mean junction density is 2.90 compared with 1.02 [1].

The Area Type distribution also differs. In the training set, 66.7% of RSI observations and 78.3% of RSB observations belong to the Accident Case group, whereas 38.3% of RSO observations belong to that group [1].

However, these statistics should not be interpreted as isolated causal relationships. They are descriptive summaries of the model-development data. The machine-learning classifier considers all input factors jointly.

For example, the mean horizontal tortuosity index is higher in the Non-Accident Case group than in the Accident Case group in the reported training data. Therefore, simply assuming that greater horizontal tortuosity always corresponds to greater accident susceptibility would not be supported by this table.

The correct interpretation is that the model learns a multivariable classification boundary from the complete set of features.

## 4.20 Goodness-of-Fit Versus Predictive Performance

One of the useful aspects of the base paper is the explicit separation between training and testing performance.

Goodness-of-fit refers to how well the model represents the training data.

Predictive performance refers to how well the trained model classifies previously unseen observations in the test set.

If a model has substantially better training performance than test performance, overfitting may be present. In the base paper, the training and testing metrics are comparatively close for the five classifiers. The authors therefore report no significant overfitting issue [1].

For RF:

$$
F1_{train}=0.716
$$

and:

$$
F1_{test}=0.735
$$

for the weighted average.

Similarly:

$$
AUROC_{train}=0.783
$$

and:

$$
AUROC_{test}=0.795
$$

The test values are not lower than the training values for these two metrics in the reported results.

This does not prove that the model is universally robust. It only describes the observed relationship between the training and test results in the dataset used by the authors.

## 4.21 Practical Screening Workflow

The practical workflow proposed by the study can be represented in the following sequence:

1. obtain road-network geometry and accident records;
2. collect traffic and built-up-area information;
3. integrate the datasets using GIS;
4. divide the road network into 500 m road sites;
5. calculate the eight input factors for every road site;
6. assign Accident Case or Non-Accident Case labels;
7. randomly select equal numbers of non-accident sites to balance the dataset;
8. divide the observations into 70% training and 30% testing sets;
9. develop LR, CART, RF, KNN and NB models;
10. use ten-fold cross-validation for the training phase;
11. evaluate the models using Accuracy, Precision, Recall, F1-Score, confusion matrices, ROC and AUROC;
12. evaluate final predictive performance using the independent test set;
13. use the screening output to identify road sites requiring further inspection.

This workflow is important because the model is not the first step. Data definition, segmentation, feature calculation and class definition occur before machine-learning training.

## 4.22 Potential Application to Road-Authority Decision Making

The authors propose using machine-learning classifiers as a supporting tool for road-authority decision making.

The proposed application is not to allow the algorithm to make the final engineering decision. Instead, the model can produce a restricted list of potentially susceptible road sites. These sites can then be assigned higher priority for inspection, maintenance assessment or further engineering investigation [1].

The practical chain is therefore:

$$
\text{Large road network}
\rightarrow
\text{ML screening}
\rightarrow
\text{restricted set of potentially hazardous sites}
\rightarrow
\text{engineering inspection}
\rightarrow
\text{possible intervention}
$$

This is particularly useful where the available inspection and maintenance resources are limited.

The paper also emphasizes that the approach could potentially classify new road sites or sites without a long-term crash history. This is one of the principal reasons the method extends beyond simple historical blackspot counting.

## 4.23 Relationship Between the Base Paper and GIS

GIS performs several functions in the base study.

First, it allows accident locations to be matched to the road network.

Second, it enables the road network to be divided into fixed 500 m road sites.

Third, it allows built-up-area information to be overlaid on the road network so that Area Type can be assigned.

Fourth, it provides the spatial structure necessary for combining geometry, traffic and accident data.

The GIS component can therefore be viewed as the bridge between raw spatial data and the tabular machine-learning dataset.

Without this spatial matching stage, an accident record would not automatically be associated with the correct road-site geometry, traffic exposure or environmental category.

## 4.24 Limitations of the Base Study

The base paper provides a complete screening framework, but its limitations must be considered when interpreting the results.

### 4.24.1 Study-area limitation

The network consists mainly of two-lane rural roads in Tuscany. Therefore, the reported 73.53% RF accuracy is a result for this specific network, dataset and modelling procedure. It should not be assumed to represent the accuracy that would be obtained on urban roads, motorways or roads in another country.

### 4.24.2 Five-year response definition

The output label is based on whether at least one qualifying accident occurred during 2012–2016. The model therefore represents a five-year susceptibility classification rather than a short-term accident forecast.

### 4.24.3 Binary outcome

The Accident Case/Non-Accident Case formulation loses information about the number and severity of accidents. A road site with one qualifying accident and a road site with many qualifying accidents can both receive the same Accident Case label.

This limitation is directly relevant to the supporting papers. The 2025 study demonstrates a more detailed approach to fatal, serious and slight injury counts [4], while Yan and Shen explicitly model severity levels [2].

### 4.24.4 Balanced sampling

The authors randomly selected 995 non-accident road sites to match the 995 Accident Case sites [1]. This produces a balanced classification problem, but the resulting class proportions do not necessarily represent the natural proportion of accident and non-accident road sites in the complete road network.

Consequently, the reported accuracy should be interpreted within the study's balanced modelling framework.

### 4.24.5 Feature availability

The eight variables depend on detailed road-administration data. A road authority without reliable geometry, traffic, junction, driveway and built-up-area datasets may not be able to reproduce the method directly.

### 4.24.6 Model interpretability

A single CART can be visualized through decision rules, while RF is an ensemble of many trees. The RF therefore provides less direct interpretability than one small decision tree [1].

### 4.24.7 Potential spatial dependence

The observations are road sites located along a continuous network. Nearby road sites may share traffic, geometry and environmental characteristics. A random train/test split may therefore not fully represent the difficulty of transferring the model to a geographically separate road network. This issue is a methodological consideration for future research rather than a reported failure of the study.

## 4.25 Significance of the Base Paper for the Seminar

The Fiorentini and Losa study provides the core framework around which the remainder of this seminar can be organized.

Its importance lies in the complete integration of:

- long-term accident history;
- road segmentation;
- GIS-based data integration;
- geometric variables;
- traffic variables;
- environmental classification;
- balanced supervised learning;
- multiple machine-learning algorithms;
- ten-fold cross-validation;
- independent test evaluation;
- confusion-matrix analysis;
- ROC/AUROC assessment;
- practical road-authority screening.

The supporting papers extend this framework rather than replacing it.

Ghadi and Török contribute an alternative approach to road segmentation and accident clustering [5].

Yan and Shen extend the Random Forest concept into accident-severity prediction and Bayesian hyperparameter optimization [2].

The telematics-based study extends the feature space into temporal, weather and behavioural information and adds SHAP and partial-dependence interpretation [6].

The segment-level injury-count study extends the prediction target from binary accident occurrence to severity-related injury counts and uses RF, KNN and Gradient Boosting [4].

Khan and Hussain demonstrate a GIS-first workflow in which Local Moran's I identifies spatial hotspots before field investigation and machine-learning accident prediction [3].

Thus, the base paper serves as the methodological foundation, while the other studies demonstrate how the same broad data-driven road-safety concept can be adapted to different spatial scales, prediction targets, feature sets and modelling techniques.

## 4.26 Chapter Summary

The Fiorentini and Losa base study develops a long-term road blackspot screening procedure using five supervised machine-learning classifiers. The study network covers approximately 1190.136 km of mainly two-lane rural roads in Tuscany. Accident records from 2012–2016 were linked to 500 m road sites using GIS. The final balanced dataset contains 995 Accident Case sites and 995 randomly selected Non-Accident Case sites.

Eight input factors were constructed:

1. Area Type;
2. Average Annual Daily Traffic;
3. Average Carriageway Width;
4. Average Slope;
5. Horizontal Tortuosity Index;
6. Vertical Tortuosity Index;
7. Driveway Density;
8. Density of Road Junctions.

The dataset was divided into 70% training and 30% testing observations. Ten-fold cross-validation was used in the training phase. LR, CART, RF, KNN and NB were compared using Accuracy, Precision, Recall, F1-Score, confusion matrices, ROC and AUROC.

In the reported independent test results, RF achieved 73.53% accuracy, weighted Precision of 0.736, weighted Recall of 0.735, weighted F1-Score of 0.735 and AUROC of 0.795 [1]. The authors reported that the training and test results were sufficiently similar to indicate no significant overfitting in their modelling procedure.

The main methodological lesson is that machine learning is only one part of the road-safety workflow. The quality of the output depends on how the road network is segmented, how accident records are labelled, how geometric and traffic variables are calculated, how the dataset is balanced and divided, and how model performance is evaluated.

For the remainder of the seminar, this framework will be used as the reference point for comparing the five supporting studies.

---

# References Used in Part 2

[1] Fiorentini, N., and Losa, M. (2020). “Long-Term-Based Road Blackspot Screening Procedures by Machine Learning Algorithms.” Sustainability, 12, 5972.

[2] Yan, X., and Shen, Y. (2022). “Traffic Accident Severity Prediction Based on Random Forest.” Sustainability, 14, 1729.

[3] Khan, A. A., and Hussain, J. (2024). “Utilizing GIS and Machine Learning for Traffic Accident Prediction in Urban Environment.” Civil Engineering Journal, 10(6).

[4] Hamdan, M., and Sipos, T. (2025). “Predicting Segment-Level Road Traffic Injury Counts Using Machine Learning Models.” Future Transportation, 5, 197.

[5] Ghadi, M., and Török, Á. (2020). “Evaluation of the Impact of Spatial and Environmental Factors on Road Accident Severity.” Periodica Polytechnica Transportation Engineering.

[6] Golestani et al. (2025). “Interpretable Machine Learning for Traffic Accident Hotspot Prediction Using Telematics, Temporal and Weather-Related Information.” PLOS ONE, 2025.

---

## Source and Figure Insertion Notes for the Final Report

The following figures should be inserted into the final seminar document after the text is reviewed:

- Fig. 3: Fiorentini and Losa workflow.
- Fig. 4: Tuscany Region road network analysed in the base paper.
- Fig. 5: Conceptual classification of Accident Case and Non-Accident Case road sites.
- Fig. 6: Training/testing and ten-fold cross-validation structure.
- Fig. 7: Pruned CART structure reported by Fiorentini and Losa.
- Fig. 8: Conceptual Random Forest ensemble structure.
- Fig. 9: ROC curves for the training phase.
- Fig. 10: ROC curves for the testing phase.
- Fig. 11: GIS and Local Moran's I hotspot workflow from the supporting study.
- Fig. 12: Integrated GIS–machine-learning road-safety framework.

All reproduced or adapted figures must retain source attribution and should be checked against the original paper before final submission. Tables in this chapter are intentionally written as seminar-ready adaptations of the reported numerical results rather than as unverified redrawings of the original page layout.
