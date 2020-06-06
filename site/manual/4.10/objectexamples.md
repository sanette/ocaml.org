<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="coreexamples.html">The core language</a></li><li><a href="moduleexamples.html">The module system</a></li><li class="active"><a href="objectexamples.html">Objects in OCaml</a></li><li><a href="lablexamples.html">Labels and variants</a></li><li><a href="polymorphism.html">Polymorphism and its limitations</a></li><li><a href="advexamples.html">Advanced examples with classes and modules</a></li></ul>




<h1 class="chapter" id="sec26"><span>Chapter 3</span>&nbsp;&nbsp;Objects in OCaml</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.10</a></div><div class="toc_title"><a href="#">Objects in OCaml</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="objectexamples.html#s%3Aclasses-and-objects">1&nbsp;&nbsp;Classes and objects</a>
</li><li><a href="objectexamples.html#s%3Aimmediate-objects">2&nbsp;&nbsp;Immediate objects</a>
</li><li><a href="objectexamples.html#s%3Areference-to-self">3&nbsp;&nbsp;Reference to self</a>
</li><li><a href="objectexamples.html#s%3Ainitializers">4&nbsp;&nbsp;Initializers</a>
</li><li><a href="objectexamples.html#s%3Avirtual-methods">5&nbsp;&nbsp;Virtual methods</a>
</li><li><a href="objectexamples.html#s%3Aprivate-methods">6&nbsp;&nbsp;Private methods</a>
</li><li><a href="objectexamples.html#s%3Aclass-interfaces">7&nbsp;&nbsp;Class interfaces</a>
</li><li><a href="objectexamples.html#s%3Ainheritance">8&nbsp;&nbsp;Inheritance</a>
</li><li><a href="objectexamples.html#s%3Amultiple-inheritance">9&nbsp;&nbsp;Multiple inheritance</a>
</li><li><a href="objectexamples.html#s%3Aparameterized-classes">10&nbsp;&nbsp;Parameterized classes</a>
</li><li><a href="objectexamples.html#s%3Apolymorphic-methods">11&nbsp;&nbsp;Polymorphic methods</a>
</li><li><a href="objectexamples.html#s%3Ausing-coercions">12&nbsp;&nbsp;Using coercions</a>
</li><li><a href="objectexamples.html#s%3Afunctional-objects">13&nbsp;&nbsp;Functional objects</a>
</li><li><a href="objectexamples.html#s%3Acloning-objects">14&nbsp;&nbsp;Cloning objects</a>
</li><li><a href="objectexamples.html#s%3Arecursive-classes">15&nbsp;&nbsp;Recursive classes</a>
</li><li><a href="objectexamples.html#s%3Abinary-methods">16&nbsp;&nbsp;Binary methods</a>
</li><li><a href="objectexamples.html#s%3Afriends">17&nbsp;&nbsp;Friends</a>
</li></ul></nav></header>
<p>
<a id="c:objectexamples"></a>
</p><p>
</p><p><br>
<br>
</p><p>This chapter gives an overview of the object-oriented features of
OCaml.</p><p>Note that the relationship between object, class and type in OCaml is
different than in mainstream object-oriented languages such as Java and
C++, so you shouldn’t assume that similar keywords mean the same thing.
Object-oriented features are used much less frequently in OCaml than
in those languages. OCaml has alternatives that are often more appropriate,
such as modules and functors. Indeed, many OCaml programs do not use objects
at all.</p>
<h2 class="section" id="s:classes-and-objects"><a class="section-anchor" href="#s:classes-and-objects" aria-hidden="true"></a>1&nbsp;&nbsp;Classes and objects</h2>
<p>The class <span class="c003">point</span> below defines one instance variable <span class="c003">x</span> and two methods
<span class="c003">get_x</span> and <span class="c003">move</span>. The initial value of the instance variable is <span class="c003">0</span>.
The variable <span class="c003">x</span> is declared mutable, so the method <span class="c003">move</span> can change
its value.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = 0
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">method</span> move : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>

</div><p>We now create a new point <span class="c003">p</span>, instance of the <span class="c003">point</span> class.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> point;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : point = &lt;obj&gt;</div></div>

</div><p>


Note that the type of <span class="c003">p</span> is <span class="c003">point</span>. This is an abbreviation
automatically defined by the class definition above. It stands for the
object type <span class="c003">&lt;get_x : int; move : int -&gt; unit&gt;</span>, listing the methods
of class <span class="c003">point</span> along with their types.</p><p>We now invoke some methods of <span class="c003">p</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 0</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#move 3;;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 3</div></div>

</div><p>The evaluation of the body of a class only takes place at object
creation time. Therefore, in the following example, the instance
variable <span class="c003">x</span> is initialized to different values for two different
objects.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> x0 = <span class="ocamlkeyword">ref</span> 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> x0 : int <span class="ocamlkeyword">ref</span> = {contents = 0}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = incr x0; !x0
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">method</span> move : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">new</span> point#get_x;;</div>



<div class="pre caml-output ok">- : int = 1</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">new</span> point#get_x;;</div>



<div class="pre caml-output ok">- : int = 2</div></div>

</div><p>The class <span class="c003">point</span> can also be abstracted over the initial values of
the <span class="c003">x</span> coordinate.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point = <span class="ocamlkeyword">fun</span> x_init -&gt;
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  int -&gt;
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">method</span> move : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>

</div><p>


Like in function definitions, the definition above can be
abbreviated as:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  int -&gt;
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">method</span> move : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>

</div><p>


An instance of the class <span class="c003">point</span> is now a function that expects an
initial parameter to create a point object:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">new</span> point;;</div>



<div class="pre caml-output ok">- : int -&gt; point = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> point 7;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : point = &lt;obj&gt;</div></div>

</div><p>


The parameter <span class="c003">x_init</span> is, of course, visible in the whole body of the
definition, including methods. For instance, the method <span class="c003">get_offset</span>
in the class below returns the position of the object relative to its
initial position.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> get_offset = x - x_init
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Expressions can be evaluated and bound before defining the object body
of the class. This is useful to enforce invariants. For instance,
points can be automatically adjusted to the nearest point on a grid,
as follows:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> adjusted_point x_init =
   <span class="ocamlkeyword">let</span> origin = (x_init / 10) * 10 <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = origin
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> get_offset = x - origin
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> adjusted_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


(One could also raise an exception if the <span class="c003">x_init</span> coordinate is not
on the grid.) In fact, the same effect could here be obtained by
calling the definition of class <span class="c003">point</span> with the value of the
<span class="c003">origin</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> adjusted_point x_init =  point ((x_init / 10) * 10);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> adjusted_point : int -&gt; point</div></div>

</div><p>


An alternate solution would have been to define the adjustment in
a special allocation function:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> new_adjusted_point x_init = <span class="ocamlkeyword">new</span> point ((x_init / 10) * 10);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> new_adjusted_point : int -&gt; point = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


However, the former pattern is generally more appropriate, since
the code for adjustment is part of the definition of the class and will be
inherited.</p><p>This ability provides class constructors as can be found in other
languages. Several constructors can be defined this way to build objects of
the same class but with different initialization patterns; an
alternative is to use initializers, as described below in
section&nbsp;<a href="#s%3Ainitializers">3.4</a>.</p>
<h2 class="section" id="s:immediate-objects"><a class="section-anchor" href="#s:immediate-objects" aria-hidden="true">﻿</a>2&nbsp;&nbsp;Immediate objects</h2>
<p>There is another, more direct way to create an object: create it
without going through a class.</p><p>The syntax is exactly the same as for class expressions, but the
result is a single object rather than a class. All the constructs
described in the rest of this section also apply to immediate objects.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = 0
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : &lt; get_x : int; move : int -&gt; unit &gt; = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 0</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#move 3;;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 3</div></div>

</div><p>Unlike classes, which cannot be defined inside an expression,
immediate objects can appear anywhere, using variables from their
environment.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> minmax x y =
   <span class="ocamlkeyword">if</span> x &lt; y <span class="ocamlkeyword">then</span> <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> min = x <span class="ocamlkeyword">method</span> max = y <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">else</span> <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> min = y <span class="ocamlkeyword">method</span> max = x <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> minmax : 'a -&gt; 'a -&gt; &lt; max : 'a; min : 'a &gt; = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Immediate objects have two weaknesses compared to classes: their types
