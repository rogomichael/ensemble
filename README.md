# Ensemble Model Outputs Instructions
This repository contains output files for VBD-MODE SP3 forecasting ensemble model outputs

Data submission instructions
This page is intended to provide all contributors to the VBD-MODE near-future forecasting (SP3) with all the information they need to submit projections.

All projections should be submitted directly to the model-output/ folder. Data in this directory should be added to the repository  through a pull request.


## Subdirectory
Each sub-directory within the model-output/ directory has the format:

   team-model

where


•	team is the abbreviated team name and


•	model is the  abbreviated name of your model.

Both team and model should be less than 15 characters, and not include hyphens nor spaces.


## Metadata
Each submission team should have an associated metadata file. The file should be submitted with the first projection in the  model-metadata/ folder, in a file named: team-model.yml.

For more information on the metadata file format, please consult the associated README in the model-metadata/ folder


## Model Results
Each model results file within the model-outputs/ subdirectory should follow naming convention:

Disease-YYYY-MM-DD-team-model.csv

where


•	Disease is the target disease. Disease has to be one of the following options


o	TBE


o	Lyme


o	WNF


o	Dengue


o	ADD MORE OPTIONS IF NEEDED


•	YYYY is the 4 digit year,


•	MM is the 2 digit month,


•	DD is the 2 digit day. Here DD should be set to 01, 


•	team is the team name, and


•	model is the name of your model.

The date YYYY-MM-DD should correspond to the start date for the scenarios projection (Initial time of the simulations). Consult the main README for information regarding the expected start date options.  

The team and model in this file must match the team and model in the directory this file is in. Both team and model should be less than 15 characters, alphanumeric and underscores only, with no spaces or hyphens.


Model results file format
The output file must contain eight columns (in any order):


•	origin_date


•	GCM


•	scenarioID


•	target


•	horizon


•	location


•	output_type


•	output_typeID


•	value

No additional columns are allowed. (WE MIGHT WANT TO ADD OPTIONAL COLUMNS)

Each row in the file is a specific type for a coupled-model-scenario pair for a location on a particular date for a particular target.
Column format
Column Name	Accepted Format
origin_date	character, date
GCM	character
scenarioID	character
target	character
horizon	numeric, integer
location	character
output_type	character
output_type_id	numeric, character, logical (NA)
value	numeric
origin_date
Values in the origin_date column must be a date in the format

YYYY-MM-DD

The origin_date is the start date for the scenario projections (initial time for the simulation). The origin_date and date in the filename should correspond. Please read the main README for a full list of accepted origin_date options.
GCM
GCM is the Global Climate Models (GCM) used to force the model. Specifically, GCM is the abbreviation of the GCM.  Please read the main README for a full list of accepted GCM options.
scenarioID
scenarioID is the ID for the selected scenario, e.g., SSP126 for the low greenhouse gas emissions Shared Socioeconomic Pathway (SSP) scenario. For a full list of accepted ScenarioIDs and the description of the scenarios please read the main README.
target
The submission can contain multiple output_type information:


•	A "mean" value and an optional set of quantiles for all targets. We will call this format "quantile" type output. For more information, please consult the quantile section.

The requested targets are:


•	monthly case reports

Optional target:


•	ADD OTHER OPTIONS

Values in the target column must be one of the following character strings:


•	"rep"


•	ADD OTHER OPTIONS
"rep"
This target is the (monthly accumulated) number of reported cases during the month that is N (defined by the corresponding value in the horizon column) months after origin_date.
horizon
Values in the horizon column must be an integer (N) between 1 and 360 (30 years projections).

Horizon value representing the associated target value during the N months after origin_date. Add a link to the main README.
location
Values in the location column must be one of the "locations ID" listed in the main README. (This could be NUTS-3-IDs) 
output_type
Values in the output_type column are either


•	"mean" or


•	"quantile" (optional)
output_type_id
mean
If the corresponding output_type value (value on the same row) is mean then the value in the output_type_id column is NA.
quantile
If the corresponding output_type value (value on the same row) is quantile then the values in the quantile column are quantiles in the format

0.###

For quantile scenarios, this value indicates the quantile for the value in this row.

Teams should provide the following 2 quantiles:

0.025 0.975

This means that if a team wants to submit quantiles there needs to be 1+2 rows for every origin_date``-``GCM-scenarioID-target+horizon-location group (combination)
value
Values in the value column are non-negative numbers integer or with one decimal place indicating the "quantile" prediction for this row.

For a "quantile" prediction, value is the inverse of the cumulative distribution function (CDF) for the origin_date-GCM-scenarioID-target+horizon-location, and quantile associated with that row.


Model output validation
To ensure proper data formatting, pull requests for new data or updates in model-output/ and model-metadata/ are validated before they are merged into the main branch of the VBD-MODE Scenario Projection HUB.


