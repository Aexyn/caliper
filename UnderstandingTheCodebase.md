# The caliper command-line framework #

This code lives in [caliper/src/main/java](http://code.google.com/p/caliper/source/browse/#git%2Fcaliper%2Fsrc%2Fmain%2Fjava%2Fcom%2Fgoogle%2Fcaliper)

Currently, there are two mostly-separate codebases sitting in there!  The code that's directly in `com.google.caliper` is the current "legacy" codebase that's about to be thrown out.  The new codebase exists entirely in the various _subpackages_ of `com.google.caliper`.

## `com.google.caliper.api` ##

These few classes are the only things that most users' benchmark classes will interact with.  After the old codebase is gone, they'll move up a level to sit in `com.google.caliper`.

## `com.google.caliper.model` ##

These are dead-simple, easily-mappable-to-JSON classes that hold the result data that caliper produces.  After a run, everything that caliper records (what was run, with what parameters, in what environment and vm, all the measurements that were gathered, etc.) is shoved into these classes and then converted to JSON for upload to the webapp.

## `com.google.caliper.runner` ##

This code makes up the Caliper "parent process" which is what you invoke directly from the command line when you run your benchmark. It does a lot of "coordination", but doesn't perform any actual measurements itself.

Some important classes:

### `CaliperRun` ###

This is the meat of the runner. It could stand to be decomposed a bit.

### `BenchmarkClass` ###

This class is the keeper of the knowledge about the structure of the user's benchmark class and how Caliper interacts with that.

### `ParsedOptions` ###

This is where the command line gets parsed.

### `MicrobenchmarkInstrument` ###

This implementation of `Instrument` handles microbenchmark runtime measurements, as opposed to what the other instruments we'll add (soon?) will do, like measure memory allocation or consumption, or generate a profiling report, etc.

## `com.google.caliper.util` ##

Random stuff we need that isn't very caliper-specific.

## `com.google.caliper.worker` ##

This is for the code that gets invoked in a subprocess by caliper. Ideally we should keep the dependencies as light as possible for this stuff.

Some important classes:

### `WorkerMain` ###

Contains the main() method the parent process invokes.

### `WorkerRequest` and `WorkerResponse` ###

How the parent and worker processes talk to each other.

### `MicrobenchmarkWorker` ###

This is what actually runs and times your code!  (Wondering when we'd ever get to that?)

# The caliper web application #

This code lives in [svn/cloud/src](http://code.google.com/p/caliper/source/browse/#svn%2Fcloud%2Fsrc%2Fcom%2Fgoogle%2Fcaliper%2Fcloud).

Jesse would love to tell you more here.... :-)