are not abbreviated, and you cannot inherit from them. But these two
weaknesses can be advantages in some situations, as we will see
in sections&nbsp;<a href="#s%3Areference-to-self">3.3</a> and&nbsp;<a href="#s%3Aparameterized-classes">3.10</a>.</p>
<h2 class="section" id="s:reference-to-self"><a class="section-anchor" href="#s:reference-to-self" aria-hidden="true">﻿</a>3&nbsp;&nbsp;Reference to self</h2>
<p>A method or an initializer can invoke methods on self (that is,
the current object). For that, self must be explicitly bound, here to
the variable <span class="c003">s</span> (<span class="c003">s</span> could be any identifier, even though we will
often choose the name <span class="c003">self</span>.)


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> printable_point x_init =
   <span class="ocamlkeyword">object</span> (s)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
     <span class="ocamlkeyword">method</span> print = print_int s#get_x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> printable_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> print : unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> printable_point 7;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : printable_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#print;;</div>



<div class="pre caml-output ok">7- : unit = ()</div></div>

</div><p>


Dynamically, the variable <span class="c003">s</span> is bound at the invocation of a method. In
particular, when the class <span class="c003">printable_point</span> is inherited, the variable
<span class="c003">s</span> will be correctly bound to the object of the subclass.</p><p>A common problem with self is that, as its type may be extended in
subclasses, you cannot fix it in advance. Here is a simple example.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> ints = <span class="ocamlkeyword">ref</span> [];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> ints : '_weak1 list <span class="ocamlkeyword">ref</span> = {contents = []}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> my_int =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">method</span> n = 1
     <span class="ocamlkeyword">method</span> register = ints := <span class="ocamlhighlight">self</span> :: !ints
   <span class="ocamlkeyword">end</span> ;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type &lt; n : int; register : 'a; .. &gt;
       but an expression was expected of type 'weak1
       Self type cannot escape its class</div></div>

</div><p>


You can ignore the first two lines of the error message. What matters
is the last one: putting self into an external reference would make it
impossible to extend it through inheritance.
We will see in section&nbsp;<a href="#s%3Ausing-coercions">3.12</a> a workaround to this
problem.
Note however that, since immediate objects are not extensible, the
problem does not occur with them.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> my_int =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">method</span> n = 1
     <span class="ocamlkeyword">method</span> register = ints := self :: !ints
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> my_int : &lt; n : int; register : unit &gt; = &lt;obj&gt;</div></div>

</div>
<h2 class="section" id="s:initializers"><a class="section-anchor" href="#s:initializers" aria-hidden="true">﻿</a>4&nbsp;&nbsp;Initializers</h2>
<p>Let-bindings within class definitions are evaluated before the object
is constructed. It is also possible to evaluate an expression
immediately after the object has been built. Such code is written as
an anonymous hidden method called an initializer. Therefore, it can
access self and the instance variables.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> printable_point x_init =
   <span class="ocamlkeyword">let</span> origin = (x_init / 10) * 10 <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = origin
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
     <span class="ocamlkeyword">method</span> print = print_int self#get_x
     <span class="ocamlkeyword">initializer</span> print_string <span class="ocamlstring">"new point at "</span>; self#print; print_newline ()
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> printable_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> print : unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> printable_point 17;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">new</span> point at 10
<span class="ocamlkeyword">val</span> p : printable_point = &lt;obj&gt;</div></div>

</div><p>


Initializers cannot be overridden. On the contrary, all initializers are
evaluated sequentially.
Initializers are particularly useful to enforce invariants.
Another example can be seen in section&nbsp;<a href="advexamples.html#s%3Aextended-bank-accounts">6.1</a>.</p>
<h2 class="section" id="s:virtual-methods"><a class="section-anchor" href="#s:virtual-methods" aria-hidden="true">﻿</a>5&nbsp;&nbsp;Virtual methods</h2>
<p>It is possible to declare a method without actually defining it, using
the keyword <span class="c003">virtual</span>. This method will be provided later in
subclasses. A class containing virtual methods must be flagged
<span class="c003">virtual</span>, and cannot be instantiated (that is, no object of this class
can be created). It still defines type abbreviations (treating virtual methods
as other methods.)


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> abstract_point x_init =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> get_x : int
     <span class="ocamlkeyword">method</span> get_offset = self#get_x - x_init
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> move : int -&gt; unit
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> abstract_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> get_x : int
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> abstract_point x_init
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>Instance variables can also be declared as virtual, with the same effect
as with methods.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> abstract_point2 =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> <span class="ocamlkeyword">virtual</span> x : int
     <span class="ocamlkeyword">method</span> move d = x &lt;- x + d
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> abstract_point2 :
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> <span class="ocamlkeyword">virtual</span> x : int <span class="ocamlkeyword">method</span> move : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point2 x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> abstract_point2
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_offset = x - x_init
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point2 :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div>
<h2 class="section" id="s:private-methods"><a class="section-anchor" href="#s:private-methods" aria-hidden="true">﻿</a>6&nbsp;&nbsp;Private methods</h2>
<p>Private methods are methods that do not appear in object interfaces.
They can only be invoked from other methods of the same object.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> restricted_point x_init =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> move d = x &lt;- x + d
     <span class="ocamlkeyword">method</span> bump = self#move 1
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> restricted_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> bump : unit
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> restricted_point 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : restricted_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlhighlight">p</span>#move 10 ;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type restricted_point
       It has no method move</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#bump;;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>

</div><p>


Note that this is not the same thing as private and protected methods
in Java or C++, which can be called from other objects of the same
class. This is a direct consequence of the independence between types
and classes in OCaml: two unrelated classes may produce
objects of the same type, and there is no way at the type level to
ensure that an object comes from a specific class. However a possible
encoding of friend methods is given in section&nbsp;<a href="#s%3Afriends">3.17</a>.</p><p>Private methods are inherited (they are by default visible in subclasses),
unless they are hidden by signature matching, as described below.</p><p>Private methods can be made public in a subclass.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point_again x =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> restricted_point x
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> move : _
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point_again :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> bump : unit
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


The annotation <span class="c003">virtual</span> here is only used to mention a method without
providing its definition. Since we didn’t add the <span class="c003">private</span>
annotation, this makes the method public, keeping the original
definition.</p><p>An alternative definition is


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point_again x =
   <span class="ocamlkeyword">object</span> (self : &lt; move : _; ..&gt; )
     <span class="ocamlkeyword">inherit</span> restricted_point x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point_again :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> bump : unit
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


The constraint on self’s type is requiring a public <span class="c003">move</span> method, and
this is sufficient to override <span class="c003">private</span>.</p><p>One could think that a private method should remain private in a subclass.
However, since the method is visible in a subclass, it is always possible
to pick its code and define a method of the same name that runs that
code, so yet another (heavier) solution would be:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> point_again x =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> restricted_point x <span class="ocamlkeyword">as</span> super
     <span class="ocamlkeyword">method</span> move = super#move
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> point_again :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> bump : unit
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>Of course, private methods can also be virtual. Then, the keywords must
appear in this order <span class="c003">method private virtual</span>.</p>
<h2 class="section" id="s:class-interfaces"><a class="section-anchor" href="#s:class-interfaces" aria-hidden="true">﻿</a>7&nbsp;&nbsp;Class interfaces</h2>
<p>Class interfaces are inferred from class definitions. They may also
be defined directly and used to restrict the type of a class. Like class
declarations, they also define a new type abbreviation.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> restricted_point_type =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> get_x : int
     <span class="ocamlkeyword">method</span> bump : unit
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> restricted_point_type =
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> bump : unit <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">fun</span> (x : restricted_point_type) -&gt; x;;</div>



<div class="pre caml-output ok">- : restricted_point_type -&gt; restricted_point_type = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


In addition to program documentation, class interfaces can be used to
constrain the type of a class. Both concrete instance variables and concrete
private methods can be hidden by a class type constraint. Public
methods and virtual members, however, cannot.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> restricted_point' x = (restricted_point x : restricted_point_type);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> restricted_point' : int -&gt; restricted_point_type</div></div>

</div><p>


Or, equivalently:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> restricted_point' = (restricted_point : int -&gt; restricted_point_type);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> restricted_point' : int -&gt; restricted_point_type</div></div>

</div><p>


