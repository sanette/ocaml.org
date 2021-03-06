<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.01</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">StdLabels.String</a></div><ul></ul></nav></header>

<h1>Module <a href="type_StdLabels.String.html">StdLabels.String</a></h1>

<pre><span class="keyword">module</span> String: <code class="code"><span class="keyword">sig</span></code> <a href="StdLabels.String.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><hr width="100%">

<pre><span id="VALlength"><span class="keyword">val</span> length</span> : <code class="type">string -&gt; int</code></pre>
<pre><span id="VALget"><span class="keyword">val</span> get</span> : <code class="type">string -&gt; int -&gt; char</code></pre>
<pre><span id="VALset"><span class="keyword">val</span> set</span> : <code class="type">string -&gt; int -&gt; char -&gt; unit</code></pre>
<pre><span id="VALcreate"><span class="keyword">val</span> create</span> : <code class="type">int -&gt; string</code></pre>
<pre><span id="VALmake"><span class="keyword">val</span> make</span> : <code class="type">int -&gt; char -&gt; string</code></pre>
<pre><span id="VALcopy"><span class="keyword">val</span> copy</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALsub"><span class="keyword">val</span> sub</span> : <code class="type">string -&gt; pos:int -&gt; len:int -&gt; string</code></pre>
<pre><span id="VALfill"><span class="keyword">val</span> fill</span> : <code class="type">string -&gt; pos:int -&gt; len:int -&gt; char -&gt; unit</code></pre>
<pre><span id="VALblit"><span class="keyword">val</span> blit</span> : <code class="type">src:string -&gt; src_pos:int -&gt; dst:string -&gt; dst_pos:int -&gt; len:int -&gt; unit</code></pre>
<pre><span id="VALconcat"><span class="keyword">val</span> concat</span> : <code class="type">sep:string -&gt; string list -&gt; string</code></pre>
<pre><span id="VALiter"><span class="keyword">val</span> iter</span> : <code class="type">f:(char -&gt; unit) -&gt; string -&gt; unit</code></pre>
<pre><span id="VALiteri"><span class="keyword">val</span> iteri</span> : <code class="type">f:(int -&gt; char -&gt; unit) -&gt; string -&gt; unit</code></pre>
<pre><span id="VALmap"><span class="keyword">val</span> map</span> : <code class="type">f:(char -&gt; char) -&gt; string -&gt; string</code></pre>
<pre><span id="VALtrim"><span class="keyword">val</span> trim</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALescaped"><span class="keyword">val</span> escaped</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALindex"><span class="keyword">val</span> index</span> : <code class="type">string -&gt; char -&gt; int</code></pre>
<pre><span id="VALrindex"><span class="keyword">val</span> rindex</span> : <code class="type">string -&gt; char -&gt; int</code></pre>
<pre><span id="VALindex_from"><span class="keyword">val</span> index_from</span> : <code class="type">string -&gt; int -&gt; char -&gt; int</code></pre>
<pre><span id="VALrindex_from"><span class="keyword">val</span> rindex_from</span> : <code class="type">string -&gt; int -&gt; char -&gt; int</code></pre>
<pre><span id="VALcontains"><span class="keyword">val</span> contains</span> : <code class="type">string -&gt; char -&gt; bool</code></pre>
<pre><span id="VALcontains_from"><span class="keyword">val</span> contains_from</span> : <code class="type">string -&gt; int -&gt; char -&gt; bool</code></pre>
<pre><span id="VALrcontains_from"><span class="keyword">val</span> rcontains_from</span> : <code class="type">string -&gt; int -&gt; char -&gt; bool</code></pre>
<pre><span id="VALuppercase"><span class="keyword">val</span> uppercase</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALlowercase"><span class="keyword">val</span> lowercase</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALcapitalize"><span class="keyword">val</span> capitalize</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="VALuncapitalize"><span class="keyword">val</span> uncapitalize</span> : <code class="type">string -&gt; string</code></pre>
<pre><span id="TYPEt"><span class="keyword">type</span> <code class="type"></code>t</span> = <code class="type">string</code> </pre>


<pre><span id="VALcompare"><span class="keyword">val</span> compare</span> : <code class="type"><a href="StdLabels.String.html#TYPEt">t</a> -&gt; <a href="StdLabels.String.html#TYPEt">t</a> -&gt; int</code></pre>
<pre><span id="VALunsafe_get"><span class="keyword">val</span> unsafe_get</span> : <code class="type">string -&gt; int -&gt; char</code></pre>
<pre><span id="VALunsafe_set"><span class="keyword">val</span> unsafe_set</span> : <code class="type">string -&gt; int -&gt; char -&gt; unit</code></pre>
<pre><span id="VALunsafe_blit"><span class="keyword">val</span> unsafe_blit</span> : <code class="type">src:string -&gt; src_pos:int -&gt; dst:string -&gt; dst_pos:int -&gt; len:int -&gt; unit</code></pre>
<pre><span id="VALunsafe_fill"><span class="keyword">val</span> unsafe_fill</span> : <code class="type">string -&gt; pos:int -&gt; len:int -&gt; char -&gt; unit</code></pre><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>