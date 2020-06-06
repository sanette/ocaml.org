<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.09</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Scanf.Scanning.html">Scanf.Scanning</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;in_channel<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;scanbuf&nbsp;=&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;stdin&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;file_name&nbsp;=&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;open_in&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.file_name&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;open_in_bin&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.file_name&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;close_in&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_file&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.file_name&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_file_bin&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_string&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_function&nbsp;:&nbsp;(unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;char)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;from_channel&nbsp;:&nbsp;<span class="constructor">Stdlib</span>.in_channel&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;end_of_input&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;beginning_of_input&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;name_of_input&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;stdib&nbsp;:&nbsp;<span class="constructor">Scanf</span>.<span class="constructor">Scanning</span>.in_channel<br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>