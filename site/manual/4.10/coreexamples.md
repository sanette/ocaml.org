<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li class="active"><a href="coreexamples.html">The core language</a></li><li><a href="moduleexamples.html">The module system</a></li><li><a href="objectexamples.html">Objects in OCaml</a></li><li><a href="lablexamples.html">Labels and variants</a></li><li><a href="polymorphism.html">Polymorphism and its limitations</a></li><li><a href="advexamples.html">Advanced examples with classes and modules</a></li></ul>




<h1 class="chapter" id="sec7"><span>Chapter 1</span>&nbsp;&nbsp;The core language</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.10</a></div><div class="toc_title"><a href="#">The core language</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="coreexamples.html#s%3Abasics">1&nbsp;&nbsp;Basics</a>
</li><li><a href="coreexamples.html#s%3Adatatypes">2&nbsp;&nbsp;Data types</a>
</li><li><a href="coreexamples.html#s%3Afunctions-as-values">3&nbsp;&nbsp;Functions as values</a>
</li><li><a href="coreexamples.html#s%3Atut-recvariants">4&nbsp;&nbsp;Records and variants</a>
</li><li><a href="coreexamples.html#s%3Aimperative-features">5&nbsp;&nbsp;Imperative features</a>
</li><li><a href="coreexamples.html#s%3Aexceptions">6&nbsp;&nbsp;Exceptions</a>
</li><li><a href="coreexamples.html#s%3Alazy-expr">7&nbsp;&nbsp;Lazy expressions</a>
</li><li><a href="coreexamples.html#s%3Asymb-expr">8&nbsp;&nbsp;Symbolic processing of expressions</a>
</li><li><a href="coreexamples.html#s%3Apretty-printing">9&nbsp;&nbsp;Pretty-printing</a>
</li><li><a href="coreexamples.html#s%3Aprintf">10&nbsp;&nbsp;Printf formats</a>
</li><li><a href="coreexamples.html#s%3Astandalone-programs">11&nbsp;&nbsp;Standalone OCaml programs</a>
</li></ul></nav></header>
<p> <a id="c:core-xamples"></a>
</p><p>This part of the manual is a tutorial introduction to the
OCaml language. A good familiarity with programming in a conventional
languages (say, C or Java) is assumed, but no prior exposure to
functional languages is required. The present chapter introduces the
core language. Chapter&nbsp;<a href="moduleexamples.html#c%3Amoduleexamples">2</a> deals with the
module system, chapter&nbsp;<a href="objectexamples.html#c%3Aobjectexamples">3</a> with the
object-oriented features, chapter&nbsp;<a href="lablexamples.html#c%3Alabl-examples">4</a> with
extensions to the core language (labeled arguments and polymorphic
variants), and chapter&nbsp;<a href="advexamples.html#c%3Aadvexamples">6</a> gives some advanced examples.</p>
<h2 class="section" id="s:basics"><a class="section-anchor" href="#s:basics" aria-hidden="true"></a>1&nbsp;&nbsp;Basics</h2>
<p>For this overview of OCaml, we use the interactive system, which
is started by running <span class="c003">ocaml</span> from the Unix shell, or by launching the
<span class="c003">OCamlwin.exe</span> application under Windows. This tutorial is presented
as the transcript of a session with the interactive system:
lines starting with <span class="c003">#</span> represent user input; the system responses are
printed below, without a leading <span class="c003">#</span>.</p><p>Under the interactive system, the user types OCaml phrases terminated
by <span class="c003">;;</span> in response to the <span class="c003">#</span> prompt, and the system compiles them
on the fly, executes them, and prints the outcome of evaluation.
Phrases are either simple expressions, or <span class="c003">let</span> definitions of
identifiers (either values or functions).


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> 1+2*3;;</div>



<div class="pre caml-output ok">- : int = 7</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> pi = 4.0 *. atan 1.0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> pi : float = 3.14159265358979312</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> square x = x *. x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> square : float -&gt; float = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> square (sin pi) +. square (cos pi);;</div>



<div class="pre caml-output ok">- : float = 1.</div></div>

</div><p>


The OCaml system computes both the value and the type for
each phrase. Even function parameters need no explicit type declaration:
the system infers their types from their usage in the
function. Notice also that integers and floating-point numbers are
distinct types, with distinct operators: <span class="c003">+</span> and <span class="c003">*</span> operate on
integers, but <span class="c003">+.</span> and <span class="c003">*.</span> operate on floats.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlhighlight">1.0</span> * 2;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type float but an expression was expected of type
         int</div></div>

</div><p>Recursive functions are defined with the <span class="c003">let rec</span> binding:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> fib n =
   <span class="ocamlkeyword">if</span> n &lt; 2 <span class="ocamlkeyword">then</span> n <span class="ocamlkeyword">else</span> fib (n-1) + fib (n-2);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> fib : int -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> fib 10;;</div>



<div class="pre caml-output ok">- : int = 55</div></div>

</div>
<h2 class="section" id="s:datatypes"><a class="section-anchor" href="#s:datatypes" aria-hidden="true">﻿</a>2&nbsp;&nbsp;Data types</h2>
<p>In addition to integers and floating-point numbers, OCaml offers the
usual basic data types:
</p><ul class="itemize"><li class="li-itemize">booleans


<div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> (1 &lt; 2) = <span class="ocamlkeyword">false</span>;;</div>



<div class="pre caml-output ok">- : bool = <span class="ocamlkeyword">false</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> one = <span class="ocamlkeyword">if</span> <span class="ocamlkeyword">true</span> <span class="ocamlkeyword">then</span> 1 <span class="ocamlkeyword">else</span> 2;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> one : int = 1</div></div>

</div>


</li><li class="li-itemize">characters


<div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">  'a';;</div>



<div class="pre caml-output ok">- : char = 'a'</div></div>
<div class="ocaml">



<div class="pre caml-input">  int_of_char '\n';;</div>



<div class="pre caml-output ok">- : int = 10</div></div>

</div>


</li><li class="li-itemize">immutable character strings


