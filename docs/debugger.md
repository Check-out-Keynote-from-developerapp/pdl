
### domain: Debugger

Debugger domain exposes JavaScript debugging capabilities. It allows setting and removing
breakpoints, stepping through execution, exploring stack traces, etc.

---


#### command: Debugger.continueToLocation

Continues execution until specific location is reached.

*parameters*
-  `location` <[Debugger.Location]> Location to continue to
- *optional* `targetCallFrames` <[string]> 

---


#### command: Debugger.disable

Disables debugger for given page.

---


#### command: Debugger.enable

Enables debugger for the given page. Clients should not assume that the debugging has been
enabled until the result for this command is received.

*returns*
-  `debuggerId` <[Runtime.UniqueDebuggerId]> 🌱 Unique identifier of the debugger

---


#### command: Debugger.evaluateOnCallFrame

Evaluates expression on a given call frame.

*parameters*
-  `callFrameId` <[Debugger.CallFrameId]> Call frame identifier to evaluate on
-  `expression` <[string]> Expression to evaluate
- *optional* `objectGroup` <[string]> String object group name to put result into (allows rapid releasing resulting object handles
using `releaseObjectGroup`)
- *optional* `includeCommandLineAPI` <[boolean]> Specifies whether command line API should be available to the evaluated expression, defaults
to false
- *optional* `silent` <[boolean]> In silent mode exceptions thrown during evaluation are not reported and do not pause
execution. Overrides `setPauseOnException` state
- *optional* `returnByValue` <[boolean]> Whether the result is expected to be a JSON object that should be sent by value
- *optional* `generatePreview` <[boolean]> 🌱 Whether preview should be generated for the result
- *optional* `throwOnSideEffect` <[boolean]> Whether to throw an exception if side effect cannot be ruled out during evaluation

*returns*
-  `result` <[Runtime.RemoteObject]> Object wrapper for the evaluation result
- *optional* `exceptionDetails` <[Runtime.ExceptionDetails]> Exception details

---


#### command: Debugger.getPossibleBreakpoints

Returns possible locations for breakpoint. scriptId in start and end range locations should be
the same.

*parameters*
-  `start` <[Debugger.Location]> Start of range to search possible breakpoint locations in
- *optional* `end` <[Debugger.Location]> End of range to search possible breakpoint locations in (excluding). When not specified, end
of scripts is used as end of range
- *optional* `restrictToFunction` <[boolean]> Only consider locations which are in the same (non-nested) function as start

*returns*
-  `locations` <array of [Debugger.BreakLocation]> List of the possible breakpoint locations

---


#### command: Debugger.getScriptSource

Returns source for the script with given id.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Id of the script to get source for

*returns*
-  `scriptSource` <[string]> Script source

---


#### command: Debugger.getStackTrace 🌱

Returns stack trace with given `stackTraceId`.

*parameters*
-  `stackTraceId` <[Runtime.StackTraceId]> 

*returns*
-  `stackTrace` <[Runtime.StackTrace]> 

---


#### command: Debugger.pause

Stops on the next JavaScript statement.

---


#### command: Debugger.pauseOnAsyncCall 🌱

*parameters*
-  `parentStackTraceId` <[Runtime.StackTraceId]> Debugger will pause when async call with given stack trace is started

---


#### command: Debugger.removeBreakpoint

Removes JavaScript breakpoint.

*parameters*
-  `breakpointId` <[Debugger.BreakpointId]> 

---


#### command: Debugger.restartFrame

Restarts particular call frame from the beginning.

*parameters*
-  `callFrameId` <[Debugger.CallFrameId]> Call frame identifier to evaluate on

*returns*
-  `callFrames` <array of [Debugger.CallFrame]> New stack trace
- *optional* `asyncStackTrace` <[Runtime.StackTrace]> Async stack trace, if any
- *optional* `asyncStackTraceId` <[Runtime.StackTraceId]> 🌱 Async stack trace, if any

---


#### command: Debugger.resume

Resumes JavaScript execution.

---


#### command: Debugger.scheduleStepIntoAsync 🌱

