**The Caliper 1.0 branch has not been tested to work on Android.  It is likely broken.  Consider 0.5 for Android benchmarks.**

## Introduction ##

The easiest way to run Caliper benchmarks on Android is to use a handy little tool called [Vogar](http://code.google.com/p/vogar/).

If you have vogar, you can use it run a Caliper benchmark like so:

<pre>
$ vogar --benchmark $dalvik/benchmarks/regression/StringIsEmptyBenchmark.java<br>
Actions: 1<br>
Action benchmarks.regression.StringIsEmptyBenchmark<br>
0% Scenario{vm=dalvikvm, benchmark=EqualsEmpty} 46.25ns; σ=4.22ns @ 10 trials<br>
25% Scenario{vm=dalvikvm, benchmark=IsEmpty_Empty} 14.07ns; σ=0.02ns @ 3 trials<br>
50% Scenario{vm=dalvikvm, benchmark=IsEmpty_NonEmpty} 19.10ns; σ=0.19ns @ 3 trials<br>
75% Scenario{vm=dalvikvm, benchmark=LengthEqualsZero} 21.11ns; σ=0.01ns @ 3 trials<br>
<br>
benchmark   ns logarithmic runtime<br>
EqualsEmpty 46.3 =============================<br>
IsEmpty_Empty 14.1 =<br>
IsEmpty_NonEmpty 19.1 ========<br>
LengthEqualsZero 21.1 ==========<br>
vm: dalvikvm<br>
View current and previous benchmark results online:<br>
http://microbenchmarks.appspot.com/run/example@example.com/benchmarks.regression.StringIsEmptyBenchmark<br>
<br>
benchmarks.regression.StringIsEmptyBenchmark OK (SUCCESS)<br>
Outcomes: 1. All successful. Took 1m4s.<br>
$</pre>

Note that you must have the device attached by USB and have USB debugging enabled (on the device, go to Home screen context menu -> Settings -> Applications -> Development -> USB debugging).

## Gotchas ##

1. Why was the example above so slow? Because I'd just booted a development Nexus One and it was at the "touch the Android" screen with the default live wallpaper running behind it. There's a bug that makes this eat CPU (internal bug http://b/2582506), and the solution is to either go through the setup wizard or `adb shell stop` to kill all the unnecessary stuff running on the device.

2. How do I run on production devices? Vogar will take care of this for you. Basically, the only trick is making sure you can write to the VM's `dalvik-cache` directory. Vogar sets up a separate writable `dalvik-cache` for you, the only drawback of which is that you'll have to wait for `dexopt` to re-optimize the system jars, because there's no way to tell `dalvikvm` to use two caches.

## Working without Vogar ##

If you can't or don't want to use vogar, you can manually compile your benchmark to a `.class`, then `dx` that class and Caliper and its dependencies together into one jar file, and then use `adb shell dalvikvm` to run your benchmark (or Caliper's built-in runner) directly.