# Topic/Data Set/ SME
## Homeless house in Albuquerque 

#### Topic 1: Bed shortage evidence for Abq 
-  Business problem: A nonprofit applying for funding has to show which kind of bed Albuquerque lacks most (emergency shelter, transitional housing, or permanent supportive housing) to justify what it wants to build or expand.

-  Data science problem: Put two yearly datasets side by side for Albuquerque, people counted and beds available, and measure how the gap for each bed type has changed since 2007. 
- data: https://www.huduser.gov/portal/datasets/ahar/2024-ahar-part-1-pit-estimates-of-homelessness-in-the-us.html

-Model: Linear regression

#### Topic 1a: 
Business problem: A nonprofit applying for funding needs evidence of which kind of bed Albuquerque is shortest on (emergency shelter, transitional housing or permanent supportive housing), so it can justify what it wants to build or expand.

Data science problem: Using HUD’s 2007–2024 data for every region in the U.S., predict how many people sleep unsheltered from how many beds of each type a region has. Then check whether Albuquerque has more unsheltered people than its beds predict, and which bed type matters most in the model.

Target to predict: the number of unsheltered people in a region in a given year.

Inputs: emergency shelter beds, transitional housing beds, permanent supportive housing beds and year (plus population if you can add it).

Models: linear regression first (lecture 204), then ridge or lasso to see which bed types the model keeps as important (lecture 211). Score them with RMSE and MAE (lecture 203).

Backup version (classification): predict yes or no for whether a region’s unsheltered count goes up next year, using logistic regression (lecture 224).

The model shows which bed types go with fewer unsheltered people, not that adding beds would cause a drop. Say that in the write-up.




#### Topic 2: Is the system getting people housed faster?
- Business problem: A nonprofit or funder needs to know whether Albuquerque's homeless response system is getting better or worse at moving people into housing and keeping them housed, to decide where to focus funding and to report results to its board or funders.

- Data science problem: Track Albuquerque's yearly performance measures since fiscal year 2015 (how long people stay homeless, how many return to homelessness after being housed, how many become homeless for the first time) and compare them with similar cities.
- data: HUD "System Performance Measures Data Since FY 2015" (Excel, by community). Linked from https://www.huduser.gov/portal/datasets/ahar.html under "System Performance data files (XLSX) since FY 2015"

- Model: Linear regression

#### Topic 2a
Business problem: A nonprofit or funder needs to know whether Albuquerque is getting better or worse at moving people into housing and keeping them housed, so it can decide where to put funding and report results to its board.

Data science problem: Using HUD’s system performance data for every region in the U.S. since fiscal year 2015, predict how long people stay homeless from what each region has to work with. Then check whether Albuquerque does better or worse than predicted, and whether that has changed over time.

Target to predict: average number of days people stay homeless in a region in a given year.

Inputs:

Number of people becoming homeless for the first time
Beds by type (emergency shelter, transitional housing, permanent supportive housing, rapid re-housing). These come from the bed-count file from Topic 1, merged on region and year, so the two topics can share data.
Year

Models: linear regression (lecture 204), then ridge or lasso to see which inputs matter (lecture 211). Score with RMSE and MAE (lecture 203).

How it answers the business question: For each year, compare Albuquerque’s actual days homeless with what the model predicts. If Albuquerque goes from above the prediction to below it, the system is improving relative to similar regions.

Alternate target: the percent of people who return to homelessness within two years after being housed. Use it if the funder cares more about keeping people housed than about getting them housed fast.



#### Topic 4: Is Albuquerque an outlier among peer cities?
- Business problem: A nonprofit or advocate asking the city or state for funding needs to show whether Albuquerque's homelessness rate is higher or lower than expected for a city with its rents and housing market, to argue that local conditions (not just national trends) call for action.

- Data science problem: Using data for all U.S. communities, build a regression model that predicts the homelessness rate from housing and economic factors (rent, evictions, crowding, poverty), then compare Albuquerque's actual rate with the model's prediction.
- data: HUD Homelessness Prediction Model dataset (CSV with codebook, one row per community, 2011-2017). Data page: https://www.huduser.gov/PORTAL/node/8208. Mirror download: https://www.datalumos.org/datalumos/project/219151/version/V3/view

- Model: Linear regression (204) plus ridge/lasso

#### Topic 5: Where to target eviction prevention
- Business problem: An eviction prevention nonprofit (legal aid, rental assistance) needs to know which Albuquerque neighborhoods to focus outreach on before families lose their housing.

- Data science problem: Find Albuquerque census tracts with high and rising eviction filings, group tracts with similar patterns (clustering), and test which neighborhood characteristics predict high filing rates.
- data: Eviction Lab (Princeton) Eviction Tracking System, Albuquerque weekly and monthly filings by census tract (CSV). https://evictionlab.org/eviction-tracking/get-the-data/

- Model Logistic regression

## Political/policy 

#### Topic 1: Predicting whether a bill passes the New Mexico Legislature

- Business problem: Advocates, nonprofits, and lobbyists have limited time each
60/30-day session. Which bills are worth fighting for or against? What features
of a bill at introduction (sponsors, committee path, type, subject) are
associated with it becoming law?

- Data science problem: Binary classification. Each row is one bill; outcome is
signed into law (1) vs not (0). Features known at introduction only (avoid
leakage from later actions). Logistic regression with class balancing;
report precision/recall/F1 and a confusion matrix, not accuracy alone.
Secondary descriptive piece: party loyalty / party-line vote rates by chamber.

