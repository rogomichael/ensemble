# Ensemble Model Outputs Instructions
https://github.com/CDCgov/rsv-forecast-hub/blob/main/model-output/README.md
This repository contains output files for VBD-MODE SP3 forecasting ensemble model outputs

## Data submission instructions
The intention is to provide all contributors to the VBD-MODE near-future forecasting (SP3) with all the information they need to submit projections.

All projections should be submitted directly to the model-output/ folder. Data in this directory should be added to the repository  through a pull request.

### Subdirectory

Each sub-directory within the model-output/ directory has the format:

    team-model

where


- `team` is the abbreviated team name and
- `model` is the  abbreviated name of your model.

Both `team` and `model` should be less than 15 characters, and not include hyphens nor spaces.


### Metadata

Each submission team should have an associated `metadata` file. The file should be submitted with the first forecast in the  model-metadata/ folder, in a file named: team-model.yml.

For more information on the metadata file format, please consult the associated README in the model-metadata/ folder


### Model Results

Each model results file within the model-outputs/ subdirectory should follow naming convention:

    Disease-YYYY-MM-DD-team-model.csv

where

- `Disease` is the target disease. Disease has to be one of the following options


    -    TBE


    -	Lyme


    -	WNF


    -	Dengue


 - `YYYY` is the 4 digit year,


- `MM` is the 2 digit month,


- `DD` is the 2 digit day. Here DD should be set to 01, 


- `team` is the team name, and


- `model` is the name of your model.

The date `YYYY-MM-DD` should correspond to the start date for the forecasting (Initial time of the simulations). Consult the main README for information regarding the expected start date options. 

### TO DO (Set the start date based on agreed structure i.e ISO or otherwise). For example, submission from a team named exampleteam with a model named examplemodel for a reference date of September, 09, 2026 would be named:
    `2026-09-09-exampleteam-examplemodel.csv`

The `team` and `model` in this file must match the `team` and `model` in the directory this file is in. Both team and model should be less than 15 characters, alphanumeric and underscores only, with no spaces or hyphens. Submission of both targets- quantiles and samples must be in the same monthly csv submission file.


### Model results file format

The output file must be in a CSV file with the following columns (in any order):
-   `reference_date`
-   `origin_date`
-   `target`
-   `horizon`
-   `location`
-   `output_type`
-   `output_typeID`
-   `value`


Each row in the file is a specific type for a coupled-model-scenario pair for a location on a particular date for a particular target.

-    `Column format`
-    `Column Name`:	Accepted Format
-    `origin_date`:    character, date
-    `target`:	character
-    `horizon`:	numeric, integer
-    `location`:	character
-    `output_type`:	character
-    `output_type_id`:	numeric, character, logical (NA)
-    `value`:	numeric
-    `origin_date`

Values in the origin_date column must be a date in the format

    YYYY-MM-DD

The origin_date is the start date for the scenario projections (initial time for the simulation). The origin_date and date in the filename should correspond. Please read the main README for a full list of accepted origin_date options.

## target
The submission can contain multiple output_type information:


    •	A "mean" value and an optional set of quantiles for all targets. We will call this format "quantile" type output. For more information, please consult the quantile section.

The requested targets are:


    •	`monthly case reports`

Optional target:


    •	`ADD OTHER OPTIONS`

Values in the target column must be one of the following character strings:


    •	"rep"


    •	ADD OTHER OPTIONS
    "rep"
This target is the (monthly accumulated) number of reported cases during the month that is N (defined by the corresponding value in the horizon column) months after origin_date.
## horizon
Values in the horizon column must be an integer (N) between 1 and 360 (30 years projections).

Horizon value representing the associated target value during the N months after origin_date. Add a link to the main README.
## location
Values in the location column must be one of the "locations ID" listed in the main README. (This could be NUTS-3-IDs) 
## output_type
Values in the output_type column are either


    •    samples
    •    "mean" or
    •	"quantile" 

### TOD DO: decide whether (Samples can either encode both temporal and spatial dependency across forecast horizons and locations or just encode temporal dependency across horizon but treats each location independently.)

## output_type_id
Values in the output_type_id column specify identifying information for the output type.

If the corresponding output_type value (value on the same row) is mean then the value in the output_type_id column is NA.
## quantile output
When the predictions are quantiles, values in the output_type_id column are a quantile probability level in the format

    0.###

For quantile forecast, this value indicates the quantile for the value in this row.

Teams should provide the following 2 quantiles:

    0.025 0.975

### TO DO: Refine the sample output below 

## sample output

When the predictions are samples, values in the output_type_id column are indexes for the samples. The output_type_id is used to indicate the dependence across multiple task id variables when samples come from a joint predictive distribution. For example, samples from a joint predictive distribution across horizons for a given location, will share output_type_id for predictions for different horizons within a same location, as shown in the table below:

| origin_date|horizon| location | output_type| output_type_id | value |
|:---------- |:-----:|:-----:| :-------- | :------------ | :---- |
| 2026-09-09 | -1      |  DE254 | sample | s0 | - |
| 2026-09-09 |  0      |  DE254 | sample | s0 | - |
| 2026-09-09 |  1      |  DE254 | sample | s0 | - |
| 2026-09-09 | -1      |  DE110 | sample | s1 | - |
| 2026-09-09 |  0      |  DE110 | sample | s1 | - |
| 2026-09-09 |  1      |  DE110 | sample | s1 | - |
| 2026-09-09 | -1      |  DE254 | sample | s2 | - |
| 2026-09-09 |  0      |  DE254 | sample | s2 | - |
| 2026-09-09 |  1      |  DE254 | sample | s2 | - |
| 2026-09-09 | -1      |  DE110 | sample | s3 | - |
| 2026-09-09 |  0      |  DE110 | sample | s3 | - |
| 2026-09-09 |  1      |  DE110 | sample | s3 | - |

## Forecast Validation

To ensure proper data formatting, pull requests for new data in
`model-output/` will be automatically run. Optionally, you may also run these validations locally.

### Pull request forecast validation

When a pull request is submitted, the data are validated through [Github Actions](https://docs.github.com/en/actions) which runs the tests present in [the vbd-modeValidations package](`create INHOUSE validations`). The intent for these tests are to validate the requirements above. Please [let us know](../../../issues) if you are facing issues while running the tests.

### Local forecast validation

Optionally, you may validate a forecast file locally before submitting it to the hub in a pull request. Note that this is not required, since the validations will also run on the pull request. To run the validations locally, follow the steps described [here](create a page on how to run local validations).

