<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.09</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">CamlinternalMenhirLib.PackedIntArray</a></div><ul></ul></nav></header>

<h1>Module <a href="type_CamlinternalMenhirLib.PackedIntArray.html">CamlinternalMenhirLib.PackedIntArray</a></h1>

<pre><span id="MODULEPackedIntArray"><span class="keyword">module</span> PackedIntArray</span>: <code class="code"><span class="keyword">sig</span></code> <a href="CamlinternalMenhirLib.PackedIntArray.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><hr width="100%">

<pre><span id="TYPEt"><span class="keyword">type</span> <code class="type"></code>t</span> = <code class="type">int * string</code> </pre>


<pre><span id="VALpack"><span class="keyword">val</span> pack</span> : <code class="type">int array -&gt; <a href="CamlinternalMenhirLib.PackedIntArray.html#TYPEt">t</a></code></pre>
<pre><span id="VALget"><span class="keyword">val</span> get</span> : <code class="type"><a href="CamlinternalMenhirLib.PackedIntArray.html#TYPEt">t</a> -&gt; int -&gt; int</code></pre>
<pre><span id="VALget1"><span class="keyword">val</span> get1</span> : <code class="type">string -&gt; int -&gt; int</code></pre>
<pre><span id="VALunflatten1"><span class="keyword">val</span> unflatten1</span> : <code class="type">int * string -&gt; int -&gt; int -&gt; int</code></pre>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>