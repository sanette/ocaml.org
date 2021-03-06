<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li class="active"><a href="language.html">The OCaml language</a></li><li><a href="extn.html">Language extensions</a></li></ul>




<h1 class="chapter" id="sec59"><span>Chapter 6</span>&nbsp;&nbsp;The OCaml language</h1>
<p> <a id="c:refman"></a>

</p><h3 class="subsection" id="sec60">Foreword</h3>
<p>This document is intended as a reference manual for the OCaml
language. It lists the language constructs, and gives their precise
syntax and informal semantics. It is by no means a tutorial
introduction to the language: there is not a single example. A good
working knowledge of OCaml is assumed.</p><p>No attempt has been made at mathematical rigor: words are employed
with their intuitive meaning, without further definition. As a
consequence, the typing rules have been left out, by lack of the
mathematical framework required to express them, while they are
definitely part of a full formal definition of the language.</p><h3 class="subsection" id="sec61">Notations</h3>
<p>The syntax of the language is given in BNF-like notation. Terminal
symbols are set in typewriter font (<span class="c005"><span class="c007">like</span> <span class="c007">this</span></span>).
Non-terminal symbols are set in italic font (<span class="c014">like</span> &nbsp;<span class="c014">that</span>).
Square brackets […] denote optional components. Curly brackets
{…} denotes zero, one or several repetitions of the enclosed
components. Curly brackets with a trailing plus sign {…}<sup>+</sup>
denote one or several repetitions of the enclosed components.
Parentheses (…) denote grouping.</p><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.02</a></div><div class="toc_title"><a href="#">The OCaml language</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="lex.html#start-section">Lexical conventions</a>
</li><li><a href="values.html#start-section">Values</a>
</li><li><a href="names.html#start-section">Names</a>
</li><li><a href="types.html#start-section">Type expressions</a>
</li><li><a href="const.html#start-section">Constants</a>
</li><li><a href="patterns.html#start-section">Patterns</a>
</li><li><a href="expr.html#start-section">Expressions</a>
</li><li><a href="typedecl.html#start-section">Type and exception definitions</a>
</li><li><a href="classes.html#start-section">Classes</a>
</li><li><a href="modtypes.html#start-section">Module types (module specifications)</a>
</li><li><a href="modules.html#start-section">Module expressions (module implementations)</a>
</li><li><a href="compunit.html#start-section">Compilation units</a>
</li></ul></nav></header><a id="start-section"></a><section id="section">