The interface of a class can also be specified in a module
signature, and used to restrict the inferred signature of a module.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> POINT = <span class="ocamlkeyword">sig</span>
   <span class="ocamlkeyword">class</span> restricted_point' : int -&gt;
     <span class="ocamlkeyword">object</span>
       <span class="ocamlkeyword">method</span> get_x : int
       <span class="ocamlkeyword">method</span> bump : unit
     <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> POINT =
  <span class="ocamlkeyword">sig</span>
    <span class="ocamlkeyword">class</span> restricted_point' :
      int -&gt; <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> bump : unit <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">end</span>
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Point : POINT = <span class="ocamlkeyword">struct</span>
   <span class="ocamlkeyword">class</span> restricted_point' = restricted_point
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">module</span> Point : POINT</div></div>

</div>
<h2 class="section" id="s:inheritance"><a class="section-anchor" href="#s:inheritance" aria-hidden="true">﻿</a>8&nbsp;&nbsp;Inheritance</h2>
<p>We illustrate inheritance by defining a class of colored points that
inherits from the class of points. This class has all instance
variables and all methods of class <span class="c003">point</span>, plus a new instance
variable <span class="c003">c</span> and a new method <span class="c003">color</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> colored_point x (c : string) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> point x
     <span class="ocamlkeyword">val</span> c = c
     <span class="ocamlkeyword">method</span> color = c
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> colored_point :
  int -&gt;
  string -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> c : string
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> color : string
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p' = <span class="ocamlkeyword">new</span> colored_point 5 <span class="ocamlstring">"red"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p' : colored_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p'#get_x, p'#color;;</div>



<div class="pre caml-output ok">- : int * string = (5, <span class="ocamlstring">"red"</span>)</div></div>

</div><p>


A point and a colored point have incompatible types, since a point has
no method <span class="c003">color</span>. However, the function <span class="c003">get_x</span> below is a generic
function applying method <span class="c003">get_x</span> to any object <span class="c003">p</span> that has this
method (and possibly some others, which are represented by an ellipsis
in the type). Thus, it applies to both points and colored points.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> get_succ_x p = p#get_x + 1;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> get_succ_x : &lt; get_x : int; .. &gt; -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> get_succ_x p + get_succ_x p';;</div>



<div class="pre caml-output ok">- : int = 8</div></div>

</div><p>


