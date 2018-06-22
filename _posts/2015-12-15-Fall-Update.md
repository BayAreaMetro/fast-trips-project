---
title: "Fall 2015 Update"
author: Elizabeth
image: /img/posts/leaves.png
comments: true
layout: post
tags: [meta]

---

Over the past few months, we have made substantial progress on our standards, the network 
preparation, and the Fast-Trips software itself.  Paperwork has delayed some of our 
progress in the Travel Behavior task, but that is now behind us and we can push on.  Here 
is a brief summary of a few of the things we have been working on.

### Evolution of Standards
We have iterated some on our  standards, and updated all of our tools to use them.  

*[Network Standard](https://github.com/osplanning-data-standards/GTFS-PLUS)*

 * Biggest pain is still the fares, which have changed slightly as we have worked through 
the various fare types in each region and realized that there were too many exceptions 
to our simplifications.
 * The biggest changes to the standard are to decrease ambiguity.
 
*[Demand Standard](https://github.com/osplanning-data-standards/dyno-demand)*

 * Has remained more constant.

### Network Creation
We have substantively completed the code to do the network creation process for Fast-Trips 
on the fly from within SoundCast and SF-CHAMP.

<!--break-->

 * Includes schedule creation from headways [ using GTFS if it is available ].
 * Fares have been the most difficult component to “get right.” There are a multitude of 
fare rules by operator of multiple types [ zone, flat, station-to-station ], and multiple 
transfer policies.  These were all roughly approximated in our current system and so 
transferring them to the new data standard requires a lot of care and thought.
 * The [PSRC Version](https://github.com/psrc/fast-trips_network_builder) has undergone 
small-scale testing and will be scaling to entire network this week.  It utilizes the 
EMME API, so may be of limited use outside of EMME users.
 * The [SFCTA version](https://github.com/sfcta/NetworkWrangler/tree/fasttrips) is within their 
stand-alone NetworkWrangler and is slightly behind PSRC in maturity.

### Demand Validation
Our initial investigation into validating the demand has been met with the [ not 
unexpected ] issue that the OD data we have [ on-board surveys and CHTS ] is significantly 
higher [ when weighted ] than the ridership data we have at screenlines.  We are looking 
into this issue and hope to not get lost down this rabbit-hole if it isn’t going to benefit 
us too much in the long term since SF-CHAMP hits the screenline data fairly well.

### Fast-Trips Travel Model Integration
Joe developed a white paper summarizing the various issues and potential strategies for 
feeding LOS information coming out of Fast-Trips back up to the travel demand models. 

Joe, Elizabeth, and Lisa have been working to develop an approach that addresses these 
issues.   The process is challenging, because SF-CHAMP and SoundCast have very different 
approaches to mode choice.

### Software Released!
You can download and use Fast-Trips yourself!  We had Bhargava [ somebody who wasn’t 
involved in the coding ] work through the small test scenario and make sure he could 
download, compile, and use it.  

Instructions and code are on [GitHub](https://github.com/MetropolitanTransportationCommission/fast-trips/tree/develop ) 
and will be summarized in a forthcoming blog post.

