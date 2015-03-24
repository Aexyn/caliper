# Best Practices #

## Benchmarks should be deterministic and symmetric ##
Always do the exact same work within the body of the `reps` loop. Generating a random value or using the loop counter (`reps` in this example) within the body of the loop may introduce unnecessary bias in your benchmark, lowering the quality of the result.

Sometimes it's desirable to test how an operation performs when its inputs are mixed. To test this define a fixed script in `setUp()` and walk through the script each iteration of the loop. For example, to measure how fast `Set.contains()` is when 25% of the queries will be null, we create a queries script:
```
  /** the set under test */
  private Set<String> set;

  /** twenty-five percent nulls */
  private List<Object> queries = new ArrayList<Object>();

  public void setUp() {
    // initialize set
    set = ...

    for (int i = 0; i < 25; i++) {
      queries.add(null);
    }
    for (int i = 25; i < 100; i++) {
      queries.add(new Object());
    }
    Collections.shuffle(queries, new Random(0));
  }

  public void timeContains(int reps) {
    for (int i = 0; i < reps; i++) {
      for (Object query : queries) {
        set.contains(query);
      }
    }
  }
```

To calculate the average runtime of an individual `contains()` call, Caliper's measurement must be divided by 100.