Methods need not be declared previously, as shown by the example:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> set_x p = p#set_x;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> set_x : &lt; set_x : 'a; .. &gt; -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> incr p = set_x p (get_succ_x p);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> incr : &lt; get_x : int; set_x : int -&gt; 'a; .. &gt; -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div>
<h2 class="section" id="s:multiple-inheritance"><a class="section-anchor" href="#s:multiple-inheritance" aria-hidden="true">﻿</a>9&nbsp;&nbsp;Multiple inheritance</h2>
<p>Multiple inheritance is allowed. Only the last definition of a method
is kept: the redefinition in a subclass of a method that was visible in
the parent class overrides the definition in the parent class.
Previous definitions of a method can be reused by binding the related
ancestor. Below, <span class="c003">super</span> is bound to the ancestor <span class="c003">printable_point</span>.
The name <span class="c003">super</span> is a pseudo value identifier that can only be used to
invoke a super-class method, as in <span class="c003">super#print</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> printable_colored_point y c =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">val</span> c = c
     <span class="ocamlkeyword">method</span> color = c
     <span class="ocamlkeyword">inherit</span> printable_point y <span class="ocamlkeyword">as</span> super
     <span class="ocamlkeyword">method</span>! print =
       print_string <span class="ocamlstring">"("</span>;
       super#print;
       print_string <span class="ocamlstring">", "</span>;
       print_string (self#color);
       print_string <span class="ocamlstring">")"</span>
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> printable_colored_point :
  int -&gt;
  string -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> c : string
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> color : string
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> print : unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p' = <span class="ocamlkeyword">new</span> printable_colored_point 17 <span class="ocamlstring">"red"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">new</span> point at (10, red)
<span class="ocamlkeyword">val</span> p' : printable_colored_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p'#print;;</div>



<div class="pre caml-output ok">(10, red)- : unit = ()</div></div>

</div><p>


A private method that has been hidden in the parent class is no longer
visible, and is thus not overridden. Since initializers are treated as
private methods, all initializers along the class hierarchy are evaluated,
in the order they are introduced.</p><p>Note that for clarity’s sake, the method <span class="c003">print</span> is explicitly marked as
overriding another definition by annotating the <span class="c003">method</span> keyword with
an exclamation mark <span class="c003">!</span>. If the method <span class="c003">print</span> were not overriding the
<span class="c003">print</span> method of <span class="c003">printable_point</span>, the compiler would raise an error:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input">   <span class="ocamlkeyword">object</span>
     <span class="ocamlhighlight">method! m = ()</span>
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: The method `m' has no previous definition</div></div>

</div><p>This explicit overriding annotation also works
for <span class="c003">val</span> and <span class="c003">inherit</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> another_printable_colored_point y c c' =
   <span class="ocamlkeyword">object</span> (self)
   <span class="ocamlkeyword">inherit</span> printable_point y
   <span class="ocamlkeyword">inherit</span>! printable_colored_point y c
   <span class="ocamlkeyword">val</span>! c = c'
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> another_printable_colored_point :
  int -&gt;
  string -&gt;
  string -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> c : string
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> color : string
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> print : unit
  <span class="ocamlkeyword">end</span></div></div>

</div>
<h2 class="section" id="s:parameterized-classes"><a class="section-anchor" href="#s:parameterized-classes" aria-hidden="true">﻿</a>10&nbsp;&nbsp;Parameterized classes</h2>
<p>Reference cells can be implemented as objects.
The naive definition fails to typecheck:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlhighlight">class oref x_init =
   object
     val mutable x = x_init
     method get = x
     method set y = x &lt;- y
   end</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: Some type variables are unbound in this type:
         class oref :
           'a -&gt;
           object
             val mutable x : 'a
             method get : 'a
             method set : 'a -&gt; unit
           end
       The method get has type 'a where 'a is unbound</div></div>

</div><p>


The reason is that at least one of the methods has a polymorphic type
(here, the type of the value stored in the reference cell), thus
either the class should be parametric, or the method type should be
constrained to a monomorphic type. A monomorphic instance of the class could
be defined by:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> oref (x_init:int) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get = x
     <span class="ocamlkeyword">method</span> set y = x &lt;- y
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> oref :
  int -&gt;
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int <span class="ocamlkeyword">method</span> get : int <span class="ocamlkeyword">method</span> set : int -&gt; unit <span class="ocamlkeyword">end</span></div></div>

</div><p>


Note that since immediate objects do not define a class type, they have
no such restriction.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> new_oref x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init
     <span class="ocamlkeyword">method</span> get = x
     <span class="ocamlkeyword">method</span> set y = x &lt;- y
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> new_oref : 'a -&gt; &lt; get : 'a; set : 'a -&gt; unit &gt; = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


On the other hand, a class for polymorphic references must explicitly
list the type parameters in its declaration. Class type parameters are
listed between <span class="c003">[</span> and <span class="c003">]</span>. The type parameters must also be
bound somewhere in the class body by a type constraint.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] oref x_init =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = (x_init : 'a)
     <span class="ocamlkeyword">method</span> get = x
     <span class="ocamlkeyword">method</span> set y = x &lt;- y
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] oref :
  'a -&gt; <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : 'a <span class="ocamlkeyword">method</span> get : 'a <span class="ocamlkeyword">method</span> set : 'a -&gt; unit <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> r = <span class="ocamlkeyword">new</span> oref 1 <span class="ocamlkeyword">in</span> r#set 2; (r#get);;</div>



<div class="pre caml-output ok">- : int = 2</div></div>

</div><p>


The type parameter in the declaration may actually be constrained in the
body of the class definition. In the class type, the actual value of
the type parameter is displayed in the <span class="c003">constraint</span> clause.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] oref_succ (x_init:'a) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x = x_init + 1
     <span class="ocamlkeyword">method</span> get = x
     <span class="ocamlkeyword">method</span> set y = x &lt;- y
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] oref_succ :
  'a -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = int
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> get : int
    <span class="ocamlkeyword">method</span> set : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Let us consider a more complex example: define a circle, whose center
may be any kind of point. We put an additional type
constraint in method <span class="c003">move</span>, since no free variables must remain
unaccounted for by the class type parameters.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] circle (c : 'a) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> center = c
     <span class="ocamlkeyword">method</span> center = center
     <span class="ocamlkeyword">method</span> set_center c = center &lt;- c
     <span class="ocamlkeyword">method</span> move = (center#move : int -&gt; unit)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] circle :
  'a -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = &lt; move : int -&gt; unit; .. &gt;
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> center : 'a
    <span class="ocamlkeyword">method</span> center : 'a
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> set_center : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


An alternate definition of <span class="c003">circle</span>, using a <span class="c003">constraint</span> clause in
the class definition, is shown below. The type <span class="c003">#point</span> used below in
the <span class="c003">constraint</span> clause is an abbreviation produced by the definition
of class <span class="c003">point</span>. This abbreviation unifies with the type of any
object belonging to a subclass of class <span class="c003">point</span>. It actually expands to
<span class="c003">&lt; get_x : int; move : int -&gt; unit; .. &gt;</span>. This leads to the following
alternate definition of <span class="c003">circle</span>, which has slightly stronger
constraints on its argument, as we now expect <span class="c003">center</span> to have a
method <span class="c003">get_x</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] circle (c : 'a) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">constraint</span> 'a = #point
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> center = c
     <span class="ocamlkeyword">method</span> center = center
     <span class="ocamlkeyword">method</span> set_center c = center &lt;- c
     <span class="ocamlkeyword">method</span> move = center#move
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] circle :
  'a -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = #point
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> center : 'a
    <span class="ocamlkeyword">method</span> center : 'a
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> set_center : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


The class <span class="c003">colored_circle</span> is a specialized version of class
<span class="c003">circle</span> that requires the type of the center to unify with
<span class="c003">#colored_point</span>, and adds a method <span class="c003">color</span>. Note that when specializing a
parameterized class, the instance of type parameter must always be
explicitly given. It is again written between <span class="c003">[</span> and <span class="c003">]</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] colored_circle c =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">constraint</span> 'a = #colored_point
     <span class="ocamlkeyword">inherit</span> ['a] circle c
     <span class="ocamlkeyword">method</span> color = center#color
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] colored_circle :
  'a -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = #colored_point
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> center : 'a
    <span class="ocamlkeyword">method</span> center : 'a
    <span class="ocamlkeyword">method</span> color : string
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> set_center : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div>
<h2 class="section" id="s:polymorphic-methods"><a class="section-anchor" href="#s:polymorphic-methods" aria-hidden="true">﻿</a>11&nbsp;&nbsp;Polymorphic methods</h2>
<p>While parameterized classes may be polymorphic in their contents, they
are not enough to allow polymorphism of method use.</p><p>A classical example is defining an iterator.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> List.fold_left;;</div>



<div class="pre caml-output ok">- : ('a -&gt; 'b -&gt; 'a) -&gt; 'a -&gt; 'b list -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] intlist (l : int list) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> empty = (l = [])
     <span class="ocamlkeyword">method</span> fold f (accu : 'a) = List.fold_left f accu l
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] intlist :
  int list -&gt;
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> empty : bool <span class="ocamlkeyword">method</span> fold : ('a -&gt; int -&gt; 'a) -&gt; 'a -&gt; 'a <span class="ocamlkeyword">end</span></div></div>

</div><p>


At first look, we seem to have a polymorphic iterator, however this
does not work in practice.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> l = <span class="ocamlkeyword">new</span> intlist [1; 2; 3];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : '_weak2 intlist = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> l#fold (<span class="ocamlkeyword">fun</span> x y -&gt; x+y) 0;;</div>



<div class="pre caml-output ok">- : int = 6</div></div>
<div class="ocaml">



<div class="pre caml-input"> l;;</div>



<div class="pre caml-output ok">- : int intlist = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> l#fold (<span class="ocamlkeyword">fun</span> s x -&gt; <span class="ocamlhighlight">s</span> ^ Int.to_string x ^ <span class="ocamlstring">" "</span>) <span class="ocamlstring">""</span> ;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type int but an expression was expected of type
         string</div></div>

</div><p>


Our iterator works, as shows its first use for summation. However,
since objects themselves are not polymorphic (only their constructors
are), using the <span class="c003">fold</span> method fixes its type for this individual object.
Our next attempt to use it as a string iterator fails.</p><p>The problem here is that quantification was wrongly located: it is
not the class we want to be polymorphic, but the <span class="c003">fold</span> method.
This can be achieved by giving an explicitly polymorphic type in the
method definition.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> intlist (l : int list) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> empty = (l = [])
     <span class="ocamlkeyword">method</span> fold : 'a. ('a -&gt; int -&gt; 'a) -&gt; 'a -&gt; 'a =
       <span class="ocamlkeyword">fun</span> f accu -&gt; List.fold_left f accu l
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> intlist :
  int list -&gt;
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> empty : bool <span class="ocamlkeyword">method</span> fold : ('a -&gt; int -&gt; 'a) -&gt; 'a -&gt; 'a <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> l = <span class="ocamlkeyword">new</span> intlist [1; 2; 3];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : intlist = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> l#fold (<span class="ocamlkeyword">fun</span> x y -&gt; x+y) 0;;</div>



<div class="pre caml-output ok">- : int = 6</div></div>
<div class="ocaml">



<div class="pre caml-input"> l#fold (<span class="ocamlkeyword">fun</span> s x -&gt; s ^ Int.to_string x ^ <span class="ocamlstring">" "</span>) <span class="ocamlstring">""</span>;;</div>



<div class="pre caml-output ok">- : string = <span class="ocamlstring">"1 2 3 "</span></div></div>

</div><p>


As you can see in the class type shown by the compiler, while
polymorphic method types must be fully explicit in class definitions
(appearing immediately after the method name), quantified type
variables can be left implicit in class descriptions. Why require types
to be explicit? The problem is that <span class="c003">(int -&gt; int -&gt; int) -&gt; int -&gt; int</span> would also be a valid type for <span class="c003">fold</span>, and it happens to be
incompatible with the polymorphic type we gave (automatic
instantiation only works for toplevel types variables, not for inner
quantifiers, where it becomes an undecidable problem.) So the compiler
cannot choose between those two types, and must be helped.</p><p>However, the type can be completely omitted in the class definition if
it is already known, through inheritance or type constraints on self.
Here is an example of method overriding.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> intlist_rev l =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> intlist l
     <span class="ocamlkeyword">method</span>! fold f accu = List.fold_left f accu (List.rev l)
   <span class="ocamlkeyword">end</span>;;</div></div>

</div><p>


The following idiom separates description and definition.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> ['a] iterator =
   <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> fold : ('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b <span class="ocamlkeyword">end</span>;;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> intlist' l =
   <span class="ocamlkeyword">object</span> (self : int #iterator)
     <span class="ocamlkeyword">method</span> empty = (l = [])
     <span class="ocamlkeyword">method</span> fold f accu = List.fold_left f accu l
   <span class="ocamlkeyword">end</span>;;</div></div>

</div><p>


Note here the <span class="c003">(self : int #iterator)</span> idiom, which ensures that this
object implements the interface <span class="c003">iterator</span>.</p><p>Polymorphic methods are called in exactly the same way as normal
methods, but you should be aware of some limitations of type
inference. Namely, a polymorphic method can only be called if its
type is known at the call site. Otherwise, the method will be assumed
to be monomorphic, and given an incompatible type.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sum lst = lst#fold (<span class="ocamlkeyword">fun</span> x y -&gt; x+y) 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sum : &lt; fold : (int -&gt; int -&gt; int) -&gt; int -&gt; 'a; .. &gt; -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> sum <span class="ocamlhighlight">l</span> ;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression has type intlist
       but an expression was expected of type
         &lt; fold : (int -&gt; int -&gt; int) -&gt; int -&gt; 'a; .. &gt;
       Types for method fold are incompatible</div></div>

</div><p>


The workaround is easy: you should put a type constraint on the
parameter.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sum (lst : _ #iterator) = lst#fold (<span class="ocamlkeyword">fun</span> x y -&gt; x+y) 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sum : int #iterator -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Of course the constraint may also be an explicit method type.
Only occurrences of quantified variables are required.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> sum lst =
   (lst : &lt; fold : 'a. ('a -&gt; _ -&gt; 'a) -&gt; 'a -&gt; 'a; .. &gt;)#fold (+) 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> sum : &lt; fold : 'a. ('a -&gt; int -&gt; 'a) -&gt; 'a -&gt; 'a; .. &gt; -&gt; int = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>Another use of polymorphic methods is to allow some form of implicit
subtyping in method arguments. We have already seen in
section&nbsp;<a href="#s%3Ainheritance">3.8</a> how some functions may be polymorphic in the
class of their argument. This can be extended to methods.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> point0 = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> point0 = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> get_x : int <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> distance_point x =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> point x
     <span class="ocamlkeyword">method</span> distance : 'a. (#point0 <span class="ocamlkeyword">as</span> 'a) -&gt; int =
       <span class="ocamlkeyword">fun</span> other -&gt; abs (other#get_x - x)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> distance_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : int
    <span class="ocamlkeyword">method</span> distance : #point0 -&gt; int
    <span class="ocamlkeyword">method</span> get_offset : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> distance_point 3 <span class="ocamlkeyword">in</span>
 (p#distance (<span class="ocamlkeyword">new</span> point 8), p#distance (<span class="ocamlkeyword">new</span> colored_point 1 <span class="ocamlstring">"blue"</span>));;</div>



<div class="pre caml-output ok">- : int * int = (5, 2)</div></div>

</div><p>


Note here the special syntax <span class="c003">(#point0 as 'a)</span> we have to use to
quantify the extensible part of <span class="c003">#point0</span>. As for the variable binder,
it can be omitted in class specifications. If you want polymorphism
inside object field it must be quantified independently.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> multi_poly =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> m1 : 'a. (&lt; n1 : 'b. 'b -&gt; 'b; .. &gt; <span class="ocamlkeyword">as</span> 'a) -&gt; _ =
       <span class="ocamlkeyword">fun</span> o -&gt; o#n1 <span class="ocamlkeyword">true</span>, o#n1 <span class="ocamlstring">"hello"</span>
     <span class="ocamlkeyword">method</span> m2 : 'a 'b. (&lt; n2 : 'b -&gt; bool; .. &gt; <span class="ocamlkeyword">as</span> 'a) -&gt; 'b -&gt; _ =
       <span class="ocamlkeyword">fun</span> o x -&gt; o#n2 x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> multi_poly :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">method</span> m1 : &lt; n1 : 'b. 'b -&gt; 'b; .. &gt; -&gt; bool * string
    <span class="ocamlkeyword">method</span> m2 : &lt; n2 : 'b -&gt; bool; .. &gt; -&gt; 'b -&gt; bool
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


In method <span class="c003">m1</span>, <span class="c003">o</span> must be an object with at least a method <span class="c003">n1</span>,
itself polymorphic. In method <span class="c003">m2</span>, the argument of <span class="c003">n2</span> and <span class="c003">x</span> must
have the same type, which is quantified at the same level as <span class="c003">'a</span>.</p>
<h2 class="section" id="s:using-coercions"><a class="section-anchor" href="#s:using-coercions" aria-hidden="true">﻿</a>12&nbsp;&nbsp;Using coercions</h2>
<p>Subtyping is never implicit. There are, however, two ways to perform
subtyping. The most general construction is fully explicit: both the
domain and the codomain of the type coercion must be given.</p><p>We have seen that points and colored points have incompatible types.
For instance, they cannot be mixed in the same list. However, a
colored point can be coerced to a point, hiding its <span class="c003">color</span> method:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> colored_point_to_point cp = (cp : colored_point :&gt; point);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> colored_point_to_point : colored_point -&gt; point = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> point 3 <span class="ocamlkeyword">and</span> q = <span class="ocamlkeyword">new</span> colored_point 4 <span class="ocamlstring">"blue"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : point = &lt;obj&gt;
<span class="ocamlkeyword">val</span> q : colored_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> l = [p; (colored_point_to_point q)];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> l : point list = [&lt;obj&gt;; &lt;obj&gt;]</div></div>

</div><p>


An object of type <span class="c003">t</span> can be seen as an object of type <span class="c003">t'</span>
only if <span class="c003">t</span> is a subtype of <span class="c003">t'</span>. For instance, a point cannot be
seen as a colored point.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlhighlight">(p : point :&gt; colored_point)</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: Type point = &lt; get_offset : int; get_x : int; move : int -&gt; unit &gt;
       is not a subtype of
         colored_point =
           &lt; color : string; get_offset : int; get_x : int;
             move : int -&gt; unit &gt;
       The first object type has no method color</div></div>

</div><p>


Indeed, narrowing coercions without runtime checks would be unsafe.
Runtime type checks might raise exceptions, and they would require
the presence of type information at runtime, which is not the case in
the OCaml system.
For these reasons, there is no such operation available in the language.</p><p>Be aware that subtyping and inheritance are not related. Inheritance is a
syntactic relation between classes while subtyping is a semantic relation
between types. For instance, the class of colored points could have been
defined directly, without inheriting from the class of points; the type of
colored points would remain unchanged and thus still be a subtype of
points.
</p><p>The domain of a coercion can often be omitted. For instance, one can
define:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> to_point cp = (cp :&gt; point);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> to_point : #point -&gt; point = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


In this case, the function <span class="c003">colored_point_to_point</span> is an instance of the
function <span class="c003">to_point</span>. This is not always true, however. The fully
explicit coercion is more precise and is sometimes unavoidable.
Consider, for example, the following class:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c0 = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m = {&lt; &gt;} <span class="ocamlkeyword">method</span> n = 0 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> c0 : <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> m : 'a <span class="ocamlkeyword">method</span> n : int <span class="ocamlkeyword">end</span></div></div>

</div><p>


The object type <span class="c003">c0</span> is an abbreviation for <span class="c003">&lt;m : 'a; n : int&gt; as 'a</span>.
Consider now the type declaration:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c1 =  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : c1 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c1 = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : c1 <span class="ocamlkeyword">end</span></div></div>

</div><p>


The object type <span class="c003">c1</span> is an abbreviation for the type <span class="c003">&lt;m : 'a&gt; as 'a</span>.
The coercion from an object of type <span class="c003">c0</span> to an object of type <span class="c003">c1</span> is
correct:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">fun</span> (x:c0) -&gt; (x : c0 :&gt; c1);;</div>



<div class="pre caml-output ok">- : c0 -&gt; c1 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


However, the domain of the coercion cannot always be omitted.
In that case, the solution is to use the explicit form.
Sometimes, a change in the class-type definition can also solve the problem


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c2 = <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> m : 'a <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c2 = <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> m : 'a <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">fun</span> (x:c0) -&gt; (x :&gt; c2);;</div>



<div class="pre caml-output ok">- : c0 -&gt; c2 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


While class types <span class="c003">c1</span> and <span class="c003">c2</span> are different, both object types
<span class="c003">c1</span> and <span class="c003">c2</span> expand to the same object type (same method names and types).
Yet, when the domain of a coercion is left implicit and its co-domain
is an abbreviation of a known class type, then the class type, rather
than the object type, is used to derive the coercion function. This
allows leaving the domain implicit in most cases when coercing form a
subclass to its superclass.
The type of a coercion can always be seen as below:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> to_c1 x = (x :&gt; c1);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> to_c1 : &lt; m : #c1; .. &gt; -&gt; c1 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> to_c2 x = (x :&gt; c2);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> to_c2 : #c2 -&gt; c2 = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Note the difference between these two coercions: in the case of <span class="c003">to_c2</span>,
the type
<span class="c003">#c2 = &lt; m : 'a; .. &gt; as 'a</span> is polymorphically recursive (according
to the explicit recursion in the class type of <span class="c003">c2</span>); hence the
success of applying this coercion to an object of class <span class="c003">c0</span>.
On the other hand, in the first case, <span class="c003">c1</span> was only expanded and
unrolled twice to obtain <span class="c003">&lt; m : &lt; m : c1; .. &gt;; .. &gt;</span> (remember <span class="c003">#c1 = &lt; m : c1; .. &gt;</span>), without introducing recursion.
You may also note that the type of <span class="c003">to_c2</span> is <span class="c003">#c2 -&gt; c2</span> while
the type of <span class="c003">to_c1</span> is more general than <span class="c003">#c1 -&gt; c1</span>. This is not always true,
since there are class types for which some instances of <span class="c003">#c</span> are not subtypes
of <span class="c003">c</span>, as explained in section&nbsp;<a href="#s%3Abinary-methods">3.16</a>. Yet, for
parameterless classes the coercion <span class="c003">(_ :&gt; c)</span> is always more general than
<span class="c003">(_ : #c :&gt; c)</span>.
</p><p>A common problem may occur when one tries to define a coercion to a
class <span class="c003">c</span> while defining class <span class="c003">c</span>. The problem is due to the type
abbreviation not being completely defined yet, and so its subtypes are not
clearly known. Then, a coercion <span class="c003">(_ :&gt; c)</span> or <span class="c003">(_ : #c :&gt; c)</span> is taken to be
the identity function, as in


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">function</span> x -&gt; (x :&gt; 'a);;</div>



<div class="pre caml-output ok">- : 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


As a consequence, if the coercion is applied to <span class="c003">self</span>, as in the
following example, the type of <span class="c003">self</span> is unified with the closed type
<span class="c003">c</span> (a closed object type is an object type without ellipsis). This
would constrain the type of self be closed and is thus rejected.
Indeed, the type of self cannot be closed: this would prevent any
further extension of the class. Therefore, a type error is generated
when the unification of this type with another type would result in a
closed object type.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m = 1 <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">and</span> d = <span class="ocamlkeyword">object</span> (self)
   <span class="ocamlkeyword">inherit</span> c
   <span class="ocamlkeyword">method</span> n = 2
   <span class="ocamlkeyword">method</span> as_c = (<span class="ocamlhighlight">self</span> :&gt; c)
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output error"><span class="ocamlerror">Error</span>: This expression cannot be coerced to type c = &lt; m : int &gt;; it has type
         &lt; as_c : c; m : int; n : int; .. &gt;
       but is here used with type c
       Self type cannot escape its class</div></div>

</div><p>


However, the most common instance of this problem, coercing self to
its current class, is detected as a special case by the type checker,
and properly typed.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c = <span class="ocamlkeyword">object</span> (self) <span class="ocamlkeyword">method</span> m = (self :&gt; c) <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> c : <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : c <span class="ocamlkeyword">end</span></div></div>

</div><p>


This allows the following idiom, keeping a list of all objects
belonging to a class or its subclasses:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> all_c = <span class="ocamlkeyword">ref</span> [];;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> all_c : '_weak3 list <span class="ocamlkeyword">ref</span> = {contents = []}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c (m : int) =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">method</span> m = m
     <span class="ocamlkeyword">initializer</span> all_c := (self :&gt; c) :: !all_c
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> c : int -&gt; <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : int <span class="ocamlkeyword">end</span></div></div>

</div><p>


This idiom can in turn be used to retrieve an object whose type has
been weakened:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> lookup_obj obj = <span class="ocamlkeyword">function</span> [] -&gt; raise Not_found
   | obj' :: l -&gt;
      <span class="ocamlkeyword">if</span> (obj :&gt; &lt; &gt;) = (obj' :&gt; &lt; &gt;) <span class="ocamlkeyword">then</span> obj' <span class="ocamlkeyword">else</span> lookup_obj obj l ;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> lookup_obj : &lt; .. &gt; -&gt; (&lt; .. &gt; <span class="ocamlkeyword">as</span> 'a) list -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> lookup_c obj = lookup_obj obj !all_c;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> lookup_c : &lt; .. &gt; -&gt; &lt; m : int &gt; = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


The type <span class="c003">&lt; m : int &gt;</span> we see here is just the expansion of <span class="c003">c</span>, due
to the use of a reference; we have succeeded in getting back an object
of type <span class="c003">c</span>.</p><p><br>
The previous coercion problem can often be avoided by first
defining the abbreviation, using a class type:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c' = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : int <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> c' = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : int <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c : c' = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m = 1 <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">and</span> d = <span class="ocamlkeyword">object</span> (self)
   <span class="ocamlkeyword">inherit</span> c
   <span class="ocamlkeyword">method</span> n = 2
   <span class="ocamlkeyword">method</span> as_c = (self :&gt; c')
 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> c : c'
<span class="ocamlkeyword">and</span> d : <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> as_c : c' <span class="ocamlkeyword">method</span> m : int <span class="ocamlkeyword">method</span> n : int <span class="ocamlkeyword">end</span></div></div>

</div><p>


It is also possible to use a virtual class. Inheriting from this class
simultaneously forces all methods of <span class="c003">c</span> to have the same
type as the methods of <span class="c003">c'</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> c' = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> m : int <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> c' : <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> m : int <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> c = <span class="ocamlkeyword">object</span> (self) <span class="ocamlkeyword">inherit</span> c' <span class="ocamlkeyword">method</span> m = 1 <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> c : <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> m : int <span class="ocamlkeyword">end</span></div></div>

</div><p>


One could think of defining the type abbreviation directly:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> c' = &lt;m : int&gt;;;</div></div>

</div><p>


However, the abbreviation <span class="c003">#c'</span> cannot be defined directly in a similar way.
It can only be defined by a class or a class-type definition.
This is because a <span class="c003">#</span>-abbreviation carries an implicit anonymous
variable <span class="c003">..</span> that cannot be explicitly named.
The closer you get to it is:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> 'a c'_class = 'a <span class="ocamlkeyword">constraint</span> 'a = &lt; m : int; .. &gt;;;</div></div>

</div><p>


with an extra type variable capturing the open object type.</p>
<h2 class="section" id="s:functional-objects"><a class="section-anchor" href="#s:functional-objects" aria-hidden="true">﻿</a>13&nbsp;&nbsp;Functional objects</h2>
<p>It is possible to write a version of class <span class="c003">point</span> without assignments
on the instance variables. The override construct <span class="c003">{&lt; ... &gt;}</span> returns a copy of
“self” (that is, the current object), possibly changing the value of
some instance variables.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> functional_point y =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> x = y
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = {&lt; x = x + d &gt;}
     <span class="ocamlkeyword">method</span> move_to x = {&lt; x &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> functional_point :
  int -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> x : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; 'a
    <span class="ocamlkeyword">method</span> move_to : int -&gt; 'a
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> functional_point 7;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : functional_point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 7</div></div>
<div class="ocaml">



<div class="pre caml-input"> (p#move 3)#get_x;;</div>



<div class="pre caml-output ok">- : int = 10</div></div>
<div class="ocaml">



<div class="pre caml-input"> (p#move_to 15)#get_x;;</div>



<div class="pre caml-output ok">- : int = 15</div></div>
<div class="ocaml">



<div class="pre caml-input"> p#get_x;;</div>



<div class="pre caml-output ok">- : int = 7</div></div>

</div><p>


As with records, the form <span class="c003">{&lt; x &gt;}</span> is an elided version of
<span class="c003">{&lt; x = x &gt;}</span> which avoids the repetition of the instance variable name.
Note that the type abbreviation <span class="c003">functional_point</span> is recursive, which can
be seen in the class type of <span class="c003">functional_point</span>: the type of self is <span class="c003">'a</span>
and <span class="c003">'a</span> appears inside the type of the method <span class="c003">move</span>.</p><p>The above definition of <span class="c003">functional_point</span> is not equivalent
to the following:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> bad_functional_point y =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> x = y
     <span class="ocamlkeyword">method</span> get_x = x
     <span class="ocamlkeyword">method</span> move d = <span class="ocamlkeyword">new</span> bad_functional_point (x+d)
     <span class="ocamlkeyword">method</span> move_to x = <span class="ocamlkeyword">new</span> bad_functional_point x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> bad_functional_point :
  int -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> x : int
    <span class="ocamlkeyword">method</span> get_x : int
    <span class="ocamlkeyword">method</span> move : int -&gt; bad_functional_point
    <span class="ocamlkeyword">method</span> move_to : int -&gt; bad_functional_point
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


While objects of either class will behave the same, objects of their
subclasses will be different. In a subclass of <span class="c003">bad_functional_point</span>,
the method <span class="c003">move</span> will
keep returning an object of the parent class. On the contrary, in a
subclass of <span class="c003">functional_point</span>, the method <span class="c003">move</span> will return an
object of the subclass.</p><p>Functional update is often used in conjunction with binary methods
as illustrated in section&nbsp;<a href="advexamples.html#ss%3Astring-as-class">6.2.1</a>.</p>
<h2 class="section" id="s:cloning-objects"><a class="section-anchor" href="#s:cloning-objects" aria-hidden="true">﻿</a>14&nbsp;&nbsp;Cloning objects</h2>
<p>Objects can also be cloned, whether they are functional or imperative.
The library function <span class="c003">Oo.copy</span> makes a shallow copy of an object. That is,
it returns a new object that has the same methods and instance
variables as its argument. The
instance variables are copied but their contents are shared.
Assigning a new value to an instance variable of the copy (using a method
call) will not affect instance variables of the original, and conversely.
A deeper assignment (for example if the instance variable is a reference cell)
will of course affect both the original and the copy.</p><p>The type of <span class="c003">Oo.copy</span> is the following:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> Oo.copy;;</div>



<div class="pre caml-output ok">- : (&lt; .. &gt; <span class="ocamlkeyword">as</span> 'a) -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


The keyword <span class="c003">as</span> in that type binds the type variable <span class="c003">'a</span> to
the object type <span class="c003">&lt; .. &gt;</span>. Therefore, <span class="c003">Oo.copy</span> takes an object with
any methods (represented by the ellipsis), and returns an object of
the same type. The type of <span class="c003">Oo.copy</span> is different from type <span class="c003">&lt; .. &gt; -&gt; &lt; .. &gt;</span> as each ellipsis represents a different set of methods.
Ellipsis actually behaves as a type variable.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> point 5;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> p : point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> q = Oo.copy p;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> q : point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> q#move 7; (p#get_x, q#get_x);;</div>



<div class="pre caml-output ok">- : int * int = (5, 12)</div></div>

</div><p>


In fact, <span class="c003">Oo.copy p</span> will behave as <span class="c003">p#copy</span> assuming that a public
method <span class="c003">copy</span> with body <span class="c003">{&lt; &gt;}</span> has been defined in the class of <span class="c003">p</span>.</p><p>Objects can be compared using the generic comparison functions <span class="c003">=</span> and <span class="c003">&lt;&gt;</span>.
Two objects are equal if and only if they are physically equal. In
particular, an object and its copy are not equal.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> q = Oo.copy p;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> q : point = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> p = q, p = p;;</div>



<div class="pre caml-output ok">- : bool * bool = (<span class="ocamlkeyword">false</span>, <span class="ocamlkeyword">true</span>)</div></div>

</div><p>


Other generic comparisons such as (<span class="c003">&lt;</span>, <span class="c003">&lt;=</span>, ...) can also be used on
objects. The
relation <span class="c003">&lt;</span> defines an unspecified but strict ordering on objects. The
ordering relationship between two objects is fixed once for all after the
two objects have been created and it is not affected by mutation of fields.</p><p>Cloning and override have a non empty intersection.
They are interchangeable when used within an object and without
overriding any field:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> copy =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> copy = {&lt; &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> copy : <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> copy : 'a <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> copy =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">method</span> copy = Oo.copy self
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> copy : <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> copy : 'a <span class="ocamlkeyword">end</span></div></div>

</div><p>


Only the override can be used to actually override fields, and
only the <span class="c003">Oo.copy</span> primitive can be used externally.</p><p>Cloning can also be used to provide facilities for saving and
restoring the state of objects.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> backup =
   <span class="ocamlkeyword">object</span> (self : 'mytype)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy = None
     <span class="ocamlkeyword">method</span> save = copy &lt;- Some {&lt; copy = None &gt;}
     <span class="ocamlkeyword">method</span> restore = <span class="ocamlkeyword">match</span> copy <span class="ocamlkeyword">with</span> Some x -&gt; x | None -&gt; self
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> backup :
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy : 'a option
    <span class="ocamlkeyword">method</span> restore : 'a
    <span class="ocamlkeyword">method</span> save : unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


The above definition will only backup one level.
The backup facility can be added to any class by using multiple inheritance.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] backup_ref x = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">inherit</span> ['a] oref x <span class="ocamlkeyword">inherit</span> backup <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] backup_ref :
  'a -&gt;
  <span class="ocamlkeyword">object</span> ('b)
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy : 'b option
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : 'a
    <span class="ocamlkeyword">method</span> get : 'a
    <span class="ocamlkeyword">method</span> restore : 'b
    <span class="ocamlkeyword">method</span> save : unit
    <span class="ocamlkeyword">method</span> set : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> get p n = <span class="ocamlkeyword">if</span> n = 0 <span class="ocamlkeyword">then</span> p # get <span class="ocamlkeyword">else</span> get (p # restore) (n-1);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> get : (&lt; get : 'b; restore : 'a; .. &gt; <span class="ocamlkeyword">as</span> 'a) -&gt; int -&gt; 'b = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> backup_ref 0  <span class="ocamlkeyword">in</span>
 p # save; p # set 1; p # save; p # set 2;
 [get p 0; get p 1; get p 2; get p 3; get p 4];;</div>



<div class="pre caml-output ok">- : int list = [2; 1; 1; 1; 1]</div></div>

</div><p>


We can define a variant of backup that retains all copies. (We also
add a method <span class="c003">clear</span> to manually erase all copies.)


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> backup =
   <span class="ocamlkeyword">object</span> (self : 'mytype)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy = None
     <span class="ocamlkeyword">method</span> save = copy &lt;- Some {&lt; &gt;}
     <span class="ocamlkeyword">method</span> restore = <span class="ocamlkeyword">match</span> copy <span class="ocamlkeyword">with</span> Some x -&gt; x | None -&gt; self
     <span class="ocamlkeyword">method</span> clear = copy &lt;- None
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> backup :
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy : 'a option
    <span class="ocamlkeyword">method</span> clear : unit
    <span class="ocamlkeyword">method</span> restore : 'a
    <span class="ocamlkeyword">method</span> save : unit
  <span class="ocamlkeyword">end</span></div></div>

</div><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] backup_ref x = <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">inherit</span> ['a] oref x <span class="ocamlkeyword">inherit</span> backup <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] backup_ref :
  'a -&gt;
  <span class="ocamlkeyword">object</span> ('b)
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> copy : 'b option
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> x : 'a
    <span class="ocamlkeyword">method</span> clear : unit
    <span class="ocamlkeyword">method</span> get : 'a
    <span class="ocamlkeyword">method</span> restore : 'b
    <span class="ocamlkeyword">method</span> save : unit
    <span class="ocamlkeyword">method</span> set : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> p = <span class="ocamlkeyword">new</span> backup_ref 0  <span class="ocamlkeyword">in</span>
 p # save; p # set 1; p # save; p # set 2;
 [get p 0; get p 1; get p 2; get p 3; get p 4];;</div>



<div class="pre caml-output ok">- : int list = [2; 1; 0; 0; 0]</div></div>

</div>
<h2 class="section" id="s:recursive-classes"><a class="section-anchor" href="#s:recursive-classes" aria-hidden="true">﻿</a>15&nbsp;&nbsp;Recursive classes</h2>
<p>Recursive classes can be used to define objects whose types are
mutually recursive.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> window =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> top_widget = (None : widget option)
     <span class="ocamlkeyword">method</span> top_widget = top_widget
   <span class="ocamlkeyword">end</span>
 <span class="ocamlkeyword">and</span> widget (w : window) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> window = w
     <span class="ocamlkeyword">method</span> window = window
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> window :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> top_widget : widget option
    <span class="ocamlkeyword">method</span> top_widget : widget option
  <span class="ocamlkeyword">end</span>
<span class="ocamlkeyword">and</span> widget : window -&gt; <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">val</span> window : window <span class="ocamlkeyword">method</span> window : window <span class="ocamlkeyword">end</span></div></div>

</div><p>


Although their types are mutually recursive, the classes <span class="c003">widget</span> and
<span class="c003">window</span> are themselves independent.</p>
<h2 class="section" id="s:binary-methods"><a class="section-anchor" href="#s:binary-methods" aria-hidden="true">﻿</a>16&nbsp;&nbsp;Binary methods</h2>
<p>A binary method is a method which takes an argument of the same type
as self. The class <span class="c003">comparable</span> below is a template for classes with a
binary method <span class="c003">leq</span> of type <span class="c003">'a -&gt; bool</span> where the type variable <span class="c003">'a</span>
is bound to the type of self. Therefore, <span class="c003">#comparable</span> expands to <span class="c003">&lt; leq : 'a -&gt; bool; .. &gt; as 'a</span>. We see here that the binder <span class="c003">as</span> also
allows writing recursive types.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> comparable =
   <span class="ocamlkeyword">object</span> (_ : 'a)
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> leq : 'a -&gt; bool
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> comparable : <span class="ocamlkeyword">object</span> ('a) <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> leq : 'a -&gt; bool <span class="ocamlkeyword">end</span></div></div>

</div><p>


We then define a subclass <span class="c003">money</span> of <span class="c003">comparable</span>. The class <span class="c003">money</span>
simply wraps floats as comparable objects. We will extend it below with
more operations. We have to use a type constraint on the class parameter <span class="c003">x</span>
because the primitive <span class="c003">&lt;=</span> is a polymorphic function in
OCaml. The <span class="c003">inherit</span> clause ensures that the type of objects
of this class is an instance of <span class="c003">#comparable</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> money (x : float) =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> comparable
     <span class="ocamlkeyword">val</span> repr = x
     <span class="ocamlkeyword">method</span> value = repr
     <span class="ocamlkeyword">method</span> leq p = repr &lt;= p#value
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> money :
  float -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : float
    <span class="ocamlkeyword">method</span> leq : 'a -&gt; bool
    <span class="ocamlkeyword">method</span> value : float
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Note that the type <span class="c003">money</span> is not a subtype of type
<span class="c003">comparable</span>, as the self type appears in contravariant position
in the type of method <span class="c003">leq</span>.
Indeed, an object <span class="c003">m</span> of class <span class="c003">money</span> has a method <span class="c003">leq</span>
that expects an argument of type <span class="c003">money</span> since it accesses
its <span class="c003">value</span> method. Considering <span class="c003">m</span> of type <span class="c003">comparable</span> would allow a
call to method <span class="c003">leq</span> on <span class="c003">m</span> with an argument that does not have a method
<span class="c003">value</span>, which would be an error.</p><p>Similarly, the type <span class="c003">money2</span> below is not a subtype of type <span class="c003">money</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> money2 x =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> money x
     <span class="ocamlkeyword">method</span> times k = {&lt; repr = k *. repr &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> money2 :
  float -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : float
    <span class="ocamlkeyword">method</span> leq : 'a -&gt; bool
    <span class="ocamlkeyword">method</span> times : float -&gt; 'a
    <span class="ocamlkeyword">method</span> value : float
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


It is however possible to define functions that manipulate objects of
type either <span class="c003">money</span> or <span class="c003">money2</span>: the function <span class="c003">min</span>
will return the minimum of any two objects whose type unifies with
<span class="c003">#comparable</span>. The type of <span class="c003">min</span> is not the same as <span class="c003">#comparable -&gt; #comparable -&gt; #comparable</span>, as the abbreviation <span class="c003">#comparable</span> hides a
type variable (an ellipsis). Each occurrence of this abbreviation
generates a new variable.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> min (x : #comparable) y =
   <span class="ocamlkeyword">if</span> x#leq y <span class="ocamlkeyword">then</span> x <span class="ocamlkeyword">else</span> y;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> min : (#comparable <span class="ocamlkeyword">as</span> 'a) -&gt; 'a -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


This function can be applied to objects of type <span class="c003">money</span>
or <span class="c003">money2</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> (min (<span class="ocamlkeyword">new</span> money  1.3) (<span class="ocamlkeyword">new</span> money 3.1))#value;;</div>



<div class="pre caml-output ok">- : float = 1.3</div></div>
<div class="ocaml">



<div class="pre caml-input"> (min (<span class="ocamlkeyword">new</span> money2 5.0) (<span class="ocamlkeyword">new</span> money2 3.14))#value;;</div>



<div class="pre caml-output ok">- : float = 3.14</div></div>

</div><p>More examples of binary methods can be found in
sections&nbsp;<a href="advexamples.html#ss%3Astring-as-class">6.2.1</a> and&nbsp;<a href="advexamples.html#ss%3Aset-as-class">6.2.3</a>.</p><p>Note the use of override for method <span class="c003">times</span>.
Writing <span class="c003">new money2 (k *. repr)</span> instead of <span class="c003">{&lt; repr = k *. repr &gt;}</span>
would not behave well with inheritance: in a subclass <span class="c003">money3</span> of <span class="c003">money2</span>
the <span class="c003">times</span> method would return an object of class <span class="c003">money2</span> but not of class
<span class="c003">money3</span> as would be expected.</p><p>The class <span class="c003">money</span> could naturally carry another binary method. Here is a
direct definition:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> money x =
   <span class="ocamlkeyword">object</span> (self : 'a)
     <span class="ocamlkeyword">val</span> repr = x
     <span class="ocamlkeyword">method</span> value = repr
     <span class="ocamlkeyword">method</span> print = print_float repr
     <span class="ocamlkeyword">method</span> times k = {&lt; repr = k *. x &gt;}
     <span class="ocamlkeyword">method</span> leq (p : 'a) = repr &lt;= p#value
     <span class="ocamlkeyword">method</span> plus (p : 'a) = {&lt; repr = x +. p#value &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> money :
  float -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : float
    <span class="ocamlkeyword">method</span> leq : 'a -&gt; bool
    <span class="ocamlkeyword">method</span> plus : 'a -&gt; 'a
    <span class="ocamlkeyword">method</span> print : unit
    <span class="ocamlkeyword">method</span> times : float -&gt; 'a
    <span class="ocamlkeyword">method</span> value : float
  <span class="ocamlkeyword">end</span></div></div>

</div>
<h2 class="section" id="s:friends"><a class="section-anchor" href="#s:friends" aria-hidden="true">﻿</a>17&nbsp;&nbsp;Friends</h2>
<p>The above class <span class="c003">money</span> reveals a problem that often occurs with binary
methods. In order to interact with other objects of the same class, the
representation of <span class="c003">money</span> objects must be revealed, using a method such as
<span class="c003">value</span>. If we remove all binary methods (here <span class="c003">plus</span> and <span class="c003">leq</span>),
the representation can easily be hidden inside objects by removing the method
<span class="c003">value</span> as well. However, this is not possible as soon as some binary
method requires access to the representation of objects of the same
class (other than self).


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> safe_money x =
   <span class="ocamlkeyword">object</span> (self : 'a)
     <span class="ocamlkeyword">val</span> repr = x
     <span class="ocamlkeyword">method</span> print = print_float repr
     <span class="ocamlkeyword">method</span> times k = {&lt; repr = k *. x &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> safe_money :
  float -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : float
    <span class="ocamlkeyword">method</span> print : unit
    <span class="ocamlkeyword">method</span> times : float -&gt; 'a
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Here, the representation of the object is known only to a particular object.
To make it available to other objects of the same class, we are forced to
make it available to the whole world. However we can easily restrict the
visibility of the representation using the module system.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> MONEY =
   <span class="ocamlkeyword">sig</span>
     <span class="ocamlkeyword">type</span> t
     <span class="ocamlkeyword">class</span> c : float -&gt;
       <span class="ocamlkeyword">object</span> ('a)
         <span class="ocamlkeyword">val</span> repr : t
         <span class="ocamlkeyword">method</span> value : t
         <span class="ocamlkeyword">method</span> print : unit
         <span class="ocamlkeyword">method</span> times : float -&gt; 'a
         <span class="ocamlkeyword">method</span> leq : 'a -&gt; bool
         <span class="ocamlkeyword">method</span> plus : 'a -&gt; 'a
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Euro : MONEY =
   <span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">type</span> t = float
     <span class="ocamlkeyword">class</span> c x =
       <span class="ocamlkeyword">object</span> (self : 'a)
         <span class="ocamlkeyword">val</span> repr = x
         <span class="ocamlkeyword">method</span> value = repr
         <span class="ocamlkeyword">method</span> print = print_float repr
         <span class="ocamlkeyword">method</span> times k = {&lt; repr = k *. x &gt;}
         <span class="ocamlkeyword">method</span> leq (p : 'a) = repr &lt;= p#value
         <span class="ocamlkeyword">method</span> plus (p : 'a) = {&lt; repr = x +. p#value &gt;}
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>

</div><p>


Another example of friend functions may be found in section&nbsp;<a href="advexamples.html#ss%3Aset-as-class">6.2.3</a>.
These examples occur when a group of objects (here
objects of the same class) and functions should see each others internal
representation, while their representation should be hidden from the
outside. The solution is always to define all friends in the same module,
give access to the representation and use a signature constraint to make the
representation abstract outside the module.</p>
<hr>





<span class="authors c009">(Chapter written by Jérôme Vouillon, Didier Rémy and Jacques Garrigue)</span><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>