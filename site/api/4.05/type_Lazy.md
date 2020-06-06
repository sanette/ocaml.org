<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.05</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Lazy.html">Lazy</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;t&nbsp;=&nbsp;<span class="keywordsign">'</span>a&nbsp;lazy_t<br>
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Undefined</span><br>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;force&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;=&nbsp;<span class="string">"%lazy_force"</span><br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;force_val&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_fun&nbsp;:&nbsp;(unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_val&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;is_val&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lazy_from_fun&nbsp;:&nbsp;(unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lazy_from_val&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lazy_is_val&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
<span class="keyword">end</span></code><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>