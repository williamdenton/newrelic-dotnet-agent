# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### New Features
### Fixes
* Fixes issue [#485](https://github.com/newrelic/newrelic-dotnet-agent/issues/485): `SendDataOnExit` configuration setting will prevent Infinite Traces data sending interuption on application exit. ([#550](https://github.com/newrelic/newrelic-dotnet-agent/pull/609))
* Fixes issue [#155](https://github.com/newrelic/newrelic-dotnet-agent/issues/155): MVC invalid Action for valid Controller can cause MGI. ([#608](https://github.com/newrelic/newrelic-dotnet-agent/pull/608))
* Fixes issue [#186](https://github.com/newrelic/newrelic-dotnet-agent/issues/186): Attribute based Routing (ex WebAPI) can cause transaction naming issues. ([#612](https://github.com/newrelic/newrelic-dotnet-agent/pull/612))
* Fixes issue [#463](https://github.com/newrelic/newrelic-dotnet-agent/issues/463): Handle OPTIONS requests for asp.net applications. ([#612](https://github.com/newrelic/newrelic-dotnet-agent/pull/612))
* Fixes issue [#551](https://github.com/newrelic/newrelic-dotnet-agent/issues/551): Missing external calls in WCF Service. ([#610](https://github.com/newrelic/newrelic-dotnet-agent/pull/610))
* Fixes issue [#616](https://github.com/newrelic/newrelic-dotnet-agent/issues/616): Linux Kudu not accessible when .NET agent presents. ([#618](https://github.com/newrelic/newrelic-dotnet-agent/pull/618))
* Fixes issue [#266](https://github.com/newrelic/newrelic-dotnet-agent/issues/266): Agent fails to initialize and provides no logs when configured with capitalized booleans. ([#617](https://github.com/newrelic/newrelic-dotnet-agent/pull/617))
* Explain plans will be created if [transactionTracer.explainEnabled](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration/#tracer-explainEnabled) is true and one or both [transactionTracer.enabled](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration/#tracer-enabled) or [slowSql.enabled](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration/#slow_sql) are true.  If transactionTracer.explainEnabled is false or both transactionTracer.enabled and slowSql.enabled are false, no Explain Plans will be created.
* Fixes issue [#476](https://github.com/newrelic/newrelic-dotnet-agent/issues/476): When generating and explain plan MS SQL parsing is matching parts of words instead of whole words

## [8.40.0] - 2021-06-08
### New Features
* Adds Agent support for capturing HTTP Request Headers.
  * Support included for ASP.NET 4.x, ASP.NET Core, Owin, and WCF instrumentation. ([#558](https://github.com/newrelic/newrelic-dotnet-agent/issues/558), [#559](https://github.com/newrelic/newrelic-dotnet-agent/issues/559), [#560](https://github.com/newrelic/newrelic-dotnet-agent/issues/560), [#561](https://github.com/newrelic/newrelic-dotnet-agent/issues/561))

### Fixes
* Fixes issue [#264](https://github.com/newrelic/newrelic-dotnet-agent/issues/264): Negative GC count metrics will now be clamped to 0, and a log message will be written to note the correction. This should resolve an issue where the GCSampler was encountering negative values and crashing. ([#550](https://github.com/newrelic/newrelic-dotnet-agent/pull/550))
* Fixes issue [#584](https://github.com/newrelic/newrelic-dotnet-agent/issues/584): When the agent is configured to log to the console, the configured logging level from `newrelic.config` will be respected. ([#587](https://github.com/newrelic/newrelic-dotnet-agent/pull/587))

## [8.39.2] - 2021-04-14
### Fixes
* Fixes issue [#500](https://github.com/newrelic/newrelic-dotnet-agent/issues/500): For transactions without errors, Agent should still create the `error` intrinsics attribute with its value set to `false`. ([#501](https://github.com/newrelic/newrelic-dotnet-agent/pull/501))
* Fixes issue [#522](https://github.com/newrelic/newrelic-dotnet-agent/issues/522): When the `maxStackTraceLines` config value is set to 0, the agent should not send any stack trace data in the `error_data` payload. ([#523](https://github.com/newrelic/newrelic-dotnet-agent/pull/523))

## [8.39.1] - 2021-03-17
### Fixes
* Fixes issue [#22](https://github.com/newrelic/newrelic-dotnet-agent/issues/22): Agent causes exception when distributed tracing is enabled in ASP.NET Core applications that use the RequestLocalization middleware in a Linux environment. ([#493](https://github.com/newrelic/newrelic-dotnet-agent/pull/493))
* Fixes issue [#267](https://github.com/newrelic/newrelic-dotnet-agent/issues/267): On Linux, the profiler fails to parse config files that start with a UTF-8 byte-order-mark (BOM). ([#492](https://github.com/newrelic/newrelic-dotnet-agent/pull/492))
* Fixes issue [#464](https://github.com/newrelic/newrelic-dotnet-agent/issues/464): Distributed tracing over RabbitMQ does not work with `RabbitMQ.Client` versions 6.x+ ([#466](https://github.com/newrelic/newrelic-dotnet-agent/pull/466))
* Fixes issue [#169](https://github.com/newrelic/newrelic-dotnet-agent/issues/169): Profiler should be able to match method parameters from XML that contain a space. ([#461](https://github.com/newrelic/newrelic-dotnet-agent/pull/461))

## [8.39] - 2021-02-10
### New Features
* Add `GetBrowserTimingHeader(string nonce)` overload.
  * This allows sites with a `Content-Security-Policy` that disables `'unsafe-inline'` to emit the inline script with a nonce.

### Fixes
* Fixes Issue [#394](https://github.com/newrelic/newrelic-dotnet-agent/issues/394): agent fails to enable infinite tracing in net5.0 docker images

## [8.38] - 2021-01-26
### New Features
* **Improvements to New Relic Edge (Infinite Tracing)** <br/>
  * The agent will now handle having its infinite tracing traffic moved from one backend host to another without losing data or requiring an agent restart.
  * Improved logging of infinite tracing connections.

## [8.37] - 2021-01-04
### New Features
* **Updated support for RabbitMQ** <br/>
  * Adds support for .NET Core applications using RabbitMQ.Client.
  * Adds support for RabbitMQ.Client version 6.2.1.
  * Not supported: Distributed Tracing is not supported with the RabbitMQ AMQP 1.0 plugin.

* **Adds [configuration](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration) Environment Variables** <br/>
  * Adds MAX_TRANSACTION_SAMPLES_STORE - the maximum number of samples stored for Transaction Events.
  * Adds MAX_EVENT_SAMPLES_STORED - the maximum number of samples stored for Custom Events. 
  * Adds NEW_RELIC_LOG - the unqualifed name for the Agent's log file.

## [8.36] - 2020-12-08

### Fixes
* Fixes Issue [#224](https://github.com/newrelic/newrelic-dotnet-agent/issues/224): leading "SET" commands will be ignored when parsing compound SQL statements. ([#370](https://github.com/newrelic/newrelic-dotnet-agent/pull/370))
* Fixes Issue [#226](https://github.com/newrelic/newrelic-dotnet-agent/issues/226): the profiler ignores drive letter in `HOME_EXPANDED` when detecting running in Azure Web Apps. ([#373](https://github.com/newrelic/newrelic-dotnet-agent/pull/373))
* Fixes Issue [#93](https://github.com/newrelic/newrelic-dotnet-agent/issues/93): when the parent methods are blocked by their asynchronous child methods, the agent deducts the child methods' duration from the parent methods' exclusive duration.([#374](https://github.com/newrelic/newrelic-dotnet-agent/pull/374))
* Fixes Issue [#9](https://github.com/newrelic/newrelic-dotnet-agent/issues/9) where the agent failed to read settings from `appsettings.{environment}.json` files. ([#372](https://github.com/newrelic/newrelic-dotnet-agent/pull/372))
* Fixes Issue [#116](https://github.com/newrelic/newrelic-dotnet-agent/issues/116) where the agent failed to read settings from `appsettings.json` in certain hosting scenarios. ([#375](https://github.com/newrelic/newrelic-dotnet-agent/pull/375))
* Fixes Issue [#234](https://github.com/newrelic/newrelic-dotnet-agent/issues/234) by reducing the likelihood of a Fatal CLR Error. ([#376](https://github.com/newrelic/newrelic-dotnet-agent/pull/376))
* Fixes Issue [#377](https://github.com/newrelic/newrelic-dotnet-agent/issues/377) when using the `AddCustomAttribute` API with `Microsoft.Extensions.Primitives.StringValues` type causes unsupported type exception. ([378](https://github.com/newrelic/newrelic-dotnet-agent/pull/378))


## [8.35] - 2020-11-09

### New Features
* **.NET 5 GA Support** <br/>
We have validated that this version of the agent is compatible with .NET 5 GA. See the [compatibility and requirements for .NET Core](https://docs.newrelic.com/docs/agents/net-agent/getting-started/net-agent-compatibility-requirements-net-core) page for more details.

### Fixes
* Fixes Issue [#337](https://github.com/newrelic/newrelic-dotnet-agent/issues/337) by removing obsolete code which was causing memory growth associated with a large number of transaction names.
* PR [#348](https://github.com/newrelic/newrelic-dotnet-agent/pull/348): guards against potential exceptions being thrown from the agent API when the agent is not attached.  

## [8.34] - 2020-10-26

### New Features
* **.NET 5 RC2 Support** <br/>
We have validated that this version of the agent is compatible with .NET 5 Release Candidate 2.

### Fixes
* Fixes issue [#301](https://github.com/newrelic/newrelic-dotnet-agent/issues/301) where the agent incorrectly parses server-side configuration causing agent to shutdown.([#310](https://github.com/newrelic/newrelic-dotnet-agent/pull/310))
* Modifies WCF Instrumentation to address [#314](https://github.com/newrelic/newrelic-dotnet-agent/issues/314) by minimizing the reliance upon handled exceptions during the  attempt to capture CAT and DT payloads.

## [8.33] - 2020-10-12

### Fixes
* Fixes [#223](https://github.com/newrelic/newrelic-dotnet-agent/issues/223) so the agent can be compatible with ASP.NET Core 5 RC1.
* Fixes issue in .NET 5 applications where external calls made with HttpClient may not get instrumented. For example, calls made with `HttpClient.GetStringAsync` would be missed. ([#235](https://github.com/newrelic/newrelic-dotnet-agent/pull/235))
* Fixes issue [#257](https://github.com/newrelic/newrelic-dotnet-agent/issues/223) where .NET Standard Libraries that do not reference `mscorlib` fail to be instrumented in .NET Framework applications.
* Reduces the performance impact of large amounts of instrumentation. See issue [#269](https://github.com/newrelic/newrelic-dotnet-agent/issues/269) for more information.

## [8.32] - 2020-09-17

### New Features
* **Proxy Password Obfuscation Support** <br/>
Agent configuration supports the obfuscation of the proxy password. [The New Relic Command Line Interface (CLI)](https://github.com/newrelic/newrelic-cli/blob/master/README.md) may be used to obscure the proxy password.  The following [documentation](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#proxy) describes how to use an obscured proxy password in the .NET Agent configuration.
* **MySqlConnector Support** <br/>
The MySqlConnector ADO.NET driver is instrumented by default. Fixes [#85](https://github.com/newrelic/newrelic-dotnet-agent/issues/85) and implements [this suggestion](https://discuss.newrelic.com/t/feature-idea-support-mysqlconnector-driver-for-db-instrumentation/63414).

* **Nullable Reference Type support in the API**<br/>
Enables nullable reference types that are part of the C# 8.0 language specification and updates the signatures of API methods accordingly.  There should be no required changes in API usage.

* **Improved Support for NetTCP Binding in WCF Instrumation**
When the NetTCP Binding type is used in Windows Communication Foundation (WCF), the Agent will now send and receive trace context information in support of Distributed Tracing (DT) or Cross Application Tracing (CAT).  Implements [#209](https://github.com/newrelic/newrelic-dotnet-agent/issues/209).

### Fixes
* Fixes an issue that may cause `InvalidCastException` due to an assembly version mismatch in Mvc3 instrumentation.
* Fixes an async timing issue that can cause the end time of `Task`-returning methods to be determined incorrectly.


## [8.31] - 2020-08-17
### New Features
* **Expected Errors Support** <br/>
Certain errors that are expected within the application may be identified so that they will not be counted towards the application's error rate and Apdex Score.  Only errors that truly affect the health of the application will be alerted on.  Please review the following [documentation](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error_collector) for details on how to configure Expected Errors.

* **Ignored Errors Enhancements** <br/>
Certain errors may be identified in configuration so that they will be ignored.  These errors will not be counted towards the application's error rate, Apdex score, and will not be reported by the agent. Please review the following [documentation](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error_collector) for details on how to configure Ignored Errors.
    * New configuration element [`<ignoreMessages>`](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error-ignoreErrors)supports filtering based on the error message. 
    * Please note that the [`<ignoreErrors>`](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error-ignoreErrors) configuration element has been deprecated and replaced by [`<ignoreClasses>`](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error-ignoreClasses).  The .NET Agent continues to support this configuration element, but its support may be removed in the future.

### Fixes
* **Garbage Collection Performance Metrics for Windows** <br/>
Fixes an issue where Garbage Collection Performance Metrics may not be reported for Windows Applications.

* **Maintaining newrelic.config on Linux package upgrades** <br/>
Fixes an issue where `newrelic.config` was being overwritten when upgrading the agent via either `rpm`/`yum` (RedHat/Centos) or `dpkg`/`apt` (Debian/Ubuntu).

## [8.30] - 2020-07-15
### New Features
* **The .NET Agent is now open source!** <br/>
The New Relic .NET agent is now open source! Now you can view the source code to help with troubleshooting, observe the project roadmap, and file issues directly in this repository.  We are now using the [Apache 2 license](/LICENSE). See our [Contributing guide](/CONTRIBUTING.md) and [Code of Conduct](https://opensource.newrelic.com/code-of-conduct/) for details on contributing!

### Fixes
* **Memory Usage Reporting for Linux** <br/>
Fixes issue where applications running on Linux were either reporting no physical memory usage or using VmData to report the physical memory usage of the application. The agent now uses VmRSS through a call to [`Process.WorkingSet64`](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.process.workingset64) to report physical memory usage. See the [dotnet runtime discussion](https://github.com/dotnet/runtime/issues/28990) and the [proc man pages](https://man7.org/linux/man-pages/man5/proc.5.html) for more details about this change.

* **Infinite Tracing Performance** <br/>
Fixes issue where the Agent may consume too much memory when using Infinite Tracing.

* **.NET 5 support** <br/>
Fixes issue with applications running on .NET 5 that prevented instrumentation changes at runtime (either though editing instrumentation XML files or through the Live Instrumentation editor Beta).

## [8.29] - 2020-06-25
### New Features

* **Additional Transaction Information applied to Span Events** <br/>
When Distributed Tracing and/or Infinite Tracing are enabled, the Agent will now incorporate additional information from the Transaction Event on to the root Span Event of the transaction.

    * The following items are affected:

        * Request Parameters `request.parameter.*`
        * Custom Attribute Values applied to the Transaction via API Calls [`AddCustomParameter`](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/add-custom-parameter) and [`ITransaction.AddCustomAttribute`](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#addcustomattribute).
        * `request.uri`
        * `response.status`
        * `host.displayName`
    * **Security Recommendation** <br>
    Review your [Transaction Attributes](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#transaction_events) configuration.  Any attribute include or exclude settings specific to Transaction Events, should be applied to your [Span Attributes](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#span_events) configuration or your [Global Attributes](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#agent-attributes) configuration.
    
### Fixes
Fixes issue where updating custom instrumentation while application is running could cause application to crash.

## [8.28] - 2020-06-04
### New Features
### Fixes
* **Infinite Tracing** <br>
    * Fixes issue with Infinite Tracing where a communication error can result in consuming too much CPU.
    * Fixes issue with Infinite Tracing where a communication error did not clean up its corresponding communication threads.
    * <p style="color:red;">Agent version 8.30 introduces significant performance enhancements to Infinite Tracing.  To use Infinite Tracing, please upgrade to version 8.30 or later.</p>

* Fixes issue in .NET Framework ASP.NET MVC applications where transactions started on one thread would flow to background threads (e.g., started with `Task.Run`) in some scenarios but not others. Transaction state used to only flow to a background thread if the transaction originated from an async controller action. Transaction state now flows to background threads regardless of whether the controller action is async or not.
* Fixes issue in .NET Framework ASP.NET MVC applications where agent instrumentation of an MVC controller action could cause an `InvalidProgramException`.
* Fixes a problem with the reporting of Errors where Error Events may not appear even though Error Traces are being sent.

## [8.27] - 2020-04-30
### New Features
* **Support for W3C Trace Context, with easy upgrade from New Relic trace context**
  * [Distributed Tracing now supports W3C Trace Context headers](https://docs.newrelic.com/docs/understand-dependencies/distributed-tracing/get-started/introduction-distributed-tracing#w3c-support) for HTTP when distributed tracing is enabled.  Our implementation can accept and emit both W3C trace header format and New Relic trace header format. This simplifies agent upgrades, allowing trace context to be propagated between services with older and newer releases of New Relic agents. W3C trace header format will always be accepted and emitted. New Relic trace header format will be accepted, and you can optionally disable emission of the New Relic trace header format.
  * When distributed tracing is enabled with `<distributedTracing enabled="true" />`, the .NET agent will now accept W3C's `traceparent` and `tracestate` headers when calling [Transaction.AcceptDistributedTraceHeaders](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#acceptdistributedtraceheaders).  When calling [Transaction.InsertDistributedTraceHeaders](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#insertdistributedtraceheaders), the .NET agent will include the W3C headers along with the New Relic distributed tracing header, unless the New Relic trace header format is disabled using `<distributedTracing enabled="true" excludeNewrelicHeader="true" />`.
  * The existing `Transaction.AcceptDistributedTracePayload` and `Transaction.CreateDistributedTracePayload` APIs are **deprecated** in favor of [Transaction.AcceptDistributedTraceHeaders](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#acceptdistributedtraceheaders) and [Transaction.InsertDistributedTraceHeaders](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#insertdistributedtraceheaders).

### Fixes
* Fixes issue which prevented Synthetics from working when distributed tracing is enabled.
* Fixes issue where our RPM package for installing the agent on RPM-based Linux distributions included a 32-bit shared library, which created unnecessary dependencies on 
  32-bit system libraries.
* Fixes issue where the TransportDuration metric for distributed traces was always reporting 0.


## [8.26] - 2020-04-20
### New Features
* **Infinite Tracing on New Relic Edge**

  This release adds support for [Infinite Tracing on New Relic Edge](https://docs.newrelic.com/docs/understand-dependencies/distributed-tracing/enable-configure/enable-distributed-tracing). Infinite Tracing observes 100% of your distributed traces and provides visualizations for the most actionable data so you have the examples of errors and long-running traces so you can better diagnose and troubleshoot your systems.

  You configure your agent to send traces to a trace observer in New Relic Edge. You view your distributed traces through the New Relic’s UI. There is no need to install a collector on your network.

  Infinite Tracing is currently available on a sign-up basis. If you would like to participate, please contact your sales representative.

  <p style="color:red;">Agent version 8.30 introduces significant performance enhancements to Infinite Tracing.  To use Infinite Tracing, please upgrade to version 8.30 or later.</p>
  
* **Error attributes now added to each span that exits with an error or exception**

  Error attributes `error.class` and `error.message` are now included on the span event in which an error or exception was noticed, and, in the case of unhandled exceptions, on any ancestor spans that also exit with an error. The public API method `NoticeError` now attaches these error attributes to the currently executing span.

  [Spans with error details are now highlighted red in the Distributed Tracing UI](https://docs.newrelic.com/docs/apm/distributed-tracing/ui-data/understand-use-distributed-tracing-data#rules-limits), and error details will expose the associated `error.class` and `error.message`. It is also now possible to see when an exception leaves the boundary of the span, and if it is caught in an ancestor span without reaching the entry span. NOTE: This “bubbling up” of exceptions will impact the error count when compared to prior behavior for the same trace. It is possible to have a trace that now has span errors without the trace level showing an error.

  If multiple errors occur on the same span, only the most recent error information is added to the attributes. Prior errors on the same span are overwritten.

  These span event attributes conform to [ignored errors](https://docs.newrelic.com/docs/agents/manage-apm-agents/agent-data/manage-errors-apm-collect-ignore-or-mark-expected#ignore) configuration.

### Fixes
* Fixes issue in the MSI installer which prevented the `InstrumentAllNETFramework` feature selection from working as expected on the command line.
* Fixes issue for Azure App Service environments running on Linux that caused both the application and its Kudu process to be instrumented by the agent. The Kudu process is no longer instrumented.
* Fixes issue when using the [`ignoreErrors` configuration](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#error-ignoreErrors). Previously, when an exception contained a inner exception(s), the `ignoreErrors` config was only applied to the outer-most exception. Now, both the outer-most and inner-most exception type are considered when evaluating the `ignoreErrors` configuration.
* Fixes an issue that could cause an exception to occur in the instrumentation for StackExchange Redis. This exception caused the instrumentation to shut down leaving StackExchange Redis uninstrumented.

## [8.25] - 2020-03-11

### New Features
* **Thread profiling support for Linux**

  Thread profiling on Linux will be supported on .NET Core 3.0 or later applications when running .NET agent version 8.23 or later. Triggering a thread profile is done from the `Thread profiler` page in APM. This page does not yet have the functionality enabled, but it will be enabled in the next few business days.

* **Accessing Span-Specific information using the .NET Agent API**
  
  New property, `CurrentSpan` has been added to `IAgent` and `ITransaction`.  It returns an object implementing `ISpan` which provides access to span-specific functions within the API.

* **Adding Custom Span Attributes using the .NET Agent API**
  
  New method, `AddCustomAttribute(string, object)` has been added to `ISpan`.

  * This new method accepts and supports all data-types.
  * Further information may be found within [.NET Agent API documentation](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/ispan).
  * Adding custom attributes to spans requires distributed tracing and span events to be enabled. See [.NET agent configuration](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#distributed_tracing)


### Fixes
* Fixes issue where adding multiple custom attributes on a Transaction using [`ITransaction.AddCustomAttribute`](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction#addcustomattribute) causes the agent to ignore additional attempts to add custom attributes to any transaction. 
* Fixes issue that prevented Custom Events from being sent to New Relic until the agent shuts down.
* Fixes issue that can cause asynchronous Redis calls in an ASP.NET MVC application to report an inflated duration.


## [8.24] - 2020-02-19

### New Features
* **Adding Custom Transaction Attributes using the .NET Agent API**

  New method, `AddCustomAttribute(string, object)` has been added to `ITransaction`.
  * This new method accepts and supports all data-types.
  * Method `AddCustomParameter(string, IConvertable)` is still available with limited data-type support; however, this method should be considered obsolete and will  be removed in a future release of the Agent API.
  * Further information may be found within [.NET Agent API documentation](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api/itransaction).

* **Enhanced type support for `RecordCustomEvent` and `NoticeError` API Methods.**

  APIs for recording exceptions and custom events now support values of all types.
  * The `NoticeError` API Method has new overloads that accept an `IDictionary<string, object>`.
  * The `RecordCustomEvent` methods have been modified to handle all types of data.  In that past, they only handled `string` and `float` types.
  * Further information may be found within [.NET Agent API documentation](https://docs.newrelic.com/docs/agents/net-agent/net-agent-api).

* **New attributes on span events**

  * Spans created for external HTTP calls now include the `http.statusCode` attribute representing the status code of the call.
  * Spans created for calls to a datastore now include the `db.collection` attribute. For instance, this will be the table name for a call to MS SQL Server.

* **Ability to exclude attributes from span events**

  Attributes on span events (e.g., `http.url`) can now be excluded via configuration. See [.NET agent configuration](https://docs.newrelic.com/docs/agents/net-agent/configuration/net-agent-configuration#span_events) for further information.


### Fixes
* New Relic distributed tracing relies on propagating trace and span identifiers in the headers of external calls (e.g., an HTTP call). These identifiers now only contain lowercase alphanumeric characters. Previous versions of the .NET agent used uppercase alphanumeric characters. The usage of uppercase alphanumeric characters can break traces when calling downstream services also monitored by a New Relic agent that supports W3C trace context (New Relic's .NET agent does not currently support W3C trace context. Support for W3C trace context for .NET will be in an upcoming release). This is only a problem if a .NET application is the originator of the trace.

[Unreleased]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.40.0...HEAD
[8.40.0]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.39.2...v8.40.0
[8.39.2]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.39.1...v8.39.2
[8.39.1]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.39.0...v8.39.1
[8.39]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.38.0...v8.39.0
[8.38]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.37.0...v8.38.0
[8.37]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.36.0...v8.37.0
[8.36]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.35.0...v8.36.0
[8.35]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.34.0...v8.35.0
[8.34]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.33.0...v8.34.0
[8.33]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.32.0...v8.33.0
[8.32]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.31.0...v8.32.0
[8.31]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.30.0...v8.31.0
[8.30]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.29.0...v8.30.0
[8.29]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.28.0...v8.29.0
[8.28]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.27.139...v8.28.0
[8.27]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.26.630...v8.27.139
[8.26]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.25.214...v8.26.630
[8.25]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.24.244...v8.25.214
[8.24]: https://github.com/newrelic/newrelic-dotnet-agent/compare/v8.23.107...v8.24.244
