---
title: Logging Philosophy
layout: post
category: Software
tags: [Philosophy, Logging]
---
I've compiled my logging philosophy into a single place so that I can reference it for later. Here is what I've found so far...

<!-- more -->

## Why logging?
  
**Troubleshooting** -- Show context and details for when the unexpected/undesired happens (developers)

**Telemetry** -- Gather wisdom and insight from the forest of data (telemetrists)

**Legal** -- Because we live in a world where you have to protect your butt legally (audit & legal)

## Summarized levels
  
**DEBUG** Detailed context for troubleshooting an issue.

**INFO** Normal operations for user-driven action context and system specific operations.

**WARNING** Strange or unexpected states that are acceptable.

**ERROR** Something serious went wrong, but the process can recover.

**FATAL** The process cannot recover. The app will likely die and may take the vm with it.

## In practice

### Levels in more detail

> **Note:** I have combined these levels from blogs such as the _[The Art of Logging](http://www.codeproject.com/Articles/42354/The-Art-of-Logging)_, _[Log Level Philosophy](http://tech.puredanger.com/2008/03/25/log-levels/)_, _[The 10 Commandments of Logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/)_, as well as best practices from industry leaders: _[Google](http://googletesting.blogspot.com/2013/06/optimal-logging.html)_, _[Apple](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/LoggingErrorsAndWarnings.html)_, _[Python](https://docs.python.org/2/howto/logging.html)_, and _[Atlassian](https://developer.atlassian.com/confdev/development-resources/confluence-architecture/logging-guidelines)_. 

### Debug
  
Debug messages should be aimed directly at future you or future [insert other dev] who will be troubleshooting your code. These are the hardest messages to write because you need to output as much information as possible without flooding the log with useless garbage.

> DEBUG – whatever your OCD programmer mind desires.
> 
> ~ [Log Level Philosophy](http://tech.puredanger.com/2008/03/25/log-levels/) 

Debug messages should be very abundant in the development phase of a project and significantly pruned as the application nears production. _Only the most meaningful messages should remain in production._

> I’d advocate trimming down the number of debug statement before entering the production stage, so that only the most meaningful entries are left
> 
> ~ [10 Commandments of Logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/) 

### Info
  
Info should represent represent a correctly functioning application with useful and specific. If it is not data-rich, it is probably not a good log message: `Unrecognized field "*" found in json when deserializating`

> log at this level all actions that are user-driven, or system specific (ie regularly scheduled operations…)
> 
> ~ [10 Commandments of Logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/) 

### Warning
  
Warning is the first of the actual failure levels. A warn message means that **the system can recover and the user is not affected.**

**System Notifications:** This is the perfect place to put long database requests, timed out web-service requests (that will retry), depleted thread pools, and other warning signs that the system is approaching a breaking point.

> Any condition that, while not an error in itself, may indicate that the system is running sub-optimally
> 
> ~ [Atlassian: Logging Guidelines](https://developer.atlassian.com/confdev/development-resources/confluence-architecture/logging-guidelines) 

### Error
  
Something is actually broken and needs to be fixed. If this appears in a production log, it should merit immediate action.

This is where a the database connection is dropped, where servers are unresponsive, where clients and business are lost.

### Fatal
  
Fatal (also called critical) means the application cannot recover (or start). It will die and potentially bring down other systems that rely on it. If it's really bad, it may bring down the vm. Please explain why in concise detail.

> FATAL level: too bad it’s doomsday.
> 
> ~ [10 Commandments of Logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/) 

Many logging systems don't use this level because it's too late, but the most meaningful words people say are often on their deathbeds. Our applications can also give us insight into how they lived and how they died if we give them the opportunity.

### Google's good/bad lists
  
**Good things to log** (_[Google: Optimal Logging](http://googletesting.blogspot.com/2013/06/optimal-logging.html)_)

  * Important startup configuration
  * Errors
  * Warnings
  * Changes to persistent data
  * Requests and responses between major system components
  * Significant state changes
  * User interactions
  * Calls with a known risk of failure
  * Waits on conditions that could take measurable time to satisfy
  * Periodic progress during long-running tasks
  * Significant branch points of logic and conditions that led to the branch
  * Summaries of processing steps or events from high level functions -- Avoid logging every step of a complex process in low-level functions.

**Bad things to log**

  * Function entry -- Don’t log a function entry unless it is significant or logged at the debug level.
  * Data within a loop -- Avoid logging from many iterations of a loop. It is OK to log from iterations of small loops or to log periodically from large loops.
  * Content of large messages or files -- Truncate or summarize the data in some way that will be useful to debugging.
  * Benign errors -- Errors that are not really errors can confuse the log reader. This sometimes happens when exception handling is part of successful execution flow.
  * Repetitive errors -- Do not repetitively log the same or similar error. This can quickly fill a log and hide the actual cause. Frequency of error types is best handled by monitoring. Logs only need to capture detail for some of those errors.

### More like guidelines

> **Note:** I took some liberties summarizing and pruning _[The 10 Commandments of Logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/)_ 

**Use real libraries** -- **Never** use `printf` or `System.out` to make your own log files. Use the libraries. In most cases, use Log4j. If that's not available, use a real library.

**Log at the proper level** -- Log levels determine how they will be searched. An Error in production means a Critical in Jira. Fatal means the app will die and maybe take other with it. Debugs are not a free-for-all once it's past the dev environment.

**Write meaningful logs** -- Anticipate that one day the server log will be all the information you have to solve a critical problem. Provide **concise** information with **context** so that some poor soul years from now can debug your broken code.

**Log with context** -- Do not assume your log messages will be next to each other. It's a big world out there. Do not make their making sense depend on another message. If possible use a transaction ID or other identifying information to help the debugger tie messages together and gain a larger picture.

**Use machine parsable formats** -- ElasticSearch and LogStash have the ability to parse JSON data and make it awesomely searchable. Where possible, use `{'user':1334563, 'card':'4 of spade', 'game':23425656}` over the plaintext alternative, `"User 1334563 plays 4 of spades in game 23425656"`

**Do not log too much nor too little** -- Too much log will flood the servers (slowing them) and making it difficult to find anything of use. Too little log will make it difficult to diagnose problems. Use a tight feedback loop: spamming? less log. Troubleshooting? more log.

**Think to the reader** -- Think about the poor soul who has to dig through these messages to find a problem that eluded all the devs, qa, and many clients. You are writing messages to the future. Maybe even to your future self. Poor soul. Thinking toward the reader will help focus the messages (and hopefully push toward the other commandments).

**Do not log only for troubleshooting** -- Logging is not just for troubleshooting a specific problem. It is for **auditing and telemetry** as well. Talk to your auditor and telemetrist to discover what they need to pass through to the logs.

## Sources

  * [Google: Optimal Logging](http://googletesting.blogspot.com/2013/06/optimal-logging.html)
  * [MasterZen: 10 commandments of logging](http://www.masterzen.fr/2013/01/13/the-10-commandments-of-logging/)
  * [CodeProject: Art of Logging](http://www.codeproject.com/Articles/42354/The-Art-of-Logging)
  * [Python: Logging](https://docs.python.org/2/howto/logging.html)
  * [Apple: Logging Errors and Warnings](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/LoggingErrorsAndWarnings.html)
  * [PureDanger: Log levels](http://tech.puredanger.com/2008/03/25/log-levels/)
  * [Atlassian: Logging Guidelines](https://developer.atlassian.com/confdev/development-resources/confluence-architecture/logging-guidelines)