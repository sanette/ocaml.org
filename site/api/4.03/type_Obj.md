<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.03</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="Obj.html">Obj</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;repr&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;=&nbsp;<span class="string">"%identity"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;obj&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;=&nbsp;<span class="string">"%identity"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;magic&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>b&nbsp;=&nbsp;<span class="string">"%identity"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;is_block&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool&nbsp;=&nbsp;<span class="string">"caml_obj_is_block"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;is_int&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool&nbsp;=&nbsp;<span class="string">"%obj_is_int"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;tag&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;=&nbsp;<span class="string">"caml_obj_tag"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;size&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;=&nbsp;<span class="string">"%obj_size"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;field&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;=&nbsp;<span class="string">"%obj_field"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;set_field&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit&nbsp;=&nbsp;<span class="string">"%obj_set_field"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;set_tag&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit&nbsp;=&nbsp;<span class="string">"caml_obj_set_tag"</span>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;double_field&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;float
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;set_double_field&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;float&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;new_block&nbsp;:&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;=&nbsp;<span class="string">"caml_obj_block"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;dup&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;=&nbsp;<span class="string">"caml_obj_dup"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;truncate&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit&nbsp;=&nbsp;<span class="string">"caml_obj_truncate"</span>
&nbsp;&nbsp;<span class="keyword">external</span>&nbsp;add_offset&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Int32</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;=&nbsp;<span class="string">"caml_obj_add_offset"</span>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;first_non_constant_constructor_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;last_non_constant_constructor_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lazy_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;closure_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;object_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;infix_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;forward_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;no_scan_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;abstract_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;string_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;double_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;double_array_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;custom_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;final_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;int_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;out_of_heap_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;unaligned_tag&nbsp;:&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;extension_constructor&nbsp;:&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;extension_constructor
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;extension_name&nbsp;:&nbsp;extension_constructor&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;string
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;extension_id&nbsp;:&nbsp;extension_constructor&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;marshal&nbsp;:&nbsp;<span class="constructor">Obj</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bytes
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;unmarshal&nbsp;:&nbsp;bytes&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.t&nbsp;*&nbsp;int
&nbsp;&nbsp;<span class="keyword">module</span>&nbsp;<span class="constructor">Ephemeron</span>&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">sig</span>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;obj_t&nbsp;=&nbsp;<span class="constructor">Obj</span>.t
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;t
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;create&nbsp;:&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;length&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;get_key&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;option
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;get_key_copy&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;option
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;set_key&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;unset_key&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_key&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;blit_key&nbsp;:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;get_data&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;option
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;get_data_copy&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;option
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;set_data&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.obj_t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;unset_data&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;check_data&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;blit_data&nbsp;:&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Obj</span>.<span class="constructor">Ephemeron</span>.t&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">end</span>
<span class="keyword">end</span></code><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>