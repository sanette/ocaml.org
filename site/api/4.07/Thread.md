<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.07</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Thread</a></div><ul><li><a href="#1_Threadcreationandtermination">Thread creation and termination</a></li><li><a href="#1_Suspendingthreads">Suspending threads</a></li></ul></nav></header>

<h1>Module <a href="type_Thread.html">Thread</a></h1>

<pre><span id="MODULEThread"><span class="keyword">module</span> Thread</span>: <code class="code"><span class="keyword">sig</span></code> <a href="Thread.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
<div class="info-desc">
<p>Lightweight threads.</p>
</div>
</div>
<hr width="100%">

<pre><span id="TYPEt"><span class="keyword">type</span> <code class="type"></code>t</span> </pre>
<div class="info ">
<div class="info-desc">
<p>The type of thread handles.</p>
</div>
</div>

<h2 id="1_Threadcreationandtermination">Thread creation and termination</h2>
<pre><span id="VALcreate"><span class="keyword">val</span> create</span> : <code class="type">('a -&gt; 'b) -&gt; 'a -&gt; <a href="Thread.html#TYPEt">t</a></code></pre><div class="info ">
<div class="info-desc">
<p><code class="code"><span class="constructor">Thread</span>.create&nbsp;funct&nbsp;arg</code> creates a new thread of control,
   in which the function application <code class="code">funct&nbsp;arg</code>
   is executed concurrently with the other threads of the program.
   The application of <code class="code"><span class="constructor">Thread</span>.create</code>
   returns the handle of the newly created thread.
   The new thread terminates when the application <code class="code">funct&nbsp;arg</code>
   returns, either normally or by raising an uncaught exception.
   In the latter case, the exception is printed on standard error,
   but not propagated back to the parent thread. Similarly, the
   result of the application <code class="code">funct&nbsp;arg</code> is discarded and not
   directly accessible to the parent thread.</p>
</div>
</div>

<pre><span id="VALself"><span class="keyword">val</span> self</span> : <code class="type">unit -&gt; <a href="Thread.html#TYPEt">t</a></code></pre><div class="info ">
<div class="info-desc">
<p>Return the thread currently executing.</p>
</div>
</div>

<pre><span id="VALid"><span class="keyword">val</span> id</span> : <code class="type"><a href="Thread.html#TYPEt">t</a> -&gt; int</code></pre><div class="info ">
<div class="info-desc">
<p>Return the identifier of the given thread. A thread identifier
   is an integer that identifies uniquely the thread.
   It can be used to build data structures indexed by threads.</p>
</div>
</div>

<pre><span id="VALexit"><span class="keyword">val</span> exit</span> : <code class="type">unit -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p>Terminate prematurely the currently executing thread.</p>
</div>
</div>

<pre><span id="VALkill"><span class="keyword">val</span> kill</span> : <code class="type"><a href="Thread.html#TYPEt">t</a> -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p>Terminate prematurely the thread whose handle is given.
   This functionality is available only with bytecode-level threads.</p>
</div>
</div>
<h2 id="1_Suspendingthreads">Suspending threads</h2>
<pre><span id="VALdelay"><span class="keyword">val</span> delay</span> : <code class="type">float -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p><code class="code">delay&nbsp;d</code> suspends the execution of the calling thread for
   <code class="code">d</code> seconds. The other program threads continue to run during
   this time.</p>
</div>
</div>

<pre><span id="VALjoin"><span class="keyword">val</span> join</span> : <code class="type"><a href="Thread.html#TYPEt">t</a> -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p><code class="code">join&nbsp;th</code> suspends the execution of the calling thread
   until the thread <code class="code">th</code> has terminated.</p>
</div>
</div>

<pre><span id="VALwait_read"><span class="keyword">val</span> wait_read</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p>See <a href="Thread.html#VALwait_write"><code class="code"><span class="constructor">Thread</span>.wait_write</code></a>.</p>
</div>
</div>

<pre><span id="VALwait_write"><span class="keyword">val</span> wait_write</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p>Suspend the execution of the calling thread until at least
   one character or EOF is available for reading (<a href="Thread.html#VALwait_read"><code class="code"><span class="constructor">Thread</span>.wait_read</code></a>) or
   one character can be written without blocking (<code class="code">wait_write</code>)
   on the given Unix file descriptor.</p>
</div>
</div>

<pre><span id="VALwait_timed_read"><span class="keyword">val</span> wait_timed_read</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; float -&gt; bool</code></pre><div class="info ">
<div class="info-desc">
<p>See <a href="Thread.html#VALwait_timed_write"><code class="code"><span class="constructor">Thread</span>.wait_timed_write</code></a>.</p>
</div>
</div>

<pre><span id="VALwait_timed_write"><span class="keyword">val</span> wait_timed_write</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; float -&gt; bool</code></pre><div class="info ">
<div class="info-desc">
<p>Same as <a href="Thread.html#VALwait_read"><code class="code"><span class="constructor">Thread</span>.wait_read</code></a> and <a href="Thread.html#VALwait_write"><code class="code"><span class="constructor">Thread</span>.wait_write</code></a>, but wait for at most
   the amount of time given as second argument (in seconds).
   Return <code class="code"><span class="keyword">true</span></code> if the file descriptor is ready for input/output
   and <code class="code"><span class="keyword">false</span></code> if the timeout expired.</p>
</div>
</div>

<pre><span id="VALselect"><span class="keyword">val</span> select</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       float -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list</code></pre><div class="info ">
<div class="info-desc">
<p>Suspend the execution of the calling thread until input/output
   becomes possible on the given Unix file descriptors.
   The arguments and results have the same meaning as for
   <a href="Unix.html#VALselect"><code class="code"><span class="constructor">Unix</span>.select</code></a>.</p>
</div>
</div>

<pre><span id="VALwait_pid"><span class="keyword">val</span> wait_pid</span> : <code class="type">int -&gt; int * <a href="Unix.html#TYPEprocess_status">Unix.process_status</a></code></pre><div class="info ">
<div class="info-desc">
<p><code class="code">wait_pid&nbsp;p</code> suspends the execution of the calling thread
   until the Unix process specified by the process identifier <code class="code">p</code>
   terminates. A pid <code class="code">p</code> of <code class="code">-1</code> means wait for any child.
   A pid of <code class="code">0</code> means wait for any child in the same process group
   as the current process. Negative pid arguments represent
   process groups. Returns the pid of the child caught and
   its termination status, as per <a href="Unix.html#VALwait"><code class="code"><span class="constructor">Unix</span>.wait</code></a>.</p>
</div>
</div>

<pre><span id="VALwait_signal"><span class="keyword">val</span> wait_signal</span> : <code class="type">int list -&gt; int</code></pre><div class="info ">
<div class="info-desc">
<p><code class="code">wait_signal&nbsp;sigs</code> suspends the execution of the calling thread
   until the process receives one of the signals specified in the
   list <code class="code">sigs</code>.  It then returns the number of the signal received.
   Signal handlers attached to the signals in <code class="code">sigs</code> will not
   be invoked.  Do not call <code class="code">wait_signal</code> concurrently
   from several threads on the same signals.</p>
</div>
</div>

<pre><span id="VALyield"><span class="keyword">val</span> yield</span> : <code class="type">unit -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p>Re-schedule the calling thread without suspending it.
   This function can be used to give scheduling hints,
   telling the scheduler that now is a good time to
   switch to other threads.</p>
</div>
</div>

<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>