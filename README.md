# King-County-Housing-Market-Analysis Project Report
## Summary of Findings
The process of shopping for a house can be overwhelming, with many homebuyers not knowing what of
a wide variety of factors truly impact how affordable or expensive a house is. Because of this, someone
unfamiliar with the housing market might end up spending more money on a house based on a factor that
actually isn’t that valuable to them, all because they didn’t understand how different characteristics of a
house impact its price. Our report examines the relationship between a wide variety of characteristics of
properties in King County, Washington. The goal is to understand how these factors affect the price of the
home with the goal of better informing prospective homebuyers of what to consider when shopping for an
affordable home. Our report finds a specific set of factors that, when used together, best predict the price of
a home in King County. Specifically, this combination of predictors is: whether a house is waterfront or has a
view, whether it has a basement, its lot size, number of floors, condition, grade, and the average size of living
spaces and lots in its surrounding neighborhood. All of these are positively correlated with higher prices,
meaning that as their values increase, there reliably is an increase in house price. Alternatively, houses that
are older tend to have higher prices, although this negative correlation between price and the year a house
was built is very slight. If a homebuyer is looking to efficiently cut costs, these factors are the first ones they
should evaluate to see whether they are willing to trade off on any of them to find a more affordable home.
Most prospective homebuyers look to avoid the expensive repairs and constant upkeep that can come with
a house by looking for one of a higher construction quality. Many times, this is difficult to ascertain for a
typical homeowner without any expertise. Our report finds that in King County, a prospective buyer can
quickly and easily estimate whether a home has an average/above average construction grade or not using
three characteristics that show up on any listing: price, square footage, and the year in which the home is
built. As price and square footage increase, a home is more likely to have an average or above construction
rating. As the age of the home increases, a home is more likely to have a below average construction
rating. Specifically for King County we also found that if you’re looking for an older home, it is best to look
in the western region of the county near the water. However, with these older homes, you’re more likely
to be purchasing a home with a below average construction grade. If looking for a newer home with an
average/above average quality, it is best to focus your search east of Lake Washington where higher quality
and newer developments are abundant.

## Dataset Description
This dataset contains 21,613 observations of property sales in King County, Washington between May, 2014
and May, 2015. The dataset included 21 variables before the ones we have added. See the description of
variables below.
### Existing Variables
• id (numeric) - Unique ID for each home in the dataset
• date (character) - Date the home was sold
• price (numeric) - Sale price of the home
• bedrooms (numeric) - Number of bedrooms in the home
• bathrooms (numeric) - Number of bathrooms in the home
• sqft_living (numeric) - Square footage of the living space
• sqft_lot (numeric) - Square footage of the land
• floors (factor) - Number of floors in the home
• waterfront (factor) - Logical variable indicating whether the home is waterfront
• view (factor) - Rating from 0-4 of the quality of the view from the home
• condition (numeric) - Rating from 1-5 of the condition of the apartment
• grade (factor) - Rating from 1-13 of the quality of construction and design of the building (with an
average building condition being a grade of 7)
• sqft_above (numeric) - Square footage of living space above ground level
• sqft_basement (numeric) - Square footage of living space below ground level
• yr_built (numeric) - Year of construction
• yr_renovated (numeric) - Year of last renovation
• zipcode (numeric) - Zipcode where the home is located
• lat (numeric) - Latitude of the home
• long (numeric) - Longitude of the home
• sqft_living15 (numeric) - Average interior square footage of the nearest 15 homes
• sqft_lot15 (numeric) - Avg square footage of the land of the nearest 15 homes
### New Variables
• binary_grade (factor) - 1 if grade is greater than 7, 0 if not
• basement (factor) - 1 if home has a basement, 0 if not
• renovated (factor) - 1 if home has been renovated since construction, 0 if not
• rooms (numeric) - Total number of bedrooms and bathrooms on the property

