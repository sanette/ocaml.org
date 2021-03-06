<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="language.html">The OCaml language</a></li><li class="active"><a href="extn.html">Language extensions</a></li></ul>




<h1 class="chapter" id="sec238"><span>Chapter 8</span>&nbsp;&nbsp;Language extensions</h1>
<p> <a id="c:extensions"></a>
</p><p>This chapter describes language extensions and convenience features
that are implemented in OCaml, but not described in the
OCaml reference manual.</p><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.10</a></div><div class="toc_title"><a href="#">Language extensions</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="letrecvalues.html#start-section">1&nbsp;&nbsp;Recursive definitions of values</a>
</li><li><a href="manual024.html#start-section">2&nbsp;&nbsp;Recursive modules</a>
</li><li><a href="privatetypes.html#start-section">3&nbsp;&nbsp;Private types</a>
</li><li><a href="locallyabstract.html#start-section">4&nbsp;&nbsp;Locally abstract types</a>
</li><li><a href="firstclassmodules.html#start-section">5&nbsp;&nbsp;First-class modules</a>
</li><li><a href="moduletypeof.html#start-section">6&nbsp;&nbsp;Recovering the type of a module</a>
</li><li><a href="signaturesubstitution.html#start-section">7&nbsp;&nbsp;Substituting inside a signature</a>
</li><li><a href="modulealias.html#start-section">8&nbsp;&nbsp;Type-level module aliases</a>
</li><li><a href="overridingopen.html#start-section">9&nbsp;&nbsp;Overriding in open statements</a>
</li><li><a href="gadts.html#start-section">10&nbsp;&nbsp;Generalized algebraic datatypes</a>
</li><li><a href="bigarray.html#start-section">11&nbsp;&nbsp;Syntax for Bigarray access</a>
</li><li><a href="attributes.html#start-section">12&nbsp;&nbsp;Attributes</a>
</li><li><a href="extensionnodes.html#start-section">13&nbsp;&nbsp;Extension nodes</a>
</li><li><a href="extensiblevariants.html#start-section">14&nbsp;&nbsp;Extensible variant types</a>
</li><li><a href="generativefunctors.html#start-section">15&nbsp;&nbsp;Generative functors</a>
</li><li><a href="extensionsyntax.html#start-section">16&nbsp;&nbsp;Extension-only syntax</a>
</li><li><a href="inlinerecords.html#start-section">17&nbsp;&nbsp;Inline records</a>
</li><li><a href="doccomments.html#start-section">18&nbsp;&nbsp;Documentation comments</a>
</li><li><a href="indexops.html#start-section">19&nbsp;&nbsp;Extended indexing operators </a>
</li><li><a href="emptyvariants.html#start-section">20&nbsp;&nbsp;Empty variant types</a>
</li><li><a href="alerts.html#start-section">21&nbsp;&nbsp;Alerts</a>
</li><li><a href="generalizedopens.html#start-section">22&nbsp;&nbsp;Generalized open statements</a>
</li><li><a href="bindingops.html#start-section">23&nbsp;&nbsp;Binding operators</a>
</li></ul></nav></header><a id="start-section"></a><section id="section">




