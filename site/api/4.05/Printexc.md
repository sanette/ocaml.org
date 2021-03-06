<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.05</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Printexc</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Printexc.html">Printexc</a></h1>

<pre><span class="keyword">module</span> Printexc: <code class="code"><span class="keyword">sig</span></code> <a href="Printexc.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
Facilities for printing exceptions and inspecting current call stack.<br>
</div>
<hr width="100%">

<pre><span id="VALto_string"><span class="keyword">val</span> to_string</span> : <code class="type">exn -&gt; string</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.to_string&nbsp;e</code> returns a string representation of
   the exception <code class="code">e</code>.<br>
</div>

<pre><span id="VALprint"><span class="keyword">val</span> print</span> : <code class="type">('a -&gt; 'b) -&gt; 'a -&gt; 'b</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.print&nbsp;fn&nbsp;x</code> applies <code class="code">fn</code> to <code class="code">x</code> and returns the result.
   If the evaluation of <code class="code">fn&nbsp;x</code> raises any exception, the
   name of the exception is printed on standard error output,
   and the exception is raised again.
   The typical use is to catch and report exceptions that
   escape a function application.<br>
</div>

<pre><span id="VALcatch"><span class="keyword">val</span> catch</span> : <code class="type">('a -&gt; 'b) -&gt; 'a -&gt; 'b</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.catch&nbsp;fn&nbsp;x</code> is similar to <a href="Printexc.html#VALprint"><code class="code"><span class="constructor">Printexc</span>.print</code></a>, but
   aborts the program with exit code 2 after printing the
   uncaught exception.  This function is deprecated: the runtime
   system is now able to print uncaught exceptions as precisely
   as <code class="code"><span class="constructor">Printexc</span>.catch</code> does.  Moreover, calling <code class="code"><span class="constructor">Printexc</span>.catch</code>
   makes it harder to track the location of the exception
   using the debugger or the stack backtrace facility.
   So, do not use <code class="code"><span class="constructor">Printexc</span>.catch</code> in new code.<br>
</div>

<pre><span id="VALprint_backtrace"><span class="keyword">val</span> print_backtrace</span> : <code class="type"><a href="Pervasives.html#TYPEout_channel">out_channel</a> -&gt; unit</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.print_backtrace&nbsp;oc</code> prints an exception backtrace
    on the output channel <code class="code">oc</code>.  The backtrace lists the program
    locations where the most-recently raised exception was raised
    and where it was propagated through function calls.
<p>

    If the call is not inside an exception handler, the returned
    backtrace is unspecified. If the call is after some
    exception-catching code (before in the handler, or in a when-guard
    during the matching of the exception handler), the backtrace may
    correspond to a later exception than the handled one.<br>
<b>Since</b> 3.11.0<br>
</p></div>

<pre><span id="VALget_backtrace"><span class="keyword">val</span> get_backtrace</span> : <code class="type">unit -&gt; string</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.get_backtrace&nbsp;()</code> returns a string containing the
    same exception backtrace that <code class="code"><span class="constructor">Printexc</span>.print_backtrace</code> would
    print. Same restriction usage than <a href="Printexc.html#VALprint_backtrace"><code class="code"><span class="constructor">Printexc</span>.print_backtrace</code></a>.<br>
<b>Since</b> 3.11.0<br>
</div>

<pre><span id="VALrecord_backtrace"><span class="keyword">val</span> record_backtrace</span> : <code class="type">bool -&gt; unit</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.record_backtrace&nbsp;b</code> turns recording of exception backtraces
    on (if <code class="code">b&nbsp;=&nbsp;<span class="keyword">true</span></code>) or off (if <code class="code">b&nbsp;=&nbsp;<span class="keyword">false</span></code>).  Initially, backtraces
    are not recorded, unless the <code class="code">b</code> flag is given to the program
    through the <code class="code"><span class="constructor">OCAMLRUNPARAM</span></code> variable.<br>
<b>Since</b> 3.11.0<br>
</div>

<pre><span id="VALbacktrace_status"><span class="keyword">val</span> backtrace_status</span> : <code class="type">unit -&gt; bool</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.backtrace_status()</code> returns <code class="code"><span class="keyword">true</span></code> if exception
    backtraces are currently recorded, <code class="code"><span class="keyword">false</span></code> if not.<br>
