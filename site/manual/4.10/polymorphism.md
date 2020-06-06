<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="coreexamples.html">The core language</a></li><li><a href="moduleexamples.html">The module system</a></li><li><a href="objectexamples.html">Objects in OCaml</a></li><li><a href="lablexamples.html">Labels and variants</a></li><li class="active"><a href="polymorphism.html">Polymorphism and its limitations</a></li><li><a href="advexamples.html">Advanced examples with classes and modules</a></li></ul>




<h1 class="chapter" id="sec53"><span>Chapter 5</span>&nbsp;&nbsp;Polymorphism and its limitations</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.10</a></div><div class="toc_title"><a href="#">Polymorphism and its limitations</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="polymorphism.html#s%3Aweak-polymorphism">1&nbsp;&nbsp;Weak polymorphism and mutation</a>
</li><li><a href="polymorphism.html#s%3Apolymorphic-recursion">2&nbsp;&nbsp;Polymorphic recursion</a>
</li><li><a href="polymorphism.html#s%3Ahigher-rank-poly">3&nbsp;&nbsp;Higher-rank polymorphic functions</a>
</li></ul></nav></header>
<p><a id="c:polymorphism"></a>
</p><p><br>
<br>
</p><p>This chapter covers more advanced questions related to the
limitations of polymorphic functions and types. There are some situations
in OCaml where the type inferred by the type checker may be less generic
than expected. Such non-genericity can stem either from interactions
between side-effect and typing or the difficulties of implicit polymorphic
recursion and higher-rank polymorphism.</p><p>This chapter details each of these situations and, if it is possible,
how to recover genericity.</p>
<h2 class="section" id="s:weak-polymorphism"><a class="section-anchor" href="#s:weak-polymorphism" aria-hidden="true"></a>1&nbsp;&nbsp;Weak polymorphism and mutation</h2>
<h3 class="subsection" id="ss:weak-types"><a class="section-anchor" href="#ss:weak-types" aria-hidden="true">﻿</a>1.1&nbsp;&nbsp;Weakly polymorphic types</h3>
<p>
Maybe the most frequent examples of non-genericity derive from the
interactions between polymorphic types and mutation. A simple example
appears when typing the following expression


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> store = <span class="ocamlkeyword">ref</span> None ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> store : '_weak1 option <span class="ocamlkeyword">ref</span> = {contents = None}</div></div>

</div><p>


Since the type of <span class="c003">None</span> is <span class="c003">'a option</span> and the function <span class="c003">ref</span> has type
<span class="c003">'b -&gt; 'b ref</span>, a natural deduction for the type of <span class="c003">store</span> would be
<span class="c003">'a option ref</span>. However, the inferred type, <span class="c003">'_weak1 option ref</span>, is
different. Type variables whose name starts with a <span class="c003">_weak</span> prefix like
<span class="c003">'_weak1</span> are weakly polymorphic type variables, sometimes shortened as
weak type variables.
A weak type variable is a placeholder for a single type that is currently
unknown. Once the specific type <span class="c003">t</span> behind the placeholder type <span class="c003">'_weak1</span>
is known, all occurrences of <span class="c003">'_weak1</span> will be replaced by <span class="c003">t</span>. For instance,
we can define another option reference and store an <span class="c003">int</span> inside:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> another_store = <span class="ocamlkeyword">ref</span> None ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> another_store : '_weak2 option <span class="ocamlkeyword">ref</span> = {contents = None}</div></div>
<div class="ocaml">



<div class="pre caml-input"> another_store := Some 0;
 another_store ;;</div>



<div class="pre caml-output ok">- : int option <span class="ocamlkeyword">ref</span> = {contents = Some 0}</div></div>

</div><p>


