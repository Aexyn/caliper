# Caliper command line options #

## -h, --help ##

Prints usage summary.

## -n, --dry-run ##

Instead of measuring, execute a single rep for each scenario scenario in-process. This is primarily useful for making sure that benchmarks execute cleanly (though not necessarily correctly).  It can be a good idea to use dry run invocations of your benchmarks

## -b, --benchmark ##

Comma-separated list of benchmark methods to run; 'foo' is an alias for 'timeFoo' (default: all found in class).

## -m, --vm ##

Comma-separated list of VMs to test on; possible values are configured in Caliper's configuration file(default: whichever VM caliper itself is running in, only).  For example, if `~/.caliper/config.properties` contains:
```
  vm.jdk6.home=/path/to/jdk6
  vm.jdk7.home=/path/to/jdk6
```
Then `jdk6` and `jdk7` are valid values for this flag.

## -i, --instrument ##

Measuring instrument to use; possible values are configured in Caliper's configuration file (default: 'allocation,micro,footprint').  Use `--print-config` to see the list of configured instruments.

## -t, --trials ##

The number of independent measurements to take per benchmark scenario; a positive integer (default: 1).  JIT is often non-deterministic.  Performance-related decisions should almost always be based on data from multiple trials to account for that fact.

## -l, --time-limit ##

The maximum length of time allowed for a single trial; use 0 to allow  trials to run indefinitely. (default: 30s).  This is primarily used as a safeguard against runaway instruments and workers that don't terminate.  It is likely that instruments such as the macrobenchmark (`macro`) instrument may require a higher time limit for normal operation.

## -r, --run-name ##

A user-friendly string used to identify the run.  It is _highly recommended_ that this be provided as it makes browsing results a much more user-friendly experience.

## -v, --verbose ##

in addition to normal console output, display a raw feed of very detailed information from the worker (GC, compilation events, etc.).  Runner output via loggers can also be controlled via `$HOME/.caliper/logging.properties`.

## -p, --print-config ##

Print the effective configuration that will be used by Caliper.  This is the composition of values from Caliper's global configuration, the user's configuration in `$HOME/.caliper/config.properties` and values specified on the command line using the `-C` flag.

## -d, --delimiter ##

Separator used in options that take multiple values (default: ',')

## -c, --config ##

The location of Caliper's configuration file (default: $HOME/.caliper/config.properties).  Note that if the `--directory` flag is set, but this flag is not, Caliper will look for a `config.properties` file in that directory.

## --directory ##

The location of Caliper's configuration and data directory (default: $HOME/.caliper)

## -D ##

-Dparam=val1,val2,... specifies the values to inject into the 'param' field of the benchmark class; if multiple values or parameters are specified in this way, caliper will try all possible combinations.

## -C ##
-CconfigProperty=value specifies a value for any property that could otherwise be specified in `$HOME/.caliper/config.properties`. Properties specified on the command line will override those specified in the file.