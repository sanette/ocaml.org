<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="coreexamples.html">The core language</a></li><li><a href="moduleexamples.html">The module system</a></li><li><a href="objectexamples.html">Objects in OCaml</a></li><li><a href="lablexamples.html">Labels and variants</a></li><li><a href="polymorphism.html">Polymorphism and its limitations</a></li><li class="active"><a href="advexamples.html">Advanced examples with classes and modules</a></li></ul>




<h1 class="chapter" id="sec64"><span>Chapter 6</span>&nbsp;&nbsp;Advanced examples with classes and modules</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.10</a></div><div class="toc_title"><a href="#">Advanced examples with classes and modules</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="advexamples.html#s%3Aextended-bank-accounts">1&nbsp;&nbsp;Extended example: bank accounts</a>
</li><li><a href="advexamples.html#s%3Amodules-as-classes">2&nbsp;&nbsp;Simple modules as classes</a>
</li><li><a href="advexamples.html#s%3Asubject-observer">3&nbsp;&nbsp;The subject/observer pattern</a>
</li></ul></nav></header>
<p>
<a id="c:advexamples"></a></p><p></p><p><br>
<br>
</p><p>In this chapter, we show some larger examples using objects, classes
and modules. We review many of the object features simultaneously on
the example of a bank account. We show how modules taken from the
standard library can be expressed as classes. Lastly, we describe a
programming pattern known as <em>virtual types</em> through the example
of window managers.</p>
<h2 class="section" id="s:extended-bank-accounts"><a class="section-anchor" href="#s:extended-bank-accounts" aria-hidden="true"></a>1&nbsp;&nbsp;Extended example: bank accounts</h2>
<p>In this section, we illustrate most aspects of Object and inheritance
by refining, debugging, and specializing the following
initial naive definition of a simple bank account. (We reuse the
module <span class="c003">Euro</span> defined at the end of chapter&nbsp;<a href="objectexamples.html#c%3Aobjectexamples">3</a>.)


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> euro = <span class="ocamlkeyword">new</span> Euro.c;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> euro : float -&gt; Euro.c = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> zero = euro 0.;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> zero : Euro.c = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> neg x = x#times (-1.);;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> neg : &lt; times : float -&gt; 'a; .. &gt; -&gt; 'a = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> account =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance = zero
     <span class="ocamlkeyword">method</span> balance = balance
     <span class="ocamlkeyword">method</span> deposit x = balance &lt;- balance # plus x
     <span class="ocamlkeyword">method</span> withdraw x =
       <span class="ocamlkeyword">if</span> x#leq balance <span class="ocamlkeyword">then</span> (balance &lt;- balance # plus (neg x); x) <span class="ocamlkeyword">else</span> zero
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> account :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> c = <span class="ocamlkeyword">new</span> account <span class="ocamlkeyword">in</span> c # deposit (euro 100.); c # withdraw (euro 50.);;</div>



<div class="pre caml-output ok">- : Euro.c = &lt;obj&gt;</div></div>

</div><p>


We now refine this definition with a method to compute interest.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> account_with_interests =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> account
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> interest = self # deposit (self # balance # times 0.03)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> account_with_interests :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> interest : unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


We make the method <span class="c003">interest</span> private, since clearly it should not be
called freely from the outside. Here, it is only made accessible to subclasses
that will manage monthly or yearly updates of the account.</p><p>We should soon fix a bug in the current definition: the deposit method can
be used for withdrawing money by depositing negative amounts. We can
fix this directly:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> safe_account =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> account
     <span class="ocamlkeyword">method</span> deposit x = <span class="ocamlkeyword">if</span> zero#leq x <span class="ocamlkeyword">then</span> balance &lt;- balance#plus x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> safe_account :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


However, the bug might be fixed more safely by the following definition:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> safe_account =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> account <span class="ocamlkeyword">as</span> unsafe
     <span class="ocamlkeyword">method</span> deposit x =
       <span class="ocamlkeyword">if</span> zero#leq x <span class="ocamlkeyword">then</span> unsafe # deposit x
       <span class="ocamlkeyword">else</span> raise (Invalid_argument <span class="ocamlstring">"deposit"</span>)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> safe_account :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


In particular, this does not require the knowledge of the implementation of
the method <span class="c003">deposit</span>.</p><p>To keep track of operations, we extend the class with a mutable field
<span class="c003">history</span> and a private method <span class="c003">trace</span> to add an operation in the
log. Then each method to be traced is redefined.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> 'a operation = Deposit <span class="ocamlkeyword">of</span> 'a | Retrieval <span class="ocamlkeyword">of</span> 'a;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> 'a operation = Deposit <span class="ocamlkeyword">of</span> 'a | Retrieval <span class="ocamlkeyword">of</span> 'a</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> account_with_history =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> safe_account <span class="ocamlkeyword">as</span> super
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> history = []
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> trace x = history &lt;- x :: history
     <span class="ocamlkeyword">method</span> deposit x = self#trace (Deposit x);  super#deposit x
     <span class="ocamlkeyword">method</span> withdraw x = self#trace (Retrieval x); super#withdraw x
     <span class="ocamlkeyword">method</span> history = List.rev history
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> account_with_history :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> trace : Euro.c operation -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