<b>Since</b> 3.11.0<br>
</div>

<pre><span id="VALregister_printer"><span class="keyword">val</span> register_printer</span> : <code class="type">(exn -&gt; string option) -&gt; unit</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.register_printer&nbsp;fn</code> registers <code class="code">fn</code> as an exception
    printer.  The printer should return <code class="code"><span class="constructor">None</span></code> or raise an exception
    if it does not know how to convert the passed exception, and <code class="code"><span class="constructor">Some</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;s</code> with <code class="code">s</code> the resulting string if it can convert the passed
    exception. Exceptions raised by the printer are ignored.
<p>

    When converting an exception into a string, the printers will be invoked
    in the reverse order of their registrations, until a printer returns
    a <code class="code"><span class="constructor">Some</span>&nbsp;s</code> value (if no such printer exists, the runtime will use a
    generic printer).
</p><p>

    When using this mechanism, one should be aware that an exception backtrace
    is attached to the thread that saw it raised, rather than to the exception
    itself. Practically, it means that the code related to <code class="code">fn</code> should not use
    the backtrace if it has itself raised an exception before.<br>
<b>Since</b> 3.11.2<br>
</p></div>
<br>
<h6 id="6_Rawbacktraces">Raw backtraces</h6><br>

<pre><span id="TYPEraw_backtrace"><span class="keyword">type</span> <code class="type"></code>raw_backtrace</span> </pre>
<div class="info ">
The abstract type <code class="code">raw_backtrace</code> stores a backtrace in
    a low-level format, instead of directly exposing them as string as
    the <code class="code">get_backtrace()</code> function does.
<p>

    This allows delaying the formatting of backtraces to when they are
    actually printed, which may be useful if you record more
    backtraces than you print.
</p><p>

    Raw backtraces cannot be marshalled. If you need marshalling, you
    should use the array returned by the <code class="code">backtrace_slots</code> function of
    the next section.<br>
<b>Since</b> 4.01.0<br>
</p></div>


<pre><span id="VALget_raw_backtrace"><span class="keyword">val</span> get_raw_backtrace</span> : <code class="type">unit -&gt; <a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a></code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.get_raw_backtrace&nbsp;()</code> returns the same exception
    backtrace that <code class="code"><span class="constructor">Printexc</span>.print_backtrace</code> would print, but in
    a raw format. Same restriction usage than <a href="Printexc.html#VALprint_backtrace"><code class="code"><span class="constructor">Printexc</span>.print_backtrace</code></a>.<br>
<b>Since</b> 4.01.0<br>
</div>

<pre><span id="VALprint_raw_backtrace"><span class="keyword">val</span> print_raw_backtrace</span> : <code class="type"><a href="Pervasives.html#TYPEout_channel">out_channel</a> -&gt; <a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; unit</code></pre><div class="info ">
Print a raw backtrace in the same format
    <code class="code"><span class="constructor">Printexc</span>.print_backtrace</code> uses.<br>
<b>Since</b> 4.01.0<br>
</div>

<pre><span id="VALraw_backtrace_to_string"><span class="keyword">val</span> raw_backtrace_to_string</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; string</code></pre><div class="info ">
Return a string from a raw backtrace, in the same format
    <code class="code"><span class="constructor">Printexc</span>.get_backtrace</code> uses.<br>
<b>Since</b> 4.01.0<br>
</div>

<pre><span id="VALraise_with_backtrace"><span class="keyword">val</span> raise_with_backtrace</span> : <code class="type">exn -&gt; <a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; 'a</code></pre><div class="info ">
Reraise the exception using the given raw_backtrace for the
    origin of the exception<br>
<b>Since</b> 4.05.0<br>
</div>
<br>
<h6 id="6_Currentcallstack">Current call stack</h6><br>

<pre><span id="VALget_callstack"><span class="keyword">val</span> get_callstack</span> : <code class="type">int -&gt; <a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a></code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.get_callstack&nbsp;n</code> returns a description of the top of the
    call stack on the current program point (for the current thread),
    with at most <code class="code">n</code> entries.  (Note: this function is not related to
    exceptions at all, despite being part of the <code class="code"><span class="constructor">Printexc</span></code> module.)<br>
