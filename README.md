# wqd7005_aa1

## Project Overview

This project is to analyse and predict customer churn of an e-commerce company. This analysis is essential in for the company to identify the customers who are more likely to churn.  This is helpful for the company to identify the potential issues that result in customer churn and plan appropriate actions to be taken to secure customers’ loyalty.

### Objectives

1.	To analyse the customer churn dataset using exploratory data analysis.
2.	To clean the customer churn dataset thoroughly based on the findings in exploratory analysis.
3.	To build a Decision Tree model and an ensemble model that predicts the churn of a customer given sets of attributes.
4.	To assess the models built and select the best model for customer churn prediction.

### Tools
 - SAS-EM : Used for the exploratory analysis, missing values imputation, data transformation and modelling.
 - Talend Data Integration: Used for merging two data sources.
 - Talend Data Preparation: Used for identifying missing values and inconsistencies in variables, as well as to standardise inconsistent data.

### Data Files
Two data files "customer_profile.csv" and "Customer_churn_dataset.csv" are used in this project.
 - customer_profile.csv: Contains the customer profile information
 - customer_churn_dataset.csv: Contains various attributes for customer churn analysis

### Code and Scripts
`import__data_to_library` contains the codes to import csv data into the SAS library.

Other functions are completed using the GUI mode of all the aforementioned tools.

## Talend Data Integration
This section describes how Talend Data Integration is used in the project.
#### Steps to import a file into a job
1) Create a project.
2) Create a new job.
3) Add "tFileInputDelimited" component into the job.
4) Edit its schema to match with the dataset's schema.
5) Select the file to be uploaded and edit some configurations as necessary/
6) Run the component.

#### Steps to integrate two files as one
1)  Add "tFileInputDelimited" component into the job, select the second data, and run the component.
2)  Add "tMap" component into the job.
3)  Match both "tFileInputDelimited" components to this "tMap" component.
4)  Double click to edit this "tMap" component.
5)  Map the "CustomerID" key in file_1 to "CustomerID" in file_2, a purple line should be linked between these two item.
6)  Select all the attributes that we want to generate in the output (drag and drop), multiple yellow lines should be linked between input and output.
7)  Apply the component.

#### Steps to generate an output file
1) Add "tFileOutputDelimited" component into the job.
2) Link "tMap" component to this "tFileOutputDelimited" component.
3) Configure the output path and file delimiter.
4) Run the component.
5) A file that contains data from both sources is generated in the output path.

## Talend Data Preparation
This section describes how Talend Data Preparation is used in the project.
1) Select the dataset.
2) Inspect each column to discover any missing values or inconsistencies within the data.
3) Identify the columns with missing values that need to be imputed and keep them as they are for now. (Imputation will be done in SAS-EM)
4) In this project, the only incosistency found is the use of different words that are referring to the same value. For example, "Mobile Phone" and "Phone". In this case, "Replace match string with..." function is used to replace a given string with another string. For instance, replace "Mobile Phone" with "Phone". Repeat this step for columns that show the same problem.
5) On the tab on the right, click "Submit" to run the preparation. The data will be replaced after each "Submit" button triggered.
6) Export the dataset.

## SAS-EM
This section describes how SAS-EM is used in the project.
#### Steps to create a data source of the data
1) Create a library.
2) Using code written in `import__data_to_library` to import the csv data into the library.
3) Create a new data source and select the library.
4) Configure the data source accordingly and save it.

#### Setting up workflow for Decision Tree analysis
1) Create a diagram.
2) Drag and drop the data source into the diagram.
3) Add a "Graph Explore" node and link it with the data source. Run this path to explore the graphs with various visualisations.
4) After exploring the data, reconfigure the variables' roles and levels as necessary.
5) Add a "Replacement" node and link it to the data source to replace outliers with "Missing" values.
6) Add a "Transform Variables" node and link it to the "Replacement" node to transform the interval values and categorical values accordingly.
7) Add a "Impute" node and link it to the "Transform Variables" node to impute missing values. Configure this node to use the tree-based model imputation technique.
8) Add a "Data Partition" node and link it to the "Impute" node to split the data into training, validation and testing set in the ratio of 7:1:2.
9) Add a "Decision Tree" node and link it to the "Data Partition" node to be trained on the dataset. Configure this node to form a underfit decision tree with small number of branches, depths, leaf size and rules.
10) Add a "Decision Tree" node and link it to the same "Data Partition" node. Configure this node to form an optimum decision tree with optimum number of branches, depths, leaf size and rules.
11) Add a "Model Comparison" node and link it to both "Decision Tree" node.
12) Run this node to inspect its final results.

#### Setting up workflow for Bagging/Boosting analysis
1) Use the same data nodes from 1) to 7) as the above.
2) Create 4 "Sample" nodes and link them to the "Impute" node created at 7) from above. Sample 25% of data for each of the node, using a different random seed value.
3) Copy 4 "Data Partition" nodes from 8) and link them to the each "Sample" node created at 2). It will use the same configuration as previous.
4) Copy 4 "Decision Tree" nodes from the one that shows the best result and link them to the each "Data Partition" node created at 3). It will use the same configuration as previous.
5) Add an "Ensemble" node and link it with all 4 "Decision Tree" nodes.
6) Add a "Gradient Boosting" node and link it with all 4 "Decision Tree" nodes.
7) Link these "Ensemble" and "Gradient Boosting" nodes to the same "Model Comparison" node at 11) from above.
8) Run this node to inspect its final results.

## Results and Analysis
Please refer to the attachment `YeoYeaErn_S2165943.pdf`.

## Reflections and Learning Outcomes
Please refer to the attachment `YeoYeaErn_S2165943.pdf`.