One may wish to open an account and simultaneously deposit some initial
amount. Although the initial implementation did not address this
requirement, it can be achieved by using an initializer.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> account_with_deposit x =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> account_with_history
     <span class="ocamlkeyword">initializer</span> balance &lt;- x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> account_with_deposit :
  Euro.c -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> trace : Euro.c operation -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


A better alternative is:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> account_with_deposit x =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> account_with_history
     <span class="ocamlkeyword">initializer</span> self#deposit x
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> account_with_deposit :
  Euro.c -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance : Euro.c
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> balance : Euro.c
    <span class="ocamlkeyword">method</span> deposit : Euro.c -&gt; unit
    <span class="ocamlkeyword">method</span> history : Euro.c operation list
    <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> trace : Euro.c operation -&gt; unit
    <span class="ocamlkeyword">method</span> withdraw : Euro.c -&gt; Euro.c
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Indeed, the latter is safer since the call to <span class="c003">deposit</span> will automatically
benefit from safety checks and from the trace.
Let’s test it:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> ccp = <span class="ocamlkeyword">new</span> account_with_deposit (euro 100.) <span class="ocamlkeyword">in</span>
 <span class="ocamlkeyword">let</span> _balance = ccp#withdraw (euro 50.) <span class="ocamlkeyword">in</span>
 ccp#history;;</div>



<div class="pre caml-output ok">- : Euro.c operation list = [Deposit &lt;obj&gt;; Retrieval &lt;obj&gt;]</div></div>

</div><p>


Closing an account can be done with the following polymorphic function:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> close c = c#withdraw c#balance;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> close : &lt; balance : 'a; withdraw : 'a -&gt; 'b; .. &gt; -&gt; 'b = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>

</div><p>


