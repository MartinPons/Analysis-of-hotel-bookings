# Analysis of hotel bookings

Author: Martín Pons

This project contains an analysis of hotel booking data of twho hotels in Portugal: one resort hotel and one city hotel. Data for this analysis coms from [Kaggle](https://www.kaggle.com/jessemostipak/hotel-booking-demand), click [here](https://www.sciencedirect.com/science/article/pii/S2352340918315191) to access the original source.

The analysis addresses three questions.

1. How strong is the seasonality in these hotels?
2. Up to what point adr, length of stay and lead time for groups reservation difers from individual / transient ones?
3. Can we predict a cancellation, just with the information available at the moment this reservation has been made?

The two first questions are commom ones for everyone that wants to enter the market. The second one is specially relevant from a business stand point. Transiend demand displaced by Groups require an specific analysis because it can affect main kpis not only for the day groups stay in, but for the surrinding days: a booking by a group it can make more difficult to sell rooms for the week the groups stays in. Finally being able to predict wether a booking will be canceled puts the marketing and sales team in an advanced position regarding selling, pricing and segmentation actions.

As expected, there is a strong seasonality for the resort and city hotel, both in adr and roomnights. Groups have shorter stays in the resort hotel, book with significant less antelation, with lower ADRs. A random forest was the model selected to predict cancellations, obtaining an 85 % accuracy and a 79 % f1-score.

The data is published under a Creative Commons license.

### File description

- **requirements.txt**: requeriments file with the modules used in the analysis.
- **Analysis of hotel bookings.ipynb**: jupyter notebook with the analysis.
- **hotel_ bookings.csv**: csv files with the data

The output of the analysis can be obtained directly by running all the cells in the Jupyter Notebook file. There are texts and visualizations explaining the output.

### Installations

Below is a list of the modules used in the analysis is shown

- pandas
- numpy
- matplotlib
- seaborn
- datetime
- statsmodels
- calendar
- scipy
- sklearn

### Aknowledgments

The original source of the data is  [Hotel Booking Demand Datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191),  by Nuno Antonio, Ana Almeida, and Luis Nunes for Data in Brief, Volume 22, February 2019.

The data was downloaded and cleaned by Thomas Mock and Antoine Bichat for [#TidyTuesday during the week of February 11th, 2020](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md), and published in kaggle by [Jesse Mostipak](https://www.jessemaegan.com/).


