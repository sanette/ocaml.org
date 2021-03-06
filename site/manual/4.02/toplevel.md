<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="comp.html">Batch compilation (ocamlc)</a></li><li class="active"><a href="toplevel.html">The toplevel system (ocaml)</a></li><li><a href="runtime.html">The runtime system (ocamlrun)</a></li><li><a href="native.html">Native-code compilation (ocamlopt)</a></li><li><a href="lexyacc.html">Lexer and parser generators (ocamllex, ocamlyacc)</a></li><li><a href="depend.html">Dependency generator (ocamldep)</a></li><li><a href="browser.html">The browser/editor (ocamlbrowser)</a></li><li><a href="ocamldoc.html">The documentation generator (ocamldoc)</a></li><li><a href="debugger.html">The debugger (ocamldebug)</a></li><li><a href="profil.html">Profiling (ocamlprof)</a></li><li><a href="ocamlbuild.html">The ocamlbuild compilation manager</a></li><li><a href="intfc.html">Interfacing C with OCaml</a></li></ul>




<h1 class="chapter" id="sec254"><span>Chapter 9</span>&nbsp;&nbsp;The toplevel system (ocaml)</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.02</a></div><div class="toc_title"><a href="#">The toplevel system (ocaml)</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="toplevel.html#sec255">Options</a>
</li><li><a href="toplevel.html#sec256">Toplevel directives</a>
</li><li><a href="toplevel.html#sec257">The toplevel and the module system</a>
</li><li><a href="toplevel.html#sec258">Common errors</a>
</li><li><a href="toplevel.html#sec259">Building custom toplevel systems: <span class="c007">ocamlmktop</span></a>
</li><li><a href="toplevel.html#sec260">Options</a>
</li></ul></nav></header>
<p> <a id="c:camllight"></a>

</p><p>This chapter describes the toplevel system for OCaml, that permits
interactive use of the OCaml system
through a read-eval-print loop. In this mode, the system repeatedly
reads OCaml phrases from the input, then typechecks, compile and
evaluate them, then prints the inferred type and result value, if
any. The system prints a <span class="c007">#</span> (sharp) prompt before reading each
phrase.</p><p>Input to the toplevel can span several lines. It is terminated by <span class="c008">;;</span> (a
double-semicolon). The toplevel input consists in one or several
toplevel phrases, with the following syntax:</p><table class="display dcenter"><tbody><tr class="c026"><td class="dcell"><table class="c002 cellpading0"><tbody><tr><td class="c025">
<a class="syntax" id="toplevel-input"><span class="c014">toplevel-input</span></a></td><td class="c022">::=</td><td class="c024">
{&nbsp;<a class="syntax" href="modules.html#definition"><span class="c014">definition</span></a>&nbsp;}<sup>+</sup>&nbsp;<span class="c008">;;</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="expr.html#expr"><span class="c014">expr</span></a>&nbsp;<span class="c008">;;</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">#</span>&nbsp;<a class="syntax" href="lex.html#ident"><span class="c014">ident</span></a>&nbsp;&nbsp;[&nbsp;<a class="syntax" href="#directive-argument"><span class="c014">directive-argument</span></a>&nbsp;]&nbsp;<span class="c008">;;</span>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td></tr>
<tr><td class="c025">
<a class="syntax" id="directive-argument"><span class="c014">directive-argument</span></a></td><td class="c022">::=</td><td class="c024">
<a class="syntax" href="lex.html#string-literal"><span class="c014">string-literal</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="lex.html#integer-literal"><span class="c014">integer-literal</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<a class="syntax" href="names.html#value-path"><span class="c014">value-path</span></a>
&nbsp;</td></tr>
<tr><td class="c025">&nbsp;</td><td class="c022">∣</td><td class="c024">&nbsp;<span class="c008">true</span>&nbsp;∣&nbsp;&nbsp;<span class="c008">false</span>
</td></tr>
</tbody></table></td></tr>
</tbody></table><p>A phrase can consist of a definition, like those found in
implementations of compilation units or in <span class="c008">struct</span> … <span class="c008">end</span>
module expressions. The definition can bind value names, type names,
an exception, a module name, or a module type name. The toplevel
system performs the bindings, then prints the types and values (if
any) for the names thus defined.</p><p>A phrase may also consist in a value expression
(section&nbsp;<a href="expr.html#s%3Avalue-expr">6.7</a>). It is simply evaluated
without performing any bindings, and its value is
printed.</p><p>Finally, a phrase can also consist in a toplevel directive,
starting with <span class="c008">#</span> (the sharp sign). These directives control the
behavior of the toplevel; they are listed below in
section&nbsp;<a href="#s%3Atoplevel-directives">9.2</a>.</p><blockquote class="quote"><span class="c011">Unix:</span>&nbsp;&nbsp;
The toplevel system is started by the command <span class="c007">ocaml</span>, as follows:
<pre>        ocaml <span class="c013">options objects</span>                # interactive mode
        ocaml <span class="c013">options objects scriptfile</span>        # script mode