<b>Since</b> 4.01.0<br>
</div>
<br>
<h6 id="6_Uncaughtexceptions">Uncaught exceptions</h6><br>

<pre><span id="VALset_uncaught_exception_handler"><span class="keyword">val</span> set_uncaught_exception_handler</span> : <code class="type">(exn -&gt; <a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; unit) -&gt; unit</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.set_uncaught_exception_handler&nbsp;fn</code> registers <code class="code">fn</code> as the handler
    for uncaught exceptions. The default handler prints the exception and
    backtrace on standard error output.
<p>

    Note that when <code class="code">fn</code> is called all the functions registered with
    <a href="Pervasives.html#VALat_exit"><code class="code">at_exit</code></a> have already been called. Because of this you must
    make sure any output channel <code class="code">fn</code> writes on is flushed.
</p><p>

    Also note that exceptions raised by user code in the interactive toplevel
    are not passed to this function as they are caught by the toplevel itself.
</p><p>

    If <code class="code">fn</code> raises an exception, both the exceptions passed to <code class="code">fn</code> and raised
    by <code class="code">fn</code> will be printed with their respective backtrace.<br>
<b>Since</b> 4.02.0<br>
</p></div>
<br>
<h6 id="6_Manipulationofbacktraceinformation">Manipulation of backtrace information</h6>
<p>

    These functions are used to traverse the slots of a raw backtrace
    and extract information from them in a programmer-friendly format.<br>

</p><pre><span id="TYPEbacktrace_slot"><span class="keyword">type</span> <code class="type"></code>backtrace_slot</span> </pre>
<div class="info ">
The abstract type <code class="code">backtrace_slot</code> represents a single slot of
    a backtrace.<br>
<b>Since</b> 4.02<br>
</div>


<pre><span id="VALbacktrace_slots"><span class="keyword">val</span> backtrace_slots</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; <a href="Printexc.html#TYPEbacktrace_slot">backtrace_slot</a> array option</code></pre><div class="info ">
Returns the slots of a raw backtrace, or <code class="code"><span class="constructor">None</span></code> if none of them
    contain useful information.
<p>

    In the return array, the slot at index <code class="code">0</code> corresponds to the most
    recent function call, raise, or primitive <code class="code">get_backtrace</code> call in
    the trace.
</p><p>

    Some possible reasons for returning <code class="code"><span class="constructor">None</span></code> are as follow:</p><ul>
<li>none of the slots in the trace come from modules compiled with
    debug information (<code class="code">-g</code>)</li>
<li>the program is a bytecode program that has not been linked with
    debug information enabled (<code class="code">ocamlc&nbsp;-g</code>)</li>
</ul>
<br>
<b>Since</b> 4.02.0<br>
</div>

<pre><code><span id="TYPElocation"><span class="keyword">type</span> <code class="type"></code>location</span> = {</code></pre><table class="typetable">
<tbody><tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTlocation.filename">filename</span>&nbsp;: <code class="type">string</code>;</code></td>

</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTlocation.line_number">line_number</span>&nbsp;: <code class="type">int</code>;</code></td>

</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTlocation.start_char">start_char</span>&nbsp;: <code class="type">int</code>;</code></td>

</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTlocation.end_char">end_char</span>&nbsp;: <code class="type">int</code>;</code></td>

</tr></tbody></table>
}

<div class="info ">
The type of location information found in backtraces. <code class="code">start_char</code>
    and <code class="code">end_char</code> are positions relative to the beginning of the
    line.<br>
<b>Since</b> 4.02<br>
</div>


<pre><span class="keyword">module</span> <a href="Printexc.Slot.html">Slot</a>: <code class="code"><span class="keyword">sig</span></code> <a href="Printexc.Slot.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info">
</div>
<br>
<h6 id="6_Rawbacktraceslots">Raw backtrace slots</h6><br>

<pre><span id="TYPEraw_backtrace_slot"><span class="keyword">type</span> <code class="type"></code>raw_backtrace_slot</span> </pre>
<div class="info ">
This type allows direct access to raw backtrace slots, without any
    conversion in an OCaml-usable data-structure. Being
    process-specific, they must absolutely not be marshalled, and are
    unsafe to use for this reason (marshalling them may not fail, but
    un-marshalling and using the result will result in
    undefined behavior).
