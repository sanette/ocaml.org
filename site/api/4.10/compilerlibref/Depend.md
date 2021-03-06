<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.10</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Depend</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Depend.html">Depend</a></h1>

<pre><span id="MODULEDepend"><span class="keyword">module</span> Depend</span>: <code class="code"><span class="keyword">sig</span></code> <a href="Depend.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
<div class="info-desc">
<p>Module dependencies.</p>

<p><b>Warning:</b> this module is unstable and part of
  <a href="Compiler_libs.html">compiler-libs</a>.</p>
</div>
</div>
<hr width="100%">

<pre><span id="MODULEString"><span class="keyword">module</span> <a href="Depend.String.html">String</a></span>: <code class="type"><a href="Misc.Stdlib.String.html">Misc.Stdlib.String</a></code></pre>
<pre><code><span id="TYPEmap_tree"><span class="keyword">type</span> <code class="type"></code>map_tree</span> = </code></pre><table class="typetable">
<tbody><tr>
<td align="left" valign="top">
<code><span class="keyword">|</span></code></td>
<td align="left" valign="top">
<code><span id="TYPEELTmap_tree.Node"><span class="constructor">Node</span></span> <span class="keyword">of</span> <code class="type">String.Set.t * <a href="Depend.html#TYPEbound_map">bound_map</a></code></code></td>

</tr></tbody></table>



<pre><span id="TYPEbound_map"><span class="keyword">type</span> <code class="type"></code>bound_map</span> = <code class="type"><a href="Depend.html#TYPEmap_tree">map_tree</a> String.Map.t</code> </pre>


<pre><span id="VALmake_leaf"><span class="keyword">val</span> make_leaf</span> : <code class="type">string -&gt; <a href="Depend.html#TYPEmap_tree">map_tree</a></code></pre>
<pre><span id="VALmake_node"><span class="keyword">val</span> make_node</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Depend.html#TYPEmap_tree">map_tree</a></code></pre>
<pre><span id="VALweaken_map"><span class="keyword">val</span> weaken_map</span> : <code class="type">String.Set.t -&gt; <a href="Depend.html#TYPEmap_tree">map_tree</a> -&gt; <a href="Depend.html#TYPEmap_tree">map_tree</a></code></pre>
<pre><span id="VALfree_structure_names"><span class="keyword">val</span> free_structure_names</span> : <code class="type">String.Set.t ref</code></pre>
<pre><span id="VALpp_deps"><span class="keyword">val</span> pp_deps</span> : <code class="type">string list ref</code></pre><div class="info ">
<div class="info-desc">
<p>dependencies found by preprocessing tools</p>
</div>
</div>

<pre><span id="VALopen_module"><span class="keyword">val</span> open_module</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Longident.html#TYPEt">Longident.t</a> -&gt; <a href="Depend.html#TYPEbound_map">bound_map</a></code></pre>
<pre><span id="VALadd_use_file"><span class="keyword">val</span> add_use_file</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Parsetree.html#TYPEtoplevel_phrase">Parsetree.toplevel_phrase</a> list -&gt; unit</code></pre>
<pre><span id="VALadd_signature"><span class="keyword">val</span> add_signature</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Parsetree.html#TYPEsignature">Parsetree.signature</a> -&gt; unit</code></pre>
<pre><span id="VALadd_implementation"><span class="keyword">val</span> add_implementation</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Parsetree.html#TYPEstructure">Parsetree.structure</a> -&gt; unit</code></pre>
<pre><span id="VALadd_implementation_binding"><span class="keyword">val</span> add_implementation_binding</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Parsetree.html#TYPEstructure">Parsetree.structure</a> -&gt; <a href="Depend.html#TYPEbound_map">bound_map</a></code></pre>
<pre><span id="VALadd_signature_binding"><span class="keyword">val</span> add_signature_binding</span> : <code class="type"><a href="Depend.html#TYPEbound_map">bound_map</a> -&gt; <a href="Parsetree.html#TYPEsignature">Parsetree.signature</a> -&gt; <a href="Depend.html#TYPEbound_map">bound_map</a></code></pre>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>