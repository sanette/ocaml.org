<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="comp.html">Batch compilation (ocamlc)</a></li><li><a href="toplevel.html">The toplevel system or REPL (ocaml)</a></li><li><a href="runtime.html">The runtime system (ocamlrun)</a></li><li><a href="native.html">Native-code compilation (ocamlopt)</a></li><li><a href="lexyacc.html">Lexer and parser generators (ocamllex, ocamlyacc)</a></li><li><a href="depend.html">Dependency generator (ocamldep)</a></li><li><a href="browser.html">The browser/editor (ocamlbrowser)</a></li><li><a href="ocamldoc.html">The documentation generator (ocamldoc)</a></li><li><a href="debugger.html">The debugger (ocamldebug)</a></li><li><a href="profil.html">Profiling (ocamlprof)</a></li><li><a href="manual057.html">The ocamlbuild compilation manager</a></li><li><a href="intfc.html">Interfacing C with OCaml</a></li><li class="active"><a href="flambda.html">Optimisation with Flambda</a></li><li><a href="spacetime.html">Memory profiling with Spacetime</a></li><li><a href="afl-fuzz.html">Fuzzing with afl-fuzz</a></li></ul>




<h1 class="chapter" id="sec487"><span>Chapter 21</span>&nbsp;&nbsp;Optimisation with Flambda</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.09</a></div><div class="toc_title"><a href="#">Optimisation with Flambda</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="flambda.html#sec488">1&nbsp;&nbsp;Overview</a>
</li><li><a href="flambda.html#sec489">2&nbsp;&nbsp;Command-line flags</a>
</li><li><a href="flambda.html#sec492">3&nbsp;&nbsp;Inlining</a>
</li><li><a href="flambda.html#sec503">4&nbsp;&nbsp;Specialisation</a>
</li><li><a href="flambda.html#sec507">5&nbsp;&nbsp;Default settings of parameters</a>
</li><li><a href="flambda.html#sec510">6&nbsp;&nbsp;Manual control of inlining and specialisation</a>
</li><li><a href="flambda.html#sec512">7&nbsp;&nbsp;Simplification</a>
</li><li><a href="flambda.html#sec513">8&nbsp;&nbsp;Other code motion transformations</a>
</li><li><a href="flambda.html#sec517">9&nbsp;&nbsp;Unboxing transformations</a>
</li><li><a href="flambda.html#sec525">10&nbsp;&nbsp;Removal of unused code and values</a>
</li><li><a href="flambda.html#sec530">11&nbsp;&nbsp;Other code transformations</a>
</li><li><a href="flambda.html#sec533">12&nbsp;&nbsp;Treatment of effects</a>
</li><li><a href="flambda.html#sec534">13&nbsp;&nbsp;Compilation of statically-allocated modules</a>
</li><li><a href="flambda.html#sec535">14&nbsp;&nbsp;Inhibition of optimisation</a>
</li><li><a href="flambda.html#sec536">15&nbsp;&nbsp;Use of unsafe operations</a>
</li><li><a href="flambda.html#sec537">16&nbsp;&nbsp;Glossary</a>
</li></ul></nav></header>

