<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.09</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="CamlinternalMenhirLib.EngineTypes.TABLE.html">CamlinternalMenhirLib.EngineTypes.TABLE</a></div><ul></ul></nav></header>
<code class="code"><span class="keyword">sig</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;state<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;number&nbsp;:&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;token<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;terminal<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;nonterminal<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;semantic_value<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;token2terminal&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.token&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;token2value&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.token&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_terminal&nbsp;:&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;error_value&nbsp;:&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;foreach_terminal&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a)&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keywordsign">'</span>a&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>a<br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;production<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;production_index&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;int<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;find_production&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;int&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;default_reduction&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer)&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;action&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bool&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer)&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer)&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;(<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer)&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>env&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="keywordsign">'</span>answer<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;goto_nt&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.nonterminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;goto_prod&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;maybe_goto_nt&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.nonterminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;option<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;is_start&nbsp;:&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">exception</span>&nbsp;<span class="constructor">Error</span><br>
&nbsp;&nbsp;<span class="keyword">type</span>&nbsp;semantic_action&nbsp;=<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.token)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.env&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_value)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.stack<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;semantic_action&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.semantic_action<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;may_reduce&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;log&nbsp;:&nbsp;bool<br>
&nbsp;&nbsp;<span class="keyword">module</span>&nbsp;<span class="constructor">Log</span>&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">sig</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;state&nbsp;:&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;shift&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;reduce_or_accept&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.production&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;lookahead_token&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.terminal&nbsp;<span class="keywordsign">-&gt;</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Lexing</span>.position&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;<span class="constructor">Stdlib</span>.<span class="constructor">Lexing</span>.position&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;initiating_error_handling&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;resuming_error_handling&nbsp;:&nbsp;unit&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">val</span>&nbsp;handling_error&nbsp;:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="constructor">CamlinternalMenhirLib</span>.<span class="constructor">EngineTypes</span>.<span class="constructor">TABLE</span>.state&nbsp;<span class="keywordsign">-&gt;</span>&nbsp;unit<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">end</span><br>
<span class="keyword">end</span></code>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>