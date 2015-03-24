# A. The benchmark class #

### 1. Does the benchmark use Caliper? ###

If it doesn't, it could still be good, but this page will not list every one of the problems you need to watch out for.  Some of the gotchas with microbenchmarking are taken care of for you by Caliper (that's why we wrote it!), and those are not mentioned here.

### 2. Could a compiler _possibly_ optimize your benchmark away? ###

If a JIT compiler can detect that your code doesn't actually depend on the "right answer" coming from the code under test, it might perform optimizations that will prevent some or all of the code you meant to test from even executing.  Make sure that your benchmark method returns a value -- it can be of any type you want -- that is dependent on actual correct execution of the method.

### 3. Are the test inputs representative of the real world? ###

If the tested code acts on phony data that doesn't resemble the kind of inputs seen in real life, the benchmark result is worthless. A JIT compiler can optimize your method differently depending on which of its code paths get taken more often (or taken at all), and you want to induce it to compile it as similarly as possible to how it does in real life.

Note that even though values for `@Param` fields can be given at the command line, it's still just as important to provide sensible default values.

### 4. Does the benchmark do too much work inside the "reps" loop? ###

You want to do as little work as possible inside the loop. Of course, in theory you'd like to do absolutely _nothing_ but invoke the method under test, but this is never really possible (see section 2 -- and then there's the looping overhead itself).  You'll have to accept that each result is going to be padded with a certain amount of noise.  Just make sure you keep that noise to a minimum.  For example, instead of using `Random.nextInt` inside the loop, fill an array with random integers during the `setUp` phase.  It's especially good to do as little memory allocation inside the loop as possible.

# B. Running the benchmark #

  * Choose appropriate environments for testing
  * Use quiescent machines
  * Run multiple --trials (at least 5 if you're serious; there is actually research that says ~40!)
  * You may need to check the verbose logs to ensure GC and compilation aren't happening during the timing intervals, and tweak your run parameters accordingly

# C. Interpreting the results #

TODO...