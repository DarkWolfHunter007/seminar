# Part 1 — Seminar Report

## Front Matter and Abstract

### Cover Page

**[COLLEGE NAME]**

**[NAME OF DEPARTMENT]**

**[UNIVERSITY NAME]**

**SEMINAR REPORT**

ON

# MACHINE LEARNING AND SPATIAL ANALYTICS FOR ROAD TRAFFIC ACCIDENT PREDICTION, SEVERITY MODELING, AND BLACKSPOT IDENTIFICATION

Submitted by

**[NAME]**

**[REGISTER NUMBER]**

Under the guidance of

**[GUIDE NAME]**

**[DESIGNATION OF GUIDE]**

in partial fulfillment of the requirements for the award of the degree of

**BACHELOR OF TECHNOLOGY**

in

**CIVIL ENGINEERING**

**[ACADEMIC YEAR]**

---

## Title Page

# MACHINE LEARNING AND SPATIAL ANALYTICS FOR ROAD TRAFFIC ACCIDENT PREDICTION, SEVERITY MODELING, AND BLACKSPOT IDENTIFICATION

A Seminar Report submitted to

**[UNIVERSITY NAME]**

in partial fulfillment of the requirements for the award of the degree of

**BACHELOR OF TECHNOLOGY**

in

**CIVIL ENGINEERING**

Submitted by

**[NAME]**

**[REGISTER NUMBER]**

Under the guidance of

**[GUIDE NAME]**

**[DESIGNATION]**

**[DEPARTMENT OF CIVIL ENGINEERING]**

**[COLLEGE NAME]**

**[PLACE]**

**[MONTH, YEAR]**

---

## Certificate

This is to certify that the seminar report entitled **“MACHINE LEARNING AND SPATIAL ANALYTICS FOR ROAD TRAFFIC ACCIDENT PREDICTION, SEVERITY MODELING, AND BLACKSPOT IDENTIFICATION”** is a bonafide record of the seminar work carried out by **[NAME]**, **[REGISTER NUMBER]**, student of **[PROGRAMME / SEMESTER]**, Department of Civil Engineering, **[COLLEGE NAME]**, under my guidance and supervision during the academic year **[ACADEMIC YEAR]**.

The seminar report is submitted in partial fulfillment of the requirements for the award of the degree of Bachelor of Technology in Civil Engineering under **[UNIVERSITY NAME]**.

**[GUIDE NAME]**  
Seminar Guide

**[HEAD OF DEPARTMENT]**  
Head of the Department

**[PLACE]**

**[DATE]**

---

## Acknowledgment

I express my sincere gratitude to **[PRINCIPAL NAME]**, Principal, **[COLLEGE NAME]**, for providing the facilities and academic environment necessary for the completion of this seminar.

I am grateful to **[HEAD OF DEPARTMENT]**, Head of the Department of Civil Engineering, for the support and encouragement provided throughout the preparation of this report.

I sincerely thank **[GUIDE NAME]**, **[DESIGNATION]**, Department of Civil Engineering, for the valuable guidance, suggestions and supervision provided during the preparation of this seminar. The discussions and technical suggestions received during the course of this work were helpful in developing a structured understanding of machine-learning and spatial-analysis approaches used in road safety research.

I also acknowledge the authors and publishers of the research papers used as the principal technical sources for this seminar. Their research on accident prediction, accident severity, injury-count prediction, GIS-based hotspot identification and machine-learning-based blackspot screening provided the foundation for the preparation of this report.

Finally, I express my gratitude to my teachers, friends and family members for their support and encouragement during the preparation of this seminar report.

---

## Abstract

Road traffic accidents are influenced by a combination of roadway geometry, traffic characteristics, environmental conditions, spatial factors and human behaviour. Conventional road-safety analysis has traditionally relied heavily on historical accident records and statistical procedures for identifying hazardous locations. With the increasing availability of spatial, traffic and accident datasets, machine-learning techniques and Geographic Information Systems have emerged as important tools for identifying accident-prone locations, estimating injury or accident severity and supporting road-safety decision-making.

This seminar presents a literature-based study of machine learning and spatial analytics techniques used for road traffic accident prediction, severity modelling and blackspot identification. The principal methodological framework is based on the long-term road blackspot screening procedure proposed by Fiorentini and Losa, in which road sites are classified according to their susceptibility to accident occurrence using roadway, traffic and environmental variables. Their study considered approximately 1200 km of two-lane rural roads in Tuscany, Italy, and compared Logistic Regression, Classification and Regression Tree, Random Forest, K-Nearest Neighbor and Naïve Bayes classifiers. The study used 995 accident cases and an equal number of randomly selected non-accident cases, followed by a 70% training and 30% testing division and ten-fold cross-validation. Random Forest achieved an overall accuracy of 73.53% in the reported comparison.