- Data location: Open States (now Plural Policy) bulk data — per-session CSVs
of bills, actions, sponsorships, votes, vote_people, scraped nightly from
nmlegis.gov, public domain. https://open.pluralpolicy.com/data/
Known issue: legislator IDs are often blank in vote_people; joining
legislators to votes needs name cleanup. [VERIFY on load: columns, row counts]

- Nonprofit angle: any NM advocacy nonprofit (health, housing, etc.) that
tracks bills each session.


#### Topic 2: Where do bills die? Committee bottlenecks in the New Mexico Legislature

- Business problem: Nonprofits and advocates have limited staff and a short
session (60 days in odd years, 30 in even). They need to know where bills
actually stall or die so they can decide which committee hearings to show up
for, which committee members to meet with, and how early in the session to
act. Right now this knowledge lives in the heads of experienced lobbyists;
the goal is to make it visible from the public record.

- Data science problem: Mostly descriptive analysis with a small optional
model.
  1. Reconstruct each bill's path: sequence of committee referrals, dates
     entered and left, and final outcome (signed, vetoed, pocket-vetoed,
     passed one chamber, died in committee, never heard).
  2. For each committee: number of bills referred, share that moved on,
     share that died there, median days held, and how this varies by
     session, chamber, sponsor party, and bill type.
  3. Optional model: logistic regression (lecture 224) predicting "dies in
     first committee" from features known at referral (committee,
     chamber, sponsor party, bipartisan sponsorship, bill type,
     session length). Report F1 and a confusion matrix, not accuracy alone.
Key risks: labeling the outcome correctly from action text (bills can die
by never being scheduled, which leaves no "killed" action); avoiding
leakage by using only information available at referral time.

- Data location: Open States (now Plural Policy) bulk data — per-session CSVs
for New Mexico covering bills, bill actions (with dates), sponsorships,
and votes, scraped from nmlegis.gov, public domain, loadable in Colab
with pd.read_csv. https://open.pluralpolicy.com/data/
Session span to use: several regular sessions (e.g., 2019 through 2025) so
committee patterns are not driven by one unusual year.
[VERIFY on load: column names, how committee referrals appear in the
actions table, row counts per session.]
Supplementary: committee membership lists from nmlegis.gov (hand-collected
or scraped) if the group wants to connect bottlenecks to specific members.


#### Topic 3: How Albuquerque City Council works — where legislation stalls and
who votes together

- Business problem: Nonprofits that need something from City Council (funding,
a zoning change, an ordinance) have to decide when to engage, which
committee to show up for, which councilors to meet with, and whether an
item is likely to be contested. Experienced lobbyists carry this in their
heads; most nonprofits don't have one. The goal is to turn the public
Council record into a plain-language guide any organization can use.

- Data science problem: Descriptive analysis in two linked parts, with an
optional model.
  Part A — Legislative flow (C1)
    1. For each ordinance (O-), resolution (R-), and other matter type:
       introduction date, committee referrals, dates in and out of each
       committee, final action and date.
    2. Metrics by committee and by legislation type: count referred,
       median days held, share deferred/amended/withdrawn, share passed.
    3. Sponsorship profiles: what each councilor introduces (by type and
       keyword), how often "by request" (Administration) items pass vs
       councilor-originated items.
  Part B — Voting patterns (C2)
    4. Share of votes that are unanimous vs split, by year and item type.
    5. On split votes: pairwise agreement matrix across councilors
       (heatmap), and which item types produce splits (zoning, budget,
       public safety, etc., tagged by keyword).
  Optional model: logistic regression predicting "vote will be split"
    from features known at introduction (matter type, sponsor, committee
    path, by-request flag, keyword tags). Report F1 and a confusion matrix.
Key risks: with nine councilors and mostly unanimous votes, the split-vote
subset may be a few hundred rows over several years — enough to describe,
possibly thin to model. Keyword tagging will miss some items; hand-check a
sample. Avoid leakage by not using post-introduction actions as features.

- Data location: Granicus Legistar Web API, public JSON, no key required for
most clients. Endpoints (per the API's own examples):
  https://webapi.legistar.com/v1/{Client}/matters        — legislation
  https://webapi.legistar.com/v1/{Client}/matters/{id}/histories — actions
  https://webapi.legistar.com/v1/{Client}/eventitems/{id}/votes  — roll calls
  https://webapi.legistar.com/v1/{Client}/persons        — councilors
Client slug for Albuquerque is expected to be "cabq" (the city's portal is
cabq.legistar.com). Results are paged at 1,000 rows; use $top/$skip.
Loadable in Colab with requests + pd.json_normalize.
[VERIFY FIRST: that the cabq slug returns data, the date range available,
and which fields are populated for votes. This is the project's go/no-go
check and should happen before anything else.]
Fallback if the API is blocked or thin: Council action summaries (PDF) from
cabq.gov/council — hand-entry of votes for a sample of years.

Nonprofit fit: Any organization that interacts with City Council. Deliverable
they could use: a short "How to get something through Council" brief with
(a) a committee map showing where items spend time, (b) a councilor
sponsorship profile page, (c) a voting-bloc heatmap, and (d) interactive
Plotly charts filterable by year and item type.

















 
