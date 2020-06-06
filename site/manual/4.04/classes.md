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
symbols are set in typewriter font (<span class="c004"><span class="c006">like</span> <span class="c006">this</span></span>).
Non-terminal symbols are set in italic font (<span class="c013">like</span> &nbsp;<span class="c013">that</span>).
Square brackets […] denote optional components. Curly brackets
{…} denotes zero, one or several repetitions of the enclosed
components. Curly brackets with a trailing plus sign {…}<sup>+</sup>
denote one or several repetitions of the enclosed components.
Parentheses (…) denote grouping.</p><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.04</a></div><div class="toc_title"><a href="#">The OCaml language</a></div><ul><li class="top"><a href="#">Top</a></li>
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




<h2 class="section" id="sec157">9&nbsp;&nbsp;Classes</h2>
<ul>
<li><a href="classes.html#sec158">Class types</a>
</li><li><a href="classes.html#sec167">Class expressions</a>
</li><li><a href="classes.html#sec180">Class definitions</a>
</li><li><a href="classes.html#sec183">Class specifications</a>
</li><li><a href="classes.html#sec184">Class type definitions</a>
</li></ul>
<p>
Classes are defined using a small language, similar to the module
language.</p>
<h3 class="subsection" id="sec158">9.1&nbsp;&nbsp;Class types</h3>
<p>Class types are the class-level equivalent of type expressions: they
specify the general shape and type properties of classes.</p><p><a id="hevea_manual.kwd97"></a>
<a id="hevea_manual.kwd98"></a>
<a id="hevea_manual.kwd99"></a>
<a id="hevea_manual.kwd100"></a>
<a id="hevea_manual.kwd101"></a>
<a id="hevea_manual.kwd102"></a>
<a id="hevea_manual.kwd103"></a>
<a id="hevea_manual.kwd104"></a>
<a id="hevea_manual.kwd105"></a></p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-type"><span class="c013">class-type</span></a></td><td class="c018">::=</td><td class="c020">
[[<span class="c007">?</span>]<a class="syntax" href="lex.html#label-name"><span class="c013">label-name</span></a><span class="c007">:</span>]&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;<span class="c007">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;&nbsp;<a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="class-body-type"><span class="c013">class-body-type</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">object</span>&nbsp;[<span class="c007">(</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;<span class="c007">)</span>]&nbsp;&nbsp;{<a class="syntax" href="#class-field-spec"><span class="c013">class-field-spec</span></a>}&nbsp;<span class="c007">end</span>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;[<span class="c007">[</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;&nbsp;{<span class="c007">,</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>}&nbsp;<span class="c007">]</span>]&nbsp;&nbsp;<a class="syntax" href="names.html#classtype-path"><span class="c013">classtype-path</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="class-field-spec"><span class="c013">class-field-spec</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">inherit</span>&nbsp;<a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">val</span>&nbsp;[<span class="c007">mutable</span>]&nbsp;[<span class="c007">virtual</span>]&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">val</span>&nbsp;<span class="c007">virtual</span>&nbsp;<span class="c007">mutable</span>&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;[<span class="c007">private</span>]&nbsp;[<span class="c007">virtual</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;<span class="c007">virtual</span>&nbsp;<span class="c007">private</span>&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">constraint</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><h4 class="subsubsection" id="sec159">Simple class expressions</h4>
<p>The expression <a class="syntax" href="names.html#classtype-path"><span class="c013">classtype-path</span></a> is equivalent to the class type bound to
the name <a class="syntax" href="names.html#classtype-path"><span class="c013">classtype-path</span></a>. Similarly, the expression
<span class="c007">[</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub> <span class="c007">,</span> … &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub><span class="c012">n</span></sub> <span class="c007">]</span> &nbsp;<a class="syntax" href="names.html#classtype-path"><span class="c013">classtype-path</span></a> is equivalent to
the parametric class type bound to the name <a class="syntax" href="names.html#classtype-path"><span class="c013">classtype-path</span></a>, in which
type parameters have been instantiated to respectively <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub>,
…<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub><span class="c012">n</span></sub>.</p><h4 class="subsubsection" id="sec160">Class function type</h4>
<p>The class type expression <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> <span class="c007">-&gt;</span> &nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a> is the type of
class functions (functions from values to classes) that take as
argument a value of type <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> and return as result a class of
type <a class="syntax" href="#class-type"><span class="c013">class-type</span></a>.</p><h4 class="subsubsection" id="sec161">Class body type</h4>
<p>The class type expression
<span class="c007">object</span> [<span class="c007">(</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> <span class="c007">)</span>] &nbsp;{<a class="syntax" href="#class-field-spec"><span class="c013">class-field-spec</span></a>} <span class="c007">end</span>
is the type of a class body. It specifies its instance variables and
methods. In this type, <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> is matched against the self type, therefore
providing a name for the self type.</p><p>A class body will match a class body type if it provides definitions
for all the components specified in the class body type, and these
definitions meet the type requirements given in the class body type.
Furthermore, all methods either virtual or public present in the class
body must also be present in the class body type (on the other hand, some
instance variables and concrete private methods may be omitted). A
virtual method will match a concrete method, which makes it possible
to forget its implementation. An immutable instance variable will match a
mutable instance variable.</p><h4 class="subsubsection" id="sec162">Inheritance</h4>
<p><a id="hevea_manual.kwd106"></a></p><p>The inheritance construct <span class="c007">inherit</span> <a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a> provides for inclusion of
methods and instance variables from other class types.
The instance variable and method types from <a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a> are added
into the current class type.</p><h4 class="subsubsection" id="sec163">Instance variable specification</h4>
<p><a id="hevea_manual.kwd107"></a>
<a id="hevea_manual.kwd108"></a></p><p>A specification of an instance variable is written
<span class="c007">val</span> [<span class="c007">mutable</span>] [<span class="c007">virtual</span>] <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>, where
<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>
is the name of the instance variable and <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> its expected type.
The flag <span class="c007">mutable</span> indicates whether this instance variable can be
physically modified.
The flag <span class="c007">virtual</span> indicates that this instance variable is not
initialized. It can be initialized later through inheritance.</p><p>An instance variable specification will hide any previous
specification of an instance variable of the same name.</p><h4 class="subsubsection" id="sec164">Method specification</h4>
<p>
<a id="sec-methspec"></a></p><p><a id="hevea_manual.kwd109"></a>
<a id="hevea_manual.kwd110"></a></p><p>The specification of a method is written
<span class="c007">method</span> [<span class="c007">private</span>] <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>, where
<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> is the name of the method and <a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a> its
expected type, possibly polymorphic. The flag <span class="c007">private</span> indicates
that the method cannot be accessed from outside the object.</p><p>The polymorphism may be left implicit in public method specifications:
any type variable which is not bound to a class parameter and does not
appear elsewhere inside the class specification will be assumed to be
universal, and made polymorphic in the resulting method type.
Writing an explicit polymorphic type will disable this behaviour.</p><p>If several specifications are present for the same method, they
must have compatible types.
Any non-private specification of a method forces it to be public.</p><h4 class="subsubsection" id="sec165">Virtual method specification</h4>
<p><a id="hevea_manual.kwd111"></a>
<a id="hevea_manual.kwd112"></a></p><p>A virtual method specification is written <span class="c007">method</span> [<span class="c007">private</span>]
<span class="c007">virtual</span> <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>, where <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> is the
name of the method and <a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a> its expected type.</p><h4 class="subsubsection" id="sec166">Constraints on type parameters</h4>
<p><a id="hevea_manual.kwd113"></a></p><p>The construct <span class="c007">constraint</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub> <span class="c007">=</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>2</sub> forces the two
type expressions to be equal. This is typically used to specify type
parameters: in this way, they can be bound to specific type
expressions.</p>
<h3 class="subsection" id="sec167">9.2&nbsp;&nbsp;Class expressions</h3>
<p>Class expressions are the class-level equivalent of value expressions:
they evaluate to classes, thus providing implementations for the
specifications expressed in class types.</p><p><a id="hevea_manual.kwd114"></a>
<a id="hevea_manual.kwd115"></a>
<a id="hevea_manual.kwd116"></a>
<a id="hevea_manual.kwd117"></a>
<a id="hevea_manual.kwd118"></a>
<a id="hevea_manual.kwd119"></a>
<a id="hevea_manual.kwd120"></a>
<a id="hevea_manual.kwd121"></a>
<a id="hevea_manual.kwd122"></a>
<a id="hevea_manual.kwd123"></a>
<a id="hevea_manual.kwd124"></a>
<a id="hevea_manual.kwd125"></a>
<a id="hevea_manual.kwd126"></a></p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-expr"><span class="c013">class-expr</span></a></td><td class="c018">::=</td><td class="c020">
<a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">[</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;&nbsp;{<span class="c007">,</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>}&nbsp;<span class="c007">]</span>&nbsp;&nbsp;<a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">(</span>&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>&nbsp;<span class="c007">)</span>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">(</span>&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a>&nbsp;<span class="c007">)</span>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>&nbsp;&nbsp;{<a class="syntax" href="expr.html#argument"><span class="c013">argument</span></a>}<sup>+</sup>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">fun</span>&nbsp;{<a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a>}<sup>+</sup>&nbsp;<span class="c007">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">let</span>&nbsp;[<span class="c007">rec</span>]&nbsp;<a class="syntax" href="expr.html#let-binding"><span class="c013">let-binding</span></a>&nbsp;&nbsp;{<span class="c007">and</span>&nbsp;<a class="syntax" href="expr.html#let-binding"><span class="c013">let-binding</span></a>}&nbsp;<span class="c007">in</span>&nbsp;&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">object</span>&nbsp;<a class="syntax" href="#class-body"><span class="c013">class-body</span></a>&nbsp;<span class="c007">end</span>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-field"><span class="c013">class-field</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">inherit</span>&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>&nbsp;&nbsp;[<span class="c007">as</span>&nbsp;<a class="syntax" href="lex.html#lowercase-ident"><span class="c013">lowercase-ident</span></a>]
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">val</span>&nbsp;[<span class="c007">mutable</span>]&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;&nbsp;[<span class="c007">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>]&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">val</span>&nbsp;[<span class="c007">mutable</span>]&nbsp;<span class="c007">virtual</span>&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">val</span>&nbsp;<span class="c007">virtual</span>&nbsp;<span class="c007">mutable</span>&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;[<span class="c007">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;&nbsp;{<a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a>}&nbsp;&nbsp;[<span class="c007">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>]&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;[<span class="c007">private</span>]&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;[<span class="c007">private</span>]&nbsp;<span class="c007">virtual</span>&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">method</span>&nbsp;<span class="c007">virtual</span>&nbsp;<span class="c007">private</span>&nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>&nbsp;<span class="c007">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">constraint</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;&nbsp;<span class="c007">initializer</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><h4 class="subsubsection" id="sec168">Simple class expressions</h4>
<p>The expression <a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a> evaluates to the class bound to the name
<a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a>. Similarly, the expression
<span class="c007">[</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub> <span class="c007">,</span> … &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub><span class="c012">n</span></sub> <span class="c007">]</span> &nbsp;<a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a>
evaluates to the parametric class bound to the name <a class="syntax" href="names.html#class-path"><span class="c013">class-path</span></a>,
in which type parameters have been instantiated respectively to
<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub>, …<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub><span class="c012">n</span></sub>.</p><p>The expression <span class="c007">(</span> <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> <span class="c007">)</span> evaluates to the same module as
<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>.</p><p>The expression <span class="c007">(</span> <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a> <span class="c007">)</span> checks that
<a class="syntax" href="#class-type"><span class="c013">class-type</span></a> matches the type of <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> (that is, that the
implementation <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> meets the type specification
<a class="syntax" href="#class-type"><span class="c013">class-type</span></a>). The whole expression evaluates to the same class as
<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>, except that all components not specified in
<a class="syntax" href="#class-type"><span class="c013">class-type</span></a> are hidden and can no longer be accessed.</p><h4 class="subsubsection" id="sec169">Class application</h4>
<p>Class application is denoted by juxtaposition of (possibly labeled)
expressions. It denotes the class whose constructor is the first
expression applied to the given arguments. The arguments are
evaluated as for expression application, but the constructor itself will
only be evaluated when objects are created. In particular, side-effects
caused by the application of the constructor will only occur at object
creation time.</p><h4 class="subsubsection" id="sec170">Class function</h4>
<p>The expression <span class="c007">fun</span> [[<span class="c007">?</span>]<a class="syntax" href="lex.html#label-name"><span class="c013">label-name</span></a><span class="c007">:</span>]&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c013">pattern</span></a> <span class="c007">-&gt;</span> &nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> evaluates
to a function from values to classes.
When this function is applied to a value <span class="c012">v</span>, this value is
matched against the pattern <a class="syntax" href="patterns.html#pattern"><span class="c013">pattern</span></a> and the result is the result of
the evaluation of <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> in the extended environment.</p><p>Conversion from functions with default values to functions with
patterns only works identically for class functions as for normal
functions.</p><p>The expression
</p><div class="center">
<span class="c007">fun</span> <a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a><sub>1</sub> … &nbsp;<a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a><sub><span class="c012">n</span></sub> <span class="c007">-&gt;</span> &nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>
</div><p>
is a short form for
</p><div class="center">
<span class="c007">fun</span> <a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a><sub>1</sub> <span class="c007">-&gt;</span> … <span class="c007">fun</span> &nbsp;<a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a><sub><span class="c012">n</span></sub> <span class="c007">-&gt;</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
</div><h4 class="subsubsection" id="sec171">Local definitions</h4>
<p>The <span class="c006">let</span> and <span class="c006">let rec</span> constructs bind value names locally,
as for the core language expressions.</p><p>If a local definition occurs at the very beginning of a class
definition, it will be evaluated when the class is created (just as if
the definition was outside of the class).
Otherwise, it will be evaluated when the object constructor is called.</p><h4 class="subsubsection" id="ss:class-body">Class body</h4>
<table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-body"><span class="c013">class-body</span></a></td><td class="c018">::=</td><td class="c020">&nbsp;&nbsp;[<span class="c007">(</span>&nbsp;<a class="syntax" href="patterns.html#pattern"><span class="c013">pattern</span></a>&nbsp;&nbsp;[<span class="c007">:</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>]&nbsp;<span class="c007">)</span>]&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#class-field"><span class="c013">class-field</span></a>&nbsp;}
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>
The expression
<span class="c007">object</span> <a class="syntax" href="#class-body"><span class="c013">class-body</span></a> <span class="c007">end</span> denotes
a class body. This is the prototype for an object : it lists the
instance variables and methods of an objet of this class.</p><p>A class body is a class value: it is not evaluated at once. Rather,
its components are evaluated each time an object is created.</p><p>In a class body, the pattern <span class="c007">(</span> <a class="syntax" href="patterns.html#pattern"><span class="c013">pattern</span></a> &nbsp;[<span class="c007">:</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>] <span class="c007">)</span> is
matched against self, therefore providing a binding for self and self
type. Self can only be used in method and initializers.</p><p>Self type cannot be a closed object type, so that the class remains
extensible.</p><p>Since OCaml 4.01, it is an error if the same method or instance
variable name is defined several times in the same class body.</p><h4 class="subsubsection" id="sec173">Inheritance</h4>
<p><a id="hevea_manual.kwd127"></a></p><p>The inheritance construct <span class="c007">inherit</span> <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> allows reusing
methods and instance variables from other classes. The class
expression <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a> must evaluate to a class body. The instance
variables, methods and initializers from this class body are added
into the current class. The addition of a method will override any
previously defined method of the same name.</p><p><a id="hevea_manual.kwd128"></a>
An ancestor can be bound by appending <span class="c007">as</span> <a class="syntax" href="lex.html#lowercase-ident"><span class="c013">lowercase-ident</span></a>
to the inheritance construct. <a class="syntax" href="lex.html#lowercase-ident"><span class="c013">lowercase-ident</span></a> is not a true
variable and can only be used to select a method, i.e. in an expression
<a class="syntax" href="lex.html#lowercase-ident"><span class="c013">lowercase-ident</span></a> <span class="c007">#</span> &nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>. This gives access to the
method <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> as it was defined in the parent class even if it is
redefined in the current class.
The scope of this ancestor binding is limited to the current class.
The ancestor method may be called from a subclass but only indirectly.</p><h4 class="subsubsection" id="sec174">Instance variable definition</h4>
<p><a id="hevea_manual.kwd129"></a>
<a id="hevea_manual.kwd130"></a></p><p>The definition <span class="c007">val</span> [<span class="c007">mutable</span>] <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> <span class="c007">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a> adds an
instance variable <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> whose initial value is the value of
expression <a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>.
The flag <span class="c007">mutable</span> allows physical modification of this variable by
methods.</p><p>An instance variable can only be used in the methods and
initializers that follow its definition.</p><p>Since version 3.10, redefinitions of a visible instance variable with
the same name do not create a new variable, but are merged, using the
last value for initialization. They must have identical types and
mutability.
However, if an instance variable is hidden by
omitting it from an interface, it will be kept distinct from
other instance variables with the same name.</p><h4 class="subsubsection" id="sec175">Virtual instance variable definition</h4>
<p><a id="hevea_manual.kwd131"></a>
<a id="hevea_manual.kwd132"></a></p><p>A variable specification is written <span class="c007">val</span> [<span class="c007">mutable</span>] <span class="c007">virtual</span>
<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a>. It specifies whether the variable is
modifiable, and gives its type.</p><p>Virtual instance variables were added in version 3.10.</p><h4 class="subsubsection" id="sec176">Method definition</h4>
<p><a id="hevea_manual.kwd133"></a>
<a id="hevea_manual.kwd134"></a></p><p>A method definition is written <span class="c007">method</span> <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>. The
definition of a method overrides any previous definition of this
method. The method will be public (that is, not private) if any of
the definition states so.</p><p>A private method, <span class="c004"><span class="c006">method</span> <span class="c006">private</span></span> <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>, is a
method that can only be invoked on self (from other methods of the
same object, defined in this class or one of its subclasses). This
invocation is performed using the expression
<a class="syntax" href="names.html#value-name"><span class="c013">value-name</span></a> <span class="c007">#</span> &nbsp;<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a>, where <a class="syntax" href="names.html#value-name"><span class="c013">value-name</span></a> is directly bound to
self at the beginning of the class definition. Private methods do
not appear in object types. A method may have both public and private
definitions, but as soon as there is a public one, all subsequent
definitions will be made public.</p><p>Methods may have an explicitly polymorphic type, allowing them to be
used polymorphically in programs (even for the same object). The
explicit declaration may be done in one of three ways: (1) by giving an
explicit polymorphic type in the method definition, immediately after
the method name, <em>i.e.</em>
<span class="c007">method</span> [<span class="c007">private</span>] <a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">:</span> &nbsp;{<span class="c007">'</span> <a class="syntax" href="lex.html#ident"><span class="c013">ident</span></a>}<sup>+</sup> <span class="c007">.</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a> <span class="c007">=</span>
&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>; (2) by a forward declaration of the explicit polymorphic type
through a virtual method definition; (3) by importing such a
declaration through inheritance and/or constraining the type of <em>self</em>.</p><p>Some special expressions are available in method bodies for
manipulating instance variables and duplicating self:
</p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a></td><td class="c018">::=</td><td class="c020">
…
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">&lt;-</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td><td class="c018">∣</td><td class="c020">&nbsp;<span class="c007">{&lt;</span>&nbsp;[&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c007">;</span>&nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c007">;</span>]&nbsp;]&nbsp;<span class="c007">&gt;}</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The expression <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> <span class="c007">&lt;-</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a> modifies in-place the current
object by replacing the value associated to <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a> by the
value of <a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a>. Of course, this instance variable must have been
declared mutable.</p><p>The expression
<span class="c007">{&lt;</span> <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a><sub>1</sub> <span class="c007">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a><sub>1</sub> <span class="c007">;</span> … <span class="c007">;</span> &nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a><sub><span class="c012">n</span></sub> <span class="c007">=</span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a><sub><span class="c012">n</span></sub> <span class="c007">&gt;}</span>
evaluates to a copy of the current object in which the values of
instance variables <a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="names.html#inst-var-name"><span class="c013">inst-var-name</span></a><sub><span class="c012">n</span></sub> have
been replaced by the values of the corresponding expressions <a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a><sub>1</sub>,
…, &nbsp;<a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a><sub><span class="c012">n</span></sub>.</p><h4 class="subsubsection" id="sec177">Virtual method definition</h4>
<p><a id="hevea_manual.kwd135"></a>
<a id="hevea_manual.kwd136"></a></p><p>A method specification is written <span class="c007">method</span> [<span class="c007">private</span>] <span class="c007">virtual</span>
<a class="syntax" href="names.html#method-name"><span class="c013">method-name</span></a> <span class="c007">:</span> &nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c013">poly-typexpr</span></a>. It specifies whether the method is
public or private, and gives its type. If the method is intended to be
polymorphic, the type must be explicitly polymorphic.</p><h4 class="subsubsection" id="sec178">Constraints on type parameters</h4>
<p><a id="hevea_manual.kwd137"></a></p><p>The construct <span class="c007">constraint</span> <a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>1</sub> <span class="c007">=</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c013">typexpr</span></a><sub>2</sub> forces the two
type expressions to be equals. This is typically used to specify type
parameters: in that way they can be bound to specific type
expressions.</p><h4 class="subsubsection" id="sec179">Initializers</h4>
<p><a id="hevea_manual.kwd138"></a></p><p>A class initializer <span class="c007">initializer</span> <a class="syntax" href="expr.html#expr"><span class="c013">expr</span></a> specifies an expression that
will be evaluated whenever an object is created from the class, once
all its instance variables have been initialized.</p>
<h3 class="subsection" id="sec180">9.3&nbsp;&nbsp;Class definitions</h3>
<p>
<a id="s:classdef"></a></p><p><a id="hevea_manual.kwd139"></a>
<a id="hevea_manual.kwd140"></a></p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-definition"><span class="c013">class-definition</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">class</span>&nbsp;<a class="syntax" href="#class-binding"><span class="c013">class-binding</span></a>&nbsp;&nbsp;{&nbsp;<span class="c007">and</span>&nbsp;<a class="syntax" href="#class-binding"><span class="c013">class-binding</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="class-binding"><span class="c013">class-binding</span></a></td><td class="c018">::=</td><td class="c020">
[<span class="c007">virtual</span>]&nbsp;[<span class="c007">[</span>&nbsp;<a class="syntax" href="#type-parameters"><span class="c013">type-parameters</span></a>&nbsp;<span class="c007">]</span>]&nbsp;&nbsp;<a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a>
&nbsp;{<a class="syntax" href="expr.html#parameter"><span class="c013">parameter</span></a>}&nbsp;&nbsp;[<span class="c007">:</span>&nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a>]&nbsp;&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="type-parameters"><span class="c013">type-parameters</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c013">ident</span></a>&nbsp;&nbsp;{&nbsp;<span class="c007">,</span>&nbsp;<span class="c007">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c013">ident</span></a>&nbsp;}
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A class definition <span class="c007">class</span> <a class="syntax" href="#class-binding"><span class="c013">class-binding</span></a> &nbsp;{ <span class="c007">and</span> <a class="syntax" href="#class-binding"><span class="c013">class-binding</span></a> } is
recursive. Each <a class="syntax" href="#class-binding"><span class="c013">class-binding</span></a> defines a <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> that can be
used in the whole expression except for inheritance. It can also be
used for inheritance, but only in the definitions that follow its own.</p><p>A class binding binds the class name <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> to the value of
expression <a class="syntax" href="#class-expr"><span class="c013">class-expr</span></a>. It also binds the class type <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> to
the type of the class, and defines two type abbreviations :
<a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> and <span class="c007">#</span> <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a>. The first one is the type of
objects of this class, while the second is more general as it unifies
with the type of any object belonging to a subclass (see
section&nbsp;<a href="types.html#s%3Asharp-types">6.4</a>).</p><h4 class="subsubsection" id="sec181">Virtual class</h4>
<p>A class must be flagged virtual if one of its methods is virtual (that
is, appears in the class type, but is not actually defined).
Objects cannot be created from a virtual class.</p><h4 class="subsubsection" id="sec182">Type parameters</h4>
<p>The class type parameters correspond to the ones of the class type and
of the two type abbreviations defined by the class binding. They must
be bound to actual types in the class definition using type
constraints. So that the abbreviations are well-formed, type
variables of the inferred type of the class must either be type
parameters or be bound in the constraint clause.</p>
<h3 class="subsection" id="sec183">9.4&nbsp;&nbsp;Class specifications</h3>
<p>
<a id="s:class-spec"></a></p><p><a id="hevea_manual.kwd141"></a>
<a id="hevea_manual.kwd142"></a></p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="class-specification"><span class="c013">class-specification</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">class</span>&nbsp;<a class="syntax" href="#class-spec"><span class="c013">class-spec</span></a>&nbsp;&nbsp;{&nbsp;<span class="c007">and</span>&nbsp;<a class="syntax" href="#class-spec"><span class="c013">class-spec</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="class-spec"><span class="c013">class-spec</span></a></td><td class="c018">::=</td><td class="c020">
[<span class="c007">virtual</span>]&nbsp;[<span class="c007">[</span>&nbsp;<a class="syntax" href="#type-parameters"><span class="c013">type-parameters</span></a>&nbsp;<span class="c007">]</span>]&nbsp;&nbsp;<a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a>&nbsp;<span class="c007">:</span>
&nbsp;<a class="syntax" href="#class-type"><span class="c013">class-type</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>This is the counterpart in signatures of class definitions.
A class specification matches a class definition if they have the same
type parameters and their types match.</p>
<h3 class="subsection" id="sec184">9.5&nbsp;&nbsp;Class type definitions</h3>
<p>
<a id="s:classtype"></a></p><p><a id="hevea_manual.kwd143"></a>
<a id="hevea_manual.kwd144"></a>
<a id="hevea_manual.kwd145"></a></p><table class="display dcenter"><tbody><tr class="c022"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c021">
<a class="syntax" id="classtype-definition"><span class="c013">classtype-definition</span></a></td><td class="c018">::=</td><td class="c020">
<span class="c007">class</span>&nbsp;<span class="c007">type</span>&nbsp;<a class="syntax" href="#classtype-def"><span class="c013">classtype-def</span></a>
&nbsp;{&nbsp;<span class="c007">and</span>&nbsp;<a class="syntax" href="#classtype-def"><span class="c013">classtype-def</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c021">&nbsp;</td></tr>
<tr><td class="c021">
<a class="syntax" id="classtype-def"><span class="c013">classtype-def</span></a></td><td class="c018">::=</td><td class="c020">
[<span class="c007">virtual</span>]&nbsp;[<span class="c007">[</span>&nbsp;<a class="syntax" href="#type-parameters"><span class="c013">type-parameters</span></a>&nbsp;<span class="c007">]</span>]&nbsp;&nbsp;<a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a>&nbsp;<span class="c007">=</span>&nbsp;&nbsp;<a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A class type definition <span class="c007">class</span> <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> <span class="c007">=</span> &nbsp;<a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a>
defines an abbreviation <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> for the class body type
<a class="syntax" href="#class-body-type"><span class="c013">class-body-type</span></a>. As for class definitions, two type abbreviations
<a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> and <span class="c007">#</span> <a class="syntax" href="names.html#class-name"><span class="c013">class-name</span></a> are also defined. The definition can
be parameterized by some type parameters. If any method in the class
type body is virtual, the definition must be flagged <span class="c007">virtual</span>.</p><p>Two class type definitions match if they have the same type parameters
and they expand to matching types.

</p>






</section><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>