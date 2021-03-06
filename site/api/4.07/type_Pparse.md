<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.07</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Pparse.html">Pparse</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;error&nbsp;=&nbsp;<span class="constructor">CannotRun</span>&nbsp;<span class="keyword">of</span>&nbsp;string&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">WrongMagic</span>&nbsp;<span class="keyword">of</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Error</span>&nbsp;<span class="keyword">of</span>&nbsp;<span class="constructor">Pparse</span>.error<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;preprocess&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;remove_preprocessed&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;ast_kind&nbsp;=<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Structure</span>&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.structure&nbsp;<span class="constructor">Pparse</span>.ast_kind<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">|</span>&nbsp;<span class="constructor">Signature</span>&nbsp;:&nbsp;<span class="constructor">Parsetree</span>.signature&nbsp;<span class="constructor">Pparse</span>.ast_kind<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;read_ast&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Pparse</span>.ast_kind&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;write_ast&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Pparse</span>.ast_kind&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;file&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(<span class="constructor">Lexing</span>.lexbuf&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Pparse</span>.ast_kind&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;apply_rewriters&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;?restore:bool&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Pparse</span>.ast_kind&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;apply_rewriters_str&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;?restore:bool&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.structure&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.structure<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;apply_rewriters_sig&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;?restore:bool&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.signature&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.signature<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;report_error&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Pparse</span>.error&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;parse_implementation&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.structure<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;parse_interface&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;tool_name:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Parsetree</span>.signature<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;call_external_preprocessor&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;open_and_check_magic&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Pervasives</span>.in_channel&nbsp;*&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">module</span>&nbsp;<span class="constructor">ImplementationHooks</span>&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">sig</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t&nbsp;=&nbsp;<span class="constructor">Parsetree</span>.structure<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;add_hook&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(<span class="constructor">Misc</span>.hook_info&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;apply_hooks&nbsp;:&nbsp;<span class="constructor">Misc</span>.hook_info&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">end</span><br>
&nbsp;&nbsp;<span class="keyword">module</span>&nbsp;<span class="constructor">InterfaceHooks</span>&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">sig</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t&nbsp;=&nbsp;<span class="constructor">Parsetree</span>.signature<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;add_hook&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(<span class="constructor">Misc</span>.hook_info&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;apply_hooks&nbsp;:&nbsp;<span class="constructor">Misc</span>.hook_info&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;t<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">end</span><br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>