<div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlstring">"Hello"</span> ^ <span class="ocamlstring">" "</span> ^ <span class="ocamlstring">"world"</span>;;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"Hello world"</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlstring">{|This is a quoted string, here, neither \ nor " are special characters|}</span>;;</div>



<div class="pre caml-output ok">- : string =
<span class="ocamlstring">"This is a quoted string, here, neither \\ nor \" are special characters"</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlstring">{|"\\"|}</span>=<span class="ocamlstring">"\"\\\\\""</span>;;</div>



<div class="pre caml-output ok">- : bool = <span class="ocamlkeyword">true</span></div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlstring">{delimiter|the end of this|}quoted string is here|delimiter}</span>
 =           <span class="ocamlstring">"the end of this|}quoted string is here"</span>;;</div>



<div class="pre caml-output ok">- : bool = <span class="ocamlkeyword">true</span></div></div>

</div>


</li></ul><p>Predefined data structures include tuples, arrays, and lists. There are also
general mechanisms for defining your own data structures, such as records and
variants, which will be covered in more detail later; for now, we concentrate
on lists. Lists are either given in extension as a bracketed list of
semicolon-separated elements, or built from the empty list <span class="c003">[]</span>
(pronounce “nil”) by adding elements in front using the <span class="c003">::</span>
(“cons”) operator.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> l = [<span class="ocamlstring">"is"</span>; <span class="ocamlstring">"a"</span>; <span class="ocamlstring">"tale"</span>; <span class="ocamlstring">"told"</span>; <span class="ocamlstring">"etc."</span>];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : string list = [<span class="ocamlstring">"is"</span>; <span class="ocamlstring">"a"</span>; <span class="ocamlstring">"tale"</span>; <span class="ocamlstring">"told"</span>; <span class="ocamlstring">"etc."</span>]</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlstring">"Life"</span> :: l;;</div>



<div class="pre caml-output ok">- : string list = [<span class="ocamlstring">"Life"</span>; <span class="ocamlstring">"is"</span>; <span class="ocamlstring">"a"</span>; <span class="ocamlstring">"tale"</span>; <span class="ocamlstring">"told"</span>; <span class="ocamlstring">"etc."</span>]</div></div>

</div><p>


As with all other OCaml data structures, lists do not need to be
explicitly allocated and deallocated from memory: all memory
management is entirely automatic in OCaml. Similarly, there is no
explicit handling of pointers: the OCaml compiler silently introduces
pointers where necessary.</p><p>As with most OCaml data structures, inspecting and destructuring lists
is performed by pattern-matching. List patterns have exactly the same
form as list expressions, with identifiers representing unspecified
parts of the list. As an example, here is insertion sort on a list:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> sort lst =
   <span class="ocamlkeyword">match</span> lst <span class="ocamlkeyword">with</span>
     [] -&gt; []
   | head :: tail -&gt; insert head (sort tail)
 <span class="ocamlkeyword">and</span> insert elt lst =
   <span class="ocamlkeyword">match</span> lst <span class="ocamlkeyword">with</span>
     [] -&gt; [elt]
   | head :: tail -&gt; <span class="ocamlkeyword">if</span> elt &lt;= head <span class="ocamlkeyword">then</span> elt :: lst <span class="ocamlkeyword">else</span> head :: insert elt tail
 ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sort : 'a list -&gt; 'a list = &lt;<span class="ocamlkeyword">fun</span>&gt;
<span class="ocamlkeyword">val</span> insert : 'a -&gt; 'a list -&gt; 'a list = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> sort l;;</div>



<div class="pre caml-output ok">- : string list = [<span class="ocamlstring">"a"</span>; <span class="ocamlstring">"etc."</span>; <span class="ocamlstring">"is"</span>; <span class="ocamlstring">"tale"</span>; <span class="ocamlstring">"told"</span>]</div></div>

</div><p>The type inferred for <span class="c003">sort</span>, <span class="c003">'a list -&gt; 'a list</span>, means that <span class="c003">sort</span>
can actually apply to lists of any type, and returns a list of the
same type. The type <span class="c003">'a</span> is a <em>type variable</em>, and stands for any
given type. The reason why <span class="c003">sort</span> can apply to lists of any type is
that the comparisons (<span class="c003">=</span>, <span class="c003">&lt;=</span>, etc.) are <em>polymorphic</em> in OCaml:
they operate between any two values of the same type. This makes
<span class="c003">sort</span> itself polymorphic over all list types.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> sort [6;2;5;3];;</div>



<div class="pre caml-output ok">- : int list = [2; 3; 5; 6]</div></div>
<div class="ocaml">



<div class="pre caml-input"> sort [3.14; 2.718];;</div>



<div class="pre caml-output ok">- : float list = [2.718; 3.14]</div></div>

</div><p>The <span class="c003">sort</span> function above does not modify its input list: it builds
and returns a new list containing the same elements as the input list,
in ascending order. There is actually no way in OCaml to modify
a list in-place once it is built: we say that lists are <em>immutable</em>
data structures. Most OCaml data structures are immutable, but a few
(most notably arrays) are <em>mutable</em>, meaning that they can be
modified in-place at any time.</p><p>The OCaml notation for the type of a function with multiple arguments is <br>
<span class="c003">arg1_type -&gt; arg2_type -&gt; ... -&gt; return_type</span>. For example,
the type inferred for <span class="c003">insert</span>, <span class="c003">'a -&gt; 'a list -&gt; 'a list</span>, means that <span class="c003">insert</span>
takes two arguments, an element of any type <span class="c003">'a</span> and a list with elements of
the same type <span class="c003">'a</span> and returns a list of the same type.
</p>
<h2 class="section" id="s:functions-as-values"><a class="section-anchor" href="#s:functions-as-values" aria-hidden="true">﻿</a>3&nbsp;&nbsp;Functions as values</h2>
<p>OCaml is a functional language: functions in the full mathematical
sense are supported and can be passed around freely just as any other
piece of data. For instance, here is a <span class="c003">deriv</span> function that takes any
float function as argument and returns an approximation of its
derivative function:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> deriv f dx = <span class="ocamlkeyword">function</span> x -&gt; (f (x +. dx) -. f x) /. dx;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> deriv : (float -&gt; float) -&gt; float -&gt; float -&gt; float = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sin' = deriv sin 1e-6;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sin' : float -&gt; float = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> sin' pi;;</div>



<div class="pre caml-output ok">- : float = -1.00000000013961143</div></div>

</div><p>


Even function composition is definable:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> compose f g = <span class="ocamlkeyword">function</span> x -&gt; f (g x);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> compose : ('a -&gt; 'b) -&gt; ('c -&gt; 'a) -&gt; 'c -&gt; 'b = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> cos2 = compose square cos;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> cos2 : float -&gt; float = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Functions that take other functions as arguments are called
“functionals”, or “higher-order functions”. Functionals are
especially useful to provide iterators or similar generic operations
over a data structure. For instance, the standard OCaml library
provides a <span class="c003">List.map</span> functional that applies a given function to each
element of a list, and returns the list of the results:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> List.map (<span class="ocamlkeyword">function</span> n -&gt; n * 2 + 1) [0;1;2;3;4];;</div>



<div class="pre caml-output ok">- : int list = [1; 3; 5; 7; 9]</div></div>

</div><p>


This functional, along with a number of other list and array
functionals, is predefined because it is often useful, but there is
nothing magic with it: it can easily be defined as follows.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> map f l =
   <span class="ocamlkeyword">match</span> l <span class="ocamlkeyword">with</span>
     [] -&gt; []
   | hd :: tl -&gt; f hd :: map f tl;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> map : ('a -&gt; 'b) -&gt; 'a list -&gt; 'b list = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div>
<h2 class="section" id="s:tut-recvariants"><a class="section-anchor" href="#s:tut-recvariants" aria-hidden="true">﻿</a>4&nbsp;&nbsp;Records and variants</h2>
<p>User-defined data structures include records and variants. Both are
defined with the <span class="c003">type</span> declaration. Here, we declare a record type to
represent rational numbers.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> ratio = {num: int; denom: int};;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> ratio = { num : int; denom : int; }</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> add_ratio r1 r2 =
   {num = r1.num * r2.denom + r2.num * r1.denom;
    denom = r1.denom * r2.denom};;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> add_ratio : ratio -&gt; ratio -&gt; ratio = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> add_ratio {num=1; denom=3} {num=2; denom=5};;</div>



<div class="pre caml-output ok">- : ratio = {num = 11; denom = 15}</div></div>

</div><p>


Record fields can also be accessed through pattern-matching:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> integer_part r =
   <span class="ocamlkeyword">match</span> r <span class="ocamlkeyword">with</span>
     {num=num; denom=denom} -&gt; num / denom;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> integer_part : ratio -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Since there is only one case in this pattern matching, it
is safe to expand directly the argument <span class="c003">r</span> in a record pattern:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> integer_part {num=num; denom=denom} = num / denom;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> integer_part : ratio -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Unneeded fields can be omitted:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> get_denom {denom=denom} = denom;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> get_denom : ratio -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Optionally, missing fields can be made explicit by ending the list of
fields with a trailing wildcard <span class="c003">_</span>::


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> get_num {num=num; _ } = num;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> get_num : ratio -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


When both sides of the <span class="c003">=</span> sign are the same, it is possible to avoid
repeating the field name by eliding the <span class="c003">=field</span> part:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> integer_part {num; denom} = num / denom;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> integer_part : ratio -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


This short notation for fields also works when constructing records:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> ratio num denom = {num; denom};;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> ratio : int -&gt; int -&gt; ratio = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


At last, it is possible to update few fields of a record at once:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> integer_product integer ratio = { ratio <span class="ocamlkeyword">with</span> num = integer * ratio.num };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> integer_product : int -&gt; ratio -&gt; ratio = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


With this functional update notation, the record on the left-hand side
of <span class="c003">with</span> is copied except for the fields on the right-hand side which
are updated.</p><p>The declaration of a variant type lists all possible forms for values
of that type. Each case is identified by a name, called a constructor,
which serves both for constructing values of the variant type and
inspecting them by pattern-matching. Constructor names are capitalized
to distinguish them from variable names (which must start with a
lowercase letter). For instance, here is a variant
type for doing mixed arithmetic (integers and floats):


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> number = Int <span class="ocamlkeyword">of</span> int | Float <span class="ocamlkeyword">of</span> float | Error;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> number = Int <span class="ocamlkeyword">of</span> int | Float <span class="ocamlkeyword">of</span> float | Error</div></div>

</div><p>


This declaration expresses that a value of type <span class="c003">number</span> is either an
integer, a floating-point number, or the constant <span class="c003">Error</span> representing
the result of an invalid operation (e.g. a division by zero).</p><p>Enumerated types are a special case of variant types, where all
alternatives are constants:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> sign = Positive | Negative;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> sign = Positive | Negative</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sign_int n = <span class="ocamlkeyword">if</span> n &gt;= 0 <span class="ocamlkeyword">then</span> Positive <span class="ocamlkeyword">else</span> Negative;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sign_int : int -&gt; sign = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>To define arithmetic operations for the <span class="c003">number</span> type, we use
pattern-matching on the two numbers involved:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> add_num n1 n2 =
   <span class="ocamlkeyword">match</span> (n1, n2) <span class="ocamlkeyword">with</span>
     (Int i1, Int i2) -&gt;
       <span class="ocamlcomment">(* Check for overflow of integer addition *)</span>
       <span class="ocamlkeyword">if</span> sign_int i1 = sign_int i2 &amp;&amp; sign_int (i1 + i2) &lt;&gt; sign_int i1
       <span class="ocamlkeyword">then</span> Float(float i1 +. float i2)
       <span class="ocamlkeyword">else</span> Int(i1 + i2)
   | (Int i1, Float f2) -&gt; Float(float i1 +. f2)
   | (Float f1, Int i2) -&gt; Float(f1 +. float i2)
   | (Float f1, Float f2) -&gt; Float(f1 +. f2)
   | (Error, _) -&gt; Error
   | (_, Error) -&gt; Error;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> add_num : number -&gt; number -&gt; number = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> add_num (Int 123) (Float 3.14159);;</div>



<div class="pre caml-output ok">- : number = Float 126.14159</div></div>

</div><p>Another interesting example of variant type is the built-in
<span class="c003">'a option</span> type which represents either a value of type <span class="c003">'a</span> or an
absence of value:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> 'a option = Some <span class="ocamlkeyword">of</span> 'a | None;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a option = Some <span class="ocamlkeyword">of</span> 'a | None</div></div>

</div><p>


This type is particularly useful when defining function that can
fail in common situations, for instance


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> safe_square_root x = <span class="ocamlkeyword">if</span> x &gt; 0. <span class="ocamlkeyword">then</span> Some(sqrt x) <span class="ocamlkeyword">else</span> None;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> safe_square_root : float -&gt; float option = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>The most common usage of variant types is to describe recursive data
structures. Consider for example the type of binary trees:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> 'a btree = Empty | Node <span class="ocamlkeyword">of</span> 'a * 'a btree * 'a btree;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a btree = Empty | Node <span class="ocamlkeyword">of</span> 'a * 'a btree * 'a btree</div></div>

</div><p>


This definition reads as follows: a binary tree containing values of
type <span class="c003">'a</span> (an arbitrary type) is either empty, or is a node containing
one value of type <span class="c003">'a</span> and two subtrees also containing values of type
<span class="c003">'a</span>, that is, two <span class="c003">'a btree</span>.</p><p>Operations on binary trees are naturally expressed as recursive functions
following the same structure as the type definition itself. For
instance, here are functions performing lookup and insertion in
ordered binary trees (elements increase from left to right):


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> member x btree =
   <span class="ocamlkeyword">match</span> btree <span class="ocamlkeyword">with</span>
     Empty -&gt; <span class="ocamlkeyword">false</span>
   | Node(y, left, right) -&gt;
       <span class="ocamlkeyword">if</span> x = y <span class="ocamlkeyword">then</span> <span class="ocamlkeyword">true</span> <span class="ocamlkeyword">else</span>
       <span class="ocamlkeyword">if</span> x &lt; y <span class="ocamlkeyword">then</span> member x left <span class="ocamlkeyword">else</span> member x right;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> member : 'a -&gt; 'a btree -&gt; bool = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> insert x btree =
   <span class="ocamlkeyword">match</span> btree <span class="ocamlkeyword">with</span>
     Empty -&gt; Node(x, Empty, Empty)
   | Node(y, left, right) -&gt;
       <span class="ocamlkeyword">if</span> x &lt;= y <span class="ocamlkeyword">then</span> Node(y, insert x left, right)
                 <span class="ocamlkeyword">else</span> Node(y, left, insert x right);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> insert : 'a -&gt; 'a btree -&gt; 'a btree = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div>
<h3 class="subsection" id="ss:record-and-variant-disambiguation"><a class="section-anchor" href="#ss:record-and-variant-disambiguation" aria-hidden="true">﻿</a>4.1&nbsp;&nbsp;Record and variant disambiguation</h3>
<p>
( This subsection can be skipped on the first reading )</p><p>Astute readers may have wondered what happens when two or more record
fields or constructors share the same name</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> first_record  = { x:int; y:int; z:int }
 <span class="ocamlkeyword">type</span> middle_record = { x:int; z:int }
 <span class="ocamlkeyword">type</span> last_record   = { x:int };;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> first_variant = A | B | C
 <span class="ocamlkeyword">type</span> last_variant  = A;;</div></div>

</div><p>The answer is that when confronted with multiple options, OCaml tries to
use locally available information to disambiguate between the various fields
and constructors. First, if the type of the record or variant is known,
OCaml can pick unambiguously the corresponding field or constructor.
For instance:</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> look_at_x_then_z (r:first_record) =
   <span class="ocamlkeyword">let</span> x = r.x <span class="ocamlkeyword">in</span>
   x + r.z;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> look_at_x_then_z : first_record -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> permute (x:first_variant) = <span class="ocamlkeyword">match</span> x <span class="ocamlkeyword">with</span>
   | A -&gt; (B:first_variant)
   | B -&gt; A
   | C -&gt; C;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> permute : first_variant -&gt; first_variant = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> wrapped = First <span class="ocamlkeyword">of</span> first_record
 <span class="ocamlkeyword">let</span> f (First r) = r, r.x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> wrapped = First <span class="ocamlkeyword">of</span> first_record
<span class="ocamlkeyword">val</span> f : wrapped -&gt; first_record * int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>In the first example, <span class="c003">(r:first_record)</span> is an explicit annotation
telling OCaml that the type of <span class="c003">r</span> is <span class="c003">first_record</span>. With this
annotation, Ocaml knows that <span class="c003">r.x</span> refers to the <span class="c003">x</span> field of the first
record type. Similarly, the type annotation in the second example makes
it clear to OCaml that the constructors <span class="c003">A</span>, <span class="c003">B</span> and <span class="c003">C</span> come from the
first variant type. Contrarily, in the last example, OCaml has inferred
by itself that the type of <span class="c003">r</span> can only be <span class="c003">first_record</span> and there are
no needs for explicit type annotations.</p><p>Those explicit type annotations can in fact be used anywhere.
Most of the time they are unnecessary, but they are useful to guide
disambiguation, to debug unexpected type errors, or combined with some
of the more advanced features of OCaml described in later chapters.</p><p>Secondly, for records, OCaml can also deduce the right record type by
looking at the whole set of fields used in a expression or pattern:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> project_and_rotate {x;y; _ } = { x= - y; y = x ; z = 0} ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> project_and_rotate : first_record -&gt; first_record = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Since the fields <span class="c003">x</span> and <span class="c003">y</span> can only appear simultaneously in the first
record type, OCaml infers that the type of <span class="c003">project_and_rotate</span> is
<span class="c003">first_record -&gt; first_record</span>.</p><p>In last resort, if there is not enough information to disambiguate between
different fields or constructors, Ocaml picks the last defined type
amongst all locally valid choices:</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> look_at_xz {x;z} = x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> look_at_xz : middle_record -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Here, OCaml has inferred that the possible choices for the type of
<span class="c003">{x;z}</span> are <span class="c003">first_record</span> and <span class="c003">middle_record</span>, since the type
<span class="c003">last_record</span> has no field <span class="c003">z</span>. Ocaml then picks the type <span class="c003">middle_record</span>
as the last defined type between the two possibilities.</p><p>Beware that this last resort disambiguation is local: once Ocaml has
chosen a disambiguation, it sticks to this choice, even if it leads to
an ulterior type error:</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> look_at_x_then_y r =
   <span class="ocamlkeyword">let</span> x = r.x <span class="ocamlkeyword">in</span> <span class="ocamlcomment">(* Ocaml deduces [r: last_record] *)</span>
   x + r.<span class="ocamlhighlight">y</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type last_record
       The field y does not belong to type last_record</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> is_a_or_b x = <span class="ocamlkeyword">match</span> x <span class="ocamlkeyword">with</span>
   | A -&gt; <span class="ocamlkeyword">true</span> <span class="ocamlcomment">(* OCaml infers [x: last_variant] *)</span>
   | <span class="ocamlhighlight">B</span> -&gt; <span class="ocamlkeyword">true</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This variant pattern is expected to have type last_variant
       The constructor B does not belong to type last_variant</div></div>

</div><p>Moreover, being the last defined type is a quite unstable position that
may change surreptitiously after adding or moving around a type
definition, or after opening a module (see chapter <a href="moduleexamples.html#c%3Amoduleexamples">2</a>).
Consequently, adding explicit type annotations to guide disambiguation is
more robust than relying on the last defined type disambiguation.</p>
<h2 class="section" id="s:imperative-features"><a class="section-anchor" href="#s:imperative-features" aria-hidden="true">﻿</a>5&nbsp;&nbsp;Imperative features</h2>
<p>Though all examples so far were written in purely applicative style,
OCaml is also equipped with full imperative features. This includes the
usual <span class="c003">while</span> and <span class="c003">for</span> loops, as well as mutable data structures such
as arrays. Arrays are either created by listing semicolon-separated element
values between <span class="c003">[|</span> and <span class="c003">|]</span> brackets, or allocated and initialized with the
<span class="c003">Array.make</span> function, then filled up later by assignments. For instance, the
function below sums two vectors (represented as float arrays) componentwise.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> add_vect v1 v2 =
   <span class="ocamlkeyword">let</span> len = min (Array.length v1) (Array.length v2) <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> res = Array.make len 0.0 <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">for</span> i = 0 <span class="ocamlkeyword">to</span> len - 1 <span class="ocamlkeyword">do</span>
     res.(i) &lt;- v1.(i) +. v2.(i)
   <span class="ocamlkeyword">done</span>;
   res;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> add_vect : float array -&gt; float array -&gt; float array = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> add_vect [| 1.0; 2.0 |] [| 3.0; 4.0 |];;</div>



<div class="pre caml-output ok">- : float array = [|4.; 6.|]</div></div>

</div><p>Record fields can also be modified by assignment, provided they are
declared <span class="c003">mutable</span> in the definition of the record type:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> mutable_point = { <span class="ocamlkeyword">mutable</span> x: float; <span class="ocamlkeyword">mutable</span> y: float };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> mutable_point = { <span class="ocamlkeyword">mutable</span> x : float; <span class="ocamlkeyword">mutable</span> y : float; }</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> translate p dx dy =
   p.x &lt;- p.x +. dx; p.y &lt;- p.y +. dy;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> translate : mutable_point -&gt; float -&gt; float -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> mypoint = { x = 0.0; y = 0.0 };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> mypoint : mutable_point = {x = 0.; y = 0.}</div></div>
<div class="ocaml">



<div class="pre caml-input"> translate mypoint 1.0 2.0;;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> mypoint;;</div>



<div class="pre caml-output ok">- : mutable_point = {x = 1.; y = 2.}</div></div>

</div><p>OCaml has no built-in notion of variable – identifiers whose current
value can be changed by assignment. (The <span class="c003">let</span> binding is not an
assignment, it introduces a new identifier with a new scope.)
However, the standard library provides references, which are mutable
indirection cells, with operators <span class="c003">!</span> to fetch
the current contents of the reference and <span class="c003">:=</span> to assign the contents.
Variables can then be emulated by <span class="c003">let</span>-binding a reference. For
instance, here is an in-place insertion sort over arrays:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> insertion_sort a =
   <span class="ocamlkeyword">for</span> i = 1 <span class="ocamlkeyword">to</span> Array.length a - 1 <span class="ocamlkeyword">do</span>
     <span class="ocamlkeyword">let</span> val_i = a.(i) <span class="ocamlkeyword">in</span>
     <span class="ocamlkeyword">let</span> j = <span class="ocamlkeyword">ref</span> i <span class="ocamlkeyword">in</span>
     <span class="ocamlkeyword">while</span> !j &gt; 0 &amp;&amp; val_i &lt; a.(!j - 1) <span class="ocamlkeyword">do</span>
       a.(!j) &lt;- a.(!j - 1);
       j := !j - 1
     <span class="ocamlkeyword">done</span>;
     a.(!j) &lt;- val_i
   <span class="ocamlkeyword">done</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> insertion_sort : 'a array -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>References are also useful to write functions that maintain a current
state between two calls to the function. For instance, the following
pseudo-random number generator keeps the last returned number in a
reference:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> current_rand = <span class="ocamlkeyword">ref</span> 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> current_rand : int <span class="ocamlkeyword">ref</span> = {contents = 0}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> random () =
   current_rand := !current_rand * 25713 + 1345;
   !current_rand;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> random : unit -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Again, there is nothing magical with references: they are implemented as
a single-field mutable record, as follows.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> 'a <span class="ocamlkeyword">ref</span> = { <span class="ocamlkeyword">mutable</span> contents: 'a };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a <span class="ocamlkeyword">ref</span> = { <span class="ocamlkeyword">mutable</span> contents : 'a; }</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> ( ! ) r = r.contents;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> ( ! ) : 'a <span class="ocamlkeyword">ref</span> -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> ( := ) r newval = r.contents &lt;- newval;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> ( := ) : 'a <span class="ocamlkeyword">ref</span> -&gt; 'a -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>In some special cases, you may need to store a polymorphic function in
a data structure, keeping its polymorphism. Doing this requires
user-provided type annotations, since polymorphism is only introduced
automatically for global definitions. However, you can explicitly give
polymorphic types to record fields.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> idref = { <span class="ocamlkeyword">mutable</span> id: 'a. 'a -&gt; 'a };;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> idref = { <span class="ocamlkeyword">mutable</span> id : 'a. 'a -&gt; 'a; }</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> r = {id = <span class="ocamlkeyword">fun</span> x -&gt; x};;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> r : idref = {id = &lt;<span class="ocamlkeyword">fun</span>&gt;}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> g s = (s.id 1, s.id <span class="ocamlkeyword">true</span>);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> g : idref -&gt; int * bool = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> r.id &lt;- (<span class="ocamlkeyword">fun</span> x -&gt; print_string <span class="ocamlstring">"called id\n"</span>; x);;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> g r;;</div>



<div class="pre caml-output ok">called id
called id
- : int * bool = (1, <span class="ocamlkeyword">true</span>)</div></div>

</div>
<h2 class="section" id="s:exceptions"><a class="section-anchor" href="#s:exceptions" aria-hidden="true">﻿</a>6&nbsp;&nbsp;Exceptions</h2>
<p>OCaml provides exceptions for signalling and handling exceptional
conditions. Exceptions can also be used as a general-purpose non-local
control structure, although this should not be overused since it can
make the code harder to understand. Exceptions are declared with the
<span class="c003">exception</span> construct, and signalled with the <span class="c003">raise</span> operator. For instance,
the function below for taking the head of a list uses an exception to
signal the case where an empty list is given.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">exception</span> Empty_list;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">exception</span> Empty_list</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> head l =
   <span class="ocamlkeyword">match</span> l <span class="ocamlkeyword">with</span>
     [] -&gt; raise Empty_list
   | hd :: tl -&gt; hd;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> head : 'a list -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> head [1;2];;</div>



<div class="pre caml-output ok">- : int = 1</div></div>
<div class="ocaml">



<div class="pre caml-input"> head [];;</div>



<div class="pre caml-output ok">Exception: Empty_list.</div></div>

</div><p>Exceptions are used throughout the standard library to signal cases
where the library functions cannot complete normally. For instance,
the <span class="c003">List.assoc</span> function, which returns the data associated with a
given key in a list of (key, data) pairs, raises the predefined
exception <span class="c003">Not_found</span> when the key does not appear in the list:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> List.assoc 1 [(0, <span class="ocamlstring">"zero"</span>); (1, <span class="ocamlstring">"one"</span>)];;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"one"</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> List.assoc 2 [(0, <span class="ocamlstring">"zero"</span>); (1, <span class="ocamlstring">"one"</span>)];;</div>



<div class="pre caml-output ok">Exception: Not_found.</div></div>

</div><p>Exceptions can be trapped with the <span class="c003">try</span>…<span class="c003">with</span> construct:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> name_of_binary_digit digit =
   <span class="ocamlkeyword">try</span>
     List.assoc digit [0, <span class="ocamlstring">"zero"</span>; 1, <span class="ocamlstring">"one"</span>]
   <span class="ocamlkeyword">with</span> Not_found -&gt;
     <span class="ocamlstring">"not a binary digit"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> name_of_binary_digit : int -&gt; string = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> name_of_binary_digit 0;;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"zero"</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> name_of_binary_digit (-1);;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"not a binary digit"</span></div></div>

</div><p>The <span class="c003">with</span> part does pattern matching on the
exception value with the same syntax and behavior as <span class="c003">match</span>. Thus,
several exceptions can be caught by one
<span class="c003">try</span>…<span class="c003">with</span> construct:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> first_named_value values names =
   <span class="ocamlkeyword">try</span>
     List.assoc (head values) names
   <span class="ocamlkeyword">with</span>
   | Empty_list -&gt; <span class="ocamlstring">"no named value"</span>
   | Not_found -&gt; first_named_value (List.tl values) names;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> first_named_value : 'a list -&gt; ('a * string) list -&gt; string = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> first_named_value [ 0; 10 ] [ 1, <span class="ocamlstring">"one"</span>; 10, <span class="ocamlstring">"ten"</span>];;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"ten"</span></div></div>

