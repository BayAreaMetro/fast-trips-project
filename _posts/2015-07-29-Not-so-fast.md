---
title: "Not So Fast? Not So Fast..."
author: Lisa
image: /img/posts/china-hsr.jpg
comments: true
layout: post
tags: [software]
images:
   image1:
      image: /img/posts/software-time.png
      caption: "Comparison of Python and C++ Run Times"
      source: "MTC, PSRC, & SFCTA"
   image2:
      image: /img/posts/snake-viz-initial.png
      caption: "Diagnosis of Run-Time Source"
      source: "MTC, PSRC, & SFCTA"
   image3:
      image: /img/posts/cookie-c.jpg
      caption: "Need more C"
      source: "somegeekintn.com"
---

### The Good!
Translating Fast-Trips from C++ to Python turned out to be a fairly straight forward task.
I completed the straight translation within a few weeks, fixed a few bugs in the C++ version, 
and verified that the Python results were producing the same output as the fixed C++ version.

Voila, a working version of Fast-Trips in Python!

### The Bad...
We had always expected Python to not be as fast as C++, but did not anticipate just how
many orders of magnitude slower it would be.  I have been using a test batch of 121,000
riders in the San Francisco Muni network to test Fast-Trips, which I used to calculate 
the run times in the image below.

{% include image.html image=page.images.image1 %}

Out of the box, Python was over 20 times slower.  However, in order to satisfy our target
performance of six hours (for the entire Bay Area...which has several million transit trips
per day) we would need to get to a point where Fast-Trips was running much faster than the
 C++ version.
 
**scary numbers:**

 - Performance Target for Bay Area: 6 hours  
 - Initial Python Fast-Trips Performance (estimated): 1,666 hours  
 - Needed speedup: 300X  

Undaunted, we plowed ahead with the search for 300X worth of performance improvements.

<!--break-->

### The Ugly.

Where to start?  We decided to profile our nemesis in order to target its weaknesses.
Luckily, there is a really amazing tool to do this developed by [Matt Davis](https://github.com/jiffyclub) called
[SnakeViz](http://jiffyclub.github.io/snakeviz). SnakeViz makes it super easy to figure
out what part of your code is eating up all the time.  So where was the extra fat in Fast-Trips?
It turns out that it was hard to pinpoint where all the time was being taken up because 
the biggest source of time is a "catch-all" function `find_trip_based_hyperpath`. (Note to
 self, next time you write code make your functions more concise.)

{% include image.html image=page.images.image2 %}

### The UltraSlimFast Plan
So what to do?  We initiated a list of "quick fixes" and "exploratory strategies".

Quick Fixes:

 - **Pandas Fu** - Switch what we can to Pandas.

Exploratory Strategies:

 - **C is for....** [Cython](http://cython.org/), which is supposed to magically translate Python to C code. 
 And C is also for...well...C.
 - **Go forth and multiply** the number of processes that are happening at once. We have 
 a bunch of shortest path algorithms.  Shouldn't we be able to send those to a 
 zillion processors?  We thought so.
 
#### Pandas Fu

The [Pandas library](http://pandas.pydata.org/) has created a nice python wrapper a 
bunch of fast c numeric operations.

**What is involved?**

For the simulation, we converted the passenger list to a Pandas data frame.

**Did it work?**

Doing the [simulation in Pandas](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/08ba2ce270646b503ba855d93498149eb6ccbdb3)
 resulted in a 2X speedup.  Great, that was easy - only 150X to go!

#### C is for Cython

[Cython](http://cython.org/) makes it easy to compile easy-to-read Python code into C - 
and the speed advantages that come along with it.

**What is involved?**

 - Renamed files from `myprogram.py` to `myprogram.pyx`
 - Added `#cython profile=True` to the beginning of `.pxy` files
 - Added Cython to setup.py:
 
		import setuptools
		from distutils.core import setup
		from Cython.Build import cythonize
		
		setup(
		name = 'fasttrips',
		ext\_modules = cythonize("fasttrips/*.pyx"),
		)
- Let c know your variables types (instead of relying on Python dynamic typing)

		cdef:
			int start_taz_id, dir_factor
			int stop_id, trip_id, seq
			int label_iterations
			object access_link

**Did it work?**

[Early progress](https://github.com/MetropolitanTransportationCommission/fast-trips/commits/assign_cython)
 gave us a 2-4X speed improvement, without touching the mega-jumbo method:
`find_trip_based_hyperpath`.
However, the extent to which we could get more out of Cython depends on how much is math, 
versus how much are things like dictionary lookups.  Looking through our code, it turns
out that most of our time is spent on the latter, which makes Cython only so helpful. We 
would have to climb up another c-tree to get the performance improvements we really needed.


#### Go forth and multiply

The pathfinding process is fairly distributable and was [implemented using the Python Multiprocessing
library](https://github.com/MetropolitanTransportationCommission/fast-trips/pull/3/files).

There were two main issues to consider:
1. make sure the random number seeds are synced such that you will get same answer if you 
run it with varying number of processors
2. the time it takes to open the network for each worker.

The seed setting was resolved by [using the passenger id as the seed](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/424a9521eaf875b6fa840170139381cd2700bdbb).

After testing both passing the open network to each worker or having each worker re-read
 the network, we found it was quicker to [just have each worker re-read the network](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/8b1652ff9b216a0ae26bad4f10c393fb265c6247).

#### C is also for C++

{% include image.html image=page.images.image3 %}

We haven't tossed in the towel for having a usable, high-performance transit passenger 
simulator in Python - we just think we need some help from C++ behind the scenes to turbo 
charge it.  I am [currently in the process](https://github.com/MetropolitanTransportationCommission/fast-trips/commits/c_extension)
 of moving the slow stuff from `find_trip_based_hyperpath` to a very generic bunch of C++. 
 The goal is to make the C++ flexible and generic enough that no modeler in a given year would 
want or need to go into the C++ and recompile it; rather, they would be able to do everything 
they wanted from within the Python side.
 
In order to make it easier for the C++ to interact with Python, I wrapped up all the little
pieces of information floating around in tiny objects [into a single Pandas Dataframe](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/818be2f5e58c0288894676032dede76982d97c3c)
 so that we could minimize the number of exchanges between the two. 

**Did it work?**

We are still in the process of writing and wrapping the C++, but will post back with results 
when we have them.

#### Other Speedups

 - [Switched from](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/5c267e0d89c86f1dfd485d60413cdba732ab6aa8)
  a priority queue to a heapq which is not threadsafe, but is much faster.
 - Get rid of slow but pretty date-time operations and [replace with speedy but ugly integer math](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/ef712ae455b43a1f3a6d91120f84d2677ef401a2)
 
 
### A few other fixes along the way

- [Merged stochastic and deterministic assignment](https://github.com/MetropolitanTransportationCommission/fast-trips/commit/4b728aa1c70514d937003037f968a959c302ee8b)
, since deterministic is really just a special case of stochastic.


### What's Next?

1. First we need to re-profile the code using SnakeViz to see what we have improved and what we have made worse
2. Critically examine the speed/legibility/usability tradeoff 
3. Test test test
4. Add new features such as Park and Rides, etc.
5. Make it usable to front-facing users


