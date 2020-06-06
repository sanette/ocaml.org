<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.03</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Location.html">Location</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t&nbsp;=&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;loc_start&nbsp;:&nbsp;<span class="constructor">Lexing</span>.position;
&nbsp;&nbsp;&nbsp;&nbsp;loc_end&nbsp;:&nbsp;<span class="constructor">Lexing</span>.position;
&nbsp;&nbsp;&nbsp;&nbsp;loc_ghost&nbsp;:&nbsp;bool;
&nbsp;&nbsp;}
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;none&nbsp;:&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;in_file&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;init&nbsp;:&nbsp;<span class="constructor">Lexing</span>.lexbuf&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;curr&nbsp;:&nbsp;<span class="constructor">Lexing</span>.lexbuf&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;symbol_rloc&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;symbol_gloc&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;rhs_loc&nbsp;:&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;input_name&nbsp;:&nbsp;string&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;input_lexbuf&nbsp;:&nbsp;<span class="constructor">Lexing</span>.lexbuf&nbsp;option&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;get_pos_info&nbsp;:&nbsp;<span class="constructor">Lexing</span>.position&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;*&nbsp;int&nbsp;*&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_loc&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_error&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_error_cur_file&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_warning&nbsp;:&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Warnings</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;formatter_for_warnings&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;prerr_warning&nbsp;:&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Warnings</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;echo_eof&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;reset&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;warning_printer&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Warnings</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit)&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;default_warning_printer&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Warnings</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;highlight_locations&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;loc&nbsp;=&nbsp;{&nbsp;txt&nbsp;:&nbsp;<span class="keywordsign">'</span>a;&nbsp;loc&nbsp;:&nbsp;<span class="constructor">Location</span>.t;&nbsp;}
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;mknoloc&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Location</span>.loc
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;mkloc&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="constructor">Location</span>.loc
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_compact&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_filename&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;absolute_path&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;show_filename&nbsp;:&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;absname&nbsp;:&nbsp;bool&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;error&nbsp;=&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;loc&nbsp;:&nbsp;<span class="constructor">Location</span>.t;
&nbsp;&nbsp;&nbsp;&nbsp;msg&nbsp;:&nbsp;string;
&nbsp;&nbsp;&nbsp;&nbsp;sub&nbsp;:&nbsp;<span class="constructor">Location</span>.error&nbsp;list;
&nbsp;&nbsp;&nbsp;&nbsp;if_highlight&nbsp;:&nbsp;string;
&nbsp;&nbsp;}
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Error</span>&nbsp;<span class="keyword">of</span>&nbsp;<span class="constructor">Location</span>.error
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;print_error_prefix&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;?loc:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?sub:<span class="constructor">Location</span>.error&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?if_highlight:string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;errorf&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;?loc:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?sub:<span class="constructor">Location</span>.error&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?if_highlight:string&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>a,&nbsp;<span class="constructor">Format</span>.formatter,&nbsp;unit,&nbsp;<span class="constructor">Location</span>.error)&nbsp;<span class="constructor">Pervasives</span>.format4&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;errorf_prefixed&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;?loc:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?sub:<span class="constructor">Location</span>.error&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?if_highlight:string&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>a,&nbsp;<span class="constructor">Format</span>.formatter,&nbsp;unit,&nbsp;<span class="constructor">Location</span>.error)&nbsp;<span class="constructor">Pervasives</span>.format4&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;raise_errorf&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;?loc:<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?sub:<span class="constructor">Location</span>.error&nbsp;list&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;?if_highlight:string&nbsp;<span class="keywordsign">-&gt;</span>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>a,&nbsp;<span class="constructor">Format</span>.formatter,&nbsp;unit,&nbsp;<span class="keywordsign">'</span>b)&nbsp;<span class="constructor">Pervasives</span>.format4&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_of_printer&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Location</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;(<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_of_printer_file&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_of_exn&nbsp;:&nbsp;exn&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error&nbsp;option
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;register_error_of_exn&nbsp;:&nbsp;(exn&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error&nbsp;option)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;report_error&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_reporter&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit)&nbsp;<span class="constructor">Pervasives</span>.ref
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;default_error_reporter&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Location</span>.error&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;report_exception&nbsp;:&nbsp;<span class="constructor">Format</span>.formatter&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;exn&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
<span class="keyword">end</span></code><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>