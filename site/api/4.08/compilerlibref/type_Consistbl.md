<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.08</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Consistbl.html">Consistbl</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;create&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Consistbl</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;clear&nbsp;:&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check&nbsp;:&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Digest</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_noadd&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Digest</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;set&nbsp;:&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Digest</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;source&nbsp;:&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;extract&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;string&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(string&nbsp;*&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Digest</span>.t&nbsp;option)&nbsp;list<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;filter&nbsp;:&nbsp;(string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Consistbl</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Inconsistency</span>&nbsp;<span class="keyword">of</span>&nbsp;string&nbsp;*&nbsp;string&nbsp;*&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Not_available</span>&nbsp;<span class="keyword">of</span>&nbsp;string<br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>