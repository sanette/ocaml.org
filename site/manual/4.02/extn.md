<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="language.html">The OCaml language</a></li><li class="active"><a href="extn.html">Language extensions</a></li></ul>




<h1 class="chapter" id="sec210"><span>Chapter 7</span>&nbsp;&nbsp;Language extensions</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.02</a></div><div class="toc_title"><a href="#">Language extensions</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="extn.html#sec211">Integer literals for types <span class="c007">int32</span>, <span class="c007">int64</span>
and <span class="c007">nativeint</span></a>
</li><li><a href="extn.html#sec212">Streams and stream parsers</a>
</li><li><a href="extn.html#sec213">Recursive definitions of values</a>
</li><li><a href="extn.html#sec214">Range patterns</a>
</li><li><a href="extn.html#sec215">Assertion checking</a>
</li><li><a href="extn.html#sec216">Lazy evaluation</a>
</li><li><a href="extn.html#sec219">Local modules</a>
</li><li><a href="extn.html#sec220">Recursive modules</a>
</li><li><a href="extn.html#sec221">Private types</a>
</li><li><a href="extn.html#sec225">Local opens</a>
</li><li><a href="extn.html#sec226">Record notations</a>
</li><li><a href="extn.html#sec227">Explicit polymorphic type annotations</a>
</li><li><a href="extn.html#sec228">Locally abstract types</a>
</li><li><a href="extn.html#sec230">First-class modules</a>
</li><li><a href="extn.html#sec233">Recovering the type of a module</a>
</li><li><a href="extn.html#sec234">Substituting inside a signature</a>
</li><li><a href="extn.html#sec235">Type-level module aliases</a>
</li><li><a href="extn.html#sec236">Explicit overriding in class definitions</a>
</li><li><a href="extn.html#sec237">Overriding in open statements</a>
</li><li><a href="extn.html#sec238">Generalized algebraic datatypes</a>
</li><li><a href="extn.html#sec240">Syntax for Bigarray access</a>
</li><li><a href="extn.html#sec241">Attributes</a>
</li><li><a href="extn.html#sec243">Extension nodes</a>
</li><li><a href="extn.html#sec244">Quoted strings</a>
</li><li><a href="extn.html#sec245">Exception cases in pattern matching</a>
</li><li><a href="extn.html#sec246">Extensible variant types</a>
</li><li><a href="extn.html#sec247">Generative functors</a>
</li></ul></nav></header>
<p> <a id="c:extensions"></a>

</p><p>This chapter describes language extensions and convenience features
that are implemented in OCaml, but not described in the
OCaml reference manual.</p>
<h2 class="section" id="sec211">1&nbsp;&nbsp;Integer literals for types <span class="c007">int32</span>, <span class="c007">int64</span>
and <span class="c007">nativeint</span></h2>
<p>(Introduced in Objective Caml 3.07)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="const.html#constant"><span class="c014">constant</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#int32-literal"><span class="c014">int32-literal</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#int64-literal"><span class="c014">int64-literal</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#nativeint-literal"><span class="c014">nativeint-literal</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="int32-literal"><span class="c014">int32-literal</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#integer-literal"><span class="c014">integer-literal</span></a>&nbsp;<span class="c008">l</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="int64-literal"><span class="c014">int64-literal</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#integer-literal"><span class="c014">integer-literal</span></a>&nbsp;<span class="c008">L</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="nativeint-literal"><span class="c014">nativeint-literal</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#integer-literal"><span class="c014">integer-literal</span></a>&nbsp;<span class="c008">n</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>An integer literal can be followed by one of the letters <span class="c007">l</span>, <span class="c007">L</span> or <span class="c007">n</span>
to indicate that this integer has type <span class="c007">int32</span>, <span class="c007">int64</span> or <span class="c007">nativeint</span>
respectively, instead of the default type <span class="c007">int</span> for integer literals.
<a id="hevea_manual3"></a>
<a id="hevea_manual4"></a>
<a id="hevea_manual5"></a>
The library modules <span class="c007">Int32</span>[<a href="../../api/4.02/Int32.html"><span class="c007">Int32</span></a>],
<span class="c007">Int64</span>[<a href="../../api/4.02/Int64.html"><span class="c007">Int64</span></a>] and <span class="c007">Nativeint</span>[<a href="../../api/4.02/Nativeint.html"><span class="c007">Nativeint</span></a>]
provide operations on these integer types.</p>
<h2 class="section" id="sec212">2&nbsp;&nbsp;Streams and stream parsers</h2>
<p> <a id="s:streams"></a></p><p>(Removed in Objective Caml 3.03)</p><p>The syntax for streams and stream parsers is no longer part of the
OCaml language, but available through a Camlp4 syntax
extension. See the Camlp4 reference manual for more information.
Support for basic operations on streams is still available through the
<span class="c007">Stream</span>[<a href="../../api/4.02/Stream.html"><span class="c007">Stream</span></a>] module of the standard library.
OCaml programs
that use the stream parser syntax should be compiled with the
<span class="c007">-pp camlp4o</span> option to <span class="c007">ocamlc</span> and <span class="c007">ocamlopt</span>. For interactive use,
run <span class="c007">ocaml</span> and issue the <code>#load "dynlink.cma";;</code> command,
followed by the <code>#load "camlp4o.cma";;</code> command.</p>
<h2 class="section" id="sec213">3&nbsp;&nbsp;Recursive definitions of values</h2>
<p> <a id="s:letrecvalues"></a></p><p>(Introduced in Objective Caml 1.00)</p><p>As mentioned in section&nbsp;<a href="expr.html#s%3Alocaldef">6.7.1</a>, the <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> binding
construct, in addition to the definition of recursive functions,
also supports a certain class of recursive definitions of
non-functional values, such as
</p><div class="center">
<span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> <span class="c014">name</span><sub>1</sub> <span class="c005"><span class="c007">=</span> <span class="c007">1</span> <span class="c007">::</span></span> &nbsp;<span class="c014">name</span><sub>2</sub>
<span class="c008">and</span> &nbsp;<span class="c014">name</span><sub>2</sub> <span class="c005"><span class="c007">=</span> <span class="c007">2</span> <span class="c007">::</span></span> &nbsp;<span class="c014">name</span><sub>1</sub>
<span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</div><p>
which binds <span class="c014">name</span><sub>1</sub> to the cyclic list <span class="c007">1::2::1::2::</span>…, and
<span class="c014">name</span><sub>2</sub> to the cyclic list <span class="c007">2::1::2::1::</span>…Informally, the class of accepted definitions consists of those
definitions where the defined names occur only inside function
bodies or as argument to a data constructor.</p><p>More precisely, consider the expression:
</p><div class="center">
<span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> <span class="c014">name</span><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">and</span> … <span class="c008">and</span> &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</div><p>
It will be accepted if each one of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> is
statically constructive with respect to <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>,
is not immediately linked to any of <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>,
and is not an array constructor whose arguments have abstract type.</p><p>An expression <span class="c014">e</span> is said to be <em>statically constructive
with respect to</em> the variables <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub> if at least
one of the following conditions is true:
</p><ul class="itemize"><li class="li-itemize">
<span class="c014">e</span> has no free occurrence of any of <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>
</li><li class="li-itemize"><span class="c014">e</span> is a variable
</li><li class="li-itemize"><span class="c014">e</span> has the form <span class="c008">fun</span> … <span class="c008">-&gt;</span> …
</li><li class="li-itemize"><span class="c014">e</span> has the form <span class="c008">function</span> … <span class="c008">-&gt;</span> …
</li><li class="li-itemize"><span class="c014">e</span> has the form <span class="c005"><span class="c007">lazy</span> <span class="c007">(</span></span> … <span class="c008">)</span>
</li><li class="li-itemize"><span class="c014">e</span> has one of the following forms, where each one of
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> is statically constructive with respect to
<span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>, and <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> is statically constructive with
respect to <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>, &nbsp;<span class="c014">xname</span><sub>1</sub> … &nbsp;<span class="c014">xname</span><sub><span class="c013">m</span></sub>:
<ul class="itemize"><li class="li-itemize">
<span class="c008">let</span> [<span class="c008">rec</span>] <span class="c014">xname</span><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">and</span> …
<span class="c008">and</span> &nbsp;<span class="c014">xname</span><sub><span class="c013">m</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub>
</li><li class="li-itemize"><span class="c005"><span class="c007">let</span> <span class="c007">module</span></span> … <span class="c008">in</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub>
</li><li class="li-itemize"><a class="syntax" href="names.html#constr"><span class="c014">constr</span></a> <span class="c008">(</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> … <span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub><span class="c008">)</span>
</li><li class="li-itemize"><span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a> <span class="c008">(</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> … <span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub><span class="c008">)</span>
</li><li class="li-itemize"><span class="c008">[|</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">|]</span>
</li><li class="li-itemize"><span class="c008">{</span> <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">m</span></sub> = &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">}</span>
</li><li class="li-itemize"><span class="c008">{</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">with</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>2</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub><span class="c008">;</span> … <span class="c008">;</span>
&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">m</span></sub> = &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">}</span> where <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> is not immediately
linked to <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub>
</li><li class="li-itemize"><span class="c008">(</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> … <span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">)</span>
</li><li class="li-itemize"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub>
</li></ul>
</li></ul><p>An expression <span class="c014">e</span> is said to be <em>immediately linked to</em> the variable
<span class="c014">name</span> in the following cases:
</p><ul class="itemize"><li class="li-itemize">
<span class="c014">e</span> is <span class="c014">name</span>
</li><li class="li-itemize"><span class="c014">e</span> has the form <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> where <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub>
is immediately linked to <span class="c014">name</span>
</li><li class="li-itemize"><span class="c014">e</span> has the form <span class="c008">let</span> [<span class="c008">rec</span>] <span class="c014">xname</span><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">and</span> …
<span class="c008">and</span> &nbsp;<span class="c014">xname</span><sub><span class="c013">m</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">m</span></sub> <span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> where <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> is immediately
linked to <span class="c014">name</span> or to one of the <span class="c014">xname</span><sub><span class="c013">i</span></sub> such that <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub>
is immediately linked to <span class="c014">name</span>.
</li></ul>
<h2 class="section" id="sec214">4&nbsp;&nbsp;Range patterns</h2>
<p> <a id="s:range-patterns"></a></p><p>(Introduced in Objective Caml 1.00)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#char-literal"><span class="c014">char-literal</span></a>&nbsp;<span class="c008">..</span>&nbsp;&nbsp;<a class="syntax" href="lex.html#char-literal"><span class="c014">char-literal</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>In patterns, OCaml recognizes the form
<span class="c005"><span class="c007">'</span> <span class="c014">c</span> <span class="c007">'</span> <span class="c007">..</span> <span class="c007">'</span> <span class="c014">d</span> <span class="c007">'</span></span> as shorthand for the pattern
</p><div class="center">
<span class="c008">'</span> <span class="c006"><span class="c013">c</span> <span class="c005"><span class="c007">'</span> <span class="c007">|</span> <span class="c007">'</span></span> <span class="c013">c</span></span><sub>1</sub> <span class="c005"><span class="c007">'</span> <span class="c007">|</span> <span class="c007">'</span></span> <span class="c014">c</span><sub>2</sub> <span class="c005"><span class="c007">'</span> <span class="c007">|</span></span> …
<span class="c005"><span class="c007">|</span> <span class="c007">'</span></span> <span class="c014">c</span><sub><span class="c013">n</span></sub> <span class="c005"><span class="c007">'</span> <span class="c007">|</span> <span class="c007">'</span> <span class="c014">d</span> <span class="c007">'</span></span>
</div><p>
where <span class="c013">c</span><sub>1</sub>, <span class="c013">c</span><sub>2</sub>, …, <span class="c013">c</span><sub><span class="c013">n</span></sub> are the characters
that occur between <span class="c013">c</span> and <span class="c013">d</span> in the ASCII character set. For
instance, the pattern <span class="c007">'0'<span class="c005">..</span>'9'</span> matches all characters that are digits.</p>
<h2 class="section" id="sec215">5&nbsp;&nbsp;Assertion checking</h2>
<p><a id="s:assert"></a>
<a id="hevea_manual.kwd173"></a></p><p>(Introduced in Objective Caml 1.06)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">assert</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>OCaml supports the <span class="c008">assert</span> construct to check debugging assertions.
The expression <span class="c008">assert</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> evaluates the expression <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> and
returns <span class="c008">()</span> if <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> evaluates to <span class="c008">true</span>. If it evaluates to
<span class="c008">false</span> the exception
<span class="c007">Assert_failure</span> is raised with the source file name and the
location of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> as arguments. Assertion
checking can be turned off with the <span class="c007">-noassert</span> compiler option. In
this case, <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> is not evaluated at all.</p><p>As a special case, <span class="c008">assert false</span> is reduced to
<span class="c008">raise</span> <span class="c007"><span class="c005">(</span>Assert_failure ...<span class="c005">)</span></span>, which gives it a polymorphic
type. This means that it can be used in place of any expression (for
example as a branch of any pattern-matching). It also means that
the <span class="c008">assert false</span> “assertions” cannot be turned off by the
<span class="c007">-noassert</span> option.
<a id="hevea_manual6"></a></p>
<h2 class="section" id="sec216">6&nbsp;&nbsp;Lazy evaluation</h2>
<p> <a id="s:lazy"></a>
<a id="hevea_manual.kwd174"></a></p>
<h3 class="subsection" id="sec217">6.1&nbsp;&nbsp;Lazy expressions</h3>
<p>
(Introduced in Objective Caml 1.06)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">lazy</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The expression <span class="c008">lazy</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> returns a value <span class="c013">v</span> of type <span class="c007">Lazy.t</span> that
encapsulates the computation of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>. The argument <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> is not
evaluated at this point in the program. Instead, its evaluation will
be performed the first time the function <span class="c007">Lazy.force</span> is applied to the value
<span class="c013">v</span>, returning the actual value of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>. Subsequent applications
of <span class="c007">Lazy.force</span> to <span class="c013">v</span> do not evaluate <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> again. Applications
of <span class="c007">Lazy.force</span> may be implicit through pattern matching (see below).</p>
<h3 class="subsection" id="sec218">6.2&nbsp;&nbsp;Lazy patterns</h3>
<p>
(Introduced in Objective Caml 3.11)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">lazy</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The pattern <span class="c008">lazy</span> <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a> matches a value <span class="c013">v</span> of type <span class="c007">Lazy.t</span>,
provided <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a> matches the result of forcing <span class="c013">v</span> with
<span class="c007">Lazy.force</span>. A successful match of a pattern containing <span class="c008">lazy</span>
sub-patterns forces the corresponding parts of the value being matched, even
those that imply no test such as <span class="c008">lazy</span> <a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a> or <span class="c005"><span class="c007">lazy</span> <span class="c007">_</span></span>.
Matching a value with a <a class="syntax" href="expr.html#pattern-matching"><span class="c014">pattern-matching</span></a> where some patterns
contain <span class="c008">lazy</span> sub-patterns may imply forcing parts of the value,
even when the pattern selected in the end has no <span class="c008">lazy</span> sub-pattern.</p><p>For more information, see the description of module <span class="c007">Lazy</span> in the
standard library (
<a href="../../api/4.02/Lazy.html">Module <span class="c007">Lazy</span></a>).
<a id="hevea_manual7"></a><a id="hevea_manual8"></a></p>
<h2 class="section" id="sec219">7&nbsp;&nbsp;Local modules</h2>
<p>
<a id="hevea_manual.kwd175"></a>
<a id="hevea_manual.kwd176"></a></p><p>(Introduced in Objective Caml 2.00)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">let</span>&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">)</span>&nbsp;}
&nbsp;[&nbsp;<span class="c008">:</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;]&nbsp;&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;<span class="c008">in</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The expression
<span class="c005"><span class="c007">let</span> <span class="c007">module</span></span> <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> <span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
locally binds the module expression <a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> to the identifier
<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> during the evaluation of the expression <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>.
It then returns the value of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>. For example:
</p><pre>        let remove_duplicates comparison_fun string_list =
          let module StringSet =
            Set.Make(struct type t = string
                            let compare = comparison_fun end) in
          StringSet.elements
            (List.fold_right StringSet.add string_list StringSet.empty)
