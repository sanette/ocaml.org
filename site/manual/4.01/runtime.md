<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="comp.html">Batch compilation (ocamlc)</a></li><li><a href="toplevel.html">The toplevel system (ocaml)</a></li><li class="active"><a href="runtime.html">The runtime system (ocamlrun)</a></li><li><a href="native.html">Native-code compilation (ocamlopt)</a></li><li><a href="lexyacc.html">Lexer and parser generators (ocamllex, ocamlyacc)</a></li><li><a href="depend.html">Dependency generator (ocamldep)</a></li><li><a href="browser.html">The browser/editor (ocamlbrowser)</a></li><li><a href="ocamldoc.html">The documentation generator (ocamldoc)</a></li><li><a href="debugger.html">The debugger (ocamldebug)</a></li><li><a href="profil.html">Profiling (ocamlprof)</a></li><li><a href="ocamlbuild.html">The ocamlbuild compilation manager</a></li><li><a href="intfc.html">Interfacing C with OCaml</a></li></ul>




<h1 class="chapter" id="sec253"><span>Chapter 10</span>&nbsp;&nbsp;The runtime system (ocamlrun)</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.01</a></div><div class="toc_title"><a href="#">The runtime system (ocamlrun)</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="runtime.html#sec254">Overview</a>
</li><li><a href="runtime.html#sec255">Options</a>
</li><li><a href="runtime.html#sec256">Dynamic loading of shared libraries</a>
</li><li><a href="runtime.html#sec257">Common errors</a>
</li></ul></nav></header>
<p> <a id="c:runtime"></a>

