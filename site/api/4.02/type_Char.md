<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.02</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Char.html">Char</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;code&nbsp;:&nbsp;char&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;=&nbsp;<span class="string">"%identity"</span><br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;chr&nbsp;:&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;char<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;escaped&nbsp;:&nbsp;char&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lowercase&nbsp;:&nbsp;char&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;char<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;uppercase&nbsp;:&nbsp;char&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;char<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t&nbsp;=&nbsp;char<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;compare&nbsp;:&nbsp;<span class="constructor">Char</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Char</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int<br>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;unsafe_chr&nbsp;:&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;char&nbsp;=&nbsp;<span class="string">"%identity"</span><br>
<span class="keyword">end</span></code><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>