This method is deprecated - use Debugger.stepInto with breakOnAsyncCall and
Debugger.pauseOnAsyncTask instead. Steps into next scheduled async task if any is scheduled
before next pause. Returns success when async task is actually scheduled, returns error if no
task were scheduled or another scheduleStepIntoAsync was called.

---


#### command: Debugger.searchInContent

Searches for given string in script content.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Id of the script to search in
-  `query` <[string]> String to search for
- *optional* `caseSensitive` <[boolean]> If true, search is case sensitive
- *optional* `isRegex` <[boolean]> If true, treats string parameter as regex

*returns*
-  `result` <array of [Debugger.SearchMatch]> List of search matches

---


#### command: Debugger.setAsyncCallStackDepth

Enables or disables async call stacks tracking.

*parameters*
-  `maxDepth` <[integer]> Maximum depth of async call stacks. Setting to `0` will effectively disable collecting async
call stacks (default)

---


#### command: Debugger.setBlackboxPatterns 🌱

Replace previous blackbox patterns with passed ones. Forces backend to skip stepping/pausing in
scripts with url matching one of the patterns. VM will try to leave blackboxed script by
performing 'step in' several times, finally resorting to 'step out' if unsuccessful.

*parameters*
-  `patterns` <array of [string]> Array of regexps that will be used to check script url for blackbox state

---


#### command: Debugger.setBlackboxedRanges 🌱

Makes backend skip steps in the script in blackboxed ranges. VM will try leave blacklisted
scripts by performing 'step in' several times, finally resorting to 'step out' if unsuccessful.
Positions array contains positions where blackbox state is changed. First interval isn't
blackboxed. Array should be sorted.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Id of the script
-  `positions` <array of [Debugger.ScriptPosition]> 

---


#### command: Debugger.setBreakpoint

Sets JavaScript breakpoint at a given location.

*parameters*
-  `location` <[Debugger.Location]> Location to set breakpoint in
- *optional* `condition` <[string]> Expression to use as a breakpoint condition. When specified, debugger will only stop on the
breakpoint if this expression evaluates to true

*returns*
-  `breakpointId` <[Debugger.BreakpointId]> Id of the created breakpoint for further reference
-  `actualLocation` <[Debugger.Location]> Location this breakpoint resolved into

---


#### command: Debugger.setBreakpointByUrl

Sets JavaScript breakpoint at given location specified either by URL or URL regex. Once this
command is issued, all existing parsed scripts will have breakpoints resolved and returned in
`locations` property. Further matching script parsing will result in subsequent
`breakpointResolved` events issued. This logical breakpoint will survive page reloads.

*parameters*
-  `lineNumber` <[integer]> Line number to set breakpoint at
- *optional* `url` <[string]> URL of the resources to set breakpoint on
- *optional* `urlRegex` <[string]> Regex pattern for the URLs of the resources to set breakpoints on. Either `url` or
`urlRegex` must be specified
- *optional* `scriptHash` <[string]> Script hash of the resources to set breakpoint on
- *optional* `columnNumber` <[integer]> Offset in the line to set breakpoint at
- *optional* `condition` <[string]> Expression to use as a breakpoint condition. When specified, debugger will only stop on the
breakpoint if this expression evaluates to true

*returns*
-  `breakpointId` <[Debugger.BreakpointId]> Id of the created breakpoint for further reference
-  `locations` <array of [Debugger.Location]> List of the locations this breakpoint resolved into upon addition

---


#### command: Debugger.setBreakpointsActive

Activates / deactivates all breakpoints on the page.

*parameters*
-  `active` <[boolean]> New value for breakpoints active state

---


#### command: Debugger.setPauseOnExceptions

Defines pause on exceptions state. Can be set to stop on all exceptions, uncaught exceptions or
no exceptions. Initial pause on exceptions state is `none`.

*parameters*
-  `state` <[string]> Pause on exceptions mode

---


#### command: Debugger.setReturnValue 🌱

Changes return value in top frame. Available only at return break position.

