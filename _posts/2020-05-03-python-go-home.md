---
layout: post
title: "Python, let's go home. Quickly."
tags: gps track routing commute python pygohome
author: Miroslav Šedivý
date: 2020-05-03T12:00:00Z
abstract: Are you searching for the optimal route on your daily commute and can you use some Python? I am searching for you.
---

**tl;dr: If you are interested in optimizing your regular bicycle trips
(commute, shopping, …), start tracking them on your phone and save them as GPX
files. Then come back. I'm working on a Python project called `pygohome` that
does cool stuff with it.**

## Welcome to the city

- What are the places you visit regularly in your city from home? Work, all
  sorts of shops, family and friends, restaurants, clubs, doctors, parks,
  meetups?
- How do you move around? Walk, ride, drive?
- Which routes do you take? The “shortest” one from a route planner?
  Each time a randomly different one? Or do you have a few preferred
  “corridors” that take you between a few “hubs” on your way?

There are excellent online navigational apps for motorized vehicles drivers
and public transport users that take the real-time situation into account.
However, if you ask for the best route on bicycle or on foot, you usually get
wrong results. Why?

## It's called “individual traffic”

Because cycling and walking depend on very personal factors. In most cars,
most drivers are able (and have) to drive at the speed of the flow. That's why
online route planners are so good. On bicycle everything is individual:

- your normal speed
- your maximal speed
- your acceleration/braking (at intersection/lights)
- your ability/willingness to overtake slower vehicles
- your reaction to unexpected behaviour of other vehicles (or their pure
  existence on unexpected places)
- your choice of busy main roads or quiet lanes

There are also other factors that make each trip individual:

- traffic level (well, you're traffic too)
- weather, road condition
- lights (each trip may take shorter or longer)

## Find my way home

For bicycle rides between a few places in the city, I was interested in
finding _my_ best routes. Usually I like taking different routes in order to
see how the city changes, but sometimes I just need _the fastest_ route to get
somewhere as quickly as possible.

Of course I could just measure the time needed for each route, but since there
are so many factors, each time it would take more or less time. A city grid
may also offer too many possible routes (aka _Manhattan distance_, _snake
distance_ or _taxicab geometry_) and the best route may be a combination of
known segments.

## Am I feeling lucky or do I want to make sure?

What probability of success do I expect? If taking a longer road through
a park takes between 5 and 6 minutes (depends on weather/road condition only)
and a shorter road through the city takes between 4 and 8 minutes (because of
the lights and traffic, and again weather and road condition), then I _may_
get there faster through the city, but if I want to _make sure_ (or very
probable) I arrive in time, I'll take the longer park option.

Using Manhattan distance, there may be the best route that I never took as
a whole, but my tracks covered all its segments (roads between intersections)
often enough to get a good recommendation. In this case, a special attention
has to be paid to the intersections with lights and/or turn restrictions,
since they don't combine well. If there's no wait to turn right, but turning
left from the opposite direction takes minutes because of the red light, this
intersection can't be considered a simple node in the city grid.

## pygohome

So I'm tracking all my bicycle rides. From A to B, from B to A, from A to
C stopping in D, and from D to F. With over one hundred tracks in a few
months, I load them all and see a dense heatmap around and between my most
popular places, as well as a few tracks of one-time trips elsewhere.

I have added waypoints to all these “points of interest”, and, since the
current version does not support it correctly, added unnamed waypoints to all
intersections where my tracks crossed, split or joined.

Then I wrote some Python code that dissects all tracks into segments, added
special treatment of intersections where I spent more than a few seconds
(because of lights) and calculates a directed graph, that gives me the answer
to the question:

## “Which route from A to B is the fastest in 80% of the time?”

And it works. You will also be able to try it out. But first _you_ will need
a bunch of _your_ GPX tracks to play with. So just install some GPS tracking
app ([OsmAnd](https://osmand.net) works great) and take your daily trips. Ride
normally. You're doing it for the fun of statistics, not for Tour de France.

You'll make cool stuff with _pygohome_ on your computer later. No uploads of
your private information, just some tweaking of Python code.

Stay tuned.