<h2 class="section" id="sec488">1&nbsp;&nbsp;Overview</h2>
<p><em>Flambda</em> is the term used to describe a series of optimisation passes
provided by the native code compilers as of OCaml 4.03.</p><p>Flambda aims to make it easier to write idiomatic OCaml code without
incurring performance penalties.</p><p>To use the Flambda optimisers it is necessary to pass the <span class="c003">-flambda</span>
option to the OCaml <span class="c003">configure</span> script. (There is no support for a
single compiler that can operate in both Flambda and non-Flambda modes.)
Code compiled with Flambda
cannot be linked into the same program as code compiled without Flambda.
Attempting to do this will result in a compiler error.</p><p>Whether or not a particular <span class="c003">ocamlopt</span> uses Flambda may be
determined by invoking it with the <span class="c003">-config</span> option and looking
for any line starting with “<span class="c003">flambda:</span>”. If such a line is present
and says “<span class="c003">true</span>”, then Flambda is supported, otherwise it is not.</p><p>Flambda provides full optimisation across different compilation units,
so long as the <span class="c003">.cmx</span> files for the dependencies of the unit currently
being compiled are available. (A compilation unit corresponds to a
single <span class="c003">.ml</span> source file.) However it does not yet act entirely as
a whole-program compiler: for example, elimination of dead code across
a complete set of compilation units is not supported.</p><p>Optimisation with Flambda is not currently supported when generating
bytecode.</p><p>Flambda should not in general affect the semantics of existing programs.
Two exceptions to this rule are: possible elimination of pure code
that is being benchmarked (see section <a href="#inhibition">21.14</a>) and changes in
behaviour of code using unsafe operations (see section <a href="#unsafe">21.15</a>).</p><p>Flambda does not yet optimise array or string bounds checks. Neither
does it take hints for optimisation from any assertions written by the
user in the code.</p><p>Consult the <em>Glossary</em> at the end of this chapter for definitions of
technical terms used below.</p>
<h2 class="section" id="sec489">2&nbsp;&nbsp;Command-line flags</h2>
<p>The Flambda optimisers provide a variety of command-line flags that may
be used to control their behaviour. Detailed descriptions of each flag
are given in the referenced sections. Those sections also describe any
arguments which the particular flags take.</p><p>Commonly-used options:
</p><dl class="description"><dt class="dt-description">
<span class="c006">-O2</span></dt><dd class="dd-description"> Perform more optimisation than usual. Compilation
times may be lengthened. (This flag is an abbreviation for a certain
set of parameters described in section <a href="#defaults">21.5</a>.)
</dd><dt class="dt-description"><span class="c006">-O3</span></dt><dd class="dd-description"> Perform even more optimisation than usual, possibly
including unrolling of recursive functions. Compilation times may be
significantly lengthened.
</dd><dt class="dt-description"><span class="c006">-Oclassic</span></dt><dd class="dd-description"> Make inlining decisions at the point of
definition of a function rather than at the call site(s). This mirrors
the behaviour of OCaml compilers not using Flambda. Compared to compilation
using the new Flambda inlining heuristics (for example at <span class="c003">-O2</span>) it
produces
smaller <span class="c003">.cmx</span> files, shorter compilation times and code that probably
runs rather slower. When using <span class="c003">-Oclassic</span>, only the following options
described in this section are relevant: <span class="c003">-inlining-report</span> and
<span class="c003">-inline</span>. If any other of the options described in this section are
used, the behaviour is undefined and may cause an error in future versions
of the compiler.
</dd><dt class="dt-description"><span class="c006">-inlining-report</span></dt><dd class="dd-description"> Emit <span class="c003">.inlining</span> files (one per
round of optimisation) showing all of the inliner’s decisions.
</dd></dl><p>Less commonly-used options:
</p><dl class="description"><dt class="dt-description">
<span class="c006">-remove-unused-arguments</span></dt><dd class="dd-description"> Remove unused function arguments
even when the argument is not specialised. This may have a small
performance penalty.
See section <a href="#remove-unused-args">21.10.3</a>.
</dd><dt class="dt-description"><span class="c006">-unbox-closures</span></dt><dd class="dd-description"> Pass free variables via specialised arguments
rather than closures (an optimisation for reducing allocation). See
section <a href="#unbox-closures">21.9.3</a>. This may have a small performance penalty.
</dd></dl><p>Advanced options, only needed for detailed tuning:
</p><dl class="description"><dt class="dt-description">
<span class="c006">-inline</span></dt><dd class="dd-description"> The behaviour depends on whether <span class="c003">-Oclassic</span>
is used.
<ul class="itemize"><li class="li-itemize">
When not in <span class="c003">-Oclassic</span> mode, <span class="c003">-inline</span> limits the total
size of functions considered for inlining during any speculative inlining
search. (See section <a href="#speculation">21.3.6</a>.) Note that 
this parameter does
<span class="c013">not</span> control the assessment as to whether any particular function may
be inlined. Raising it to excessive amounts will not necessarily cause
more functions to be inlined.
</li><li class="li-itemize">When in <span class="c003">-Oclassic</span> mode, <span class="c003">-inline</span> behaves as in
previous versions of the compiler: it is the maximum size of function to
be considered for inlining. See section <a href="#classic">21.3.1</a>.
</li></ul>
</dd><dt class="dt-description"><span class="c006">-inline-toplevel</span></dt><dd class="dd-description"> The equivalent of <span class="c003">-inline</span> but used
when speculative inlining starts at toplevel. See
section <a href="#speculation">21.3.6</a>.
Not used in <span class="c003">-Oclassic</span> mode.
</dd><dt class="dt-description"><span class="c006">-inline-branch-factor</span></dt><dd class="dd-description"> Controls how the inliner assesses
whether a code path is likely to be hot or cold. See
section <a href="#assessment-inlining">21.3.5</a>.
</dd><dt class="dt-description"><span class="c006">-inline-alloc-cost,
-inline-branch-cost,
-inline-call-cost</span></dt><dd class="dd-description"> Controls how the inliner assesses the runtime
performance penalties associated with various operations. See
section <a href="#assessment-inlining">21.3.5</a>.
</dd><dt class="dt-description"><span class="c006">-inline-indirect-cost,
-inline-prim-cost</span></dt><dd class="dd-description"> Likewise.
</dd><dt class="dt-description"><span class="c006">-inline-lifting-benefit</span></dt><dd class="dd-description"> Controls inlining of functors
at toplevel. See section <a href="#assessment-inlining">21.3.5</a>.
</dd><dt class="dt-description"><span class="c006">-inline-max-depth</span></dt><dd class="dd-description"> The maximum depth of any
speculative inlining search. See section <a href="#speculation">21.3.6</a>.
</dd><dt class="dt-description"><span class="c006">-inline-max-unroll</span></dt><dd class="dd-description"> The maximum depth of any unrolling of
recursive functions during any speculative inlining search.
See section <a href="#speculation">21.3.6</a>.
</dd><dt class="dt-description"><span class="c006">-no-unbox-free-vars-of-closures</span></dt><dd class="dd-description"> Do not unbox closure variables. See section <a href="#unbox-fvs">21.9.1</a>.
</dd><dt class="dt-description"><span class="c006">-no-unbox-specialised-args</span></dt><dd class="dd-description"> Do not unbox arguments to which functions have been specialised. See
section <a href="#unbox-spec-args">21.9.2</a>.
</dd><dt class="dt-description"><span class="c006">-rounds</span></dt><dd class="dd-description"> How many rounds of optimisation to perform.
See section <a href="#rounds">21.2.1</a>.
</dd><dt class="dt-description"><span class="c006">-unbox-closures-factor</span></dt><dd class="dd-description"> Scaling factor for benefit
calculation when using <span class="c003">-unbox-closures</span>. See
section <a href="#unbox-closures">21.9.3</a>.
</dd></dl>
<h5 class="paragraph" id="sec490">Notes</h5>
<ul class="itemize"><li class="li-itemize">
The set of command line flags relating to optimisation should typically
be specified to be the same across an entire project. Flambda does not
currently record the requested flags in the <span class="c003">.cmx</span> files. As such,
inlining of functions from previously-compiled units will subject their code
to the optimisation parameters of the unit currently being compiled, rather
than those specified when they were previously compiled. It is hoped to
rectify this deficiency in the future.</li><li class="li-itemize">Flambda-specific flags do not affect linking with the exception of
affecting the optimisation of code in the startup file (containing
generated functions such as currying helpers). Typically such optimisation
will not be significant, so eliding such flags at link time might be
reasonable.</li><li class="li-itemize">Flambda-specific flags are silently accepted even when the
<span class="c003">-flambda</span> option was not provided to the <span class="c003">configure</span> script.
(There is no means provided to change this behaviour.)
This is intended to make it more
straightforward to run benchmarks with and without the Flambda optimisers
in effect.
</li><li class="li-itemize">Some of the Flambda flags may be subject to change in future
releases.
</li></ul>
<h3 class="subsection" id="sec491">2.1&nbsp;&nbsp;Specification of optimisation parameters by round</h3>
<p><a id="rounds"></a></p><p>Flambda operates in <em>rounds</em>: one round consists of a certain sequence
of transformations that may then be repeated in order to achieve more
satisfactory results. The number of rounds can be set manually using the
<span class="c003">-rounds</span> parameter (although this is not necessary when using
predefined optimisation levels such as with <span class="c003">-O2</span> and <span class="c003">-O3</span>).
For high optimisation the number of rounds might be set at 3 or 4.</p><p>Command-line flags that may apply per round, for example those with
<span class="c003">-cost</span> in the name, accept arguments of the form:
</p><div class="center">
<em>n</em><span class="c003"> | </span><em>round</em><span class="c003">=</span><em>n</em>[<span class="c003">,</span>...]
</div><ul class="itemize"><li class="li-itemize">
If the first form is used, with a single integer specified,
the value will apply to all rounds.
</li><li class="li-itemize">If the second form is used, zero-based <em>round</em> integers specify
values which are to be used only for those rounds.
</li></ul><p>The flags <span class="c003">-Oclassic</span>, <span class="c003">-O2</span> and <span class="c003">-O3</span> are applied before all
other flags, meaning that certain parameters may be overridden without
having to specify every parameter usually invoked by the given optimisation
level.</p>
<h2 class="section" id="sec492">3&nbsp;&nbsp;Inlining</h2>
<p><em>Inlining</em> refers to the copying of the code of a function to a
place where the function is called.
The code of the function will be surrounded by bindings of its parameters
to the corresponding arguments.</p><p>The aims of inlining are:
</p><ul class="itemize"><li class="li-itemize">
to reduce the runtime overhead caused by function calls (including
setting up for such calls and returning afterwards);
</li><li class="li-itemize">to reduce instruction cache misses by expressing frequently-taken
paths through the program using fewer machine instructions; and
</li><li class="li-itemize">to reduce the amount of allocation (especially of closures).
</li></ul><p>
These goals are often reached not just by inlining itself but also by
other optimisations that the compiler is able to perform as a result of
inlining.</p><p>When a recursive call to a function (within the definition of that function
or another in the same mutually-recursive group) is inlined, the procedure is
also known as <em>unrolling</em>. This is somewhat akin to loop peeling.
For example, given the following code:
</p><pre>let rec fact x =
  if x = 0 then
    1
  else
    x * fact (x - 1)

let n = fact 4
</pre><p>unrolling once at the call site <span class="c003">fact 4</span> produces (with the body of
<span class="c003">fact</span> unchanged):
</p><pre>let n =
  if 4 = 0 then
    1
  else
    4 * fact (4 - 1)
