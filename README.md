# Hackathon ENSAE - Microsoft - Croix-Rouge

## Introduction
Here is a summary of the methodology we used to win the 1st prize at the ["Data Science Student Challenge"](http://www.ensae.dsschack.com) organized by ENSAE ParisTech, Microsoft and Croix-Rouge. There will not be any code or data in this repository, since the competition required strict confidentiality.

*WARNING: the following methodology is a rather simple and crude one since it was developed in 24 hours. We are aware of its statistical limitations, but we hope it can serve as a basis for future work.*

Our team consisted of the following members by alphabetical order:
- David AZOULAY
- Alexandre COMBESSIE
- Gabriel DUCROCQ
- Johanna LALOU
- Alize PAPP

## Workflow
We started with a large database (~10GB) on the distribution of social help by all centers of the Croix Rouge in France. The database was loaded on a SQL Server hosted by Microsoft Azure, and we interacted with it using Python Jupyter notebooks on a virtual machine with 32GB of RAM.

Early on during the Hackathon, we split our team work in two parallel streams:
1. Extracting relevant data from the Croix-Rouge internal database
2. Collecting and cleaning Open Data on socio-economic indicators in France, mostly from INSEE

These joint efforts had a common goal: to build a regression model explaining the need for social help by a set of socio-economic indicators such as the poverty and unemployment rates. The need for social help was measured either by the number of Croix-Rouge centers per capita or by the ratio of Croix-Rouge beneficiaries in the population.  All indicators were computed at the department level. Note that due to data formatting issues, we were not able to include Mayenne, Nievre, Sarthe, Corsica, and the DOM-TOMs in our analysis. As expected, all indicators were standardized by the population of each department (in absolute numbers or in number of households).

 We used the following socio-economic indicators: population density, overall poverty rate, poverty rate below 30 year old, ratio of home owners, ratio of taxable households, ratio of households on social allowances, unemployment rate, ratio of high/middle-class, ratio of employees and factory workers, ratio of agriculture workers,  crime rate, ratio of medical urgency units. Finally, we added the ratio of Secours Populaire centers on the department population to account for other social help institutions.

 Thanks to all this data, we were able to run several regression models: Ordinary Least Square (OLS), Ridge regression, and Random Forest (to qualify each feature importance). We also tried Leave-One-Out cross-validation for the Ridge. Overall the models' fits were very good (R2 of 0.48 for the OLS regression, 0.57 for the Ridge). This is not surprising as factors like poverty and unemployment are strongly linked with the need for social help.

## Results
We used our OLS regression model as a way to "predict" the theoretical need for social help in each department. We assumed that any negative gap between predicted and observed values meant that the department did not have enough Croix-Rouge centers. We plotted these gap values on an interactive map of France using Microsoft Excel PowerMap. We also established a "Top 5 List" of priority departments by sorting the highest gaps in terms of both number of centers and beneficiaries.

The jury was quite happy with our results and final presentation, and we were very honored to receive the first prize in our competition category. To go further, we would have liked to pursue the following tracks:
- Cross-validating our results
- Performing our analysis at the city level
- Adding more data from other social help institutions
