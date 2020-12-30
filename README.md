# MarketSizing using Monte Carlo and Python
Please let me know if you EVER use this or want my help on adapting the code 
Email rrosasl@gmail.com

Market Sizing is an excercise in which we try to estimate the total the yearly revenues of an industry or company per year in a currency (e.g. USD / EUR / CHF). We can do this by having a structured process; for example: multiplying the total quantity sold per year by the average price.

We may not know in advance what are the values behind the assumptions (e.g. how many items are sold per year). Usually, we solve this by making reasonable assumptions or educated guesses that gives us an indicative value. Although that's a good starting point, it misses completely the uncertainty. With imperfect information, there will never be a single number, but rather a reasonable range in which the true value may lie; and some assumptions may have a larger impact than others, either by its role in the model or by the uncertainty. That is what we will address here.

This notebook will have a Monte Carlo simulation, that projects thousands of potential scenarios, each with different assumptions, giving us the range of potential market sizes and telling us which assumptions have the largest impact on the model.

## Structure of the model
### INPUT: ASSUMPTIONS
Type of assumption (continuous or discreet)
Low value of assumption (You think it would be quite rare, less than 10% chance, that the true value is lower)
Mid value of assumption (the most likely value of the assumption)
High value of assumption (You think it would be quite rare, less than 10% chance, that the true value is higher)
Minimum value the variable can take
Maximum value the variable can take


### PROCESS: 
(1) MONTE CARLO SIMULATION
For each assumption, generate thousands of data point from a random distribution (skewness depending on the high, mid, and low values)
Generate a dataframe that has a scenario per row and the values per assumption as column
Creates a new column that does the market sizing for each scenario
Calculates median market size and percentiles p10 and p90

(2) Feature Importance
For each variable, substitue in the dataframe with all the scenarios the value of the variable with the mid value from the assumption
Re-calculate the median market size with the p50 static assumption
Compare both the original median market size from monte carlo with the new market size. Larger values indicate a larger importance based on the uncertainty
To calculate the feature importance from the static model, check the base case with a 10% increase per variable ceteris paribus

## Cool things in the model (and others left out)
### In Scope:
Generation of thousands of scenarios
Considering skewness of data (useful but imperfect)
Visualization of each variable
Visualization of total market size
Considering min and max values
Feature importance based on model structure and on assumption uncertainty

### Out of Scope:
Correlation between variables (e.g. if price increases, quantities should be lower)
Binary events
Poisson distribution
The Example: Market for Arepas in Barcelona
Since I am writing this from holidays in Barcelona and I grew up in Venezuela, I decided to do this exercise using arepas as an example. Arepas are a typical Venezuelan food that has become more popular in Barcelona and Spain due to the large immigration from Venezuela.

I decided to approach this problem using a single restaurant as the unit of analysis and then extrapolating the revenues per year of a restaurant to the number of restaurants. To calculate the revenue per restaurant I will estimate
