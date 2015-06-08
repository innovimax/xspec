# Introduction #

XSpec is a [Behaviour Driven Development](http://en.wikipedia.org/wiki/Behavior_Driven_Development) (BDD) framework for XML processing, currently focused on [XSLT](http://www.w3.org/TR/xslt20).

BDD is like Test Driven Development (TDD) in that it encourages you to develop your code by

  1. describing a behaviour (or writing a test)
  1. testing whether your code gives that behaviour
  1. if it doesn't, fixing the code until it does and the test passes

The difference between BDD and TDD is about how you write the tests. In BDD, your focus is on the behaviour of the code: the descriptions form the double role of both a human-readable documentation of what the code should do and runnable tests that can test whether the code does what it should do.

In BDD, we describe **scenarios** and the expected behaviour of the application with these scenarios. Scenarios fit particularly well with XSLT's source-driven (or template-driven) approach. For example, a scenario might be:

> when processing a `<para>` element, it should create a `<p>` element.

or something more complex like:

> when processing a `<fn>` element with a `label` attribute in `footnote` mode,
> it should create a `<p>` element with a `<sup>` child holding the value of the `label` element.

Scenarios written like this naturally map onto XSLT templates.

# Install #

Just unzip the distribution file (see the `Downloads` tab at the bottom of the page) somewhere in your hard drive.  Alternatively you can use the trunk version directly out of Subversion (once downloaded, you use both the same way).

The directory contains a batch file to be used on Windows, a shell script to be used on Unix-like systems (including Mac OS X) and an XProc script to be used on systems with support for XProc.

The batch script needs you to adapt the path to Saxon (the line `SET CP=...` at the very beginning) to point to an existing [Saxon](http://www.saxonica.com/) JAR file. For the shell script, you have to define either `$SAXON_HOME` (to point to the directory you installed Saxon) or `$SAXON_CP` (a full classpath containing Saxon). If you move the script, you have to define the environment variable `$XSPEC_HOME`.

Just follow your system's conventions regarding applications.  For instance, you can add the directory to your `$PATH`.  Personally, I have a directory `~/bin/` which is already in my `$PATH`.  I just create a new script for each program I install, which just runs the original one, still in its original directory.

# From Here #

  * Learn how to [write XSpec scenarios](WritingScenarios.md).
  * Learn how to [run XSpec scenarios](RunningScenarios.md).