</pre>
<span class="c013">options</span> are described below.
<span class="c013">objects</span> are filenames ending in <span class="c007">.cmo</span> or <span class="c007">.cma</span>; they are
loaded into the interpreter immediately after <span class="c013">options</span> are set.
<span class="c013">scriptfile</span> is any file name not ending in <span class="c007">.cmo</span> or <span class="c007">.cma</span>.<p>If no <span class="c013">scriptfile</span> is given on the command line, the toplevel system
enters interactive mode: phrases are read on standard input, results
are printed on standard output, errors on standard error. End-of-file
on standard input terminates <span class="c007">ocaml</span> (see also the <span class="c007">#quit</span> directive
in section&nbsp;<a href="#s%3Atoplevel-directives">9.2</a>).</p><p>On start-up (before the first phrase is read), if the file
<span class="c007">.ocamlinit</span> exists in the current directory,
its contents are read as a sequence of OCaml phrases
and executed as per the <span class="c007">#use</span> directive
described in section&nbsp;<a href="#s%3Atoplevel-directives">9.2</a>.
The evaluation outcode for each phrase are not displayed.
If the current directory does not contain an <span class="c007">.ocamlinit</span> file, but
the user’s home directory (environment variable <span class="c007">HOME</span>) does, the
latter is read and executed as described below.</p><p>The toplevel system does not perform line editing, but it can
easily be used in conjunction with an external line editor such as
<span class="c007">ledit</span>, <span class="c007">ocaml2</span> or <span class="c007">rlwrap</span>


(see the
<a href="http://caml.inria.fr/humps/index_framed_caml.html">Caml Hump</a>).

