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




<h2 class="section" id="sec149">8&nbsp;&nbsp;Type and exception definitions</h2>
<ul>
<li><a href="typedecl.html#sec150">Type definitions</a>
</li><li><a href="typedecl.html#sec151">Exception definitions</a>
</li></ul>

<h3 class="subsection" id="sec150">8.1&nbsp;&nbsp;Type definitions</h3>
<p>
<a id="s:type-defs"></a></p><p>Type definitions bind type constructors to data types: either
variant types, record types, type abbreviations, or abstract data
types. They also bind the value constructors and record fields
associated with the definition.</p><p><a id="hevea_manual.kwd53"></a></p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="type-definition"><span class="c014">type-definition</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">type</span>&nbsp;<a class="syntax" href="#typedef"><span class="c014">typedef</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">and</span>&nbsp;<a class="syntax" href="#typedef"><span class="c014">typedef</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="typedef"><span class="c014">typedef</span></a></td><td class="c022">::=</td><td class="c024">
[<a class="syntax" href="#type-params"><span class="c014">type-params</span></a>]&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr-name"><span class="c014">typeconstr-name</span></a>&nbsp;&nbsp;<a class="syntax" href="#type-information"><span class="c014">type-information</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-information"><span class="c014">type-information</span></a></td><td class="c022">::=</td><td class="c024">
[<a class="syntax" href="#type-equation"><span class="c014">type-equation</span></a>]&nbsp;&nbsp;[<a class="syntax" href="#type-representation"><span class="c014">type-representation</span></a>]&nbsp;&nbsp;{&nbsp;<a class="syntax" href="#type-constraint"><span class="c014">type-constraint</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-equation"><span class="c014">type-equation</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">=</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-representation"><span class="c014">type-representation</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">=</span>&nbsp;[<span class="c008">|</span>]&nbsp;<a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">=</span>&nbsp;<span class="c008">{</span>&nbsp;<a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>]&nbsp;<span class="c008">}</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-params"><span class="c014">type-params</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="#type-param"><span class="c014">type-param</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#type-param"><span class="c014">type-param</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">,</span>&nbsp;<a class="syntax" href="#type-param"><span class="c014">type-param</span></a>&nbsp;}&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-param"><span class="c014">type-param</span></a></td><td class="c022">::=</td><td class="c024">
[<a class="syntax" href="#variance"><span class="c014">variance</span></a>]&nbsp;<span class="c008">'</span>&nbsp;&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="variance"><span class="c014">variance</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">+</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">-</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="constr-decl"><span class="c014">constr-decl</span></a></td><td class="c022">::=</td><td class="c024">
(<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;∣&nbsp;&nbsp;<span class="c008">()</span>)&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="field-decl"><span class="c014">field-decl</span></a></td><td class="c022">::=</td><td class="c024">
[<span class="c008">mutable</span>]&nbsp;<a class="syntax" href="names.html#field-name"><span class="c014">field-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="type-constraint"><span class="c014">type-constraint</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">constraint</span>&nbsp;<span class="c008">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>
<a id="hevea_manual.kwd54"></a>
<a id="hevea_manual.kwd55"></a></p><p>Type definitions are introduced by the <span class="c007">type</span> keyword, and
consist in one or several simple definitions, possibly mutually
recursive, separated by the <span class="c007">and</span> keyword. Each simple definition
defines one type constructor.</p><p>A simple definition consists in a lowercase identifier, possibly
preceded by one or several type parameters, and followed by an
optional type equation, then an optional type representation, and then
a constraint clause. The identifier is the name of the type
constructor being defined.</p><p>The optional type parameters are either one type variable <span class="c008">'</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>,
for type constructors with one parameter, or a list of type variables
<span class="c008">('</span><a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a><sub>1</sub>,…,<span class="c008">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a><sub><span class="c013">n</span></sub><span class="c008">)</span>, for type constructors with several
parameters. Each type parameter may be prefixed by a variance
constraint <span class="c008">+</span> (resp. <span class="c008">-</span>) indicating that the parameter is
covariant (resp. contravariant). These type parameters can appear in
the type expressions of the right-hand side of the definition,
optionally restricted by a variance constraint ; <em>i.e.</em> a
covariant parameter may only appear on the right side of a functional
arrow (more precisely, follow the left branch of an even number of
arrows), and a contravariant parameter only the left side (left branch of
an odd number of arrows). If the type has a representation or
an equation, and the parameter is free (<em>i.e.</em> not bound via a
type constraint to a constructed type), its variance constraint is
checked but subtyping <em>etc.</em> will use the inferred variance of the
parameter, which may be less restrictive; otherwise (<em>i.e.</em> for abstract
types or non-free parameters), the variance must be given explicitly,
and the parameter is invariant if no variance is given.</p><p>The optional type equation <span class="c008">=</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> makes the defined type
equivalent to the type expression <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>:
one can be substituted for the other during typing.
If no type equation is given, a new type is generated: the defined type
is incompatible with any other type.</p><p>The optional type representation describes the data structure
representing the defined type, by giving the list of associated
constructors (if it is a variant type) or associated fields (if it is
a record type). If no type representation is given, nothing is
assumed on the structure of the type besides what is stated in the
optional type equation.</p><p>The type representation <span class="c008">=</span> [<span class="c008">|</span>] <a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a> &nbsp;{ <span class="c008">|</span> <a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a> }
describes a variant type. The constructor declarations
<a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="#constr-decl"><span class="c014">constr-decl</span></a><sub><span class="c013">n</span></sub> describe the constructors
associated to this variant type. The constructor
declaration <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a> <span class="c008">of</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">*</span> … <span class="c008">*</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub>
declares the name <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a> as a non-constant constructor, whose
arguments have types <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> …<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub>.
The constructor declaration <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>
declares the name <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a> as a constant
constructor. Constructor names must be capitalized.</p><p>The type representation <span class="c005"><span class="c007">=</span> <span class="c007">{</span></span> <a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a> &nbsp;{ <span class="c008">;</span> <a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a> } &nbsp;[<span class="c008">;</span>] <span class="c008">}</span>
describes a record type. The field declarations <a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a><sub>1</sub>, …,
&nbsp;<a class="syntax" href="#field-decl"><span class="c014">field-decl</span></a><sub><span class="c013">n</span></sub> describe the fields associated to this record type.
The field declaration <a class="syntax" href="names.html#field-name"><span class="c014">field-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a> declares
<a class="syntax" href="names.html#field-name"><span class="c014">field-name</span></a> as a field whose argument has type <a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>.
The field declaration <span class="c008">mutable</span> <a class="syntax" href="names.html#field-name"><span class="c014">field-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="types.html#poly-typexpr"><span class="c014">poly-typexpr</span></a>
<a id="hevea_manual.kwd56"></a>
behaves similarly; in addition, it allows physical modification of
this field.
Immutable fields are covariant, mutable fields are non-variant.
Both mutable and immutable fields may have a explicitly polymorphic
types. The polymorphism of the contents is statically checked whenever
a record value is created or modified. Extracted values may have their
types instantiated.</p><p>The two components of a type definition, the optional equation and the
optional representation, can be combined independently, giving
rise to four typical situations:</p><dl class="description"><dt class="dt-description">
<span class="c019">Abstract type: no equation, no representation.</span></dt><dd class="dd-description"> &nbsp;<br>
When appearing in a module signature, this definition specifies
nothing on the type constructor, besides its number of parameters:
its representation is hidden and it is assumed incompatible with any
other type.</dd><dt class="dt-description"><span class="c019">Type abbreviation: an equation, no representation.</span></dt><dd class="dd-description"> &nbsp;<br>
This defines the type constructor as an abbreviation for the type
expression on the right of the <span class="c008">=</span> sign.</dd><dt class="dt-description"><span class="c019">New variant type or record type: no equation, a representation.</span></dt><dd class="dd-description"> &nbsp;<br>
This generates a new type constructor and defines associated
constructors or fields, through which values of that type can be
directly built or inspected.</dd><dt class="dt-description"><span class="c019">Re-exported variant type or record type: an equation,
a representation.</span></dt><dd class="dd-description"> &nbsp;<br>
In this case, the type constructor is defined as an abbreviation for
the type expression given in the equation, but in addition the
constructors or fields given in the representation remain attached to
the defined type constructor. The type expression in the equation part
must agree with the representation: it must be of the same kind
(record or variant) and have exactly the same constructors or fields,
in the same order, with the same arguments.
</dd></dl><p>The type variables appearing as type parameters can optionally be
prefixed by <span class="c007">+</span> or <span class="c007">-</span> to indicate that the type constructor is
covariant or contravariant with respect to this parameter. This
variance information is used to decide subtyping relations when
checking the validity of <span class="c008">:&gt;</span> coercions (see section <a href="expr.html#s%3Acoercions">6.7.6</a>).</p><p>For instance, <span class="c007">type +'a t</span> declares <span class="c007">t</span> as an abstract type that is
covariant in its parameter; this means that if the type τ is a
subtype of the type σ, then τ <span class="c009"> t</span> is a subtype of σ
<span class="c009"> t</span>. Similarly, <span class="c007">type -'a t</span> declares that the abstract type <span class="c007">t</span> is
contravariant in its parameter: if τ is a subtype of σ, then
σ <span class="c009"> t</span> is a subtype of τ <span class="c009"> t</span>. If no <span class="c007">+</span> or <span class="c007">-</span> variance
annotation is given, the type constructor is assumed non-variant in the
corresponding parameter. For instance, the abstract type declaration
<span class="c007">type 'a t</span> means that τ <span class="c009"> t</span> is neither a subtype nor a
supertype of σ <span class="c009"> t</span> if τ is subtype of σ.</p><p>The variance indicated by the <span class="c007">+</span> and <span class="c007">-</span> annotations on parameters
are required only for abstract types. For abbreviations, variant
types or record types, the variance properties of the type constructor
are inferred from its definition, and the variance annotations are
only checked for conformance with the definition.</p><p><a id="hevea_manual.kwd57"></a>
The construct  <span class="c005"><span class="c007">constraint</span> <span class="c007">'</span></span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>  allows the
specification of
type parameters. Any actual type argument corresponding to the type
parameter <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> has to be an instance of <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> (more precisely,
<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> and <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> are unified). Type variables of <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> can
appear in the type equation and the type declaration.</p>
<h3 class="subsection" id="sec151">8.2&nbsp;&nbsp;Exception definitions</h3>
<p> <a id="s:excdef"></a>
<a id="hevea_manual.kwd58"></a></p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="exception-definition"><span class="c014">exception-definition</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">exception</span>&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">exception</span>&nbsp;<a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a>&nbsp;<span class="c008">=</span>&nbsp;&nbsp;<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Exception definitions add new constructors to the built-in variant
type <code>exn</code> of exception values. The constructors are declared as
for a definition of a variant type.</p><p>The form <span class="c008">exception</span> <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a> &nbsp;[<span class="c008">of</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a> &nbsp;{<span class="c008">*</span> <a class="syntax" href="types.html#typexpr"><span class="c014">typexpr</span></a>}]
generates a new exception, distinct from all other exceptions in the system.
The form <span class="c008">exception</span> <a class="syntax" href="names.html#constr-name"><span class="c014">constr-name</span></a> <span class="c008">=</span> &nbsp;<a class="syntax" href="names.html#constr"><span class="c014">constr</span></a>
gives an alternate name to an existing exception.

</p>






</section><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>