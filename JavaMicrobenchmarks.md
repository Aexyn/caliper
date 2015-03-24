# What is a microbenchmark? #

A microbenchmark attempts to measure the performance of a "small" bit of code. These tests are typically in the sub-millisecond range. The code being tested usually performs no I/O, or else is a test of some single, specific I/O task.

Microbenchmarking is very different from _profiling_! When profiling, you work with an entire application, either in production or in an environment very _painstakingly_ contrived to resemble production. Because of this, you get performance data that is, for lack of a better term, _real_.  When you microbenchmark, you get a result that is essentially _fictional_, and you must be very careful about what conclusions you draw from it.

## What? Why would a microbenchmark result be fictional? ##

The goal you probably have in mind when you seek to write a Java microbenchmark is, "what are the _intrinsic_ performance properties of this snippet of Java code?"  Unfortunately, this is an unanswerable question. Java code itself does not _have_ intrinsic performance properties, any more than a cocktail-napkin sketch of an airplane has intrinsic aerodynamic properties.

In the olden days, studying the performance of code was like the study of physics or chemistry: you could perform controlled experiments and get predictable results. Periodically our model needed to evolve, incorporating ideas like relativity and quantum physics, but as it evolved it got better at predicting and explaining the world.

But today, the entire stack of all the various bits of genius that sit between your code and the bare metal more closely resembles a _biological_ system. Asking whether method foo() or method bar() will run faster can be like asking whether patient Fred or patient Brad will have a heart attack tomorrow. It might be possible to know this if we were omniscient, but in reality the sheer number of variables involved -- which we often can't even observe, much less control -- overwhelms our predictive capability.

Examples of microbenchmark fallibility:

  * The JIT compiler will likely compile your bytecode differently from how it does (if it does) in real life
  * The results you see are valid only for the particular hardware, operating system and JRE it was run on; one small change to any of these, and things can be drastically different
  * Your code might not suffer nearly as many cache misses when it's running inside a microbenchmark as it does in real life
  * Differing circumstances can affect the dozens of layers of abstraction that lie below even the _machine code_, in unpredictable and uncontrollable ways
  * It is next to impossible to simulate realistic patterns of multithreaded activity in a microbenchmark
  * The inputs you choose might just not be representative of what you get in real life
  * and the list goes on and on.

## Why would I ever write a microbenchmark then? ##

**Most of the time, you shouldn't!** Instead, slavishly follow a principle of simple, clear coding that avoids clever optimizations. This is the type of code that JITs of the present and future are most likely to know how to optimize themselves. And that's a job which truly should be theirs, not yours.

It is still a good idea to seek to minimize the overall "amount of work" that your code needs to perform.  If you can break a loop early, or do something in O(log n) instead of O(n) (for sufficiently large n), you should probably do so!  What you should generally _not_ do is obsess over whether to loop backwards or forwards, cache a field value in a local variable, and other such tricks.

## Ok, but... I think I really do want to write a microbenchmark. ##

The most common reason to write microbenchmarks is that you are a developer of a _library or framework_ which will be used in contexts you cannot predict.  Real-world profiling tends to not be an option for you.

What you need is _some plausible excuse_ for deciding

  * Should I go with Reasonable Implemenation A, or Reasonable Implementation B?
  * Should I advise users with Use Case X to use Library A, or Library B?
  * Is this confusing "optimization" really worth the simplicity it sacrifices?
  * Can I honestly claim that API Z even has a reason to exist, when API Y does the same thing?
  * How does upgrading to the latest JRE affect performance of my library?

A microbenchmark usually can't provide a definitive, final answer to these questions. What it can do, if carefully developed, is offer you "as good a reason as any" for your choice.

## How should I do it? ##

Learn to use Caliper from the tutorial (link) and other examples (link). Then see JavaMicrobenchmarkReviewCriteria.