The supporting studies extend this framework in several directions. Spatial and environmental factors have been investigated in relation to accident severity; telematics and meteorological information have been combined with interpretable machine learning for accident-hotspot analysis; machine-learning models have been applied to predict segment-level injury counts; Bayesian-optimized Random Forest has been used for accident-severity classification; and GIS-based spatial autocorrelation has been combined with machine learning for urban accident prediction. Together, these studies demonstrate how accident analysis can move from simple historical identification towards data-driven prediction, spatial interpretation and severity assessment.

The seminar therefore examines the principles of machine learning and GIS in road safety, the datasets and variables used by the selected studies, the major algorithms employed, their evaluation methods and their practical implications for road-safety management. Particular attention is given to Random Forest because of its repeated application across the selected research and its ability to model nonlinear relationships between road characteristics and accident-related outcomes.

---

## Table of Contents

Certificate

Acknowledgment

Table of Contents

List of Tables

List of Figures

Abstract

**1. INTRODUCTION**

1.1 Background

1.2 Road Traffic Accidents and Road Safety

1.3 Need for Data-Driven Accident Analysis

1.4 Role of Machine Learning in Road Safety

1.5 Role of Geographic Information Systems

1.6 Need for Blackspot Identification

1.7 Problem Statement

1.8 Objectives of the Seminar

1.9 Scope of the Seminar

1.10 Organization of the Report

**2. FUNDAMENTALS OF ROAD TRAFFIC ACCIDENT ANALYSIS**

2.1 Road Traffic Accident Characteristics

2.2 Accident Frequency and Severity

2.3 Road Segmentation

2.4 Roadway Geometric Factors

2.5 Traffic Flow Factors

2.6 Environmental and Spatial Factors

2.7 Blackspots and Accident Hotspots

2.8 Conventional Accident Analysis

**3. MACHINE LEARNING AND GIS FOR ROAD SAFETY**

3.1 Machine Learning in Transportation Engineering

3.2 Supervised Learning

3.3 Classification and Regression

3.4 Logistic Regression

3.5 Decision Trees and CART

3.6 Random Forest

3.7 K-Nearest Neighbor

3.8 Naïve Bayes

3.9 Gradient Boosting

3.10 XGBoost

3.11 Bayesian Optimization

3.12 Geographic Information Systems

3.13 Spatial Autocorrelation

3.14 Moran’s I

3.15 Integration of GIS and Machine Learning

**4. BASE PAPER: LONG-TERM ROAD BLACKSPOT SCREENING USING MACHINE LEARNING**

4.1 Introduction to the Base Study

4.2 Study Area

4.3 Dataset Development

4.4 Road-Site Definition

4.5 Input Variables

4.6 Output Classification

4.7 Machine-Learning Algorithms

4.8 Training and Testing Procedure

4.9 Ten-Fold Cross-Validation

4.10 Performance Evaluation

4.11 Results

4.12 Importance of Random Forest

4.13 Practical Application

4.14 Limitations of the Base Study

**5. SUPPORTING STUDIES**

5.1 Spatial and Environmental Factors Affecting Accident Severity

5.2 Interpretable Machine Learning for Accident Hotspots

5.3 Segment-Level Road Traffic Injury Prediction

5.4 Random Forest for Accident Severity Prediction

5.5 GIS and Machine Learning for Urban Accident Prediction

**6. COMPARATIVE ANALYSIS OF THE SIX STUDIES**

6.1 Comparison of Study Objectives

6.2 Comparison of Datasets

6.3 Comparison of Input Variables

6.4 Comparison of Machine-Learning Algorithms

6.5 Comparison of Spatial Analysis Techniques

6.6 Comparison of Prediction Targets

6.7 Model Evaluation Methods

6.8 Role of Random Forest

6.9 Role of GIS

6.10 Interpretability of Machine-Learning Models

**7. APPLICATIONS, CHALLENGES AND FUTURE SCOPE**

7.1 Applications in Road Safety Management

7.2 Identification of High-Risk Road Segments

7.3 Road Infrastructure Planning

7.4 Traffic Management

7.5 Limitations of Machine-Learning-Based Accident Prediction