</pre>
<h2 class="section" id="sec220">8&nbsp;&nbsp;Recursive modules</h2>
<p> <a id="s-recursive-modules"></a>
<a id="hevea_manual.kwd177"></a>
<a id="hevea_manual.kwd178"></a></p><p>(Introduced in Objective Caml 3.07)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">rec</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;
&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">rec</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>
&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a><span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;}
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Recursive module definitions, introduced by the <span class="c008">module rec</span> …<span class="c008">and</span> … construction, generalize regular module definitions
<span class="c008">module</span> <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> and module specifications
<span class="c008">module</span> <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a> by allowing the defining
<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> and the <a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a> to refer recursively to the module
identifiers being defined. A typical example of a recursive module
definition is:
</p><pre>    module rec A : sig
                     type t = Leaf of string | Node of ASet.t
                     val compare: t -&gt; t -&gt; int
                   end
                 = struct
                     type t = Leaf of string | Node of ASet.t
                     let compare t1 t2 =
                       match (t1, t2) with
                         (Leaf s1, Leaf s2) -&gt; Pervasives.compare s1 s2
                       | (Leaf _, Node _) -&gt; 1
                       | (Node _, Leaf _) -&gt; -1
                       | (Node n1, Node n2) -&gt; ASet.compare n1 n2
                   end
        and ASet : Set.S with type elt = A.t
                 = Set.Make(A)
</pre><p>It can be given the following specification:
</p><pre>    module rec A : sig
                     type t = Leaf of string | Node of ASet.t
                     val compare: t -&gt; t -&gt; int
                   end
        and ASet : Set.S with type elt = A.t
