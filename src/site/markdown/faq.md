#Frequently Asked Questions

###    Why should I adopt activity streams for my project?

Odds are the dataset you are working with is some combination of timestamped events and observations of entities and their relationships at various points in time.  Activity Streams provides a simple yet powerful standard format for these types of data, regardless of their origin, publisher, or specific details.  As an community-driven specification designed for interoperability and flexibility, by adopting activity streams you maximize the chance that a new data-source of interest to you will be compatible with your existing database, and that your database will be compatible with a community working on a new project.

###    Why should I consider using Apache Streams for my project?

If you are working with structured event and or entity data that fits with an Activity Streams model, and working with a JVM language, Apache Streams can simplify many of the challenging aspects involved with these types of projects.

Here are a few examples:

* Keeping track of the original source of each piece of information
* Harmonizing a multitude of date-time formats
* Moving between JSON, XML, YAML, and binary serializations
* Writing processing logic that can run in both batch and real-time workflows
* Defining constraints and validation rules for up-stream (third-party) and in-stream (your sphere of control) data
* Supplying run-time configuration globally and per-stream-component in a sensible manner

###    What does Apache Streams actually do?

Apache Streams is

* an SDK for data-centric JVM software
* a set of modules that connect data-providing APIs and data-persisting analytical systems
* a community working to make web and enterprise datasets interoperable by default

Apache Streams is not

* highly prescriptive or opinionated
* one-size-fits-all
* only useful for projects fully dedicated to activity streams datasets

The primary Streams git repository incubator-streams (org.apache.streams:streams-project) which contains a library of modules inputs, outputs, and reusable components for tranforming and enriching data streams.  Similar modules can also be hosted externally - so long as they publish maven artifacts compatible with your version of streams, you can import and use them in your streams easily.

The streams community also supports a seperate repository incubator-streams-examples (org.apache.streams:streams-examples) which contains a library of simple streams that are 'ready-to-run'.  Look here to see what Streams user code look like.

###    Why bother with any data framework at all?

Why use Linux, Java, Postgres, Elasticsearch, Cassandra, or Hadoop?

Frameworks make important but boring parts of systems and code just work so your team can focus on features important to your users.

If you are sure you can write code that is some combination of faster, more readable, better tested, easier to learn, easier to build with, or more maintainable than any existing framework (including Streams), maybe you should.

On the other hand, maybe you are under-estimating how difficult it will be to optimize across these factors and keep improving.

Or maybe your time is just more valuable focused on your product rather than on plumbing.

Or maybe by joining forces with others who have more than just a passing interest in running water everyone can benefit from .

###    How is streams different than "*processing framework*"?

You don't have to look hard to find great data processing frameworks for batch or for real-time.  Storm, Spark, Flink, and Dataflow are well-known and pretty solid.  At the core these platforms help you specify inputs, outputs, and a directed graph of computation and then run your code at scale.

Streams supports a similar computational model, but is more focused on intelligently modeling the data that will flow through the stream.  In this sense Streams has an alternative to avro or protocol buffers, that places flexibility, expressivity and tooling ahead of speed or compute efficiency.

Streams also seeks to make it easy to design and evolve streams, and to configure complex streams sensibly.  Where many processing frameworks leave all business logic and configuration issues to the developer, streams modules are designed to mix-and-match.

###    How do I deploy Streams?

Currently you cannot deploy "Streams".  Streams has no shrink-wrapped ready-to-run server process.  You can however deploy streams.  The right method for packaging, deploying, and running streams depends on what runtime you are going to use.

Streams includes a local runtime that uses blocking queues and multi-threaded execution within a single process.  In this scenario you build an uberjar with few exclusions and ship it to a target environment however you want - maven, scp, docker, etc...  You launch the stream process with an appropriate run configuration and watch the magic / catastrophic fail.

Alternatively, components written to streams interfaces can be bound within other platforms such as pig or spark.  In this scenario, you build an uberjar that excludes the platform parts of the classpath and launch your stream using the launch style of that platform.

###    Can't I just dump source data directly into files or databases?

Absolutely - and that will work great right up until the point where the requirements, the tools, or the way you want to index your data need to change.

A better long-term approach is to archive each data series you observe, and label each piece of data by source, connector, connector version, and execution.  Once data is 'under management' in it's original form, normalize it into a format that fits your application with a set of core fields you don't ever expect to change.  Then add metadata piece by piece using code and APIs managed by you and/or third-parties.  Write these finished data points sequentially or simultaneouly to all of the places from which your applications will look them up.

###    What if I need data from "*specific API*"?

No problem - anyone can write a Streams provider.  The project contains providers that use sockets, webhooks, and polling to generate near-real-time data streams.  There are providers which work sequentially through a backlog of items from the stream configuration, running a thread to collect data related to each item.  And if you need to collect so many items that you can't fit all of their ids in the memory available to your stream, a stream can read an arbitrarily long sequence of ids and launch new streams for each batch that terminate when complete.

###    What if I want to keep data in "*unsupported database*"?

No problem - anyone can write a Streams persist reader or persist writer.  The project contains persist writers that write documents efficiently with batch-style binary indexing, that write documents one-by-one to services with REST api endpoints, and that write data to local or distributed buffers.  If you just want to get incoming data into a queueing system to work with outside of streams that's understandable.

###    Can't I just use "*third-party SDK*" to do the same thing?

For any specific data collection, processing, or storage function there are several if not tens of basic implementations on GitHub.  There may even be language-specific libraries published by a vendor backing the technology in question.

However, in general there are a set of tradeoffs involved relying on these package.  They often have transitive dependencies.  They may not use performant HTTP and JSON libraries.  The object representations and lifecycle mechanisms they provide may not be consistent with the rest of your code.

Streams goes to great lengths to regularize many of these challenges so they uniform across existing modules, and easy to reuse within new modules.  Where quality java libraries exist, the most useful parts of their classpath may be included within a streams implementation while other dependencies are excluded.  

###    Where do I start?

Navigate the list of 'Getting Started' recommendation in order to get up and running with streams.

###    How can I help?

Please join our mailing list, then ask questions and suggest features.  Contribute to the documentation in one of the streams repositories.  Consider writing a new provider using an existing provider as a template.  