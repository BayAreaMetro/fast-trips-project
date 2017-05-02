---
layout: default
title: Calibration Update
---

{:toc}

## Tier I: Quality of Service and Routes

The first tier of validation will use demand and chosen route information from the on-board surveys (OBS) and California Household Travel Survey (CHTS) and will evaluate the performance categories that require knowledge of routes including:

  - Path-based quality of service,  
  - Path coverage, and  
  - Path probabilities.

In order to reasonably satisfy our targeted performance of Fast-Trips across these categories, we will utilize calibration techniques such as:

  - Correction to base year networks or demand;  
  - Tweaking of run parameters such as the delta for the hyperpath;  
  - Addition or modification of the specification of various factors or their parameters.

### OBS

### CHTS Run 1

### CHTS Run 2

### CHTS Run 3


##### Inputs

**Network:** v1.11  
**Demand:**  CHTS v0.4  
**Configs:**  .. 

##### Results

**[Observed vs. Modeled Paths]()** 
**[Validation Summary Dashboard]()** 

##### Known Issues



### CHTS Run 4

Run on 2017-03-22
Run by Bhargava Sana at SFCTA

##### Summary of Changes  

- Same demand/networks as CHTS Run 3;
- 50% more penalty on xfers

##### Inputs

**Network:** v1.11  
[Access Egress Link Viewer](https://public.tableau.com/profile/lmz8249#!/vizhome/sfctanetwork_draft1_11_fareAccessandEgress/Dashboard1)** 
[Network Explorer](https://public.tableau.com/profile/lmz8249#!/vizhome/sfctanetwork_draft1_11_fareRoutesandTrips/TransitLinesMap)** 


**Demand:**  CHTS v0.4  
**Parameters:**  ..   
**Configs:**  .. 

##### Results

[Observed vs. Modeled Paths](https://public.tableau.com/profile/lmz8249#!/vizhome/ft_vs_obs_mapssfctanetworkv1_11_farechtsv0_4run20170322/ObsvsModeledDashboard)  

[Validation Summary Dashboard]()

[Box Location](https://app.box.com/files/0/f/22642907012/CHTS_run4)

##### Known Issues

Network:  

  - No KNR access links  
  - No PNR station capacities  
  - Missing access and xfer links  

Parameters:  

  - Transfers still to easy relative to access/egress distance  
  - Access and Egress parameters are not even; egress far too onerous.

Other:

  - Strange switching between Caltrain routes

##### Supporting Analysis




## Tier II: Regional Assignment and Computation Feasibility

The second tier of calibration will utilize the full regional demand in order to assess the two remaining performance targets: the assignment as a whole as well as the computational efficiency.  


## Tier III: Regional Assignment with Feedback

The final tier of calibration will assess the performance of the Fast-Trips parameters within a full SF-CHAMP model run.
