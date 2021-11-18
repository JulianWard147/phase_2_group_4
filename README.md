# phase_2_group_4
Group project for phase 2 DS


Our stakeholder is a property investor/redeveloper hoping to purchase and update properties. 

For the sake of this experiment, this developer is considering scraping the existing buildings. With this in mind, the developer is interested in both underlying values of the property and the more mutable properties. This developer is looking for a mismatch, where a property might have a high underlying value but other characteristics that aren't optimized. Finally, the developer would want to know how to then optimize the property once it has been purchased.

#### The following characteristics are being considered as 'fixed':

Zipcode, view, waterfront, sqft_living15, sqft_lot15, lat and long, sqft_lot

#### The following characteristics are being considered as 'fixable':

bedrooms, bathrooms, sqft_living, floors, sqft_above, grade

Our exploration in the model will attempt to tease these factors apart in order to help guide our analysis.

### Data cleaning

Some initial data cleaning needed to be done. 
Zipcodes were processed out to make categorical data. 
The waterfront data had some holes. After a quick check on the latitude/longitude data, it was decided that these missing data points were likely not waterfront property, and nulls were filled with nos.
Grade was turned into numeric data.
A quick check was run on sqft_living. To weed out extreme outliers, any values that were too different than the neighbors.



### The baseline model

Insert image


Insert analysis of baseline here.


### The first iteration

![Model_1_res_graph](https://user-images.githubusercontent.com/85522002/142089408-705158f1-fe91-4d10-be58-79a612ce124e.png)

The first iteration of the model takes in a whole lot of data, including the zipcodes, which we've discovered have a huge predictive effect. This leads to a very high R-squared, but not a lot of useful analysis.


### The next iteration

![Prich_housing_in_out_king](https://user-images.githubusercontent.com/85522002/142224940-1c9ea6e6-68d7-4ef2-a590-5f2c72876bcd.png)

For the next iteration a new category was created, collapsing the zipcode data into more useful metrics of 'in Seattle' and 'not in Seattle'. This allowed the model to still account for geographical location without becoming totally overwhelmed by the zipcode data. As the chart above shows, there is a difference in the distribution of prices within those two categories. 

The model was then run through RFECV filtering, and features were selected that way. This model includes:

**Fixed**
C(waterfront)
view
sqft_living15
sqft_lot15
C(in_Seattle)

**Fixable**
bedrooms
sqft_living
floors
grade_num

In this model waterfront, views, and the location within Seattle clearly had a strong impact on final price. The livable square footage of neighboring lots had a moderate effect, about half of the effect of living square footage of the actual property. The square footage of neighboring lots had a minor negatively correlated effect, likely helping the model compensate for lower prices in more rural areas, supplementing the more brute caluclation in the zipcode. 

As far as 'fixable' characteristics go, we find our most interesting results. The number of bedrooms and floors come in as negatively correlated. This is not to say that adding a bedroom to a home will nessesarily make it worse. An additional bedroom will come with additional square feet of living space, for instance. If we were to drop the sqft_living feature from the model, bedrooms would become a proxy for square footage and become positively correlated with price. However, given the inclusion of square footage, bedrooms themselves drop in priority. The group has theorized this as the 'room for activities' effect, where more luxerious housing might include less emphasis on simply sleeping and include more ammenities. 

Finally, grade clearly has a large positive effect on the price of the house. While not unexpected, this does confirm what our stakeholder hopes to hear. There is potencial value to be capture by purchasing homes with high 'fixed' scores (e.g., in Seattle, with a nice view, along the waterfront) but poor 'fixable' metrics (e.g. low grade, or small livable square footage). Additionally, this might guide our stakeholder's determination with regards to density of bedrooms and floors. While not nessesarily poor choices (again, an additional bedroom comes along with additional livable square footage) they should not be the factor focused on to maximize sales price.

The extend to which this might be a profitable model will depend on construction costs, of course, but assuming that those costs are fairly even from location to location this model should help the client maximise efficiency when selecting locations to redevelop. 

## The final model!


Insert image

Justify why the model is good/talk about weaknesses




Insight 1 - Knowing the limitations of our model, we would recommend focusing on houses that are on the market for less than 1 million dollars. At prices above that, our model tends to under value homes and we cannot confidently predict prices above that point. 

Insight 2 - 
Insight 3




Recommendation recommendation recommendation.