*parameters*
-  `newValue` <[Runtime.CallArgument]> New return value

---


#### command: Debugger.setScriptSource

Edits JavaScript source live.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Id of the script to edit
-  `scriptSource` <[string]> New content of the script
- *optional* `dryRun` <[boolean]> If true the change will not actually be applied. Dry run may be used to get result
description without actually modifying the code

*returns*
- *optional* `callFrames` <array of [Debugger.CallFrame]> New stack trace in case editing has happened while VM was stopped
- *optional* `stackChanged` <[boolean]> Whether current call stack  was modified after applying the changes
- *optional* `asyncStackTrace` <[Runtime.StackTrace]> Async stack trace, if any
- *optional* `asyncStackTraceId` <[Runtime.StackTraceId]> 🌱 Async stack trace, if any
- *optional* `exceptionDetails` <[Runtime.ExceptionDetails]> Exception details if any

---


#### command: Debugger.setSkipAllPauses

Makes page not interrupt on any pauses (breakpoint, exception, dom exception etc).

*parameters*
-  `skip` <[boolean]> New value for skip pauses state

---


#### command: Debugger.setVariableValue

Changes value of variable in a callframe. Object-based scopes are not supported and must be
mutated manually.

*parameters*
-  `scopeNumber` <[integer]> 0-based number of scope as was listed in scope chain. Only 'local', 'closure' and 'catch'
scope types are allowed. Other scopes could be manipulated manually
-  `variableName` <[string]> Variable name
-  `newValue` <[Runtime.CallArgument]> New variable value
-  `callFrameId` <[Debugger.CallFrameId]> Id of callframe that holds variable

---


#### command: Debugger.stepInto

Steps into the function call.

*parameters*
- *optional* `breakOnAsyncCall` <[boolean]> 🌱 Debugger will issue additional Debugger.paused notification if any async task is scheduled
before next pause

---


#### command: Debugger.stepOut

Steps out of the function call.

---


#### command: Debugger.stepOver

Steps over the statement.

---


#### event: Debugger.breakpointResolved

Fired when breakpoint is resolved to an actual script and location.

*parameters*
-  `breakpointId` <[Debugger.BreakpointId]> Breakpoint unique identifier
-  `location` <[Debugger.Location]> Actual breakpoint location

---


#### event: Debugger.paused

Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

*parameters*
-  `callFrames` <array of [Debugger.CallFrame]> Call stack the virtual machine stopped on
-  `reason` <[string]> Pause reason
- *optional* `data` <[object]> Object containing break-specific auxiliary properties
- *optional* `hitBreakpoints` <array of [string]> Hit breakpoints IDs
- *optional* `asyncStackTrace` <[Runtime.StackTrace]> Async stack trace, if any
- *optional* `asyncStackTraceId` <[Runtime.StackTraceId]> 🌱 Async stack trace, if any
- *optional* `asyncCallStackTraceId` <[Runtime.StackTraceId]> 🌱 Just scheduled async call will have this stack trace as parent stack during async execution.
This field is available only after `Debugger.stepInto` call with `breakOnAsynCall` flag

---


#### event: Debugger.resumed

Fired when the virtual machine resumed execution.

---


#### event: Debugger.scriptFailedToParse

Fired when virtual machine fails to parse the script.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Identifier of the script parsed
-  `url` <[string]> URL or name of the script parsed (if any)
-  `startLine` <[integer]> Line offset of the script within the resource with given URL (for script tags)
-  `startColumn` <[integer]> Column offset of the script within the resource with given URL
-  `endLine` <[integer]> Last line of the script
-  `endColumn` <[integer]> Length of the last line of the script
-  `executionContextId` <[Runtime.ExecutionContextId]> Specifies script creation context
-  `hash` <[string]> Content hash of the script
- *optional* `executionContextAuxData` <[object]> Embedder-specific auxiliary data
- *optional* `sourceMapURL` <[string]> URL of source map associated with script (if any)
- *optional* `hasSourceURL` <[boolean]> True, if this script has sourceURL
- *optional* `isModule` <[boolean]> True, if this script is ES6 module
- *optional* `length` <[integer]> This script length
- *optional* `stackTrace` <[Runtime.StackTrace]> 🌱 JavaScript top stack frame of where the script parsed event was triggered if available

