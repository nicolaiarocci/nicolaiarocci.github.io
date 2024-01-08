---
date: 2021-04-05T07:05:25+01:00
title: "School assignments that count: simulating the COVID outbreak with the C language"
share: false
tags: ["giulia", "programming", "teaching"]
---
Giulia got an exciting assignment from her teacher: 

> Write a C program that simulates (a simplified version of) COVID outbreak
> spreading across a population of 200 people. When a healthy person comes into
> contact with a sick person, the healthy person becomes ill, too. After some
> time, a sick person will recover. A recovered person cannot infect a healthy
> person nor become sick again after coming in contact with a sick person.

In more prosaic terms: the world comprises a 30*50 cell grid. Of these, 200
cells are randomly selected to be alive. Throughout the simulation, each of
these cells can be in one of the following three states: healthy, sick, or
recovered. If a cell is ill, at the next cycle, all neighbouring cells will
also be diseased. A cell stays sick for 14 cycles. At cycle 15, it is healed.
The simulation ends when all 200 cells are either recovered or healthy.

Giulia's implementation was fine, but a couple of subtle bugs prevented it from
succeeding, and that's how I got involved. In general, she doesn't ask for
help, nor do I ask her about her progress. If she reaches out to me, it's only
for serious trouble, and when that happens, I enjoy working with her. Besides,
while I do a lot C# these days, I don't do C since aeons ago, so it's great to
get back to it every once in a while.

![first cyckle](/images/covid-sim-prima-esecuzione.png)
Above, the healthy population inhabiting its 1500-cells world, right before the outbreak.

![intermediate](/images/covid-sim-esecuzione-intermedia.png)
Halfway through the simulation, 86 cells are healthy, 46 are sick, and 68 are
healed.

![final cycle](/images/covid-sim-ultima-esecuzione.png)
End of the simulation. It doesn't matter how many times you run it; the number
of people who were never infected is stunningly low by the end. Moreover,
a simulation like this one, albeit simplified, reveals how dramatically an epidemic
can spread if not contained with social distancing.

I was pleasantly surprised by this assignment. Here we have a teacher who
doesn't constraint herself to the standard, well-established routine. Instead,
she keeps her students engaged and challenges them. At the same time, she takes
the chance to educate them on the current sanitary emergency. Giulia tells me
that her teacher was inspired by a March 2020 Washington Post article: *[Why
outbreaks like coronavirus spread exponentially, and how to "flatten the
curve."][1]* That's excellent work. It includes several animated simulations,
Giulia's assignment being one of them.


*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://www.washingtonpost.com/graphics/2020/world/corona-simulator/
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