<h2 class="section" id="s:value-expr">7&nbsp;&nbsp;Expressions</h2>
<ul>
<li><a href="expr.html#sec116">Basic expressions</a>
</li><li><a href="expr.html#sec124">Control structures</a>
</li><li><a href="expr.html#sec131">Operations on data structures</a>
</li><li><a href="expr.html#sec138">Operators</a>
</li><li><a href="expr.html#sec139">Objects</a>
</li><li><a href="expr.html#sec145">Coercions</a>
</li></ul>
<p>
<a id="hevea_manual.kwd8"></a>
<a id="hevea_manual.kwd9"></a>
<a id="hevea_manual.kwd10"></a>
<a id="hevea_manual.kwd11"></a>
<a id="hevea_manual.kwd12"></a>
<a id="hevea_manual.kwd13"></a>
<a id="hevea_manual.kwd14"></a>
<a id="hevea_manual.kwd15"></a>
<a id="hevea_manual.kwd16"></a>
<a id="hevea_manual.kwd17"></a>
<a id="hevea_manual.kwd18"></a>
<a id="hevea_manual.kwd19"></a>
<a id="hevea_manual.kwd20"></a>
<a id="hevea_manual.kwd21"></a>
<a id="hevea_manual.kwd22"></a>
<a id="hevea_manual.kwd23"></a>
<a id="hevea_manual.kwd24"></a>
<a id="hevea_manual.kwd25"></a>
<a id="hevea_manual.kwd26"></a>
<a id="hevea_manual.kwd27"></a>
<a id="hevea_manual.kwd28"></a>
<a id="hevea_manual.kwd29"></a>
<a id="hevea_manual.kwd30"></a>
<a id="hevea_manual.kwd31"></a></p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="expr"><span class="c014">expr</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="names.html#value-path"><span class="c014">value-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="const.html#constant"><span class="c014">constant</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">begin</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">end</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{<span class="c008">,</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>}<sup>+</sup>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">::</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">[</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">[|</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">|]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">with</span>&nbsp;&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a>&nbsp;}<sup>+</sup>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#prefix-symbol"><span class="c014">prefix-symbol</span></a>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">-</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">-.</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;<a class="syntax" href="names.html#infix-op"><span class="c014">infix-op</span></a>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a>&nbsp;<span class="c008">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.(</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.(</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">)</span>&nbsp;<span class="c008">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.[</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">.[</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">]</span>&nbsp;<span class="c008">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">if</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">then</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;[&nbsp;<span class="c008">else</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">while</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">do</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">done</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">for</span>&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;(&nbsp;<span class="c008">to</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">downto</span>&nbsp;)&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">do</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">done</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">;</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">match</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">with</span>&nbsp;&nbsp;<a class="syntax" href="#pattern-matching"><span class="c014">pattern-matching</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">function</span>&nbsp;<a class="syntax" href="#pattern-matching"><span class="c014">pattern-matching</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">fun</span>&nbsp;<a class="syntax" href="#multiple-matching"><span class="c014">multiple-matching</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">try</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">with</span>&nbsp;&nbsp;<a class="syntax" href="#pattern-matching"><span class="c014">pattern-matching</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">let</span>&nbsp;[<span class="c008">rec</span>]&nbsp;<a class="syntax" href="#let-binding"><span class="c014">let-binding</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="#let-binding"><span class="c014">let-binding</span></a>&nbsp;}&nbsp;<span class="c008">in</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">new</span>&nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">object</span>&nbsp;<a class="syntax" href="classes.html#class-body"><span class="c014">class-body</span></a>&nbsp;<span class="c008">end</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">#</span>&nbsp;&nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>&nbsp;<span class="c008">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">:&gt;</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">:&gt;</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">{&lt;</span>&nbsp;[&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;]&nbsp;<span class="c008">&gt;}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="argument"><span class="c014">argument</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">~</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">~</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="pattern-matching"><span class="c014">pattern-matching</span></a></td><td class="c022">::=</td><td class="c024">
[&nbsp;<span class="c008">|</span>&nbsp;]&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>]&nbsp;<span class="c008">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>]&nbsp;<span class="c008">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="multiple-matching"><span class="c014">multiple-matching</span></a></td><td class="c022">::=</td><td class="c024">
{&nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a>&nbsp;}<sup>+</sup>&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>]&nbsp;<span class="c008">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="let-binding"><span class="c014">let-binding</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#value-name"><span class="c014">value-name</span></a>&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;&nbsp;[<span class="c008">:&gt;</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="parameter"><span class="c014">parameter</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">~</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">~</span>&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">~</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>]&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">?</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;<span class="c008">(</span>&nbsp;&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a>&nbsp;&nbsp;[<span class="c008">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>]&nbsp;&nbsp;[<span class="c008">=</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>]&nbsp;<span class="c008">)</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The table below shows the relative precedences and associativity of
operators and non-closed constructions. The constructions with higher
precedence come first. For infix and prefix symbols, we write
“<span class="c007">*</span>…” to mean “any symbol starting with <span class="c007">*</span>”.
<a id="hevea_manual.kwd32"></a><a id="hevea_manual.kwd33"></a><a id="hevea_manual.kwd34"></a><a id="hevea_manual.kwd35"></a><a id="hevea_manual.kwd36"></a><a id="hevea_manual.kwd37"></a><a id="hevea_manual.kwd38"></a></p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">Construction or operator</span></td><td class="c021"><span class="c019">Associativity</span> </td></tr>
<tr><td class="c023">
prefix-symbol</td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">.   .(   .[   .{</span> (see section&nbsp;<a href="extn.html#s%3Abigarray-access">7.21</a>)</td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">#</span></td><td class="c023">– </td></tr>
<tr><td class="c023">function application, constructor application, tag
application, <span class="c007">assert</span> (see&nbsp;<a href="extn.html#s%3Aassert">7.5</a>),
<span class="c007">lazy</span> (see&nbsp;<a href="extn.html#s%3Alazy">7.6</a>)</td><td class="c023">left </td></tr>
<tr><td class="c023"><span class="c007">-   -.</span> (prefix)</td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">**</span>…<span class="c007">   lsl   lsr   asr</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">*</span>…<span class="c007">   /</span>…<span class="c007">   %</span>…<span class="c007">   mod   land   lor   lxor</span></td><td class="c023">left </td></tr>
<tr><td class="c023"> <span class="c007">+</span>…<span class="c007">   -</span>…</td><td class="c023">left </td></tr>
<tr><td class="c023"><span class="c007">::</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">@</span>…<span class="c007">   ^</span>…</td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">=</span>…<span class="c007">   &lt;</span>…<span class="c007">   &gt;</span>…<span class="c007">   |</span>…<span class="c007">   &amp;</span>…<span class="c007">   $</span>…<span class="c007">   !=</span></td><td class="c023">left </td></tr>
<tr><td class="c023"><span class="c007">&amp;   &amp;&amp;</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">or  ||</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">,</span></td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">&lt;-   :=</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">if</span></td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">;</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">let  match  fun  function  try</span></td><td class="c023">– </td></tr>
</tbody></table></div>
<h3 class="subsection" id="sec116">7.1&nbsp;&nbsp;Basic expressions</h3>
<h4 class="subsubsection" id="sec117">Constants</h4>
<p>An expression consisting in a constant evaluates to this constant.</p><h4 class="subsubsection" id="sec118">Value paths</h4>
<p> <a id="expr:var"></a></p><p>An expression consisting in an access path evaluates to the value bound to
this path in the current evaluation environment. The path can
be either a value name or an access path to a value component of a module.</p><h4 class="subsubsection" id="sec119">Parenthesized expressions</h4>
<p>
<a id="hevea_manual.kwd39"></a>
<a id="hevea_manual.kwd40"></a></p><p>The expressions <span class="c008">(</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">)</span> and <span class="c008">begin</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">end</span> have the same
value as <a class="syntax" href="#expr"><span class="c014">expr</span></a>. The two constructs are semantically equivalent, but it
is good style to use <span class="c008">begin</span> … <span class="c008">end</span> inside control structures:
</p><pre>        if … then begin … ; … end else begin … ; … end
</pre><p>
and <span class="c008">(</span> … <span class="c008">)</span> for the other grouping situations.</p><p>Parenthesized expressions can contain a type constraint, as in <span class="c008">(</span>
<a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> <span class="c008">)</span>. This constraint forces the type of <a class="syntax" href="#expr"><span class="c014">expr</span></a> to be
compatible with <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>.</p><p>Parenthesized expressions can also contain coercions
<span class="c008">(</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a> &nbsp;[<span class="c008">:</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>] <span class="c008">:&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><span class="c008">)</span> (see
subsection&nbsp;<a href="#s%3Acoercions">6.7.6</a> below).</p><h4 class="subsubsection" id="sec120">Function application</h4>
<p>Function application is denoted by juxtaposition of (possibly labeled)
expressions. The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> &nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub><span class="c013">n</span></sub>
evaluates the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> and those appearing in <a class="syntax" href="#argument"><span class="c014">argument</span></a><sub>1</sub>
to <a class="syntax" href="#argument"><span class="c014">argument</span></a><sub><span class="c013">n</span></sub>. The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> must evaluate to a
functional value <span class="c013">f</span>, which is then applied to the values of
<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub><span class="c013">n</span></sub>.</p><p>The order in which the expressions <a class="syntax" href="#expr"><span class="c014">expr</span></a>, &nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub>1</sub>, …,
&nbsp;<a class="syntax" href="#argument"><span class="c014">argument</span></a><sub><span class="c013">n</span></sub> are evaluated is not specified.</p><p>Arguments and parameters are matched according to their respective
labels. Argument order is irrelevant, except among arguments with the
same label, or no label.</p><p>If a parameter is specified as optional (label prefixed by <span class="c008">?</span>) in the
type of <a class="syntax" href="#expr"><span class="c014">expr</span></a>, the corresponding argument will be automatically
wrapped with the constructor <span class="c007">Some</span>, except if the argument itself is
also prefixed by <span class="c008">?</span>, in which case it is passed as is.
If a non-labeled argument is passed, and its corresponding parameter
is preceded by one or several optional parameters, then these
parameters are <em>defaulted</em>, <em>i.e.</em> the value <span class="c007">None</span> will be
passed for them.
All other missing parameters (without corresponding argument), both
optional and non-optional, will be kept, and the result of the
function will still be a function of these missing parameters to the
body of <span class="c013">f</span>.</p><p>As a special case, if the function has a known arity, all the
arguments are unlabeled, and their number matches the number of
non-optional parameters, then labels are ignored and non-optional
parameters are matched in their definition order. Optional arguments
are defaulted.</p><p>In all cases but exact match of order and labels, without optional
parameters, the function type should be known at the application
point. This can be ensured by adding a type constraint. Principality
of the derivation can be checked in the <span class="c007">-principal</span> mode.</p><h4 class="subsubsection" id="sec121">Function definition</h4>
<p>Two syntactic forms are provided to define functions. The first form
is introduced by the keyword <span class="c007">function</span>:
<a id="hevea_manual.kwd41"></a></p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025"><span class="c008">function</span></td><td class="c024"><span class="c018">pattern</span><sub>1</sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub>1</sub>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024">…&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024"><span class="c018">pattern</span><sub><span class="c013">n</span></sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub><span class="c013">n</span></sub>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>
This expression evaluates to a functional value with one argument.
When this function is applied to a value <span class="c013">v</span>, this value is
matched against each pattern <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> to <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>.
If one of these matchings succeeds, that is, if the value <span class="c013">v</span>
matches the pattern <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">i</span></sub> for some <span class="c013">i</span>,
then the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> associated to the selected pattern
is evaluated, and its value becomes the value of the function
application. The evaluation of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> takes place in an
environment enriched by the bindings performed during the matching.</p><p>If several patterns match the argument <span class="c013">v</span>, the one that occurs
first in the function definition is selected. If none of the patterns
matches the argument, the exception <span class="c007">Match_failure</span> is raised.
<a id="hevea_manual0"></a></p><p><br>
</p><p>The other form of function definition is introduced by the keyword <span class="c007">fun</span>:
<a id="hevea_manual.kwd42"></a>
</p><div class="center">
<span class="c008">fun</span> <a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub><span class="c013">n</span></sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
This expression is equivalent to:
</p><div class="center">
<span class="c008">fun</span> <a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub>1</sub> <span class="c008">-&gt;</span> … <span class="c008">fun</span> &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub><span class="c013">n</span></sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>The parameter patterns <span class="c008">~</span><a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> and <span class="c008">~(</span><a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> &nbsp;[<span class="c008">:</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>]<span class="c008">)</span>
are shorthands for respectively <span class="c008">~</span><a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a><span class="c008">:</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> and
<span class="c008">~</span><a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a><span class="c008">:(</span>&nbsp;<a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> &nbsp;[<span class="c008">:</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>]<span class="c008">)</span>, and similarly for their optional
counterparts.</p><p>A function of the form <span class="c005"><span class="c007">fun</span> <span class="c007">?</span></span> <a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> <span class="c008">:(</span> &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>0</sub> <span class="c005"><span class="c007">)</span> <span class="c007">-&gt;</span></span>
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> is equivalent to
</p><div class="center">
<span class="c005"><span class="c007">fun</span> <span class="c007">?</span></span> <a class="syntax" href="lex.html#label-name"><span class="c014">lab</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c005"><span class="c007">-&gt;</span>
<span class="c007">let</span></span> &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a> <span class="c005"><span class="c007">=</span>
<span class="c007">match</span></span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c005"><span class="c007">with</span> <span class="c007">Some</span></span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c005"><span class="c007">|</span> <span class="c007">None</span> <span class="c007">-&gt;</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>0</sub>
<span class="c008">in</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
where <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>
is a fresh variable, except that it is unspecified when <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>0</sub> is evaluated.</p><p>After these two transformations, expressions are of the form
</p><div class="center">
<span class="c008">fun</span> [<a class="syntax" href="lex.html#label"><span class="c014">label</span></a><sub>1</sub>] &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> <span class="c008">-&gt;</span> … <span class="c008">fun</span> &nbsp;[<a class="syntax" href="lex.html#label"><span class="c014">label</span></a><sub><span class="c013">n</span></sub>] &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
If we ignore labels, which will only be meaningful at function
application, this is equivalent to
</p><div class="center">
<span class="c008">function</span> <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> <span class="c008">-&gt;</span> … <span class="c008">function</span> &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
That is, the <span class="c008">fun</span> expression above evaluates to a curried function
with <span class="c013">n</span> arguments: after applying this function <span class="c013">n</span> times to the
values <span class="c014">v</span><sub>1</sub> … <span class="c014">v</span><sub><span class="c013">n</span></sub>, the values will be matched
in parallel against the patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>.
If the matching succeeds, the function returns the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a> in
an environment enriched by the bindings performed during the matchings.
If the matching fails, the exception <span class="c007">Match_failure</span> is raised.</p><h4 class="subsubsection" id="sec122">Guards in pattern-matchings</h4>
<p><a id="hevea_manual.kwd43"></a>
The cases of a pattern matching (in the <span class="c008">function</span>, <span class="c008">fun</span>, <span class="c008">match</span> and
<span class="c008">try</span> constructs) can include guard expressions, which are
arbitrary boolean expressions that must evaluate to <span class="c007">true</span> for the
match case to be selected. Guards occur just before the <span class="c008">-&gt;</span> token and
are introduced by the <span class="c008">when</span> keyword:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025"><span class="c008">function</span></td><td class="c024"><span class="c014">pattern</span><sub>1</sub>&nbsp;&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;&nbsp;&nbsp;<span class="c014">cond</span><sub>1</sub>]</td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c014">expr</span><sub>1</sub>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024">…&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024"><span class="c014">pattern</span><sub><span class="c013">n</span></sub>&nbsp;&nbsp;&nbsp;&nbsp;[<span class="c008">when</span>&nbsp;&nbsp;&nbsp;<span class="c014">cond</span><sub><span class="c013">n</span></sub>]</td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c014">expr</span><sub><span class="c013">n</span></sub>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Matching proceeds as described before, except that if the value
matches some pattern <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">i</span></sub> which has a guard <span class="c014">cond</span><sub><span class="c013">i</span></sub>, then the
expression <span class="c014">cond</span><sub><span class="c013">i</span></sub> is evaluated (in an environment enriched by the
bindings performed during matching). If <span class="c014">cond</span><sub><span class="c013">i</span></sub> evaluates to <span class="c007">true</span>,
then <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> is evaluated and its value returned as the result of the
matching, as usual. But if <span class="c014">cond</span><sub><span class="c013">i</span></sub> evaluates to <span class="c007">false</span>, the matching
is resumed against the patterns following <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">i</span></sub>.</p><h4 class="subsubsection" id="sec123">Local definitions</h4>
<p> <a id="s:localdef"></a></p><p><a id="hevea_manual.kwd44"></a></p><p>The <span class="c008">let</span> and <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> constructs bind value names locally.
The construct
</p><div class="center">
<span class="c008">let</span> <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">and</span> … <span class="c008">and</span> &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">in</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
evaluates <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> in some unspecified order and matches
their values against the patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>. If the
matchings succeed, <a class="syntax" href="#expr"><span class="c014">expr</span></a> is evaluated in the environment enriched by
the bindings performed during matching, and the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a> is
returned as the value of the whole <span class="c008">let</span> expression. If one of the
matchings fails, the exception <span class="c007">Match_failure</span> is raised.
<a id="hevea_manual1"></a></p><p>An alternate syntax is provided to bind variables to functional
values: instead of writing
</p><div class="center">
<span class="c008">let</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c005"><span class="c007">=</span> <span class="c007">fun</span></span> &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub><span class="c013">m</span></sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
in a <span class="c008">let</span> expression, one may instead write
</p><div class="center">
<span class="c008">let</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#parameter"><span class="c014">parameter</span></a><sub><span class="c013">m</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p><br>
Recursive definitions of names are introduced by <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span>:
</p><div class="center">
<span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">and</span> … <span class="c008">and</span> &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>
<span class="c008">in</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
The only difference with the <span class="c008">let</span> construct described above is
that the bindings of names to values performed by the
pattern-matching are considered already performed when the expressions
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> are evaluated. That is, the expressions <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>
to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> can reference identifiers that are bound by one of the
patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>, and expect them to have the
same value as in <a class="syntax" href="#expr"><span class="c014">expr</span></a>, the body of the <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> construct.</p><p>The recursive definition is guaranteed to behave as described above if
the expressions <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> are function definitions
(<span class="c008">fun</span> … or <span class="c008">function</span> …), and the patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub>
… &nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub> are just value names, as in:
</p><div class="center">
<span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> <span class="c014">name</span><sub>1</sub> <span class="c005"><span class="c007">=</span> <span class="c007">fun</span></span> …
<span class="c008">and</span> …
<span class="c008">and</span> &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub> <span class="c005"><span class="c007">=</span> <span class="c007">fun</span></span> …
<span class="c008">in</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>
</div><p>
This defines <span class="c014">name</span><sub>1</sub> … &nbsp;<span class="c014">name</span><sub><span class="c013">n</span></sub> as mutually recursive functions
local to <a class="syntax" href="#expr"><span class="c014">expr</span></a>.</p><p>The behavior of other forms of <span class="c005"><span class="c007">let</span> <span class="c007">rec</span></span> definitions is
implementation-dependent. The current implementation also supports
a certain class of recursive definitions of non-functional values,
as explained in section&nbsp;<a href="extn.html#s%3Aletrecvalues">7.3</a>.</p>
<h3 class="subsection" id="sec124">7.2&nbsp;&nbsp;Control structures</h3>
<h4 class="subsubsection" id="sec125">Sequence</h4>
<p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> first, then
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>, and returns the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>.</p><h4 class="subsubsection" id="sec126">Conditional</h4>
<p>
<a id="hevea_manual.kwd45"></a></p><p>The expression <span class="c008">if</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">then</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">else</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> evaluates to
the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> if <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> evaluates to the boolean <span class="c008">true</span>,
and to the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> if <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> evaluates to the boolean
<span class="c008">false</span>.</p><p>The <span class="c008">else</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> part can be omitted, in which case it defaults to
<span class="c005"><span class="c007">else</span> <span class="c007">()</span></span>.</p><h4 class="subsubsection" id="sec127">Case expression</h4>
<p><a id="hevea_manual.kwd46"></a></p><p>The expression
</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025"><span class="c008">match</span></td><td class="c024"><span class="c018">expr</span>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">with</span></td><td class="c024"><span class="c018">pattern</span><sub>1</sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub>1</sub>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024">…&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024"><span class="c018">pattern</span><sub><span class="c013">n</span></sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub><span class="c013">n</span></sub>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>
matches the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a> against the patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> to
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>. If the matching against <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">i</span></sub> succeeds, the
associated expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> is evaluated, and its value becomes the
value of the whole <span class="c008">match</span> expression. The evaluation of
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> takes place in an environment enriched by the bindings
performed during matching. If several patterns match the value of
<a class="syntax" href="#expr"><span class="c014">expr</span></a>, the one that occurs first in the <span class="c008">match</span> expression is
selected. If none of the patterns match the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a>, the
exception <span class="c007">Match_failure</span> is raised.
<a id="hevea_manual2"></a></p><h4 class="subsubsection" id="sec128">Boolean operators</h4>
<p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">&amp;&amp;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates to <span class="c008">true</span> if both
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> and <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluate to <span class="c008">true</span>; otherwise, it evaluates to
<span class="c008">false</span>. The first component, <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, is evaluated first. The
second component, <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>, is not evaluated if the first component
evaluates to <span class="c008">false</span>. Hence, the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">&amp;&amp;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> behaves
exactly as
</p><div class="center">
<span class="c008">if</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">then</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c005"><span class="c007">else</span> <span class="c007">false</span></span>.
</div><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">||</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates to <span class="c008">true</span> if one of
the expressions
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> and <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates to <span class="c008">true</span>; otherwise, it evaluates to
<span class="c008">false</span>. The first component, <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, is evaluated first. The
second component, <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>, is not evaluated if the first component
evaluates to <span class="c008">true</span>. Hence, the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">||</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> behaves
exactly as
</p><div class="center">
<span class="c008">if</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c005"><span class="c007">then</span> <span class="c007">true</span> <span class="c007">else</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>.
</div><p><a id="hevea_manual.kwd47"></a>
The boolean operators <span class="c008">&amp;</span> and <span class="c008">or</span> are deprecated synonyms for
(respectively) <span class="c008">&amp;&amp;</span> and <span class="c008">||</span>.</p><h4 class="subsubsection" id="sec129">Loops</h4>
<p><a id="hevea_manual.kwd48"></a>
The expression <span class="c008">while</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">do</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">done</span> repeatedly
evaluates <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> while <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> evaluates to <span class="c008">true</span>. The loop
condition <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> is evaluated and tested at the beginning of each
iteration. The whole <span class="c008">while</span> … <span class="c008">done</span> expression evaluates to
the unit value <span class="c008">()</span>.</p><p><a id="hevea_manual.kwd49"></a>
The expression <span class="c005"><span class="c007">for</span> <span class="c014">name</span> <span class="c007">=</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">to</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">do</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> <span class="c008">done</span>
first evaluates the expressions <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> and <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> (the boundaries)
into integer values <span class="c013">n</span> and <span class="c013">p</span>. Then, the loop body <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> is
repeatedly evaluated in an environment where <span class="c014">name</span> is successively
bound to the values
<span class="c013">n</span>, <span class="c013">n</span>+1, …, <span class="c013">p</span>−1, <span class="c013">p</span>.
The loop body is never evaluated if <span class="c013">n</span> &gt; <span class="c013">p</span>.</p><p>The expression <span class="c005"><span class="c007">for</span> <span class="c014">name</span> <span class="c007">=</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">downto</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">do</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> <span class="c008">done</span>
evaluates similarly, except that <span class="c014">name</span> is successively bound to the values
<span class="c013">n</span>, <span class="c013">n</span>−1, …, <span class="c013">p</span>+1, <span class="c013">p</span>.
The loop body is never evaluated if <span class="c013">n</span> &lt; <span class="c013">p</span>.</p><p>In both cases, the whole <span class="c008">for</span> expression evaluates to the unit
value <span class="c008">()</span>.</p><h4 class="subsubsection" id="sec130">Exception handling</h4>
<p>
<a id="hevea_manual.kwd50"></a></p><p>The expression
</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025"><span class="c008">try&nbsp;</span></td><td class="c024"><span class="c018">expr</span>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">with</span></td><td class="c024"><span class="c018">pattern</span><sub>1</sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub>1</sub>&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024">…&nbsp;</td></tr>
<tr><td class="c025"><span class="c008">|</span></td><td class="c024"><span class="c018">pattern</span><sub><span class="c013">n</span></sub></td><td class="c024"><span class="c008">-&gt;</span></td><td class="c024"><span class="c018">expr</span><sub><span class="c013">n</span></sub>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>
evaluates the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> and returns its value if the
evaluation of <a class="syntax" href="#expr"><span class="c014">expr</span></a> does not raise any exception. If the evaluation
of <a class="syntax" href="#expr"><span class="c014">expr</span></a> raises an exception, the exception value is matched against
the patterns <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub>1</sub> to <a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">n</span></sub>. If the matching against
<a class="syntax" href="patterns.html#pattern"><span class="c014">pattern</span></a><sub><span class="c013">i</span></sub> succeeds, the associated expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> is evaluated,
and its value becomes the value of the whole <span class="c008">try</span> expression. The
evaluation of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> takes place in an environment enriched by the
bindings performed during matching. If several patterns match the value of
<a class="syntax" href="#expr"><span class="c014">expr</span></a>, the one that occurs first in the <span class="c008">try</span> expression is
selected. If none of the patterns matches the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a>, the
exception value is raised again, thereby transparently “passing
through” the <span class="c008">try</span> construct.</p>
<h3 class="subsection" id="sec131">7.3&nbsp;&nbsp;Operations on data structures</h3>
<h4 class="subsubsection" id="sec132">Products</h4>
<p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">,</span> … <span class="c008">,</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> evaluates to the
<span class="c013">n</span>-tuple of the values of expressions <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>. The
evaluation order of the subexpressions is not specified.</p><h4 class="subsubsection" id="sec133">Variants</h4>
<p>The expression <a class="syntax" href="names.html#constr"><span class="c014">constr</span></a> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> evaluates to the unary variant value
whose constructor is <a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>, and whose argument is the value of
<a class="syntax" href="#expr"><span class="c014">expr</span></a>. Similarly, the expression <a class="syntax" href="names.html#constr"><span class="c014">constr</span></a> <span class="c008">(</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">,</span> … <span class="c008">,</span>
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">)</span> evaluates to the n-ary variant value whose constructor is
<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a> and whose arguments are the values of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, …,
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>.</p><p>The expression <a class="syntax" href="names.html#constr"><span class="c014">constr</span></a> <span class="c008">(</span>&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub><span class="c008">)</span> evaluates to the
variant value whose constructor is <a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>, and whose arguments are
the values of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>.</p><p>For lists, some syntactic sugar is provided. The expression
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">::</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> stands for the constructor <span class="c005"><span class="c007">(</span> <span class="c007">::</span> <span class="c007">)</span></span> 
applied to the arguments <span class="c008">(</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">,</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">)</span>, and therefore
evaluates to the list whose head is the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> and whose tail
is the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>. The expression <span class="c008">[</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span>
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">]</span> is equivalent to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">::</span> … <span class="c008">::</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c005"><span class="c007">::</span>
<span class="c007">[]</span></span>, and therefore evaluates to the list whose elements are the
values of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>.</p><h4 class="subsubsection" id="sec134">Polymorphic variants</h4>
<p>The expression <span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> evaluates to the polymorphic variant
value whose tag is <a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>, and whose argument is the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a>.</p><h4 class="subsubsection" id="sec135">Records</h4>
<p>The expression <span class="c008">{</span> <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">n</span></sub> <span class="c008">=</span>
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">}</span> evaluates to the record value
{ <span class="c013">field</span><sub>1</sub> = <span class="c013">v</span><sub>1</sub>; …; <span class="c013">field</span><sub><span class="c013">n</span></sub> = <span class="c013">v</span><sub><span class="c013">n</span></sub> }
where <span class="c013">v</span><sub><span class="c013">i</span></sub> is the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">i</span></sub> for <span class="c013">i</span> = 1,… , <span class="c013">n</span>.
The fields <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> to <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">n</span></sub> must all belong to the same record
type; each field of this record type must appear exactly
once in the record expression, though they can appear in any
order. The order in which <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> are evaluated is not
specified.</p><p>The expression
<span class="c008">{</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">with</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">n</span></sub> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">}</span>
builds a fresh record with fields <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">n</span></sub> equal to
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>, and all other fields having the same value as
in the record <a class="syntax" href="#expr"><span class="c014">expr</span></a>. In other terms, it returns a shallow copy of
the record <a class="syntax" href="#expr"><span class="c014">expr</span></a>, except for the fields <a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a><sub><span class="c013">n</span></sub>,
which are initialized to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub>.</p><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a> evaluates <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to a record
value, and returns the value associated to <a class="syntax" href="names.html#field"><span class="c014">field</span></a> in this record
value.</p><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a> <span class="c008">&lt;-</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to a record
value, which is then modified in-place by replacing the value
associated to <a class="syntax" href="names.html#field"><span class="c014">field</span></a> in this record by the value of
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>. This operation is permitted only if <a class="syntax" href="names.html#field"><span class="c014">field</span></a> has been
declared <span class="c008">mutable</span> in the definition of the record type. The whole
expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.</span> &nbsp;<a class="syntax" href="names.html#field"><span class="c014">field</span></a> <span class="c008">&lt;-</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> evaluates to the unit value
<span class="c008">()</span>.</p><h4 class="subsubsection" id="sec136">Arrays</h4>
<p>The expression <span class="c008">[|</span> <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> <span class="c008">|]</span> evaluates to
a <span class="c013">n</span>-element array, whose elements are initialized with the values of
<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> to <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub><span class="c013">n</span></sub> respectively. The order in which these
expressions are evaluated is unspecified.</p><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.(</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">)</span> returns the value of element
number <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> in the array denoted by <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>. The first element
has number 0; the last element has number <span class="c013">n</span>−1, where <span class="c013">n</span> is the
size of the array. The exception <span class="c007">Invalid_argument</span> is raised if the
access is out of bounds.</p><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.(</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c005"><span class="c007">)</span> <span class="c007">&lt;-</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> modifies in-place
the array denoted by <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, replacing element number <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> by
the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub>. The exception <span class="c007">Invalid_argument</span> is raised if
the access is out of bounds. The value of the whole expression is <span class="c008">()</span>.</p><h4 class="subsubsection" id="sec137">Strings</h4>
<p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.[</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c008">]</span> returns the value of character
number <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> in the string denoted by <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>. The first character
has number 0; the last character has number <span class="c013">n</span>−1, where <span class="c013">n</span> is the
length of the string. The exception <span class="c007">Invalid_argument</span> is raised if the
access is out of bounds.</p><p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> <span class="c008">.[</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> <span class="c005"><span class="c007">]</span> <span class="c007">&lt;-</span></span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub> modifies in-place
the string denoted by <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub>, replacing character number <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> by
the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>3</sub>. The exception <span class="c007">Invalid_argument</span> is raised if
the access is out of bounds. The value of the whole expression is <span class="c008">()</span>.</p><p><span class="c019">Note:</span> this possibility is offered only for backward
compatibility with older versions of OCaml and will be removed in a
future version. New code should use byte sequences and the <span class="c007">Bytes.set</span>
function.</p>
<h3 class="subsection" id="sec138">7.4&nbsp;&nbsp;Operators</h3>
<p>Symbols from the class <a class="syntax" href="lex.html#infix-symbol"><span class="c014">infix-symbol</span></a>, as well as the keywords
<span class="c008">*</span>, <span class="c008">+</span>, <span class="c008">-</span>, <span class="c008">-.</span>, <span class="c008">=</span>, <span class="c008">!=</span>, <span class="c008">&lt;</span>, <span class="c008">&gt;</span>, <span class="c008">or</span>, <span class="c008">||</span>,
<span class="c008">&amp;</span>, <span class="c008">&amp;&amp;</span>, <span class="c008">:=</span>, <span class="c008">mod</span>, <span class="c008">land</span>, <span class="c008">lor</span>, <span class="c008">lxor</span>, <span class="c008">lsl</span>, <span class="c008">lsr</span>,
and <span class="c008">asr</span> can appear in infix position (between two
expressions). Symbols from the class <a class="syntax" href="lex.html#prefix-symbol"><span class="c014">prefix-symbol</span></a>, as well as
the keywords <span class="c008">-</span> and <span class="c008">-.</span>
can appear in prefix position (in front of an expression).</p><p>Infix and prefix symbols do not have a fixed meaning: they are simply
interpreted as applications of functions bound to the names
corresponding to the symbols. The expression <a class="syntax" href="lex.html#prefix-symbol"><span class="c014">prefix-symbol</span></a> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> is
interpreted as the application <span class="c008">(</span> <a class="syntax" href="lex.html#prefix-symbol"><span class="c014">prefix-symbol</span></a> <span class="c008">)</span>
&nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a>. Similarly, the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="lex.html#infix-symbol"><span class="c014">infix-symbol</span></a> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub> is
interpreted as the application <span class="c008">(</span> <a class="syntax" href="lex.html#infix-symbol"><span class="c014">infix-symbol</span></a> <span class="c008">)</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>1</sub> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a><sub>2</sub>.</p><p>The table below lists the symbols defined in the initial environment
and their initial meaning. (See the description of the core
library module <span class="c007">Pervasives</span> in chapter&nbsp;<a href="core.html#c%3Acorelib">20</a> for more
details). Their meaning may be changed at any time using
<span class="c005"><span class="c007">let</span> <span class="c007">(</span></span> <a class="syntax" href="names.html#infix-op"><span class="c014">infix-op</span></a> <span class="c008">)</span> &nbsp;<span class="c014">name</span><sub>1</sub> &nbsp;<span class="c014">name</span><sub>2</sub> <span class="c008">=</span> …</p><p>Note: the operators <span class="c008">&amp;&amp;</span>, <span class="c008">||</span>, and <span class="c008">~-</span> are handled specially
and it is not advisable to change their meaning.</p><p>The keywords <span class="c008">-</span> and <span class="c008">-.</span> can appear both as infix and
prefix operators. When they appear as prefix operators, they are
interpreted respectively as the functions <span class="c008">(~-)</span> and <span class="c008">(~-.)</span>.</p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">Operator</span></td><td class="c021"><span class="c019">Initial meaning</span> </td></tr>
<tr><td class="c029">
<span class="c007">+</span></td><td class="c028">Integer addition. </td></tr>
<tr><td class="c029"><span class="c007">-</span> (infix)</td><td class="c028">Integer subtraction. </td></tr>
<tr><td class="c029"><span class="c007">~-   -</span> (prefix)</td><td class="c028">Integer negation. </td></tr>
<tr><td class="c029"><span class="c007">*</span></td><td class="c028">Integer multiplication. </td></tr>
<tr><td class="c029"><span class="c007">/</span></td><td class="c028">Integer division.
Raise <span class="c007">Division_by_zero</span> if second argument is zero. </td></tr>
<tr><td class="c029"><span class="c007">mod</span></td><td class="c028">Integer modulus. Raise
<span class="c007">Division_by_zero</span> if second argument is zero. </td></tr>
<tr><td class="c029"><span class="c007">land</span></td><td class="c028">Bitwise logical “and” on integers. </td></tr>
<tr><td class="c029"><span class="c007">lor</span></td><td class="c028">Bitwise logical “or” on integers. </td></tr>
<tr><td class="c029"><span class="c007">lxor</span></td><td class="c028">Bitwise logical “exclusive or” on integers. </td></tr>
<tr><td class="c029"><span class="c007">lsl</span></td><td class="c028">Bitwise logical shift left on integers. </td></tr>
<tr><td class="c029"><span class="c007">lsr</span></td><td class="c028">Bitwise logical shift right on integers. </td></tr>
<tr><td class="c029"><span class="c007">asr</span></td><td class="c028">Bitwise arithmetic shift right on integers. </td></tr>
<tr><td class="c029"><span class="c007">+.</span></td><td class="c028">Floating-point addition. </td></tr>
<tr><td class="c029"><span class="c007">-.</span> (infix)</td><td class="c028">Floating-point subtraction. </td></tr>
<tr><td class="c029"><span class="c007">~-.   -.</span> (prefix)</td><td class="c028">Floating-point negation. </td></tr>
<tr><td class="c029"><span class="c007">*.</span></td><td class="c028">Floating-point multiplication. </td></tr>
<tr><td class="c029"><span class="c007">/.</span></td><td class="c028">Floating-point division. </td></tr>
<tr><td class="c029"><span class="c007">**</span></td><td class="c028">Floating-point exponentiation. </td></tr>
<tr><td class="c029"><span class="c007">@</span> </td><td class="c028">List concatenation. </td></tr>
<tr><td class="c029"><span class="c007">^</span> </td><td class="c028">String concatenation. </td></tr>
<tr><td class="c029"><span class="c007">!</span> </td><td class="c028">Dereferencing (return the current
contents of a reference). </td></tr>
<tr><td class="c029"><span class="c007">:=</span></td><td class="c028">Reference assignment (update the
reference given as first argument with the value of the second
argument). </td></tr>
<tr><td class="c029"><span class="c007">=</span> </td><td class="c028">Structural equality test. </td></tr>
<tr><td class="c029"><span class="c007">&lt;&gt;</span> </td><td class="c028">Structural inequality test. </td></tr>
<tr><td class="c029"><span class="c007">==</span> </td><td class="c028">Physical equality test. </td></tr>
<tr><td class="c029"><span class="c007">!=</span> </td><td class="c028">Physical inequality test. </td></tr>
<tr><td class="c029"><span class="c007">&lt;</span> </td><td class="c028">Test “less than”. </td></tr>
<tr><td class="c029"><span class="c007">&lt;=</span> </td><td class="c028">Test “less than or equal”. </td></tr>
<tr><td class="c029"><span class="c007">&gt;</span> </td><td class="c028">Test “greater than”. </td></tr>
<tr><td class="c029"><span class="c007">&gt;=</span> </td><td class="c028">Test “greater than or equal”. </td></tr>
<tr><td class="c029"><span class="c007">&amp;&amp;   &amp;</span></td><td class="c028">Boolean conjunction. </td></tr>
<tr><td class="c029"><span class="c007">||   or</span></td><td class="c028">Boolean disjunction. </td></tr>
</tbody></table></div>
<h3 class="subsection" id="sec139">7.5&nbsp;&nbsp;Objects</h3>
<p> <a id="s:objects"></a></p><h4 class="subsubsection" id="sec140">Object creation</h4>
<p><a id="hevea_manual.kwd51"></a></p><p>When <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> evaluates to a class body, <span class="c008">new</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
evaluates to a new object containing the instance variables and
methods of this class.</p><p>When <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> evaluates to a class function, <span class="c008">new</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
evaluates to a function expecting the same number of arguments and
returning a new object of this class.</p><h4 class="subsubsection" id="sec141">Immediate object creation</h4>
<p><a id="hevea_manual.kwd52"></a></p><p>Creating directly an object through the <span class="c008">object</span> <a class="syntax" href="classes.html#class-body"><span class="c014">class-body</span></a> <span class="c008">end</span>
construct is operationally equivalent to defining locally a <span class="c008">class</span>
<a class="syntax" href="names.html#class-name"><span class="c014">class-name</span></a> <span class="c005"><span class="c007">=</span> <span class="c007">object</span></span> &nbsp;<a class="syntax" href="classes.html#class-body"><span class="c014">class-body</span></a> <span class="c008">end</span> —see sections
<a href="classes.html#ss%3Aclass-body">6.9.2</a> and following for the syntax of <a class="syntax" href="classes.html#class-body"><span class="c014">class-body</span></a>—
and immediately creating a single object from it by <span class="c008">new</span> <a class="syntax" href="names.html#class-name"><span class="c014">class-name</span></a>.</p><p>The typing of immediate objects is slightly different from explicitly
defining a class in two respects. First, the inferred object type may
contain free type variables. Second, since the class body of an
immediate object will never be extended, its self type can be unified
with a closed object type.</p><h4 class="subsubsection" id="sec142">Method invocation</h4>
<p>The expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">#</span> &nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a> invokes the method
<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a> of the object denoted by <a class="syntax" href="#expr"><span class="c014">expr</span></a>.</p><p>If <a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a> is a polymorphic method, its type should be known at
the invocation site. This is true for instance if <a class="syntax" href="#expr"><span class="c014">expr</span></a> is the name
of a fresh object (<span class="c008">let</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> = <span class="c008">new</span> &nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> … ) or if
there is a type constraint. Principality of the derivation can be
checked in the <span class="c007">-principal</span> mode.</p><h4 class="subsubsection" id="sec143">Accessing and modifying instance variables</h4>
<p>The instance variables of a class are visible only in the body of the
methods defined in the same class or a class that inherits from the
class defining the instance variables. The expression <a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>
evaluates to the value of the given instance variable. The expression
<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a> <span class="c008">&lt;-</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> assigns the value of <a class="syntax" href="#expr"><span class="c014">expr</span></a> to the instance
variable <a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a>, which must be mutable. The whole expression
<a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a> <span class="c008">&lt;-</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> evaluates to <span class="c008">()</span>.</p><h4 class="subsubsection" id="sec144">Object duplication</h4>
<p>An object can be duplicated using the library function <span class="c007">Oo.copy</span>
(see
<a href="../../api/4.02/Oo.html">Module <span class="c007">Oo</span></a>). Inside a method, the expression
 <span class="c008">{&lt;</span> <a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> &nbsp;{ <span class="c008">;</span> <a class="syntax" href="names.html#inst-var-name"><span class="c014">inst-var-name</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="#expr"><span class="c014">expr</span></a> } <span class="c008">&gt;}</span>
returns a copy of self with the given instance variables replaced by
the values of the associated expressions; other instance variables
have the same value in the returned object as in self.</p>
<h3 class="subsection" id="sec145">7.6&nbsp;&nbsp;Coercions</h3>
<p> <a id="s:coercions"></a></p><p>Expressions whose type contains object or polymorphic variant types
can be explicitly coerced (weakened) to a supertype.
The expression <span class="c008">(</span><a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">:&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><span class="c008">)</span> coerces the expression <a class="syntax" href="#expr"><span class="c014">expr</span></a>
to type <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>.
The expression <span class="c008">(</span><a class="syntax" href="#expr"><span class="c014">expr</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">:&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>2</sub><span class="c008">)</span> coerces the
expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> from type <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> to type <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>2</sub>.</p><p>The former operator will sometimes fail to coerce an expression <a class="syntax" href="#expr"><span class="c014">expr</span></a>
from a type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> to a type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>
even if type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> is a subtype of type
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>: in the current implementation it only expands two levels of
type abbreviations containing objects and/or polymorphic variants,
keeping only recursion when it is explicit in the class type (for objects).
As an exception to the above algorithm, if both the inferred type of <a class="syntax" href="#expr"><span class="c014">expr</span></a>
and <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a> are ground (<em>i.e.</em> do not contain type variables), the
former operator behaves as the latter one, taking the inferred type of
<a class="syntax" href="#expr"><span class="c014">expr</span></a> as <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub>. In case of failure with the former operator,
the latter one should be used.</p><p>It is only possible to coerce an expression <a class="syntax" href="#expr"><span class="c014">expr</span></a> from type
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> to type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>, if the type of <a class="syntax" href="#expr"><span class="c014">expr</span></a> is an instance of
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> (like for a type annotation), and <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> is a subtype
of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>. The type of the coerced expression is an
instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>. If the types contain variables,
they may be instantiated by the subtyping algorithm, but this is only
done after determining whether <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> is a potential subtype of
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>. This means that typing may fail during this latter
unification step, even if some instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> is a subtype of
some instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub>.
In the following paragraphs we describe the subtyping relation used.</p><h4 class="subsubsection" id="sec146">Object types</h4>
<p>A fixed object type admits as subtype any object type that includes all
its methods. The types of the methods shall be subtypes of those in
the supertype. Namely,
</p><div class="center">
 <span class="c008">&lt;</span> <a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub>1</sub> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span> &nbsp;<a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub><span class="c013">n</span></sub> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub><span class="c013">n</span></sub> <span class="c008">&gt;</span> 
</div><p>
is a supertype of
</p><div class="center">
 <span class="c008">&lt;</span> <a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub>1</sub> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub> <span class="c008">;</span> … <span class="c008">;</span> <a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub><span class="c013">n</span></sub> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span></sub> <span class="c008">;</span>
<a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub><span class="c013">n</span>+1</sub> <span class="c008">:</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span>+1</sub> <span class="c008">;</span> … <span class="c008">;</span> <a class="syntax" href="names.html#method-name"><span class="c014">met</span></a><sub><span class="c013">n</span>+<span class="c013">m</span></sub> <span class="c008">:</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span>+<span class="c013">m</span></sub>
&nbsp;[<span class="c005"><span class="c007">;</span> <span class="c007">..</span></span>] <span class="c008">&gt;</span> 
</div><p>
which may contain an ellipsis <span class="c007">..</span> if every <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub><span class="c013">i</span></sub> is a supertype of
the corresponding <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">i</span></sub>.</p><p>A monomorphic method type can be a supertype of a polymorphic method
type. Namely, if <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a> is an instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′, then  <span class="c008">'</span><span class="c014">a</span><sub>1</sub>
… <span class="c008">'</span><span class="c014">a</span><sub><span class="c013">n</span></sub> <span class="c008">.</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′ is a subtype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>.</p><p>Inside a class definition, newly defined types are not available for
subtyping, as the type abbreviations are not yet completely
defined. There is an exception for coercing <span class="c014">self</span> to the (exact)
type of its class: this is allowed if the type of <span class="c014">self</span> does not
appear in a contravariant position in the class type, <em>i.e.</em> if
there are no binary methods.</p><h4 class="subsubsection" id="sec147">Polymorphic variant types</h4>
<p>A polymorphic variant type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a> is a subtype of another polymorphic
variant type <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′ if the upper bound of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a> (<em>i.e.</em> the
maximum set of constructors that may appear in an instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>)
is included in the lower bound of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′, and the types of arguments
for the constructors of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a> are subtypes of those in
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′. Namely,
</p><div class="center">
 <span class="c008">[</span>[<span class="c008">&lt;</span>] <span class="c008">`</span><a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub>1</sub> <span class="c008">of</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> <span class="c008">|</span> … <span class="c005"><span class="c007">|</span> <span class="c007">`</span></span>&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub><span class="c013">n</span></sub> <span class="c008">of</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub><span class="c013">n</span></sub> <span class="c008">]</span> 
</div><p>
which may be a shrinkable type, is a subtype of
</p><div class="center">
 <span class="c008">[</span>[<span class="c008">&gt;</span>] <span class="c008">`</span><a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub>1</sub> <span class="c008">of</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub> <span class="c008">|</span> … <span class="c005"><span class="c007">|</span> <span class="c007">`</span></span><a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub><span class="c013">n</span></sub> <span class="c008">of</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span></sub>
<span class="c005"><span class="c007">|</span> <span class="c007">`</span></span><a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub><span class="c013">n</span>+1</sub> <span class="c008">of</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span>+1</sub> <span class="c008">|</span> … <span class="c005"><span class="c007">|</span> <span class="c007">`</span></span><a class="syntax" href="names.html#constr-name"><span class="c014">C</span></a><sub><span class="c013">n</span>+<span class="c013">m</span></sub> <span class="c008">of</span>
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">n</span>+<span class="c013">m</span></sub> <span class="c008">]</span> 
</div><p>
which may be an extensible type, if every <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub><span class="c013">i</span></sub> is a subtype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub><span class="c013">i</span></sub>.</p><h4 class="subsubsection" id="sec148">Variance</h4>
<p>Other types do not introduce new subtyping, but they may propagate the
subtyping of their arguments. For instance, <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> <span class="c008">*</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub> is a
subtype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub> <span class="c008">*</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>2</sub> when <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> and <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub> are
respectively subtypes of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub> and <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>2</sub>.
For function types, the relation is more subtle:
<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub> is a subtype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub>&nbsp;<span class="c008">-&gt;</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>2</sub>
if <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>1</sub> is a supertype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>1</sub> and <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a><sub>2</sub> is a
subtype of <a class="syntax" href="types.html#typexpr"><span class="c014">typ</span></a>′<sub>2</sub>. For this reason, function types are covariant in
their second argument (like tuples), but contravariant in their first
argument. Mutable types, like <span class="c007">array</span> or <span class="c007">ref</span> are neither covariant
nor contravariant, they are nonvariant, that is they do not propagate
subtyping.</p><p>For user-defined types, the variance is automatically inferred: a
parameter is covariant if it has only covariant occurrences,
contravariant if it has only contravariant occurrences,
variance-free if it has no occurrences, and nonvariant otherwise.
A variance-free parameter may change freely through subtyping, it does
not have to be a subtype or a supertype.
For abstract and private types, the variance must be given explicitly
(see section&nbsp;<a href="typedecl.html#s%3Atype-defs">6.8.1</a>),
otherwise the default is nonvariant. This is also the case for
constrained arguments in type definitions.</p>






</section><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>