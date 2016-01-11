---
title: "SF Transit Demand - Take One"
author: Bhargava
image: /img/posts/demand.png
comments: true
layout: post
tags: [demand, software]
---

We have transit demand – a version of it, anyway.  I started with a script that 
[Lisa Zorn](https://github.com/lmz) developed back in 2012 when she and 
[Alireza Khani](https://github.com/akhani) worked on the paper 
[ *Integration of the FAST-TrIPs Person-Based Dynamic Transit Assignment Model, the 
SF-CHAMP Regional Activity-Based Travel Demand Model, and San Francisco's Citywide Dynamic 
Traffic Assignment Model*](http://amonline.trb.org/13-4601-1.2527510?qr=1).  The script 
currently does two things: reformats the data, and assigns disaggregated preferred departure 
and arrival times. In the future, it may combine data from other sources and perform minimal 
variable synthesis. 

### Time blocks to time of day
In order to distribute the trips to discrete times from the five aggregate time periods 
that [SF-CHAMP](http://www.sfcta.org/modeling) uses [ AM Peak, Midday, PM Peak, Evening, 
and Early AM ], the script uses cumulative density functions for preferred arrival and 
departure times derived from observed [SFMTA](http://www.sfmta.com) Automated Passenger 
Counter (APC) boardings and alightings.

### Data reformatting
The demand data is then reformatted to the 
[Dyno-Demand](https://github.com/osplanning-data-standards/dyno-demand) format to be able 
to be read by [Fast-Trips](https://github.com/MetropolitanTransportationCommission/fast-trips). 
The Dyno-demand format has one mandatory file 
([`trip_list.txt`](https://github.com/osplanning-data-standards/dyno-demand/blob/master/files/trip_list.md)) 
and two optional files [ 
[`household.txt`](https://github.com/osplanning-data-standards/dyno-demand/blob/master/files/household.md) 
and [`person.txt`](https://github.com/osplanning-data-standards/dyno-demand/blob/master/files/person.md) ].  

One other item of note is that although [SF-CHAMP](http://www.sfcta.org/modeling) currently 
models a variety of sub-modes in its trip mode choice model [ e.g., ferry, local-bus, 
express-bus, commuter-rail, etc ], the team decided that it would be better to let 
[Fast-Trips](https://github.com/MetropolitanTransportationCommission/fast-trips) make the 
sub-mode selection in the route choice model.  Therefore, the transit sub-modes from SF-CHAMP 
are collapsed in this script to Walk-to-Transit and Drive-to-Transit.

### Transit Travel Demand - Take One
If you are interested in reviewing our “first take” of the San Francisco disaggregate 
transit demand, you can 
[download it here](https://mtcdrive.box.com/s/wzthprl227f2l5aim5iohyal0guh8wra).  Please 
note that this is by no means a finished product and still needs a fair amount of work, 
as documented in the various GitHub 
[Issues](https://github.com/sfcta/fast-trips_demand_converter/issues).  That said, if you 
want some demand that is bigger than the test network, here is something you can use in 
combination with 
[Take-1 of the San Francisco Bay Area Network](https://mtcdrive.box.com/s/g1sny1wqg3bp7w54l5f1p1oom9rj6jg8).