<h2 class="section" id="s:first-class-modules"><a class="section-anchor" href="#s:first-class-modules" aria-hidden="true"></a>5&nbsp;&nbsp;First-class modules</h2>
<p>
<a id="hevea_manual.kwd212"></a>
<a id="hevea_manual.kwd213"></a>
<a id="hevea_manual.kwd214"></a>
<a id="hevea_manual.kwd215"></a>
</p><p>(Introduced in OCaml 3.12; pattern syntax and package type inference
introduced in 4.00; structural comparison of package types introduced in 4.02.;
fewer parens required starting from 4.05)</p><div class="syntax"><table class="display dcenter"><tbody><tr class="c019"><td class="dcell"><table class="c001 cellpading0"><tbody><tr><td class="c018">
<a class="syntax" href="types.html#typexpr"><span class="c010">typexpr</span></a></td><td class="c015">::=</td><td class="c017">
...
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td><td class="c015">∣</td><td class="c017">&nbsp;<span class="c004">(module</span>&nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a><span class="c004">)</span>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
<tr><td class="c018">
<a class="syntax" href="modules.html#module-expr"><span class="c010">module-expr</span></a></td><td class="c015">::=</td><td class="c017">
...
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td><td class="c015">∣</td><td class="c017">&nbsp;<span class="c004">(val</span>&nbsp;<a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a>&nbsp;&nbsp;[<span class="c004">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a>]<span class="c004">)</span>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
<tr><td class="c018">
<a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a></td><td class="c015">::=</td><td class="c017">
...
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td><td class="c015">∣</td><td class="c017">&nbsp;<span class="c004">(module</span>&nbsp;<a class="syntax" href="modules.html#module-expr"><span class="c010">module-expr</span></a>&nbsp;&nbsp;[<span class="c004">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a>]<span class="c004">)</span>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
<tr><td class="c018">
<a class="syntax" href="patterns.html#pattern"><span class="c010">pattern</span></a></td><td class="c015">::=</td><td class="c017">
...
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td><td class="c015">∣</td><td class="c017">&nbsp;<span class="c004">(module</span>&nbsp;<a class="syntax" href="names.html#module-name"><span class="c010">module-name</span></a>&nbsp;&nbsp;[<span class="c004">:</span>&nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a>]<span class="c004">)</span>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
<tr><td class="c018">
<a class="syntax" id="package-type"><span class="c010">package-type</span></a></td><td class="c015">::=</td><td class="c017">
<a class="syntax" href="names.html#modtype-path"><span class="c010">modtype-path</span></a>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td><td class="c015">∣</td><td class="c017">&nbsp;<a class="syntax" href="names.html#modtype-path"><span class="c010">modtype-path</span></a>&nbsp;<span class="c004">with</span>&nbsp;&nbsp;<a class="syntax" href="#package-constraint"><span class="c010">package-constraint</span></a>&nbsp;&nbsp;{&nbsp;<span class="c004">and</span>&nbsp;<a class="syntax" href="#package-constraint"><span class="c010">package-constraint</span></a>&nbsp;}
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
<tr><td class="c018">
<a class="syntax" id="package-constraint"><span class="c010">package-constraint</span></a></td><td class="c015">::=</td><td class="c017">
<span class="c004">type</span>&nbsp;<a class="syntax" href="names.html#typeconstr"><span class="c010">typeconstr</span></a>&nbsp;<span class="c004">=</span>&nbsp;&nbsp;<a class="syntax" href="types.html#typexpr"><span class="c010">typexpr</span></a>
&nbsp;</td></tr>
<tr><td class="c018">&nbsp;</td></tr>
</tbody></table></td></tr>
</tbody></table></div><p>Modules are typically thought of as static components. This extension
makes it possible to pack a module as a first-class value, which can
later be dynamically unpacked into a module.</p><p>The expression <span class="c002"><span class="c003">(</span> <span class="c003">module</span></span> <a class="syntax" href="modules.html#module-expr"><span class="c010">module-expr</span></a> <span class="c004">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c004">)</span> converts the
module (structure or functor) denoted by module expression <a class="syntax" href="modules.html#module-expr"><span class="c010">module-expr</span></a>
to a value of the core language that encapsulates this module. The
type of this core language value is <span class="c002"><span class="c003">(</span> <span class="c003">module</span></span> <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c004">)</span>.
The <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> annotation can be omitted if it can be inferred
from the context.</p><p>Conversely, the module expression <span class="c002"><span class="c003">(</span> <span class="c003">val</span></span> <a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a> <span class="c004">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c004">)</span>
evaluates the core language expression <a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a> to a value, which must
have type <span class="c004">module</span> <a class="syntax" href="#package-type"><span class="c010">package-type</span></a>, and extracts the module that was
encapsulated in this value. Again <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> can be omitted if the
type of <a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a> is known.
If the module expression is already parenthesized, like the arguments
of functors are, no additional parens are needed: <span class="c003">Map.Make(val key)</span>.</p><p>The pattern <span class="c002"><span class="c003">(</span> <span class="c003">module</span></span> <a class="syntax" href="names.html#module-name"><span class="c010">module-name</span></a> <span class="c004">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c004">)</span> matches a
package with type <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> and binds it to <a class="syntax" href="names.html#module-name"><span class="c010">module-name</span></a>.
It is not allowed in toplevel let bindings.
Again <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> can be omitted if it can be inferred from the
enclosing pattern.</p><p>The <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> syntactic class appearing in the <span class="c002"><span class="c003">(</span> <span class="c003">module</span></span>
<a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c004">)</span> type expression and in the annotated forms represents a
subset of module types.
This subset consists of named module types with optional constraints
of a limited form: only non-parametrized types can be specified.</p><p>For type-checking purposes (and starting from OCaml 4.02), package types
are compared using the structural comparison of module types.</p><p>In general, the module expression <span class="c002"><span class="c003">(</span> <span class="c003">val</span></span> <a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a> <span class="c004">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a>
<span class="c004">)</span> cannot be used in the body of a functor, because this could cause
unsoundness in conjunction with applicative functors.
Since OCaml 4.02, this is relaxed in two ways:
if <a class="syntax" href="#package-type"><span class="c010">package-type</span></a> does not contain nominal type declarations (<em>i.e.</em> types that are created with a proper identity), then this
expression can be used anywhere, and even if it contains such types
it can be used inside the body of a generative
functor, described in section&nbsp;<a href="generativefunctors.html#s%3Agenerative-functors">8.15</a>.
It can also be used anywhere in the context of a local module binding
<span class="c002"><span class="c003">let</span> <span class="c003">module</span></span> <a class="syntax" href="names.html#module-name"><span class="c010">module-name</span></a> <span class="c002"><span class="c003">=</span> <span class="c003">(</span> <span class="c003">val</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a><sub>1</sub> <span class="c004">:</span> &nbsp;<a class="syntax" href="#package-type"><span class="c010">package-type</span></a> <span class="c002"><span class="c003">)</span>
<span class="c003">in</span></span> &nbsp;<a class="syntax" href="expr.html#expr"><span class="c010">expr</span></a><sub>2</sub>.</p>
<h5 class="paragraph" id="p:fst-mod-example"><a class="section-anchor" href="#p:fst-mod-example" aria-hidden="true">﻿</a>Basic example</h5>
<p> A typical use of first-class modules is to
select at run-time among several implementations of a signature.
Each implementation is a structure that we can encapsulate as a
first-class module, then store in a data structure such as a hash
table:


</p><div class="caml-example verbatim">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> picture = …
 <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> DEVICE = <span class="ocamlkeyword">sig</span>
   <span class="ocamlkeyword">val</span> draw : picture -&gt; unit
   …
 <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">let</span> devices : (string, (<span class="ocamlkeyword">module</span> DEVICE)) Hashtbl.t = Hashtbl.create 17

 <span class="ocamlkeyword">module</span> SVG = <span class="ocamlkeyword">struct</span> … <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">let</span> _ = Hashtbl.add devices <span class="ocamlstring">"SVG"</span> (<span class="ocamlkeyword">module</span> SVG : DEVICE)

 <span class="ocamlkeyword">module</span> PDF = <span class="ocamlkeyword">struct</span> … <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">let</span> _ = Hashtbl.add devices <span class="ocamlstring">"PDF"</span> (<span class="ocamlkeyword">module</span> PDF : DEVICE)</div></div>

</div><p>We can then select one implementation based on command-line
arguments, for instance:


</p><div class="caml-example verbatim">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> parse_cmdline () = …
 <span class="ocamlkeyword">module</span> Device =
   (<span class="ocamlkeyword">val</span> (<span class="ocamlkeyword">let</span> device_name = parse_cmdline () <span class="ocamlkeyword">in</span>
         <span class="ocamlkeyword">try</span> Hashtbl.find devices device_name
         <span class="ocamlkeyword">with</span> Not_found -&gt;
           Printf.eprintf <span class="ocamlstring">"Unknown device %s\n"</span> device_name;
           exit 2)
    : DEVICE)</div></div>

</div><p>


Alternatively, the selection can be performed within a function:


</p><div class="caml-example verbatim">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> draw_using_device device_name picture =
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">module</span> Device =
     (<span class="ocamlkeyword">val</span> (Hashtbl.find devices device_name) : DEVICE)
   <span class="ocamlkeyword">in</span>
   Device.draw picture</div></div>

</div>
<h5 class="paragraph" id="p:fst-mod-advexamples"><a class="section-anchor" href="#p:fst-mod-advexamples" aria-hidden="true">﻿</a>Advanced examples</h5>
<p>
With first-class modules, it is possible to parametrize some code over the
implementation of a module without using a functor.</p><div class="caml-example verbatim">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sort (<span class="ocamlkeyword">type</span> s) (<span class="ocamlkeyword">module</span> Set : Set.S <span class="ocamlkeyword">with</span> <span class="ocamlkeyword">type</span> elt = s) l =
   Set.elements (List.fold_right Set.add l Set.empty)</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sort : (<span class="ocamlkeyword">module</span> Set.S <span class="ocamlkeyword">with</span> <span class="ocamlkeyword">type</span> elt = 's) -&gt; 's list -&gt; 's list = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>To use this function, one can wrap the <span class="c003">Set.Make</span> functor:</p><div class="caml-example verbatim">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> make_set (<span class="ocamlkeyword">type</span> s) cmp =
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">module</span> S = Set.Make(<span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">type</span> t = s
     <span class="ocamlkeyword">let</span> compare = cmp
   <span class="ocamlkeyword">end</span>) <span class="ocamlkeyword">in</span>
   (<span class="ocamlkeyword">module</span> S : Set.S <span class="ocamlkeyword">with</span> <span class="ocamlkeyword">type</span> elt = s)</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> make_set : ('s -&gt; 's -&gt; int) -&gt; (<span class="ocamlkeyword">module</span> Set.S <span class="ocamlkeyword">with</span> <span class="ocamlkeyword">type</span> elt = 's) = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div>






</section><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>