7.6 Data Quality and Availability

7.7 Spatial and Temporal Transferability

7.8 Model Interpretability

7.9 Future Scope

**8. CONCLUSION**

References

---

## List of Tables

Table 1.1 Research papers considered in the seminar

Table 4.1 Input factors used in the base study

Table 4.2 Descriptive statistics of input factors

Table 4.3 Classification of accident and non-accident road sites

Table 4.4 Machine-learning algorithms considered in the base study

Table 4.5 Performance measures used for model evaluation

Table 5.1 Characteristics of the supporting studies

Table 6.1 Comparison of datasets used in the six studies

Table 6.2 Comparison of prediction targets

Table 6.3 Comparison of machine-learning methods

Table 6.4 Comparison of spatial-analysis methods

Table 6.5 Summary of major findings

---

## List of Figures

Fig. 1. Conceptual framework of machine-learning-based road safety analysis

Fig. 2. General workflow of road accident prediction and blackspot identification

Fig. 3. Workflow of the base paper

Fig. 4. Study road network considered in the base paper

Fig. 5. Classification of road sites into accident and non-accident cases

Fig. 6. Machine-learning model development and validation procedure

Fig. 7. Conceptual structure of a Random Forest model

Fig. 8. GIS-based accident hotspot identification framework

Fig. 9. Spatial distribution of accident hotspots

Fig. 10. Workflow of the GIS and machine-learning supporting study

Fig. 11. Conceptual framework for accident severity prediction

Fig. 12. Comparative framework of the six studies

The final figure numbering will be adjusted after the actual source figures are selected and inserted. Every figure used from a paper will be accompanied by its source and original paper/page information.

---

# CHAPTER 1 — INTRODUCTION

## 1.1 Background

Road transportation is an essential component of modern infrastructure because it provides mobility for people and facilitates the movement of goods between residential, commercial and industrial areas. The effectiveness of a road transportation system, however, depends not only on mobility but also on safety. Traffic accidents can result in fatalities, injuries, property damage, congestion and significant social and economic consequences. Consequently, identifying locations and conditions associated with increased accident risk is an important component of transportation engineering and road-safety management.

Traditional road-safety investigations have generally relied on historical accident records, statistical models and engineering inspection of locations with relatively high accident frequencies. Such methods remain important, but the increasing availability of detailed traffic, geometric, environmental and spatial datasets has created opportunities for more data-driven approaches. Machine learning can identify relationships between multiple explanatory variables and accident-related outcomes without requiring the relationships to be represented entirely through conventional statistical assumptions.

The six research studies considered in this seminar demonstrate different applications of this approach. The studies address long-term blackspot screening, spatial and environmental influences on accident severity, telematics-based accident-hotspot prediction, segment-level injury-count prediction, Random Forest-based accident-severity classification and GIS-based urban accident prediction. The research corpus therefore provides a broad basis for examining the relationship between machine learning, spatial analysis and road safety.

Among these studies, the work of Fiorentini and Losa provides the principal framework for this seminar because it directly addresses long-term road blackspot screening using multiple machine-learning algorithms. The study considers road sites as the basic analytical units and combines accident history with roadway, traffic and environmental information.

The importance of this framework is that blackspot identification is not treated simply as a process of counting previous accidents. Instead, the road network is transformed into defined road segments, relevant characteristics are extracted for each segment, and machine-learning models are trained to classify sites according to accident susceptibility. This provides a useful connection between conventional road-safety engineering and modern data-driven prediction.

## 1.2 Road Traffic Accidents and Road Safety

Road traffic accidents occur through the interaction of roadway, vehicle, traffic, environmental and human factors. The characteristics of an accident may vary substantially according to location, road geometry, traffic volume, weather, time and surrounding land use. Consequently, a road network cannot always be assessed adequately using a single explanatory variable.

The long-term blackspot study demonstrates this multidimensional nature of accident analysis. Its database incorporated accident history, geometric characteristics, traffic flow and built-up-area information. Geometric information included characteristics such as road topology, curves, radius, slopes, lane width and junction characteristics, while traffic information included Average Annual Daily Traffic and driveway density.

The study also incorporated environmental context by classifying road sites according to whether they were inside, outside or at the boundary of built-up areas. This approach demonstrates why road accident prediction can benefit from integrating multiple sources of information rather than relying solely on accident counts.

## 1.3 Need for Data-Driven Accident Analysis

