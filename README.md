# Energy Market Linear Modelling
## Project Overview
* Imported and merged various NEM datasets for highlight features such as demand, trading prices and import/export limits.
* Cleaned the data, standardising datetime variables and handling missing data.
* Feature-engineered new values including a renewables binary feature, and a region feature.
* Using the real-world NEM data an arbitrary objective was created and a linear model was built to imitate how the market would work to minimise prices. 

## Resources
***Python Version:*** 3.13   
***Packages***  
Data cleaning and analysis: numpy, pandas, matplotlib, seaborn   
Model production: pulp  
***NEM data:*** https://nemweb.com.au/Data_Archive/Wholesale_Electricity/MMSDM/2024/MMSDM_2024_04/MMSDM_Historical_Data_SQLLoader/DATA/
* PUBLIC_DVD_DISPATCH_UNIT_SCADA_202403010000.CSV
* PUBLIC_DVD_DISPATCHREGIONSUM_202403010000
* PUBLIC_DVD_TRADINGPRICE_202403010000
* PUBLIC_DVD_DISPATCHINTERCONNECTORRES_202403010000
 
[NEM registration and exemption list for generator information](https://www.aemo.com.au/-/media/Files/Electricity/NEM/Participant_Information/NEM-Registration-and-Exemption-List.xls) (region, renewables status).

## Data Cleaning
* Ensured proper headers for each df.
* Assigned region IDs to DUIDs (generators), utilising information from the NEM registration and exemption list.
* Stanadardiesd datetime format across datasets.
* Categorised each generator as renewable or non-renewable, again utilising info from the NEM registration and exemption list.
* Feature engineered a max energy output feature for each generator.
* Assigned regions to interconnectors and generators.
* Merged the datasets and grouped them on settlement date, region and renewable status to facilitate modelling.

## Modelling
### Model Objective
The model was built on an arbitrary objective that may not replicate the actual energy market but uses real market data to depict how a carbon tax may influence energy supply and pricing. To enable this, DUIDs (generators) were earlier classified as renewable or non-renewable. In the model, any electricity being produced by non-renewable sources was priced at RRP*1.01, whereas renewable sources were simply priced at RRP. Regions could export and import between themselves according to real-world limits. The overall objective was to minimise the price of energy.
### Model results
* On average, 13% of energy production was from a renewable source.
* Time series data depicting energy production from each region:
![image](https://github.com/reversed-xelA/EnergyMarketModelling/assets/141697086/f4160e71-9a86-4b37-9792-19a78a206151)  
* Renewable generation across regions:
![image](https://github.com/reversed-xelA/EnergyMarketModelling/assets/141697086/d26036d4-b9f0-4169-a33b-283a27056c0e)  
* Non-renewable generation over time:
![image](https://github.com/reversed-xelA/EnergyMarketModelling/assets/141697086/58393a35-cea2-4a31-a2bc-cec29586059f)  