Another option is to use <span class="c007">ocaml</span> under Gnu Emacs, which gives the
full editing power of Emacs (command <span class="c007">run-caml</span> from library <span class="c007">inf-caml</span>).</p><p>At any point, the parsing, compilation or evaluation of the current
phrase can be interrupted by pressing <span class="c007">ctrl-C</span> (or, more precisely,
by sending the <span class="c007">INTR</span> signal to the <span class="c007">ocaml</span> process). The toplevel
then immediately returns to the <span class="c007">#</span> prompt.</p><p>If <span class="c013">scriptfile</span> is given on the command-line to <span class="c007">ocaml</span>, the toplevel
system enters script mode: the contents of the file are read as a
sequence of OCaml phrases and executed, as per the <span class="c007">#use</span>
directive (section&nbsp;<a href="#s%3Atoplevel-directives">9.2</a>). The outcome of the
evaluation is not printed. On reaching the end of file, the <span class="c007">ocaml</span>
command exits immediately. No commands are read from standard input.
<span class="c007">Sys.argv</span> is transformed, ignoring all OCaml parameters, and
starting with the script file name in <span class="c007">Sys.argv.(0)</span>.</p><p>In script mode, the first line of the script is ignored if it starts
with <span class="c007">#!</span>. Thus, it should be possible to make the script
itself executable and put as first line <span class="c007">#!/usr/local/bin/ocaml</span>,
thus calling the toplevel system automatically when the script is
run. However, <span class="c007">ocaml</span> itself is a <span class="c007">#!</span> script on most installations
of OCaml, and Unix kernels usually do not handle nested <span class="c007">#!</span>
scripts. A better solution is to put the following as the first line
of the script:
</p><pre>        #!/usr/local/bin/ocamlrun /usr/local/bin/ocaml
</pre></blockquote><blockquote class="quote"><span class="c011">Windows:</span>&nbsp;&nbsp;
In addition to the text-only command <span class="c007">ocaml.exe</span>, which works exactly
as under Unix (see above), a graphical user interface for the
toplevel is available under the name <span class="c007">ocamlwin.exe</span>. It should be
launched from the Windows file manager or program manager.
This interface provides a text window in which commands can be entered
and edited, and the toplevel responses are printed.
</blockquote>
<h2 class="section" id="sec255">1&nbsp;&nbsp;Options</h2>
<p> <a id="s:toplevel-options"></a></p><p>The following command-line options are recognized by the <span class="c007">ocaml</span> command.</p><dl class="description"><dt class="dt-description"><span class="c010">-absname</span></dt><dd class="dd-description">
Force error messages to show absolute paths for file names.</dd><dt class="dt-description"><span class="c019"><span class="c007">-I</span> <span class="c013">directory</span></span></dt><dd class="dd-description">
Add the given directory to the list of directories searched for
source and compiled files. By default, the current directory is
searched first, then the standard library directory. Directories added
with <span class="c007">-I</span> are searched after the current directory, in the order in
which they were given on the command line, but before the standard
library directory.<p>If the given directory starts with <span class="c007">+</span>, it is taken relative to the
standard library directory. For instance, <span class="c007">-I +labltk</span> adds the
subdirectory <span class="c007">labltk</span> of the standard library to the search path.</p><p>Directories can also be added to the list once
the toplevel is running with the <span class="c007">#directory</span> directive
(section&nbsp;<a href="#s%3Atoplevel-directives">9.2</a>).</p></dd><dt class="dt-description"><span class="c019"><span class="c007">-init</span> <span class="c013">file</span></span></dt><dd class="dd-description">
Load the given file instead of the default initialization file.
The default file is <span class="c007">.ocamlinit</span> in the current directory if it
exists, otherwise <span class="c007">.ocamlinit</span> in the user’s home directory.</dd><dt class="dt-description"><span class="c010">-labels</span></dt><dd class="dd-description">
Labels are not ignored in types, labels may be used in applications,
and labelled parameters can be given in any order. This is the default.</dd><dt class="dt-description"><span class="c010">-no-app-funct</span></dt><dd class="dd-description">
Deactivates the applicative behaviour of functors. With this option,
each functor application generates new types in its result and
applying the same functor twice to the same argument yields two
incompatible structures.</dd><dt class="dt-description"><span class="c010">-noassert</span></dt><dd class="dd-description">
Do not compile assertion checks. Note that the special form
<span class="c007">assert false</span> is always compiled because it is typed specially.</dd><dt class="dt-description"><span class="c010">-nolabels</span></dt><dd class="dd-description">
Ignore non-optional labels in types. Labels cannot be used in
applications, and parameter order becomes strict.</dd><dt class="dt-description"><span class="c010">-noprompt</span></dt><dd class="dd-description">
Do not display any prompt when waiting for input.</dd><dt class="dt-description"><span class="c010">-nopromptcont</span></dt><dd class="dd-description">
Do not display the secondary prompt when waiting for continuation
lines in multi-line inputs. This should be used e.g. when running
<span class="c007">ocaml</span> in an <span class="c007">emacs</span> window.</dd><dt class="dt-description"><span class="c010">-nostdlib</span></dt><dd class="dd-description">
Do not include the standard library directory in the list of
directories searched for source and compiled files.</dd><dt class="dt-description"><span class="c019"><span class="c007">-ppx</span> <span class="c013">command</span></span></dt><dd class="dd-description">
After parsing, pipe the abstract syntax tree through the preprocessor
<span class="c013">command</span>. The format of the input and ouput of the preprocessor
are not yet documented.</dd><dt class="dt-description"><span class="c010">-principal</span></dt><dd class="dd-description">
Check information paths during type-checking, to make sure that all
types are derived in a principal way. When using labelled arguments
and/or polymorphic methods, this flag is required to ensure future
versions of the compiler will be able to infer types correctly, even
if internal algorithms change.
All programs accepted in <span class="c007">-principal</span> mode are also accepted in the
default mode with equivalent types, but different binary signatures,
and this may slow down type checking; yet it is a good idea to
use it once before publishing source code.</dd><dt class="dt-description"><span class="c010">-rectypes</span></dt><dd class="dd-description">
Allow arbitrary recursive types during type-checking. By default,
only recursive types where the recursion goes through an object type
are supported.</dd><dt class="dt-description"><span class="c010">-safe-string</span></dt><dd class="dd-description">
Enforce the separation between types <span class="c007">string</span> and <span class="c007">bytes</span>,
thereby making strings read-only. This will become the default in
a future version of OCaml.</dd><dt class="dt-description"><span class="c010">-short-paths</span></dt><dd class="dd-description">
When a type is visible under several module-paths, use the shortest
one when printing the type’s name in inferred interfaces and error and
warning messages.</dd><dt class="dt-description"><span class="c010">-stdin</span></dt><dd class="dd-description">
Read the standard input as a script file rather than starting an
interactive session.</dd><dt class="dt-description"><span class="c010">-strict-sequence</span></dt><dd class="dd-description">
Force the left-hand part of each sequence to have type unit.</dd><dt class="dt-description"><span class="c010">-strict-formats</span></dt><dd class="dd-description">
Reject invalid formats that were accepted in legacy format
implementations. You should use this flag to detect and fix such
invalid formats, as they will be rejected by future OCaml versions.</dd><dt class="dt-description"><span class="c010">-unsafe</span></dt><dd class="dd-description">
See the corresponding option for <span class="c007">ocamlc</span>, chapter&nbsp;<a href="comp.html#c%3Acamlc">8</a>.
Turn bound checking off on array and string accesses (the <span class="c007">v.(i)</span> and
<span class="c007">s.[i]</span> constructs). Programs compiled with <span class="c007">-unsafe</span> are therefore
slightly faster, but unsafe: anything can happen if the program
accesses an array or string outside of its bounds.</dd><dt class="dt-description"><span class="c010">-unsafe-string</span></dt><dd class="dd-description">
Identify the types <span class="c007">string</span> and <span class="c007">bytes</span>,
thereby making strings writable. For reasons of backward compatibility,
this is the default setting for the moment, but this will change in a future
version of OCaml.</dd><dt class="dt-description"><span class="c010">-version</span></dt><dd class="dd-description">
Print version string and exit.</dd><dt class="dt-description"><span class="c010">-vnum</span></dt><dd class="dd-description">
Print short version number and exit.</dd><dt class="dt-description"><span class="c019"><span class="c007">-w</span> <span class="c013">warning-list</span></span></dt><dd class="dd-description">
Enable or disable warnings according to the argument <span class="c013">warning-list</span>.
See section&nbsp;<a href="comp.html#s%3Acomp-options">8.2</a> for the syntax of the argument.</dd><dt class="dt-description"><span class="c019"><span class="c007">-warn-error</span> <span class="c013">warning-list</span></span></dt><dd class="dd-description">
Mark as fatal the warnings enabled by the argument <span class="c013">warning-list</span>.
See section&nbsp;<a href="comp.html#s%3Acomp-options">8.2</a> for the syntax of the argument.</dd><dt class="dt-description"><span class="c010">-warn-help</span></dt><dd class="dd-description">
Show the description of all available warning numbers.</dd><dt class="dt-description"><span class="c019"><span class="c007">-</span> <span class="c013">file</span></span></dt><dd class="dd-description">
Use <span class="c013">file</span> as a script file name, even when it starts with a
hyphen (-).</dd><dt class="dt-description"><span class="c019"><span class="c007">-help</span> or <span class="c007">--help</span></span></dt><dd class="dd-description">
Display a short usage summary and exit.
</dd></dl><blockquote class="quote"><span class="c011">Unix:</span>&nbsp;&nbsp;
The following environment variables are also consulted:
<dl class="description"><dt class="dt-description">
<span class="c010">LC_CTYPE</span></dt><dd class="dd-description"> If set to <span class="c007">iso_8859_1</span>, accented characters (from the
ISO Latin-1 character set) in string and character literals are
printed as is; otherwise, they are printed as decimal escape sequences
(<span class="c007">\</span><span class="c013">ddd</span>).</dd><dt class="dt-description"><span class="c010">TERM</span></dt><dd class="dd-description"> When printing error messages, the toplevel system
attempts to underline visually the location of the error. It
consults the <span class="c007">TERM</span> variable to determines the type of output terminal
and look up its capabilities in the terminal database.</dd><dt class="dt-description"><span class="c010">HOME</span></dt><dd class="dd-description"> Directory where the <span class="c007">.ocamlinit</span> file is searched.
</dd></dl>
</blockquote>
<h2 class="section" id="sec256">2&nbsp;&nbsp;Toplevel directives</h2>
<p>
<a id="s:toplevel-directives"></a></p><p>The following directives control the toplevel behavior, load files in
memory, and trace program execution.</p><p><span class="c019">Note:</span> all directives start with a <span class="c007">#</span> (sharp) symbol. This <span class="c007">#</span>
must be typed before the directive, and must not be confused with the
<span class="c007">#</span> prompt displayed by the interactive loop. For instance,
typing <span class="c007">#quit;;</span> will exit the toplevel loop, but typing <span class="c007">quit;;</span>
will result in an “unbound value <span class="c007">quit</span>” error.</p><dl class="description"><dt class="dt-description"><span class="c010">#quit;;</span></dt><dd class="dd-description">
Exit the toplevel loop and terminate the <span class="c007">ocaml</span> command.</dd><dt class="dt-description"><span class="c019"><span class="c007">#labels </span><span class="c013">bool</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Ignore labels in function types if argument is <span class="c007">false</span>, or switch back
to default behaviour (commuting style) if argument is <span class="c007">true</span>.</dd><dt class="dt-description"><span class="c019"><span class="c007">#principal </span><span class="c013">bool</span><span class="c007">;;</span></span></dt><dd class="dd-description">
If the argument is <span class="c007">true</span>, check information paths during
type-checking, to make sure that all types are derived in a principal
way. If the argument is <span class="c007">false</span>, do not check information paths.</dd><dt class="dt-description"><span class="c010">#rectypes;;</span></dt><dd class="dd-description">
Allow arbitrary recursive types during type-checking. Note: once
enabled, this option cannot be disabled because that would lead to
unsoundness of the type system.</dd><dt class="dt-description"><span class="c019"><span class="c007">#warnings "</span><span class="c013">warning-list</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Enable or disable warnings according to the argument.</dd><dt class="dt-description"><span class="c019"><span class="c007">#warn_error "</span><span class="c013">warning-list</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Treat as errors the warnings enabled by the argument and as normal
warnings the warnings disabled by the argument.</dd><dt class="dt-description"><span class="c019"><span class="c007">#directory "</span><span class="c013">dir-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Add the given directory to the list of directories searched for
source and compiled files.</dd><dt class="dt-description"><span class="c019"><span class="c007">#remove_directory "</span><span class="c013">dir-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Remove the given directory from the list of directories searched for
source and compiled files. Do nothing if the list does not contain
the given directory.</dd><dt class="dt-description"><span class="c019"><span class="c007">#cd "</span><span class="c013">dir-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Change the current working directory.</dd><dt class="dt-description"><span class="c019"><span class="c007">#load "</span><span class="c013">file-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Load in memory a bytecode object file (<span class="c007">.cmo</span> file) or library file
(<span class="c007">.cma</span> file) produced by the batch compiler <span class="c007">ocamlc</span>.</dd><dt class="dt-description"><span class="c019"><span class="c007">#load_rec "</span><span class="c013">file-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Load in memory a bytecode object file (<span class="c007">.cmo</span> file) or library file
(<span class="c007">.cma</span> file) produced by the batch compiler <span class="c007">ocamlc</span>.
When loading an object file that depends on other modules
which have not been loaded yet, the .cmo files for these modules
are searched and loaded as well, recursively. The loading order
is not specified.</dd><dt class="dt-description"><span class="c019"><span class="c007">#use "</span><span class="c013">file-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Read, compile and execute source phrases from the given file.
This is textual inclusion: phrases are processed just as if
they were typed on standard input. The reading of the file stops at
the first error encountered.</dd><dt class="dt-description"><span class="c019"><span class="c007">#mod_use "</span><span class="c013">file-name</span><span class="c007">";;</span></span></dt><dd class="dd-description">
Similar to <span class="c007">#use</span> but also wrap the code into a top-level module of the
same name as capitalized file name without extensions, following
semantics of the compiler.</dd><dt class="dt-description"><span class="c019"><span class="c007">#install_printer </span><span class="c013">printer-name</span><span class="c007">;;</span></span></dt><dd class="dd-description">
This directive registers the function named <span class="c013">printer-name</span> (a
value path) as a printer for values whose types match the argument
type of the function. That is, the toplevel loop will call
<span class="c013">printer-name</span> when it has such a value to print.<p>The printing function <span class="c013">printer-name</span> should have type
<span class="c005"><span class="c007">Format.formatter</span> <span class="c007">-&gt;</span> <span class="c014">t</span> <span class="c007">-&gt;</span> <span class="c007">unit</span></span>, where <span class="c014">t</span> is the
type for the values to be printed, and should output its textual
representation for the value of type <span class="c014">t</span> on the given formatter,
using the functions provided by the <span class="c007">Format</span> library. For backward
compatibility, <span class="c013">printer-name</span> can also have type
<span class="c014">t</span> <span class="c005"><span class="c007">-&gt;</span> <span class="c007">unit</span></span> and should then output on the standard
formatter, but this usage is deprecated.</p></dd><dt class="dt-description"><span class="c019"><span class="c007">#remove_printer </span><span class="c013">printer-name</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Remove the named function from the table of toplevel printers.</dd><dt class="dt-description"><span class="c019"><span class="c007">#trace </span><span class="c013">function-name</span><span class="c007">;;</span></span></dt><dd class="dd-description">
After executing this directive, all calls to the function named
<span class="c013">function-name</span> will be “traced”. That is, the argument and the
result are displayed for each call, as well as the exceptions escaping
out of the function, raised either by the function itself or by
another function it calls. If the function is curried, each argument
is printed as it is passed to the function.</dd><dt class="dt-description"><span class="c019"><span class="c007">#untrace </span><span class="c013">function-name</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Stop tracing the given function.</dd><dt class="dt-description"><span class="c010">#untrace_all;;</span></dt><dd class="dd-description">
Stop tracing all functions traced so far.</dd><dt class="dt-description"><span class="c019"><span class="c007">#print_depth </span><span class="c013">n</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Limit the printing of values to a maximal depth of <span class="c013">n</span>.
The parts of values whose depth exceeds <span class="c013">n</span> are printed as <span class="c007">...</span>
(ellipsis).</dd><dt class="dt-description"><span class="c019"><span class="c007">#print_length </span><span class="c013">n</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Limit the number of value nodes printed to at most <span class="c013">n</span>.
Remaining parts of values are printed as <span class="c007">...</span> (ellipsis).</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_val </span><span class="c013">value-path</span><span class="c007">;;</span></span></dt><dd class="dd-description">
</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_type </span><span class="c013">typeconstr</span><span class="c007">;;</span></span></dt><dd class="dd-description">
</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_module </span><span class="c013">module-path</span><span class="c007">;;</span></span></dt><dd class="dd-description">
</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_module_type </span><span class="c013">modtype-path</span><span class="c007">;;</span></span></dt><dd class="dd-description">
</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_class </span><span class="c013">class-path</span><span class="c007">;;</span></span></dt><dd class="dd-description">
</dd><dt class="dt-description"><span class="c019"><span class="c007">#show_class_type </span><span class="c013">class-path</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Print the signature of the corresponding component.</dd><dt class="dt-description"><span class="c019"><span class="c007">#show </span><span class="c013">ident</span><span class="c007">;;</span></span></dt><dd class="dd-description">
Print the signatures of components with name <span class="c013">ident</span> in all the
above categories.</dd></dl>
<h2 class="section" id="sec257">3&nbsp;&nbsp;The toplevel and the module system</h2>
<p> <a id="s:toplevel-modules"></a></p><p>Toplevel phrases can refer to identifiers defined in compilation units
with the same mechanisms as for separately compiled units: either by
using qualified names (<span class="c007">Modulename.localname</span>), or by using
the <span class="c007">open</span> construct and unqualified names (see section&nbsp;<a href="names.html#s%3Anames">6.3</a>).</p><p>However, before referencing another compilation unit, an
implementation of that unit must be present in memory.
At start-up, the toplevel system contains implementations for all the
modules in the the standard library. Implementations for user modules
can be entered with the <span class="c007">#load</span> directive described above. Referencing
a unit for which no implementation has been provided
results in the error <span class="c007">Reference to undefined global `...'</span>.</p><p>Note that entering <span class="c007">open </span><span class="c013">Mod</span> merely accesses the compiled
interface (<span class="c007">.cmi</span> file) for <span class="c013">Mod</span>, but does not load the
implementation of <span class="c013">Mod</span>, and does not cause any error if no
implementation of <span class="c013">Mod</span> has been loaded. The error
“reference to undefined global <span class="c013">Mod</span>” will occur only when
executing a value or module definition that refers to <span class="c013">Mod</span>.</p>
<h2 class="section" id="sec258">4&nbsp;&nbsp;Common errors</h2>
<p>This section describes and explains the most frequently encountered
error messages.</p><dl class="description"><dt class="dt-description"><span class="c019">Cannot find file <span class="c013">filename</span></span></dt><dd class="dd-description">
The named file could not be found in the current directory, nor in the
directories of the search path.<p>If <span class="c013">filename</span> has the format <span class="c013">mod</span><span class="c007">.cmi</span>, this
means you have referenced the compilation unit <span class="c013">mod</span>, but its
compiled interface could not be found. Fix: compile <span class="c013">mod</span><span class="c007">.mli</span> or
<span class="c013">mod</span><span class="c007">.ml</span> first, to create the compiled interface <span class="c013">mod</span><span class="c007">.cmi</span>.</p><p>If <span class="c013">filename</span> has the format <span class="c013">mod</span><span class="c007">.cmo</span>, this
means you are trying to load with <span class="c007">#load</span> a bytecode object file that
does not exist yet. Fix: compile <span class="c013">mod</span><span class="c007">.ml</span> first.</p><p>If your program spans several directories, this error can also appear
because you haven’t specified the directories to look into. Fix: use
the <span class="c007">#directory</span> directive to add the correct directories to the
search path.</p></dd><dt class="dt-description"><span class="c019">This expression has type </span><span class="c013">t</span><sub>1</sub><span class="c019">, but is used with type </span><span class="c013">t</span><sub>2</sub></dt><dd class="dd-description">
See section&nbsp;<a href="comp.html#s%3Acomp-errors">8.4</a>.</dd><dt class="dt-description"><span class="c019">Reference to undefined global <span class="c013">mod</span></span></dt><dd class="dd-description">
You have neglected to load in memory an implementation for a module
with <span class="c007">#load</span>. See section&nbsp;<a href="#s%3Atoplevel-modules">9.3</a> above.</dd></dl>
<h2 class="section" id="sec259">5&nbsp;&nbsp;Building custom toplevel systems: <span class="c007">ocamlmktop</span></h2>
<p>The <span class="c007">ocamlmktop</span> command builds OCaml toplevels that
contain user code preloaded at start-up.</p><p>The <span class="c007">ocamlmktop</span> command takes as argument a set of <span class="c007">.cmo</span> and <span class="c007">.cma</span>
files, and links them with the object files that implement the OCaml toplevel.
The typical use is:
</p><pre>        ocamlmktop -o mytoplevel foo.cmo bar.cmo gee.cmo
</pre><p>This creates the bytecode file <span class="c007">mytoplevel</span>, containing the OCaml toplevel
system, plus the code from the three <span class="c007">.cmo</span>
files. This toplevel is directly executable and is started by:
</p><pre>        ./mytoplevel
</pre><p>This enters a regular toplevel loop, except that the code from
<span class="c007">foo.cmo</span>, <span class="c007">bar.cmo</span> and <span class="c007">gee.cmo</span> is already loaded in memory, just as
if you had typed:
</p><pre>        #load "foo.cmo";;
        #load "bar.cmo";;
        #load "gee.cmo";;
</pre><p>on entrance to the toplevel. The modules <span class="c007">Foo</span>, <span class="c007">Bar</span> and <span class="c007">Gee</span> are
not opened, though; you still have to do
</p><pre>        open Foo;;
</pre><p>yourself, if this is what you wish.</p>
<h2 class="section" id="sec260">6&nbsp;&nbsp;Options</h2>
<p>The following command-line options are recognized by <span class="c007">ocamlmktop</span>.</p><dl class="description"><dt class="dt-description"><span class="c019"><span class="c007">-cclib</span> <span class="c013">libname</span></span></dt><dd class="dd-description">
Pass the <span class="c007">-l</span><span class="c013">libname</span> option to the C linker when linking in
“custom runtime” mode. See the corresponding option for
<span class="c007">ocamlc</span>, in chapter&nbsp;<a href="comp.html#c%3Acamlc">8</a>.</dd><dt class="dt-description"><span class="c019"><span class="c007">-ccopt</span> <span class="c013">option</span></span></dt><dd class="dd-description">
Pass the given option to the C compiler and linker, when linking in
“custom runtime” mode. See the corresponding option for
<span class="c007">ocamlc</span>, in chapter&nbsp;<a href="comp.html#c%3Acamlc">8</a>.</dd><dt class="dt-description"><span class="c010">-custom</span></dt><dd class="dd-description">
Link in “custom runtime” mode. See the corresponding option for
<span class="c007">ocamlc</span>, in chapter&nbsp;<a href="comp.html#c%3Acamlc">8</a>.</dd><dt class="dt-description"><span class="c019"><span class="c007">-I</span> <span class="c013">directory</span></span></dt><dd class="dd-description">
Add the given directory to the list of directories searched for
compiled object code files (<span class="c007">.cmo</span> and <span class="c007">.cma</span>).</dd><dt class="dt-description"><span class="c019"><span class="c007">-o</span> <span class="c013">exec-file</span></span></dt><dd class="dd-description">
Specify the name of the toplevel file produced by the linker.
The default is <span class="c007">a.out</span>.</dd></dl>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>