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




<h2 class="section" id="sec91">4&nbsp;&nbsp;Type expressions</h2>
<p>
<a id="hevea_manual.kwd2"></a></p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="typexpr"><span class="c014">typexpr</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">_</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">)</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;[[<span class="c008">?</span>]<a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a><span class="c008">:</span>]&nbsp;&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">-&gt;</span>&nbsp;&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">*</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;}<sup>+</sup>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">,</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;<span class="c008">)</span>&nbsp;&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">as</span>&nbsp;<span class="c008">'</span>&nbsp;&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#polymorphic-variant-type"><span class="c014">polymorphic-variant-type</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">&lt;</span>&nbsp;[<span class="c008">..</span>]&nbsp;<span class="c008">&gt;</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">&lt;</span>&nbsp;<a class="syntax" href="#method-type"><span class="c014">method-type</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">;</span>&nbsp;<a class="syntax" href="#method-type"><span class="c014">method-type</span></a>&nbsp;}&nbsp;&nbsp;[<span class="c008">;</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">;</span>&nbsp;<span class="c008">..</span>]&nbsp;<span class="c008">&gt;</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">#</span>&nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;<span class="c008">#</span>&nbsp;&nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">(</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">,</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;<span class="c008">)</span>&nbsp;<span class="c008">#</span>&nbsp;&nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="poly-typexpr"><span class="c014">poly-typexpr</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;{&nbsp;<span class="c008">'</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>&nbsp;}<sup>+</sup>&nbsp;<span class="c008">.</span>&nbsp;&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="method-type"><span class="c014">method-type</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="names.html#method-name"><span class="c014">method-name</span></a>&nbsp;<span class="c008">:</span>&nbsp;&nbsp;<a class="syntax" href="#poly-typexpr"><span class="c014">poly-typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>The table below shows the relative precedences and associativity of
operators and non-closed type constructions. The constructions with
higher precedences come first.
<a id="hevea_manual.kwd3"></a>
</p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">Operator</span></td><td class="c021"><span class="c019">Associativity</span> </td></tr>
<tr><td class="c023">
Type constructor application</td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">#</span></td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">*</span></td><td class="c023">– </td></tr>
<tr><td class="c023"><span class="c007">-&gt;</span></td><td class="c023">right </td></tr>
<tr><td class="c023"><span class="c007">as</span></td><td class="c023">– </td></tr>
</tbody></table></div><p>Type expressions denote types in definitions of data types as well as
in type constraints over patterns and expressions.</p><h4 class="subsubsection" id="sec92">Type variables</h4>
<p>The type expression <span class="c008">'</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> stands for the type variable named
<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>. The type expression <span class="c008">_</span> stands for an anonymous type variable.
In data type definitions, type variables are names for the
data type parameters. In type constraints, they represent unspecified
types that can be instantiated by any type to satisfy the type
constraint. In general the scope of a named type variable is the
whole top-level phrase where it appears, and it can only be
generalized when leaving
this scope. Anonymous variables have no such restriction.
In the following cases, the scope of named type variables is
restricted to the type expression where they appear: 1) for universal
(explicitly polymorphic) type variables; 2) for type variables that
only appear in public method specifications (as those variables will
be made universal, as described in section&nbsp;<a href="classes.html#sec-methspec">6.9.1</a>);
3) for variables used as aliases, when the type they are aliased to
would be invalid in the scope of the enclosing definition (<span class="c013">i.e.</span>
when it contains free universal type variables, or locally
defined types.)</p><h4 class="subsubsection" id="sec93">Parenthesized types</h4>
<p>The type expression <span class="c008">(</span> <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> <span class="c008">)</span> denotes the same type as
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>.</p><h4 class="subsubsection" id="sec94">Function types</h4>
<p>The type expression <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub> denotes the type of
functions mapping arguments of type <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> to results of type
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub>.</p><p><a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub> denotes the same function type, but
the argument is labeled <a class="syntax" href="lex.html#label"><span class="c014">label</span></a>.</p><p><span class="c008">?</span> <a class="syntax" href="lex.html#label-name"><span class="c014">label-name</span></a> <span class="c008">:</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">-&gt;</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub> denotes the type of functions
mapping an optional labeled argument of type <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> to results of
type <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub>. That is, the physical type of the function will be
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c005"><span class="c007">option</span> <span class="c007">-&gt;</span></span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>2</sub>.</p><h4 class="subsubsection" id="sec95">Tuple types</h4>
<p>The type expression <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> <span class="c008">*</span> … <span class="c008">*</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub>
denotes the type of tuples whose elements belong to types <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub>,
… &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub> respectively.</p><h4 class="subsubsection" id="sec96">Constructed types</h4>
<p>Type constructors with no parameter, as in <a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>, are type
expressions.</p><p>The type expression <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> &nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>, where <a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a> is a type
constructor with one parameter, denotes the application of the unary type
constructor <a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a> to the type <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>.</p><p>The type expression (<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub>,…,&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub>) &nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a>, where
<a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a> is a type constructor with <span class="c013">n</span> parameters, denotes the
application of the <span class="c013">n</span>-ary type constructor <a class="syntax" href="names.html#typeconstr"><span class="c014">typeconstr</span></a> to the types
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub>1</sub> through <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a><sub><span class="c013">n</span></sub>.</p><h4 class="subsubsection" id="sec97">Aliased and recursive types</h4>
<p><a id="hevea_manual.kwd4"></a></p><p>The type expression <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> <span class="c005"><span class="c007">as</span> <span class="c007">'</span></span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> denotes the same type as
<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>, and also binds the type variable <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> to type <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> both
in <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> and in other types. In general the scope of an alias is
the same as for a named type variable, and covers the whole enclosing
definition. If the type variable
<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> actually occurs in <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>, a recursive type is created. Recursive
types for which there exists a recursive path that does not contain
an object or polymorphic variant type constructor are rejected, except
when the <span class="c007">-rectypes</span> mode is selected.</p><p>If <span class="c008">'</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> denotes an explicit polymorphic variable, and <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
denotes either an object or polymorphic variant type, the row variable
of <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a> is captured by <span class="c008">'</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>, and quantified upon.</p><h4 class="subsubsection" id="sec98">Polymorphic variant types</h4>
<table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="polymorphic-variant-type"><span class="c014">polymorphic-variant-type</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">[</span>&nbsp;<a class="syntax" href="#tag-spec-first"><span class="c014">tag-spec-first</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="#tag-spec"><span class="c014">tag-spec</span></a>&nbsp;}&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">[&gt;</span>&nbsp;[&nbsp;<a class="syntax" href="#tag-spec"><span class="c014">tag-spec</span></a>&nbsp;]&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="#tag-spec"><span class="c014">tag-spec</span></a>&nbsp;}&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">[&lt;</span>&nbsp;[<span class="c008">|</span>]&nbsp;<a class="syntax" href="#tag-spec-full"><span class="c014">tag-spec-full</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">|</span>&nbsp;<a class="syntax" href="#tag-spec-full"><span class="c014">tag-spec-full</span></a>&nbsp;}
&nbsp;[&nbsp;<span class="c008">&gt;</span>&nbsp;{&nbsp;<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>&nbsp;}<sup>+</sup>&nbsp;]&nbsp;<span class="c008">]</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="tag-spec-first"><span class="c014">tag-spec-first</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;[&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;]&nbsp;<span class="c008">|</span>&nbsp;&nbsp;<a class="syntax" href="#tag-spec"><span class="c014">tag-spec</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="tag-spec"><span class="c014">tag-spec</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="tag-spec-full"><span class="c014">tag-spec-full</span></a></td><td class="c022">::=</td><td class="c024">
<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a>&nbsp;&nbsp;[&nbsp;<span class="c008">of</span>&nbsp;[<span class="c008">&amp;</span>]&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;&nbsp;{&nbsp;<span class="c008">&amp;</span>&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>&nbsp;}&nbsp;]
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>Polymorphic variant types describe the values a polymorphic variant
may take.</p><p>The first case is an exact variant type: all possible tags are
known, with their associated types, and they can all be present.
Its structure is fully known.</p><p>The second case is an open variant type, describing a polymorphic
variant value: it gives the list of all tags the value could take,
with their associated types. This type is still compatible with a
variant type containing more tags. A special case is the unknown
type, which does not define any tag, and is compatible with any
variant type.</p><p>The third case is a closed variant type. It gives information about
all the possible tags and their associated types, and which tags are
known to potentially appear in values. The exact variant type (first
case) is
just an abbreviation for a closed variant type where all possible tags
are also potentially present.</p><p>In all three cases, tags may be either specified directly in the
<span class="c008">`</span><a class="syntax" href="names.html#tag-name"><span class="c014">tag-name</span></a> &nbsp;[<span class="c008">of</span> <a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>] form, or indirectly through a type
expression, which must expand to an
exact variant type, whose tag specifications are inserted in its
place.</p><p>Full specifications of variant tags are only used for non-exact closed
types. They can be understood as a conjunctive type for the argument:
it is intended to have all the types enumerated in the
specification.</p><p>Such conjunctive constraints may be unsatisfiable. In such a case the
corresponding tag may not be used in a value of this type. This
does not mean that the whole type is not valid: one can still use
other available tags.
Conjunctive constraints are mainly intended as output from the type
checker. When they are used in source programs, unsolvable constraints
may cause early failures.</p><h4 class="subsubsection" id="sec99">Object types</h4>
<p>An object type
<span class="c008">&lt;</span> [<a class="syntax" href="#method-type"><span class="c014">method-type</span></a> &nbsp;{ <span class="c008">;</span> <a class="syntax" href="#method-type"><span class="c014">method-type</span></a> }] <span class="c008">&gt;</span>
is a record of method types.</p><p>Each method may have an explicit polymorphic type: { <span class="c008">'</span> <a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a> }<sup>+</sup>
<span class="c008">.</span> &nbsp;<a class="syntax" href="#typexpr"><span class="c014">typexpr</span></a>. Explicit polymorphic variables have a local scope, and
an explicit polymorphic type can only be unified to an
equivalent one, where only the order and names of polymorphic
variables may change.</p><p>The type <span class="c008">&lt;</span> {<a class="syntax" href="#method-type"><span class="c014">method-type</span></a> <span class="c008">;</span>} <span class="c005"><span class="c007">..</span> <span class="c007">&gt;</span></span> is the
type of an object whose method names and types are described by
<a class="syntax" href="#method-type"><span class="c014">method-type</span></a><sub>1</sub>, …, &nbsp;<a class="syntax" href="#method-type"><span class="c014">method-type</span></a><sub><span class="c013">n</span></sub>, and possibly some other
methods represented by the ellipsis. This ellipsis actually is
a special kind of type variable (called <em>row variable</em> in the
literature) that stands for any number of extra method types.</p><h4 class="subsubsection" id="sec100">#-types</h4>
<p>
<a id="s:sharp-types"></a></p><p>The type <span class="c008">#</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> is a special kind of abbreviation. This
abbreviation unifies with the type of any object belonging to a subclass
of class <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a>.
It is handled in a special way as it usually hides a type variable (an
ellipsis, representing the methods that may be added in a subclass).
In particular, it vanishes when the ellipsis gets instantiated.
Each type expression <span class="c008">#</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> defines a new type variable, so
type <span class="c008">#</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> <span class="c005"><span class="c007">-&gt;</span> <span class="c007">#</span></span> &nbsp;<a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> is usually not the same as
type (<span class="c008">#</span> <a class="syntax" href="names.html#class-path"><span class="c014">class-path</span></a> <span class="c005"><span class="c007">as</span> <span class="c007">'</span></span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>) <span class="c005"><span class="c007">-&gt;</span> <span class="c007">'</span></span> &nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>.
</p><p>Use of #-types to abbreviate polymorphic variant types is deprecated.
If <span class="c014">t</span> is an exact variant type then <span class="c008">#</span><span class="c014">t</span> translates to <span class="c005"><span class="c007">[&lt;</span> <span class="c014">t</span><span class="c007">]</span></span>,
and <span class="c005"><span class="c007">#</span><span class="c014">t</span><span class="c007">[&gt;</span> <span class="c007">`</span></span><a class="syntax" href="names.html#tag-name"><span class="c014">tag</span></a><sub>1</sub> …<span class="c008">`</span>&nbsp;<a class="syntax" href="names.html#tag-name"><span class="c014">tag</span></a><sub><span class="c013">k</span></sub><span class="c008">]</span> translates to
<span class="c005"><span class="c007">[&lt;</span> <span class="c014">t</span> <span class="c007">&gt;</span> <span class="c007">`</span></span><a class="syntax" href="names.html#tag-name"><span class="c014">tag</span></a><sub>1</sub> …<span class="c008">`</span>&nbsp;<a class="syntax" href="names.html#tag-name"><span class="c014">tag</span></a><sub><span class="c013">k</span></sub><span class="c008">]</span></p><h4 class="subsubsection" id="sec101">Variant and record types</h4>
<p>There are no type expressions describing (defined) variant types nor
record types, since those are always named, i.e. defined before use
and referred to by name. Type definitions are described in
section&nbsp;<a href="typedecl.html#s%3Atype-defs">6.8.1</a>.

</p>






</section><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>