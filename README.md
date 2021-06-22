# Housing-Price-Prediction

## Introduction
In this project, we look are looking to build a predictive model for predicting the sale price of houses based on a variety of categorical and numerical features.

The dataset we are working with is the Ames Housing Dataset. Ames is a city in Story County Iowa. It is best know as the home of Iowa State University. Ames also has a population of approximately 66,258 with almost half being students of the university. [Source](https://en.wikipedia.org/wiki/Ames,_Iowa)

The original data (obtained directly from the Ames Assessor’s Office) is used for tax assessment purposes but lends itself directly to the prediction of home selling prices. The type of information contained in the data is similar to what a typical home buyer would want to know before making a purchase and students should find most variables straightforward and understandable.

We have 2 seperate datasets:
* Train data: A dataset with house characteristics and SalePrice
* Test data: This is similar to the train dataset with the exception of SalePrice

## Problem Statement

*Our goal will be to find out if we can use linear regression models to accurately predict house prices on a chosen set of variables. Thereafter, we explore the results and find out which model serves us best and what the results of the model mean for predicting housing prices. We will be using root mean squared error to evaluate our models and choose the best one.*

## Project Flow

* **Section 1: Groundwork**
    * We import libraries, data and also take a look at the variable of interest, house price, on the train data set.
* **Section 2: Primary Variable Selection**
    * We understand the variables we have and also cut out some of the more obvious ones that have no relation to house price and variables that contain majority of nans.
* **Section 3: Handling Irregular Data**
    * We handle nan values and outliers
* **Section 4: Identifying Potential Interaction Variables**
* **Section 5: Feature Engineering (Numeric Variables)**
    * We look to transform certain numeric variables and also drop some
* **Section 6: Secondary Variable Selection (Numeric Variables)**
    * We look to drop more numeric variables based on correlation
* **Section 7: Feature Engineering (Categorical Variables)**
    * We drop some categorical variables based on values. We also perform EDA to understand the distribution of these variables better. We then engineer the ordinal and nominal variables seperately.
* **Section 8: Summary of Variables**
    * We look at the final set of variables we have
* **Section 9: Model Fitting**
    * We perform train-test split and find the optimal model. We further fine tune the model and analyse residuals
* **Section 10: Prediction**
    * We use our final model to predict the variable of interest in our test dataset

## Main Findings

We find that the best model in our initial fitting was the Lasso Regression. This is understandable as we are dealing with many variables. We use the coefficients of our Lasso Regression to fine tune our selection of variables and run another round of fitting. We then find that the Ridge Regression performs best due to its ability to fine tune the coefficients.

### Summary of Models
|Model|StandardScaler|Variables|Mean Squared Error|
|---|---|---|---|
|**Linear Regression**|No|Original|734410767.92|
|**Ridge Regression**|No|Original|734143633.95|
|**Lasso Regression**|No|Original|1169563685.70|
|**Elastic Net Regression**|No|Original|1169563685.70|
|**Ridge Regression**|Yes|Original|733657123.27|
|**Lasso Regression**|Yes|Original|734691265.93|
|**Elastic Net Regression**|Yes|Original|734691265.93|
|**Linear Regression**|No|Refined|691132691.90|
|**Ridge Regression**|Yes|Refined|690447400.87|
|**Lasso Regression**|Yes|Refined|694845573.86|
|**Elastic Net Regression**|Yes|Refined|695424166.38|


|Variable|Coefficient|
|---|---|
|MS Zoning|3764.44|
|Lot Area|6273.03
|Lot Shape|387.77
|House Style|-3418.32
|Overall Qual|11024.81
|Exterior 1st|5742.03
|Exterior 2nd|-4989.30
|Mas Vnr Type|-4142.91
|Mas Vnr Area|7093.37
|Exter Qual|11504.55
|Foundation|1361.83
|Bsmt Qual|-2050.09
|BsmtFin Type 1|-612.16    
|BsmtFin SF 1|11800.23
|Total Bsmt SF|7814.66
|Heating QC|1956.02
|Gr Liv Area|22719.27
|Kitchen Qual|9858.53
|Fireplaces|3341.90
|Fireplace Qu|650.87
|Garage Type|-814.75
|Garage Finish|1890.48
|Garage Area|5565.86
|House Age|-5267.79
|Remod Age|-3421.61
|Decks|2754.43
|Baths|-563.01
|Neighborhood_BrkSideE|11041.47
|Neighborhood_CollgCr|-4681.50
|Neighborhood_Crawfor|18563.66
|Neighborhood_Gilbert|-3753.05
|Neighborhood_Mitchel|54511.90
|Neighborhood_NWAmes|-2502.71
|Neighborhood_NoRidge|-6516.83
|Neighborhood_NridgHt|16597.02
|Neighborhood_OldTown|27629.63
|Neighborhood_Sawyer|1604.82
|Neighborhood_SawyerW|1485.48
|Neighborhood_Somerst|-10387.10
|Neighborhood_StoneBr|4672.69
|Neighborhood_Veenker|43854.60

### 9.5 Conclusions and Findings

We circle back to the our original problem:

We have indeed produced a model that allows us to predict house prices. We have presented the results of that model above (variables, coefficients and also the plot of residuals). Here are some thoughts from the model:

#### Neighborhoods/ Location plays an important role

We see that the different dummies for neighborhoods have some of the highest and lowest (most negative) coefficients in the model. What this translates to is that depending on the location of the house, there can be a significant premium or discount to the house price. For example, based on our model, StoneBr fetches over 43,000 in premium whereas SayerW is at a discount of over 10,000. However, we do have to keep in mind that this might just be the case of certain eighborhoods having larger houses and hence fetching a higher price. This is something to keep in mind when anaysing the data.

#### Maintaining House Quality is important

External quality, Overall quality and Kitchen quality have some of the most positive coefficients as well. This goes to show that maintaining the quality of some facets of your house can greatly impact house prices.

#### Living Area (of course)

It comes with no surprise that living area is also one of the top predictors of housing prices and this should come as no surprise.

#### Age of the House

We can also see that the age of the house matters. House Age and Remod Age are some of the most negative variables in our model. The older the house/ longer the time it has been since remodelling, the lower the house price.

### Implications for Home owners/ buyers

Overall our model gives us much insight and the information we gathered can be particularly useful for home owners looking to sell or buyers. Home owners looking to sell should ensure that they are familiar with the premium or discount of their location and also that the quality of the house is decent. They might even want to consider remodelling the house slightly before sale to reduce the negative impact this variable has on price. They should also look to sell earlier than later as each year that the house ages, the price of the house will decrease.

For home buyers, it is also necessary to check the premium and discount based on location. An extensive check on the quality of the house should also be in order before committing to the purchase.



#### Drawbacks of the model

From our plot of residuals, we can see that as house prices increase over the 400,000 range, our model starts to show a higher degree of variance and poorer predictions (greater residuals). This might be the case as the functional form of the model might not be a linear equation that has the same gradient over different ranges. I believe it would be fair to say that housing prices do not increase in step with any set of variables (of the first degree). However, our model still works decently well within the mainstream range of housing prices.

#### Refining our model with results

Another interesting finding is that using the lasso model's coefficients to eliminate irrelevant variables can in turn increase the accuracy of our overall model. We have done so and used ridge thereafter as we will be able to fine tune the coefficients, resulting in ridge being our favored model.


### Future Steps

A step that we can possibly take in the future is to fit different models over different house price ranges or different house sizes. My hypothesis is that the models will have some significant difference bepedning on the size and price range of the houses. We should also look to collect more data points for houses in the higher range as we lack observations and this could have caused some inaccuracy in our model towards the higher end of the house price range.


## Data Dictionary
|Variable|NaNs|Relevance/ Importance|Recommendation|
|---|---|---|---|
|**ID**|0|Observation number|Keep, but will not use|
|**PID**|0|Parcel ID, might be useful but too many iterations for us to cateorise|Potential drop|
|**MS Subclass**|0|Type of housing|Keep, might use|
|**MS Zoning**|0|Zoning, agri, commercial etc|Might use but hard to convert, potential dummy|
|**Lot Frontage**|330|Length of street connect to prop|Not useful|
|**Lot Area**|0|Size in sq ft|Useful|
|**Street**|0|Gravel or paved|Not useful, only 7 gravel|
|**Alley**|1911|Alley acces to prop|Not useful, drop|
|**Lot Shape**|0|State of regularity|Potentially useful, can convert|
|**Land Contour**|0|Flatness of land|Potentially useful, can convert|
|**Utilities**|0|Number of utilities (E,G,W,S)|Potentially useful, can convert|
|**Lot Config**|0|Configuration of lot|Potentially useful, can convert|
|**Land Slope**|0|Slope of property|Potentially useful, can convert|
|**Neighbourhood**|0|Location|Might be useful but too many unique values|
|**Condition 1**|0|Proximity to various conditions|Might be useful but hard to convert|
|**Condition 2**|0|Proximity to various conditions (more than 1)|Might be useful but hard to convert|
|**Bldg Type**|0|Type of housing|Useful, convert to dummy|
|**House Style**|0|Style of dwelling|Useful, many, convert to dummies|
|**Overall Qual**|0|Quality of materials and finish|Useful, little conversion needed|
|**Overall Cond**|0|Condition of house|Useful, little conversion needed|
|**Year Built**|0|Year built|Useful, but can use remodelling date too|
|**Year Remod/Add**|0|Remodel date|Useful, can take diff between this and current time|
|**Roof Style**|0|Type of roof|Doesn't look useful|
|**Roof Matl**|0|Roof Material|Doesn't look useful|
|**Exterior 1st**|0|Exterior covering house|Potentially useful, too many uniques|
|**Exterior 2nd**|0|Exterior convering house|Potentially useful, too many uniques|
|**Mas Vnr Type**|22|Type of Masonry veneer|Potentially useful, convert to dummies|
|**Mas Vnr Area**|22|Area of Masonry veneer|Easy to use but check correlation with lot area|
|**Exter Qual**|0|Quality of exterior|Useful, convert to numerical|
|**Exter Cond**|0|condition of exterior|Useful, convert to numberical|
|**Foundation**|0|Type of foundation|Potentially useful, convert to dummies if needed|
|**Bsmt Qual**|55|Height of basement|Useful, can convert to numerical|
|**Bsmt Cond**|55|Condition of basement|Useful, can convert to numberical|
|**Bsmt Exposure**|58|Walkout or garden level walls|Doesn't look too useful|
|**BsmtFin Type 1**|55|Rating of basement finish|Useful, can convert to numberical|
|**BsmtFin SF 1**|1|Type 1 finished in sq ft|Potentially useful|
|**BsmtFin Type 2**|56|Rating of basement finished area|Useful, can convert|
|**BsmtFin SF 2**|1|Type 2 finished in sq ft|Potentially useful|
|**Bsmt Unf SF**|1|Unfinished sq ft of basement|Potentially useful|
|**Total Bsmt SF**|1|Total sq ft of basement|Potentially useful|
|**Heating**|0|Type of heating|Not useful, majority same heating|
|**Heating QC**|0|Quality of heating|Useful, can convert to numerical|
|**Central Air**|0|Central air conditioning|Not useful, majority has|
|**Electrical**|0|Electrical system type|Not useful, majority same|
|**1st Flr SF**|0|First floor sq ft|Useful|
|**2nd Flr SF**|0|Second floor sq ft|Useful|
|**Low Qual Fin SF**|0|Low quality finished sq, all floors|Useful|
|**Gr Liv Area**|0|Above grade livng sq ft|Useful|
|**Bsmt Fulll Bath**|2|Basement full bathrooms|Potentially useful|
|**Bsmt Half Bath**|2|Basement half bathrooms|Potentially useful|
|**Full Bath**|0|Full bathroom above grade|Potentially useful|
|**Half Bath**|0|Half bathroom above grade|Potentially useful|
|**Bedroom AbvGr**|0|Above grade bedroom|Useful|
|**Kitchen AbvGr**|0|Above grade kitchen|Useful|
|**Kitchen Qual**|0|Kitchen quality|Useful, can convert to numerical|
|**TotRms AbvGrd**|0|Total rooms above ground|Useful|
|**Functional**|0|Home Functionality|Home functionality, can convert to numerical|
|**Fireplaces**|0|Number of fireplaces|Not useful|
|**Fireplace Qu**|1000|Quality of fireplaces|Not useful|
|**Garage Type**|113|Garage Location|Potentially useful, need dummies|
|**Garage Yr Blt**|114|Year garage built|Unlikley to be useful|
|**Garage Finish**|114|Interior finish of garage|Potentially useful, can convert numerical or dummy|
|**Garage Cars**|1|Size of garage|Unnecessary as we have specified area|
|**Garage Area**|1|Size of garage in sq ft|Potentially useful|
|**Garage Qual**|114|Garage Quality|Potentially useful, can convert to numerical|
|**Garage Cond**|114|Condition of garage|Potentially useful, can convert to numerical|
|**Paved Drive**|0|Paved driveway|Not useful, mostly have paved|
|**Wood Deck SF**|0|Wooden deck area in sq ft|Potentially useful|
|**Open Porch SF**|0|Open porch area in sq ft|Potentially useful|
|**Enclosed Porch**|0|Enclosed porch area in sq ft|Potentially useful|
|**3Ssn Porch**|0|3 season porch in sq ft|Not useful, most do not have|
|**Screen Porch**|0|Screen porch area in sq ft|Not useful, most do not have|
|**Pool Area**|0|Pool area in sq ft|Not useful, most no pool|
|**Pool QC**|2042|Pool condition|Not useful as too many missing, can drop|
|**Fence**|1651|Fence qaulity|Not useful as too many missing, can drop|
|**Misc Feature**|1986|Misc features|Not useful as too many missing, can drop|
|**Misc Val**|0|Misc features value|Not useful as too many 0|
|**Mo Sold**|0|Month Sold|Might be useful but year should be sufficient|
|**Yr Sold**|0|Year Sold|Useful in calculating age of house at sale|
|**Sale Type**|0|Sale type|Useful in getting rid of outliers|
|**SalePrice**|0|Sales price|Y Value|
|**age**|0|Years since built/ remodelled|Useful|
|**Irregularity**|0|State of irregularity based on Lot Shape coolumn|Useful|
|**Slope**|0|Level of slope based on land slope column|Useful|
