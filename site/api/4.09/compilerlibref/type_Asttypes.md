<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.09</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Asttypes.html">Asttypes</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;constant&nbsp;=<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Const_int</span>&nbsp;<span class="keyword">of</span>&nbsp;int<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_char</span>&nbsp;<span class="keyword">of</span>&nbsp;char<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_string</span>&nbsp;<span class="keyword">of</span>&nbsp;string&nbsp;*&nbsp;string&nbsp;option<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_float</span>&nbsp;<span class="keyword">of</span>&nbsp;string<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_int32</span>&nbsp;<span class="keyword">of</span>&nbsp;int32<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_int64</span>&nbsp;<span class="keyword">of</span>&nbsp;int64<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Const_nativeint</span>&nbsp;<span class="keyword">of</span>&nbsp;nativeint<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;rec_flag&nbsp;=&nbsp;<span class="constructor">Nonrecursive</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Recursive</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;direction_flag&nbsp;=&nbsp;<span class="constructor">Upto</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Downto</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;private_flag&nbsp;=&nbsp;<span class="constructor">Private</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Public</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;mutable_flag&nbsp;=&nbsp;<span class="constructor">Immutable</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Mutable</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;virtual_flag&nbsp;=&nbsp;<span class="constructor">Virtual</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Concrete</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;override_flag&nbsp;=&nbsp;<span class="constructor">Override</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Fresh</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;closed_flag&nbsp;=&nbsp;<span class="constructor">Closed</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Open</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;label&nbsp;=&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;arg_label&nbsp;=&nbsp;<span class="constructor">Nolabel</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Labelled</span>&nbsp;<span class="keyword">of</span>&nbsp;string&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Optional</span>&nbsp;<span class="keyword">of</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;loc&nbsp;=&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Location</span>.loc&nbsp;=&nbsp;{&nbsp;txt&nbsp;:&nbsp;<span class="keywordsign">'</span>a;&nbsp;loc&nbsp;:&nbsp;<span class="constructor">Location</span>.t;&nbsp;}<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;variance&nbsp;=&nbsp;<span class="constructor">Covariant</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Contravariant</span>&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Invariant</span><br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>