---


#### event: Debugger.scriptParsed

Fired when virtual machine parses script. This event is also fired for all known and uncollected
scripts upon enabling debugger.

*parameters*
-  `scriptId` <[Runtime.ScriptId]> Identifier of the script parsed
-  `url` <[string]> URL or name of the script parsed (if any)
-  `startLine` <[integer]> Line offset of the script within the resource with given URL (for script tags)
-  `startColumn` <[integer]> Column offset of the script within the resource with given URL
-  `endLine` <[integer]> Last line of the script
-  `endColumn` <[integer]> Length of the last line of the script
-  `executionContextId` <[Runtime.ExecutionContextId]> Specifies script creation context
-  `hash` <[string]> Content hash of the script
- *optional* `executionContextAuxData` <[object]> Embedder-specific auxiliary data
- *optional* `isLiveEdit` <[boolean]> 🌱 True, if this script is generated as a result of the live edit operation
- *optional* `sourceMapURL` <[string]> URL of source map associated with script (if any)
- *optional* `hasSourceURL` <[boolean]> True, if this script has sourceURL
- *optional* `isModule` <[boolean]> True, if this script is ES6 module
- *optional* `length` <[integer]> This script length
- *optional* `stackTrace` <[Runtime.StackTrace]> 🌱 JavaScript top stack frame of where the script parsed event was triggered if available

---


#### type: Debugger.BreakpointId

Breakpoint identifier.

*base type*
- **string**

*accepted by command*
- [Debugger.removeBreakpoint]

*returned from command*
- [Debugger.setBreakpoint]
- [Debugger.setBreakpointByUrl]

*parameter in event*
- [Debugger.breakpointResolved]

---


#### type: Debugger.CallFrameId

Call frame identifier.

*base type*
- **string**

*property of type*
- [Debugger.CallFrame]

*accepted by command*
- [Debugger.evaluateOnCallFrame]
- [Debugger.restartFrame]
- [Debugger.setVariableValue]

---


#### type: Debugger.Location

Location in the source code.

*base type*
- **object**

*properties*
-  `scriptId` <[Runtime.ScriptId]> Script identifier as reported in the `Debugger.scriptParsed`
-  `lineNumber` <[integer]> Line number in the script (0-based)
- *optional* `columnNumber` <[integer]> Column number in the script (0-based)

*property of type*
- [Debugger.CallFrame]
- [Debugger.Scope]

*accepted by command*
- [Debugger.continueToLocation]
- [Debugger.getPossibleBreakpoints]
- [Debugger.setBreakpoint]

*returned from command*
- [Debugger.setBreakpoint]
- [Debugger.setBreakpointByUrl]

*parameter in event*
- [Debugger.breakpointResolved]
- [Profiler.consoleProfileFinished]
- [Profiler.consoleProfileStarted]

---


#### type: Debugger.ScriptPosition

Location in the source code.

*base type*
- **object**

*properties*
-  `lineNumber` <[integer]> 
-  `columnNumber` <[integer]> 

*accepted by command*
- [Debugger.setBlackboxedRanges]

---


#### type: Debugger.CallFrame

JavaScript call frame. Array of call frames form the call stack.

*base type*
- **object**

*properties*
-  `callFrameId` <[Debugger.CallFrameId]> Call frame identifier. This identifier is only valid while the virtual machine is paused
-  `functionName` <[string]> Name of the JavaScript function called on this call frame
- *optional* `functionLocation` <[Debugger.Location]> Location in the source code
-  `location` <[Debugger.Location]> Location in the source code
-  `url` <[string]> JavaScript script name or url
-  `scopeChain` <array of [Debugger.Scope]> Scope chain for this call frame
-  `this` <[Runtime.RemoteObject]> `this` object for this call frame
- *optional* `returnValue` <[Runtime.RemoteObject]> The value being returned, if the function is at return point