</pre><p>This simplifies to:
</p><pre>let n = 4 * fact 3
</pre><p>Flambda provides significantly enhanced inlining capabilities relative to
previous versions of the compiler.</p>
<h4 class="subsubsection" id="sec493">Aside: when inlining is performed</h4>
<p>Inlining is performed together with all of the other Flambda optimisation
passes, that is to say, after closure conversion. This has three particular
advantages over a potentially more straightforward implementation prior to
closure conversion:
</p><ul class="itemize"><li class="li-itemize">
It permits higher-order inlining, for example when a non-inlinable
function always returns the same function yet with different environments
of definition. Not all such cases are supported yet, but it is intended
that such support will be improved in future.
</li><li class="li-itemize">It is easier to integrate with cross-module optimisation, since
imported information about other modules is already in the correct
intermediate language.
</li><li class="li-itemize">It becomes more straightforward to optimise closure allocations since
the layout of closures does not have to be estimated in any way: it is
known. Similarly,
it becomes more straightforward to control which variables end up
in which closures, helping to avoid closure bloat.
</li></ul>
<h3 class="subsection" id="sec494">3.1&nbsp;&nbsp;Classic inlining heuristic</h3>
<p><a id="classic"></a></p><p>In <span class="c003">-Oclassic</span> mode the behaviour of the Flambda inliner
mimics previous versions
of the compiler. (Code may still be subject to further optimisations not
performed by previous versions of the compiler: functors may be inlined,
constants are lifted and unused code is eliminated all as described elsewhere
in this chapter. See sections <a href="#functors">21.3.3</a>, <a href="#lift-const">21.8.1</a> and <a href="#remove-unused">21.10</a>.
At the definition site of a function, the body of the
function is measured. It will then be marked as eligible for inlining
(and hence inlined at every direct call site) if:
</p><ul class="itemize"><li class="li-itemize">
the measured size (in unspecified units) is smaller than that of a
function call plus the argument of the <span class="c003">-inline</span> command-line flag; and
</li><li class="li-itemize">the function is not recursive.
</li></ul><p>Non-Flambda versions of the compiler cannot inline functions that
contain a definition of another function. However <span class="c003">-Oclassic</span> does
permit this. Further, non-Flambda versions also cannot inline functions
that are only themselves exposed as a result of a previous pass of inlining,
but again this is permitted by <span class="c003">-Oclassic</span>.
For example:
</p><pre>module M : sig
  val i : int
end = struct
  let f x =
    let g y = x + y in
    g
  let h = f 3
  let i = h 4  (* h is correctly discovered to be g and inlined *)
end
</pre><p>
All of this contrasts with the normal Flambda mode, that is to say
without <span class="c003">-Oclassic</span>, where:
</p><ul class="itemize"><li class="li-itemize">
the inlining decision is made at the <span class="c013">call site</span>; and
</li><li class="li-itemize">recursive functions can be handled, by <em>specialisation</em> (see
below).
</li></ul><p>
The Flambda mode is described in the next section.</p>
<h3 class="subsection" id="sec495">3.2&nbsp;&nbsp;Overview of “Flambda” inlining heuristics</h3>
<p>The Flambda inlining heuristics, used whenever the compiler is configured
for Flambda and <span class="c003">-Oclassic</span> was not specified, make inlining decisions
at call sites. This helps in situations where the context is important.
For example:
</p><pre>let f b x =
  if b then
    x
  else
    ... big expression ...

let g x = f true x
</pre><p>In this case, we would like to inline <span class="c003">f</span> into <span class="c003">g</span>, because a
conditional jump can be eliminated and the code size should reduce. If the
inlining decision has been made after the declaration of <span class="c003">f</span> without
seeing the use, its size would have probably made it ineligible for
inlining; but at the call site, its final size can be known. Further,
this function should probably not be inlined systematically: if <span class="c003">b</span>
is unknown, or indeed <span class="c003">false</span>, there is little benefit to trade off
against a large increase in code size. In the existing non-Flambda inliner
this isn’t a great problem because chains of inlining were cut off fairly
quickly. However it has led to excessive use of overly-large inlining
parameters such as <span class="c003">-inline 10000</span>.</p><p>In more detail, at each call site the following procedure is followed:
</p><ul class="itemize"><li class="li-itemize">
Determine whether it is clear that inlining would be beneficial
without, for the moment, doing any inlining within the function itself.
(The exact assessment of <em>benefit</em> is described below.) If so, the
function is inlined.
</li><li class="li-itemize">If inlining the function is not clearly beneficial, then inlining
will be performed <em>speculatively</em> inside the function itself. The
search for speculative inlining possibilities is controlled by two
parameters: the <em>inlining threshold</em> and the <em>inlining depth</em>.
(These are described in more detail below.)
<ul class="itemize"><li class="li-itemize">
If such speculation shows that performing some inlining inside the
function would be beneficial, then such inlining is performed and the
resulting function inlined at the original call site.
</li><li class="li-itemize">Otherwise, nothing happens.
</li></ul>
</li></ul><p>
Inlining within recursive functions of calls to other
functions in the same mutually-recursive group is kept in check by
an <em>unrolling depth</em>, described below. This ensures that functions are
not unrolled to excess. (Unrolling is only enabled
if <span class="c003">-O3</span> optimisation level is selected and/or the
<span class="c003">-inline-max-unroll</span>
flag is passed with an argument greater than zero.)</p>
<h3 class="subsection" id="sec496">3.3&nbsp;&nbsp;Handling of specific language constructs</h3>
<h4 class="subsubsection" id="sec497">Functors</h4>
<p><a id="functors"></a></p><p>There is nothing particular about functors that inhibits inlining compared
to normal functions. To the inliner, these both look the same, except
that functors are marked as such.</p><p>Applications of functors at toplevel are biased in favour of inlining.
(This bias may be adjusted:
see the documentation for <span class="c003">-inline-lifting-benefit</span> below.)</p><p>Applications of functors not at toplevel, for example in a local module
inside some other expression, are treated by the inliner identically to
normal function calls.</p>
<h4 class="subsubsection" id="sec498">First-class modules</h4>
<p>The inliner will be able to consider inlining a call to a function in a first
class module if it knows which particular function is going to be called.
The presence of the first-class module record that wraps the set of functions
in the module does not per se inhibit inlining.</p>
<h4 class="subsubsection" id="sec499">Objects</h4>
<p>Method calls to objects are not at present inlined by Flambda.</p>
<h3 class="subsection" id="sec500">3.4&nbsp;&nbsp;Inlining reports</h3>
<p>If the <span class="c003">-inlining-report</span> option is provided to the compiler then a file
will be emitted corresponding to each round of optimisation. For the
OCaml source file <em>basename</em><span class="c003">.ml</span> the files
are named <em>basename</em><span class="c003">.</span><em>round</em><span class="c003">.inlining.org</span>,
with <em>round</em> a
zero-based integer. Inside the files, which are formatted as “org mode”,
will be found English prose describing the decisions that the inliner took.</p>
<h3 class="subsection" id="sec501">3.5&nbsp;&nbsp;Assessment of inlining benefit</h3>
<p><a id="assessment-inlining"></a></p><p>Inlining typically
results in an increase in code size, which if left unchecked, may not only
lead to grossly large executables and excessive compilation times but also
a decrease in performance due to worse locality. As such, the
Flambda inliner trades off the change in code size against
the expected runtime performance benefit, with the benefit being computed
based on the number of operations that the compiler observes may be removed
as a result of inlining.</p><p>For example given the following code:
</p><pre>let f b x =
  if b then
    x
  else
    ... big expression ...

let g x = f true x
</pre><p>it would be observed that inlining of <span class="c003">f</span> would remove:
</p><ul class="itemize"><li class="li-itemize">
one direct call;
</li><li class="li-itemize">one conditional branch.
</li></ul><p>Formally, an estimate of runtime performance benefit is computed by
first summing
the cost of the operations that are known to be removed as a result of the
inlining and subsequent simplification of the inlined body.
The individual costs for the various kinds of operations may be adjusted
using the various <span class="c003">-inline-...-cost</span> flags as follows. Costs are
specified as integers. All of these flags accept a single argument
describing such integers using the conventions
detailed in section <a href="#rounds">21.2.1</a>.
</p><dl class="description"><dt class="dt-description">
<span class="c006">-inline-alloc-cost</span></dt><dd class="dd-description"> The cost of an allocation.
</dd><dt class="dt-description"><span class="c006">-inline-branch-cost</span></dt><dd class="dd-description"> The cost of a branch.
</dd><dt class="dt-description"><span class="c006">-inline-call-cost</span></dt><dd class="dd-description"> The cost of a direct function call.
</dd><dt class="dt-description"><span class="c006">-inline-indirect-cost</span></dt><dd class="dd-description"> The cost of an indirect function call.
</dd><dt class="dt-description"><span class="c006">-inline-prim-cost</span></dt><dd class="dd-description"> The cost of a <em>primitive</em>. Primitives
encompass operations including arithmetic and memory access.
</dd></dl><p>
(Default values are described in section <a href="#defaults">21.5</a> below.)</p><p>The initial benefit value is then scaled by a factor that attempts to
compensate for the fact that the current point in the code, if under some
number of conditional branches, may be cold. (Flambda does not currently
compute hot and cold paths.) The factor—the estimated probability that
the inliner really is on a <em>hot</em> path—is calculated as
1/(1 + <span class="c009">f</span>)<sup><span class="c009">d</span></sup>, where <span class="c009">f</span> is set by
<span class="c003">-inline-branch-factor</span> and <span class="c009">d</span> is the nesting depth of branches
at the current point. As the inliner descends into more deeply-nested
branches, the benefit of inlining thus lessens.</p><p>The resulting benefit value is known as the <em>estimated benefit</em>.</p><p>The change in code size is also estimated: morally speaking it should be the
change in machine code size, but since that is not available to the inliner,
an approximation is used.</p><p>If the estimated benefit exceeds the increase in code size then the inlined
version of the function will be kept. Otherwise the function will not be
inlined.</p><p>Applications of functors at toplevel will be given
an additional benefit (which may be controlled by the
<span class="c003">-inline-lifting-benefit</span> flag) to bias inlining in such situations
towards keeping the inlined version.</p>
<h3 class="subsection" id="sec502">3.6&nbsp;&nbsp;Control of speculation</h3>
<p><a id="speculation"></a></p><p>As described above, there are three parameters that restrict the search
for inlining opportunities during speculation:
</p><ul class="itemize"><li class="li-itemize">
the <em>inlining threshold</em>;
</li><li class="li-itemize">the <em>inlining depth</em>;
</li><li class="li-itemize">the <em>unrolling depth</em>.
</li></ul><p>
These parameters are ultimately bounded by the arguments provided to
the corresponding command-line flags (or their default values):
</p><ul class="itemize"><li class="li-itemize">
<span class="c003">-inline</span> (or, if the call site that triggered speculation is
at toplevel, <span class="c003">-inline-toplevel</span>);
</li><li class="li-itemize"><span class="c003">-inline-max-depth</span>;
</li><li class="li-itemize"><span class="c003">-inline-max-unroll</span>.
</li></ul><p>
<span class="c013">Note in particular</span> that <span class="c003">-inline</span> does not have the meaning that
it has in the previous compiler or in <span class="c003">-Oclassic</span> mode. In both of those
situations <span class="c003">-inline</span> was effectively some kind of basic assessment of
inlining benefit. However in Flambda inlining mode it corresponds to a
constraint on the search; the assessment of benefit is independent, as
described above.</p><p>When speculation starts the inlining threshold starts at the value set
by <span class="c003">-inline</span> (or <span class="c003">-inline-toplevel</span> if appropriate, see above).
Upon making a speculative inlining decision the
threshold is reduced by the code size of the function being inlined.
If the threshold becomes exhausted, at or below zero, no further speculation
will be performed.</p><p>The inlining depth starts at zero
and is increased by one every time the inliner
descends into another function. It is then decreased by one every time the
inliner leaves such function. If the depth exceeds the value set by
<span class="c003">-inline-max-depth</span> then speculation stops. This parameter is intended
as a general backstop for situations where the inlining
threshold does not control the search sufficiently.</p><p>The unrolling depth applies to calls within the same mutually-recursive
group of functions. Each time an inlining of such a call is performed
the depth is incremented by one when examining the resulting body. If the
depth reaches the limit set by <span class="c003">-inline-max-unroll</span> then speculation
stops.</p>
<h2 class="section" id="sec503">4&nbsp;&nbsp;Specialisation</h2>
<p><a id="specialisation"></a></p><p>The inliner may discover a call site to a recursive function where
something is known about the arguments: for example, they may be equal to
some other variables currently in scope. In this situation it may be
beneficial to <em>specialise</em> the function to those arguments. This is
done by copying the declaration of the function (and any others involved
in any same mutually-recursive declaration) and noting the extra information
about the arguments. The arguments augmented by this information are known
as <em>specialised arguments</em>. In order to try to ensure that specialisation
is not performed uselessly, arguments are only specialised if it can be shown
that they are <em>invariant</em>: in other words, during the execution of the
recursive function(s) themselves, the arguments never change.</p><p>Unless overridden by an attribute (see below), specialisation of a function
will not be attempted if:
</p><ul class="itemize"><li class="li-itemize">
the compiler is in <span class="c003">-Oclassic</span> mode;
</li><li class="li-itemize">the function is not obviously recursive;
</li><li class="li-itemize">the function is not closed.
</li></ul><p>The compiler can prove invariance of function arguments across multiple
functions within a recursive group (although this has some limitations,
as shown by the example below).</p><p>It should be noted that the <em>unboxing of closures</em> pass (see below)
can introduce specialised arguments on non-recursive functions. (No other
place in the compiler currently does this.)</p>
<h5 class="paragraph" id="sec504">Example: the well-known <span class="c003">List.iter</span> function</h5>
<p>
This function might be written like so:
</p><pre>let rec iter f l =
  match l with
  | [] -&gt; ()
  | h :: t -&gt;
    f h;
    iter f t
</pre><p>and used like this:
</p><pre>let print_int x =
  print_endline (Int.to_string x)

let run xs =
  iter print_int (List.rev xs)
</pre><p>The argument <span class="c003">f</span> to <span class="c003">iter</span> is invariant so the function may be
specialised:
</p><pre>let run xs =
  let rec iter' f l =
    (* The compiler knows: f holds the same value as foo throughout iter'. *)
    match l with
    | [] -&gt; ()
    | h :: t -&gt;
      f h;
      iter' f t
  in
  iter' print_int (List.rev xs)
</pre><p>The compiler notes down that for the function <span class="c003">iter’</span>, the argument
<span class="c003">f</span> is specialised to the constant closure <span class="c003">print_int</span>. This
means that the body of <span class="c003">iter’</span> may be simplified:
</p><pre>let run xs =
  let rec iter' f l =
    (* The compiler knows: f holds the same value as foo throughout iter'. *)
    match l with
    | [] -&gt; ()
    | h :: t -&gt;
      print_int h;  (* this is now a direct call *)
      iter' f t
  in
  iter' print_int (List.rev xs)
</pre><p>The call to <span class="c003">print_int</span> can indeed be inlined:
</p><pre>let run xs =
  let rec iter' f l =
    (* The compiler knows: f holds the same value as foo throughout iter'. *)
    match l with
    | [] -&gt; ()
    | h :: t -&gt;
      print_endline (Int.to_string h);
      iter' f t
  in
  iter' print_int (List.rev xs)
</pre><p>The unused specialised argument <span class="c003">f</span> may now be removed, leaving:
</p><pre>let run xs =
  let rec iter' l =
    match l with
    | [] -&gt; ()
    | h :: t -&gt;
      print_endline (Int.to_string h);
      iter' t
  in
  iter' (List.rev xs)
</pre>
<h5 class="paragraph" id="sec505">Aside on invariant parameters.</h5>
<p> The compiler cannot currently
detect invariance in cases such as the following.
</p><pre>let rec iter_swap f g l =
  match l with
  | [] -&gt; ()
  | 0 :: t -&gt;
    iter_swap g f l
  | h :: t -&gt;
    f h;
    iter_swap f g t
</pre>
<h3 class="subsection" id="sec506">4.1&nbsp;&nbsp;Assessment of specialisation benefit</h3>
<p>The benefit of specialisation is assessed in a similar way as for inlining.
Specialised argument information may mean that the body of the function
being specialised can be simplified: the removed operations are accumulated
into a benefit. This, together with the size of the duplicated (specialised)
function declaration, is then assessed against the size of the call to the
original function.</p>
<h2 class="section" id="sec507">5&nbsp;&nbsp;Default settings of parameters</h2>
<p><a id="defaults"></a></p><p>The default settings (when not using <span class="c003">-Oclassic</span>) are for one
round of optimisation using the following parameters.
</p><div class="tableau">
<div class="center"><table class="c000 cellpadding1" border="1"><tbody><tr><td class="c014"><span class="c013">Parameter</span></td><td class="c014"><span class="c013">Setting</span> </td></tr>
<tr><td class="c016">
<span class="c003">-inline</span></td><td class="c016">10 </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-factor</span></td><td class="c016">0.1 </td></tr>
<tr><td class="c016"><span class="c003">-inline-alloc-cost</span></td><td class="c016">7 </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-cost</span></td><td class="c016">5 </td></tr>
<tr><td class="c016"><span class="c003">-inline-call-cost</span></td><td class="c016">5 </td></tr>
<tr><td class="c016"><span class="c003">-inline-indirect-cost</span></td><td class="c016">4 </td></tr>
<tr><td class="c016"><span class="c003">-inline-prim-cost</span></td><td class="c016">3 </td></tr>
<tr><td class="c016"><span class="c003">-inline-lifting-benefit</span></td><td class="c016">1300 </td></tr>
<tr><td class="c016"><span class="c003">-inline-toplevel</span></td><td class="c016">160 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-depth</span></td><td class="c016">1 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-unroll</span></td><td class="c016">0 </td></tr>
<tr><td class="c016"><span class="c003">-unbox-closures-factor</span></td><td class="c016">10 </td></tr>
</tbody></table></div></div>
<h3 class="subsection" id="sec508">5.1&nbsp;&nbsp;Settings at -O2 optimisation level</h3>
<p>When <span class="c003">-O2</span> is specified two rounds of optimisation are performed.
The first round uses the default parameters (see above). The second uses
the following parameters.</p><div class="tableau">
<div class="center"><table class="c000 cellpadding1" border="1"><tbody><tr><td class="c014"><span class="c013">Parameter</span></td><td class="c014"><span class="c013">Setting</span> </td></tr>
<tr><td class="c016">
<span class="c003">-inline</span></td><td class="c016">25 </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-factor</span></td><td class="c016">Same as default </td></tr>
<tr><td class="c016"><span class="c003">-inline-alloc-cost</span></td><td class="c016">Double the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-cost</span></td><td class="c016">Double the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-call-cost</span></td><td class="c016">Double the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-indirect-cost</span></td><td class="c016">Double the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-prim-cost</span></td><td class="c016">Double the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-lifting-benefit</span></td><td class="c016">Same as default </td></tr>
<tr><td class="c016"><span class="c003">-inline-toplevel</span></td><td class="c016">400 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-depth</span></td><td class="c016">2 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-unroll</span></td><td class="c016">Same as default </td></tr>
<tr><td class="c016"><span class="c003">-unbox-closures-factor</span></td><td class="c016">Same as default </td></tr>
</tbody></table></div></div>
<h3 class="subsection" id="sec509">5.2&nbsp;&nbsp;Settings at -O3 optimisation level</h3>
<p>When <span class="c003">-O3</span> is specified three rounds of optimisation are performed.
The first two rounds are as for <span class="c003">-O2</span>. The third round uses
the following parameters.</p><div class="tableau">
<div class="center"><table class="c000 cellpadding1" border="1"><tbody><tr><td class="c014"><span class="c013">Parameter</span></td><td class="c014"><span class="c013">Setting</span> </td></tr>
<tr><td class="c016">
<span class="c003">-inline</span></td><td class="c016">50 </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-factor</span></td><td class="c016">Same as default </td></tr>
<tr><td class="c016"><span class="c003">-inline-alloc-cost</span></td><td class="c016">Triple the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-branch-cost</span></td><td class="c016">Triple the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-call-cost</span></td><td class="c016">Triple the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-indirect-cost</span></td><td class="c016">Triple the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-prim-cost</span></td><td class="c016">Triple the default </td></tr>
<tr><td class="c016"><span class="c003">-inline-lifting-benefit</span></td><td class="c016">Same as default </td></tr>
<tr><td class="c016"><span class="c003">-inline-toplevel</span></td><td class="c016">800 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-depth</span></td><td class="c016">3 </td></tr>
<tr><td class="c016"><span class="c003">-inline-max-unroll</span></td><td class="c016">1 </td></tr>
<tr><td class="c016"><span class="c003">-unbox-closures-factor</span></td><td class="c016">Same as default </td></tr>
</tbody></table></div></div>
<h2 class="section" id="sec510">6&nbsp;&nbsp;Manual control of inlining and specialisation</h2>
<p>Should the inliner prove recalcitrant and refuse to inline a particular
function, or if the observed inlining decisions are not to the programmer’s
satisfaction for some other reason, inlining behaviour can be dictated by the
programmer directly in the source code.
One example where this might be appropriate is when the programmer,
but not the compiler, knows that a particular function call is on a cold
code path. It might be desirable to prevent inlining of the function so
that the code size along the hot path is kept smaller, so as to increase
locality.</p><p>The inliner is directed using attributes.
For non-recursive functions (and one-step unrolling of recursive functions,
although <span class="c003">@unroll</span> is more clear for this purpose)
the following are supported:
</p><dl class="description"><dt class="dt-description">
<span class="c013"><span class="c003">@@inline always</span> or <span class="c003">@@inline never</span></span></dt><dd class="dd-description"> Attached
to a <em>declaration</em> of a function or functor, these direct the inliner to
either
always or never inline, irrespective of the size/benefit calculation. (If
the function is recursive then the body is substituted and no special
action is taken for the recursive call site(s).)
<span class="c003">@@inline</span> with no argument is equivalent to
<span class="c003">@@inline always</span>.
</dd><dt class="dt-description"><span class="c013"><span class="c003">@inlined always</span> or <span class="c003">@inlined never</span></span></dt><dd class="dd-description"> Attached
to a function <em>application</em>, these direct the inliner likewise. These
attributes at call sites override any other attribute that may be present
on the corresponding declaration.
<span class="c003">@inlined</span> with no argument is equivalent to
<span class="c003">@inlined always</span>.
</dd></dl><p>For recursive functions the relevant attributes are:
</p><dl class="description"><dt class="dt-description">
<span class="c013"><span class="c003">@@specialise always</span> or <span class="c003">@@specialise never</span></span></dt><dd class="dd-description">Attached to a declaration of a function
or functor, this directs the inliner to either always or never
specialise the function so
long as it has appropriate contextual knowledge, irrespective of the
size/benefit calculation.
<span class="c003">@@specialise</span> with no argument is equivalent to
<span class="c003">@@specialise always</span>.
</dd><dt class="dt-description"><span class="c013"><span class="c003">@specialised always</span> or <span class="c003">@specialised never</span></span></dt><dd class="dd-description">Attached to a function application, this
directs the inliner likewise. This attribute at a call site overrides any
other attribute that may be present on the corresponding declaration.
(Note that the function will still only be specialised if there exist
one or more invariant parameters whose values are known.)
<span class="c003">@specialised</span> with no argument is equivalent to
<span class="c003">@specialised always</span>.
</dd><dt class="dt-description"><span class="c006">@unrolled </span><span class="c009">n</span></dt><dd class="dd-description"> This attribute is attached to a function
application and always takes an integer argument. Each time the inliner sees
the attribute it behaves as follows:
<ul class="itemize"><li class="li-itemize">
If <span class="c009">n</span> is zero or less, nothing happens.
</li><li class="li-itemize">Otherwise the function being called is substituted at the call site
with its body having been rewritten such that 
any recursive calls to that function <em>or
any others in the same mutually-recursive group</em> are annotated with the
attribute <span class="c003">unrolled(</span><span class="c009">n</span> − 1<span class="c003">)</span>. Inlining may continue on that body.
</li></ul>
As such, <span class="c009">n</span> behaves as the “maximum depth of unrolling”.
</dd></dl><p>A compiler warning will be emitted if it was found impossible to obey an
annotation from an <span class="c003">@inlined</span> or <span class="c003">@specialised</span> attribute.</p>
<h5 class="paragraph" id="sec511">Example showing correct placement of attributes</h5>
<pre>module F (M : sig type t end) = struct
  let[@inline never] bar x =
    x * 3

  let foo x =
    (bar [@inlined]) (42 + x)
end [@@inline never]

module X = F [@inlined] (struct type t = int end)
</pre>
<h2 class="section" id="sec512">7&nbsp;&nbsp;Simplification</h2>
<p>Simplification, which is run in conjunction with inlining,
propagates information (known as <em>approximations</em>) about which
variables hold what values at runtime. Certain relationships between
variables and symbols are also tracked: for example, some variable may be
known to always hold the same value as some other variable; or perhaps
some variable may be known to always hold the value pointed to by some
symbol.</p><p>The propagation can help to eliminate allocations in cases such as:
</p><pre>let f x y =
  ...
  let p = x, y in
  ...
  ... (fst p) ... (snd p) ...
</pre><p>The projections from <span class="c003">p</span> may be replaced by uses of the variables
<span class="c003">x</span> and <span class="c003">y</span>, potentially meaning that <span class="c003">p</span> becomes unused.</p><p>The propagation performed by the simplification pass is also important for
discovering which functions flow to indirect call sites. This can enable
the transformation of such call sites into direct call sites, which makes
them eligible for an inlining transformation.</p><p>Note that no information is propagated about the contents of strings,
even in <span class="c003">safe-string</span> mode, because it cannot yet be guaranteed
that they are immutable throughout a given program.</p>
<h2 class="section" id="sec513">8&nbsp;&nbsp;Other code motion transformations</h2>
<h3 class="subsection" id="sec514">8.1&nbsp;&nbsp;Lifting of constants</h3>
<p><a id="lift-const"></a></p><p>Expressions found to be constant will be lifted to symbol
bindings—that is to say, they will be statically allocated in the
object file—when
they evaluate to boxed values. Such constants may be straightforward numeric
constants, such as the floating-point number <span class="c003">42.0</span>, or more complicated
values such as constant closures.</p><p>Lifting of constants to toplevel reduces allocation at runtime.</p><p>The compiler aims to share constants lifted to toplevel such that there
are no duplicate definitions. However if <span class="c003">.cmx</span> files are hidden
from the compiler then maximal sharing may not be possible.</p>
<h5 class="paragraph" id="sec515">Notes about float arrays</h5>
<p> The following language semantics apply specifically to constant float arrays.
(By “constant float array” is meant an array consisting entirely of floating
point numbers that are known at compile time. A common case is a literal
such as <span class="c003">[| 42.0; 43.0; |]</span>.
</p><ul class="itemize"><li class="li-itemize">
Constant float arrays at the toplevel are mutable and never shared.
(That is to say, for each
such definition there is a distinct symbol in the data section of the object
file pointing at the array.)
</li><li class="li-itemize">Constant float arrays not at toplevel are mutable and are created each
time the expression is evaluated. This can be thought of as an operation that
takes an immutable array (which in the source code has no associated name; let
us call it the <em>initialising array</em>) and
duplicates it into a fresh mutable array.
<ul class="itemize"><li class="li-itemize">
If the array is of size four or less, the expression will create a
fresh block and write the values into it one by one. There is no reference
to the initialising array as a whole.</li><li class="li-itemize">Otherwise, the initialising array is lifted out and subject to the
normal constant sharing procedure;
creation of the array consists of bulk copying the initialising array
into a fresh value on the OCaml heap.
</li></ul>
</li></ul>
<h3 class="subsection" id="sec516">8.2&nbsp;&nbsp;Lifting of toplevel let bindings</h3>
<p>Toplevel <span class="c003">let</span>-expressions may be lifted to symbol bindings to ensure
that the corresponding bound variables are not captured by closures. If the
defining expression of a given binding is found to be constant, it is bound
as such (the technical term is a <em>let-symbol</em> binding).</p><p>Otherwise, the symbol is bound to a (statically-allocated)
<em>preallocated block</em> containing one field. At runtime, the defining
expression will be evaluated and the first field of the block filled with
the resulting value. This <em>initialise-symbol</em> binding
causes one extra indirection but ensures, by
virtue of the symbol’s address being known at compile time, that uses of the
value are not captured by closures.</p><p>It should be noted that the blocks corresponding to initialise-symbol
bindings are kept alive forever, by virtue of them occurring in a static
table of GC roots within the object file. This extended lifetime of
expressions may on occasion be surprising. If it is desired to create
some non-constant value (for example when writing GC tests) that does not
have this
extended lifetime, then it may be created and used inside a function,
with the application point of that function (perhaps at toplevel)—or
indeed the function declaration itself—marked
as to never be inlined. This technique prevents lifting of the definition
of the value in question (assuming of course that it is not constant).</p>
<h2 class="section" id="sec517">9&nbsp;&nbsp;Unboxing transformations</h2>
<p>The transformations in this section relate to the splitting apart of
<em>boxed</em> (that is to say, non-immediate) values. They are largely
intended to reduce allocation, which tends to result in a runtime
performance profile with lower variance and smaller tails.</p>
<h3 class="subsection" id="sec518">9.1&nbsp;&nbsp;Unboxing of closure variables</h3>
<p><a id="unbox-fvs"></a></p><p>This transformation is enabled unless
<span class="c003">-no-unbox-free-vars-of-closures</span> is provided.</p><p>Variables that appear in closure environments may themselves be boxed
values. As such, they may be split into further closure variables, each
of which corresponds to some projection from the original closure variable(s).
This transformation is called <em>unboxing of closure variables</em> or
<em>unboxing of free variables of closures</em>. It is only applied when
there is
reasonable certainty that there are no uses of the boxed free variable itself
within the corresponding function bodies.
</p>
<h5 class="paragraph" id="sec519">Example:</h5>
<p> In the following code, the compiler observes that
the closure returned from the function <span class="c003">f</span> contains a variable <span class="c003">pair</span>
(free in the body of <span class="c003">f</span>) that may be split into two separate variables.
</p><pre>let f x0 x1 =
  let pair = x0, x1 in
  Printf.printf "foo\n";
  fun y -&gt;
    fst pair + snd pair + y
</pre><p>After some simplification one obtains:
</p><pre>let f x0 x1 =
  let pair_0 = x0 in
  let pair_1 = x1 in
  Printf.printf "foo\n";
  fun y -&gt;
    pair_0 + pair_1 + y
</pre><p>and then:
</p><pre>let f x0 x1 =
  Printf.printf "foo\n";
  fun y -&gt;
    x0 + x1 + y
</pre><p>The allocation of the pair has been eliminated.</p><p>This transformation does not operate if it would cause the closure to
contain more than twice as many closure variables as it did beforehand.</p>
<h3 class="subsection" id="sec520">9.2&nbsp;&nbsp;Unboxing of specialised arguments</h3>
<p><a id="unbox-spec-args"></a></p><p>This transformation is enabled unless
<span class="c003">-no-unbox-specialised-args</span> is provided.</p><p>It may become the case during compilation that one or more invariant arguments
to a function become specialised to a particular value. When such values are
themselves boxed the corresponding specialised arguments may be split into
more specialised arguments corresponding to the projections out of the boxed
value that occur within the function body. This transformation is called
<em>unboxing of specialised arguments</em>. It is only applied when there is
reasonable certainty that the boxed argument itself is unused within the
function.</p><p>If the function in question is involved in a recursive group then unboxing
of specialised arguments may be immediately replicated across the group
based on the dataflow between invariant arguments.</p>
<h5 class="paragraph" id="sec521">Example:</h5>
<p> Having been given the following code, the compiler
will inline <span class="c003">loop</span> into <span class="c003">f</span>, and then observe <span class="c003">inv</span>
being invariant and always the pair formed by adding <span class="c003">42</span> and <span class="c003">43</span>
to the argument <span class="c003">x</span> of the function <span class="c003">f</span>.
</p><pre>let rec loop inv xs =
  match xs with
  | [] -&gt; fst inv + snd inv
  | x::xs -&gt; x + loop2 xs inv
and loop2 ys inv =
  match ys with
  | [] -&gt; 4
  | y::ys -&gt; y - loop inv ys

let f x =
  Printf.printf "%d\n" (loop (x + 42, x + 43) [1; 2; 3])
</pre><p>Since the functions have sufficiently few arguments, more specialised
arguments will be added. After some simplification one obtains:
</p><pre>let f x =
  let rec loop' xs inv_0 inv_1 =
    match xs with
    | [] -&gt; inv_0 + inv_1
    | x::xs -&gt; x + loop2' xs inv_0 inv_1
  and loop2' ys inv_0 inv_1 =
    match ys with
    | [] -&gt; 4
    | y::ys -&gt; y - loop' ys inv_0 inv_1
  in
  Printf.printf "%d\n" (loop' [1; 2; 3] (x + 42) (x + 43))
</pre><p>The allocation of the pair within <span class="c003">f</span> has been removed. (Since the
two closures for <span class="c003">loop’</span> and <span class="c003">loop2’</span> are constant they will also be
lifted to toplevel with no runtime allocation penalty. This
would also happen without having run the transformation to unbox
specialise arguments.)</p><p>The transformation to unbox specialised arguments never introduces extra
allocation.</p><p>The transformation will not unbox arguments if it would result in the
original function having sufficiently many arguments so as to inhibit
tail-call optimisation.</p><p>The transformation is implemented by creating a wrapper function that
accepts the original arguments. Meanwhile, the original function is renamed
and extra arguments are added corresponding to the unboxed specialised
arguments; this new function
is called from the wrapper. The wrapper will then be inlined
at direct call sites. Indeed, all call sites will be direct unless
<span class="c003">-unbox-closures</span> is being used, since they will have been generated
by the compiler when originally specialising the function. (In the case
of <span class="c003">-unbox-closures</span> other functions may appear with specialised
arguments; in this case there may be indirect calls and these will incur
a small penalty owing to having to bounce through the wrapper. The technique
of <em>direct call surrogates</em> used for <span class="c003">-unbox-closures</span> is not
used by the transformation to unbox specialised arguments.)</p>
<h3 class="subsection" id="sec522">9.3&nbsp;&nbsp;Unboxing of closures</h3>
<p><a id="unbox-closures"></a></p><p>This transformation is <em>not</em> enabled by default. It may be enabled
using the <span class="c003">-unbox-closures</span> flag.</p><p>The transformation replaces closure variables by specialised arguments.
The aim is to cause more closures to become closed. It is particularly
applicable, as a means of reducing allocation, where the function concerned
cannot be inlined or specialised. For example, some non-recursive function
might be too large to inline; or some recursive function might offer
no opportunities for specialisation perhaps because its only argument is
one of type <span class="c003">unit</span>.</p><p>At present there may be a small penalty in terms of actual runtime
performance when this transformation is enabled, although more stable
performance may be obtained due to reduced allocation. It is recommended
that developers experiment to determine whether the option is beneficial
for their code. (It is expected that in the future it will be possible
for the performance degradation to be removed.)</p>
<h5 class="paragraph" id="sec523">Simple example:</h5>
<p> In the following code (which might typically
occur when <span class="c003">g</span> is too large to inline) the value of <span class="c003">x</span> would usually
be communicated to the application of the <span class="c003">+</span> function via the closure
of <span class="c003">g</span>.
</p><pre>let f x =
  let g y =
    x + y
  in
  (g [@inlined never]) 42
</pre><p>Unboxing of the closure causes the value for <span class="c003">x</span> inside <span class="c003">g</span> to
be passed as an argument to <span class="c003">g</span> rather than through its closure. This
means that the closure of <span class="c003">g</span> becomes constant and may be lifted to
toplevel, eliminating the runtime allocation.</p><p>The transformation is implemented by adding a new wrapper function in the
manner of that used when unboxing specialised arguments. The closure
variables are still free in the wrapper, but the intention is that when
the wrapper is inlined at direct call sites, the relevant values are
passed directly to the main function via the new specialised arguments.</p><p>Adding such a wrapper will penalise indirect calls to the function
(which might exist in arbitrary places; remember that this transformation
is not for example applied only on functions the compiler has produced
as a result of specialisation) since such calls will bounce through
the wrapper. To
mitigate this, if a function is small enough when weighed up against
the number of free variables being removed, it will be duplicated by the
transformation to obtain two versions: the original (used for indirect calls,
since we can do no better) and the wrapper/rewritten function pair as
described in the previous paragraph. The wrapper/rewritten function pair
will only be used at direct call sites of the function. (The wrapper in
this case is known as a <em>direct call surrogate</em>, since
it takes the place of another function—the unchanged version used for
indirect calls—at direct call sites.)</p><p>The <span class="c003">-unbox-closures-factor</span> command line flag, which takes an
integer, may be used to adjust the point at which a function is deemed
large enough to be ineligible for duplication. The benefit of
duplication is scaled by the integer before being evaluated against the
size.</p>
<h5 class="paragraph" id="sec524">Harder example:</h5>
<p> In the following code, there are two closure
variables that would typically cause closure allocations. One is called
<span class="c003">fv</span> and occurs inside the function <span class="c003">baz</span>; the other is called
<span class="c003">z</span> and occurs inside the function <span class="c003">bar</span>.
In this toy (yet sophisticated) example we again use an attribute to
simulate the typical situation where the first argument of <span class="c003">baz</span> is
too large to inline.
</p><pre>let foo c =
  let rec bar zs fv =
    match zs with
    | [] -&gt; []
    | z::zs -&gt;
      let rec baz f = function
        | [] -&gt; []
        | a::l -&gt; let r = fv + ((f [@inlined never]) a) in r :: baz f l
      in
      (map2 (fun y -&gt; z + y) [z; 2; 3; 4]) @ bar zs fv
  in
  Printf.printf "%d" (List.length (bar [1; 2; 3; 4] c))
</pre><p>The code resulting from applying <span class="c003">-O3 -unbox-closures</span> to this code
passes the free variables via function arguments in
order to eliminate all closure allocation in this example (aside from any
that might be performed inside <span class="c003">printf</span>).</p>
<h2 class="section" id="sec525">10&nbsp;&nbsp;Removal of unused code and values</h2>
<p><a id="remove-unused"></a></p>
<h3 class="subsection" id="sec526">10.1&nbsp;&nbsp;Removal of redundant let expressions</h3>
<p>The simplification pass removes unused <span class="c003">let</span> bindings so long as
their corresponding defining expressions have “no effects”. See
the section “Treatment of effects” below for the precise definition of
this term.</p>
<h3 class="subsection" id="sec527">10.2&nbsp;&nbsp;Removal of redundant program constructs</h3>
<p>This transformation is analogous to the removal of <span class="c003">let</span>-expressions
whose defining expressions have no effects. It operates instead on symbol
bindings, removing those that have no effects.</p>
<h3 class="subsection" id="sec528">10.3&nbsp;&nbsp;Removal of unused arguments</h3>
<p><a id="remove-unused-args"></a></p><p>This transformation is only enabled by default for specialised arguments.
It may be enabled for all arguments using the <span class="c003">-remove-unused-arguments</span>
flag.</p><p>The pass analyses functions to determine which arguments are unused.
Removal is effected by creating a wrapper function, which will be inlined
at every direct call site, that accepts the original arguments and then
discards the unused ones before calling the original function. As a
consequence, this transformation may be detrimental if the original
function is usually indirectly called, since such calls will now bounce
through the wrapper. (The technique of <em>direct call surrogates</em> used
to reduce this penalty during unboxing of closure variables (see above)
does not yet apply to the pass that removes unused arguments.)</p>
<h3 class="subsection" id="sec529">10.4&nbsp;&nbsp;Removal of unused closure variables</h3>
<p>This transformation performs an analysis across
the whole compilation unit to determine whether there exist closure variables
that are never used. Such closure variables are then eliminated. (Note that
this has to be a whole-unit analysis because a projection of a closure
variable from some particular closure may have propagated to an arbitrary
location within the code due to inlining.)</p>
<h2 class="section" id="sec530">11&nbsp;&nbsp;Other code transformations</h2>
<h3 class="subsection" id="sec531">11.1&nbsp;&nbsp;Transformation of non-escaping references into mutable variables</h3>
<p>Flambda performs a simple analysis analogous to that performed elsewhere
in the compiler that can transform <span class="c003">ref</span>s into mutable variables
that may then be held in registers (or on the stack as appropriate) rather
than being allocated on the OCaml heap. This only happens so long as the
reference concerned can be shown to not escape from its defining scope.</p>
<h3 class="subsection" id="sec532">11.2&nbsp;&nbsp;Substitution of closure variables for specialised arguments</h3>
<p>This transformation discovers closure variables that are known to be
equal to specialised arguments. Such closure variables are replaced by
the specialised arguments; the closure variables may then be removed by
the “removal of unused closure variables” pass (see below).</p>
<h2 class="section" id="sec533">12&nbsp;&nbsp;Treatment of effects</h2>
<p>The Flambda optimisers classify expressions in order to determine whether
an expression:
</p><ul class="itemize"><li class="li-itemize">
does not need to be evaluated at all; and/or
</li><li class="li-itemize">may be duplicated.
</li></ul><p>This is done by forming judgements on the <em>effects</em> and the <em>coeffects</em>
that might be performed were the expression to be executed. Effects talk
about how the expression might affect the world; coeffects talk about how
the world might affect the expression.</p><p>Effects are classified as follows:
</p><dl class="description"><dt class="dt-description">
<span class="c013">No effects:</span></dt><dd class="dd-description"> The expression does not change the observable state
of the world. For example, it must not write to any mutable storage,
call arbitrary external functions or change control flow (e.g. by raising
an exception). Note that allocation is <em>not</em> classed as having
“no effects” (see below).
<ul class="itemize"><li class="li-itemize">
It is assumed in the compiler that expressions with no
effects, whose results are not used, may be eliminated. (This typically
happens where the expression in question is the defining expression of a
<span class="c003">let</span>; in such cases the <span class="c003">let</span>-expression will be
eliminated.) It is further
assumed that such expressions with no effects may be
duplicated (and thus possibly executed more than once).
</li><li class="li-itemize">Exceptions arising from allocation points, for example
“out of memory” or
exceptions propagated from finalizers or signal handlers, are treated as
“effects out of the ether” and thus ignored for our determination here
of effectfulness. The same goes for floating point operations that may
cause hardware traps on some platforms.
</li></ul>
</dd><dt class="dt-description"><span class="c013">Only generative effects:</span></dt><dd class="dd-description"> The expression does not change the
observable state of the world save for possibly affecting the state of
the garbage collector by performing an allocation. Expressions
that only have generative effects and whose results are unused
may be eliminated by the compiler. However, unlike expressions with
“no effects”, such expressions will never be eligible for duplication.
</dd><dt class="dt-description"><span class="c013">Arbitrary effects:</span></dt><dd class="dd-description"> All other expressions.
</dd></dl><p>There is a single classification for coeffects:
</p><dl class="description"><dt class="dt-description">
<span class="c013">No coeffects:</span></dt><dd class="dd-description"> The expression does not observe the effects (in
the sense described above) of other expressions. For example, it must not
read from any mutable storage or call arbitrary external functions.
</dd></dl><p>It is assumed in the compiler that, subject to data dependencies,
expressions with neither effects nor coeffects may be reordered with
respect to other expressions.</p>
<h2 class="section" id="sec534">13&nbsp;&nbsp;Compilation of statically-allocated modules</h2>
<p>Compilation of modules that are able to be statically allocated (for example,
the module corresponding to an entire compilation unit, as opposed to a first
class module dependent on values computed at runtime) initially follows the
strategy used for bytecode. A sequence of <span class="c003">let</span>-bindings, which may be
interspersed with arbitrary effects, surrounds a record creation that becomes
the module block. The Flambda-specific transformation follows: these bindings
are lifted to toplevel symbols, as described above.</p>
<h2 class="section" id="sec535">14&nbsp;&nbsp;Inhibition of optimisation</h2>
<p><a id="inhibition"></a></p><p>Especially when writing benchmarking suites that run non-side-effecting
algorithms in loops, it may be found that the optimiser entirely
elides the code being benchmarked. This behaviour can be prevented by
using the <span class="c003">Sys.opaque_identity</span> function (which indeed behaves as a
normal OCaml function and does not possess any “magic” semantics). The
documentation of the <span class="c003">Sys</span> module should be consulted for further details.</p>
<h2 class="section" id="sec536">15&nbsp;&nbsp;Use of unsafe operations</h2>
<p><a id="unsafe"></a></p><p>The behaviour of the Flambda simplification pass means that certain unsafe
operations, which may without Flambda or when using previous versions of
the compiler be safe, must not be used. This specifically refers to
functions found in the <span class="c003">Obj</span> module.</p><p>In particular, it is forbidden to change any value (for example using
<span class="c003">Obj.set_field</span> or <span class="c003">Obj.set_tag</span>) that is not mutable.
(Values returned from C stubs
are always treated as mutable.) The compiler will emit warning 59 if it
detects such a write—but it cannot warn in all cases. Here is an example
of code that will trigger the warning:
</p><pre>let f x =
  let a = 42, x in
  (Obj.magic a : int ref) := 1;
  fst a
</pre><p>The reason this is unsafe is because the simplification pass believes that
<span class="c003">fst a</span> holds the value <span class="c003">42</span>; and indeed it must, unless type
soundness has been broken via unsafe operations.</p><p>If it must be the case that code has to be written that triggers warning 59,
but the code is known to actually be correct (for some definition of
correct), then <span class="c003">Sys.opaque_identity</span> may be used to wrap the value
before unsafe operations are performed upon it. Great care must be taken
when doing this to ensure that the opacity is added at the correct place.
It must be emphasised that this use of <span class="c003">Sys.opaque_identity</span> is only
for <span class="c013">exceptional</span> cases. It should not be used in normal code or to
try to guide the optimiser.</p><p>As an example, this code will return the integer <span class="c003">1</span>:
</p><pre>let f x =
  let a = Sys.opaque_identity (42, x) in
  (Obj.magic a : int ref) := 1;
  fst a
</pre><p>However the following code will still return <span class="c003">42</span>:
</p><pre>let f x =
  let a = 42, x in
  Sys.opaque_identity (Obj.magic a : int ref) := 1;
  fst a
</pre><p>
High levels of inlining performed by Flambda may expose bugs in code
thought previously to be correct. Take care, for example, not
to add type annotations that claim some mutable value is always immediate
if it might be possible for an unsafe operation to update it to a boxed
value.</p>
<h2 class="section" id="sec537">16&nbsp;&nbsp;Glossary</h2>
<p>The following terminology is used in this chapter of the manual.</p><dl class="description"><dt class="dt-description">
<span class="c013">Call site</span></dt><dd class="dd-description"> See <em>direct call site</em> and <em>indirect call site</em> below.
</dd><dt class="dt-description"><span class="c013">Closed function</span></dt><dd class="dd-description"> A function whose body has no free variables
except its parameters and any to which are bound other functions within
the same (possibly mutually-recursive) declaration.
</dd><dt class="dt-description"><span class="c013">Closure</span></dt><dd class="dd-description"> The runtime representation of a function. This
includes pointers to the code of the function
together with the values of any variables that are used in the body of
the function but actually defined outside of the function, in the
enclosing scope.
The values of such variables, collectively known as the
<em>environment</em>, are required because the function may be
invoked from a place where the original bindings of such variables are
no longer in scope. A group of possibly
mutually-recursive functions defined using <em>let rec</em> all share a
single closure. (Note to developers: in the Flambda source code a
<em>closure</em> always corresponds to a single function; a
<em>set of closures</em> refers to a group of such.)
</dd><dt class="dt-description"><span class="c013">Closure variable</span></dt><dd class="dd-description"> A member of the environment held within the
closure of a given function.
</dd><dt class="dt-description"><span class="c013">Constant</span></dt><dd class="dd-description"> Some entity (typically an expression) the value of which
is known by the compiler at compile time. Constantness may be explicit from
the source code or inferred by the Flambda optimisers.
</dd><dt class="dt-description"><span class="c013">Constant closure</span></dt><dd class="dd-description"> A closure that is statically allocated in an
object file. It is almost always the case that the environment portion of
such a closure is empty.
</dd><dt class="dt-description"><span class="c013">Defining expression</span></dt><dd class="dd-description"> The expression <span class="c003">e</span> in <span class="c003">let x = e in e’</span>.
</dd><dt class="dt-description"><span class="c013">Direct call site</span></dt><dd class="dd-description"> A place in a program’s code where a function is
called and it is known at compile time which function it will always be.
</dd><dt class="dt-description"><span class="c013">Indirect call site</span></dt><dd class="dd-description"> A place in a program’s code where a function
is called but is not known to be a <em>direct call site</em>.
</dd><dt class="dt-description"><span class="c013">Program</span></dt><dd class="dd-description"> A collection of <em>symbol bindings</em> forming the
definition of a single compilation unit (i.e. <span class="c003">.cmx</span> file).
</dd><dt class="dt-description"><span class="c013">Specialised argument</span></dt><dd class="dd-description"> An argument to a function that is known
to always hold a particular value at runtime. These are introduced by the
inliner when specialising recursive functions; and the <span class="c003">unbox-closures</span>
pass. (See section <a href="#specialisation">21.4</a>.)
</dd><dt class="dt-description"><span class="c013">Symbol</span></dt><dd class="dd-description"> A name referencing a particular place in an object file
or executable image. At that particular place will be some constant value.
Symbols may be examined using operating system-specific tools (for
example <span class="c003">objdump</span> on Linux).
</dd><dt class="dt-description"><span class="c013">Symbol binding</span></dt><dd class="dd-description"> Analogous to a <span class="c003">let</span>-expression but working
at the level of symbols defined in the object file. The address of a symbol is
fixed, but it may be bound to both constant and non-constant expressions.
</dd><dt class="dt-description"><span class="c013">Toplevel</span></dt><dd class="dd-description"> An expression in the current program which is not
enclosed within any function declaration.
</dd><dt class="dt-description"><span class="c013">Variable</span></dt><dd class="dd-description"> A named entity to which some OCaml value is bound by a
<span class="c003">let</span> expression, pattern-matching construction, or similar.
</dd></dl>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>