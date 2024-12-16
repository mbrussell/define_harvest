# define_harvest
Replicates FIA EVALIDator output of timber harvest occurrence, and evaluates other definitions of timber harvest.

Current example uses the state of Maine. The R script replicates FIA EVALIDator output to obtain total acres harvested in the most recent FIA panel (e.g., 2018-2022 for Maine).

The run_harvest.Rmd script calculates different harvest definitions using the calculate_harvest.Rmd script (e.g., harvesting occurred when basal area or relative density removed exceeds 25% of pre-harvest basal area). 