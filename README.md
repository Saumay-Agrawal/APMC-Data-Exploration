# APMC-Data-Exploration


## Objectives
1. Test and filter outliers.
2. Understand price fluctuations accounting the seasonal effect
	1. Detect seasonality type (multiplicative or additive) for each cluster of APMC and commodities
	2. De-seasonalise prices for each commodity and APMC according to the detected seasonality type
3. Compare prices in APMC/Mandi with MSP(Minimum Support Price)- raw and deseasonalised
4. Flag set of APMC/mandis and commodities with highest price fluctuation across different commodities in each relevant season, and year.


## Approach and Methodology

This is merely a summary of the approach and methodology used to reach the objectives. For details, refer the respective python notebooks.

#### Data Cleaning
* Handled the case difference in commodity name, and minor typos.
* Found null values and substituted them using forward filling technique.
* Found zero price values and substituted them using appropriate technique.
* Saved the cleaned files in ./data/

#### Outlier Detection and Filtering
* Detected outliers for each commodity separately.
* Used the modal price as outlier indication, because it is an overall representative of prices and we work with these values later also.
* Removed the outliers using IQR method.
* Scatter plots comparing data with and without outliers for each commodity can be found in ./data/outlier-detection/

#### Seasonality Detection and Filtering
* Detected seasonality type (multiplicative/additive) for each combination of APMC and Commodity, and discretely.
* Used the autocorrelation of residuals to decide which model suits better additive or multiplicative.
* Deseasonalised the series according to type of seasonality detected.
* Plotted lines plots comparing raw and deseasonalised modal prices, can be found in ./visuals/deseasonalisation/
	* /apmc/ - contains plots for APMC-wise analysis by aggregating the commodities (an overview of every APMC cluster)
	* /commodity/ - contains plots for Commodity-wise analysis by aggregating the APMCs (an overview of every Commodity cluster)
	* /apmc-commodity/ - contains plots for the analysis of each commodity in each APMC.

#### Raw, Deseasonalised and Minimum Support Price Comparison
* Combined both the datasets for the common Commodities.
* Deseasonalised the modal prices for these commodities.
* Adjusted the MSP timeseries for easy merging with modal price timeseries.
* Created line plots for fulfilling the purpose (can be found at ./visuals/msp-comparison/)
	* /commodity/ - contains plots for the Commodity-wise price comparison (Commodity cluster overview)
	* /apmc-commodity/ - contains plot for price comparison for each commodity in each APMC.

#### Find set of APMC/Commodity with highest price fluctuations
* Used two methods for finding fluctuations
	* General method : Fluctuation = Maximum price - Minimum price
	* Ratio method: Fluctuation = Maximum price / Minimum price
* Plotted price fluctuations along with the minimum, maximum and modal price values for each APMC and commodity pair. (./visuals/fluctuations/apmc-commodity/)
* Aggregated and restructured data 
	* by year and commodities to find commodities with highest fluctuation in prices per year
	* by year, commodities and APMCs to find APMCs with highest fluctuation for each commodity per year.
* The results were plotted in form of heatmaps. (./visuals/fluctuations/commodity-year)