</pre><p>
This is an experimental extension of OCaml: the class of
recursive definitions accepted, as well as its dynamic semantics are
not final and subject to change in future releases.</p><p>Currently, the compiler requires that all dependency cycles between
the recursively-defined module identifiers go through at least one
“safe” module. A module is “safe” if all value definitions that
it contains have function types <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>2</sub>. Evaluation of a
recursive module definition proceeds by building initial values for
the safe modules involved, binding all (functional) values to
<span class="c005"><span class="c007">fun</span> <span class="c007">_</span> <span class="c007">-&gt;</span> <span class="c007">raise</span></span> <span class="c007">Undefined_recursive_module</span>. The defining
module expressions are then evaluated, and the initial values
for the safe modules are replaced by the values thus computed. If a
function component of a safe module is applied during this computation
(which corresponds to an ill-founded recursive definition), the
<span class="c007">Undefined_recursive_module</span> exception is raised.</p><p>Note that, in the <a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a> case, the <a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>s must be
parenthesized if they use the <span class="c008">with</span> <a class="syntax" href="modtypes.html#mod-constraint"><span class="c014">mod-constraint</span></a> construct.</p>
<h2 class="section" id="sec221">9&nbsp;&nbsp;Private types</h2>
<p>
<a id="hevea_manual.kwd179"></a></p><p>Private type declarations in module signatures, of the form
<span class="c007">type t = private ...</span>, enable libraries to
reveal some, but not all aspects of the implementation of a type to
clients of the library. In this respect, they strike a middle ground
between abstract type declarations, where no information is revealed
on the type implementation, and data type definitions and type
abbreviations, where all aspects of the type implementation are
publicized. Private type declarations come in three flavors: for
variant and record types (section&nbsp;<a href="#s-private-types-variant">7.9.1</a>),
for type abbreviations (section&nbsp;<a href="#s-private-types-abbrev">7.9.2</a>),
and for row types (section&nbsp;<a href="#s-private-rows">7.9.3</a>).</p>
<h3 class="subsection" id="sec222">9.1&nbsp;&nbsp;Private variant and record types</h3>
<p> <a id="s-private-types-variant"></a></p><p>(Introduced in Objective Caml 3.07)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="typedecl.html#type-representation"><span class="c014">type-representation</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">private</span>&nbsp;[&nbsp;<span class="c008">|</span>&nbsp;]&nbsp;<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">private</span>&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="typedecl.html#field-decl"><span class="c014">field-decl</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="typedecl.html#field-decl"><span class="c014">field-decl</span></a>&nbsp;}&nbsp;&nbsp;[&nbsp;<span class="c008">;</span>&nbsp;]&nbsp;<span class="c008">}</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Values of a variant or record type declared <span class="c008">private</span>
can be de-structured normally in pattern-matching or via
the <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> <span class="c008">.</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a> notation for record accesses. However, values of
these types cannot be constructed directly by constructor application
or record construction. Moreover, assignment on a mutable field of a
private record type is not allowed.</p><p>The typical use of private types is in the export signature of a
module, to ensure that construction of values of the private type always
go through the functions provided by the module, while still allowing
pattern-matching outside the defining module. For example:
</p><pre>        module M : sig
                     type t = private A | B of int
                     val a : t
                     val b : int -&gt; t
                   end
                 = struct
                     type t = A | B of int
                     let a = A
                     let b n = assert (n &gt; 0); B n
                   end
</pre><p>Here, the <span class="c008">private</span> declaration ensures that in any value of type
<span class="c007">M.t</span>, the argument to the <span class="c007">B</span> constructor is always a positive integer.</p><p>With respect to the variance of their parameters, private types are
handled like abstract types. That is, if a private type has
parameters, their variance is the one explicitly given by prefixing
the parameter by a ‘<span class="c007">+</span>’ or a ‘<span class="c007">-</span>’, it is invariant otherwise.</p>
<h3 class="subsection" id="sec223">9.2&nbsp;&nbsp;Private type abbreviations</h3>
<p> <a id="s-private-types-abbrev"></a></p><p>(Introduced in Objective Caml 3.11)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="typedecl.html#type-equation"><span class="c014">type-equation</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">private</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Unlike a regular type abbreviation, a private type abbreviation
declares a type that is distinct from its implementation type <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>.
However, coercions from the type to <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> are permitted.
Moreover, the compiler “knows” the implementation type and can take
advantage of this knowledge to perform type-directed optimizations.
For ambiguity reasons, <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> cannot be an object or polymorphic
variant type, but a similar behaviour can be obtained through private
row types.</p><p>The following example uses a private type abbreviation to define a
module of nonnegative integers:
</p><pre>        module N : sig
                     type t = private int
                     val of_int: int -&gt; t
                     val to_int: t -&gt; int
                   end
                 = struct
                     type t = int
                     let of_int n = assert (n &gt;= 0); n
                     let to_int n = n
                   end
