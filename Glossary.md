# Glossary #

**Benchmark.** Also _benchmark class_. A user-written class which extends `Benchmark`. Example:

```
public class ClockBenchmark extends Benchmark {
  public void timeNanoTime(int reps) {
    for (int i = 0; i < reps; i++) {
      System.nanoTime();
    }
  }
}
```

**Benchmark Method.** A single method in a benchmark class, whose purpose is to execute the code you wish to measure for the given number of reps. For the microbenchmark (and allocation) instruments, this method's name must begin with `time` and it must accept an `int` or `long` parameter for the rep count.

**Caliper.** This framework, or specifically the `caliper` executable command that runs a single _benchmark_.

**Environment.** An automatically-recorded description of the hardware, operating system, and JRE installation on which a particular measurement was taken. This does not include JVM arguments, benchmark parameters or other settings the user can _directly_ control; environment attributes are specified only _indirectly_, by telling Caliper what hostname to connect to and the pathname of the JRE to invoke.

**Instrument.** (Definition.) Examples: microbenchmark, macrobenchmark, allocation, footprint, arbitrary measurement.

**Measurement.** A fact (usually a quantity) measured empirically by Caliper, corresponding to a specific _scenario_. Each _run_ of a _benchmark_ will record one or more measurements per _scenario_ derived. Usually a measurement is of elapsed time, but it is possible to specify alternate _instruments_ to gather measurements of other types.

**Parameter.** A value that is injected into a field of a _benchmark_ class that has been marked with the `@Param` annotation. Multiple values can be configured for each parameter, either by defaults embedded in the class itself or at the command line, and the framework will test each value separately.

**Reps.** the number of times that the benchmark method will loop for a given _measurement._ Users typically don't have to control this directly; caliper chooses these values (hopefully) sensibly.

**Scenario.** a fully-specified "instance" of a _benchmark_, having a specific value for each _axis_. A scenario is executable. For example, a run of a benchmark that has one parameter that can take on three values, that is requested to run on both the server and client VMs, will yield six distinct scenarios, all of which will be measured. In a perfect world, a given scenario would only need to be measured once, because its value would never change.

**Run.** a collection of distinct scenarios executed in batch on a single host environment.

**Trial.** The collection of a single _measurement_, for a specific _scenario_, which involves spawning a new JVM, warming up, and a number of invocations of your _benchmark method._ Currently, by default, Caliper conducts only one trial per _scenario_, but it is a good idea to increase this using `--trials n` on the command line.

**Axis.** any factor affecting your benchmark that can take on multiple potential values. A _parameter_ is one type of axis -- one that is user-defined. Other axes include those detected in the _environment_, which _benchmark method_ is running, the version of your code, JVM arguments, etc.