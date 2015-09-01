---
title: "Speed Demons"
author: Lisa
comments: true
layout: post
tags: [software]

---

In my previous post, I unveiled the size of our "performance problem" for Fast-Trips
and discussed various ways that we had and were planning on attacking it.  I had already 
made some speed ups by using the multi-processing for pathfinding (while making sure the 
random number seeds that were used were unaffected), but the big question mark was if 
a c++ extension would make a big-enough dent into our run time to be tolerable enough 
to run in at least a "*development mode*". 

I [spent the past two weeks](https://github.com/MetropolitanTransportationCommission/fast-trips/commits/c_extension) 
creating, testing, and documenting the c++ extension and am happy to say that when combined 
with the multi-processing across 64 cores (reasonable for our case), the projected runtime
will be **four hours** (as opposed to four weeks/months).  The c extension alone represented
 a 40x processing speedup.
 
Phew!
 
Next up:

 * explore allowing non-additive costs in path search
 * improve usability and parameterizing the c-extension
 * allow modal biases / selectivity 
 
 