</p><p>The <span class="c007">ocamlrun</span> command executes bytecode files produced by the
linking phase of the <span class="c007">ocamlc</span> command.</p>
<h2 class="section" id="sec254">1&nbsp;&nbsp;Overview</h2>
<p>The <span class="c007">ocamlrun</span> command comprises three main parts: the bytecode
interpreter, that actually executes bytecode files; the memory
allocator and garbage collector; and a set of C functions that
implement primitive operations such as input/output.</p><p>The usage for <span class="c007">ocamlrun</span> is:
</p><pre>        ocamlrun <span class="c013">options bytecode-executable arg</span><sub>1</sub> ... <span class="c013">arg</span><sub><span class="c013">n</span></sub>
</pre><p>
The first non-option argument is taken to be the name of the file
containing the executable bytecode. (That file is searched in the
executable path as well as in the current directory.) The remaining
arguments are passed to the OCaml program, in the string array
<span class="c007">Sys.argv</span>. Element 0 of this array is the name of the
bytecode executable file; elements 1 to <span class="c013">n</span> are the remaining
arguments <span class="c013">arg</span><sub>1</sub> to <span class="c013">arg</span><sub><span class="c013">n</span></sub>.</p><p>As mentioned in chapter&nbsp;<a href="comp.html#c%3Acamlc">8</a>, the bytecode executable files
produced by the <span class="c007">ocamlc</span> command are self-executable, and manage to
launch the <span class="c007">ocamlrun</span> command on themselves automatically. That is,
assuming <span class="c007">a.out</span> is a bytecode executable file,
</p><pre>        a.out <span class="c013">arg</span><sub>1</sub> ... <span class="c013">arg</span><sub><span class="c013">n</span></sub>
</pre><p>
works exactly as
</p><pre>        ocamlrun a.out <span class="c013">arg</span><sub>1</sub> ... <span class="c013">arg</span><sub><span class="c013">n</span></sub>
</pre><p>
Notice that it is not possible to pass options to <span class="c007">ocamlrun</span> when
invoking <span class="c007">a.out</span> directly.</p><blockquote class="quote"><span class="c011">Windows:</span>&nbsp;&nbsp;
Under several versions of Windows, bytecode executable files are
self-executable only if their name ends in <span class="c007">.exe</span>. It is recommended
to always give <span class="c007">.exe</span> names to bytecode executables, e.g. compile
with <span class="c007">ocamlc -o myprog.exe ...</span> rather than <span class="c007">ocamlc -o myprog ...</span>.
</blockquote>
<h2 class="section" id="sec255">2&nbsp;&nbsp;Options</h2>
<p> <a id="ocamlrun-options"></a></p><p>The following command-line options are recognized by <span class="c007">ocamlrun</span>.</p><dl class="description"><dt class="dt-description"><span class="c010">-b</span></dt><dd class="dd-description">
When the program aborts due to an uncaught exception, print a detailed
“back trace” of the execution, showing where the exception was
raised and which function calls were outstanding at this point. The
back trace is printed only if the bytecode executable contains
debugging information, i.e. was compiled and linked with the <span class="c007">-g</span>
option to <span class="c007">ocamlc</span> set. This is equivalent to setting the <span class="c007">b</span> flag
in the <span class="c007">OCAMLRUNPARAM</span> environment variable (see below).
</dd><dt class="dt-description"><span class="c019"><span class="c007">-I</span> <span class="c013">dir</span></span></dt><dd class="dd-description">
Search the directory <span class="c013">dir</span> for dynamically-loaded libraries,
in addition to the standard search path (see
section&nbsp;<a href="#s-ocamlrun-dllpath">10.3</a>).
</dd><dt class="dt-description"><span class="c010">-p</span></dt><dd class="dd-description">
Print the names of the primitives known to this version of
<span class="c007">ocamlrun</span> and exit.
</dd><dt class="dt-description"><span class="c010">-v</span></dt><dd class="dd-description">
Direct the memory manager to print some progress messages on
standard error. This is equivalent to setting <span class="c007">v=63</span> in the
<span class="c007">OCAMLRUNPARAM</span> environment variable (see below).
</dd><dt class="dt-description"><span class="c010">-version</span></dt><dd class="dd-description">
Print version string and exit.
</dd><dt class="dt-description"><span class="c010">-vnum</span></dt><dd class="dd-description">
Print short version number and exit.</dd></dl><p>The following environment variables are also consulted:</p><dl class="description"><dt class="dt-description">
<span class="c010">CAML_LD_LIBRARY_PATH</span></dt><dd class="dd-description"> Additional directories to search for
dynamically-loaded libraries (see section&nbsp;<a href="#s-ocamlrun-dllpath">10.3</a>).</dd><dt class="dt-description"><span class="c010">OCAMLLIB</span></dt><dd class="dd-description"> The directory containing the OCaml standard
library. (If <span class="c007">OCAMLLIB</span> is not set, <span class="c007">CAMLLIB</span> will be used instead.)
Used to locate the <span class="c007">ld.conf</span> configuration file for
dynamic loading (see section&nbsp;<a href="#s-ocamlrun-dllpath">10.3</a>). If not set,
default to the library directory specified when compiling OCaml.</dd><dt class="dt-description"><span class="c010">OCAMLRUNPARAM</span></dt><dd class="dd-description"> Set the runtime system options
and garbage collection parameters.
(If <span class="c007">OCAMLRUNPARAM</span> is not set, <span class="c007">CAMLRUNPARAM</span> will be used instead.)
This variable must be a sequence of parameter specifications.
A parameter specification is an option letter followed by an <span class="c007">=</span>
sign, a decimal number (or an hexadecimal number prefixed by <span class="c007">0x</span>),
and an optional multiplier. The options are documented below;
the last six correspond to the fields of the
<span class="c007">control</span> record documented in
<a href="../../api/4.01/Gc.html">Module <span class="c007">Gc</span></a>.
<dl class="description"><dt class="dt-description">
<span class="c019">b</span></dt><dd class="dd-description"> (backtrace) Trigger the printing of a stack backtrace
when an uncaught exception aborts the program.
This option takes no argument.
</dd><dt class="dt-description"><span class="c019">p</span></dt><dd class="dd-description"> (parser trace) Turn on debugging support for
<span class="c007">ocamlyacc</span>-generated parsers. When this option is on,
the pushdown automaton that executes the parsers prints a
trace of its actions. This option takes no argument.
</dd><dt class="dt-description"><span class="c019">R</span></dt><dd class="dd-description"> (randomize) Turn on randomization of all hash tables by default
(see
<a href="../../api/4.01/Hashtbl.html">Module <span class="c007">Hashtbl</span></a>).
This option takes no argument.
</dd><dt class="dt-description"><span class="c019">h</span></dt><dd class="dd-description"> The initial size of the major heap (in words).
</dd><dt class="dt-description"><span class="c019">s</span></dt><dd class="dd-description"> (<span class="c007">minor_heap_size</span>) Size of the minor heap. (in words)
</dd><dt class="dt-description"><span class="c019">i</span></dt><dd class="dd-description"> (<span class="c007">major_heap_increment</span>) Default size increment for the
major heap. (in words)
</dd><dt class="dt-description"><span class="c019">o</span></dt><dd class="dd-description"> (<span class="c007">space_overhead</span>) The major GC speed setting.
</dd><dt class="dt-description"><span class="c019">O</span></dt><dd class="dd-description"> (<span class="c007">max_overhead</span>) The heap compaction trigger setting.
</dd><dt class="dt-description"><span class="c019">v</span></dt><dd class="dd-description"> (<span class="c007">verbose</span>) What GC messages to print to stderr. This
is a sum of values selected from the following:
<dl class="description"><dt class="dt-description">
<span class="c019">1 (= 0x001)</span></dt><dd class="dd-description"> Start of major GC cycle.
</dd><dt class="dt-description"><span class="c019">2 (= 0x002)</span></dt><dd class="dd-description"> Minor collection and major GC slice.
</dd><dt class="dt-description"><span class="c019">4 (= 0x004)</span></dt><dd class="dd-description"> Growing and shrinking of the heap.
</dd><dt class="dt-description"><span class="c019">8 (= 0x008)</span></dt><dd class="dd-description"> Resizing of stacks and memory manager tables.
</dd><dt class="dt-description"><span class="c019">16 (= 0x010)</span></dt><dd class="dd-description"> Heap compaction.
</dd><dt class="dt-description"><span class="c019">32 (= 0x020)</span></dt><dd class="dd-description"> Change of GC parameters.
</dd><dt class="dt-description"><span class="c019">64 (= 0x040)</span></dt><dd class="dd-description"> Computation of major GC slice size.
</dd><dt class="dt-description"><span class="c019">128 (= 0x080)</span></dt><dd class="dd-description"> Calling of finalisation functions
</dd><dt class="dt-description"><span class="c019">256 (= 0x100)</span></dt><dd class="dd-description"> Startup messages (loading the bytecode
executable file, resolving shared libraries).
</dd></dl>
</dd><dt class="dt-description"><span class="c019">l</span></dt><dd class="dd-description"> (<span class="c007">stack_limit</span>) The limit (in words) of the stack size.
</dd></dl>
The multiplier is <span class="c007">k</span>, <span class="c007">M</span>, or <span class="c007">G</span>, for multiplication by 2<sup>10</sup>,
2<sup>20</sup>, and 2<sup>30</sup> respectively.
For example, on a 32-bit machine, under <span class="c007">bash</span> the command
<pre>        export OCAMLRUNPARAM='b,s=256k,v=0x015'
</pre> tells a subsequent <span class="c007">ocamlrun</span> to print backtraces for uncaught exceptions,
set its initial minor heap size to 1&nbsp;megabyte and
print a message at the start of each major GC cycle, when the heap
size changes, and when compaction is triggered.</dd><dt class="dt-description"><span class="c010">CAMLRUNPARAM</span></dt><dd class="dd-description"> If <span class="c007">OCAMLRUNPARAM</span> is not found in the
environment, then <span class="c007">CAMLRUNPARAM</span> will be used instead. If
<span class="c007">CAMLRUNPARAM</span> is not found, then the default values will be used.</dd><dt class="dt-description"><span class="c010">PATH</span></dt><dd class="dd-description"> List of directories searched to find the bytecode
executable file.
</dd></dl>
<h2 class="section" id="sec256">3&nbsp;&nbsp;Dynamic loading of shared libraries</h2>
<p> <a id="s-ocamlrun-dllpath"></a></p><p>On platforms that support dynamic loading, <span class="c007">ocamlrun</span> can link
dynamically with C shared libraries (DLLs) providing additional C primitives
beyond those provided by the standard runtime system. The names for
these libraries are provided at link time as described in
section&nbsp;<a href="intfc.html#dynlink-c-code">19.1.4</a>), and recorded in the bytecode executable
file; <span class="c007">ocamlrun</span>, then, locates these libraries and resolves references
to their primitives when the bytecode executable program starts.</p><p>The <span class="c007">ocamlrun</span> command searches shared libraries in the following
directories, in the order indicated:
</p><ol class="enumerate" type="1"><li class="li-enumerate">
Directories specified on the <span class="c007">ocamlrun</span> command line with the
<span class="c007">-I</span> option.
</li><li class="li-enumerate">Directories specified in the <span class="c007">CAML_LD_LIBRARY_PATH</span> environment
variable.
</li><li class="li-enumerate">Directories specified at link-time via the <span class="c007">-dllpath</span> option to
<span class="c007">ocamlc</span>. (These directories are recorded in the bytecode executable
file.)
</li><li class="li-enumerate">Directories specified in the file <span class="c007">ld.conf</span>. This file resides
in the OCaml standard library directory, and lists directory
names (one per line) to be searched. Typically, it contains only one
line naming the <span class="c007">stublibs</span> subdirectory of the OCaml standard
library directory. Users can add there the names of other directories
containing frequently-used shared libraries; however, for consistency
of installation, we recommend that shared libraries are installed
directly in the system <span class="c007">stublibs</span> directory, rather than adding lines
to the <span class="c007">ld.conf</span> file.
</li><li class="li-enumerate">Default directories searched by the system dynamic loader.
Under Unix, these generally include <span class="c007">/lib</span> and <span class="c007">/usr/lib</span>, plus the
directories listed in the file <span class="c007">/etc/ld.so.conf</span> and the environment
variable <span class="c007">LD_LIBRARY_PATH</span>. Under Windows, these include the Windows
system directories, plus the directories listed in the <span class="c007">PATH</span>
environment variable.
</li></ol>
<h2 class="section" id="sec257">4&nbsp;&nbsp;Common errors</h2>
<p>This section describes and explains the most frequently encountered
error messages.</p><dl class="description"><dt class="dt-description"><span class="c019"><span class="c013">filename</span><span class="c007">: no such file or directory</span></span></dt><dd class="dd-description">
If <span class="c013">filename</span> is the name of a self-executable bytecode file, this
means that either that file does not exist, or that it failed to run
the <span class="c007">ocamlrun</span> bytecode interpreter on itself. The second possibility
indicates that OCaml has not been properly installed on your
system.</dd><dt class="dt-description"><span class="c010">Cannot exec ocamlrun</span></dt><dd class="dd-description">
(When launching a self-executable bytecode file.) The <span class="c007">ocamlrun</span>
could not be found in the executable path. Check that OCaml
has been properly installed on your system.</dd><dt class="dt-description"><span class="c010">Cannot find the bytecode file</span></dt><dd class="dd-description">
The file that <span class="c007">ocamlrun</span> is trying to execute (e.g. the file given as
first non-option argument to <span class="c007">ocamlrun</span>) either does not exist, or is
not a valid executable bytecode file.</dd><dt class="dt-description"><span class="c010">Truncated bytecode file</span></dt><dd class="dd-description">
The file that <span class="c007">ocamlrun</span> is trying to execute is not a valid executable
bytecode file. Probably it has been truncated or mangled since
created. Erase and rebuild it.</dd><dt class="dt-description"><span class="c010">Uncaught exception</span></dt><dd class="dd-description">
The program being executed contains a “stray” exception. That is,
it raises an exception at some point, and this exception is never
caught. This causes immediate termination of the program. The name of
the exception is printed, along with its string and integer arguments
(arguments of more complex types are not correctly printed).
To locate the context of the uncaught exception, compile the program
with the <span class="c007">-g</span> option and either run it again under the <span class="c007">ocamldebug</span>
debugger (see chapter&nbsp;<a href="debugger.html#c%3Adebugger">16</a>), or run it with <span class="c007">ocamlrun -b</span>
or with the <span class="c007">OCAMLRUNPARAM</span> environment variable set to <span class="c007">b=1</span>.</dd><dt class="dt-description"><span class="c010">Out of memory</span></dt><dd class="dd-description">
The program being executed requires more memory than available. Either
the program builds excessively large data structures; or the program
contains too many nested function calls, and the stack overflows. In
some cases, your program is perfectly correct, it just requires more
memory than your machine provides. In other cases, the “out of
memory” message reveals an error in your program: non-terminating
recursive function, allocation of an excessively large array or
string, attempts to build an infinite list or other data structure,
…<p>To help you diagnose this error, run your program with the <span class="c007">-v</span> option
to <span class="c007">ocamlrun</span>, or with the <span class="c007">OCAMLRUNPARAM</span> environment variable set to
<span class="c007">v=63</span>. If it displays lots of “<span class="c007">Growing stack</span>…”
messages, this is probably a looping recursive function. If it
displays lots of “<span class="c007">Growing heap</span>…” messages, with the heap size
growing slowly, this is probably an attempt to construct a data
structure with too many (infinitely many?) cells. If it displays few
“<span class="c007">Growing heap</span>…” messages, but with a huge increment in the
heap size, this is probably an attempt to build an excessively large
array or string.</p></dd></dl>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>