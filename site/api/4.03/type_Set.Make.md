<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.03</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Set.Make.html">Set.Make</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">functor</span>&nbsp;(<span class="constructor">Ord</span>&nbsp;:&nbsp;<span class="constructor">OrderedType</span>)&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;<span class="keyword">sig</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;elt&nbsp;=&nbsp;<span class="constructor">Ord</span>.t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;empty&nbsp;:&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;is_empty&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;mem&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;add&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;singleton&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;remove&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;union&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;inter&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;diff&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;compare&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;equal&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;subset&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;iter&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;fold&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;for_all&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;exists&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;filter&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;partition&nbsp;:&nbsp;(elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;*&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;cardinal&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;elements&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;elt&nbsp;list
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;min_elt&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;elt
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;max_elt&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;elt
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;choose&nbsp;:&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;elt
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;split&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;*&nbsp;bool&nbsp;*&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;find&nbsp;:&nbsp;elt&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;elt
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;of_list&nbsp;:&nbsp;elt&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t
&nbsp;&nbsp;<span class="keyword">end</span></code><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>