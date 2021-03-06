<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.08</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Spacetime.Snapshot</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Spacetime.Snapshot.html">Spacetime.Snapshot</a></h1>

<pre><span id="MODULESnapshot"><span class="keyword">module</span> Snapshot</span>: <code class="code"><span class="keyword">sig</span></code> <a href="Spacetime.Snapshot.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><hr width="100%">

<pre><span id="VALtake"><span class="keyword">val</span> take</span> : <code class="type">?time:float -&gt; <a href="Spacetime.Series.html#TYPEt">Spacetime.Series.t</a> -&gt; unit</code></pre><div class="info ">
<div class="info-desc">
<p><code class="code">take&nbsp;series</code> takes a snapshot of the profiling annotations on the values
      in the minor and major heaps, together with GC stats, and write the
      result to the <code class="code">series</code> file.  This function triggers a minor GC but does
      not allocate any memory itself.
      If the optional <code class="code">time</code> is specified, it will be used instead of the
      result of <a href="Sys.html#VALtime"><code class="code"><span class="constructor">Sys</span>.time</code></a> as the timestamp of the snapshot.  Such <code class="code">time</code>s
      should start from zero and be monotonically increasing.  This parameter
      is intended to be used so that snapshots can be correlated against wall
      clock time (which is not supported in the standard library) rather than
      elapsed CPU time.</p>
</div>
</div>

<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>