![http://caliper.googlecode.com/svn/static/caliper.png](http://caliper.googlecode.com/svn/static/caliper.png)

Caliper is Google's open-source framework for writing, running and viewing the results of JavaMicrobenchmarks.

The latest release is `1.0-beta-1`.  It can be downloaded as a [single uberjar](https://code.google.com/p/caliper/downloads/detail?name=caliper-1.0-beta-1-all.jar) or referenced as a maven dependency:

```
<dependency>
  <groupId>com.google.caliper</groupId>
  <artifactId>caliper</artifactId>
  <version>1.0-beta-1</version>
</dependency>
```

## Getting Started ##

The simplest complete Caliper benchmark looks like this:

```
  public class MyBenchmark extends Benchmark {
    public void timeMyOperation(int reps) {
      for (int i = 0; i < reps; i++) {
        MyClass.myOperation();
      }
    }
  }
```

### Tutorial Video ###

<a href='http://www.youtube.com/watch?feature=player_embedded&v=Rbx0HUCnF24' target='_blank'><img src='http://img.youtube.com/vi/Rbx0HUCnF24/0.jpg' width='425' height=344 /></a>

_Best viewed [in YouTube](http://youtu.be/Rbx0HUCnF24) @ 1080p_

### Code Samples ###

**[Very short tutorial examples](http://code.google.com/p/caliper/source/browse/tutorial/Tutorial.java).**

**[More introductory examples](http://code.google.com/p/caliper/source/browse/examples/src/main/java/examples/).**

## Caliper Design ##

A discussion of the design and methodology employed by caliper can be found in the [Caliper Design Document](https://docs.google.com/document/d/1M0e2UNf1ZxixotjBO9r4FKzJGO7VyhrXxbKqwX1LAzo/pub).