*returned from command*
- [Debugger.restartFrame]
- [Debugger.setScriptSource]

*parameter in event*
- [Debugger.paused]

---


#### type: Debugger.Scope

Scope description.

*base type*
- **object**

*properties*
-  `type` <[string]> Scope type
-  `object` <[Runtime.RemoteObject]> Object representing the scope. For `global` and `with` scopes it represents the actual
object; for the rest of the scopes, it is artificial transient object enumerating scope
variables as its properties
- *optional* `name` <[string]> 
- *optional* `startLocation` <[Debugger.Location]> Location in the source code where scope starts
- *optional* `endLocation` <[Debugger.Location]> Location in the source code where scope ends

*property of type*
- [Debugger.CallFrame]

---


#### type: Debugger.SearchMatch

Search match for resource.

*base type*
- **object**

*properties*
-  `lineNumber` <[number]> Line number in resource content
-  `lineContent` <[string]> Line with match content

*returned from command*
- [Debugger.searchInContent]
- [Page.searchInResource]
- [Network.searchInResponseBody]

---


#### type: Debugger.BreakLocation

*base type*
- **object**

*properties*
-  `scriptId` <[Runtime.ScriptId]> Script identifier as reported in the `Debugger.scriptParsed`
-  `lineNumber` <[integer]> Line number in the script (0-based)
- *optional* `columnNumber` <[integer]> Column number in the script (0-based)
- *optional* `type` <[string]> 

*returned from command*
- [Debugger.getPossibleBreakpoints]

