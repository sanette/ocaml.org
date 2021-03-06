<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.07</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">ThreadUnix</a></div><ul><li><a href="#1_Processhandling">Process handling</a></li><li><a href="#1_Basicinputoutput">Basic input/output</a></li><li><a href="#1_Inputoutputwithtimeout">Input/output with timeout</a></li><li><a href="#1_Polling">Polling</a></li><li><a href="#1_Pipesandredirections">Pipes and redirections</a></li><li><a href="#1_Time">Time</a></li><li><a href="#1_Sockets">Sockets</a></li></ul></nav></header>

<h1>Module <a href="type_ThreadUnix.html">ThreadUnix</a></h1>

<pre><span id="MODULEThreadUnix"><span class="keyword">module</span> ThreadUnix</span>: <code class="code"><span class="keyword">sig</span></code> <a href="ThreadUnix.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
<div class="info-deprecated">
<span class="warning">Deprecated.</span>The functionality of this module has been merged back into
   the <a href="Unix.html"><code class="code"><span class="constructor">Unix</span></code></a> module.  Threaded programs can now call the functions
   from module <a href="Unix.html"><code class="code"><span class="constructor">Unix</span></code></a> directly, and still get the correct behavior
   (block the calling thread, if required, but do not block all threads
   in the process).</div>
<div class="info-desc">
<p>Thread-compatible system calls.</p>
</div>
</div>
<hr width="100%">
<h2 id="1_Processhandling">Process handling</h2>
<pre><span id="VALexecv"><span class="keyword">val</span> execv</span> : <code class="type">string -&gt; string array -&gt; unit</code></pre>
<pre><span id="VALexecve"><span class="keyword">val</span> execve</span> : <code class="type">string -&gt; string array -&gt; string array -&gt; unit</code></pre>
<pre><span id="VALexecvp"><span class="keyword">val</span> execvp</span> : <code class="type">string -&gt; string array -&gt; unit</code></pre>
<pre><span id="VALwait"><span class="keyword">val</span> wait</span> : <code class="type">unit -&gt; int * <a href="Unix.html#TYPEprocess_status">Unix.process_status</a></code></pre>
<pre><span id="VALwaitpid"><span class="keyword">val</span> waitpid</span> : <code class="type"><a href="Unix.html#TYPEwait_flag">Unix.wait_flag</a> list -&gt; int -&gt; int * <a href="Unix.html#TYPEprocess_status">Unix.process_status</a></code></pre>
<pre><span id="VALsystem"><span class="keyword">val</span> system</span> : <code class="type">string -&gt; <a href="Unix.html#TYPEprocess_status">Unix.process_status</a></code></pre><h2 id="1_Basicinputoutput">Basic input/output</h2>
<pre><span id="VALread"><span class="keyword">val</span> read</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; int</code></pre>
<pre><span id="VALwrite"><span class="keyword">val</span> write</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; int</code></pre>
<pre><span id="VALsingle_write"><span class="keyword">val</span> single_write</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; int</code></pre>
<pre><span id="VALwrite_substring"><span class="keyword">val</span> write_substring</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; string -&gt; int -&gt; int -&gt; int</code></pre>
<pre><span id="VALsingle_write_substring"><span class="keyword">val</span> single_write_substring</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; string -&gt; int -&gt; int -&gt; int</code></pre><h2 id="1_Inputoutputwithtimeout">Input/output with timeout</h2>
<pre><span id="VALtimed_read"><span class="keyword">val</span> timed_read</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; float -&gt; int</code></pre><div class="info ">
<div class="info-desc">
<p>See <a href="ThreadUnix.html#VALtimed_write"><code class="code"><span class="constructor">ThreadUnix</span>.timed_write</code></a>.</p>
</div>
</div>

<pre><span id="VALtimed_write"><span class="keyword">val</span> timed_write</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; float -&gt; int</code></pre><div class="info ">
<div class="info-desc">
<p>Behave as <a href="ThreadUnix.html#VALread"><code class="code"><span class="constructor">ThreadUnix</span>.read</code></a> and <a href="ThreadUnix.html#VALwrite"><code class="code"><span class="constructor">ThreadUnix</span>.write</code></a>, except that
   <code class="code"><span class="constructor">Unix_error</span>(<span class="constructor">ETIMEDOUT</span>,_,_)</code> is raised if no data is
   available for reading or ready for writing after <code class="code">d</code> seconds.
   The delay <code class="code">d</code> is given in the fifth argument, in seconds.</p>
</div>
</div>

