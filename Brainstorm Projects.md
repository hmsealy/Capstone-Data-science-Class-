# Topic/Data Set/ SME
## Homeless house in Albuquerque 

#### Topic 1: Bed shortage evidence for Abq 
-  Business problem: A nonprofit applying for funding has to show which kind of bed Albuquerque lacks most (emergency shelter, transitional housing, or permanent supportive housing) to justify what it wants to build or expand.

-  Data science problem: Put two yearly datasets side by side for Albuquerque, people counted and beds available, and measure how the gap for each bed type has changed since 2007. 
- data: https://www.huduser.gov/portal/datasets/ahar/2024-ahar-part-1-pit-estimates-of-homelessness-in-the-us.html

#### Topic 2: Is the system getting people housed faster?
- Business problem: A nonprofit or funder needs to know whether Albuquerque's homeless response system is getting better or worse at moving people into housing and keeping them housed, to decide where to focus funding and to report results to its board or funders.

- Data science problem: Track Albuquerque's yearly performance measures since fiscal year 2015 (how long people stay homeless, how many return to homelessness after being housed, how many become homeless for the first time) and compare them with similar cities.
- data: HUD "System Performance Measures Data Since FY 2015" (Excel, by community). Linked from https://www.huduser.gov/portal/datasets/ahar.html under "System Performance data files (XLSX) since FY 2015"

#### Topic 4: Is Albuquerque an outlier among peer cities?
- Business problem: A nonprofit or advocate asking the city or state for funding needs to show whether Albuquerque's homelessness rate is higher or lower than expected for a city with its rents and housing market, to argue that local conditions (not just national trends) call for action.

- Data science problem: Using data for all U.S. communities, build a regression model that predicts the homelessness rate from housing and economic factors (rent, evictions, crowding, poverty), then compare Albuquerque's actual rate with the model's prediction.
- data: HUD Homelessness Prediction Model dataset (CSV with codebook, one row per community, 2011-2017). Data page: https://www.huduser.gov/PORTAL/node/8208. Mirror download: https://www.datalumos.org/datalumos/project/219151/version/V3/view

#### Topic 5: Where to target eviction prevention
- Business problem: An eviction prevention nonprofit (legal aid, rental assistance) needs to know which Albuquerque neighborhoods to focus outreach on before families lose their housing.

- Data science problem: Find Albuquerque census tracts with high and rising eviction filings, group tracts with similar patterns (clustering), and test which neighborhood characteristics predict high filing rates.
- data: Eviction Lab (Princeton) Eviction Tracking System, Albuquerque weekly and monthly filings by census tract (CSV). https://evictionlab.org/eviction-tracking/get-the-data/


 
