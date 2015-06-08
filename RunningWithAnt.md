# Introduction #

Apache Ant (http://ant.apache.org/) is a Java library and command-line tool usually used to compile and build software applications -- particularly Java applications -- but "Ant can be used to pilot any type of process which can be described in terms of targets and tasks".

An Ant 'build file' is well-formed XML.

If you know "Make", you can think of Ant build files as Make files with pointy brackets.  Or you can think of build files as a particularly verbose and rather unwieldy programming language.  Or think of them any way you like.

You can incorporate running XSpec tests into your own Ant build process, or you can Ant to run the XSpec tests from the command line similarly to how you run one of the provided scripts.

**Requires Ant 1.8 or later**

# XSpec from your Ant build file #

There are two ways to run XSpec from within your Ant build file:
  * Using the `<xspec>` macro
  * Calling the XSpec target in XSpec's build file

## Importing XSpec's `build.xml` file ##

The essential feature is to tell Ant where to find XSpec's `build.xml`, which contains the property, macro and target definitions needed to run XSpec.

The simplest way is to just import XSpec's file:
```xml
  <import file="../../xspec/build.xml" />```

When you need to override (by predefining) the properties used in XSpec's `build.xml` (e.g., when your Saxon jar file has a different location from the default) you can either:
  * Define the properties individually in your own build file; or
  * Define a `xspec.properties` property that refers to a property file that will be used by XSpec's `build.xml`.

```xml
  <property name="xspec.properties" location="../../system.properties" />

<property name="xspec.project.dir" location="../../xspec" />

<import file="${xspec.project.dir}/build.xml" />```

## `<xspec>` macro ##

This runs XSpec and produces the HTML report for a single XSpec file.

You would typically put one or more `<xspec>` macros in a target named "`test`" (or similar) that you would execute whenever you need to run the tests:

```xml
  <target name="test">
<xspec xspec.xml="para.xspec" />
<xspec xspec.xml="note.xspec" />
<xspec xspec.xml="inline.xspec" />
<xspec xspec.xml="table.xspec" />


Unknown end tag for &lt;/target&gt;

```

## Calling XSpec build file target ##

The more verbose way, which you will probably never need to do, is to call the `xspec` target in XSpec's `build.xml` directly:

```xml
  <target name="test-old">
<antcall target="xspec.xspec" inheritall="false">
<param name="xspec.xml"
location="${basedir}/table.xspec" />
<param name="xspec.base.dir"
location="${basedir}" />
<param name="xspec.dir"
location="${basedir}" />
<param name="xspec.base"
value="table" />


Unknown end tag for &lt;/antcall&gt;




Unknown end tag for &lt;/target&gt;

```

# Ant on the command line #

You can run a single XSpec test file using Ant on the command line from the installed XSpec directory:

```
  > ant -Dxspec.xml=filename
```

You'll need to specify the filename of the XSpec test file each time.

When you need to set other properties, e.g., when your Saxon jar isn't in the expected place, you can set them on the command line, too:

```
  > ant -Dxspec.xml=filename -Dsaxon.jar=/path/to/your/saxon.jar
```

Since your Saxon jar doesn't move around nearly as often as you use XSpec, you can instead specify such more stable properties in a `xspec.properties` file in the installed XSpec directory.

# Useful Properties #

The XSpec `build.xml` file contains reasonable default values for the properties that it uses -- except `xspec.xml` since that's the file with the XSpec tests.

You can override the defaults by predefining the property:

  * On the Ant command line using "`-Dname=value`"
  * In a build file that imports XSpec's `build.xml`
  * In a `xspec.properties` file in the XSpec installation directory
    * Or a different property file to which the `xspec.properties` property refers

The useful properties are:

| **Name** | **Comment** |
|:---------|:------------|
| `xspec.xml` | Name of XSpec test file.  Required |
| `saxon.home` | Directory containing a `saxon.jar` file.  If your Saxon jar file isn't named `saxon.jar`, then you'll instead need to set `saxon.jar` to the full path to your Saxon jar file|
| `saxon.jar` | Full filename of Saxon jar file.  Defaults to `${saxon.home}/saxon.jar`.|
| `xspec.properties` | Location of Ant properties file for use by XSpec. (Specify on the command line or in the calling build file since it's too late if you set this within the `xspec.properties` file.)|
| `xspec.dir` | Where to write the XSpec intermediate and result files.  Defaults to a `xspec` directory created as a subdirectory of the directory containing the XSpec test file (i.e., as a subdirectory of the directory containing `xspec.xml`). |