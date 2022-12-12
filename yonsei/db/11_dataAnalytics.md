# 11. Data Analytics

## Decision Support Systems
1. Data Analysis
1. Statistical Analysis
1. Data Mining
1. Data Warehouse

## Online Analytical Processing (OLAP)
Interactive analysis, different views/summaries of data

### Multi-dimensional Data
* **Measure attributes**: Measure some value
* **Dimension attributes**: Dimensions on which the measure attribs are viewed

#### Cross Tabulation (Pivot Table)
 ![pivot table](./11_1.png)

* **row/column headers**: Dimension attributes form 
    * Rest of the dimension attributes listed at the top
* **cell value**: Aggregates of dimension attributes

#### Data Cube
Multidimensional($n$) generalization of a cross-tab

![data cube](./11_2.png)


### Types of OLAP
1. **Pivoting**: Change dimesions of cross-tab
1. **Slicing** (dicing): cross-tab for fixed-values only
1. **Rollup**: Finer → coarser granularity data
1. **Drill down**: Coarser → finer granularity data

## Data Warehousing
A **data warehouse** is a repository of information gathered from multiple sources, stored under a *unified* schema, at a *single* site. Data sources often store *current* data, while warehouses provides unified view of all data, including *historical* data.

### Design Issues
#### When/How to gather data
* **Source-Driven Architecture**: Data sources transmit data (continuous or periodic)
* **Destination-Driven Architecture**: Warehouses request data (periodic)
* Syncing source/destination expensive
#### What schema to use
* Schema integartion

#### Data cleansing
* Mistakes: **Merge** from multiple sources and **purge** duplicates

#### Propagating Updates
* Warehouse may be materialized view of data source schema

#### What to summarize
* Raw data: too large → Aggregated data often enough
* Queries on raw data can often be transformed by query optimizer to use aggregate values

### Star Schemas
* Encoded using small integers, mapped to full values via **dimension tables**

![star schema](./11_3.png)

## Data Mining
**Data mining** is the process of semi-automatically analyzing large databases to find useful **patterns**.

### Prediction
Make a prediction based on past values
1. **Classification:** Predict class of new item
1. **Regression Formulae:** Predict function result from a set of mappings of unknown function

### Descriptive Patterns
1. **Associations** *(e.g. books bought by similar customers)*
1. **Clusters** *(e.g. sickness clustered around contamination point)*

---

## Classification

### Decision Tree
Classification rules can be shown as a **decision tree**

![decision tree](./11_4.png)

#### Construction of Decision Trees
* **Training Set**: Data with known classes
* Greedy, top-down generation of decision trees
    * Internal node: Partitions the data into groups based on...
        * Partiioning attribute
        * paritioning column
    * Leaf node: Either...
        * Data items are of the same class
        * No further classification possible

### Best Splits

### Bayesian Classifiers

### Support Vector Machine Classifiers

### Higher Dimensions: Visual

### Kernel Trick: Visual

### Neural Network Classifiers

## Regression
Find coefficient that gives the best possible **fit**

## Association

### Rules
*Antecedent* → *Consequent*

### Support
What fraction satisfies both antecedent and consequent?

$$Support(X \Rightarrow Y) = {Frequencey(X, Y) \over N}$$

### Confidence
How often is the consequent true when the antecedent is true?

$$Confidence(X \Rightarrow Y) = {Frequency(X, Y) \over Frequency(X)}$$

## Clustering

### Hierarchial Clustering

## Other types of Mining

### Text Mining

### Data Visualization