</pre><p>The type <span class="c007">N.t</span> is incompatible with <span class="c007">int</span>, ensuring that nonnegative
integers and regular integers are not confused. However, if <span class="c007">x</span> has
type <span class="c007">N.t</span>, the coercion <span class="c007">(x :&gt; int)</span> is legal and returns the
underlying integer, just like <span class="c007">N.to_int x</span>. Deep coercions are also
supported: if <span class="c007">l</span> has type <span class="c007">N.t list</span>, the coercion <span class="c007">(l :&gt; int list)</span>
returns the list of underlying integers, like <span class="c007">List.map N.to_int l</span>
but without copying the list <span class="c007">l</span>.</p><p>Note that the coercion <span class="c008">(</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> <span class="c008">:&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> <span class="c008">)</span> is actually an abbreviated
form,
and will only work in presence of private abbreviations if neither the
type of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> nor <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> contain any type variables. If they do,
you must use the full form <span class="c008">(</span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">:&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>2</sub> <span class="c008">)</span> where
<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> is the expected type of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>. Concretely, this would be <span class="c007">(x : N.t :&gt; int)</span> and <span class="c007">(l : N.t list :&gt; int list)</span> for the above examples.</p>
<h3 class="subsection" id="sec224">9.3&nbsp;&nbsp;Private row types</h3>
<p> <a id="s-private-rows"></a>
<a id="hevea_manual.kwd180"></a></p><p>(Introduced in Objective Caml 3.09)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="typedecl.html#type-equation"><span class="c014">type-equation</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">private</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Private row types are type abbreviations where part of the
structure of the type is left abstract. Concretely <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> in the
above should denote either an object type or a polymorphic variant
type, with some possibility of refinement left. If the private
declaration is used in an interface, the corresponding implementation
may either provide a ground instance, or a refined private type.
</p><pre>   module M : sig type c = private &lt; x : int; .. &gt; val o : c end =
     struct
       class c = object method x = 3 method y = 2 end
       let o = new c
     end
</pre><p>This declaration does more than hiding the <span class="c007">y</span> method, it also makes
the type <span class="c007">c</span> incompatible with any other closed object type, meaning
that only <span class="c007">o</span> will be of type <span class="c007">c</span>. In that respect it behaves
similarly to private record types. But private row types are
more flexible with respect to incremental refinement. This feature can
be used in combination with functors.
</p><pre>   module F(X : sig type c = private &lt; x : int; .. &gt; end) =
     struct
       let get_x (o : X.c) = o#x
     end
   module G(X : sig type c = private &lt; x : int; y : int; .. &gt; end) =
     struct
       include F(X)
       let get_y (o : X.c) = o#y
     end
</pre><p>
Polymorphic variant types can be refined in two ways, either to allow
the addition of new constructors, or to allow the disparition of
declared constructors. The second case corresponds to private variant
types (one cannot create a value of the private type), while the first
case requires default cases in pattern-matching to handle addition.
</p><pre>   type t = [ `A of int | `B of bool ]
   type u = private [&lt; t &gt; `A ]
   type v = private [&gt; t ]
</pre><p>With type <span class="c007">u</span>, it is possible to create values of the form <span class="c007">(`A n)</span>,
but not <span class="c007">(`B b)</span>. With type <span class="c007">v</span>, construction is not restricted but
pattern-matching must have a default case.</p><p>Similarly to abstract types, the variance of type parameters
is not inferred, and must be given explicitly.</p>
<h2 class="section" id="sec225">10&nbsp;&nbsp;Local opens</h2>
<p>
<a id="hevea_manual.kwd181"></a>
<a id="hevea_manual.kwd182"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">let</span>&nbsp;<span class="c008">open</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>&nbsp;<span class="c008">in</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>&nbsp;<span class="c008">.(</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">)</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The expressions
<span class="c005"><span class="c007">let</span> <span class="c007">open</span></span> <a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a> <span class="c008">in</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
and
<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a><span class="c008">.(</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><span class="c008">)</span> are strictly equivalent. They
locally open the module referred to by the module path <a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a> in
the scope of the expression <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>.</p><p>Restricting opening to the scope of a single expression instead of a
whole structure allows one to benefit from shorter syntax to refer to
components of the opened module, without polluting the global
scope. Also, this can make the code easier to read (the open statement is
closer to where it is used) and to refactor (because the code
fragment is more self-contained).</p>
<h2 class="section" id="sec226">11&nbsp;&nbsp;Record notations</h2>
<p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>]&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>]&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>&nbsp;<span class="c008">_</span>&nbsp;]&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>]&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>]&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">with</span>&nbsp;&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>]&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>]&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>In a record pattern or a record construction expression, a single
identifier <span class="c014">id</span> stands for <span class="c014">id</span> <span class="c008">=</span> &nbsp;<span class="c014">id</span>, and a qualified identifier
<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a> <span class="c008">.</span> &nbsp;<span class="c014">id</span> stands for <a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a> <span class="c008">.</span> &nbsp;<span class="c014">id</span> <span class="c008">=</span> &nbsp;<span class="c014">id</span>.
For example, assuming
the record type
</p><pre>          type point = { x: float; y: float }
</pre><p>has been declared, the following expressions are equivalent:
</p><pre>          let x = 1 and y = 2 in { x = x; y = y }
          let x = 1 and y = 2 in { x; y }
          let x = 1 and y = 2 in { x = x; y }
</pre><p>Likewise, the following functions are equivalent:
</p><pre>          fun {x = x; y = y} -&gt; x + y
          fun {x; y} -&gt; x + y
</pre><p>
Optionally, a record pattern can be terminated by <span class="c005"><span class="c007">;</span> <span class="c007">_</span></span> to convey the
fact that not all fields of the record type are listed in the record
pattern and that it is intentional. By default, the compiler ignores
the <span class="c005"><span class="c007">;</span> <span class="c007">_</span></span> annotation. If warning 9 is turned on,
the compiler will warn when a record pattern fails to list all fields of
the corresponding record type and is not terminated by <span class="c005"><span class="c007">;</span> <span class="c007">_</span></span>.
Continuing the <span class="c007">point</span> example above,
</p><pre>          fun {x} -&gt; x + 1
</pre><p>will warn if warning 9 is on, while
</p><pre>          fun {x; _} -&gt; x + 1
</pre><p>will not warn. This warning can help spot program points where
record patterns may need to be modified after new fields are added to a
record type.</p>
<h2 class="section" id="sec227">12&nbsp;&nbsp;Explicit polymorphic type annotations</h2>
<p>
<a id="hevea_manual.kwd183"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#let-binding"><span class="c014">let-binding</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Polymorphic type annotations in <span class="c008">let</span>-definitions behave in a way
similar to polymorphic methods: they explicitly require the defined
value to be polymorphic, and allow one to use this polymorphism in
recursive occurrences (when using <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span>). Note however that this
is a normal polymorphic type, unifiable with any instance of
itself.</p><p>There are two possible applications of this feature. One is polymorphic
recursion:
</p><pre>        type 'a t = Leaf of 'a | Node of ('a * 'a) t
        let rec depth : 'a. 'a t -&gt; 'b = function
            Leaf _ -&gt; 1
          | Node x -&gt; 1 + depth x
</pre><p>Note that <span class="c007">'b</span> is not explicitly polymorphic here, and it will
actually be unified with <span class="c007">int</span>.</p><p>The other application is to ensure that some definition is sufficiently
polymorphic.
</p><pre><span class="c004">#</span><span class="c003"> let id : 'a. 'a -&gt; 'a = <u>fun x -&gt; x+1</u> ;;
</span><span class="c006">Error: This definition has type int -&gt; int which is less general than
         'a. 'a -&gt; 'a
</span></pre>
<h2 class="section" id="sec228">13&nbsp;&nbsp;Locally abstract types</h2>
<p>
<a id="hevea_manual.kwd184"></a>
<a id="hevea_manual.kwd185"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#parameter"><span class="c014">parameter</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<span class="c008">type</span>&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;<span class="c008">)</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The expression <span class="c005"><span class="c007">fun</span> <span class="c007">(</span> <span class="c007">type</span></span> <a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a> <span class="c005"><span class="c007">)</span> <span class="c007">-&gt;</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> introduces a
type constructor named <a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a> which is considered abstract
in the scope of the sub-expression, but then replaced by a fresh type
variable. Note that contrary to what the syntax could suggest, the
expression <span class="c005"><span class="c007">fun</span> <span class="c007">(</span> <span class="c007">type</span></span> <a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a> <span class="c005"><span class="c007">)</span> <span class="c007">-&gt;</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> itself does not
suspend the evaluation of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> as a regular abstraction would. The
syntax has been chosen to fit nicely in the context of function
declarations, where it is generally used. It is possible to freely mix
regular function parameters with pseudo type parameters, as in:
</p><pre>        let f = fun (type t) (foo : t list) -&gt; ...
</pre><p>and even use the alternative syntax for declaring functions:
</p><pre>        let f (type t) (foo : t list) = ...
</pre><p>
This construction is useful because the type constructor it introduces
can be used in places where a type variable is not allowed. For
instance, one can use it to define an exception in a local module
within a polymorphic function.
</p><pre>        let f (type t) () =
          let module M = struct exception E of t end in
          (fun x -&gt; M.E x), (function M.E x -&gt; Some x | _ -&gt; None)
</pre><p>
Here is another example:
</p><pre>        let sort_uniq (type s) (cmp : s -&gt; s -&gt; int) =
          let module S = Set.Make(struct type t = s let compare = cmp end) in
          fun l -&gt;
            S.elements (List.fold_right S.add l S.empty)
</pre><p>
It is also extremely useful for first-class modules and GADTs.</p>
<h5 class="paragraph" id="sec229">Polymorphic syntax</h5>
<p> (Introduced in OCaml 4.00)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#let-binding"><span class="c014">let-binding</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;<span class="c008">type</span>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;}<sup>+</sup>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">method</span>&nbsp;[<span class="c008">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;<span class="c008">type</span>
&nbsp;{&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;}<sup>+</sup>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">method!</span>&nbsp;[<span class="c008">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;<span class="c008">type</span>
&nbsp;{&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;}<sup>+</sup>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The <span class="c008">(type</span> <a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a><span class="c008">)</span> syntax construction by itself does not make
polymorphic the type variable it introduces, but it can be combined
with explicit polymorphic annotations where needed.
The above rule is provided as syntactic sugar to make this easier:
</p><pre>        let rec f : type t1 t2. t1 * t2 list -&gt; t1 = ...
</pre><p>is automatically expanded into
</p><pre>        let rec f : 't1 't2. 't1 * 't2 list -&gt; 't1 =
          fun (type t1) (type t2) -&gt; (... : t1 * t2 list -&gt; t1)
</pre><p>
The same feature is provided for method definitions.
The <span class="c008">method!</span> form combines this extension with the
“explicit overriding” extension described in
section&nbsp;<a href="#s%3Aexplicit-overriding">7.18</a>.</p>
<h2 class="section" id="sec230">14&nbsp;&nbsp;First-class modules</h2>
<p><a id="s-first-class-modules"></a>
<a id="hevea_manual.kwd186"></a>
<a id="hevea_manual.kwd187"></a>
<a id="hevea_manual.kwd188"></a></p><p>(Introduced in OCaml 3.12; pattern syntax and package type inference
introduced in 4.00; structural comparison of package types introduced in 4.02.)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(module</span>&nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a><span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(val</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a>]<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(module</span>&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a>]<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a>]<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="package-type"><span class="c014">package-type</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="names.html#modtype-path"><span class="c014">modtype-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#modtype-path"><span class="c014">modtype-path</span></a>&nbsp;<span class="c008">with</span>&nbsp;&nbsp;<a class="syntax" href="#package-constraint"><span class="c014">package-constraint</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="#package-constraint"><span class="c014">package-constraint</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="package-constraint"><span class="c014">package-constraint</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">type</span>&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Modules are typically thought of as static components. This extension
makes it possible to pack a module as a first-class value, which can
later be dynamically unpacked into a module.</p><p>The expression <span class="c005"><span class="c007">(</span> <span class="c007">module</span></span> <a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c008">)</span> converts the
module (structure or functor) denoted by module expression <a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>
to a value of the core language that encapsulates this module. The
type of this core language value is <span class="c005"><span class="c007">(</span> <span class="c007">module</span></span> <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c008">)</span>.
The <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> annotation can be omitted if it can be inferred
from the context.</p><p>Conversely, the module expression <span class="c005"><span class="c007">(</span> <span class="c007">val</span></span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c008">)</span>
evaluates the core language expression <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> to a value, which must
have type <span class="c008">module</span> <a class="syntax" href="#package-type"><span class="c014">package-type</span></a>, and extracts the module that was
encapsulated in this value. Again <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> can be omitted if the
type of <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> is known.</p><p>The pattern <span class="c005"><span class="c007">(</span> <span class="c007">module</span></span> <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c008">)</span> matches a
package with type <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> and binds it to <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>.
It is not allowed in toplevel let bindings.
Again <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> can be omitted if it can be inferred from the
enclosing pattern.</p><p>The <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> syntactic class appearing in the <span class="c005"><span class="c007">(</span> <span class="c007">module</span></span>
<a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c008">)</span> type expression and in the annotated forms represents a
subset of module types.
This subset consists of named module types with optional constraints
of a limited form: only non-parametrized types can be specified.</p><p>For type-checking purposes (and starting from OCaml 4.02), package types
are compared using the structural comparison of module types.</p><p>In general, the module expression <span class="c005"><span class="c007">(</span> <span class="c007">val</span></span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a>
<span class="c008">)</span> cannot be used in the body of a functor, because this could cause
unsoundness in conjunction with applicative functors.
Since OCaml 4.02, this is relaxed in two ways:
if <a class="syntax" href="#package-type"><span class="c014">package-type</span></a> does not contain nominal type declarations (<em>i.e.</em> types that are created with a proper identity), then this
expression can be used anywhere, and even if it contains such types
it can be used inside the body of a generative
functor, described in section&nbsp;<a href="#s%3Agenerative-functors">7.27</a>.
It can also be used anywhere in the context of a local module binding
<span class="c005"><span class="c007">let</span> <span class="c007">module</span></span> <a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a> <span class="c005"><span class="c007">=</span> <span class="c007">(</span> <span class="c007">val</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c014">package-type</span></a> <span class="c005"><span class="c007">)</span>
<span class="c007">in</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub>.</p>
<h5 class="paragraph" id="sec231">Basic example</h5>
<p> A typical use of first-class modules is to
select at run-time among several implementations of a signature.
Each implementation is a structure that we can encapsulate as a
first-class module, then store in a data structure such as a hash
table:
</p><pre>        module type DEVICE = sig ... end
        let devices : (string, (module DEVICE)) Hashtbl.t = Hashtbl.create 17

        module SVG = struct ... end
        let _ = Hashtbl.add devices "SVG" (module SVG : DEVICE)

        module PDF = struct ... end
        let _ = Hashtbl.add devices "PDF" (module PDF: DEVICE)
</pre><p>We can then select one implementation based on command-line
arguments, for instance:
</p><pre>        module Device =
          (val (try Hashtbl.find devices (parse_cmdline())
                with Not_found -&gt; eprintf "Unknown device %s\n"; exit 2)
           : DEVICE)
</pre><p>Alternatively, the selection can be performed within a function:
</p><pre>        let draw_using_device device_name picture =
          let module Device =
            (val (Hashtbl.find_devices device_name) : DEVICE)
          in
            Device.draw picture
</pre>
<h5 class="paragraph" id="sec232">Advanced examples</h5>
<p>
With first-class modules, it is possible to parametrize some code over the
implementation of a module without using a functor.</p><pre>        let sort (type s) (module Set : Set.S with type elt = s) l =
          Set.elements (List.fold_right Set.add l Set.empty)
        val sort : (module Set.S with type elt = 'a) -&gt; 'a list -&gt; 'a list
</pre><p>
To use this function, one can wrap the <span class="c007">Set.Make</span> functor:</p><pre>        let make_set (type s) cmp =
          let module S = Set.Make(struct
            type t = s
            let compare = cmp
          end) in
          (module S : Set.S with type elt = s)
        val make_set : ('a -&gt; 'a -&gt; int) -&gt; (module Set.S with type elt = 'a)
</pre>
<h2 class="section" id="sec233">15&nbsp;&nbsp;Recovering the type of a module</h2>
<p><a id="hevea_manual.kwd189"></a>
<a id="hevea_manual.kwd190"></a>
<a id="hevea_manual.kwd191"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">type</span>&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The construction <span class="c005"><span class="c007">module</span> <span class="c007">type</span> <span class="c007">of</span></span> <a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a> expands to the module type
(signature or functor type) inferred for the module expression <a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>.
To make this module type reusable in many situations, it is
intentionally not strengthened: abstract types and datatypes are not
explicitly related with the types of the original module.
For the same reason, module aliases in the inferred type are expanded.</p><p>A typical use, in conjunction with the signature-level <span class="c008">include</span>
construct, is to extend the signature of an existing structure.
In that case, one wants to keep the types equal to types in the
original module. This can done using the following idiom.
</p><pre>        module type MYHASH = sig
          include module type of struct include Hashtbl end
          val replace: ('a, 'b) t -&gt; 'a -&gt; 'b -&gt; unit
        end
</pre><p>The signature <span class="c007">MYHASH</span> then contains all the fields of the signature
of the module <span class="c007">Hashtbl</span> (with strengthened type definitions), plus the
new field <span class="c007">replace</span>. An implementation of this signature can be
obtained easily by using the <span class="c008">include</span> construct again, but this
time at the structure level:
</p><pre>        module MyHash : MYHASH = struct
          include Hashtbl
          let replace t k v = remove t k; add t k v
        end
</pre><p>
Another application where the absence of strengthening comes handy, is
to provide an alternative implementation for an existing module.
</p><pre>        module MySet : module type of Set = struct
          ...
        end
</pre><p>This idiom guarantees that <span class="c007">Myset</span> is compatible with Set, but allows
it to represent sets internally in a different way.</p>
<h2 class="section" id="sec234">16&nbsp;&nbsp;Substituting inside a signature</h2>
<p>
<a id="hevea_manual.kwd192"></a>
<a id="hevea_manual.kwd193"></a>
<a id="hevea_manual.kwd194"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modtypes.html#mod-constraint"><span class="c014">mod-constraint</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">type</span>&nbsp;[<a class="syntax" href="typedecl.html#type-params"><span class="c014">type-params</span></a>]&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;<span class="c008">:=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:=</span>&nbsp;&nbsp;<a class="syntax" href="names.html#extended-module-path"><span class="c014">extended-module-path</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>“Destructive” substitution (<span class="c008">with</span> ... <span class="c008">:=</span> ...) behaves essentially like
normal signature constraints (<span class="c008">with</span> ... <span class="c008">=</span> ...), but it additionally removes
the redefined type or module from the signature. There are a number of
restrictions: one can only remove types and modules at the outermost
level (not inside submodules), and in the case of <span class="c008">with type</span> the
definition must be another type constructor with the same type
parameters.</p><p>A natural application of destructive substitution is merging two
signatures sharing a type name.
</p><pre>        module type Printable = sig
          type t
          val print : Format.formatter -&gt; t -&gt; unit
        end
        module type Comparable = sig
          type t
          val compare : t -&gt; t -&gt; int
        end
        module type PrintableComparable = sig
          include Printable
          include Comparable with type t := t
        end
</pre><p>
One can also use this to completely remove a field:
</p><pre><span class="c004">#<span class="c003"> module type S = Comparable with type t := int;;
<span class="c006">module type S = sig val compare : int -&gt; int -&gt; int end
</span></span></span></pre><p>
or to rename one:
</p><pre><span class="c004">#<span class="c003"> module type S = sig
    type u
    include Comparable with type t := u
  end;;
<span class="c006">module type S = sig type u val compare : u -&gt; u -&gt; int end
</span></span></span></pre><p>Note that you can also remove manifest types, by substituting with the
same type.
</p><pre><span class="c004">#</span><span class="c003"> module type ComparableInt = Comparable with type t = int ;;
<span class="c006">module type ComparableInt = sig type t = int val compare : t -&gt; t -&gt; int end
</span><span class="c004">#</span> module type CompareInt = ComparableInt with type t := int ;;
</span><span class="c006">module type CompareInt = sig val compare : int -&gt; int -&gt; int end
</span></pre>
<h2 class="section" id="sec235">17&nbsp;&nbsp;Type-level module aliases</h2>
<p>
<a id="hevea_manual.kwd195"></a>
<a id="s:module-alias"></a></p><p>(Introduced in OCaml 4.02)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The above specification, inside a signature, only matches a module
definition equal to <a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>. Conversely, a type-level module
alias can be matched by itself, or by any supertype of the type of the
module it references.</p><p>There are several restrictions on <a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>:
</p><ol class="enumerate" type="1"><li class="li-enumerate">
it should be of the form <span class="c013">M</span><sub>0</sub>.<span class="c013">M</span><sub>1</sub>...<span class="c013">M</span><sub><span class="c013">n</span></sub> (<em>i.e.</em> without
functor applications);
</li><li class="li-enumerate">inside the body of a functor, <span class="c013">M</span><sub>0</sub> should not be one of the
functor parameters;
</li><li class="li-enumerate">inside a recursive module definition, <span class="c013">M</span><sub>0</sub> should not be one of
the recursively defined modules.
</li></ol><p>Such specifications are also inferred. Namely, when <span class="c014">P</span> is a path
satisfying the above constraints,
</p><pre><span class="c004">#<span class="c003"> module N = P
</span></span></pre><p>
has type
</p><pre><span class="c006">module N = P
</span></pre><p>Type-level module aliases are used when checking module path
equalities. That is, in a context where module name <span class="c014">N</span> is known to be
an alias for <span class="c014">P</span>, not only these two module paths check as equal, but
<span class="c014">F</span>&nbsp;(<span class="c014">N</span>) and <span class="c014">F</span>&nbsp;(<span class="c014">P</span>) are also recognized as equal. In the default
compilation mode, this is the only difference with the previous
approach of module aliases having just the same module type as the
module they reference.</p><p>When the compiler flag <span class="c008">-no-alias-deps</span> is enabled, type-level
module aliases are also exploited to avoid introducing dependencies
between compilation units. Namely, a module alias referring to a
module inside another compilation unit does not introduce a link-time
dependency on that compilation unit, as long as it is not
dereferenced; it still introduces a compile-time dependency if the
interface needs to be read, <em>i.e.</em> if the module is a submodule
of the compilation unit, or if some type components are referred to.
Additionally, accessing a module alias introduces a link-time
dependency on the compilation unit containing the module referenced by
the alias, rather than the compilation unit containing the alias.
Note that these differences in link-time behavior may be incompatible
with the previous behavior, as some compilation units might not be
extracted from libraries, and their side-effects ignored.</p><p>These weakened dependencies make possible to use module aliases in
place of the <span class="c008">-pack</span> mechanism. Suppose that you have a library
<span class="c008">Mylib</span> composed of modules <span class="c008">A</span> and <span class="c008">B</span>. Using <span class="c008">-pack</span>, one
would issue the command line
</p><pre>  ocamlc -pack a.cmo b.cmo -o mylib.cmo
</pre><p>and as a result obtain a <span class="c008">Mylib</span> compilation unit, containing
physically <span class="c008">A</span> and <span class="c008">B</span> as submodules, and with no dependencies on
their respective compilation units.
Here is a concrete example of a possible alternative approach:
</p><ol class="enumerate" type="1"><li class="li-enumerate">
Rename the files containing <span class="c008">A</span> and <span class="c008">B</span> to <span class="c008">Mylib_A</span> and
<span class="c008">Mylib_B</span>.
</li><li class="li-enumerate">Create a packing interface <span class="c008">Mylib.ml</span>, containing the
following lines.
<pre>    module A = Mylib_A
    module B = Mylib_B
</pre></li><li class="li-enumerate">Compile <span class="c008">Mylib.ml</span> using <span class="c008">-no-alias-deps</span>, and the other
files using <span class="c008">-no-alias-deps</span> and <span class="c005"><span class="c007">-open</span> <span class="c007">Mylib</span></span> (the last one is
equivalent to adding the line <span class="c005"><span class="c007">open!</span> <span class="c007">Mylib</span></span> at the top of each
file).
<pre>    ocamlc -c -no-alias-deps Mylib.ml
    ocamlc -c -no-alias-deps -open Mylib Mylib_*.mli Mylib_*.ml
</pre></li><li class="li-enumerate">Finally, create a library containing all the compilation units,
and export all the compiled interfaces.
<pre>    ocamlc -a Mylib*.cmo -o Mylib.cma
</pre></li></ol><p>
This approach lets you access <span class="c008">A</span> and <span class="c008">B</span> directly inside the
library, and as <span class="c008">Mylib.A</span> and <span class="c008">Mylib.B</span> from outside.
It also has the advantage that <span class="c008">Mylib</span> is no longer monolithic: if
you use <span class="c008">Mylib.A</span>, only <span class="c008">Mylib_A</span> will be linked in, not
<span class="c008">Mylib_B</span>.
</p>
<h2 class="section" id="sec236">18&nbsp;&nbsp;Explicit overriding in class definitions</h2>
<p><a id="s:explicit-overriding"></a>
<a id="hevea_manual.kwd196"></a>
<a id="hevea_manual.kwd197"></a>
<a id="hevea_manual.kwd198"></a></p><p>(Introduced in OCaml 3.12)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">inherit!</span>&nbsp;<a class="syntax" href="classes.html#class-expr"><span class="c014">class-expr</span></a>&nbsp;&nbsp;[<span class="c008">as</span>&nbsp;<a class="syntax" href="lex.html#lowercase-ident"><span class="c014">lowercase-ident</span></a>]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">val!</span>&nbsp;[<span class="c008">mutable</span>]&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">method!</span>&nbsp;[<span class="c008">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>&nbsp;&nbsp;{<a class="syntax" href="expr.html#parameter"><span class="c014">parameter</span></a>}&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">method!</span>&nbsp;[<span class="c008">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The keywords <span class="c008">inherit!</span>, <span class="c008">val!</span> and <span class="c008">method!</span> have the same semantics
as <span class="c008">inherit</span>, <span class="c008">val</span> and <span class="c008">method</span>, but they additionally require the
definition they introduce to be an overriding. Namely, <span class="c008">method!</span>
requires <a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a> to be already defined in this class, <span class="c008">val!</span>
requires <a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a> to be already defined in this class, and
<span class="c008">inherit!</span> requires <a class="syntax" href="classes.html#class-expr"><span class="c014">class-expr</span></a> to override some definitions.
If no such overriding occurs, an error is signaled.</p><p>As a side-effect, these 3 keywords avoid the warnings&nbsp;7
(method override) and&nbsp;13 (instance variable override).
Note that warning&nbsp;7 is disabled by default.</p>
<h2 class="section" id="sec237">19&nbsp;&nbsp;Overriding in open statements</h2>
<p><a id="s:explicit-overriding-open"></a>
<a id="hevea_manual.kwd199"></a></p><p>(Introduced in OCaml 4.01)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">open!</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">open!</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">let</span>&nbsp;<span class="c008">open!</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>&nbsp;<span class="c008">in</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Since OCaml 4.01, <span class="c008">open</span> statements shadowing an existing identifier
(which is later used) trigger the warning 44. Adding a <span class="c008">!</span>
character after the <span class="c008">open</span> keyword indicates that such a shadowing is
intentional and should not trigger the warning.</p>
<h2 class="section" id="sec238">20&nbsp;&nbsp;Generalized algebraic datatypes</h2>
<p> <a id="hevea_manual.kwd200"></a>
<a id="hevea_manual.kwd201"></a></p><p>(Introduced in OCaml 4.00)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;[&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;<span class="c008">-&gt;</span>&nbsp;]&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="typedecl.html#type-param"><span class="c014">type-param</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;[<a class="syntax" href="typedecl.html#variance"><span class="c014">variance</span></a>]&nbsp;<span class="c008">_</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Generalized algebraic datatypes, or GADTs, extend usual sum types in
two ways: constraints on type parameters may change depending on the
value constructor, and some type variables may be existentially
quantified.
Adding constraints is done by giving an explicit return type
(the rightmost <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> in the above syntax), where type parameters
are instantiated.
This return type must use the same type constructor as the type being
defined, and have the same number of parameters.
Variables are made existential when they appear inside a constructor’s
argument, but not in its return type.</p><p>Since the use of a return type often eliminates the need to name type
parameters in the left-hand side of a type definition, one can replace
them with anonymous types <span class="c008">_</span> in that case.</p><p>The constraints associated to each constructor can be recovered
through pattern-matching.
Namely, if the type of the scrutinee of a pattern-matching contains
a locally abstract type, this type can be refined according to the
constructor used.
These extra constraints are only valid inside the corresponding branch
of the pattern-matching.
If a constructor has some existential variables, fresh locally
abstract types are generated, and they must not escape the
scope of this branch.</p><p>Here is a concrete example:
</p><pre>        type _ term =
          | Int : int -&gt; int term
          | Add : (int -&gt; int -&gt; int) term
          | App : ('b -&gt; 'a) term * 'b term -&gt; 'a term

        let rec eval : type a. a term -&gt; a = function
          | Int n    -&gt; n                 (* a = int *)
          | Add      -&gt; (fun x y -&gt; x+y)  (* a = int -&gt; int -&gt; int *)
          | App(f,x) -&gt; (eval f) (eval x)
                  (* eval called at types (b-&gt;a) and b for fresh b *)

        let two = eval (App (App (Add, Int 1), Int 1))
        val two : int = 2
</pre><p>
Type inference for GADTs is notoriously hard.
This is due to the fact some types may become ambiguous when escaping
from a branch.
For instance, in the <span class="c007">Int</span> case above, <span class="c007">n</span> could have either type <span class="c007">int</span>
or <span class="c007">a</span>, and they are not equivalent outside of that branch.
As a first approximation, type inference will always work if a
pattern-matching is annotated with types containing no free type
variables (both on the scrutinee and the return type).
This is the case in the above example, thanks to the type annotation
containing only locally abstract types.</p><p>In practice, type inference is a bit more clever than that: type
annotations do not need to be immediately on the pattern-matching, and
the types do not have to be always closed.
As a result, it is usually enough to only annotate functions, as in
the example above. Type annotations are
propagated in two ways: for the scrutinee, they follow the flow of
type inference, in a way similar to polymorphic methods; for the
return type, they follow the structure of the program, they are split
on functions, propagated to all branches of a pattern matching,
and go through tuples, records, and sum types.
Moreover, the notion of ambiguity used is stronger: a type is only
seen as ambiguous if it was mixed with incompatible types (equated by
constraints), without type annotations between them.
For instance, the following program types correctly.
</p><pre>        let rec sum : type a. a term -&gt; _ = fun x -&gt;
          let y =
            match x with
            | Int n -&gt; n
            | Add   -&gt; 0
            | App(f,x) -&gt; sum f + sum x
          in y + 1
        val sum : 'a term -&gt; int = &lt;fun&gt;
</pre><p>Here the return type <span class="c007">int</span> is never mixed with <span class="c007">a</span>, so it is seen as
non-ambiguous, and can be inferred.
When using such partial type annotations we strongly suggest
specifying the <span class="c007">-principal</span> mode, to check that inference is
principal.</p><p>The exhaustiveness check is aware of GADT constraints, and can
automatically infer that some cases cannot happen.
For instance, the following pattern matching is correctly seen as
exhaustive (the <span class="c007">Add</span> case cannot happen).
</p><pre>        let get_int : int term -&gt; int = function
          | Int n    -&gt; n
          | App(_,_) -&gt; 0
</pre>
<h5 class="paragraph" id="sec239">Advanced examples</h5>
<p>
The <span class="c007">term</span> type we have defined above is an <em>indexed</em> type, where
a type parameter reflects a property of the value contents.
Another use of GADTs is <em>singleton</em> types, where a GADT value
represents exactly one type. This value can be used as runtime
representation for this type, and a function receiving it can have a
polytypic behavior.</p><p>Here is an example of a polymorphic function that takes the
runtime representation of some type <span class="c007">t</span> and a value of the same type,
then pretty-prints the value as a string:
</p><pre>        type _ typ =
          | Int : int typ
          | String : string typ
          | Pair : 'a typ * 'b typ -&gt; ('a * 'b) typ

        let rec to_string: type t. t typ -&gt; t -&gt; string =
          fun t x -&gt;
          match t with
          | Int -&gt; string_of_int x
          | String -&gt; Printf.sprintf "%S" x
          | Pair(t1,t2) -&gt;
              let (x1, x2) = x in
              Printf.sprintf "(%s,%s)" (to_string t1 x1) (to_string t2 x2)
</pre><p>
Another frequent application of GADTs is equality witnesses.
</p><pre>        type (_,_) eq = Eq : ('a,'a) eq

        let cast : type a b. (a,b) eq -&gt; a -&gt; b = fun Eq x -&gt; x
</pre><p>Here type <span class="c007">eq</span> has only one constructor, and by matching on it one
adds a local constraint allowing the conversion between <span class="c007">a</span> and <span class="c007">b</span>.
By building such equality witnesses, one can make equal types which
are syntactically different.</p><p>Here is an example using both singleton types and equality witnesses
to implement dynamic types.
</p><pre>        let rec eq_type : type a b. a typ -&gt; b typ -&gt; (a,b) eq option =
          fun a b -&gt;
          match a, b with
          | Int, Int -&gt; Some Eq
          | String, String -&gt; Some Eq
          | Pair(a1,a2), Pair(b1,b2) -&gt;
              begin match eq_type a1 b1, eq_type a2 b2 with
              | Some Eq, Some Eq -&gt; Some Eq
              | _ -&gt; None
              end
          | _ -&gt; None

        type dyn = Dyn : 'a typ * 'a -&gt; dyn

        let get_dyn : type a. a typ -&gt; dyn -&gt; a option =
          fun a (Dyn(b,x)) -&gt;
          match eq_type a b with
          | None -&gt; None
          | Some Eq -&gt; Some x
</pre>
<h2 class="section" id="sec240">21&nbsp;&nbsp;Syntax for Bigarray access</h2>
<p><a id="s:bigarray-access"></a></p><p>(Introduced in Objective Caml 3.00)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.{</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">,</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.{</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">,</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;<span class="c008">}</span>&nbsp;<span class="c008">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>This extension provides syntactic sugar for getting and setting
elements in the arrays provided by the
<span class="c007">Bigarray</span>[<a href="../../api/4.02/Bigarray.html"><span class="c007">Bigarray</span></a>] library.</p><p>The short expressions are translated into calls to functions of the
<span class="c007">Bigarray</span> module as described in the following table.</p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">expression</span></td><td class="c021"><span class="c019">translation</span> </td></tr>
<tr><td class="c023">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">}</span></td><td class="c023"><span class="c007">Bigarray.Array1.get </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c005"><span class="c007">}</span> <span class="c007">&lt;-</span></span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c023"><span class="c007">Bigarray.Array1.set </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub><span class="c008">}</span></td><td class="c023"><span class="c007">Bigarray.Array2.get </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub><span class="c005"><span class="c007">}</span> <span class="c007">&lt;-</span></span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c023"><span class="c007">Bigarray.Array2.set </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>3</sub><span class="c008">}</span></td><td class="c023"><span class="c007">Bigarray.Array3.get </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>3</sub> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub><span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>3</sub><span class="c005"><span class="c007">}</span> <span class="c007">&lt;-</span></span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c023"><span class="c007">Bigarray.Array3.set </span><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>2</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>3</sub> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> …<span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub><span class="c008">}</span></td><td class="c023"><span class="c007">Bigarray.Genarray.get </span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> <span class="c008">[|</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> … <span class="c008">,</span>
&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">|]</span> </td></tr>
<tr><td class="c023"><a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub><span class="c008">.{</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> …<span class="c008">,</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub><span class="c005"><span class="c007">}</span> <span class="c007">&lt;-</span></span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c023"><span class="c007">Bigarray.Genarray.set </span> <a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>0</sub> <span class="c008">[|</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub>1</sub><span class="c008">,</span> … <span class="c008">,</span>
&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">|]</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a> </td></tr>
</tbody></table></div><p>The last two entries are valid for any <span class="c013">n</span> &gt; 3.</p>
<h2 class="section" id="sec241">22&nbsp;&nbsp;Attributes</h2>
<p><a id="s:attributes"></a></p><p>(Introduced in OCaml 4.02)</p><p>Attributes are “decorations” of the syntax tree which are mostly
ignored by the type-checker but can be used by external tools. An
attribute is made of an identifier and a payload, which can be a
structure, a type expression (prefixed with <span class="c007">:</span>) or a pattern
(prefixed with <span class="c007">?</span>) optionally followed by a <span class="c007">when</span> clause:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="attr-id"><span class="c014">attr-id</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="lex.html#lowercase-ident"><span class="c014">lowercase-ident</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<a class="syntax" href="lex.html#capitalized-ident"><span class="c014">capitalized-ident</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="attr-payload"><span class="c014">attr-payload</span></a></td><td class="c022">::=</td><td class="c024">
[&nbsp;<a class="syntax" href="modules.html#module-items"><span class="c014">module-items</span></a>&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The first form of attributes is attached with a postfix notation on
“algebraic” categories:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="attribute"><span class="c014">attribute</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[@</span>&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;&nbsp;<a class="syntax" href="#attr-payload"><span class="c014">attr-payload</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-expr</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-expr"><span class="c014">class-expr</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-type</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-type"><span class="c014">class-type</span></a>&nbsp;&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>This form of attributes can also be inserted after the <span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>
in polymorphic variant type expressions (<a class="syntax" href="types.html#tag-spec-first"><span class="c014">tag-spec-first</span></a>, <a class="syntax" href="types.html#tag-spec"><span class="c014">tag-spec</span></a>,
<a class="syntax" href="types.html#tag-spec-full"><span class="c014">tag-spec-full</span></a>) or after the <a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a> in <a class="syntax" href="types.html#method-type"><span class="c014">method-type</span></a>.</p><p>The same syntactic form is also used to attach attributes to labels and
constructors in type declarations:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<span class="c014">field-decl</span></td><td class="c022">::=</td><td class="c024">
[<span class="c008">mutable</span>]&nbsp;<a class="syntax" href="names.html#field-name"><span class="c014">field-name</span></a>&nbsp;&nbsp;{<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>}&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a></td><td class="c022">::=</td><td class="c024">
(<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;∣&nbsp;&nbsp;<span class="c008">()</span>)&nbsp;{<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>}&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The second form of attributes are attached to “blocks” such as type
declarations, class fields, etc:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="item-attribute"><span class="c014">item-attribute</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[@@</span>&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;&nbsp;<a class="syntax" href="#attr-payload"><span class="c014">attr-payload</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">typedef</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="typedecl.html#typedef"><span class="c014">typedef</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">exception-definition</span></td><td class="c022">::=</td><td class="c024">
<span class="c008">exception</span>&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#attribute"><span class="c014">attribute</span></a>&nbsp;}&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">exception</span>&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">module-items</span></td><td class="c022">::=</td><td class="c024">
[<span class="c008">;;</span>]&nbsp;(&nbsp;<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a>&nbsp;∣&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}&nbsp;)&nbsp;&nbsp;{&nbsp;[<span class="c008">;;</span>]&nbsp;<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a>&nbsp;∣&nbsp;&nbsp;<span class="c008">;;</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}&nbsp;}&nbsp;&nbsp;[<span class="c008">;;</span>]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-binding</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-binding"><span class="c014">class-binding</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-spec</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-spec"><span class="c014">class-spec</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">classtype-def</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#classtype-def"><span class="c014">classtype-def</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">let</span>&nbsp;[<span class="c008">rec</span>]&nbsp;<a class="syntax" href="expr.html#let-binding"><span class="c014">let-binding</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="expr.html#let-binding"><span class="c014">let-binding</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">external</span>&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="intfc.html#external-declaration"><span class="c014">external-declaration</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="typedecl.html#type-definition"><span class="c014">type-definition</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="typedecl.html#exception-definition"><span class="c014">exception-definition</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-definition"><span class="c014">class-definition</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#classtype-definition"><span class="c014">classtype-definition</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">)</span>&nbsp;}
&nbsp;[&nbsp;<span class="c008">:</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;]&nbsp;&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">type</span>&nbsp;<a class="syntax" href="names.html#modtype-name"><span class="c014">modtype-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">open</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">include</span>&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">rec</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">=</span>&nbsp;
&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}&nbsp;
&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;
&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">val</span>&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">external</span>&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="intfc.html#external-declaration"><span class="c014">external-declaration</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="typedecl.html#type-definition"><span class="c014">type-definition</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">exception</span>&nbsp;<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-specification"><span class="c014">class-specification</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#classtype-definition"><span class="c014">classtype-definition</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">)</span>&nbsp;}
<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">type</span>&nbsp;<a class="syntax" href="names.html#modtype-name"><span class="c014">modtype-name</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<span class="c008">type</span>&nbsp;<a class="syntax" href="names.html#modtype-name"><span class="c014">modtype-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">open</span>&nbsp;<a class="syntax" href="names.html#module-path"><span class="c014">module-path</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">include</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-field-spec</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-field-spec"><span class="c014">class-field-spec</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a>&nbsp;&nbsp;<a class="syntax" href="#item-attribute"><span class="c014">item-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A third form of attributes appears as stand-alone structure or
signature items in the module or class sub-languages. They are not
attached to any specific node in the syntax tree:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="floating-attribute"><span class="c014">floating-attribute</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[@@@</span>&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;&nbsp;<a class="syntax" href="#attr-payload"><span class="c014">attr-payload</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#floating-attribute"><span class="c014">floating-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#floating-attribute"><span class="c014">floating-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-field-spec</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#floating-attribute"><span class="c014">floating-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#floating-attribute"><span class="c014">floating-attribute</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>(Note: contrary to what the grammar above describes, <span class="c014">item-attributes</span>
cannot be attached to these floating attributes in <a class="syntax" href="classes.html#class-field-spec"><span class="c014">class-field-spec</span></a>
and <a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a>.)</p><p>It is also possible to specify attributes on expressions using an
infix syntax. This applies to all expressions starting with one or
two keywords: <span class="c007">assert</span>, <span class="c007">begin</span>, <span class="c007">for</span>, <span class="c007">fun</span>, <span class="c007">function</span>, <span class="c007">if</span>,
<span class="c007">lazy</span>, <span class="c007">let</span>, <span class="c007">let module</span>, <span class="c007">let open</span>, <span class="c007">match</span>, <span class="c007">new</span>, <span class="c007">object</span>,
<span class="c007">try</span>, <span class="c007">while</span>. Those expressions supports adding one or several
attributes just after those initial keyword(s). For instance:</p><pre>let [@foo][@bar x] x = 2 in x + 1 === (let x = 2 in x + 1)[@foo][@bar x]
begin[@foo] ... end               === (begin ... end)[@foo]
</pre>
<h3 class="subsection" id="sec242">22.1&nbsp;&nbsp;Built-in attributes</h3>
<p>Some attributes are understood by the type-checker:
</p><ul class="itemize"><li class="li-itemize">
“ocaml.warning” or “warning”, with a string literal payload.
This can be used as floating attributes in a
signature/structure/object/object type. The string is parsed and has
the same effect as the <span class="c007">-w</span> command-line option, in the scope between
the attribute and the end of the current
signature/structure/object/object type. The attribute can also be
used on an expression,
in which case its scope is limited to that expression.
Note that it is not well-defined which scope is used for a specific
warning. This is implementation dependant and can change between versions.
For instance, warnings triggerd by the “ppwarning” attribute (see below)
are issued using the global warning configuration.
</li><li class="li-itemize">“ocaml.warnerror” or “warnerror”, with a string literal payload.
Same as “ocaml.warning”, for the <span class="c007">-warn-error</span> command-line option.
</li><li class="li-itemize">“ocaml.deprecated” or “deprecated”.
Can be applied to most kind of items in signatures or
structures. When the element is later referenced, a warning (3) is
triggered. If the payload of the attribute is a string literal,
the warning message includes this text.
</li><li class="li-itemize">“ocaml.ppwarning” or “ppwarning”, in any context, with
a string literal payload. The text is reported as warning (22)
by the compiler (currently, the warning location is the location
of the string payload). This is mostly useful for preprocessors which
need to communicate warnings to the user. This could also be used
to mark explicitly some code location for further inspection.
</li></ul><pre>module X = struct
  [@@warning "+9"]  (* locally enable warning 9 in this structure *)
  ...
end

let x = begin[@warning "+9] ... end in ....

type t = A | B
  [@@deprecated "Please use type 's' instead.]


let f x =
  assert (x &gt;= 0) [@ppwarning "TODO: remove this later"];
  ....

</pre>
<h2 class="section" id="sec243">23&nbsp;&nbsp;Extension nodes</h2>
<p><a id="s:extension-nodes"></a></p><p>(Introduced in OCaml 4.02)</p><p>Extension nodes are generic placeholders in the syntax tree. They are
rejected by the type-checker and are intended to be “expanded” by external
tools such as <span class="c007">-ppx</span> rewriters.</p><p>Extension nodes share the same notion of identifier and payload as
attributes&nbsp;<a href="#s%3Aattributes">7.22</a>.</p><p>The first form of extension node is used for “algebraic” categories:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="extension"><span class="c014">extension</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[%</span>&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;&nbsp;<a class="syntax" href="#attr-payload"><span class="c014">attr-payload</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-expr</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-type</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#extension"><span class="c014">extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A second form of extension node can be used in structures and
signatures, both in the module and object languages:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="item-extension"><span class="c014">item-extension</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[%%</span>&nbsp;<a class="syntax" href="#attr-id"><span class="c014">attr-id</span></a>&nbsp;&nbsp;<a class="syntax" href="#attr-payload"><span class="c014">attr-payload</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#item-extension"><span class="c014">item-extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#item-extension"><span class="c014">item-extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<span class="c014">class-field-spec</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#item-extension"><span class="c014">item-extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="classes.html#class-field"><span class="c014">class-field</span></a></td><td class="c022">::=</td><td class="c024">
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#item-extension"><span class="c014">item-extension</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>An infix form is available for extension nodes as expressions, when
the payload is a single expression. This form applies to all
expressions starting with one or two keywords: the percent sign and then
and extension identifier follow immediately the initial keyword(s).</p><p>Examples:</p><pre>let%foo x = 2 in x + 1     === [%foo let x = 2 in x + 1]
begin%foo ... end          === [%foo begin ... end]
</pre><p>
When this form is used together with the infix syntax for attributes,
the attributes are considered to apply to the payload:</p><pre>begin%foo[@bar] ... end     === [%foo (let x = 2 in x + 1) [@bar]]
</pre>
<h2 class="section" id="sec244">24&nbsp;&nbsp;Quoted strings</h2>
<p><a id="s:quoted-strings"></a></p><p>(Introduced in OCaml 4.02)</p><p>Quoted strings provide a different lexical syntax to write string
literals in OCaml code. This can be used to embed pieces of foreign
syntax fragments in OCaml code, to be interpret by a <span class="c007">-ppx</span> filter or
just a library.</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<span class="c014">string-literal</span></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="#quoted-string-id"><span class="c014">quoted-string-id</span></a>&nbsp;<span class="c008">|</span>&nbsp;&nbsp;........&nbsp;<span class="c008">|</span>&nbsp;&nbsp;<a class="syntax" href="#quoted-string-id"><span class="c014">quoted-string-id</span></a>&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="quoted-string-id"><span class="c014">quoted-string-id</span></a></td><td class="c022">::=</td><td class="c024">
{&nbsp;<span class="c008">a</span>...<span class="c008">z</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">_</span>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The opening delimiter has the form <span class="c007">{id|</span> where <span class="c007">id</span> is a (possibly
empty) sequence of lowercase letters and underscores. The
corresponding closing delimiter is <span class="c007">|id}</span> (with the same
identifier). Unlike regular OCaml string literals, quoted
strings do not interpret any character in a special way.</p><p>Example:</p><pre>String.length {|\"|}         (* returns 2 *)
String.length {foo|\"|foo}   (* returns 2 *)
</pre>
<h2 class="section" id="sec245">25&nbsp;&nbsp;Exception cases in pattern matching</h2>
<p><a id="s:exception-match"></a></p><p>(Introduced in OCaml 4.02)</p><p>A new form of exception patterns is allowed, only as a toplevel
pattern under a <span class="c007">match</span>...<span class="c007">with</span> pattern-matching (other occurrences
are rejected by the type-checker).</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">exception</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Cases with such a toplevel pattern are called “exception cases”,
as opposed to regular “value cases”. Exception cases are applied
when the evaluation of the matched expression raises an exception.
The exception value is then matched against all the exception cases
and re-raised if none of them accept the exception (as for a
<span class="c007">try</span>...<span class="c007">with</span> block). Since the bodies of all exception and value
cases is outside the scope of the exception handler, they are all
considered to be in tail-position: if the <span class="c007">match</span>...<span class="c007">with</span> block
itself is in tail position in the current function, any function call
in tail position in one of the case bodies results in an actual tail
call.</p><p>It is an error if all cases are exception cases in a given pattern
matching.</p>
<h2 class="section" id="sec246">26&nbsp;&nbsp;Extensible variant types</h2>
<p><a id="s:extensible-variants"></a></p><p>(Introduced in OCaml 4.02)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="typedecl.html#type-representation"><span class="c014">type-representation</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">..</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">type</span>&nbsp;[<a class="syntax" href="typedecl.html#type-params"><span class="c014">type-params</span></a>]&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>&nbsp;&nbsp;<a class="syntax" href="#type-extension-spec"><span class="c014">type-extension-spec</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">type</span>&nbsp;[<a class="syntax" href="typedecl.html#type-params"><span class="c014">type-params</span></a>]&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>&nbsp;&nbsp;<a class="syntax" href="#type-extension-def"><span class="c014">type-extension-def</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-extension-spec"><span class="c014">type-extension-spec</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;<span class="c008">+=</span>&nbsp;[<span class="c008">private</span>]&nbsp;[<span class="c008">|</span>]&nbsp;<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-extension-def"><span class="c014">type-extension-def</span></a></td><td class="c022">::=</td><td class="c024">&nbsp;<span class="c008">+=</span>&nbsp;[<span class="c008">private</span>]&nbsp;[<span class="c008">|</span>]&nbsp;<a class="syntax" href="#constr-def"><span class="c014">constr-def</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="#constr-def"><span class="c014">constr-def</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="constr-def"><span class="c014">constr-def</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="typedecl.html#constr-decl"><span class="c014">constr-decl</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Extensible variant types are variant types which can be extended with
new variant constructors. Extensible variant types are defined using
<span class="c007">..</span>. New variant constructors are added using <span class="c007">+=</span>.
</p><pre>        type attr = ..

        type attr += Str of string

        type attr +=
          | Int of int
          | Float of float
</pre><p>
Pattern matching on an extensible variant type requires a default case
to handle unknown variant constructors:
</p><pre>        let to_string = function
          | Str s -&gt; s
          | Int i -&gt; string_of_int i
          | Float f -&gt; string_of_float f
          | _ -&gt; "?"
</pre><p>
A preexisting example of an extensible variant type is the built-in
<span class="c007">exn</span> type used for exceptions. Indeed, exception constructors can be
declared using the type extension syntax:
</p><pre>        type exn += Exc of int
</pre><p>
Extensible variant constructors can be rebound to a different name. This
allows exporting variants from another module.
</p><pre>        type Expr.attr += Str = Expr.Str
</pre><p>
Extensible variant constructors can be declared <span class="c007">private</span>. As with
regular variants, this prevents them from being constructed directly by
constructor application while still allowing them to be de-structured in
pattern-matching.</p>
<h2 class="section" id="sec247">27&nbsp;&nbsp;Generative functors</h2>
<p><a id="s:generative-functors"></a></p><p>(Introduced in OCaml 4.02)</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">functor</span>&nbsp;<span class="c008">()</span>&nbsp;<span class="c008">-&gt;</span>&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>&nbsp;<span class="c008">()</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">)</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">()</span>&nbsp;}
[&nbsp;<span class="c008">:</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;]&nbsp;&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c014">module-expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">functor</span>&nbsp;<span class="c008">()</span>&nbsp;<span class="c008">-&gt;</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" href="modtypes.html#specification"><span class="c014">specification</span></a></td><td class="c022">::=</td><td class="c024">
...
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c014">module-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>&nbsp;<span class="c008">)</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">()</span>&nbsp;}
<span class="c008">:</span>&nbsp;<a class="syntax" href="modtypes.html#module-type"><span class="c014">module-type</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A generative functor takes a unit <span class="c007">()</span> argument.
In order to use it, one must necessarily apply it to this unit argument,
ensuring that all type components in the result of the functor behave
in a generative way, <em>i.e.</em> they are different from types obtained
by other applications of the same functor.
This is equivalent to taking an argument of signature <span class="c007">sig end</span>, and always
applying to <span class="c007">struct end</span>, but not to some defined module (in the
latter case, applying twice to the same module would return identical
types).</p><p>As a side-effect of this generativity, one is allowed to unpack
first-class modules in the body of generative functors.
</p>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>