A major difficulty in road-safety management is that accident events are relatively infrequent when compared with the total number of vehicle movements and road-site observations. At the same time, accident occurrence is affected by several interacting factors. A road segment may have a particular combination of traffic volume, road width, curvature, slope, junction density and surrounding development that cannot be adequately represented by a single variable.

Machine-learning techniques provide an approach for analysing such multidimensional datasets. In the base study, the roadway was divided into 500 m stretches and the relevant input factors were calculated for each road site. The resulting database contained 995 accident cases and an equal number of randomly selected non-accident cases.

The use of equal numbers of accident and non-accident cases was intended to reduce potential problems associated with imbalanced classes. The resulting dataset was divided into training and testing portions, while ten-fold cross-validation was used during model development. Performance was assessed using precision, recall, F1-score, confusion matrices and the Area Under the Receiver Operating Characteristic curve.

This methodology provides the central analytical structure for the seminar.

## 1.4 Role of Machine Learning in Road Safety

Machine learning refers to computational methods through which patterns in data can be used to develop predictive or classification models. In road safety, the dependent variable may represent accident occurrence, accident frequency, injury count, accident severity or another road-safety outcome.

The six selected studies demonstrate several forms of this application. Fiorentini and Losa considered Logistic Regression, Classification and Regression Tree, Random Forest, K-Nearest Neighbor and Naïve Bayes for long-term accident susceptibility classification. The output was a binary categorical variable representing accident and non-accident road sites.

The supporting papers broaden the machine-learning perspective. The telematics study uses interpretable machine learning to examine accident-hotspot-related errors while considering temporal, weather and behavioural variables. The injury-count study addresses the prediction of the number of injuries at road-segment level. The accident-severity study applies Random Forest to severity classification, while the GIS-based urban study combines spatial analysis with machine-learning prediction.

Thus, machine learning in road safety is not a single technique or a single prediction problem. It represents a group of methods that can be adapted to different response variables and data structures.

## 1.5 Role of Geographic Information Systems

Geographic Information Systems provide the spatial framework required to connect accident records with their physical locations and surrounding characteristics. Accident records contain both attribute information and geographical information. GIS allows these datasets to be displayed, combined, analysed and spatially interpreted.

In the base study, GIS was used to combine information collected from the road administration and to define the input variables for the machine-learning models. The road network was divided into fixed-length 500 m road sites, after which the relevant characteristics were calculated for each site.

The GIS-based supporting study demonstrates another application. Accident records from Faisalabad were analysed spatially using Local Moran’s I to identify statistically significant clusters of accidents. The researchers subsequently selected survey locations within identified hotspot areas for collecting traffic, geometric and road-furniture information.

This shows that GIS and machine learning can perform complementary functions. GIS can identify and represent spatial patterns, while machine learning can model relationships between accident outcomes and explanatory variables.

## 1.6 Need for Blackspot Identification

A road blackspot can broadly be understood as a location or road section associated with an unusually high level of crash risk or accident occurrence. Identification of such locations is important because road authorities have limited resources for detailed inspections and safety improvements.

The base paper describes blackspot screening as a low-cost approach for investigating a road network using historical databases and calibrated analytical tools. Rather than inspecting every location in detail, screening can be used to identify a smaller group of road sites that require greater attention.

The long-term approach adopted by Fiorentini and Losa is particularly relevant because it considers a five-year accident period. Their objective was to determine whether machine-learning algorithms could identify road sites that had experienced long-term safety problems and potentially classify new sites according to accident susceptibility.

This concept forms the backbone of the present seminar.

## 1.7 Problem Statement

Conventional road-safety assessment based only on historical accident frequency may not fully capture the complex interaction between roadway characteristics, traffic exposure and environmental context. Furthermore, accident datasets can contain multiple variables with nonlinear and interacting relationships.

The problem addressed in this seminar is therefore the development and application of data-driven approaches for identifying accident-prone road locations and understanding accident-related outcomes using machine learning and spatial analytics. The seminar examines how roadway, traffic, environmental, temporal and spatial variables can be integrated into predictive frameworks and how the resulting models can assist road-safety analysis.

The principal methodological reference is the long-term blackspot screening procedure of Fiorentini and Losa, while the other five studies are used to extend the discussion to spatial severity analysis, interpretable machine learning, injury-count prediction, Random Forest severity classification and GIS-based urban hotspot prediction.

## 1.8 Objectives of the Seminar

The primary objective of this seminar is to study the application of machine-learning and spatial-analysis techniques for road traffic accident prediction, accident severity modelling and blackspot identification.

