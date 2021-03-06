<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.01</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">StdLabels.Array</a></div><ul></ul></nav></header>

<h1>Module <a href="type_StdLabels.Array.html">StdLabels.Array</a></h1>

<pre><span class="keyword">module</span> Array: <code class="code"><span class="keyword">sig</span></code> <a href="StdLabels.Array.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><hr width="100%">

<pre><span id="VALlength"><span class="keyword">val</span> length</span> : <code class="type">'a array -&gt; int</code></pre>
<pre><span id="VALget"><span class="keyword">val</span> get</span> : <code class="type">'a array -&gt; int -&gt; 'a</code></pre>
<pre><span id="VALset"><span class="keyword">val</span> set</span> : <code class="type">'a array -&gt; int -&gt; 'a -&gt; unit</code></pre>
<pre><span id="VALmake"><span class="keyword">val</span> make</span> : <code class="type">int -&gt; 'a -&gt; 'a array</code></pre>
<pre><span id="VALcreate"><span class="keyword">val</span> create</span> : <code class="type">int -&gt; 'a -&gt; 'a array</code></pre>
<pre><span id="VALinit"><span class="keyword">val</span> init</span> : <code class="type">int -&gt; f:(int -&gt; 'a) -&gt; 'a array</code></pre>
<pre><span id="VALmake_matrix"><span class="keyword">val</span> make_matrix</span> : <code class="type">dimx:int -&gt; dimy:int -&gt; 'a -&gt; 'a array array</code></pre>
<pre><span id="VALcreate_matrix"><span class="keyword">val</span> create_matrix</span> : <code class="type">dimx:int -&gt; dimy:int -&gt; 'a -&gt; 'a array array</code></pre>
<pre><span id="VALappend"><span class="keyword">val</span> append</span> : <code class="type">'a array -&gt; 'a array -&gt; 'a array</code></pre>
<pre><span id="VALconcat"><span class="keyword">val</span> concat</span> : <code class="type">'a array list -&gt; 'a array</code></pre>
<pre><span id="VALsub"><span class="keyword">val</span> sub</span> : <code class="type">'a array -&gt; pos:int -&gt; len:int -&gt; 'a array</code></pre>
<pre><span id="VALcopy"><span class="keyword">val</span> copy</span> : <code class="type">'a array -&gt; 'a array</code></pre>
<pre><span id="VALfill"><span class="keyword">val</span> fill</span> : <code class="type">'a array -&gt; pos:int -&gt; len:int -&gt; 'a -&gt; unit</code></pre>
<pre><span id="VALblit"><span class="keyword">val</span> blit</span> : <code class="type">src:'a array -&gt; src_pos:int -&gt; dst:'a array -&gt; dst_pos:int -&gt; len:int -&gt; unit</code></pre>
<pre><span id="VALto_list"><span class="keyword">val</span> to_list</span> : <code class="type">'a array -&gt; 'a list</code></pre>
<pre><span id="VALof_list"><span class="keyword">val</span> of_list</span> : <code class="type">'a list -&gt; 'a array</code></pre>
<pre><span id="VALiter"><span class="keyword">val</span> iter</span> : <code class="type">f:('a -&gt; unit) -&gt; 'a array -&gt; unit</code></pre>
<pre><span id="VALmap"><span class="keyword">val</span> map</span> : <code class="type">f:('a -&gt; 'b) -&gt; 'a array -&gt; 'b array</code></pre>
<pre><span id="VALiteri"><span class="keyword">val</span> iteri</span> : <code class="type">f:(int -&gt; 'a -&gt; unit) -&gt; 'a array -&gt; unit</code></pre>
<pre><span id="VALmapi"><span class="keyword">val</span> mapi</span> : <code class="type">f:(int -&gt; 'a -&gt; 'b) -&gt; 'a array -&gt; 'b array</code></pre>
<pre><span id="VALfold_left"><span class="keyword">val</span> fold_left</span> : <code class="type">f:('a -&gt; 'b -&gt; 'a) -&gt; init:'a -&gt; 'b array -&gt; 'a</code></pre>
<pre><span id="VALfold_right"><span class="keyword">val</span> fold_right</span> : <code class="type">f:('a -&gt; 'b -&gt; 'b) -&gt; 'a array -&gt; init:'b -&gt; 'b</code></pre>
<pre><span id="VALsort"><span class="keyword">val</span> sort</span> : <code class="type">cmp:('a -&gt; 'a -&gt; int) -&gt; 'a array -&gt; unit</code></pre>
<pre><span id="VALstable_sort"><span class="keyword">val</span> stable_sort</span> : <code class="type">cmp:('a -&gt; 'a -&gt; int) -&gt; 'a array -&gt; unit</code></pre>
<pre><span id="VALfast_sort"><span class="keyword">val</span> fast_sort</span> : <code class="type">cmp:('a -&gt; 'a -&gt; int) -&gt; 'a array -&gt; unit</code></pre>
<pre><span id="VALunsafe_get"><span class="keyword">val</span> unsafe_get</span> : <code class="type">'a array -&gt; int -&gt; 'a</code></pre>
<pre><span id="VALunsafe_set"><span class="keyword">val</span> unsafe_set</span> : <code class="type">'a array -&gt; int -&gt; 'a -&gt; unit</code></pre><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>