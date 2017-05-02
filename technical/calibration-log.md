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

### OBS Run 1

*Run on:*   June 30, 2016  
*Run by:*   Lisa at MTC  

##### Summary of Changes  

##### Inputs

**Network:**   
**Demand:**  OBS v0.1  
**Configs:**  [Pathweights](https://app.box.com/files/0/f/8380345213/1/f_72033980657)  

##### Results

*[Outputs](https://app.box.com/files/0/f/8648895105)*   
**[Vehicle Loads](https://public.tableau.com/profile/lmz8249#!/vizhome/FastTrips-VehicleLoads-OBS/RouteDrilldown)**   
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

No drive access or egress for now.  
Memory issues

##### Supporting Analysis

##### Bellwether Paths

##### Actions Taken

Addressed memory issues.

### OBS Run 2

*Run on:*   August 16, 2016  
*Run by:*   Lisa at MTC  

##### Summary of Changes  

##### Inputs

**Network:**  v1.4  
**Demand:**  v1.0  
**Configs:**  [Pathweights](https://app.box.com/files/0/f/8380345213/1/f_72033980657) 

##### Results

*[Outputs](https://app.box.com/files/0/f/10959543824/OBS_fasttrips_demand_v1.0_stochastic_iter2_cap)*      

##### Known Issues

Walk Access/Egress to/from Rail
Xfer links uni-directional rather than bi-directional
Demand input error: person IDs not unique

##### Supporting Analysis

##### Bellwether Paths

3072 - No walk egress from teh N line to TAZ475
Person IDs 35, 377, 517


##### Actions Taken

- Made xfers bi-directional

### OBS Run 3

*Run on:*   October 7, 2016  
*Run by:*   Lisa at MTC  

##### Summary of Changes  

##### Inputs

**Network:**   
**Demand:**  v1.1  
**Configs:**  .. 

##### Results

*[Outputs](https://app.box.com/files/0/f/11611885837)*     
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

Get memory overflow with too many trips.

##### Supporting Analysis

##### Bellwether Paths

##### Next Steps

### CHTS Run 0

*Run on:*   July 19, 2016  
*Run by:*   Lisa at MTC  

##### Summary of Changes  

##### Inputs

**Network:**   
**Demand:**  [CHTS v0.1](https://app.box.com/files/0/f/8885475158)  
**Configs:**  .. 

##### Results

*[Outputs](https://app.box.com/files/0/f/8935480610)*     
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

No BART Boards.

##### Supporting Analysis

##### Bellwether Paths

### CHTS Run 0.1

*Run on:*   October 7, 2016   
*Run by:*   Lisa at MTC   

##### Summary of Changes  

##### Inputs

**Network:**   v1.9  
**Demand:**    CHTS v0.2   
**Configs:**  .. 

##### Results

*[Outputs](https://app.box.com/files/0/f/11612101663)*       
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

##### Supporting Analysis

##### Bellwether Paths

### CHTS Run 1

*Run on:*   December 16th, 2016  
*Run by:*   Lisa at MTC  

##### Summary of Changes  

##### Inputs

**Network:**     
**Demand:**   CHTS v0.3  
**Configs:**  ..   

##### Results

*[Outputs](https://app.box.com/files/0/f/14572736917)*      
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

##### Supporting Analysis

##### Bellwether Paths

### CHTS Run 2

*Run on:*   Feb 6, 2017   
*Run by:*   Bhargava at SFCTA   

##### Summary of Changes  

##### Inputs

**Network:**  SFCTA v1.10    
**Demand:**  v0.4   
**Configs:**  .. 
 
##### Results

*[Outputs]()*     
**[Observed vs. Modeled Paths]()**   
**[Validation Summary Dashboard]()**   

##### Known Issues

##### Supporting Analysis

##### Bellwether Paths

### CHTS Run 3

*Run on:*   March 21, 2017   
*Run by:*   Bhargava at SFCTA   

##### Inputs

**Network:** v1.10  
**Demand:**  CHTS v0.4    
**Configs:**  ..   

##### Results

*[Outputs](https://app.box.com/files/0/f/17999192280/CHTS_fasttrips_demand_v0.4_stochastic_iter1_nocap_networkv1.10)*     
**[Observed vs. Modeled Paths](https://public.tableau.com/profile/lmz8249#!/vizhome/ft_vs_obs_mapssfctanetworkv1_11_farechtsv0_4run20170322/ObsvsModeledDashboard)**   
**[Validation Summary Dashboard]()**   

##### Known Issues

  - xfer not onerous enough  
  - egress penalty too high  
  - no dwell times  
  - no KNR  
  - no PNR lot capacities  

##### Supporting Analysis

[Routes where they transfer between different trips on same route](https://docs.google.com/spreadsheets/d/11ozYkQBksn_8EM4wpAX6E08qUJQqdiedj2Uc8EnblkQ/edit?usp=sharing)

##### Bellwether Paths

__Issue__

BART paths for the following should be found; access/egress links appear to exist.

Peninsula -> SF  
person_id: `1379781_2` person_trip_id: 6

East Bay <-> SF  
`1498957_1` person_trip_id: 14  
`3006352_2` person_trip_id: 7  
`3007326_2` person_trip_id: 5  


`7162320_2`  
_Issue_: Path that uses bart - but not sure how.  CHTS must have coded a phantom BART trip or didn't identify an intermediate stop.

`1407624_2`   
_Issue_: High probability paths have a transfer to the 19 Polk rather than just getting on the 47 or 49.  The 47 and 49 are found, but given <1% probabilities.  This is b/c the 19 has an egress distance of 0.06  whereas 47/49 have egress distance of 0.21. This is a cost difference of ~13 whereas the xfer only costs 5

`1474991_2`	  
_Issue_: Tradeoff between egress distance and transfers.  Transfers are too cheap.

`3006352_2` person_trip_id: 7    
_Issue_: Tradeoff between egress distance and transfers.  Transfers are too cheap.

_Issue_: Suspicious Caltrain-to-Caltrain transfers  

  * `2625922_1`, 3 (Bb2N to Bb1N)  
  * `2630962_2`, 11 (AB2N to AB1N)  
  * `2630962_2`, 19 (AB2N to AB1N)  
  * `3016440_1`. 7 (AB2N to AB1S (???))  

### CHTS Run 4

Run on 2017-03-22  
Run by Bhargava Sana at SFCTA  

##### Summary of Changes  

- Same demand/networks as CHTS Run 3;  
- 50% more penalty on xfers  

##### Inputs

**Network:** v1.11  
[Access Egress Link Viewer](https://public.tableau.com/profile/lmz8249#!/vizhome/sfctanetwork_draft1_11_fareAccessandEgress/Dashboard1)**   
[Network  Explorer](https://public.tableau.com/profile/lmz8249#!/vizhome/sfctanetwork_draft1_11_fareRoutesandTrips/TransitLinesMap)**   


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

[Path Traces](https://www.backcountry.com/Store/catalog/search.jsp?q=mammut&s=u)

##### Bellwether Paths

`1710214_1` : FT doesn't find anything N of Geary, including the observed route downtown via the 1AX

`1407624_2`	

_Previous Issue_ High probability paths have a transfer to the 19 Polk rather than just getting on the 47 or 49.  The 47 and 49 are found, but given <1% probabilities.  This is b/c the 19 has an egress distance of 0.06  whereas 47/49 have egress distance of 0.21. This is a cost difference of ~13 whereas the xfer only costs 5

_Run 4_: FT still strongly preferring the strange path with the transfer to the 9 and 19.  

`1474991_2`	

_Previous Issue_: Tradeoff between egress distance and transfers.  Transfers are too cheap.

_Run 4_: Fixed!

`3006352_2` person_trip_id: 7    

_Previous Issue_: Tradeoff between egress distance and transfers.  Transfers are too cheap.

_Run 4_: Still there

`1710214_1` 
Run 3: FT doesn't find anything N of Geary, including the observed route downtown via the 1AX
Run 4: same issue

## Tier II: Regional Assignment and Computation Feasibility

The second tier of calibration will utilize the full regional demand in order to assess the two remaining performance targets: the assignment as a whole as well as the computational efficiency.  

## Tier III: Regional Assignment with Feedback

The final tier of calibration will assess the performance of the Fast-Trips parameters within a full SF-CHAMP model run.
