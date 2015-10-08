---
title: "Version Controlling a Data Standard"
author: Elizabeth
image: /img/posts/puzzle-pieces.jpg
comments: true
layout: post
tags: [demand, standard]
---


We have a number of data standards that we are creating as a part of this project (see my previous 
[post](http://fast-trips.mtc.ca.gov/2015/08/21/standard-deviation/) about the development of a few).  As 
we progress in the project, we realize that the standards will evolve and need to be updated.  As good little developers, 
we knew that we needed to start version controlling the data standard as well as the software 
that uses it.  You can see the finished result of a version-controlled standard [on GithHub](https://github.com/osplanning-data-standards/GTFS-PLUS), 
but if you are interested in the journey to get there, read-on!

### Starting 
We started with using different saved copies of the memo that described the standard:

    Network Standard v0.1.pdf
    Network Standard v0.2.pdf
    Network Standard v0.3.pdf
    
While sufficient, there are a number of obvious drawbacks with this approach.  Most notably, 
is that in order to see the differences between versions you have to compare each entire PDF 
document.  Even if we were to include a changelog, it would require somebody to cycle through 
multiple documents if they wanted to understand differences between multiple versions.  

### What are others doing?
I did some online research to find out how other data standards are controlled and found 
a variety of examples, which are described below.

##### Google and GTFS

Google does keep a [record of the changes](https://developers.google.com/transit/gtfs/changes) 
they have made to the GTFS specification but does not assign each change a unique version number 
or track it in any other way than a change-log.  While the specification is very openly "not 
set in stone", one of the guiding principles for changes is that they should be backward compatible.  

<!--break-->

Google does version control its [GTFS Feed Validator](https://github.com/google/transitfeed/wiki/FeedValidator). 
However, the feed validator version does not have a relationship to the GTFS version - e.g., 
you cannot ask it to validate a feed per the June 1st 2014 version of GTFS.

In short, I didn't find a lot to be learned from the GTFS example and decided to jump to 
some examples where the version really did matter: i.e. the standards underlying the foundation 
of the world-wide web.

##### W3C

[W3C](www.w3.org), the organization that standardizes the bulk of the soft internet uses *numbered 
release versions* (e.g., HTML [5.0](http://www.w3.org/TR/html5/), [5.1](http://www.w3.org/TR/html51/), 
etc) and then *dates* for small changes made between such as [HTML 5.1 from September 29th 
2015](http://www.w3.org/TR/2015/WD-html51-20150929/).  

While this provides traceability between different versions, there is no good guide between 
them or way to do "diffs" from one version to another.  

##### IESG

The [Internet Engineering Steering Group](http://www.ietf/iesg) manages the internet's engineering
standards process, which dates back to the days of DARPAnet.  The process for developing 
internet standards is of course documented by...its own standard: [ RFC2026 ](https://www.ietf.org/rfc/rfc2026.txt). 

Standards are developed through the "Request for Comment" (better known as RFC) process.  All 
RFCs are maintained on [www.rfc-editor.org](www.rfc-editor.org) and are assigned a serial number. 
 Not all RFCs are standards, but those that are go through an evolution from proposed -> draft 
-> standard.  Standards also each have serial numbers (e.g. [STD 77](http://www.rfc-editor.org/info/std77)) 
and new RFCs can obsolete or update existing standards.  So the STANDARD has a number and the RFC number
is changed to reflect changes to that standard.

If you want to see if anything changes, RFC-editor maintains a [rolling list of status-changes](https://www.rfc-editor.org/status_changes.php).
The problem is that if you are using a canonical reference to the RFC, you might not ever know 
that anything has changed or moved forward.


A few other notables:

 *  There is a very popular RFC "style guide" ( [RFC 7322](https://www.rfc-editor.org/rfc/rfc7322.txt) ) 
which is used for defining many standards across many disciplines.
 *  There is another type of RFC called "best current practice" (BCP), which are not standards, 
but define the coalescence around a certain way of doing things in practice.

After reading all of this, I still wondered why none of these efforts used version control 
for controlling versions of standards. It seems like a natural fit, so I stumbled around GitHub 
to seek some examples out.

##### Version controlling versions of standards

The [Open Knowledge Foundation](https://okfn.org) has a project to specify certain data standards and they use 
github extensively to manage the [jekyll](http://jekyllrb.com/) webpages that manage the standard.  For example, 
each Spec page uses a webpage [layout template](https://github.com/dataprotocols/dataprotocols/blob/gh-pages/_layouts/spec.html) 
and then the information in each standard is represented by an RFC-style description that 
is in a [version-controlled markdown file](https://github.com/dataprotocols/dataprotocols/blob/gh-pages/data-packages/index.md).  
The markdown file has a change-log and meta-data such as `version` in the 
[YAML front matter](http://jekyllrb.com/docs/frontmatter/).  [Markdown](https://help.github.com/articles/markdown-basics/) 
is just ASCII and it is thus easy to see the changes between versions as a [GitHub Diff view](https://github.com/dataprotocols/dataprotocols/commit/e1500a06d971c311b4ad743a0604624d05ddaba3#diff-e7271c46c4299b50c58fbc0b7da3f495).

This approach is nice for several reasons:

 *  It forces any change to be noticed.  Because you are using version control software, you 
 can't 'cheat' and slip in something else to a previous version
 *  It is ASCII-based, which allows for easy viewing of differences across versions of the standard
 *  It is human-readable and allows for more formatting than the pure ASCII view of RFCs
 *  It has a seamless translation between the version-controlled ASCII and the front-end webpage which reduces possible error or misalignment
 *  You can use all the GitHub tools which will allow you to subscribe to a repository which will 
 let you keep abreast of any changes.
 
 While this seems like a good solution, I still have a few questions/issues:
 
 *  Do you create a new GitHub repository for each standard so they can move forward separately 
 or lump them all into one?  
 *  Do you really need to create a Jekyll site for this or can it just be a standalone markdown file?


### Our evolving methods...

Based on the examples we researched above, we decided to create separate GitHub repositories 
for each data standard so that they could easily be separately referenced and versioned.  For example, our [network standard](https://github.com/osplanning-data-standards/GTFS-PLUS) 
repository stores a reference to our network standard and provides several ways 
for the public to respond to the standard and request changes: [pull requests](https://github.com/osplanning-data-standards/GTFS-PLUS/pulls) 
and [issues](https://github.com/osplanning-data-standards/GTFS-PLUS/issues).

So that each standard would not get bogged down within the many repositories in an existing GitHub 
organization, we decided to put them in a separate organization: [OSPlanning-Data-Standards](https://github.com/osplanning-data-standards). 

### Versioning

So now that I have some ideas of how to control the versions of the standard, what do I name them?  If I were 
to control my data standard like I control my documents it would be something like:

 *  DRAFT
 *  FINAL
 *  FINAL2
 *  FINAL2tuesday
 *  FINALFINAL
 *  FINALFINALwFIXEDTYPO
 *  FINALFINALwFIXEDTYPO-REALLYFINAL
 
Fortunately, the software world has come up with something better called **semantic versioning**, 
which is well documented at [semver.org](http://semver.org) (which itself is version controlled 
on GitHub).  There are a lot of good details on the site, but the core principal is that versions 
should be numbered as:

    MAJOR.MINOR.PATCH (e.g., v1.0.2)
    
    s.t.
    
    MAJOR =  0 if in development mode before a major release
             Increment for each version that you make incompatible API changes
    MINOR =  0 for each new MAJOR release
             1 for first version (e.g., v0.1.0)
             Increment when you add backward-compatible functionality
    PATCH =  0 for each new MAJOR or MINOR release
             Increment when you make backward-compatible bug fixes
             
We have already made a variety of changes to the standard we first started with.  

 *  v0.1.0 was our first go at it
 *  v0.2.0 moved up a minor point because it added some 'features' related to fares
 *  v0.2.1 moved up a patch point because it addressed a minor 'issue' in the date time format used (HHMMSS vs HH:MM:SS).

### More to come...

We still need to see if this will work out in practice or be too cumbersome.  Up until this 
point, we have not explicitly sought the opinion of others and will be curious if we get any 
buy in or feedback on our proposals (we hope so!)  