After storing an <span class="c003">int</span> inside <span class="c003">another_store</span>, the type of <span class="c003">another_store</span> has
been updated from <span class="c003">'_weak2 option ref</span> to <span class="c003">int option ref</span>.
This distinction between weakly and generic polymorphic type variable protects
OCaml programs from unsoundness and runtime errors. To understand from where
unsoundness might come, consider this simple function which swaps a value <span class="c003">x</span>
with the value stored inside a <span class="c003">store</span> reference, if there is such value:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> swap store x = <span class="ocamlkeyword">match</span> !store <span class="ocamlkeyword">with</span>
   | None -&gt; store := Some x; x
   | Some y -&gt; store := Some x; y;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> swap : 'a option <span class="ocamlkeyword">ref</span> -&gt; 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


We can apply this function to our store


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> one = swap store 1
 <span class="ocamlkeyword">let</span> one_again = swap store 2
 <span class="ocamlkeyword">let</span> two = swap store 3;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> one : int = 1
<span class="ocamlkeyword">val</span> one_again : int = 1
<span class="ocamlkeyword">val</span> two : int = 2</div></div>

</div><p>


After these three swaps the stored value is <span class="c003">3</span>. Everything is fine up to
now. We can then try to swap <span class="c003">3</span> with a more interesting value, for
instance a function:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> error = swap store <span class="ocamlhighlight">(fun x -&gt; x)</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression should not be a function, the expected type is int</div></div>

</div><p>


At this point, the type checker rightfully complains that it is not
possible to swap an integer and a function, and that an <span class="c003">int</span> should always
be traded for another <span class="c003">int</span>. Furthermore, the type checker prevents us to
change manually the type of the value stored by <span class="c003">store</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> store := Some <span class="ocamlhighlight">(fun x -&gt; x)</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression should not be a function, the expected type is int</div></div>

</div><p>


Indeed, looking at the type of store, we see that the weak type <span class="c003">'_weak1</span> has
been replaced by the type <span class="c003">int</span>


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> store;;</div>



<div class="pre caml-output ok">- : int option <span class="ocamlkeyword">ref</span> = {contents = Some 3}</div></div>

</div><p>


Therefore, after placing an <span class="c003">int</span> in <span class="c003">store</span>, we cannot use it to store any
value other than an <span class="c003">int</span>. More generally, weak types protect the program from
undue mutation of values with a polymorphic type.</p><p>Moreover, weak types cannot appear in the signature of toplevel modules:
types must be known at compilation time. Otherwise, different compilation
units could replace the weak type with different and incompatible types.
For this reason, compiling the following small piece of code
</p><pre>let option_ref = ref None
</pre><p>yields a compilation error
</p><pre>Error: The type of this expression, '_weak1 option ref,
       contains type variables that cannot be generalized
</pre><p>To solve this error, it is enough to add an explicit type annotation to
specify the type at declaration time:
</p><pre>let option_ref: int option ref = ref None
</pre><p>This is in any case a good practice for such global mutable variables.
Otherwise, they will pick out the type of first use. If there is a mistake
at this point, this can result in confusing type errors when later, correct
uses are flagged as errors.</p>
<h3 class="subsection" id="ss:valuerestriction"><a class="section-anchor" href="#ss:valuerestriction" aria-hidden="true">﻿</a>1.2&nbsp;&nbsp;The value restriction</h3>
<p>Identifying the exact context in which polymorphic types should be
replaced by weak types in a modular way is a difficult question. Indeed
the type system must handle the possibility that functions may hide persistent
mutable states. For instance, the following function uses an internal reference
to implement a delayed identity function


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> make_fake_id () =
   <span class="ocamlkeyword">let</span> store = <span class="ocamlkeyword">ref</span> None <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">fun</span> x -&gt; swap store x ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> make_fake_id : unit -&gt; 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> fake_id = make_fake_id();;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> fake_id : '_weak3 -&gt; '_weak3 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


