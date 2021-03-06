<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.02</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Event</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Event.html">Event</a></h1>

<pre><span class="keyword">module</span> Event: <code class="code"><span class="keyword">sig</span></code> <a href="Event.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
First-class synchronous communication.
<p>

   This module implements synchronous inter-thread communications over
   channels. As in John Reppy's Concurrent ML system, the communication
   events are first-class values: they can be built and combined
   independently before being offered for communication.<br>
</p></div>
<hr width="100%">

<pre><span id="TYPEchannel"><span class="keyword">type</span> <code class="type">'a</code> channel</span> </pre>
<div class="info ">
The type of communication channels carrying values of type <code class="code"><span class="keywordsign">'</span>a</code>.<br>
</div>


<pre><span id="VALnew_channel"><span class="keyword">val</span> new_channel</span> : <code class="type">unit -&gt; 'a <a href="Event.html#TYPEchannel">channel</a></code></pre><div class="info ">
Return a new channel.<br>
</div>

<pre><span id="TYPEevent"><span class="keyword">type</span> <code class="type">+'a</code> event</span> </pre>
<div class="info ">
The type of communication events returning a result of type <code class="code"><span class="keywordsign">'</span>a</code>.<br>
</div>


<pre><span id="VALsend"><span class="keyword">val</span> send</span> : <code class="type">'a <a href="Event.html#TYPEchannel">channel</a> -&gt; 'a -&gt; unit <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">send ch v</code> returns the event consisting in sending the value <code class="code">v</code>
   over the channel <code class="code">ch</code>. The result value of this event is <code class="code">()</code>.<br>
</div>

<pre><span id="VALreceive"><span class="keyword">val</span> receive</span> : <code class="type">'a <a href="Event.html#TYPEchannel">channel</a> -&gt; 'a <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">receive ch</code> returns the event consisting in receiving a value
   from the channel <code class="code">ch</code>. The result value of this event is the
   value received.<br>
</div>

<pre><span id="VALalways"><span class="keyword">val</span> always</span> : <code class="type">'a -&gt; 'a <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">always v</code> returns an event that is always ready for
   synchronization.  The result value of this event is <code class="code">v</code>.<br>
</div>

<pre><span id="VALchoose"><span class="keyword">val</span> choose</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> list -&gt; 'a <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">choose evl</code> returns the event that is the alternative of
   all the events in the list <code class="code">evl</code>.<br>
</div>

<pre><span id="VALwrap"><span class="keyword">val</span> wrap</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> -&gt; ('a -&gt; 'b) -&gt; 'b <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">wrap ev fn</code> returns the event that performs the same communications
   as <code class="code">ev</code>, then applies the post-processing function <code class="code">fn</code>
   on the return value.<br>
</div>

<pre><span id="VALwrap_abort"><span class="keyword">val</span> wrap_abort</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> -&gt; (unit -&gt; unit) -&gt; 'a <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">wrap_abort ev fn</code> returns the event that performs
   the same communications as <code class="code">ev</code>, but if it is not selected
   the function <code class="code">fn</code> is called after the synchronization.<br>
</div>

<pre><span id="VALguard"><span class="keyword">val</span> guard</span> : <code class="type">(unit -&gt; 'a <a href="Event.html#TYPEevent">event</a>) -&gt; 'a <a href="Event.html#TYPEevent">event</a></code></pre><div class="info ">
<code class="code">guard fn</code> returns the event that, when synchronized, computes
   <code class="code">fn()</code> and behaves as the resulting event. This allows to
   compute events with side-effects at the time of the synchronization
   operation.<br>
</div>

<pre><span id="VALsync"><span class="keyword">val</span> sync</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> -&gt; 'a</code></pre><div class="info ">
'Synchronize' on an event: offer all the communication
   possibilities specified in the event to the outside world,
   and block until one of the communications succeed. The result
   value of that communication is returned.<br>
</div>

<pre><span id="VALselect"><span class="keyword">val</span> select</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> list -&gt; 'a</code></pre><div class="info ">
'Synchronize' on an alternative of events.
   <code class="code">select evl</code> is shorthand for <code class="code">sync(choose evl)</code>.<br>
</div>

<pre><span id="VALpoll"><span class="keyword">val</span> poll</span> : <code class="type">'a <a href="Event.html#TYPEevent">event</a> -&gt; 'a option</code></pre><div class="info ">
Non-blocking version of <a href="Event.html#VALsync"><code class="code"><span class="constructor">Event</span>.sync</code></a>: offer all the communication
   possibilities specified in the event to the outside world,
   and if one can take place immediately, perform it and return
   <code class="code"><span class="constructor">Some</span> r</code> where <code class="code">r</code> is the result value of that communication.
   Otherwise, return <code class="code"><span class="constructor">None</span></code> without blocking.<br>
</div>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>