<pre><span id="VALtimed_write_substring"><span class="keyword">val</span> timed_write_substring</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; string -&gt; int -&gt; int -&gt; float -&gt; int</code></pre><div class="info ">
<div class="info-desc">
<p>See <a href="ThreadUnix.html#VALtimed_write"><code class="code"><span class="constructor">ThreadUnix</span>.timed_write</code></a>.</p>
</div>
</div>
<h2 id="1_Polling">Polling</h2>
<pre><span id="VALselect"><span class="keyword">val</span> select</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list -&gt;<br>       float -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> list</code></pre><h2 id="1_Pipesandredirections">Pipes and redirections</h2>
<pre><span id="VALpipe"><span class="keyword">val</span> pipe</span> : <code class="type">?cloexec:bool -&gt; unit -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a></code></pre>
<pre><span id="VALopen_process_in"><span class="keyword">val</span> open_process_in</span> : <code class="type">string -&gt; <a href="Pervasives.html#TYPEin_channel">in_channel</a></code></pre>
<pre><span id="VALopen_process_out"><span class="keyword">val</span> open_process_out</span> : <code class="type">string -&gt; <a href="Pervasives.html#TYPEout_channel">out_channel</a></code></pre>
<pre><span id="VALopen_process"><span class="keyword">val</span> open_process</span> : <code class="type">string -&gt; <a href="Pervasives.html#TYPEin_channel">in_channel</a> * <a href="Pervasives.html#TYPEout_channel">out_channel</a></code></pre>
<pre><span id="VALopen_process_full"><span class="keyword">val</span> open_process_full</span> : <code class="type">string -&gt;<br>       string array -&gt;<br>       <a href="Pervasives.html#TYPEin_channel">in_channel</a> * <a href="Pervasives.html#TYPEout_channel">out_channel</a> * <a href="Pervasives.html#TYPEin_channel">in_channel</a></code></pre><h2 id="1_Time">Time</h2>
<pre><span id="VALsleep"><span class="keyword">val</span> sleep</span> : <code class="type">int -&gt; unit</code></pre><h2 id="1_Sockets">Sockets</h2>
<pre><span id="VALsocket"><span class="keyword">val</span> socket</span> : <code class="type">?cloexec:bool -&gt;<br>       <a href="Unix.html#TYPEsocket_domain">Unix.socket_domain</a> -&gt; <a href="Unix.html#TYPEsocket_type">Unix.socket_type</a> -&gt; int -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a></code></pre>
<pre><span id="VALsocketpair"><span class="keyword">val</span> socketpair</span> : <code class="type">?cloexec:bool -&gt;<br>       <a href="Unix.html#TYPEsocket_domain">Unix.socket_domain</a> -&gt;<br>       <a href="Unix.html#TYPEsocket_type">Unix.socket_type</a> -&gt; int -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> * <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a></code></pre>
<pre><span id="VALaccept"><span class="keyword">val</span> accept</span> : <code class="type">?cloexec:bool -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; <a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> * <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a></code></pre>
<pre><span id="VALconnect"><span class="keyword">val</span> connect</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a> -&gt; unit</code></pre>
<pre><span id="VALrecv"><span class="keyword">val</span> recv</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; int</code></pre>
<pre><span id="VALrecvfrom"><span class="keyword">val</span> recvfrom</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt;<br>       bytes -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; int * <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a></code></pre>
<pre><span id="VALsend"><span class="keyword">val</span> send</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; bytes -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; int</code></pre>
<pre><span id="VALsend_substring"><span class="keyword">val</span> send_substring</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; string -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; int</code></pre>
<pre><span id="VALsendto"><span class="keyword">val</span> sendto</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt;<br>       bytes -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a> -&gt; int</code></pre>
<pre><span id="VALsendto_substring"><span class="keyword">val</span> sendto_substring</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt;<br>       string -&gt; int -&gt; int -&gt; <a href="Unix.html#TYPEmsg_flag">Unix.msg_flag</a> list -&gt; <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a> -&gt; int</code></pre>
<pre><span id="VALopen_connection"><span class="keyword">val</span> open_connection</span> : <code class="type"><a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a> -&gt; <a href="Pervasives.html#TYPEin_channel">in_channel</a> * <a href="Pervasives.html#TYPEout_channel">out_channel</a></code></pre>
<pre><span id="VALestablish_server"><span class="keyword">val</span> establish_server</span> : <code class="type">(<a href="Pervasives.html#TYPEin_channel">in_channel</a> -&gt; <a href="Pervasives.html#TYPEout_channel">out_channel</a> -&gt; unit) -&gt;<br>       <a href="Unix.html#TYPEsockaddr">Unix.sockaddr</a> -&gt; unit</code></pre>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>