</div><p>Also, finalization can be performed by
trapping all exceptions, performing the finalization, then re-raising
the exception:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> temporarily_set_reference <span class="ocamlkeyword">ref</span> newval funct =
   <span class="ocamlkeyword">let</span> oldval = !<span class="ocamlkeyword">ref</span> <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">try</span>
     <span class="ocamlkeyword">ref</span> := newval;
     <span class="ocamlkeyword">let</span> res = funct () <span class="ocamlkeyword">in</span>
     <span class="ocamlkeyword">ref</span> := oldval;
     res
   <span class="ocamlkeyword">with</span> x -&gt;
     <span class="ocamlkeyword">ref</span> := oldval;
     raise x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> temporarily_set_reference : 'a <span class="ocamlkeyword">ref</span> -&gt; 'a -&gt; (unit -&gt; 'b) -&gt; 'b = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>An alternative to <span class="c003">try</span>…<span class="c003">with</span> is to catch the exception while
pattern matching:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> assoc_may_map f x l =
   <span class="ocamlkeyword">match</span> List.assoc x l <span class="ocamlkeyword">with</span>
   | <span class="ocamlkeyword">exception</span> Not_found -&gt; None
   | y -&gt; f y;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> assoc_may_map : ('a -&gt; 'b option) -&gt; 'c -&gt; ('c * 'a) list -&gt; 'b option =
  &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Note that this construction is only useful if the exception is raised
between <span class="c003">match</span>…<span class="c003">with</span>. Exception patterns can be combined
with ordinary patterns at the toplevel,


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> flat_assoc_opt x l =
   <span class="ocamlkeyword">match</span> List.assoc x l <span class="ocamlkeyword">with</span>
   | None | <span class="ocamlkeyword">exception</span> Not_found -&gt; None
   | Some _ <span class="ocamlkeyword">as</span> v -&gt; v;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> flat_assoc_opt : 'a -&gt; ('a * 'b option) list -&gt; 'b option = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


but they cannot be nested inside other patterns. For instance,
the pattern <span class="c003">Some (exception A)</span> is invalid.</p><p>When exceptions are used as a control structure, it can be useful to make
them as local as possible by using a locally defined exception.
For instance, with


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> fixpoint f x =
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">exception</span> Done <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> x = <span class="ocamlkeyword">ref</span> x <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">try</span> <span class="ocamlkeyword">while</span> <span class="ocamlkeyword">true</span> <span class="ocamlkeyword">do</span>
       <span class="ocamlkeyword">let</span> y = f !x <span class="ocamlkeyword">in</span>
       <span class="ocamlkeyword">if</span> !x = y <span class="ocamlkeyword">then</span> raise Done <span class="ocamlkeyword">else</span> x := y
     <span class="ocamlkeyword">done</span>; <span class="ocamlkeyword">assert</span> <span class="ocamlkeyword">false</span>
   <span class="ocamlkeyword">with</span> Done -&gt; !x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> fixpoint : ('a -&gt; 'a) -&gt; 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


the function <span class="c003">f</span> cannot raise a <span class="c003">Done</span> exception, which removes an
entire class of misbehaving functions.</p>
<h2 class="section" id="s:lazy-expr"><a class="section-anchor" href="#s:lazy-expr" aria-hidden="true">﻿</a>7&nbsp;&nbsp;Lazy expressions</h2>
<p>OCaml allows us to defer some computation until later when we need the result of
that computation. </p><p>We use <span class="c003">lazy (expr)</span> to delay the evaluation of some expression <span class="c003">expr</span>. For 
example, we can defer the computation of <span class="c003">1+1</span> until we need the result of that
expression, <span class="c003">2</span>. Let us see how we initialize a lazy expression. </p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> lazy_two = <span class="ocamlkeyword">lazy</span> ( print_endline <span class="ocamlstring">"lazy_two evaluation"</span>; 1 + 1 );;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> lazy_two : int lazy_t = &lt;<span class="ocamlkeyword">lazy</span>&gt;</div></div>

</div><p>We added <span class="c003">print_endline "lazy_two evaluation"</span> to see when the lazy
expression is being evaluated.</p><p>The value of <span class="c003">lazy_two</span> is displayed as <span class="c003">&lt;lazy&gt;</span>, which means the expression 
has not been evaluated yet, and its final value is unknown.</p><p>Note that <span class="c003">lazy_two</span> has type <span class="c003">int lazy_t</span>. However, the type <span class="c003">'a lazy_t</span> is an 
internal type name, so the type <span class="c003">'a Lazy.t</span> should be preferred when possible.</p><p>When we finally need the result of a lazy expression, we can call <span class="c003">Lazy.force</span> 
on that expression to force its evaluation. The function <span class="c003">force</span> comes from 
standard-library module <a href="../../api/4.10/Lazy.html"><span class="c003">Lazy</span></a>.</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   Lazy.force lazy_two;;</div>



<div class="pre caml-output ok">lazy_two evaluation
- : int = 2</div></div>

</div><p>Notice that our function call above prints “lazy_two evaluation” and then 
returns the plain value of the computation. </p><p>Now if we look at the value of <span class="c003">lazy_two</span>, we see that it is not displayed as 
<span class="c003">&lt;lazy&gt;</span> anymore but as <span class="c003">lazy 2</span>.</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   lazy_two;;</div>



<div class="pre caml-output ok">- : int lazy_t = <span class="ocamlkeyword">lazy</span> 2</div></div>

</div><p>This is because <span class="c003">Lazy.force</span> memoizes the result of the forced expression. In other 
words, every subsequent call of <span class="c003">Lazy.force</span> on that expression returns the 
result of the first computation without recomputing the lazy expression. Let us 
force <span class="c003">lazy_two</span> once again. </p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   Lazy.force lazy_two;;</div>



<div class="pre caml-output ok">- : int = 2</div></div>

</div><p>The expression is not evaluated this time; notice that “lazy_two evaluation” is
not printed. The result of the initial computation is simply returned. </p><p>Lazy patterns provide another way to force a lazy expression. </p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> lazy_l = <span class="ocamlkeyword">lazy</span> ([1; 2] @ [3; 4]);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> lazy_l : int list lazy_t = &lt;<span class="ocamlkeyword">lazy</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">lazy</span> l = lazy_l;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : int list = [1; 2; 3; 4]</div></div>

</div><p>We can also use lazy patterns in pattern matching.</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">let</span> maybe_eval lazy_guard lazy_expr =
     <span class="ocamlkeyword">match</span> lazy_guard, lazy_expr <span class="ocamlkeyword">with</span>
     | <span class="ocamlkeyword">lazy</span> <span class="ocamlkeyword">false</span>, _ -&gt; <span class="ocamlstring">"matches if (Lazy.force lazy_guard = false); lazy_expr not forced"</span>
     | <span class="ocamlkeyword">lazy</span> <span class="ocamlkeyword">true</span>, <span class="ocamlkeyword">lazy</span> _ -&gt; <span class="ocamlstring">"matches if (Lazy.force lazy_guard = true); lazy_expr forced"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> maybe_eval : bool lazy_t -&gt; 'a lazy_t -&gt; string = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>The lazy expression <span class="c003">lazy_expr</span> is forced only if the <span class="c003">lazy_guard</span> value yields 
<span class="c003">true</span> once computed. Indeed, a simple wildcard pattern (not lazy) never forces 
the lazy expression’s evaluation. However, a pattern with keyword <span class="c003">lazy</span>, even 
if it is wildcard, always forces the evaluation of the deferred computation.</p>
<h2 class="section" id="s:symb-expr"><a class="section-anchor" href="#s:symb-expr" aria-hidden="true">﻿</a>8&nbsp;&nbsp;Symbolic processing of expressions</h2>
<p>We finish this introduction with a more complete example
representative of the use of OCaml for symbolic processing: formal
manipulations of arithmetic expressions containing variables. The
following variant type describes the expressions we shall manipulate:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> expression =
     Const <span class="ocamlkeyword">of</span> float
   | Var <span class="ocamlkeyword">of</span> string
   | Sum <span class="ocamlkeyword">of</span> expression * expression    <span class="ocamlcomment">(* e1 + e2 *)</span>
   | Diff <span class="ocamlkeyword">of</span> expression * expression   <span class="ocamlcomment">(* e1 - e2 *)</span>
   | Prod <span class="ocamlkeyword">of</span> expression * expression   <span class="ocamlcomment">(* e1 * e2 *)</span>
   | Quot <span class="ocamlkeyword">of</span> expression * expression   <span class="ocamlcomment">(* e1 / e2 *)</span>
 ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> expression =
    Const <span class="ocamlkeyword">of</span> float
  | Var <span class="ocamlkeyword">of</span> string
  | Sum <span class="ocamlkeyword">of</span> expression * expression
  | Diff <span class="ocamlkeyword">of</span> expression * expression
  | Prod <span class="ocamlkeyword">of</span> expression * expression
  | Quot <span class="ocamlkeyword">of</span> expression * expression</div></div>

</div><p>We first define a function to evaluate an expression given an
environment that maps variable names to their values. For simplicity,
the environment is represented as an association list.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">exception</span> Unbound_variable <span class="ocamlkeyword">of</span> string;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">exception</span> Unbound_variable <span class="ocamlkeyword">of</span> string</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> eval env exp =
   <span class="ocamlkeyword">match</span> exp <span class="ocamlkeyword">with</span>
     Const c -&gt; c
   | Var v -&gt;
       (<span class="ocamlkeyword">try</span> List.assoc v env <span class="ocamlkeyword">with</span> Not_found -&gt; raise (Unbound_variable v))
   | Sum(f, g) -&gt; eval env f +. eval env g
   | Diff(f, g) -&gt; eval env f -. eval env g
   | Prod(f, g) -&gt; eval env f *. eval env g
   | Quot(f, g) -&gt; eval env f /. eval env g;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> eval : (string * float) list -&gt; expression -&gt; float = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> eval [(<span class="ocamlstring">"x"</span>, 1.0); (<span class="ocamlstring">"y"</span>, 3.14)] (Prod(Sum(Var <span class="ocamlstring">"x"</span>, Const 2.0), Var <span class="ocamlstring">"y"</span>));;</div>



<div class="pre caml-output ok">- : float = 9.42</div></div>

</div><p>Now for a real symbolic processing, we define the derivative of an
expression with respect to a variable <span class="c003">dv</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> deriv exp dv =
   <span class="ocamlkeyword">match</span> exp <span class="ocamlkeyword">with</span>
     Const c -&gt; Const 0.0
   | Var v -&gt; <span class="ocamlkeyword">if</span> v = dv <span class="ocamlkeyword">then</span> Const 1.0 <span class="ocamlkeyword">else</span> Const 0.0
   | Sum(f, g) -&gt; Sum(deriv f dv, deriv g dv)
   | Diff(f, g) -&gt; Diff(deriv f dv, deriv g dv)
   | Prod(f, g) -&gt; Sum(Prod(f, deriv g dv), Prod(deriv f dv, g))
   | Quot(f, g) -&gt; Quot(Diff(Prod(deriv f dv, g), Prod(f, deriv g dv)),
                        Prod(g, g))
 ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> deriv : expression -&gt; string -&gt; expression = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> deriv (Quot(Const 1.0, Var <span class="ocamlstring">"x"</span>)) <span class="ocamlstring">"x"</span>;;</div>



<div class="pre caml-output ok">- : expression =
Quot (Diff (Prod (Const 0., Var <span class="ocamlstring">"x"</span>), Prod (Const 1., Const 1.)),
 Prod (Var <span class="ocamlstring">"x"</span>, Var <span class="ocamlstring">"x"</span>))</div></div>

</div>
<h2 class="section" id="s:pretty-printing"><a class="section-anchor" href="#s:pretty-printing" aria-hidden="true">﻿</a>9&nbsp;&nbsp;Pretty-printing</h2>
<p>As shown in the examples above, the internal representation (also
called <em>abstract syntax</em>) of expressions quickly becomes hard to
read and write as the expressions get larger. We need a printer and a
parser to go back and forth between the abstract syntax and the <em>concrete syntax</em>, which in the case of expressions is the familiar
algebraic notation (e.g. <span class="c003">2*x+1</span>).</p><p>For the printing function, we take into account the usual precedence
rules (i.e. <span class="c003">*</span> binds tighter than <span class="c003">+</span>) to avoid printing unnecessary
parentheses. To this end, we maintain the current operator precedence
and print parentheses around an operator only if its precedence is
less than the current precedence.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> print_expr exp =
   <span class="ocamlcomment">(* Local function definitions *)</span>
   <span class="ocamlkeyword">let</span> open_paren prec op_prec =
     <span class="ocamlkeyword">if</span> prec &gt; op_prec <span class="ocamlkeyword">then</span> print_string <span class="ocamlstring">"("</span> <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> close_paren prec op_prec =
     <span class="ocamlkeyword">if</span> prec &gt; op_prec <span class="ocamlkeyword">then</span> print_string <span class="ocamlstring">")"</span> <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> print prec exp =     <span class="ocamlcomment">(* prec is the current precedence *)</span>
     <span class="ocamlkeyword">match</span> exp <span class="ocamlkeyword">with</span>
       Const c -&gt; print_float c
     | Var v -&gt; print_string v
     | Sum(f, g) -&gt;
         open_paren prec 0;
         print 0 f; print_string <span class="ocamlstring">" + "</span>; print 0 g;
         close_paren prec 0
     | Diff(f, g) -&gt;
         open_paren prec 0;
         print 0 f; print_string <span class="ocamlstring">" - "</span>; print 1 g;
         close_paren prec 0
     | Prod(f, g) -&gt;
         open_paren prec 2;
         print 2 f; print_string <span class="ocamlstring">" * "</span>; print 2 g;
         close_paren prec 2
     | Quot(f, g) -&gt;
         open_paren prec 2;
         print 2 f; print_string <span class="ocamlstring">" / "</span>; print 3 g;
         close_paren prec 2
   <span class="ocamlkeyword">in</span> print 0 exp;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> print_expr : expression -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> e = Sum(Prod(Const 2.0, Var <span class="ocamlstring">"x"</span>), Const 1.0);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> e : expression = Sum (Prod (Const 2., Var <span class="ocamlstring">"x"</span>), Const 1.)</div></div>
<div class="ocaml">



<div class="pre caml-input"> print_expr e; print_newline ();;</div>



<div class="pre caml-output ok">2. * x + 1.
- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> print_expr (deriv e <span class="ocamlstring">"x"</span>); print_newline ();;</div>



<div class="pre caml-output ok">2. * 1. + 0. * x + 0.
- : unit = ()</div></div>

</div>
<h2 class="section" id="s:printf"><a class="section-anchor" href="#s:printf" aria-hidden="true">﻿</a>10&nbsp;&nbsp;Printf formats</h2>
<p>There is a <span class="c003">printf</span> function in the <a href="../../api/4.10/Printf.html"><span class="c003">Printf</span></a> module
(see chapter&nbsp;<a href="moduleexamples.html#c%3Amoduleexamples">2</a>) that allows you to make formatted
output more concisely.
It follows the behavior of the <span class="c003">printf</span> function from the C standard library.
The <span class="c003">printf</span> function takes a format string that describes the desired output
as a text interspered with specifiers (for instance <span class="c003">%d</span>, <span class="c003">%f</span>).
Next, the specifiers are substituted by the following arguments in their order
of apparition in the format string:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> Printf.printf <span class="ocamlstring">"%i + %i is an integer value, %F * %F is a float, %S\n"</span>
 3 2 4.5 1. <span class="ocamlstring">"this is a string"</span>;;</div>



<div class="pre caml-output ok">3 + 2 is an integer value, 4.5 * 1. is a float, <span class="ocamlstring">"this is a string"</span>
- : unit = ()</div></div>

</div><p>


The OCaml type system checks that the type of the arguments and the specifiers are
compatible. If you pass it an argument of a type that does not correspond to
the format specifier, the compiler will display an error message:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> Printf.printf <span class="ocamlstring">"Float value: %F"</span> <span class="ocamlhighlight">42</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type int but an expression was expected of type
         float
  Hint: Did you mean `42.'?</div></div>

</div><p>


The <span class="c003">fprintf</span> function is like <span class="c003">printf</span> except that it takes an output channel as
the first argument. The <span class="c003">%a</span> specifier can be useful to define custom printer
(for custom types). For instance, we can create a printing template that converts
an integer argument to signed decimal:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> pp_int ppf n = Printf.fprintf ppf <span class="ocamlstring">"%d"</span> n;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> pp_int : out_channel -&gt; int -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> Printf.printf <span class="ocamlstring">"Outputting an integer using a custom printer: %a "</span> pp_int 42;;</div>



<div class="pre caml-output ok">Outputting an integer using a custom printer: 42 - : unit = ()</div></div>

</div><p>


The advantage of those printers based on the <span class="c003">%a</span> specifier is that they can be
composed together to create more complex printers step by step.
We can define a combinator that can turn a printer for <span class="c003">'a</span> type into a printer
for <span class="c003">'a optional</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> pp_option printer ppf = <span class="ocamlkeyword">function</span>
   | None -&gt; Printf.fprintf ppf <span class="ocamlstring">"None"</span>
   | Some v -&gt; Printf.fprintf ppf <span class="ocamlstring">"Some(%a)"</span> printer v;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> pp_option :
  (out_channel -&gt; 'a -&gt; unit) -&gt; out_channel -&gt; 'a option -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> Printf.fprintf stdout
   <span class="ocamlstring">"The current setting is %a. \nThere is only %a\n"</span>
   (pp_option pp_int) (Some 3)
   (pp_option pp_int) None
 ;;</div>



<div class="pre caml-output ok">The current setting is Some(3).
There is only None
- : unit = ()</div></div>

</div><p>


If the value of its argument its <span class="c003">None</span>, the printer returned by pp_option
printer prints <span class="c003">None</span> otherwise it uses the provided printer to print <span class="c003">Some </span>.</p><p>Here is how to rewrite the pretty-printer using <span class="c003">fprintf</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> pp_expr ppf expr =
   <span class="ocamlkeyword">let</span> open_paren prec op_prec output =
     <span class="ocamlkeyword">if</span> prec &gt; op_prec <span class="ocamlkeyword">then</span> Printf.fprintf output <span class="ocamlstring">"%s"</span> <span class="ocamlstring">"("</span> <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> close_paren prec op_prec output =
     <span class="ocamlkeyword">if</span> prec &gt; op_prec <span class="ocamlkeyword">then</span> Printf.fprintf output <span class="ocamlstring">"%s"</span> <span class="ocamlstring">")"</span> <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> print prec ppf expr =
       <span class="ocamlkeyword">match</span> expr <span class="ocamlkeyword">with</span>
       | Const c -&gt; Printf.fprintf ppf <span class="ocamlstring">"%F"</span> c
       | Var v -&gt; Printf.fprintf ppf <span class="ocamlstring">"%s"</span> v
       | Sum(f, g) -&gt;
           open_paren prec 0 ppf;
           Printf.fprintf ppf <span class="ocamlstring">"%a + %a"</span> (print 0) f (print 0) g;
           close_paren prec 0 ppf
       | Diff(f, g) -&gt;
           open_paren prec 0 ppf;
           Printf.fprintf ppf <span class="ocamlstring">"%a - %a"</span> (print 0) f (print 1) g;
           close_paren prec 0 ppf
       | Prod(f, g) -&gt;
           open_paren prec 2 ppf;
           Printf.fprintf ppf <span class="ocamlstring">"%a * %a"</span> (print 2) f (print 2) g;
           close_paren prec 2 ppf
       | Quot(f, g) -&gt;
           open_paren prec 2 ppf;
           Printf.fprintf ppf <span class="ocamlstring">"%a / %a"</span> (print 2) f (print 3) g;
           close_paren prec 2 ppf
   <span class="ocamlkeyword">in</span> print 0 ppf expr;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> pp_expr : out_channel -&gt; expression -&gt; unit = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> pp_expr stdout e; print_newline ();;</div>



<div class="pre caml-output ok">2. * x + 1.
- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> pp_expr stdout (deriv e <span class="ocamlstring">"x"</span>); print_newline ();;</div>



<div class="pre caml-output ok">2. * 1. + 0. * x + 0.
- : unit = ()</div></div>

</div><p>Due to the way that format string are build, storing a format string requires
an explicit type annotation:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> str : _ format =
     <span class="ocamlstring">"%i is an integer value, %F is a float, %S\n"</span>;;</div></div>

</div><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> Printf.printf str 3 4.5 <span class="ocamlstring">"string value"</span>;;</div>



<div class="pre caml-output ok">3 is an integer value, 4.5 is a float, <span class="ocamlstring">"string value"</span>
- : unit = ()</div></div>

</div>
<h2 class="section" id="s:standalone-programs"><a class="section-anchor" href="#s:standalone-programs" aria-hidden="true">﻿</a>11&nbsp;&nbsp;Standalone OCaml programs</h2>
<p>All examples given so far were executed under the interactive system.
OCaml code can also be compiled separately and executed
non-interactively using the batch compilers <span class="c003">ocamlc</span> and <span class="c003">ocamlopt</span>.
The source code must be put in a file with extension <span class="c003">.ml</span>. It
consists of a sequence of phrases, which will be evaluated at runtime
in their order of appearance in the source file. Unlike in interactive
mode, types and values are not printed automatically; the program must
call printing functions explicitly to produce some output. The <span class="c003">;;</span> used
in the interactive examples is not required in
source files created for use with OCaml compilers, but can be helpful
to mark the end of a top-level expression unambiguously even when
there are syntax errors.
Here is a
sample standalone program to print Fibonacci numbers:
</p><pre>(* File fib.ml *)
let rec fib n =
  if n &lt; 2 then 1 else fib (n-1) + fib (n-2);;
let main () =
  let arg = int_of_string Sys.argv.(1) in
  print_int (fib arg);
  print_newline ();
  exit 0;;
main ();;
</pre><p><span class="c003">Sys.argv</span> is an array of strings containing the command-line
parameters. <span class="c003">Sys.argv.(1)</span> is thus the first command-line parameter.
The program above is compiled and executed with the following shell
commands:
</p><pre>$ ocamlc -o fib fib.ml
$ ./fib 10
89
$ ./fib 20
10946
</pre><p>
More complex standalone OCaml programs are typically composed of
multiple source files, and can link with precompiled libraries.
Chapters&nbsp;<a href="comp.html#c%3Acamlc">9</a> and&nbsp;<a href="native.html#c%3Anativecomp">12</a> explain how to use the
batch compilers <span class="c003">ocamlc</span> and <span class="c003">ocamlopt</span>. Recompilation of
multi-file OCaml projects can be automated using third-party
build systems, such as the
<a href="https://github.com/ocaml/ocamlbuild/">ocamlbuild</a>
compilation manager.

</p>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>