<p>

    Elements of this type can still be compared and hashed: when two
    elements are equal, then they represent the same source location
    (the converse is not necessarily true in presence of inlining,
    for example).<br>
<b>Since</b> 4.02.0<br>
</p></div>


<pre><span id="VALraw_backtrace_length"><span class="keyword">val</span> raw_backtrace_length</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; int</code></pre><div class="info ">
<code class="code">raw_backtrace_length&nbsp;bckt</code> returns the number of slots in the
    backtrace <code class="code">bckt</code>.<br>
<b>Since</b> 4.02<br>
</div>

<pre><span id="VALget_raw_backtrace_slot"><span class="keyword">val</span> get_raw_backtrace_slot</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> -&gt; int -&gt; <a href="Printexc.html#TYPEraw_backtrace_slot">raw_backtrace_slot</a></code></pre><div class="info ">
<code class="code">get_raw_backtrace_slot&nbsp;bckt&nbsp;pos</code> returns the slot in position <code class="code">pos</code> in the
    backtrace <code class="code">bckt</code>.<br>
<b>Since</b> 4.02<br>
</div>

<pre><span id="VALconvert_raw_backtrace_slot"><span class="keyword">val</span> convert_raw_backtrace_slot</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace_slot">raw_backtrace_slot</a> -&gt; <a href="Printexc.html#TYPEbacktrace_slot">backtrace_slot</a></code></pre><div class="info ">
Extracts the user-friendly <code class="code">backtrace_slot</code> from a low-level
    <code class="code">raw_backtrace_slot</code>.<br>
<b>Since</b> 4.02<br>
</div>

<pre><span id="VALget_raw_backtrace_next_slot"><span class="keyword">val</span> get_raw_backtrace_next_slot</span> : <code class="type"><a href="Printexc.html#TYPEraw_backtrace_slot">raw_backtrace_slot</a> -&gt; <a href="Printexc.html#TYPEraw_backtrace_slot">raw_backtrace_slot</a> option</code></pre><div class="info ">
<code class="code">get_raw_backtrace_next_slot&nbsp;slot</code> returns the next slot inlined, if any.
<p>

    Sample code to iterate over all frames (inlined and non-inlined):
    </p><pre class="codepre"><code class="code">      <span class="comment">(* Iterate over inlined frames *)</span>
      <span class="keyword">let</span> <span class="keyword">rec</span> iter_raw_backtrace_slot f slot =
        f slot;
        <span class="keyword">match</span> get_raw_backtrace_next_slot slot <span class="keyword">with</span>
        <span class="keywordsign">|</span> <span class="constructor">None</span> <span class="keywordsign">-&gt;</span> ()
        <span class="keywordsign">|</span> <span class="constructor">Some</span> slot' <span class="keywordsign">-&gt;</span> iter_raw_backtrace_slot f slot'

      <span class="comment">(* Iterate over stack frames *)</span>
      <span class="keyword">let</span> iter_raw_backtrace f bt =
        <span class="keyword">for</span> i = 0 <span class="keyword">to</span> raw_backtrace_length bt - 1 <span class="keyword">do</span>
          iter_raw_backtrace_slot f (get_raw_backtrace_slot bt i)
        <span class="keyword">done</span>
    </code></pre><br>
<b>Since</b> 4.04.0<br>
</div>
<br>
<h6 id="6_Exceptionslots">Exception slots</h6><br>

<pre><span id="VALexn_slot_id"><span class="keyword">val</span> exn_slot_id</span> : <code class="type">exn -&gt; int</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.exn_slot_id</code> returns an integer which uniquely identifies
    the constructor used to create the exception value <code class="code">exn</code>
    (in the current runtime).<br>
<b>Since</b> 4.02.0<br>
</div>

<pre><span id="VALexn_slot_name"><span class="keyword">val</span> exn_slot_name</span> : <code class="type">exn -&gt; string</code></pre><div class="info ">
<code class="code"><span class="constructor">Printexc</span>.exn_slot_name&nbsp;exn</code> returns the internal name of the constructor
    used to create the exception value <code class="code">exn</code>.<br>
<b>Since</b> 4.02.0<br>
</div>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>