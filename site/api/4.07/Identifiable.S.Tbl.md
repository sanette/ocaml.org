<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.07</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Identifiable.S.Tbl</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Identifiable.S.Tbl.html">Identifiable.S.Tbl</a></h1>

<pre><span id="MODULETbl"><span class="keyword">module</span> Tbl</span>: <code class="type"><a href="Identifiable.Tbl.html">Identifiable.Tbl</a></code><code class="type">  with module T := T</code></pre><hr width="100%">

<pre><span id="MODULET"><span class="keyword">module</span> <a href="Identifiable.Tbl.T.html">T</a></span>: <code class="code"><span class="keyword">sig</span></code> <a href="Identifiable.Tbl.T.html">..</a> <code class="code"><span class="keyword">end</span></code></pre>
<pre><span class="keyword">include</span> <a href="Hashtbl.S.html">Hashtbl.S</a></pre>

<pre><span id="VALto_list"><span class="keyword">val</span> to_list</span> : <code class="type">'a t -&gt; (<a href="Identifiable.Tbl.T.html#TYPEt">T.t</a> * 'a) list</code></pre>
<pre><span id="VALof_list"><span class="keyword">val</span> of_list</span> : <code class="type">(<a href="Identifiable.Tbl.T.html#TYPEt">T.t</a> * 'a) list -&gt; 'a t</code></pre>
<pre><span id="VALto_map"><span class="keyword">val</span> to_map</span> : <code class="type">'a t -&gt; 'a Map.Make(T).t</code></pre>
<pre><span id="VALof_map"><span class="keyword">val</span> of_map</span> : <code class="type">'a Map.Make(T).t -&gt; 'a t</code></pre>
<pre><span id="VALmemoize"><span class="keyword">val</span> memoize</span> : <code class="type">'a t -&gt; (key -&gt; 'a) -&gt; key -&gt; 'a</code></pre>
<pre><span id="VALmap"><span class="keyword">val</span> map</span> : <code class="type">'a t -&gt; ('a -&gt; 'b) -&gt; 'b t</code></pre>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>