# Questions
## 1. Which housing variables in King County, Washington affect house sale prices the most, and in what way?
### Motivation
Many of our group members want to live in a big city in the future, especially after we earn our master’s
degrees in data science and have to find work in the real world. We can determine what to look for while
house-hunting in the future by researching what characteristics predict home prices, especially in a county
that encompasses a large city like Seattle. We can effectively analyze whether a home is overpriced or
underpriced by studying which housing elements have the most influence on its pricing.
### Response Variable: price
### Results
It appears that our model performs quite well on the test data. We placed a line with a slope of 1 on the
graph to represent a line of perfect fit, and generally the data points fall positively along this line. We
are pleased with the performance of this model and can conclude that the predictors sqft_lot, floors,
waterfront, view, condition, grade, yr_built, sqft_living15, sqft_lot15, renovated, basement, and
rooms, when taken together, are useful in determining the sale price of homes in King County, WA. Specifically, when controlling for the other predictors, for each one unit increase in each numeric variable, price can be determined by multiplying e response. For the logical predictors in the model, log (price) increases by e response in the presence of a TRUE value of the predictor, when controlling for other variables.
Our final regression equation for the model is:
log (price) = 20.233 + 0.160floors + 0.435waterfront + 0.045view + 0.051condition + 0.240grade
−0.005yr_built + 0.000sqf t_living15 + 0.000sqf t_lot15 + 0.042renovated + 0.133basement + 0.034rooms
For the most part, these coefficients seem consistent with reality, as a higher price should correspond with
more land, better build quality and condition, number of rooms and floors, presence of a basement and a
good view, whether the home has been renovated or has a water view, and the characteristics of nearby
properties. One surprising conclusion from this equation is an inverse relationship between the age of the
home and the price. It is possible that older homes in King County have more desirable qualities than newer
homes, but we would not necessarily guessed this on our own.

## 2. Which housing variables could prospective buyers use to quickly estimate whether the construction grade of a house in King County, Washington is above or below average?
### Motivation
Cities and counties are distinguished by areas of wealthy and poor development. By examining how housing
characteristics influence a building’s construction grade, we can discover which houses are safer and more
robust. When considering potential housing, it is critical to think long-term and to invest in a property that
will last for many years. Living in a building with a lower grade might result in a variety of infrastructure
concerns as well as health risks. By educating ourselves on what housing elements commonly connect to
a higher grade, we will know what to look for when house hunting and making investment choices in the
future.
### Response Variable: binary_grade
### Results
Our full model has a logistic regression equation as follows:
ln(π/ (1 − π)) = −376.6 + 0.000008144(price) + 0.001834(sqf t_living) + 0.2306(floors) − 3.376(waterfront)
−0.1172(condition) + 0.05582(yr_built) − 2.146(long) + 0.0007627(sqf t_living15) − 0.00001007(sqf t_lot15)
+82.73(renovated) − 0.1969(basement) + 0.1302(rooms) − 0.04245(yr_built ∗ renovated)
Where π equals the probability of a house having an average or above construction grade.
This model does answer our question pertaining to which variables we can use to predict whether a house
has an average or above construction grade compared to a below average grade. As price, sqft_living,
yr_built, sqft_living15, floors, and rooms increase, the probability of a house having an average or
above average grade increases, holding all other variables constant. As condition, long, and sqft_lot15
increase, the probability of a house having an average or above average grade decreases, holding all other
variables constant. Additionally, holding our other predictors constant, a renovated house increases the
probability of having an average or above average grade, while a house on the waterfront or a house with a
basement decreases that probability. While this equation may be useful for a realtor or insurance company
who are looking for the highest possible accuracy and most accurate estimations of the effects of the predictors
on the grade, it is much too complex for a prospective homebuyer searching on their own. Because of this,
we would recommend our more simple model for prospective homebuyers:
The reduced equation is:
ln(π/ (1 − π)) = −103.8 + 0.000008552(price) + 0.002151(sqf t_living) + 0.05090(yr_built)
where π equals the probability of a house having an average or above construction grade.
This model better answers our question when it comes to prospective buyers as it is much simpler than
the other, making it more interpretable for a layperson. Using this equation, it’s much easier to see that
a one thousand dollar increase in price multiplies the odds of a house being average or above average by
exp(0.008552) = 1.00859, holding all other variables constant. Similarly, each additional square foot of living
space multiplies those odds by exp(0.002151) = 1.002153 and as a house’s year it is built in increases by
1 (the house is a year younger), those odds are multiplied by exp(0.05090) = 1.052218, holding the other
variables constant. These values may seem small but on the scale of houses, whose price values range in the
hundreds of thousands, square footage in the thousands, and year from the early 1900s to the early 2010s,
these can have a large impact.