It would be unsound to apply this <span class="c003">fake_id</span> function to values with different
types. The function <span class="c003">fake_id</span> is therefore rightfully assigned the type
<span class="c003">'_weak3 -&gt; '_weak3</span> rather than <span class="c003">'a -&gt; 'a</span>. At the same time, it ought to
be possible to use a local mutable state without impacting the type of a
function.
</p><p>To circumvent these dual difficulties, the type checker considers that any value
returned by a function might rely on persistent mutable states behind the scene
and should be given a weak type. This restriction on the type of mutable
values and the results of function application is called the value restriction.
Note that this value restriction is conservative: there are situations where the
value restriction is too cautious and gives a weak type to a value that could be
safely generalized to a polymorphic type:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> not_id = (<span class="ocamlkeyword">fun</span> x -&gt; x) (<span class="ocamlkeyword">fun</span> x -&gt; x);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> not_id : '_weak4 -&gt; '_weak4 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Quite often, this happens when defining function using higher order function.
To avoid this problem, a solution is to add an explicit argument to the
function:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> id_again = <span class="ocamlkeyword">fun</span> x -&gt; (<span class="ocamlkeyword">fun</span> x -&gt; x) (<span class="ocamlkeyword">fun</span> x -&gt; x) x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> id_again : 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


With this argument, <span class="c003">id_again</span> is seen as a function definition by the type
checker and can therefore be generalized. This kind of manipulation is called
eta-expansion in lambda calculus and is sometimes referred under this name.</p>
<h3 class="subsection" id="ss:relaxed-value-restriction"><a class="section-anchor" href="#ss:relaxed-value-restriction" aria-hidden="true">﻿</a>1.3&nbsp;&nbsp;The relaxed value restriction</h3>
<p>There is another partial solution to the problem of unnecessary weak type,
which is implemented directly within the type checker. Briefly, it is possible
to prove that weak types that only appear as type parameters in covariant
positions –also called positive positions– can be safely generalized to
polymorphic types. For instance, the type <span class="c003">'a list</span> is covariant in <span class="c003">'a</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> f () = [];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> f : unit -&gt; 'a list = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> empty = f ();;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> empty : 'a list = []</div></div>

</div><p>


Remark that the type inferred for <span class="c003">empty</span> is <span class="c003">'a list</span> and not <span class="c003">'_weak5 list</span>
that should have occurred with the value restriction since <span class="c003">f ()</span> is a
function application.</p><p>The value restriction combined with this generalization for covariant type
parameters is called the relaxed value restriction.</p>
<h3 class="subsection" id="ss:variance-and-value-restriction"><a class="section-anchor" href="#ss:variance-and-value-restriction" aria-hidden="true">﻿</a>1.4&nbsp;&nbsp;Variance and value restriction</h3>
<p>
Variance describes how type constructors behave with respect to subtyping.
Consider for instance a pair of type <span class="c003">x</span> and <span class="c003">xy</span> with <span class="c003">x</span> a subtype of <span class="c003">xy</span>,
denoted <span class="c003">x :&gt; xy</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> x = [ `X ];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> x = [ `X ]</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> xy = [ `X | `Y ];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> xy = [ `X | `Y ]</div></div>

</div><p>


