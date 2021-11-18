# Group 4 Phase 2 Project - King County Real Estate
#### Julian, TJ, and Aalok

## Introduction

Our stakeholder is a property investor/redeveloper hoping to purchase and update properties. 

For the sake of this experiment, this developer is considering scraping the existing buildings. With this in mind, the developer is interested in both underlying values of the property and the more mutable properties. This developer is looking for a mismatch, where a property might have a high underlying value but other characteristics that aren't optimized. Finally, the developer would want to know how to then optimize the property once it has been purchased.

#### The following characteristics are being considered as 'fixed':

Zipcode, view, waterfront, sqft_living15, sqft_lot15, lat and long, sqft_lot

#### The following characteristics are being considered as 'fixable':

bedrooms, bathrooms, sqft_living, floors, sqft_above, grade

Our exploration in the model will attempt to tease these factors apart in order to help guide our analysis.



### Bottom Line Up Front

  There is opporutunity in the King County area to purchase low grade housing in high value locations.


### Data cleaning

Some initial data cleaning needed to be done. 
Several variables were processed out to make categorical data. 
The waterfront data had some holes. After a quick check on the latitude/longitude data, it was decided that these missing data points were likely not waterfront property, and nulls were filled with nos.
Grade was turned into numeric data.
A quick check was run on sqft_living. To weed out extreme outliers, any values that were too different than the neighbors.
A look at bedroom revealed an outlier. A process was devised to clean out anything over 3x standard deviations.

### The simple model

![Simplemodelresidual](https://user-images.githubusercontent.com/85522002/142444303-d0a01b33-4f2b-4308-acf7-ef22a926ec8b.png)

Our simple model here looks only at sqft_living. This clearly needs work. 

### The next iterations
Several iterations of the model were tried, including  almost all available data, including the zipcodes, which we've discovered have a huge predictive effect. This leads to a very high R-squared, but not a lot of useful analysis. The model has a very high R-squared score of about .81

![Fourth model graph](https://user-images.githubusercontent.com/85522002/142446202-56609ef5-8a8d-42dc-ae49-d4130d3221a2.png)


However, the condition score here is unacceptably high at 3.591339787033922e+20

### A next step

![Prich_housing_in_out_king](https://user-images.githubusercontent.com/85522002/142224940-1c9ea6e6-68d7-4ef2-a590-5f2c72876bcd.png)

For the next iteration a new category was created, collapsing the zipcode data into more useful metrics of 'in Seattle' and 'not in Seattle'. This allowed the model to still account for geographical location without becoming totally overwhelmed by the zipcode data. As the chart above shows, there is a difference in the distribution of prices within those two categories. 

## The Final Model

The model was then run through RFECV filtering, and further narrowing of the model was done. Ultimately, the fixed features chosen were:

Waterfront
View
and whether or not the property was in Seattle.

Meanwhile the fixable features chosen were:

Bedrooms
Floors_cat
Grade

![Final model](https://user-images.githubusercontent.com/85522002/142446344-7c57d6a0-b75d-46cb-bb48-cfa7d63b6775.png)

The model explains somewhat less of the variance than the fourth model in our iterations, with an R-squared score of around .56. However, by culling our features, we've reduced the condition number to about 65, a considerable improvement.

In the end our model comes with the following coefficients.

##### Coefficients

| Variable      | Coefficients  |
| -----------   | -----------   |
|bedrooms_cat   |  42520.314097 |
|floors_cat     | -22720.359516 |
|waterfront     | 529733.421212 |
|view           |  85930.752685 |
|grade_num_cat  | 188069.319191 |
|in_Seattle     | 130107.331040 |

Unsurpisingly, placement within Seattle is important, as is a waterfront location and a good view. Our stakeholders should keep these factors in mind as they make purchases. Although our stakeholders can't directly change these variables themselves, removing them from the model would make the model far less predictive.

Helpfully, as our stakeholders might be hoping to hear, there is a considerable premium for higher grade homes and, space permitting, additional rooms. (Bedrooms here act, partially, as a proxy for overall house size.) Interestingly, floors are not in themselves bonuses. It may make sense to build vertically to increase bedroom count, but only if lot size won't allow horizontal expansion. 

The extent to which this might be a profitable model will depend on construction costs, of course, but assuming that those costs are fairly even from location to location this model should help the client maximise efficiency when selecting locations to redevelop. 

Insight 1 - Knowing the limitations of our model, we would recommend focusing on houses that are on the market for less than 1 million dollars. At prices above that, our model tends to under value homes and we cannot confidently predict prices above that point. 


### Recommendations

Looking for zipcodes with high overall prices and relatively low grades to target for improvement seems to be an opportunity to maximize profits. 

For instance, the zipcode 98115 inside Seattle has a relative mismatch between average sale price, a relatively high 600751.99 and its average grade of around 7.31. Purchasing grade 4-6 houses there and redeveloping them up to 8-9 grade houses would result in considerable profit. 
