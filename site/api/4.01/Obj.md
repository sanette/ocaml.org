<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.01</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Obj</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Obj.html">Obj</a></h1>

<pre><span class="keyword">module</span> Obj: <code class="code"><span class="keyword">sig</span></code> <a href="Obj.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
Operations on internal representations of values.
<p>

   Not for the casual user.<br>
</p></div>
<hr width="100%">

<pre><span id="TYPEt"><span class="keyword">type</span> <code class="type"></code>t</span> </pre>


<pre><span id="VALrepr"><span class="keyword">val</span> repr</span> : <code class="type">'a -&gt; <a href="Obj.html#TYPEt">t</a></code></pre>
<pre><span id="VALobj"><span class="keyword">val</span> obj</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; 'a</code></pre>
<pre><span id="VALmagic"><span class="keyword">val</span> magic</span> : <code class="type">'a -&gt; 'b</code></pre>
<pre><span id="VALis_block"><span class="keyword">val</span> is_block</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; bool</code></pre>
<pre><span id="VALis_int"><span class="keyword">val</span> is_int</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; bool</code></pre>
<pre><span id="VALtag"><span class="keyword">val</span> tag</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int</code></pre>
<pre><span id="VALset_tag"><span class="keyword">val</span> set_tag</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; unit</code></pre>
<pre><span id="VALsize"><span class="keyword">val</span> size</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int</code></pre>
<pre><span id="VALfield"><span class="keyword">val</span> field</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; <a href="Obj.html#TYPEt">t</a></code></pre>
<pre><span id="VALset_field"><span class="keyword">val</span> set_field</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; <a href="Obj.html#TYPEt">t</a> -&gt; unit</code></pre>
<pre><span id="VALdouble_field"><span class="keyword">val</span> double_field</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; float</code></pre>
<pre><span id="VALset_double_field"><span class="keyword">val</span> set_double_field</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; float -&gt; unit</code></pre>
<pre><span id="VALnew_block"><span class="keyword">val</span> new_block</span> : <code class="type">int -&gt; int -&gt; <a href="Obj.html#TYPEt">t</a></code></pre>
<pre><span id="VALdup"><span class="keyword">val</span> dup</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; <a href="Obj.html#TYPEt">t</a></code></pre>
<pre><span id="VALtruncate"><span class="keyword">val</span> truncate</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; int -&gt; unit</code></pre>
<pre><span id="VALadd_offset"><span class="keyword">val</span> add_offset</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; <a href="Int32.html#TYPEt">Int32.t</a> -&gt; <a href="Obj.html#TYPEt">t</a></code></pre>
<pre><span id="VALlazy_tag"><span class="keyword">val</span> lazy_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALclosure_tag"><span class="keyword">val</span> closure_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALobject_tag"><span class="keyword">val</span> object_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALinfix_tag"><span class="keyword">val</span> infix_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALforward_tag"><span class="keyword">val</span> forward_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALno_scan_tag"><span class="keyword">val</span> no_scan_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALabstract_tag"><span class="keyword">val</span> abstract_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALstring_tag"><span class="keyword">val</span> string_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALdouble_tag"><span class="keyword">val</span> double_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALdouble_array_tag"><span class="keyword">val</span> double_array_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALcustom_tag"><span class="keyword">val</span> custom_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALfinal_tag"><span class="keyword">val</span> final_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALint_tag"><span class="keyword">val</span> int_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALout_of_heap_tag"><span class="keyword">val</span> out_of_heap_tag</span> : <code class="type">int</code></pre>
<pre><span id="VALunaligned_tag"><span class="keyword">val</span> unaligned_tag</span> : <code class="type">int</code></pre><br>
The following two functions are deprecated.  Use module <a href="Marshal.html"><code class="code"><span class="constructor">Marshal</span></code></a>
    instead.<br>

<pre><span id="VALmarshal"><span class="keyword">val</span> marshal</span> : <code class="type"><a href="Obj.html#TYPEt">t</a> -&gt; string</code></pre>
<pre><span id="VALunmarshal"><span class="keyword">val</span> unmarshal</span> : <code class="type">string -&gt; int -&gt; <a href="Obj.html#TYPEt">t</a> * int</code></pre><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>