As <span class="c003">x</span> is a subtype of <span class="c003">xy</span>, we can convert a value of type <span class="c003">x</span>
to a value of type <span class="c003">xy</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> x:x = `X;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> x : x = `X</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> x' = ( x :&gt; xy);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> x' : xy = `X</div></div>

</div><p>


Similarly, if we have a value of type <span class="c003">x list</span>, we can convert it to a value
of type <span class="c003">xy list</span>, since we could convert each element one by one:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> l:x list = [`X; `X];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : x list = [`X; `X]</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> l' = ( l :&gt; xy list);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l' : xy list = [`X; `X]</div></div>

</div><p>


In other words, <span class="c003">x :&gt; xy</span> implies that <span class="c003">x list :&gt; xy list</span>, therefore
the type constructor <span class="c003">'a list</span> is covariant (it preserves subtyping)
in its parameter <span class="c003">'a</span>.</p><p>Contrarily, if we have a function that can handle values of type <span class="c003">xy</span>


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> f: xy -&gt; unit = <span class="ocamlkeyword">function</span>
   | `X -&gt; ()
   | `Y -&gt; ();;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> f : xy -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


it can also handle values of type <span class="c003">x</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> f' = (f :&gt; x -&gt; unit);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> f' : x -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Note that we can rewrite the type of <span class="c003">f</span> and <span class="c003">f'</span> as


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> 'a proc = 'a -&gt; unit
   <span class="ocamlkeyword">let</span> f' = (f: xy proc :&gt; x proc);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a proc = 'a -&gt; unit
<span class="ocamlkeyword">val</span> f' : x proc = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


In this case, we have <span class="c003">x :&gt; xy</span> implies <span class="c003">xy proc :&gt; x proc</span>. Notice
that the second subtyping relation reverse the order of <span class="c003">x</span> and <span class="c003">xy</span>:
the type constructor <span class="c003">'a proc</span> is contravariant in its parameter <span class="c003">'a</span>.
More generally, the function type constructor <span class="c003">'a -&gt; 'b</span> is covariant in
its return type <span class="c003">'b</span> and contravariant in its argument type <span class="c003">'a</span>.</p><p>A type constructor can also be invariant in some of its type parameters,
neither covariant nor contravariant. A typical example is a reference:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> x: x <span class="ocamlkeyword">ref</span> = <span class="ocamlkeyword">ref</span> `X;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> x : x <span class="ocamlkeyword">ref</span> = {contents = `X}</div></div>

</div><p>


If we were able to coerce <span class="c003">x</span> to the type <span class="c003">xy ref</span> as a variable <span class="c003">xy</span>,
we could use <span class="c003">xy</span> to store the value <span class="c003">`Y</span> inside the reference and then use
the <span class="c003">x</span> value to read this content as a value of type <span class="c003">x</span>,
which would break the type system.</p><p>More generally, as soon as a type variable appears in a position describing
mutable state it becomes invariant. As a corollary, covariant variables will
never denote mutable locations and can be safely generalized.
For a better description, interested readers can consult the original
article by Jacques Garrigue on
<a href="http://www.math.nagoya-u.ac.jp/~garrigue/papers/morepoly-long.pdf"><span class="c003">http://www.math.nagoya-u.ac.jp/~garrigue/papers/morepoly-long.pdf</span></a></p><p>Together, the relaxed value restriction and type parameter covariance
help to avoid eta-expansion in many situations.</p>
<h3 class="subsection" id="ss:variance:abstract-data-types"><a class="section-anchor" href="#ss:variance:abstract-data-types" aria-hidden="true">﻿</a>1.5&nbsp;&nbsp;Abstract data types</h3>
<p>
Moreover, when the type definitions are exposed, the type checker
is able to infer variance information on its own and one can benefit from
the relaxed value restriction even unknowingly. However, this is not the case
anymore when defining new abstract types. As an illustration, we can define a
module type collection as:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> COLLECTION = <span class="ocamlkeyword">sig</span>
   <span class="ocamlkeyword">type</span> 'a t
   <span class="ocamlkeyword">val</span> empty: unit -&gt; 'a t
 <span class="ocamlkeyword">end</span>

 <span class="ocamlkeyword">module</span> Implementation = <span class="ocamlkeyword">struct</span>
   <span class="ocamlkeyword">type</span> 'a t = 'a list
   <span class="ocamlkeyword">let</span> empty ()= []
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> COLLECTION = <span class="ocamlkeyword">sig</span> <span class="ocamlkeyword">type</span> 'a t <span class="ocamlkeyword">val</span> empty : unit -&gt; 'a t <span class="ocamlkeyword">end</span>
<span class="ocamlkeyword">module</span> Implementation :
  <span class="ocamlkeyword">sig</span> <span class="ocamlkeyword">type</span> 'a t = 'a list <span class="ocamlkeyword">val</span> empty : unit -&gt; 'a list <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> List2: COLLECTION = Implementation;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">module</span> List2 : COLLECTION</div></div>

</div><p>In this situation, when coercing the module <span class="c003">List2</span> to the module type
<span class="c003">COLLECTION</span>, the type checker forgets that <span class="c003">'a List2.t</span> was covariant
in <span class="c003">'a</span>. Consequently, the relaxed value restriction does not apply anymore:</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   List2.empty ();;</div>



<div class="pre caml-output ok">- : '_weak5 List2.t = &lt;abstr&gt;</div></div>

</div><p>To keep the relaxed value restriction, we need to declare the abstract type
<span class="c003">'a COLLECTION.t</span> as covariant in <span class="c003">'a</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> COLLECTION = <span class="ocamlkeyword">sig</span>
   <span class="ocamlkeyword">type</span> +'a t
   <span class="ocamlkeyword">val</span> empty: unit -&gt; 'a t
 <span class="ocamlkeyword">end</span>

 <span class="ocamlkeyword">module</span> List2: COLLECTION = Implementation;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> COLLECTION = <span class="ocamlkeyword">sig</span> <span class="ocamlkeyword">type</span> +'a t <span class="ocamlkeyword">val</span> empty : unit -&gt; 'a t <span class="ocamlkeyword">end</span>
<span class="ocamlkeyword">module</span> List2 : COLLECTION</div></div>

</div><p>We then recover polymorphism:</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   List2.empty ();;</div>



<div class="pre caml-output ok">- : 'a List2.t = &lt;abstr&gt;</div></div>

</div>
<h2 class="section" id="s:polymorphic-recursion"><a class="section-anchor" href="#s:polymorphic-recursion" aria-hidden="true">﻿</a>2&nbsp;&nbsp;Polymorphic recursion</h2>
<p>The second major class of non-genericity is directly related to the problem
of type inference for polymorphic functions. In some circumstances, the type
inferred by OCaml might be not general enough to allow the definition of
some recursive functions, in particular for recursive function acting on
non-regular algebraic data type.</p><p>With a regular polymorphic algebraic data type, the type parameters of
the type constructor are constant within the definition of the type. For
instance, we can look at arbitrarily nested list defined as:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> 'a regular_nested = List <span class="ocamlkeyword">of</span> 'a list | Nested <span class="ocamlkeyword">of</span> 'a regular_nested list
   <span class="ocamlkeyword">let</span> l = Nested[ List [1]; Nested [List[2;3]]; Nested[Nested[]] ];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a regular_nested = List <span class="ocamlkeyword">of</span> 'a list | Nested <span class="ocamlkeyword">of</span> 'a regular_nested list
<span class="ocamlkeyword">val</span> l : int regular_nested =
  Nested [List [1]; Nested [List [2; 3]]; Nested [Nested []]]</div></div>

</div><p>


Note that the type constructor <span class="c003">regular_nested</span> always appears as
<span class="c003">'a regular_nested</span> in the definition above, with the same parameter
<span class="c003">'a</span>. Equipped with this type, one can compute a maximal depth with
a classic recursive function


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> maximal_depth = <span class="ocamlkeyword">function</span>
   | List _ -&gt; 1
   | Nested [] -&gt; 0
   | Nested (a::q) -&gt; 1 + max (maximal_depth a) (maximal_depth (Nested q));;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> maximal_depth : 'a regular_nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Non-regular recursive algebraic data types correspond to polymorphic algebraic
data types whose parameter types vary between the left and right side of
the type definition. For instance, it might be interesting to define a datatype
that ensures that all lists are nested at the same depth:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> 'a nested = List <span class="ocamlkeyword">of</span> 'a list | Nested <span class="ocamlkeyword">of</span> 'a list nested;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a nested = List <span class="ocamlkeyword">of</span> 'a list | Nested <span class="ocamlkeyword">of</span> 'a list nested</div></div>

</div><p>


Intuitively, a value of type <span class="c003">'a nested</span> is a list of list …of list of
elements <span class="c003">a</span> with <span class="c003">k</span> nested list. We can then adapt the <span class="c003">maximal_depth</span>
function defined on <span class="c003">regular_depth</span> into a <span class="c003">depth</span> function that computes this
<span class="c003">k</span>. As a first try, we may define


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> depth = <span class="ocamlkeyword">function</span>
   | List _ -&gt; 1
   | Nested n -&gt; 1 + depth <span class="ocamlhighlight">n</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type 'a list nested
       but an expression was expected of type 'a nested
       The type variable 'a occurs inside 'a list</div></div>

</div><p>


The type error here comes from the fact that during the definition of <span class="c003">depth</span>,
the type checker first assigns to <span class="c003">depth</span> the type <span class="c003">'a -&gt; 'b </span>.
When typing the pattern matching, <span class="c003">'a -&gt; 'b</span> becomes <span class="c003">'a nested -&gt; 'b</span>, then
<span class="c003">'a nested -&gt; int</span> once the <span class="c003">List</span> branch is typed.
However, when typing the application <span class="c003">depth n</span> in the <span class="c003">Nested</span> branch,
the type checker encounters a problem: <span class="c003">depth n</span> is applied to
<span class="c003">'a list nested</span>, it must therefore have the type
<span class="c003">'a list nested -&gt; 'b</span>. Unifying this constraint with the previous one
leads to the impossible constraint <span class="c003">'a list nested = 'a nested</span>.
In other words, within its definition, the recursive function <span class="c003">depth</span> is
applied to values of type <span class="c003">'a t</span> with different types <span class="c003">'a</span> due to the
non-regularity of the type constructor <span class="c003">nested</span>. This creates a problem because
the type checker had introduced a new type variable <span class="c003">'a</span> only at the
<em>definition</em> of the function <span class="c003">depth</span> whereas, here, we need a
different type variable for every <em>application</em> of the function <span class="c003">depth</span>.</p>
<h3 class="subsection" id="ss:explicit-polymorphism"><a class="section-anchor" href="#ss:explicit-polymorphism" aria-hidden="true">﻿</a>2.1&nbsp;&nbsp;Explicitly polymorphic annotations</h3>
<p>
The solution of this conundrum is to use an explicitly polymorphic type
annotation for the type <span class="c003">'a</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> depth: 'a. 'a nested -&gt; int = <span class="ocamlkeyword">function</span>
   | List _ -&gt; 1
   | Nested n -&gt; 1 + depth n;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> depth : 'a nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> depth ( Nested(List [ [7]; [8] ]) );;</div>



<div class="pre caml-output ok">- : int = 2</div></div>

</div><p>


In the type of <span class="c003">depth</span>, <span class="c003">'a.'a nested -&gt; int</span>, the type variable <span class="c003">'a</span>
is universally quantified. In other words, <span class="c003">'a.'a nested -&gt; int</span> reads as
“for all type <span class="c003">'a</span>, <span class="c003">depth</span> maps <span class="c003">'a nested</span> values to integers”.
Whereas the standard type <span class="c003">'a nested -&gt; int</span> can be interpreted
as “let be a type variable <span class="c003">'a</span>, then <span class="c003">depth</span> maps <span class="c003">'a nested</span> values
to integers”. There are two major differences with these two type
expressions. First, the explicit polymorphic annotation indicates to the
type checker that it needs to introduce a new type variable every times
the function <span class="c003">depth</span> is applied. This solves our problem with the definition
of the function <span class="c003">depth</span>.</p><p>Second, it also notifies the type checker that the type of the function should
be polymorphic. Indeed, without explicit polymorphic type annotation, the
following type annotation is perfectly valid


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> sum: 'a -&gt; 'b -&gt; 'c = <span class="ocamlkeyword">fun</span> x y -&gt; x + y;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sum : int -&gt; int -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


since <span class="c003">'a</span>,<span class="c003">'b</span> and <span class="c003">'c</span> denote type variables that may or may not be
polymorphic. Whereas, it is an error to unify an explicitly polymorphic type
with a non-polymorphic type:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> sum: 'a 'b 'c. 'a -&gt; 'b -&gt; 'c = <span class="ocamlhighlight">fun x y -&gt; x + y</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This definition has type int -&gt; int -&gt; int which is less general than
         'a 'b 'c. 'a -&gt; 'b -&gt; 'c</div></div>

</div><p>An important remark here is that it is not needed to explicit fully
the type of <span class="c003">depth</span>: it is sufficient to add annotations only for the
universally quantified type variables:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> depth: 'a. 'a nested -&gt; _ = <span class="ocamlkeyword">function</span>
   | List _ -&gt; 1
   | Nested n -&gt; 1 + depth n;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> depth : 'a nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> depth ( Nested(List [ [7]; [8] ]) );;</div>



<div class="pre caml-output ok">- : int = 2</div></div>

</div>
<h3 class="subsection" id="ss:recursive-poly-examples"><a class="section-anchor" href="#ss:recursive-poly-examples" aria-hidden="true">﻿</a>2.2&nbsp;&nbsp;More examples</h3>
<p>
With explicit polymorphic annotations, it becomes possible to implement
any recursive function that depends only on the structure of the nested
lists and not on the type of the elements. For instance, a more complex
example would be to compute the total number of elements of the nested
lists:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> len nested =
     <span class="ocamlkeyword">let</span> map_and_sum f = List.fold_left (<span class="ocamlkeyword">fun</span> acc x -&gt; acc + f x) 0 <span class="ocamlkeyword">in</span>
     <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> len: 'a. ('a list -&gt; int ) -&gt; 'a nested -&gt; int =
     <span class="ocamlkeyword">fun</span> nested_len n -&gt;
       <span class="ocamlkeyword">match</span> n <span class="ocamlkeyword">with</span>
       | List l -&gt; nested_len l
       | Nested n -&gt; len (map_and_sum nested_len) n
     <span class="ocamlkeyword">in</span>
   len List.length nested;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> len : 'a nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> len (Nested(Nested(List [ [ [1;2]; [3] ]; [ []; [4]; [5;6;7]]; [[]] ])));;</div>



