---
title: "Two Metro-Area Transit Networks – Take One"
author: [Stefan, Drew]
image: /img/posts/networks.png
comments: true
layout: post
tags: [networks, software]
---

Are you enjoying running [Fast-Trips](https://github.com/MetropolitanTransportationCommission/fast-trips) 
on the small test network but ready for a “big time” network?  Today is your lucky day.  

The general approach to creating networks is to take the travel demand model networks that 
each agency already produces and add information to them to create a schedule-based network 
as required by our GTFS-PLUS network specification 
[ and [discussed in this blog post](http://fast-trips.mtc.ca.gov/2015/08/21/standard-deviation/) ].  

## Network Conversion Scripts

The team has created two network conversion scripts: one that converts PSRC’s SoundCast’s 
EMME networks into [GTFS-PLUS](https://github.com/osplanning-data-standards/GTFS-PLUS) 
networks that [Fast-Trips](https://github.com/MetropolitanTransportationCommission/fast-trips) 
can read and the other that uses SFCTA’s “Network Wrangler” to convert 
[SF-CHAMP](http:///www.sfcta.org/modeling) networks to 
[GTFS-PLUS](https://github.com/osplanning-data-standards/GTFS-PLUS).  While the PSRC version 
requires an EMME license, SFCTA’s Network Wrangler is based in Python and can therefore be 
run by anyone.  

### SoundCast Fast-Trips Network Builder

The [SoundCast Fast-Trips Network Builder](https://github.com/psrc/fast-trips_network_builder) 
converts SoundCast’s [Emme](https://www.inrosoftware.com/en/products/emme/) networks into 
GTFS-PLUS networks by completing a bunch of data transformations and simulating a transit 
schedule either based on average headways for a given time period [ good for future year 
data ] or by grabbing the GTFS schedule [ good for base year data where the schedule is known ].

### Network Wrangler

[Network Wrangler](https://github.com/sfcta/NetworkWrangler/tree/fasttrips) is the codebase 
that SFCTA uses to build their transit and highway networks.  It has class objects for things 
like [transit lines](https://github.com/sfcta/NetworkWrangler/blob/fasttrips/Wrangler/TransitLine.py), 
[nodes](https://github.com/sfcta/NetworkWrangler/blob/fasttrips/Wrangler/Node.py) and 
[transit networks](https://github.com/sfcta/NetworkWrangler/blob/fasttrips/Wrangler/TransitNetwork.py).
When possible, these classes were just extended to be able to write out 
[GTFS-PLUS](https://github.com/osplanning-data-standards/GTFS-PLUS) files. However, quite 
a bit of logic had to be built in in order to incorporate things such as complex fare 
structures.

The script can be run as follows:

`python convert_cube_to_fasttrips.py network_specification.py`

There is still a bit of work to be sorted out to come up with the version of the network 
that we will be happy with, but we can still get some good mileage out of this version. 
In particular, there are additional data fields that would be nice to populate and the base 
year schedule should be synched with existing GTFS data rather than randomized across a 
log-normal schedule.

## Network File

Want to take Fast-Trips for a spin right now?  Feel free to download 
[Take-1 of the San Francisco Bay Area Network](https://mtcdrive.box.com/s/g1sny1wqg3bp7w54l5f1p1oom9rj6jg8) 
and use it in combination with the first draft of the 
[San Francisco Bay Area Demand](https://mtcdrive.box.com/s/wzthprl227f2l5aim5iohyal0guh8wra)