[Debugger.removeBreakpoint]: debugger.md#command-debuggerremovebreakpoint "Debugger.removeBreakpoint"
[Debugger.setBreakpoint]: debugger.md#command-debuggersetbreakpoint "Debugger.setBreakpoint"
[Debugger.setBreakpointByUrl]: debugger.md#command-debuggersetbreakpointbyurl "Debugger.setBreakpointByUrl"
[Debugger.breakpointResolved]: debugger.md#event-debuggerbreakpointresolved "Debugger.breakpointResolved"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Debugger.evaluateOnCallFrame]: debugger.md#command-debuggerevaluateoncallframe "Debugger.evaluateOnCallFrame"
[Debugger.restartFrame]: debugger.md#command-debuggerrestartframe "Debugger.restartFrame"
[Debugger.setVariableValue]: debugger.md#command-debuggersetvariablevalue "Debugger.setVariableValue"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Debugger.Scope]: debugger.md#type-debuggerscope "Debugger.Scope"
[Debugger.continueToLocation]: debugger.md#command-debuggercontinuetolocation "Debugger.continueToLocation"
[Debugger.getPossibleBreakpoints]: debugger.md#command-debuggergetpossiblebreakpoints "Debugger.getPossibleBreakpoints"
[Debugger.setBreakpoint]: debugger.md#command-debuggersetbreakpoint "Debugger.setBreakpoint"
[Debugger.setBreakpoint]: debugger.md#command-debuggersetbreakpoint "Debugger.setBreakpoint"
[Debugger.setBreakpointByUrl]: debugger.md#command-debuggersetbreakpointbyurl "Debugger.setBreakpointByUrl"
[Debugger.breakpointResolved]: debugger.md#event-debuggerbreakpointresolved "Debugger.breakpointResolved"
[Profiler.consoleProfileFinished]: profiler.md#event-profilerconsoleprofilefinished "Profiler.consoleProfileFinished"
[Profiler.consoleProfileStarted]: profiler.md#event-profilerconsoleprofilestarted "Profiler.consoleProfileStarted"
[Debugger.setBlackboxedRanges]: debugger.md#command-debuggersetblackboxedranges "Debugger.setBlackboxedRanges"
[Debugger.restartFrame]: debugger.md#command-debuggerrestartframe "Debugger.restartFrame"
[Debugger.setScriptSource]: debugger.md#command-debuggersetscriptsource "Debugger.setScriptSource"
[Debugger.paused]: debugger.md#event-debuggerpaused "Debugger.paused"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Debugger.searchInContent]: debugger.md#command-debuggersearchincontent "Debugger.searchInContent"
[Page.searchInResource]: page.md#command-pagesearchinresource "Page.searchInResource"
[Network.searchInResponseBody]: network.md#command-networksearchinresponsebody "Network.searchInResponseBody"
[Debugger.getPossibleBreakpoints]: debugger.md#command-debuggergetpossiblebreakpoints "Debugger.getPossibleBreakpoints"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Debugger.CallFrameId]: debugger.md#type-debuggercallframeid "Debugger.CallFrameId"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Debugger.Scope]: debugger.md#type-debuggerscope "Debugger.Scope"
[Runtime.RemoteObject]: runtime.md#type-runtimeremoteobject "Runtime.RemoteObject"
[Runtime.RemoteObject]: runtime.md#type-runtimeremoteobject "Runtime.RemoteObject"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Runtime.UniqueDebuggerId]: runtime.md#type-runtimeuniquedebuggerid "Runtime.UniqueDebuggerId"
[Debugger.CallFrameId]: debugger.md#type-debuggercallframeid "Debugger.CallFrameId"
[Runtime.RemoteObject]: runtime.md#type-runtimeremoteobject "Runtime.RemoteObject"
[Runtime.ExceptionDetails]: runtime.md#type-runtimeexceptiondetails "Runtime.ExceptionDetails"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Debugger.BreakLocation]: debugger.md#type-debuggerbreaklocation "Debugger.BreakLocation"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Runtime.StackTraceId]: runtime.md#type-runtimestacktraceid "Runtime.StackTraceId"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[Runtime.StackTraceId]: runtime.md#type-runtimestacktraceid "Runtime.StackTraceId"
[Debugger.BreakpointId]: debugger.md#type-debuggerbreakpointid "Debugger.BreakpointId"
[Debugger.CallFrameId]: debugger.md#type-debuggercallframeid "Debugger.CallFrameId"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[Runtime.StackTraceId]: runtime.md#type-runtimestacktraceid "Runtime.StackTraceId"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Debugger.SearchMatch]: debugger.md#type-debuggersearchmatch "Debugger.SearchMatch"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Debugger.ScriptPosition]: debugger.md#type-debuggerscriptposition "Debugger.ScriptPosition"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Debugger.BreakpointId]: debugger.md#type-debuggerbreakpointid "Debugger.BreakpointId"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Debugger.BreakpointId]: debugger.md#type-debuggerbreakpointid "Debugger.BreakpointId"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Runtime.CallArgument]: runtime.md#type-runtimecallargument "Runtime.CallArgument"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[Runtime.StackTraceId]: runtime.md#type-runtimestacktraceid "Runtime.StackTraceId"
[Runtime.ExceptionDetails]: runtime.md#type-runtimeexceptiondetails "Runtime.ExceptionDetails"
[Runtime.CallArgument]: runtime.md#type-runtimecallargument "Runtime.CallArgument"
[Debugger.CallFrameId]: debugger.md#type-debuggercallframeid "Debugger.CallFrameId"
[Debugger.BreakpointId]: debugger.md#type-debuggerbreakpointid "Debugger.BreakpointId"
[Debugger.Location]: debugger.md#type-debuggerlocation "Debugger.Location"
[Debugger.CallFrame]: debugger.md#type-debuggercallframe "Debugger.CallFrame"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[Runtime.StackTraceId]: runtime.md#type-runtimestacktraceid "Runtime.StackTraceId"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Runtime.ExecutionContextId]: runtime.md#type-runtimeexecutioncontextid "Runtime.ExecutionContextId"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[Runtime.ScriptId]: runtime.md#type-runtimescriptid "Runtime.ScriptId"
[Runtime.ExecutionContextId]: runtime.md#type-runtimeexecutioncontextid "Runtime.ExecutionContextId"
[Runtime.StackTrace]: runtime.md#type-runtimestacktrace "Runtime.StackTrace"
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON boolean"
[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON string"
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON number"
[integer]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON integer"
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON object"
[any]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON any"