<div class="pre caml-output ok">- : int = 7</div></div>

</div><p>Similarly, it may be necessary to use more than one explicitly
polymorphic type variables, like for computing the nested list of
list lengths of the nested list:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> shape n =
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> shape: 'a 'b. ('a nested -&gt; int nested) -&gt;
     ('b list list -&gt; 'a list) -&gt; 'b nested -&gt; int nested
     = <span class="ocamlkeyword">fun</span> nest nested_shape -&gt;
       <span class="ocamlkeyword">function</span>
       | List l -&gt; raise
        (Invalid_argument <span class="ocamlstring">"shape requires nested_list of depth greater than 1"</span>)
       | Nested (List l) -&gt; nest @@ List (nested_shape l)
       | Nested n -&gt;
         <span class="ocamlkeyword">let</span> nested_shape = List.map nested_shape <span class="ocamlkeyword">in</span>
         <span class="ocamlkeyword">let</span> nest x = nest (Nested x) <span class="ocamlkeyword">in</span>
         shape nest nested_shape n <span class="ocamlkeyword">in</span>
   shape (<span class="ocamlkeyword">fun</span> n -&gt; n ) (<span class="ocamlkeyword">fun</span> l -&gt; List.map List.length l ) n;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> shape : 'a nested -&gt; int nested = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> shape (Nested(Nested(List [ [ [1;2]; [3] ]; [ []; [4]; [5;6;7]]; [[]] ])));;</div>



<div class="pre caml-output ok">- : int nested = Nested (List [[2; 1]; [0; 1; 3]; [0]])</div></div>

</div>
<h2 class="section" id="s:higher-rank-poly"><a class="section-anchor" href="#s:higher-rank-poly" aria-hidden="true">﻿</a>3&nbsp;&nbsp;Higher-rank polymorphic functions</h2>
<p>Explicit polymorphic annotations are however not sufficient to cover all
the cases where the inferred type of a function is less general than
expected. A similar problem arises when using polymorphic functions as arguments
of higher-order functions. For instance, we may want to compute the average
depth or length of two nested lists:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> average_depth x y = (depth x + depth y) / 2;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> average_depth : 'a nested -&gt; 'b nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> average_len x y = (len x + len y) / 2;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> average_len : 'a nested -&gt; 'b nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> one = average_len (List [2]) (List [[]]);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> one : int = 1</div></div>

</div><p>


It would be natural to factorize these two definitions as:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">     <span class="ocamlkeyword">let</span> average f x y = (f x + f y) / 2;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> average : ('a -&gt; int) -&gt; 'a -&gt; 'a -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


However, the type of <span class="c003">average len</span> is less generic than the type of
<span class="c003">average_len</span>, since it requires the type of the first and second argument to
be the same:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   average_len (List [2]) (List [[]]);;</div>



<div class="pre caml-output ok">- : int = 1</div></div>
<div class="ocaml">



<div class="pre caml-input">   average len (List [2]) (List [<span class="ocamlhighlight">[]</span>]);;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type 'a list
       but an expression was expected of type int</div></div>

</div><p>As previously with polymorphic recursion, the problem stems from the fact that
type variables are introduced only at the start of the <span class="c003">let</span> definitions. When
we compute both <span class="c003">f x</span> and <span class="c003">f y</span>, the type of <span class="c003">x</span> and <span class="c003">y</span> are unified together.
To avoid this unification, we need to indicate to the type checker
that f is polymorphic in its first argument. In some sense, we would want
<span class="c003">average</span> to have type
</p><pre>val average: ('a. 'a nested -&gt; int) -&gt; 'a nested -&gt; 'b nested -&gt; int
</pre><p>Note that this syntax is not valid within OCaml: <span class="c003">average</span> has an universally
quantified type <span class="c003">'a</span> inside the type of one of its argument whereas for
polymorphic recursion the universally quantified type was introduced before
the rest of the type. This position of the universally quantified type means
that <span class="c003">average</span> is a second-rank polymorphic function. This kind of higher-rank
functions is not directly supported by OCaml: type inference for second-rank
polymorphic function and beyond is undecidable; therefore using this kind of
higher-rank functions requires to handle manually these universally quantified
types.</p><p>In OCaml, there are two ways to introduce this kind of explicit universally
quantified types: universally quantified record fields,


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">type</span> 'a nested_reduction = { f:'elt. 'elt nested -&gt; 'a };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a nested_reduction = { f : 'elt. 'elt nested -&gt; 'a; }</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> boxed_len = { f = len };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> boxed_len : int nested_reduction = {f = &lt;<span class="ocamlkeyword">fun</span>&gt;}</div></div>

</div><p>


and universally quantified object methods:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> obj_len = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> f:'a. 'a nested -&gt; 'b = len <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> obj_len : &lt; f : 'a. 'a nested -&gt; int &gt; = &lt;obj&gt;</div></div>

</div><p>


To solve our problem, we can therefore use either the record solution:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> average nsm x y = (nsm.f x + nsm.f y) / 2 ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> average : int nested_reduction -&gt; 'a nested -&gt; 'b nested -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


or the object one:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> average (obj:&lt;f:'a. 'a nested -&gt; _ &gt; ) x y = (obj#f x + obj#f y) / 2 ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> average : &lt; f : 'a. 'a nested -&gt; int &gt; -&gt; 'b nested -&gt; 'c nested -&gt; int =
  &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>