The seminar specifically examines the methodology adopted in the long-term road blackspot screening study and explains how accident history, road geometry, traffic characteristics and environmental information can be transformed into machine-learning input variables.

It also examines the use of Random Forest and other machine-learning algorithms for road-safety prediction and classification.

The seminar further studies the contribution of GIS and spatial-analysis techniques to the identification of accident hotspots and the integration of spatial information with machine-learning models.

Another objective is to compare the six selected studies in terms of their datasets, prediction targets, explanatory variables, machine-learning algorithms, spatial methods and evaluation procedures.

Finally, the seminar discusses the practical applications, limitations and future scope of machine-learning-based road-safety analysis.

## 1.9 Scope of the Seminar

The scope of this seminar is restricted primarily to the six research papers supplied for the study. The report does not claim to present an independent accident-prediction experiment conducted by the student. Instead, it synthesizes and analyses the methodologies, datasets, results and implications reported by the selected researchers.

The main emphasis is placed on machine-learning-based road blackspot screening because the Fiorentini and Losa study provides the most complete framework for connecting road segmentation, GIS-derived variables, accident history, machine-learning classification and performance evaluation.

The supporting studies are used to expand this framework into related areas. These include spatial and environmental severity analysis, telematics-based interpretable prediction, injury-count prediction, Random Forest severity modelling and GIS-based urban accident hotspot analysis.

## 1.10 Organization of the Report

The report is organized into eight chapters. Chapter 1 introduces the problem of road traffic accidents and establishes the need for machine learning and spatial analytics. Chapter 2 explains the fundamental concepts involved in accident analysis, including road segmentation, accident frequency, severity, geometric characteristics, traffic exposure and blackspot identification.

Chapter 3 introduces the machine-learning and GIS techniques relevant to the selected studies. Chapter 4 presents an extensive analysis of the Fiorentini and Losa study as the principal base paper. Chapter 5 discusses the five supporting studies and explains how each contributes to the overall seminar topic.

Chapter 6 presents a comparative analysis of all six studies. Chapter 7 discusses practical applications, limitations, challenges and future research directions. Chapter 8 summarizes the major conclusions of the seminar.

---

## Base Paper Selection and Report Strategy

The principal base paper is:

**Fiorentini, N. and Losa, M. (2020), “Long-Term-Based Road Blackspot Screening Procedures by Machine Learning Algorithms,” Sustainability.**

This paper is used as the central methodological study because it provides an integrated framework involving road segmentation, accident history, roadway geometric variables, traffic variables, environmental information, machine-learning classification, training/testing, cross-validation and model evaluation.

The supporting papers are used for specific extensions of this framework.

The Ghadi and Török study supports the discussion of spatial and environmental factors and accident severity.

The Golestani et al. study supports the discussion of telematics, temporal factors, weather, behavioural factors, XGBoost and model interpretability through SHAP and partial-dependence analysis.

The Hamdan and Sipos study supports the discussion of segment-level injury-count prediction and the relationship between geometric design, traffic flow and injury outcomes.

The Yan and Shen study supports the Random Forest section, particularly accident-severity classification, Bayesian optimization and feature-importance interpretation.

The Khan and Hussain study supports the GIS and spatial-hotspot section, particularly Local Moran’s I and the integration of GIS with machine learning.

The base paper should receive approximately 35–40% of the technical discussion, while the five supporting papers should be used to extend specific parts of the framework rather than being presented as six unrelated mini-reports.

The base paper is particularly suitable because its workflow connects accident history, geometric information, traffic information and environmental information to a balanced dataset, followed by machine-learning classification and predictive-performance assessment.

The paper also provides useful source material for tables and figures. Its methodology workflow, input-factor table, descriptive statistics and model-performance results will be incorporated into Chapter 4 with appropriate source attribution.

## Figure Strategy

Figures will be continuously numbered according to the seminar report rather than retaining the original numbering used by the source paper.

For each reproduced or adapted figure, the report will provide a caption in the form:

**Fig. X. [Description of figure].**

**(Source: [Author(s), year]).**

The figure will be placed near the paragraph where it is first discussed. The original paper figure number and page will be tracked separately so that the source can be identified accurately.

Figures will not be inserted merely to increase the page count. Each figure will support a specific technical explanation, and all figures will be referred to in the main text.

The same approach will be followed for tables. Source-derived numerical tables will retain their original meaning and will be clearly identified as reproduced or adapted material where applicable.

