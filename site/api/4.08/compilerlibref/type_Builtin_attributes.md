<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.08</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Builtin_attributes.html">Builtin_attributes</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_alerts&nbsp;:&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_alerts_inclusion&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;def:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;use:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;alerts_of_attrs&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="constructor">Misc</span>.<span class="constructor">Stdlib</span>.<span class="constructor">String</span>.<span class="constructor">Map</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;alerts_of_sig&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.signature&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="constructor">Misc</span>.<span class="constructor">Stdlib</span>.<span class="constructor">String</span>.<span class="constructor">Map</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;alerts_of_str&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.structure&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="constructor">Misc</span>.<span class="constructor">Stdlib</span>.<span class="constructor">String</span>.<span class="constructor">Map</span>.t<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_deprecated_mutable&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_deprecated_mutable_inclusion&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;def:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;use:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_no_alert&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_of_extension&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.extension&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;warning_attribute&nbsp;:&nbsp;?ppwarning:bool&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attribute&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;warning_scope&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;?ppwarning:bool&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;warn_on_literal_pattern&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;explicit_arity&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;immediate&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;has_unboxed&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;has_boxed&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.attributes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>