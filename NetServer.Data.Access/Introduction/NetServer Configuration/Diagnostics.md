---
uid: netserver_configuration_diagnostics
title: NetServer Diagnostics Element
date: 2018-06-06
SortOrder: 75
---
Configuration of diagnostic logging tools.

```xml
<Diagnostics>
  <add key="LogError" value="true" />
  <add key="LogWarning" value="false" />
  <add key="LogInformation" value="false" />
  <add key="LogFailureAudit" value="false" />
  <add key="LogSuccessAudit" value="false" />
  <add key="LogToEventLog" value="false" />
  <add key="LogToSuperOffice" value="false" />
  <add key="LogToFile" value="true" />
  <add key="LogToTrace" value="false" />
  <add key="EnableScaffolding" value="false" />
  <add key="LogFolder" value="c:\temp\" />
  <add key="LogLongQueries" value="false" />
  <add key="LongQueryThreshold" value="5000" />
  <add key="LogServiceCalls" value="false" />
  <add key="LoggedServices" value="" />
  <add key="LogMail" value="false" />
  <add key="LogMailFolder" value="c:\temp\" />
  <add key="LogLongQueriesAsXml" value="false" />
</Diagnostics>
```

|Name|Description|
|------------|----|
|LogError|Determines whether error messages are logged. Default value is true.|
|LogWarning|Determines whether warning messages are logged. Default value is false.|
|LogInformation|Log general information. This includes successful SQL's passed to the database. Only permit this option while debugging a bug.  This will be a severe performance hit! Default value is false.|
|LogFailureAudit|Log failed authentications. Default value is true.|
|LogSuccessAudit|Log successful authentications. Default value is false.|
|LogToEventLog|Log to the OS event log. Default value is true.|
|LogToSuperOffice|Log to SuperOffice Research and Product Development (Online through a WebService). Default value is false.|
|SuperOfficeErrorServiceUrl|The URL used to log to SuperOffice Research and Product Development (Online through a WebService).|
|LogToFile|Log to a LogFile. Default value is false.|
|LogToTrace|Log to a Trace that can be listened to by a System.Diagnostics.TraceListener.Default value is false.|
|LogFolder|Folder (e.g. UNC path) where the log file is to reside.  Note that the owner of the process needs to have access to manipulate files in this folder. The Documents/Impersonation settings apply!|
|EnableScaffolding|When this option is enabled, extra logging is performed. It is strongly recommended to have this option enabled during development and testing. Huge log files are generated when this option is enabled!|
|LogLongQueries|Should long-running queries be logged in textual form to a special file. Default value is false.|
|LongQueryThreshold|Threshold for logging a long-running query, in milliseconds. Queries that execute in less than this time are not logged as long-running. The time is from the moment the SQL text is sent to the database, until the first row (for a select) or the 'nn rows affected' return value is received. Default value is  2500.|
|LogLongQueriesAsXML|Should long-running queries be logged to a special file (Query_year.month.day.log) in XML serialized format, for later analysis and reruns using the QueryWorkbench tool.|
|EnableStackTracing|Determines whether stack traces be collected by various events.|
|CheckBrowserVersion|Determines whether browser version information be sent back to SuperOffice for compatibility verification.|
|LogServiceCalls|Determines whether calls to the service layer are logged.|
|LoggedServices|List of services to be logged; default blank means all, otherwise comma-separated list of service names (without the Agent suffix, for instance: BLOB, Appointment).|
|LogMail|Log mail server communication.|
|LogMailFolder|Folder to use for mail logging.|
|LogTimes|Log times to file.|
|LogEventRecorder|Include a snapshot of the event recorder in all log entries.|
|EnableResourceTracer|Enable tracing of resource usage pr. operation to trace.|
|UsageStatUrl|URL for reporting Usage Statistics.|
|UserSyncUrl|URL for synchronizing user information.|
