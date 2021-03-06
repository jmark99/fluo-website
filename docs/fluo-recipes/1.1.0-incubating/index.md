---
layout: recipes-doc
title: Fluo Recipes 1.1.0-incubating Documentation
version: 1.1.0-incubating
---
**Fluo Recipes are common code for [Apache Fluo][fluo] application developers.**

Fluo Recipes build on the [Fluo API][fluo-api] to offer additional functionality to
developers. They are published separately from Fluo on their own release schedule.
This allows Fluo Recipes to iterate and innovate faster than Fluo (which will maintain
a more minimal API on a slower release cycle). Fluo Recipes offers code to implement
common patterns on top of Fluo's API.  It also offers glue code to external libraries
like Spark and Kryo.

### Documentation

Recipes are documented below and in the [Recipes API docs][recipes-api].

* [Combine Queue][combine-q] - A recipe for concurrently updating many keys while avoiding
  collisions.
* [Export Queue][export-q] - A recipe for exporting data from Fluo to external systems.
* [Row Hash Prefix][row-hasher] - A recipe for spreading data evenly in a row prefix.
* [RecordingTransaction][recording-tx] - A wrapper for a Fluo transaction that records all transaction
operations to a log which can be used to export data from Fluo.
* [Testing][testing] Some code to help write Fluo Integration test.

Recipes have common needs that are broken down into the following reusable components.

* [Serialization][serialization] - Common code for serializing POJOs. 
* [Transient Ranges][transient] - Standardized process for dealing with transient data.
* [Table optimization][optimization] - Standardized process for optimizing the Fluo table.
* [Spark integration][spark] - Spark+Fluo integration code.

### Usage

The Fluo Recipes project publishes multiple jars to Maven Central for each release.
The `fluo-recipes-core` jar is the primary jar. It is where most recipes live and where
they are placed by default if they have minimal dependencies beyond the Fluo API.

Fluo Recipes with dependencies that bring in many transitive dependencies publish
their own jar. For example, recipes that depend on Apache Spark are published in the
`fluo-recipes-spark` jar.  If you don't plan on using code in the `fluo-recipes-spark`
jar, you should avoid including it in your pom.xml to avoid a transitive dependency on
Spark.

Below is a sample Maven POM containing all possible Fluo Recipes dependencies:

```xml
  <properties>
    <fluo-recipes.version>1.1.0-incubating</fluo-recipes.version>
  </properties>

  <dependencies>
    <!-- Required. Contains recipes that are only depend on the Fluo API -->
    <dependency>
      <groupId>org.apache.fluo</groupId>
      <artifactId>fluo-recipes-core</artifactId>
      <version>${fluo-recipes.version}</version>
    </dependency>
    <!-- Optional. Serialization code that depends on Kryo -->
    <dependency>
      <groupId>org.apache.fluo</groupId>
      <artifactId>fluo-recipes-kryo</artifactId>
      <version>${fluo-recipes.version}</version>
    </dependency>
    <!-- Optional. Common code for using Fluo with Accumulo -->
    <dependency>
      <groupId>org.apache.fluo</groupId>
      <artifactId>fluo-recipes-accumulo</artifactId>
      <version>${fluo-recipes.version}</version>
    </dependency>
    <!-- Optional. Common code for using Fluo with Spark -->
    <dependency>
      <groupId>org.apache.fluo</groupId>
      <artifactId>fluo-recipes-spark</artifactId>
      <version>${fluo-recipes.version}</version>
    </dependency>
    <!-- Optional. Common code for writing Fluo integration tests -->
    <dependency>
      <groupId>org.apache.fluo</groupId>
      <artifactId>fluo-recipes-test</artifactId>
      <version>${fluo-recipes.version}</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
```

[fluo]: https://fluo.apache.org/
[fluo-api]: /api
[recipes-api]: /api
[combine-q]: /docs/fluo-recipes/1.1.0-incubating/combine-queue/
[export-q]: /docs/fluo-recipes/1.1.0-incubating/export-queue/
[recording-tx]: /docs/fluo-recipes/1.1.0-incubating/recording-tx/
[serialization]: /docs/fluo-recipes/1.1.0-incubating/serialization/
[transient]: /docs/fluo-recipes/1.1.0-incubating/transient/
[optimization]: /docs/fluo-recipes/1.1.0-incubating/table-optimization/
[row-hasher]: /docs/fluo-recipes/1.1.0-incubating/row-hasher/
[spark]: /docs/fluo-recipes/1.1.0-incubating/spark/
[testing]: /docs/fluo-recipes/1.1.0-incubating/testing/
[ti]: https://travis-ci.org/apache/incubator-fluo-recipes.svg?branch=main
[tl]: https://travis-ci.org/apache/incubator-fluo-recipes
[li]: http://img.shields.io/badge/license-ASL-blue.svg
[ll]: https://github.com/apache/incubator-fluo-recipes/blob/main/LICENSE
