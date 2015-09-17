---
title: "The Wheel of Progress - Summer 2015"
author: Elizabeth
image: /img/posts/beach-pneumatic-tube.png
comments: true
layout: post
tags: [meta]

---

*The following is a brief update on the overall status of the Fast-Trips implementation project.*

The Tri-Agency group implementing Fast-Trips has been making significant technical progress
 on: software development, data standards, network development, demand evaluation, and 
 evaluating route choice methodology.  In administrative news, Mark Simonson has joined 
 the Management Team from PSRC and Jeff Hood has joined from our consultant bench in order 
 to take a lead on the route choice estimation task.

In software development, we have completed a refactoring of Fast-Trips to Python and fixed 
many bugs along the way.  In order to have a tolerable run time (<6 hours), we:  

 - vectorized some of the operations so they could be completed in Pandas data frames;  
 - instituted multi-processing for the path-building; and  
 - used a C++ extension for loops that could not be vectorized.  

Representing a 40X speedup in itself, the [C++ extension]({{ site.baseurl }}/2015/09/01/speed-demons/) 
is as generalized as possible in 
order to keep all the day-to-day and month-to-month control within the much more usable 
and legible Python.  The next step is to do feature development on modal biases and 
selections and then to optimize for skimming procedures. 

In data standards, we have developed both a [transit network data standard]({{ site.baseurl }}/library/T2-NetworkDesign-WorkingCopy-July2015.pdf) that is an 
extension of GTFS (the most complex part being fare representation) and a demand data 
standard]({{ site.baseurl }}/library/T3-TransitDemandData-WorkingCopy-July2015.pdf) that 
will work equally well for auxiliary and activity-based demand.  
The networks team has moved on to develop Python code to create the networks from 
both EMME/SoundCast and SF-CHAMP/Network Wrangler using agreed upon methodology for 
translating headways to schedules, while the demand team is finalizing methodology to 
adjust our demand that we will use for route choice estimation based on the GPS data 
from the California Household Travel Survey, On-Board Surveys, and Automated Passenger 
Counter data.

Not far behind, the route choice team completed a draft literature review and is evaluating 
various possible methodologies while they await some contracting hurdles to pass and data 
availability milestones to be reached by other parts of the team.

The goal is to have all task teams converge at a mid-October time point and be able to begin 
route choice model estimation.