Of course, this applies to all sorts of accounts.</p><p>Finally, we gather several versions of the account into a module <span class="c003">Account</span>
abstracted over some currency.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> today () = (01,01,2000) <span class="ocamlcomment">(* an approximation *)</span>
 <span class="ocamlkeyword">module</span> Account (M:MONEY) =
   <span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">type</span> m = M.c
     <span class="ocamlkeyword">let</span> m = <span class="ocamlkeyword">new</span> M.c
     <span class="ocamlkeyword">let</span> zero = m 0.

     <span class="ocamlkeyword">class</span> bank =
       <span class="ocamlkeyword">object</span> (self)
         <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> balance = zero
         <span class="ocamlkeyword">method</span> balance = balance
         <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> history = []
         <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> trace x = history &lt;- x::history
         <span class="ocamlkeyword">method</span> deposit x =
           self#trace (Deposit x);
           <span class="ocamlkeyword">if</span> zero#leq x <span class="ocamlkeyword">then</span> balance &lt;- balance # plus x
           <span class="ocamlkeyword">else</span> raise (Invalid_argument <span class="ocamlstring">"deposit"</span>)
         <span class="ocamlkeyword">method</span> withdraw x =
           <span class="ocamlkeyword">if</span> x#leq balance <span class="ocamlkeyword">then</span>
             (balance &lt;- balance # plus (neg x); self#trace (Retrieval x); x)
           <span class="ocamlkeyword">else</span> zero
         <span class="ocamlkeyword">method</span> history = List.rev history
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> client_view =
       <span class="ocamlkeyword">object</span>
         <span class="ocamlkeyword">method</span> deposit : m -&gt; unit
         <span class="ocamlkeyword">method</span> history : m operation list
         <span class="ocamlkeyword">method</span> withdraw : m -&gt; m
         <span class="ocamlkeyword">method</span> balance : m
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> check_client x =
       <span class="ocamlkeyword">let</span> y = <span class="ocamlkeyword">if</span> (m 100.)#leq x <span class="ocamlkeyword">then</span> x
       <span class="ocamlkeyword">else</span> raise (Failure <span class="ocamlstring">"Insufficient initial deposit"</span>) <span class="ocamlkeyword">in</span>
       <span class="ocamlkeyword">object</span> (self)
         <span class="ocamlkeyword">initializer</span> self#deposit y
         <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> deposit: m -&gt; unit
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">module</span> Client (B : <span class="ocamlkeyword">sig</span> <span class="ocamlkeyword">class</span> bank : client_view <span class="ocamlkeyword">end</span>) =
       <span class="ocamlkeyword">struct</span>
         <span class="ocamlkeyword">class</span> account x : client_view =
           <span class="ocamlkeyword">object</span>
             <span class="ocamlkeyword">inherit</span> B.bank
             <span class="ocamlkeyword">inherit</span> check_client x
           <span class="ocamlkeyword">end</span>

         <span class="ocamlkeyword">let</span> discount x =
           <span class="ocamlkeyword">let</span> c = <span class="ocamlkeyword">new</span> account x <span class="ocamlkeyword">in</span>
           <span class="ocamlkeyword">if</span> today() &lt; (1998,10,30) <span class="ocamlkeyword">then</span> c # deposit (m 100.); c
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>

</div><p>


This shows the use of modules to group several class definitions that can in
fact be thought of as a single unit. This unit would be provided by a bank
for both internal and external uses.
This is implemented as a functor that abstracts over the currency so that
the same code can be used to provide accounts in different currencies.</p><p>The class <span class="c003">bank</span> is the <em>real</em> implementation of the bank account (it
could have been inlined). This is the one that will be used for further
extensions, refinements, etc. Conversely, the client will only be given the client view.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Euro_account = Account(Euro);;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Client = Euro_account.Client (Euro_account);;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">new</span> Client.account (<span class="ocamlkeyword">new</span> Euro.c 100.);;</div></div>

</div><p>


Hence, the clients do not have direct access to the <span class="c003">balance</span>, nor the
<span class="c003">history</span> of their own accounts. Their only way to change their balance is
to deposit or withdraw money. It is important to give the clients
a class and not just the ability to create accounts (such as the
promotional <span class="c003">discount</span> account), so that they can
personalize their account.
For instance, a client may refine the <span class="c003">deposit</span> and <span class="c003">withdraw</span> methods
so as to do his own financial bookkeeping, automatically. On the
other hand, the function <span class="c003">discount</span> is given as such, with no
possibility for further personalization.</p><p>It is important to provide the client’s view as a functor
<span class="c003">Client</span> so that client accounts can still be built after a possible
specialization of the <span class="c003">bank</span>.
The functor <span class="c003">Client</span> may remain unchanged and be passed
the new definition to initialize a client’s view of the extended account.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Investment_account (M : MONEY) =
   <span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">type</span> m = M.c
     <span class="ocamlkeyword">module</span> A = Account(M)

     <span class="ocamlkeyword">class</span> bank =
       <span class="ocamlkeyword">object</span>
         <span class="ocamlkeyword">inherit</span> A.bank <span class="ocamlkeyword">as</span> super
         <span class="ocamlkeyword">method</span> deposit x =
           <span class="ocamlkeyword">if</span> (<span class="ocamlkeyword">new</span> M.c 1000.)#leq x <span class="ocamlkeyword">then</span>
             print_string <span class="ocamlstring">"Would you like to invest?"</span>;
           super#deposit x
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">module</span> Client = A.Client
   <span class="ocamlkeyword">end</span>;;</div></div>

</div><p>


The functor <span class="c003">Client</span> may also be redefined when some new features of the
account can be given to the client.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Internet_account (M : MONEY) =
   <span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">type</span> m = M.c
     <span class="ocamlkeyword">module</span> A = Account(M)

     <span class="ocamlkeyword">class</span> bank =
       <span class="ocamlkeyword">object</span>
         <span class="ocamlkeyword">inherit</span> A.bank
         <span class="ocamlkeyword">method</span> mail s = print_string s
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> client_view =
       <span class="ocamlkeyword">object</span>
         <span class="ocamlkeyword">method</span> deposit : m -&gt; unit
         <span class="ocamlkeyword">method</span> history : m operation list
         <span class="ocamlkeyword">method</span> withdraw : m -&gt; m
         <span class="ocamlkeyword">method</span> balance : m
         <span class="ocamlkeyword">method</span> mail : string -&gt; unit
       <span class="ocamlkeyword">end</span>

     <span class="ocamlkeyword">module</span> Client (B : <span class="ocamlkeyword">sig</span> <span class="ocamlkeyword">class</span> bank : client_view <span class="ocamlkeyword">end</span>) =
       <span class="ocamlkeyword">struct</span>
         <span class="ocamlkeyword">class</span> account x : client_view =
           <span class="ocamlkeyword">object</span>
             <span class="ocamlkeyword">inherit</span> B.bank
             <span class="ocamlkeyword">inherit</span> A.check_client x
           <span class="ocamlkeyword">end</span>
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>

</div>
<h2 class="section" id="s:modules-as-classes"><a class="section-anchor" href="#s:modules-as-classes" aria-hidden="true">﻿</a>2&nbsp;&nbsp;Simple modules as classes</h2>
<p>One may wonder whether it is possible to treat primitive types such as
integers and strings as objects. Although this is usually uninteresting
for integers or strings, there may be some situations where
this is desirable. The class <span class="c003">money</span> above is such an example.
We show here how to do it for strings.</p>
<h3 class="subsection" id="ss:string-as-class"><a class="section-anchor" href="#ss:string-as-class" aria-hidden="true">﻿</a>2.1&nbsp;&nbsp;Strings</h3>
<p>A naive definition of strings as objects could be:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ostring s =
   <span class="ocamlkeyword">object</span>
      <span class="ocamlkeyword">method</span> get n = String.get s n
      <span class="ocamlkeyword">method</span> print = print_string s
      <span class="ocamlkeyword">method</span> escaped = <span class="ocamlkeyword">new</span> ostring (String.escaped s)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ostring :
  string -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">method</span> escaped : ostring
    <span class="ocamlkeyword">method</span> get : int -&gt; char
    <span class="ocamlkeyword">method</span> print : unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


However, the method <span class="c003">escaped</span> returns an object of the class <span class="c003">ostring</span>,
and not an object of the current class. Hence, if the class is further
extended, the method <span class="c003">escaped</span> will only return an object of the parent
class.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> sub_string s =
   <span class="ocamlkeyword">object</span>
      <span class="ocamlkeyword">inherit</span> ostring s
      <span class="ocamlkeyword">method</span> sub start len = <span class="ocamlkeyword">new</span> sub_string (String.sub s  start len)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> sub_string :
  string -&gt;
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">method</span> escaped : ostring
    <span class="ocamlkeyword">method</span> get : int -&gt; char
    <span class="ocamlkeyword">method</span> print : unit
    <span class="ocamlkeyword">method</span> sub : int -&gt; int -&gt; sub_string
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


As seen in section&nbsp;<a href="objectexamples.html#s%3Abinary-methods">3.16</a>, the solution is to use
functional update instead. We need to create an instance variable
containing the representation <span class="c003">s</span> of the string.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> better_string s =
   <span class="ocamlkeyword">object</span>
      <span class="ocamlkeyword">val</span> repr = s
      <span class="ocamlkeyword">method</span> get n = String.get repr n
      <span class="ocamlkeyword">method</span> print = print_string repr
      <span class="ocamlkeyword">method</span> escaped = {&lt; repr = String.escaped repr &gt;}
      <span class="ocamlkeyword">method</span> sub start len = {&lt; repr = String.sub s start len &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> better_string :
  string -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : string
    <span class="ocamlkeyword">method</span> escaped : 'a
    <span class="ocamlkeyword">method</span> get : int -&gt; char
    <span class="ocamlkeyword">method</span> print : unit
    <span class="ocamlkeyword">method</span> sub : int -&gt; int -&gt; 'a
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


As shown in the inferred type, the methods <span class="c003">escaped</span> and <span class="c003">sub</span> now return
objects of the same type as the one of the class.</p><p>Another difficulty is the implementation of the method <span class="c003">concat</span>.
In order to concatenate a string with another string of the same class,
one must be able to access the instance variable externally. Thus, a method
<span class="c003">repr</span> returning s must be defined. Here is the correct definition of
strings:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ostring s =
   <span class="ocamlkeyword">object</span> (self : 'mytype)
      <span class="ocamlkeyword">val</span> repr = s
      <span class="ocamlkeyword">method</span> repr = repr
      <span class="ocamlkeyword">method</span> get n = String.get repr n
      <span class="ocamlkeyword">method</span> print = print_string repr
      <span class="ocamlkeyword">method</span> escaped = {&lt; repr = String.escaped repr &gt;}
      <span class="ocamlkeyword">method</span> sub start len = {&lt; repr = String.sub s start len &gt;}
      <span class="ocamlkeyword">method</span> concat (t : 'mytype) = {&lt; repr = repr ^ t#repr &gt;}
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ostring :
  string -&gt;
  <span class="ocamlkeyword">object</span> ('a)
    <span class="ocamlkeyword">val</span> repr : string
    <span class="ocamlkeyword">method</span> concat : 'a -&gt; 'a
    <span class="ocamlkeyword">method</span> escaped : 'a
    <span class="ocamlkeyword">method</span> get : int -&gt; char
    <span class="ocamlkeyword">method</span> print : unit
    <span class="ocamlkeyword">method</span> repr : string
    <span class="ocamlkeyword">method</span> sub : int -&gt; int -&gt; 'a
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


Another constructor of the class string can be defined to return a new
string of a given length:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> cstring n = ostring (String.make n ' ');;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> cstring : int -&gt; ostring</div></div>

</div><p>


Here, exposing the representation of strings is probably harmless. We do
could also hide the representation of strings as we hid the currency in the
class <span class="c003">money</span> of section&nbsp;<a href="objectexamples.html#s%3Afriends">3.17</a>.</p>
<h4 class="subsubsection" id="sss:stack-as-class"><a class="section-anchor" href="#sss:stack-as-class" aria-hidden="true">﻿</a>Stacks</h4>
<p>There is sometimes an alternative between using modules or classes for
parametric data types.
Indeed, there are situations when the two approaches are quite similar.
For instance, a stack can be straightforwardly implemented as a class:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">exception</span> Empty;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">exception</span> Empty</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] stack =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> l = ([] : 'a list)
     <span class="ocamlkeyword">method</span> push x = l &lt;- x::l
     <span class="ocamlkeyword">method</span> pop = <span class="ocamlkeyword">match</span> l <span class="ocamlkeyword">with</span> [] -&gt; raise Empty | a::l' -&gt; l &lt;- l'; a
     <span class="ocamlkeyword">method</span> clear = l &lt;- []
     <span class="ocamlkeyword">method</span> length = List.length l
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] stack :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> l : 'a list
    <span class="ocamlkeyword">method</span> clear : unit
    <span class="ocamlkeyword">method</span> length : int
    <span class="ocamlkeyword">method</span> pop : 'a
    <span class="ocamlkeyword">method</span> push : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


However, writing a method for iterating over a stack is more
problematic. A method <span class="c003">fold</span> would have type
<span class="c003">('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b</span>. Here <span class="c003">'a</span> is the parameter of the stack.
The parameter <span class="c003">'b</span> is not related to the class <span class="c003">'a stack</span> but to the
argument that will be passed to the method <span class="c003">fold</span>.
A naive approach is to make <span class="c003">'b</span> an extra parameter of class <span class="c003">stack</span>:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a, 'b] stack2 =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> ['a] stack
     <span class="ocamlkeyword">method</span> fold f (x : 'b) = List.fold_left f x l
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a, 'b] stack2 :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> l : 'a list
    <span class="ocamlkeyword">method</span> clear : unit
    <span class="ocamlkeyword">method</span> fold : ('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b
    <span class="ocamlkeyword">method</span> length : int
    <span class="ocamlkeyword">method</span> pop : 'a
    <span class="ocamlkeyword">method</span> push : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


However, the method <span class="c003">fold</span> of a given object can only be
applied to functions that all have the same type:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> s = <span class="ocamlkeyword">new</span> stack2;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> s : ('_weak1, '_weak2) stack2 = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> s#fold ( + ) 0;;</div>



<div class="pre caml-output ok">- : int = 0</div></div>
<div class="ocaml">



<div class="pre caml-input"> s;;</div>



<div class="pre caml-output ok">- : (int, int) stack2 = &lt;obj&gt;</div></div>

</div><p>


A better solution is to use polymorphic methods, which were
introduced in OCaml version 3.05. Polymorphic methods makes
it possible to treat the type variable <span class="c003">'b</span> in the type of <span class="c003">fold</span> as
universally quantified, giving <span class="c003">fold</span> the polymorphic type
<span class="c003">Forall 'b. ('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b</span>.
An explicit type declaration on the method <span class="c003">fold</span> is required, since
the type checker cannot infer the polymorphic type by itself.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a] stack3 =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> ['a] stack
     <span class="ocamlkeyword">method</span> fold : 'b. ('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b
                 = <span class="ocamlkeyword">fun</span> f x -&gt; List.fold_left f x l
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] stack3 :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> l : 'a list
    <span class="ocamlkeyword">method</span> clear : unit
    <span class="ocamlkeyword">method</span> fold : ('b -&gt; 'a -&gt; 'b) -&gt; 'b -&gt; 'b
    <span class="ocamlkeyword">method</span> length : int
    <span class="ocamlkeyword">method</span> pop : 'a
    <span class="ocamlkeyword">method</span> push : 'a -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div>
<h3 class="subsection" id="ss:hashtbl-as-class"><a class="section-anchor" href="#ss:hashtbl-as-class" aria-hidden="true">﻿</a>2.2&nbsp;&nbsp;Hashtbl</h3>
<p>A simplified version of object-oriented hash tables should have the
following class type.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> ['a, 'b] hash_table =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> find : 'a -&gt; 'b
     <span class="ocamlkeyword">method</span> add : 'a -&gt; 'b -&gt; unit
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">type</span> ['a, 'b] hash_table =
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> add : 'a -&gt; 'b -&gt; unit <span class="ocamlkeyword">method</span> find : 'a -&gt; 'b <span class="ocamlkeyword">end</span></div></div>

</div><p>


A simple implementation, which is quite reasonable for small hash tables is
to use an association list:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a, 'b] small_hashtbl : ['a, 'b] hash_table =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> table = []
     <span class="ocamlkeyword">method</span> find key = List.assoc key table
     <span class="ocamlkeyword">method</span> add key valeur = table &lt;- (key, valeur) :: table
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a, 'b] small_hashtbl : ['a, 'b] hash_table</div></div>

</div><p>


A better implementation, and one that scales up better, is to use a
true hash table… whose elements are small hash tables!


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['a, 'b] hashtbl size : ['a, 'b] hash_table =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">val</span> table = Array.init size (<span class="ocamlkeyword">fun</span> i -&gt; <span class="ocamlkeyword">new</span> small_hashtbl)
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">private</span> hash key =
       (Hashtbl.hash key) <span class="ocamlkeyword">mod</span> (Array.length table)
     <span class="ocamlkeyword">method</span> find key = table.(self#hash key) # find key
     <span class="ocamlkeyword">method</span> add key = table.(self#hash key) # add key
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a, 'b] hashtbl : int -&gt; ['a, 'b] hash_table</div></div>

</div>
<h3 class="subsection" id="ss:set-as-class"><a class="section-anchor" href="#ss:set-as-class" aria-hidden="true">﻿</a>2.3&nbsp;&nbsp;Sets</h3>
<p>Implementing sets leads to another difficulty. Indeed, the method
<span class="c003">union</span> needs to be able to access the internal representation of
another object of the same class.</p><p>This is another instance of friend functions as seen in
section&nbsp;<a href="objectexamples.html#s%3Afriends">3.17</a>. Indeed, this is the same mechanism used in the module
<span class="c003">Set</span> in the absence of objects.</p><p>In the object-oriented version of sets, we only need to add an additional
method <span class="c003">tag</span> to return the representation of a set. Since sets are
parametric in the type of elements, the method <span class="c003">tag</span> has a parametric type
<span class="c003">'a tag</span>, concrete within
the module definition but abstract in its signature.
From outside, it will then be guaranteed that two objects with a method <span class="c003">tag</span>
of the same type will share the same representation.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> <span class="ocamlkeyword">type</span> SET =
   <span class="ocamlkeyword">sig</span>
     <span class="ocamlkeyword">type</span> 'a tag
     <span class="ocamlkeyword">class</span> ['a] c :
       <span class="ocamlkeyword">object</span> ('b)
         <span class="ocamlkeyword">method</span> is_empty : bool
         <span class="ocamlkeyword">method</span> mem : 'a -&gt; bool
         <span class="ocamlkeyword">method</span> add : 'a -&gt; 'b
         <span class="ocamlkeyword">method</span> union : 'b -&gt; 'b
         <span class="ocamlkeyword">method</span> iter : ('a -&gt; unit) -&gt; unit
         <span class="ocamlkeyword">method</span> tag : 'a tag
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">module</span> Set : SET =
   <span class="ocamlkeyword">struct</span>
     <span class="ocamlkeyword">let</span> <span class="ocamlkeyword">rec</span> merge l1 l2 =
       <span class="ocamlkeyword">match</span> l1 <span class="ocamlkeyword">with</span>
         [] -&gt; l2
       | h1 :: t1 -&gt;
           <span class="ocamlkeyword">match</span> l2 <span class="ocamlkeyword">with</span>
             [] -&gt; l1
           | h2 :: t2 -&gt;
               <span class="ocamlkeyword">if</span> h1 &lt; h2 <span class="ocamlkeyword">then</span> h1 :: merge t1 l2
               <span class="ocamlkeyword">else</span> <span class="ocamlkeyword">if</span> h1 &gt; h2 <span class="ocamlkeyword">then</span> h2 :: merge l1 t2
               <span class="ocamlkeyword">else</span> merge t1 l2
     <span class="ocamlkeyword">type</span> 'a tag = 'a list
     <span class="ocamlkeyword">class</span> ['a] c =
       <span class="ocamlkeyword">object</span> (_ : 'b)
         <span class="ocamlkeyword">val</span> repr = ([] : 'a list)
         <span class="ocamlkeyword">method</span> is_empty = (repr = [])
         <span class="ocamlkeyword">method</span> mem x = List.exists (( = ) x) repr
         <span class="ocamlkeyword">method</span> add x = {&lt; repr = merge [x] repr &gt;}
         <span class="ocamlkeyword">method</span> union (s : 'b) = {&lt; repr = merge repr s#tag &gt;}
         <span class="ocamlkeyword">method</span> iter (f : 'a -&gt; unit) = List.iter f repr
         <span class="ocamlkeyword">method</span> tag = repr
       <span class="ocamlkeyword">end</span>
   <span class="ocamlkeyword">end</span>;;</div></div>

</div>
<h2 class="section" id="s:subject-observer"><a class="section-anchor" href="#s:subject-observer" aria-hidden="true">﻿</a>3&nbsp;&nbsp;The subject/observer pattern</h2>
<p>The following example, known as the subject/observer pattern, is often
presented in the literature as a difficult inheritance problem with
inter-connected classes.
The general pattern amounts to the definition a pair of two
classes that recursively interact with one another.</p><p>The class <span class="c003">observer</span> has a distinguished method <span class="c003">notify</span> that requires
two arguments, a subject and an event to execute an action.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> ['subject, 'event] observer =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> notify : 'subject -&gt;  'event -&gt; unit
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> <span class="ocamlkeyword">virtual</span> ['subject, 'event] observer :
  <span class="ocamlkeyword">object</span> <span class="ocamlkeyword">method</span> <span class="ocamlkeyword">virtual</span> notify : 'subject -&gt; 'event -&gt; unit <span class="ocamlkeyword">end</span></div></div>

</div><p>


The class <span class="c003">subject</span> remembers a list of observers in an instance variable,
and has a distinguished method <span class="c003">notify_observers</span> to broadcast the message
<span class="c003">notify</span> to all observers with a particular event <span class="c003">e</span>.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['observer, 'event] subject =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> observers = ([]:'observer list)
     <span class="ocamlkeyword">method</span> add_observer obs = observers &lt;- (obs :: observers)
     <span class="ocamlkeyword">method</span> notify_observers (e : 'event) =
         List.iter (<span class="ocamlkeyword">fun</span> x -&gt; x#notify self e) observers
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a, 'event] subject :
  <span class="ocamlkeyword">object</span> ('b)
    <span class="ocamlkeyword">constraint</span> 'a = &lt; notify : 'b -&gt; 'event -&gt; unit; .. &gt;
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> observers : 'a list
    <span class="ocamlkeyword">method</span> add_observer : 'a -&gt; unit
    <span class="ocamlkeyword">method</span> notify_observers : 'event -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


The difficulty usually lies in defining instances of the pattern above
by inheritance. This can be done in a natural and obvious manner in
OCaml, as shown on the following example manipulating windows.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">type</span> event = Raise | Resize | Move;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">type</span> event = Raise | Resize | Move</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> string_of_event = <span class="ocamlkeyword">function</span>
     Raise -&gt; <span class="ocamlstring">"Raise"</span> | Resize -&gt; <span class="ocamlstring">"Resize"</span> | Move -&gt; <span class="ocamlstring">"Move"</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> string_of_event : event -&gt; string = &lt;<span class="ocamlkeyword">fun</span>&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> count = <span class="ocamlkeyword">ref</span> 0;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> count : int <span class="ocamlkeyword">ref</span> = {contents = 0}</div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['observer] window_subject =
   <span class="ocamlkeyword">let</span> id = count := succ !count; !count <span class="ocamlkeyword">in</span>
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> ['observer, event] subject
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> position = 0
     <span class="ocamlkeyword">method</span> identity = id
     <span class="ocamlkeyword">method</span> move x = position &lt;- position + x; self#notify_observers Move
     <span class="ocamlkeyword">method</span> draw = Printf.printf <span class="ocamlstring">"{Position = %d}\n"</span>  position;
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] window_subject :
  <span class="ocamlkeyword">object</span> ('b)
    <span class="ocamlkeyword">constraint</span> 'a = &lt; notify : 'b -&gt; event -&gt; unit; .. &gt;
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> observers : 'a list
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> position : int
    <span class="ocamlkeyword">method</span> add_observer : 'a -&gt; unit
    <span class="ocamlkeyword">method</span> draw : unit
    <span class="ocamlkeyword">method</span> identity : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> notify_observers : event -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['subject] window_observer =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> ['subject, event] observer
     <span class="ocamlkeyword">method</span> notify s e = s#draw
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] window_observer :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = &lt; draw : unit; .. &gt;
    <span class="ocamlkeyword">method</span> notify : 'a -&gt; event -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


As can be expected, the type of <span class="c003">window</span> is recursive.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> window = <span class="ocamlkeyword">new</span> window_subject;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> window : &lt; notify : 'a -&gt; event -&gt; unit; _.. &gt; window_subject <span class="ocamlkeyword">as</span> 'a =
  &lt;obj&gt;</div></div>

</div><p>


However, the two classes of <span class="c003">window_subject</span> and <span class="c003">window_observer</span> are not
mutually recursive.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> window_observer = <span class="ocamlkeyword">new</span> window_observer;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> window_observer : &lt; draw : unit; _.. &gt; window_observer = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> window#add_observer window_observer;;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> window#move 1;;</div>



<div class="pre caml-output ok">{Position = 1}
- : unit = ()</div></div>

</div><p>Classes <span class="c003">window_observer</span> and <span class="c003">window_subject</span> can still be extended by
inheritance. For instance, one may enrich the <span class="c003">subject</span> with new
behaviors and refine the behavior of the observer.


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['observer] richer_window_subject =
   <span class="ocamlkeyword">object</span> (self)
     <span class="ocamlkeyword">inherit</span> ['observer] window_subject
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> size = 1
     <span class="ocamlkeyword">method</span> resize x = size &lt;- size + x; self#notify_observers Resize
     <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> top = <span class="ocamlkeyword">false</span>
     <span class="ocamlkeyword">method</span> raise = top &lt;- <span class="ocamlkeyword">true</span>; self#notify_observers Raise
     <span class="ocamlkeyword">method</span> draw = Printf.printf <span class="ocamlstring">"{Position = %d; Size = %d}\n"</span>  position size;
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] richer_window_subject :
  <span class="ocamlkeyword">object</span> ('b)
    <span class="ocamlkeyword">constraint</span> 'a = &lt; notify : 'b -&gt; event -&gt; unit; .. &gt;
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> observers : 'a list
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> position : int
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> size : int
    <span class="ocamlkeyword">val</span> <span class="ocamlkeyword">mutable</span> top : bool
    <span class="ocamlkeyword">method</span> add_observer : 'a -&gt; unit
    <span class="ocamlkeyword">method</span> draw : unit
    <span class="ocamlkeyword">method</span> identity : int
    <span class="ocamlkeyword">method</span> move : int -&gt; unit
    <span class="ocamlkeyword">method</span> notify_observers : event -&gt; unit
    <span class="ocamlkeyword">method</span> raise : unit
    <span class="ocamlkeyword">method</span> resize : int -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>
<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['subject] richer_window_observer =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> ['subject] window_observer <span class="ocamlkeyword">as</span> super
     <span class="ocamlkeyword">method</span> notify s e = <span class="ocamlkeyword">if</span> e &lt;&gt; Raise <span class="ocamlkeyword">then</span> s#raise; super#notify s e
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] richer_window_observer :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = &lt; draw : unit; raise : unit; .. &gt;
    <span class="ocamlkeyword">method</span> notify : 'a -&gt; event -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


We can also create a different kind of observer:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">class</span> ['subject] trace_observer =
   <span class="ocamlkeyword">object</span>
     <span class="ocamlkeyword">inherit</span> ['subject, event] observer
     <span class="ocamlkeyword">method</span> notify s e =
       Printf.printf
         <span class="ocamlstring">"&lt;Window %d &lt;== %s&gt;\n"</span> s#identity (string_of_event e)
   <span class="ocamlkeyword">end</span>;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">class</span> ['a] trace_observer :
  <span class="ocamlkeyword">object</span>
    <span class="ocamlkeyword">constraint</span> 'a = &lt; identity : int; .. &gt;
    <span class="ocamlkeyword">method</span> notify : 'a -&gt; event -&gt; unit
  <span class="ocamlkeyword">end</span></div></div>

</div><p>


and attach several observers to the same object:


</p><div class="caml-example toplevel">

<div class="ocaml">



<div class="pre caml-input"> <span class="ocamlkeyword">let</span> window = <span class="ocamlkeyword">new</span> richer_window_subject;;</div>



<div class="pre caml-output ok"><span class="ocamlkeyword">val</span> window :
  &lt; notify : 'a -&gt; event -&gt; unit; _.. &gt; richer_window_subject <span class="ocamlkeyword">as</span> 'a = &lt;obj&gt;</div></div>
<div class="ocaml">



<div class="pre caml-input"> window#add_observer (<span class="ocamlkeyword">new</span> richer_window_observer);;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> window#add_observer (<span class="ocamlkeyword">new</span> trace_observer);;</div>



<div class="pre caml-output ok">- : unit = ()</div></div>
<div class="ocaml">



<div class="pre caml-input"> window#move 1; window#resize 2;;</div>



<div class="pre caml-output ok">&lt;Window 1 &lt;== Move&gt;
&lt;Window 1 &lt;== Raise&gt;
{Position = 1; Size = 1}
{Position = 1; Size = 1}
&lt;Window 1 &lt;== Resize&gt;
&lt;Window 1 &lt;== Raise&gt;
{Position = 1; Size = 3}
{Position = 1; Size = 3}
- : unit = ()</div></div>

</div>
<hr>





<span class="authors c009">(Chapter written by Didier Rémy)</span><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>