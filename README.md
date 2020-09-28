# Analysis of hotel bookings

Author: Martín Pons

## Business understanding

Analytics in the hotelier world today is important, and nowadays this business cannot be run with some sensible and smart use of data.

Here I demonstrate how to use data to analyze three business important concepts in the fields of revenue manamegment and marketing.

The analysis tries to answer three questions

1. How strong is the seasonality in these hotels?
2. Up to what point ADR, length of stay, and lead time for groups reservation differ from individual/transient ones? are rooms harder to sell in nearby dates of a group's stay?
3. Can we predict a cancellation, just with the information available at the moment this reservation has been made?

The first question relates to detecting seasonality patterns. A basic principle to establish a pricing strategy. The second addresses the importance of having a specific pricing strategy for groups. Specific group's behaviors can end up with lower total revenue, because they may have been booked with too much time in advance, and in odd length of stays. Moreover, this awkward behavior can make revenues having a hard time trying to sell rooms in the nearby dates. Finally, be able to detect whether or not a reservation will end up being canceled, is a powerful weapon for the marketing department, with important potential gains.

## Data understanding

The original data has been extracted from the booking changelog, one day prior to arrival date, to avoid leakages. There are some variables that had to be extracted fro, other DB systems.
The data presented consists of booking records from two hotels in Portugal: one resort hotel and one city hotel.

The direct source for this analysis is [Kaggle](https://www.kaggle.com/jessemostipak/hotel-booking-demand) and the original source is [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191).

In total there are 119,390 records and 32 features, with all of these features presenting almost (or none) null values, except for the variable "company" (94 % of records are missing).

## Data preparation

For the two first questions, the analysis has been performed only including confirmed bookings, given that some of the data can change when the client checks-in and canceled bookings can have a different distribution for some variables. Also, this is an a-posteriori analysis, that is, only clients that have stayed in the hotel will be taken into account.

Also, a major transformation is carried out: from booking records we go into daily stay data: the data is aggregated by days and months, and not by check-in date, but by stay date. This requires some complex operations that are performed using helper functions built specifically for this analysis.

Several date variables are extracted from the original data, since some of the analysis deals with aggregation for different time windows.

For prediction of canceled bookings, the analysis is performed at the booking level with the entire data set, and new features are created in the process. The major part, involves grouping qualitative data with too many categories into ones with a limited number of them.

## Modeling

For seasonality patterns detection, visual descriptive analysis has been carried out, in addition to time series analysis, from which, the seasonal component of the series was extracted, and the strength of the seasonality component was measured. The method can be accessed in [Forecasting: Principles and Practice, by Rob J Hyndman]](https://otexts.com/fpp2/seasonal-strength.html). 

For group differences, descriptive analysis and hypothesis testing have been carried out. For the measurement of the difficulty os selling rooms in the nearby dates of a group's stay, Cohen's d was also computed to measure effect size.

Regarding cancelation predictions. A random forest was perform, splitting the data into a training and test set (70 / 30).

## Evaluation

For the first two questions, results are evaluated with visualizations and hypothesis test outputs. For the third question, the model was evaluated using accuracy, precision, recall, and F1 score.

As expected, there is a strong seasonality for the resort and city hotel, both in ADR and room nights. Groups have shorter stays in the resort hotel, book with significantly less time in advance, at lower ADRs. In the city hotel, it was found that rooms in dates nearby group stays are sold at an average lower ADR. Regarding the prediction of cancellations, the model obtained an 85 % accuracy, 81 % precision, 77 % recall, and a 79 % f1-score.

Measuring the difficulty of selling rooms nearby group's stays is a very interesting task, which can be expanded much more than just detecting significant results and effect sizes after dividing the data into two groups: we can change the boundaries for what is considered a large group (in the analysis, 30 % of maxim occupation), and how many nearby dates are selected (in the study, up to 6 days away from a group stay were considered as nearby dates) and analyze how varies the difficulty of selling those rooms when we tweak some of these inputs. More complex models can be performed and more interesting results can be obtained. For a future analysis of this dataset I will delve into this question, provided that the limitations of this data set allow me to do so.

As for the prediction of cancellations concerns. it is clear that better results can be achieved in a more exhaustive machine learning process, that includes more models into consideration. Besides, this data is somewhat limited (only two years). A wider time window and more features, which sure will be at the hands of every hotelier in the business, better results could be obtained.

### File description

- **requirements.txt**: requeriments file with the modules used in the analysis.
- **Analysis of hotel bookings.ipynb**: jupyter notebook with the analysis.
- **hotel_ bookings.csv**: csv files with the data.
- **figures**: a folder containing some of the figures produced in the notebook.

The output of the analysis can be obtained directly by running all the cells in the Jupyter Notebook file. There are texts and visualizations explaining the output.

### Installations

Below is a list of the modules used in the analysis is shown

- pandas
- numpy
- matplotlib
- seaborn
- datetime
- dateutil
- statsmodels
- calendar
- scipy
- sklearn
- math

### Aknowledgments

The original source of the data is  [Hotel Booking Demand Datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191),  by Nuno Antonio, Ana Almeida, and Luis Nunes for Data in Brief, Volume 22, February 2019.

The data was downloaded and cleaned by Thomas Mock and Antoine Bichat for [#TidyTuesday during the week of February 11th, 2020](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md), and published in kaggle by [Jesse Mostipak](https://www.jessemaegan.com/).

The data is published under a Creative Commons license.


