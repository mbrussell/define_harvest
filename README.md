# Evaluate different timber harvest definitions
There are several approaches to determine whether or not a timber harvest has occured. This code replicates FIA EVALIDator estimates of timberland area harvested within a state and evaluates other definitions of timber harvest. Scripts first evaluate definitions of timber harvest then generate population-level estimates of timberland area harvested according to each definition.

## 1. Label whether or not a timber harvest occured
Example uses the state of Maine, but script can be used for any state data. The R script creates a new condition table (xx_COND_HARVEST) that labels each condition as bein harvested/non-harvested in the recent FIA panel (e.g., 2018-2022 for Maine). The following FIA data tables are required to run the scripts (can be obtained from [USFS FIA DataMart](https://apps.fs.usda.gov/fia/datamart/datamart.html):

* xx_COND
* xx_PLOT
* xx_TREE
* xx_TREE_GRM_MIDPT

The REF_SPECIES, REF_FOREST_TYPE, and REF_FOREST_TYPE_GROUP tables are also required to calculate the total acres harvested by forest type and forest type group.

The `run_harvest.Rmd` script calculates different harvest definitions for each state using the `calculate_harvest.Rmd` script (e.g., harvesting occurred when basal area removal exceeded 25% of pre-harvest basal area). In total, there are ten harvest definitions calculated:

1. **TRTCD**:	FIA code indicating a plot was treated by removing of one or more trees in a stand. Does not include stands that were disturbed.
2. **BA_RED**:	Plot basal area in live trees was reduced by greater than 25% at remeasurement.
3. **BA_RED_TREE**:	Plot basal area in live trees was reduced by greater than 25%, as indicated by an AGENTCD = 80 in FIA data.
4. **RD_RED**:	Plot relative density in live trees was reduced by greater than 10% at remeasurement. 
5. **RD_RED_TREE**:	Plot relative density in live trees was reduced by greater than 10%, as indicated by an AGENTCD = 80 in FIA data.
6. **TRTCD + BA_RED**:	FIA code indicating a plot was treated by removing of one or more trees in a stand  (and plot basal area in live trees was reduced) OR plot basal area in live trees was reduced by greater than 25% at remeasurement. Termed the “cutting and basal area reduction” variable.
7. **TRTCD + BA_RED_TREE**:	FIA code indicating a plot was treated by removing of one or more trees in a stand (and plot basal area in live trees was reduced) OR plot basal area in live trees was reduced by greater than 25%, as indicated by an AGENTCD = 80 in FIA data.
8. **TRTCD + RD_RED**:	FIA code indicating a plot was treated by removing of one or more trees in a stand (and plot basal area in live trees was reduced) OR plot relative density in live trees was reduced by greater than 10% at remeasurement.
9. **TRTCD + RD_RED_TREE**:	FIA code indicating a plot was treated by removing of one or more trees in a stand (and plot basal area in live trees was reduced) OR plot relative density in live trees was reduced by greater than 10%, as indicated by an AGENTCD = 80 in FIA data.
10. **FIA estimate (EVALIDator)**:	FIA estimate using TRTCD, including disturbed stands. FIA code indicating a plot was treated by removing one or more trees in a stand.

Pre-harvest conditions are estimated from the tree's estimated midpoint diameter (from the TREE_GRM_MIDPT table). A new condition table named xx_COND_HARVEST is created, where population-level estimates of timberland harvests can be calculated.

## 2. Generate population-level estimates of timberland area harvested

Example uses the state of Maine, but script can be used for any state data. This R script calculates population-level total timberland area harvested in a state from the most recent FIA panel (e.g., 2018-2022 for Maine). The following FIA data tables are required to run the scripts:

* xx_COND
* xx_PLOT
* xx_COND_HARVEST (created in previous step)
* xx_POP_STRATUM
* xx_POP_PLOT_STRATUM_ASSGN

The `run_pop_harvest.Rmd` script contains state data and runs `calculate_pop_harvest.Rmd` script to determine the total timberland area harvested in the state. 