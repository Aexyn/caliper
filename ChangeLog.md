# Differences Between Caliper `0.5` and `1.0` #

  * `0.5` benchmarks extended `SimpleBenchmark` while `1.0` benchmarks extend `Benchmark`
  * `0.5` only measured runtime by default.  `1.0` measures runtime and allocation.
  * Runtime results from `0.5` were subject to corruptions from factors like GC and JIT occurring mid-timing.  `1.0` now detects and reports such events.
  * `0.5` produced incomplete and possibly misleading console output.  `1.0` does not.
  * `0.5` required an API key to upload results to [the webapp](http://microbenchmarks.appspot.com/).   Caliper `1.0` uploads every run automatically, but an API key is still required to associate a run with a particular user.
  * `1.0` stores the JSON result of every run in `~/.caliper/results/`.  `0.5` required an explicit flag.
  * `0.5` was configured using `~/.caliperrc` while `1.0` uses `~/.caliper/config.properties`.
  * [Many bug fixes](https://code.google.com/p/caliper/issues/list?can=1&q=Milestone%3D1.0+status%3AFixed+&colspec=ID+Type+Status+Priority+Milestone+Owner+Summary&cells=tiles)