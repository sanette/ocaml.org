<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="comp.html">Batch compilation (ocamlc)</a></li><li><a href="toplevel.html">The toplevel system (ocaml)</a></li><li><a href="runtime.html">The runtime system (ocamlrun)</a></li><li><a href="native.html">Native-code compilation (ocamlopt)</a></li><li><a href="lexyacc.html">Lexer and parser generators (ocamllex, ocamlyacc)</a></li><li><a href="depend.html">Dependency generator (ocamldep)</a></li><li><a href="browser.html">The browser/editor (ocamlbrowser)</a></li><li><a href="ocamldoc.html">The documentation generator (ocamldoc)</a></li><li><a href="debugger.html">The debugger (ocamldebug)</a></li><li><a href="profil.html">Profiling (ocamlprof)</a></li><li class="active"><a href="ocamlbuild.html">The ocamlbuild compilation manager</a></li><li><a href="intfc.html">Interfacing C with OCaml</a></li></ul>




<h1 class="chapter" id="sec370"><span>Chapter 18</span>&nbsp;&nbsp;The ocamlbuild compilation manager</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.01</a></div><div class="toc_title"><a href="#">The ocamlbuild compilation manager</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="ocamlbuild.html#sec371">Features of <span class="c007">ocamlbuild</span></a>
</li><li><a href="ocamlbuild.html#sec372">Limitations</a>
</li><li><a href="ocamlbuild.html#sec373">Using <span class="c007">ocamlbuild</span></a>
</li><li><a href="ocamlbuild.html#sec402">Appendix: Motivations</a>
</li><li><a href="ocamlbuild.html#sec403">Appendix: Summary of default rules</a>
</li></ul></nav></header>
<p> <a id="c:ocamlbuild"></a>

</p><p></p><p><br>
<br>
</p><p><span class="c007">ocamlbuild</span> is a tool automating the compilation of most OCaml projects with minimal
user input. Its use is not restricted to projects having a simple structure –
the extra effort needed to make it work with the more complex projects is in
reasonable proportion with their added complexity. In practice, one will use a
set of small text files, and, if needed, an OCaml compilation module that can
fine-tune the behaviour and define custom rules.</p>
<h2 class="section" id="sec371">1&nbsp;&nbsp;Features of <span class="c007">ocamlbuild</span></h2>
<p>
<em>This section is intended to read like a sales brochure or a datasheet.</em></p><ul class="itemize"><li class="li-itemize">
Built-in compilation rules for OCaml projects handle all the nasty cases:
native and byte-code, missing <span class="c007">.mli</span> files, preprocessor rules,
libraries, package (-pack) debugging and profiling flags, C stubs.
</li><li class="li-itemize">Plugin mechanism for writing compilation rules and actions in a real programming language,
OCaml itself.
</li><li class="li-itemize">Automatic inference of dependencies.
</li><li class="li-itemize">Correct handling of dynamically discovered dependencies.
</li><li class="li-itemize">Object files and other temporary files are created in a specific directory, leaving your main directory uncluttered.
</li><li class="li-itemize">Sanity checks ensure that object files are where they are supposed to be: in the build directory.
</li><li class="li-itemize">Regular projects are built using a single command with no extra files.
</li><li class="li-itemize">Parallel compilation to speed up things on multi-core systems.
</li><li class="li-itemize">Sophisticated display mode to keep your screen free of boring and repetitive compilation message
while giving you important progress information in a glimpse, and correctly multiplexing the error messages.
</li><li class="li-itemize">Tags and flags provide a concise and convenient mechanism for automatic selection of compilation, preprocessing and
other options.
</li><li class="li-itemize">Extended shell-like glob patterns, that can be combined using boolean operators,
allow you to concisely define the tags that apply to a given file.
</li><li class="li-itemize">Mechanisms for defining the mutual visibility of subdirectories.
</li><li class="li-itemize">Cache mechanism avoiding unnecessary compilations where reasonably computable.
</li></ul>
<h2 class="section" id="sec372">2&nbsp;&nbsp;Limitations</h2>
<p>
<em>Not perfect nor complete yet, but already pretty damn useful.</em></p><p>We were not expecting to write the ultimate compilation tool in a few man-months, however we believe we have
a tool that solves many compilation problems, especially our own, in a satisfactory way. Hence there are a
lot of missing features, incomplete options and hideous bugs lurking in <span class="c007">ocamlbuild</span>, and we hope that the OCaml community
will find our first try at <span class="c007">ocamlbuild</span> useful and hopefully help it grow into a tool that satisfies most needs of most users
by providing feedback, bug reports and patches.</p><p>The plugin API maybe somewhat lacking in maturity, as it has only been tested
by a few people. We believe a good API can only evolve under pressure from
many peers and the courage to rewrite things cleanly when time is ripe by the
developers. Most of the important functions a user will need are encapsulated
in the plugin API, which is the <span class="c007">Ocamlbuild_plugin</span> module pack. We
intend to keep that API backwards compatible. It may happen that intricate
projects need features not available in that module – you may then use
functions or values directly from the core <span class="c007">ocamlbuild</span> modules. We ask you to report
such usage to the authors so that we may make the necessary changes to the API;
you may also want to isolate calls to the non-API parts of the <span class="c007">ocamlbuild</span> library
from the rest of your plugin to be able to keep the later when incompatible
changes arise.</p><p>The way that <span class="c007">ocamlbuild</span> handles the command-line options, the <span class="c007">_tags</span> file,
the target names, names of the tags, and so on, are not expected to change in
incompatible ways. We intend to keep a project that compiles without a plugin
compilable without modifications in the future.
</p>
<h2 class="section" id="sec373">3&nbsp;&nbsp;Using <span class="c007">ocamlbuild</span></h2>
<p>
<em>Learn how to use <span class="c007">ocamlbuild</span> with short, specific, straight-to-the-point examples.</em></p><p>The amount of time and effort spent on the compilation process of a project
should be proportionate to that spent on the project itself. It should be easy
to set up a small project, maybe a little harder for a medium-sized project,
and it may take some more time, but not too much, for a big project. Ideally
setting up a big project would be as easy as setting up a small project. However,
as projects grow, modularization techniques start to be used, and the probability
of using meta programming or multiple programming languages increases, thus making
the compilation process more delicate.</p><p><span class="c007">ocamlbuild</span> is intended to be very easy to use for projects, large or small, with a simple
compilation process: typing
<span class="c007">ocamlbuild foo.native</span> should be enough to compile the native version
of a program whose top module is <span class="c007">foo.ml</span> and whose dependencies are in
the same directory. As your project gets more complex, you will gradually
start to use command-line options to specify libraries to link with, then
configuration files, ultimately culminating in a custom OCaml plugin for
complex projects with arbitrary dependencies and actions.</p>
<h3 class="subsection" id="sec374">3.1&nbsp;&nbsp;Hygiene &amp; where is my code ?</h3>
<p>
Your code is in the <span class="c007">_build</span> directory, but <span class="c007">ocamlbuild</span> automatically creates
a symbolic link to the executables it produces in the current directory.
<span class="c007">ocamlbuild</span> copies the source files and compiles them in a separate directory
which is <span class="c007">_build</span> by default.</p><p>For <span class="c007">ocamlbuild</span>, any file that is not in the build directory is a source file.
It is not unreasonable to think that some users may have bought binary object files
they keep in their project directory. Usually binary files cluttering the project
directory are due to previous builds using other systems. <span class="c007">ocamlbuild</span> has so-called
“hygiene” rules that state that object files (<span class="c007">.cmo</span>, <span class="c007">.cmi</span>,
or <span class="c007">.o</span> files, for instance) must not appear outside of the build
directory. These rules are enforced at startup; any violations will be reported
and <span class="c007">ocamlbuild</span> will exit. You must then remove these files by hand or run, with caution,
the script <span class="c007">sanitize.sh</span>, which is generated in your source directory.
This script will contain commands to remove them for you.</p><p>To disable these checks, you can use the <span class="c007">-no-hygiene</span> flag. If you have
files that must elude the hygiene squad, just tag them with <span class="c007">precious</span>
or <span class="c007">not_hygienic</span>.
</p>
<h3 class="subsection" id="sec375">3.2&nbsp;&nbsp;Hello, world !</h3>
<p>
Assuming we are in a directory named <span class="c007">example1</span> containing one file <span class="c007">hello.ml</span>
whose contents are
</p><pre>let _ =
  Printf.printf "Hello, %s ! My name is %s\n"
    (if Array.length Sys.argv &gt; 1 then Sys.argv.(1) else "stranger")
    Sys.argv.(0)
;;
</pre><p>we can compile and link it into a native executable by invoking <span class="c007">ocamlbuild hello.native</span>.
Here, <span class="c007">hello</span> is the basename of the top-level module and <span class="c007">native</span> is an extension used
by <span class="c007">ocamlbuild</span> to denote native code executables.
</p><pre>% ls
hello.ml
% ocamlbuild hello.native
Finished, 4 targets (0 cached) in 00:00:00.
% ls -l
total 12
drwxrwx--- 2 linus gallium 4096 2007-01-17 16:24 _build/
-rw-rw---- 1 linus gallium   43 2007-01-17 16:23 hello.ml
lrwxrwxrwx 1 linus gallium   19 2007-01-17 16:24 hello.native -&gt; _build/hello.native*
</pre><p>What’s this funny <span class="c007">_build</span> directory ? Well that’s where <span class="c007">ocamlbuild</span> does its dirty work
of compiling. You usually won’t have to look very often into this directory. Source files are copied
into <span class="c007">_build</span> and this is where the compilers will be run. Various cache files are also stored
there. Its contents may look like this:
</p><pre>% ls -l _build
total 208
-rw-rw---- 1 linus gallium    337 2007-01-17 16:24 _digests
-rw-rw---- 1 linus gallium    191 2007-01-17 16:24 hello.cmi
-rw-rw---- 1 linus gallium    262 2007-01-17 16:24 hello.cmo
-rw-rw---- 1 linus gallium    225 2007-01-17 16:24 hello.cmx
-rw-rw---- 1 linus gallium     43 2007-01-17 16:23 hello.ml
-rw-rw---- 1 linus gallium     17 2007-01-17 16:24 hello.ml.depends
-rwxrwx--- 1 linus gallium 173528 2007-01-17 16:24 hello.native*
-rw-rw---- 1 linus gallium    936 2007-01-17 16:24 hello.o
-rw-rw---- 1 linus gallium     22 2007-01-17 16:24 ocamlc.where
</pre>
<h3 class="subsection" id="sec376">3.3&nbsp;&nbsp;Executing my code</h3>
<p>
You can execute your code the old-fashioned way (<span class="c007">./hello.native</span>).
You may also type
</p><pre>ocamlbuild hello.native -- Caesar
</pre><p>and it will compile and then run <span class="c007">hello.native</span> with the arguments following <span class="c007">--</span>,
which should display:
</p><pre>% ocamlbuild hello.native -- Caesar
Finished, 4 targets (0 cached) in 00:00:00.
Hello, Caesar ! My name is _build/hello.native
</pre>
<h3 class="subsection" id="sec377">3.4&nbsp;&nbsp;The log file, verbosity and debugging</h3>
<p>
By default, if you run <span class="c007">ocamlbuild</span> on a terminal, it will use some ANSI escape sequences
to display a nice, one-line progress indicator. To see what commands <span class="c007">ocamlbuild</span> has actually run,
you can check the contents of the <span class="c007">_build/_log</span> file. To change the name of the
log file or to disable logging, use the <span class="c007">-log &lt;file&gt;</span> or <span class="c007">-no-log</span> options.
Note that the log file is truncated at each execution of <span class="c007">ocamlbuild</span>.</p><p>The log file contains all the external commands that <span class="c007">ocamlbuild</span> ran or intended to
run along with the target name and the computed tags. With the
<span class="c007">-verbose &lt;level&gt;</span> option, <span class="c007">ocamlbuild</span> will also write more or less useful
debugging information; a verbosity level of 1 (which can also be specified
using the <span class="c007">-verbose</span> switch) prints generally useful information; higher
levels produce much more output.
</p>
<h3 class="subsection" id="sec378">3.5&nbsp;&nbsp;Cleaning</h3>
<p>
<span class="c007">ocamlbuild</span> may leave a <span class="c007">_build</span> directory and symbolic links to executables in
that directory (unless when using -no-links). All of these can be removed safely
by hand, or by invoking <span class="c007">ocamlbuild</span> with the <span class="c007">-clean</span> flag.
</p>
<h3 class="subsection" id="sec379">3.6&nbsp;&nbsp;Where and how to run <span class="c007">ocamlbuild</span>?</h3>
<p>
An important point is that <span class="c007">ocamlbuild</span> must be invoked from the root of the project,
even if this project has multiple, nested subdirectories. This is because <span class="c007">ocamlbuild</span> likes to store the object files in a single <span class="c007">_build</span> directory. You
can change the name of that directory with the <span class="c007">-build-dir</span> option.</p><p><span class="c007">ocamlbuild</span> can be either invoked manually from the UNIX or Windows shell, or
automatically from a build script or a Makefile. Unless run with the
<span class="c007">-no-hygiene</span> option, there is the possibility that <span class="c007">ocamlbuild</span> will prompt the
user for a response. By default, on UNIX systems, if <span class="c007">ocamlbuild</span> senses that the
standard output is a terminal, it will use a nice progress indicator using ANSI
codes, instrumenting the output of the processes it spawns to have a consistent
display. Under non-UNIX systems, or if the standard output is not a terminal,
it will run in classic mode where it will echo the executed commands on its
standard output. This selection can be overridden with the <span class="c007">-classic-display</span> option.
</p>
<h3 class="subsection" id="sec380">3.7&nbsp;&nbsp;Dependencies</h3>
<p>
<em>Dependencies are automatically discovered.</em></p><p>Most of the value of <span class="c007">ocamlbuild</span> lies in the fact that it often needs no extra
information to compile a project besides the name of the top-level module.
<span class="c007">ocamlbuild</span> calls <span class="c007">ocamldep</span> to automatically find the dependencies of any
modules it wants to compile. These dependencies are dynamically incorporated
in the dependency graph, something <span class="c007">make</span> cannot do.
For instance, let’s add a module <span class="c007">Greet</span> that implements various ways of
greeting people.
</p><pre>% cat greet.ml
type how = Nicely | Badly;;

let greet how who =
  match how with Nicely -&gt; Printf.printf "Hello, %s !\n" who
               | Badly  -&gt; Printf.printf "Oh, here is that %s again.\n" who
;;
% cat hello.ml
open Greet

let _ =
  let name =
    if Array.length Sys.argv &gt; 1 then
      Sys.argv.(1)
    else
      "stranger"
  in
  greet
    (if name = "Caesar" then Nicely else Badly)
    name;
  Printf.printf "My name is %s\n" Sys.argv.(0)
;;
</pre><p>Then the module <span class="c007">Hello</span> depends on the module <span class="c007">Greet</span> and <span class="c007">ocamlbuild</span> can
figure this out for himself – we still only have to invoke <span class="c007">ocamlbuild hello.native</span>. Needless to say, this works for any number of modules.
</p>
<h3 class="subsection" id="sec381">3.8&nbsp;&nbsp;Native and byte-code</h3>
<p>
If we want to compile byte-code instead of native, we just a target name of
<span class="c007">hello.byte</span> instead of <span class="c007">hello.native</span>, i.e., we type
<span class="c007">ocamlbuild hello.byte</span>.
</p>
<h3 class="subsection" id="sec382">3.9&nbsp;&nbsp;Compile flags</h3>
<p>
To pass a flag to the compiler, such as the <span class="c007">-rectypes</span> option,
use the <span class="c007">-cflag</span> option as in:
</p><pre>ocamlbuild -cflag -rectypes hello.native
</pre><p>You can put multiple <span class="c007">-cflag</span> options, they will be passed to the compiler
in the same order. You can also give them in a comma-separated list with the
<span class="c007">-cflags</span> option (notice the plural):
</p><pre>ocamlbuild -cflags -I,+lablgtk,-rectypes hello.native
</pre><p>These flags apply when compiling, that is, when producing <span class="c007">.cmi</span>,
<span class="c007">.cmo</span>,<span class="c007">.cmx</span> and <span class="c007">.o</span> files from <span class="c007">.ml</span> or
<span class="c007">.mli</span> files.
</p>
<h3 class="subsection" id="sec383">3.10&nbsp;&nbsp;Link flags</h3>
<p>
Link flags apply when the various object files are collected and linked into
one executable. These will typically be include directories for libraries.
They are given using the <span class="c007">-lflag</span> and <span class="c007">-lflags</span> options, which
work in the same way as the <span class="c007">-cflag</span> and <span class="c007">-cflags</span> options.
</p>
<h3 class="subsection" id="sec384">3.11&nbsp;&nbsp;Linking with external libraries</h3>
<p>
In our third example, we use one Unix system call and functions from the <span class="c007">num</span>
library:
</p><pre>% cat epoch.ml
let _ =
  let s = Num.num_of_string (Printf.sprintf "%.0f" (Unix.gettimeofday ())) in
  let ps = Num.mult_num (Num.num_of_string "1000000000000") s in
  Printf.printf "%s picoseconds have passed since January 1st, 1970.\n"
    (Num.string_of_num ps)
;;
</pre><p>This requires linking with the <span class="c007">unix</span> and <span class="c007">num</span> modules, which is accomplished
by using the <span class="c007">-lib unix</span> and <span class="c007">-lib num</span> flags, or, alternatively, <span class="c007">-libs unix,num</span>:
</p><pre>% ocamlbuild -libs nums,unix epoch.native --
Finished, 4 targets (4 cached) in 00:00:00.
1169051647000000000000 picoseconds have passed since January 1st, 1970.
</pre><p>You may need to add options such as <span class="c007">-cflags -I,/usr/local/lib/ocaml/</span>
and <span class="c007">-lflags -I,/usr/local/lib/ocaml/</span> if the libraries you wish to
link with are not in OCaml’s default search path.
</p>
<h3 class="subsection" id="sec385">3.12&nbsp;&nbsp;The <span class="c007">_tags</span> files</h3>
<p>
Finer control over the compiler flags applied to each source file, such as
preprocessing, debugging, profiling and linking options, can be gained using
<span class="c007">ocamlbuild</span>’s tagging mechanism.</p><p>Every source file has a set of tags which tells <span class="c007">ocamlbuild</span> what kind of file it is
and what to do with it. A tag is simply a string, usually lowercase, for
example <span class="c007">ocaml</span> or <span class="c007">native</span>. The set of tags attached to a file
is computed by applying the tagging rules to the filename. Tagging rules are
defined in <span class="c007">_tags</span> files in any parent directory of a file, up to the main
project directory.</p><p>Each line in the <span class="c007">_tags</span> file is made of a glob pattern (see subsection
<a href="#subsec%3Aglob">18.3.13</a>) and a list of tags. More than one rule can apply to a file
and rules are applied in the order in which they appear in a file.
By preceding a tag with a minus sign, one may remove tags from one or more files.</p>
<h4 class="subsubsection" id="sec386">Example: the built-in <span class="c007">_tags</span> file</h4>
<pre>     &lt;**/*.ml&gt; or &lt;**/*.mli&gt; or &lt;**/*.mlpack&gt; or &lt;**/*.ml.depends&gt;: ocaml
     &lt;**/*.byte&gt;: ocaml, byte, program
     &lt;**/*.odoc&gt;: ocaml, doc
     &lt;**/*.native&gt;: ocaml, native, program
     &lt;**/*.cma&gt;: ocaml, byte, library
     &lt;**/*.cmxa&gt;: ocaml, native, library
     &lt;**/*.cmo&gt;: ocaml, byte
     &lt;**/*.cmi&gt;: ocaml, byte, native
     &lt;**/*.cmx&gt;: ocaml, native
</pre><p>
Two special tags made from the path name of the file relative to the toplevel
of the project are automatically defined for each file. For a file
<span class="c007">foo/bar.ml</span> those tags will be <span class="c007">file:foo/bar.ml</span>, and
<span class="c007">extension:ml</span>.</p><p>If you do not have subdirectories, you can put <span class="c007">*.ml</span> instead of
<span class="c007">**/*.ml</span>.
</p>
<h3 class="subsection" id="sec387">3.13&nbsp;&nbsp;Glob patterns and expressions</h3>
<p>
<a id="subsec:glob"></a>
Glob patterns have a syntax similar to those used by UNIX shells to select path
names (like <span class="c007">foo_*.ba?</span>). They are used in <span class="c007">ocamlbuild</span> to define the files
and directories to which tags apply. Glob expressions are glob patterns
enclosed in brackets <span class="c007">&lt;</span> and <span class="c007">&gt;</span> combined using the standard
boolean operators <span class="c007">and</span>, <span class="c007">or</span>, <span class="c007">not</span>. This allows one to
describe sets of path names in more concise and more readable ways.</p><p>Please note that file and directory names are supposed to be made of the
following characters: <span class="c007">a</span>, …, <span class="c007">z</span>, <span class="c007">A</span>,
…, <span class="c007">Z</span>, <span class="c007">0</span>, …, <span class="c007">9</span>, <span class="c007">_</span>,
<span class="c007">-</span> and <span class="c007">.</span>. This is called the pathname alphabet <span class="c013">P</span>.</p><blockquote class="table"><div class="center"><hr class="c032"></div>
<div class="center">
<table class="c000 cellpadding1" border="1"><tbody><tr><td class="c028"><span class="c012"><em> Formal syntax</em></span></td><td class="c029"><span class="c012"><em> Example</em></span></td><td class="c028"><span class="c012"><em>Matches</em></span></td><td class="c028"><span class="c012"><em>Does not match</em></span></td><td class="c028"><span class="c012"><em> Meaning (formal meaning) </em></span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c013">u</span> <br>
 A string of pathname characters</span></td><td class="c029"><span class="c012"> <span class="c007">foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">fo.ml</span>, <span class="c007">bar/foo.ml</span></span></td><td class="c028"><span class="c012"> The exact string <span class="c013">u</span>
({ <span class="c013">u</span> }, where <span class="c013">u</span> ∈ <span class="c013">P</span></span><sup><span class="c012">*</span></sup><span class="c012">) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">*</span> <br>
 The wild-card star</span></td><td class="c029"><span class="c012"> <span class="c007">*</span></span></td><td class="c028"><span class="c012"> ε, <span class="c007">foo</span>, <span class="c007">bar</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo/bar</span>, <span class="c007">/bar</span></span></td><td class="c028"><span class="c012"> Any string not containing a slash
(<span class="c013">P</span></span><sup><span class="c012">*</span></sup><span class="c012">) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">?</span> <br>
 The joker</span></td><td class="c029"><span class="c012"> <span class="c007">?</span></span></td><td class="c028"><span class="c012"> <span class="c007">a</span>, <span class="c007">b</span>, <span class="c007">z</span></span></td><td class="c028"><span class="c012"> <span class="c007">/</span>, <span class="c007">bar</span></span></td><td class="c028"><span class="c012"> Any one-letter string, excluding the slash </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">**/</span> <br>
 The prefix inter-directory star</span></td><td class="c029"><span class="c012"> <span class="c007">**/foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo.ml</span>, <span class="c007">bar/foo.ml</span>, <span class="c007">bar/baz/foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo/bar</span>, <span class="c007">/bar</span></span></td><td class="c028"><span class="c012"> The empty string, or any string ending with a slash
(ε ∪ <span class="c013">P</span></span><sup><span class="c012">*</span></sup><span class="c012"><span class="c007">/</span>) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">/**</span> <br>
 The suffix inter-directory star</span></td><td class="c029"><span class="c012"> <span class="c007">foo/**</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo</span>, <span class="c007">foo/bar</span></span></td><td class="c028"><span class="c012"> <span class="c007">bar/foo</span></span></td><td class="c028"><span class="c012"> Any string starting with a slash, or the empty string
(ε ∪ <span class="c007">/</span><span class="c013">P</span></span><sup><span class="c012">*</span></sup><span class="c012">) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">/**/</span> <br>
 The infix inter-directory star</span></td><td class="c029"><span class="c012"> <span class="c007">bar/**/foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">bar/foo.ml</span>, <span class="c007">bar/baz/foo.ml</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo.ml</span></span></td><td class="c028"><span class="c012"> Any string starting and ending with a slash
(ε ∪ <span class="c007">/</span><span class="c013">P</span></span><sup><span class="c012">*</span></sup><span class="c012"><span class="c007">/</span>) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">[</span> <span class="c013">r</span></span><sub><span class="c012">1</span></sub><span class="c016"> r</span><sub><span class="c012">2</span></sub><span class="c012"> ⋯ <span class="c013">r</span></span><sub><span class="c016">k</span></sub><span class="c012"> <span class="c007">]</span>
where <span class="c013">r</span></span><sub><span class="c016">i</span></sub><span class="c012"> is either <span class="c013">c</span> or <span class="c013">c</span></span><sub><span class="c012">1</span></sub><span class="c012">−<span class="c013">c</span></span><sub><span class="c012">2</span></sub><span class="c012"> (1 ≤ <span class="c013">i</span> ≤ <span class="c013">k</span>)
<br>
 The positive character class</span></td><td class="c029"><span class="c012"> <span class="c007">[a-fA-F0-9_.]</span></span></td><td class="c028"><span class="c012"> <span class="c007">3</span>, <span class="c007">F</span>, <span class="c007">.</span></span></td><td class="c028"><span class="c012"> <span class="c007">z</span>, <span class="c007">bar</span></span></td><td class="c028"><span class="c012"> Any one-letter string made of characters from one of the ranges
<span class="c013">r</span></span><sub><span class="c016">i</span></sub><span class="c012"> (1 ≤ <span class="c013">i</span> ≤ <span class="c013">n</span>).
(<span class="c015">L</span>(<span class="c013">r</span></span><sub><span class="c012">1</span></sub><span class="c012">) ∪ ⋯ ∪ <span class="c015">L</span>(<span class="c013">r</span></span><sub><span class="c016">n</span></sub><span class="c012">)) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">[^</span><span class="c013">r</span></span><sub><span class="c012">1</span></sub><span class="c016"> r</span><sub><span class="c012">2</span></sub><span class="c012"> ⋯ <span class="c013">r</span></span><sub><span class="c016">k</span></sub><span class="c012"> <span class="c007">]</span>
where <span class="c013">r</span></span><sub><span class="c016">i</span></sub><span class="c012"> is either <span class="c013">c</span> or <span class="c013">c</span></span><sub><span class="c012">1</span></sub><span class="c012">−<span class="c013">c</span></span><sub><span class="c012">2</span></sub><span class="c012"> (1 ≤ <span class="c013">i</span> ≤ <span class="c013">k</span>)
<br>
 The negative character class</span></td><td class="c029"><span class="c012"> <span class="c007">[^a-fA-F0-9_.]</span></span></td><td class="c028"><span class="c012"> <span class="c007">z</span>, <span class="c007">bar</span></span></td><td class="c028"><span class="c012"> <span class="c007">3</span>, <span class="c007">F</span>, <span class="c007">.</span></span></td><td class="c028"><span class="c012"> Any one-letter string NOT made of characters from one of the ranges
<span class="c013">r</span></span><sub><span class="c016">i</span></sub><span class="c012"> (1 ≤ <span class="c013">i</span> ≤ <span class="c013">n</span>).
(Σ</span><sup><span class="c012">*</span></sup><span class="c012"> ∖ (<span class="c015">L</span>(<span class="c013">r</span></span><sub><span class="c012">1</span></sub><span class="c012">) ∪ ⋯ ∪ <span class="c015">L</span>(<span class="c013">r</span></span><sub><span class="c016">n</span></sub><span class="c012">))) </span></td></tr>
<tr><td class="c028"><span class="c016">p</span><sub><span class="c012">1</span></sub><span class="c016"> p</span><sub><span class="c012">2</span></sub><span class="c012"> <br>
 A concatenation of patterns</span></td><td class="c029"><span class="c012"> <span class="c007">foo*</span></span></td><td class="c028"><span class="c012"> <span class="c007">foo</span>, <span class="c007">foob</span>, <span class="c007">foobar</span></span></td><td class="c028"><span class="c012"> <span class="c007">fo</span>, <span class="c007">bar</span></span></td><td class="c028"><span class="c012"> Any string with a prefix matching <span class="c013">p</span></span><sub><span class="c012">1</span></sub><span class="c012"> and the corresponding suffix
matching <span class="c013">p</span></span><sub><span class="c012">2</span></sub><span class="c012">,
({ <span class="c013">uv</span> ∣ <span class="c013">u</span> ∈ <span class="c015">L</span>(<span class="c013">p</span></span><sub><span class="c012">1</span></sub><span class="c012">), <span class="c013">v</span> ∈ <span class="c015">L</span>(<span class="c013">p</span></span><sub><span class="c012">2</span></sub><span class="c012">) }) </span></td></tr>
<tr><td class="c028"><span class="c012"><span class="c007">{</span> <span class="c013">p</span></span><sub><span class="c012">1</span></sub><span class="c012"> <span class="c007">,</span> <span class="c013">p</span></span><sub><span class="c012">2</span></sub><span class="c012"> <span class="c007">,</span> ⋯ <span class="c007">,</span> <span class="c013">p</span></span><sub><span class="c016">k</span></sub><span class="c012"> <span class="c007">}</span> <br>
 A union of patterns</span></td><td class="c029"><span class="c012"> <span class="c007">toto.{ml,mli}</span></span></td><td class="c028"><span class="c012"> <span class="c007">toto.ml</span>, <span class="c007">toto.mli</span></span></td><td class="c028"><span class="c012"> <span class="c007">toto.</span></span></td><td class="c028"><span class="c012"> Any string matching one of the patterns <span class="c013">p</span></span><sub><span class="c016">i</span></sub><span class="c012"> for 1 ≤ <span class="c013">i</span> ≤ <span class="c013">k</span>.
(<span class="c015">L</span>(<span class="c013">p</span></span><sub><span class="c012">1</span></sub><span class="c012">) ∪ ⋯ ∪ <span class="c015">L</span>(<span class="c013">p</span></span><sub><span class="c016">k</span></sub><span class="c012">)) </span></td></tr>
</tbody></table><span class="c012">
</span></div>
<div class="caption"><table class="c002 cellpading0"><tbody><tr><td class="c027">Table 18.1: 
Syntax and semantics of glob patterns.
</td></tr>
</tbody></table></div>
<div class="center"><hr class="c032"></div></blockquote><blockquote class="table"><div class="center"><hr class="c032"></div>
<div class="center">
<table class="c000 cellpadding1" border="1"><tbody><tr><td class="c028"><span class="c012"><em> Formal syntax</em></span></td><td class="c029"><span class="c012"><em> Example</em></span></td><td class="c028"><span class="c012"><em> Meaning (formal meaning) </em></span></td></tr>
<tr><td class="c028"><span class="c012"> <span class="c007">&lt;</span><span class="c013">p</span><span class="c007">&gt;</span></span></td><td class="c029"><span class="c012"> <span class="c007">&lt;foo.ml&gt;</span></span></td><td class="c028"><span class="c012"> Pathnames matching the pattern <span class="c013">p</span> </span></td></tr>
<tr><td class="c028"><span class="c016"> e</span><sub><span class="c012">1</span></sub><span class="c012"> &nbsp; <span class="c009">or</span> &nbsp; <span class="c013">e</span></span><sub><span class="c012">2</span></sub></td><td class="c029"><span class="c012"> <span class="c007">&lt;*.ml&gt; or &lt;foo/bar.ml&gt;</span></span></td><td class="c028"><span class="c012"> Pathnames matching at least one of the expressions <span class="c013">e</span></span><sub><span class="c012">1</span></sub><span class="c012"> and <span class="c013">e</span></span><sub><span class="c012">2</span></sub><span class="c012"> </span></td></tr>
<tr><td class="c028"><span class="c016"> e</span><sub><span class="c012">1</span></sub><span class="c012"> &nbsp; <span class="c009">and</span> &nbsp; <span class="c013">e</span></span><sub><span class="c012">2</span></sub></td><td class="c029"><span class="c012"> <span class="c007">&lt;*.ml&gt; and &lt;foo_*&gt;</span></span></td><td class="c028"><span class="c012"> Pathnames matching both expressions <span class="c013">e</span></span><sub><span class="c012">1</span></sub><span class="c012"> and <span class="c013">e</span></span><sub><span class="c012">2</span></sub><span class="c012"> </span></td></tr>
<tr><td class="c028"><span class="c012"> <span class="c009">not</span> &nbsp; <span class="c013">e</span></span></td><td class="c029"><span class="c012"> <span class="c007">not &lt;*.mli&gt;</span></span></td><td class="c028"><span class="c012"> Pathnames not matching the expression <span class="c013">e</span> </span></td></tr>
<tr><td class="c028"><span class="c016"> <span class="c007">true</span></span></td><td class="c029"><span class="c012"> <span class="c007">true</span></span></td><td class="c028"><span class="c012"> All pathnames </span></td></tr>
<tr><td class="c028"><span class="c016"> <span class="c007">false</span></span></td><td class="c029"><span class="c012"> <span class="c007">false</span></span></td><td class="c028"><span class="c012"> No pathnames </span></td></tr>
</tbody></table><span class="c012">
</span></div>
<div class="caption"><table class="c002 cellpading0"><tbody><tr><td class="c027">Table 18.2: 
Syntax and semantics of glob expressions.
</td></tr>
</tbody></table></div>
<div class="center"><hr class="c032"></div></blockquote>
<h3 class="subsection" id="sec388">3.14&nbsp;&nbsp;Subdirectories</h3>
<p>
If the files of your project are held in one or more subdirectories,
<span class="c007">ocamlbuild</span> must be made aware of that fact using the <span class="c007">-I</span> or <span class="c007">-Is</span> options
or by adding an <span class="c007">include</span> tag. For instance, assume your project is made
of three subdirectories, <span class="c007">foo</span>, <span class="c007">bar</span> and <span class="c007">baz</span> containing
various <span class="c007">.ml</span> files, the main file being <span class="c007">foo/main.ml</span>. Then you can
either type:
</p><pre>% ocamlbuild -Is foo,bar,baz foo/main.native
</pre><p>or add the following line in the <span class="c007">_tags</span> file
</p><pre>&lt;foo&gt; or &lt;bar&gt; or &lt;baz&gt;: include
</pre><p>and call
</p><pre>% ocamlbuild foo/main.native
</pre><p>
There are then two cases. If no other modules named <span class="c007">Bar</span> or
<span class="c007">Baz</span> exist elsewhere in the project, then you are done. Just use
<span class="c007">Foo</span>, <span class="c007">Foo.Bar</span> and <span class="c007">Foo.Baz</span> in your code.
Otherwise, you will need to use the plugin mechanism and define the mutual
visibility of the subdirectories using the <span class="c007">Pathname.define_context</span>
function.</p>
<h4 class="subsubsection" id="sec389">Note on subdirectory traversal</h4>
<p>
<span class="c007">ocamlbuild</span> used to traverse by default any subdirectory not explicitly excluded.
This is no longer the case. Note that you can still have a fine grained
control using your <span class="c007">_tags</span> file and the <span class="c007">traverse</span> tag.</p><p>There is no longer the <span class="c007">true: traverse</span> tag declaration by default. To
make <span class="c007">ocamlbuild</span> recursive use one of these:
</p><ol class="enumerate" type="1"><li class="li-enumerate">
Give the <span class="c007">-r</span> flag to ocamlbuild.
</li><li class="li-enumerate">Have a <span class="c007">_tags</span> or myocamlbuild.ml file in your top directory.
</li></ol>
<h3 class="subsection" id="sec390">3.15&nbsp;&nbsp;Grouping targets with <span class="c007">.itarget</span></h3>
<p>
You can create a file named <span class="c007">foo.itarget</span> containing
a list of targets, one per line, such as
</p><pre>main.native
main.byte
stuff.docdir/index.html
</pre><p>Requesting the target <span class="c007">foo.otarget</span> will then build every target
listed in the file <span class="c007">foo.itarget</span>. Blank lines and lines starting
with a sharp (<span class="c007">#</span>) are ignored.
</p>
<h3 class="subsection" id="sec391">3.16&nbsp;&nbsp;Packing subdirectories into modules</h3>
<p>
OCaml’s <span class="c007">-pack</span> option allows you to structure the contents of a
module in a subdirectory. For instance, assume you have a directory
<span class="c007">foo</span> containing two modules <span class="c007">bar.ml</span> and <span class="c007">baz.ml</span>.
You want from these to build a module <span class="c007">Foo</span> containing <span class="c007">Bar</span>
and <span class="c007">Baz</span> as submodules. In the case where no modules named
<span class="c007">Bar</span> or <span class="c007">Baz</span> exist outside of <span class="c007">Foo</span>, to do this you
must write a file <span class="c007">foo.mlpack</span>, preferably sitting in the same
directory as the directory <span class="c007">Foo</span> and containing the list of modules
(one per line) it must contain:
</p><pre>Bar
Baz
</pre><p>Then when you will request for building <span class="c007">foo.cmo</span> the package will be
made from <span class="c007">bar.cmo</span> and <span class="c007">baz.cmo</span>.
</p>
<h3 class="subsection" id="sec392">3.17&nbsp;&nbsp;Making an OCaml library</h3>
<p>
In a similar way than for packaged modules you can make a library by putting
it’s contents in a file (with the mllib extension). For instance, assume you
have a two modules <span class="c007">bar.ml</span> and <span class="c007">baz.ml</span>. You want from these to
build a library <span class="c007">foo.cmx?a</span> containing <span class="c007">Bar</span> and <span class="c007">Baz</span>
modules. To do this you must write a file <span class="c007">foo.mllib</span> containing the
list of modules (one per line) it must contain:
</p><pre>Bar
Baz
</pre><p>Then when you will request for building <span class="c007">foo.cma</span> the library will be
made from <span class="c007">bar.cmo</span> and <span class="c007">baz.cmo</span>.
</p>
<h3 class="subsection" id="sec393">3.18&nbsp;&nbsp;Making an OCaml toplevel</h3>
<p>
Making a toplevel is almost the same thing than making a packaged module or a
library. Just write a file with the <span class="c007">mltop</span> extension (like
<span class="c007">foo.mltop</span>) and request for building the toplevel using the
<span class="c007">top</span> extension (<span class="c007">foo.top</span> in this example).
</p>
<h3 class="subsection" id="sec394">3.19&nbsp;&nbsp;Preprocessor options and tags</h3>
<p>
You can specify preprocessor options with <span class="c007">-pp</span> followed by the
preprocessor string, for instance <span class="c007">ocamlbuild -pp camlp4o.opt -unsafe</span>
would run your sources through CamlP4 with the <span class="c007">-unsafe</span> option.
Another way is to use the tags file.
</p><div class="center">
<table class="c000 cellpadding1" border="1"><tbody><tr><td class="c023"> <span class="c019">Tag</span></td><td class="c023"><span class="c019">Preprocessor command</span></td><td class="c023"><span class="c019">Remark</span> </td></tr>
<tr><td class="c023"> <span class="c007">pp(cmd...)</span></td><td class="c023"><span class="c007">cmd...</span></td><td class="c023">Arbitrary
preprocessor command<sup><a id="text3" href="#note3">1</a></sup> </td></tr>
<tr><td class="c023"> <span class="c007">camlp4o</span></td><td class="c023"><span class="c007">camlp4o</span></td><td class="c023">Original OCaml syntax </td></tr>
<tr><td class="c023"> <span class="c007">camlp4r</span></td><td class="c023"><span class="c007">camlp4r</span></td><td class="c023">Revised OCaml syntax </td></tr>
<tr><td class="c023"> <span class="c007">camlp4of</span></td><td class="c023"><span class="c007">camlp4of</span></td><td class="c023">Original OCaml syntax with extensions </td></tr>
<tr><td class="c023"> <span class="c007">camlp4rf</span></td><td class="c023"><span class="c007">camlp4rf</span></td><td class="c023">Revised OCaml syntax with extensions </td></tr>
</tbody></table>
</div>
<h3 class="subsection" id="sec395">3.20&nbsp;&nbsp;Debugging byte code and profiling native code</h3>
<p>
The preferred way of compiling code suitable for debugging with <span class="c007">ocamldebug</span> or
profiling native code with <span class="c007">ocamlprof</span> is to use the appropriate target
extensions, <span class="c007">.d.byte</span> for debugging or <span class="c007">.p.native</span>.</p><p>Another way is to add use the <span class="c007">debug</span> or <span class="c007">profile</span> tags.
Note that these tags must be applied at the compilation and linking stages.
Hence you must either use <span class="c007">-tag debug</span> or <span class="c007">-tag profile</span>
on the command line, or add a
</p><pre>true: debug
</pre><p>line to your <span class="c007">_tags</span> file.
Please note that the byte-code profiler works in a wholly different way
and is not supported by <span class="c007">ocamlbuild</span>.
</p>
<h3 class="subsection" id="sec396">3.21&nbsp;&nbsp;Generating documentation using <span class="c007">ocamldoc</span></h3>
<p>
Write the names of the modules whose interfaces will be documented in a file
whose extension is <span class="c007">.odocl</span>, for example <span class="c007">foo.odocl</span>, then invoke
<span class="c007">ocamlbuild</span> on the target <span class="c007">foo.docdir/index.html</span>. This will collect all the
documentation from the interfaces (which will be build, if necessary) using
<span class="c007">ocamldoc</span> and generate a set of HTML files under the directory
<span class="c007">foo.docdir/</span>, which is actually a link to <span class="c007">_build/foo.docdir/</span>.
As for packing subdirectories into modules, the module names must be written
one per line, without extensions and correctly capitalized. Note that
generating documentation in formats other than HTML or from implementations is
not supported.
</p>
<h3 class="subsection" id="sec397">3.22&nbsp;&nbsp;The display line</h3>
<p>
Provided <span class="c007">ocamlbuild</span> runs in a terminal under a POSIX environment, it will
display a sophisticated progress-indicator line that graciously interacts
with the output of subcommands. This line looks like this:
</p><pre>00:00:02 210  (180 ) main.cmx                             ONbp--il /
</pre><p>Here, 00:00:02 is the elapsed time in hour:minute:second format since <span class="c007">ocamlbuild</span> has
been invoked; 210 is the number of external commands, typically calls to the
compiler or the like, that may or may not have been invoked; 180 is the number
of external commands that have not been invoked since their result is already
in the build directory; <span class="c007">main.cmx</span> is the name of the last target built;
<span class="c007">ONbp--il</span> is a short string that describes the tags that have been
encountered and the slash at the end is a frame from a rotating ticker. Hence,
the display line has the following structure:
</p><pre>HH:MM:SS JOBS (CACHED) PATHNAME                           TAGS TICKER
</pre><p>
The tag string is made of 8 indicators which each monitor a tag. These tags
are <span class="c007">ocaml</span>, <span class="c007">native</span>, <span class="c007">byte</span>, <span class="c007">program</span>,
<span class="c007">pp</span>, <span class="c007">debug</span>, <span class="c007">interf</span> and <span class="c007">link</span>. Initially,
each indicator displays a dash <span class="c007">-</span>. If the current target has the
monitored tag, then the indicator displays the corresponding character
(see table <a href="#tab%3Atag-chars">18.3</a>) in uppercase. Otherwise, it displays that
character in lowercase. This allows you to see the set of tags that have
been applied to files in your project during the current invocation of <span class="c007">ocamlbuild</span>.</p><p>Hence the tag string <span class="c007">ONbp--il</span> means that the current target
<span class="c007">main.cmx</span> has the tags <span class="c007">ocaml</span> and <span class="c007">native</span>, and that
the tags <span class="c007">ocaml</span>, <span class="c007">native</span>, <span class="c007">byte</span>, <span class="c007">program</span>,
<span class="c007">interf</span> and <span class="c007">link</span> have already been seen.</p><blockquote class="table"><div class="center"><hr class="c032"></div>
<div class="center">
<table class="c000 cellpadding1" border="1"><tbody><tr><td class="c023"> <span class="c019">Tag</span></td><td class="c021"><span class="c019">Display character</span> </td></tr>
<tr><td class="c023"> ocaml</td><td class="c021">O </td></tr>
<tr><td class="c023"> native</td><td class="c021">N </td></tr>
<tr><td class="c023"> byte</td><td class="c021">B </td></tr>
<tr><td class="c023"> program</td><td class="c021">P </td></tr>
<tr><td class="c023"> pp</td><td class="c021">R </td></tr>
<tr><td class="c023"> debug</td><td class="c021">D </td></tr>
<tr><td class="c023"> interf</td><td class="c021">I </td></tr>
<tr><td class="c023"> link</td><td class="c021">L </td></tr>
</tbody></table>
</div>
<div class="caption"><table class="c002 cellpading0"><tbody><tr><td class="c027">Table 18.3: <a id="tab:tag-chars"></a> Relation between the characters displayed in
the tag string and the tags.</td></tr>
</tbody></table></div>
<div class="center"><hr class="c032"></div></blockquote>
<h3 class="subsection" id="sec398">3.23&nbsp;&nbsp;<span class="c007">ocamllex</span>, <span class="c007">ocamlyacc</span> and <span class="c007">menhir</span></h3>
<p>
<span class="c007">ocamlbuild</span> knows how to run the standard lexer and parser generator tools
<span class="c007">ocamllex</span> and <span class="c007">ocamlyacc</span> when your files have the
standard <span class="c007">.mll</span> and <span class="c007">.mly</span> extensions. If you want to
use <span class="c007">menhir</span> instead of <span class="c007">ocamlyacc</span>, you can either
launch <span class="c007">ocamlbuild</span> with the <span class="c007">-use-menhir</span> option or add a
</p><pre>true: use_menhir
</pre><p>line to your <span class="c007">_tags</span> file. Note that there is currently no way
of using <span class="c007">menhir</span> and <span class="c007">ocamlyacc</span> in the same execution
of <span class="c007">ocamlbuild</span>.
</p>
<h3 class="subsection" id="sec399">3.24&nbsp;&nbsp;Changing the compilers or tools</h3>
<p>
As <span class="c007">ocamlbuild</span> is part of your OCaml distribution, it knows if it can call the
native compilers and tools (<span class="c007">ocamlc.opt</span>, <span class="c007">ocamlopt.opt</span>...)
or not. However you may want <span class="c007">ocamlbuild</span> to use another <span class="c007">ocaml</span> compiler
for different reasons (such as cross-compiling or using a wrapper such as
<span class="c007">ocamlfind</span>). Here is the list of relevant options:
</p><ul class="itemize"><li class="li-itemize">
<span class="c007">-ocamlc &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamlopt &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamldep &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamlyacc &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-menhir &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamllex &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamlmktop &lt;command&gt;</span>
</li><li class="li-itemize"><span class="c007">-ocamlrun &lt;command&gt;</span>
</li></ul>
<h3 class="subsection" id="sec400">3.25&nbsp;&nbsp;Interaction with version control systems</h3>
<p>
Here are tips for configuring your version control system to ignore the files
and directories generated by <span class="c007">ocamlbuild</span>.</p><p>The directory <span class="c007">_build</span> and any symbolic links
pointing into <span class="c007">_build</span> should be ignored.
To do this, you must add the following ignore patterns to your version
control system’s ignore set:
</p><pre>_build
*.native
*.byte
*.d.native
*.p.byte
</pre><p>
For CVS, add the above lines to the <span class="c007">.cvsignore</span> file.
For Subversion (SVN), type <span class="c007">svn propedit svn:ignore .</span> and add the
above lines.
</p>
<h3 class="subsection" id="sec401">3.26&nbsp;&nbsp;A shell script for driving it all?</h3>
<p>
<em>To shell or to make ?</em>
Traditionally, makefiles have two major functions. The first one
is the dependency-ordering, rule-matching logic used for compiling.
The second one is as a dispatcher for various actions defined using
phony targets with shell script actions. These actions include cleaning,
cleaning really well, archiving, uploading and so on. Their characteristic
is that they rely little or not on the building process – they either need
the building to have been completed, or they don’t need anything.
As <span class="c007">/bin/sh</span> scripts have been here for three to four decades and are
not going anywhere, why not replace that functionality of makefiles with a
shell script ? We have thought of three bad reasons:
</p><ul class="itemize"><li class="li-itemize">
Typing <span class="c007">make</span> to compile is now an automatism,
</li><li class="li-itemize">We need to share variable definitions between rules and actions,
</li><li class="li-itemize">Escaping already way too special-character-sensitive shell code with
invisible tabs and backslashes is a dangerously fun game.
</li></ul><p>
We also have bad reasons for not using an OCaml script to drive everything:
</p><ul class="itemize"><li class="li-itemize">
<span class="c007">Sys.command</span> calls the <span class="c007">/bin/sh</span> anyway,
</li><li class="li-itemize">Shell scripts can execute partial commands or commands with badly formed arguments.
</li><li class="li-itemize">Shell scripts are more concise for expressing... shell scripts.
</li></ul><p>
Anyway you are of course free to use a makefile or an OCaml script to call ocamlbuild.
Here is an example shell driver script:
</p><pre>#!/bin/sh

set -e

TARGET=epoch
FLAGS="-libs unix,nums"
OCAMLBUILD=ocamlbuild

ocb()
{
  $OCAMLBUILD $FLAGS $*
}

rule() {
  case $1 in
    clean)  ocb -clean;;
    native) ocb $TARGET.native;;
    byte)   ocb $TARGET.byte;;
    all)    ocb $TARGET.native $TARGET.byte;;
    depend) echo "Not needed.";;
    *)      echo "Unknown action $1";;
  esac;
}

if [ $# -eq 0 ]; then
  rule all
else
  while [ $# -gt 0 ]; do
    rule $1;
    shift
  done
fi
</pre>
<h2 class="section" id="sec402">4&nbsp;&nbsp;Appendix: Motivations</h2>
<p>
<em>This inflammatory appendix describes the frustration that led us to write <span class="c007">ocamlbuild</span>.</em></p><p>Many people have painfully found that the utilities of the <span class="c007">make</span>
family, namely GNU Make, BSD Make, and their derivatives, fail to scale to
large projects, especially when using multi-stage compilation rules, such as
custom pre-processors, unless dependencies are hand-defined. But as your
project gets larger, more modular, and uses more diverse pre-processing tools,
it becomes increasingly difficult to correctly define dependencies by hand.
Hence people tend to use language-specific tools that attempt to extract
dependencies. However another problem then appears: <span class="c007">make</span> was designed
with the idea of a static dependency graph. Dependency extracting tools,
however, are typically run by a rule in <span class="c007">make</span> itself; this means that
make has to reload the dependency information. This is the origin of the
<span class="c007">make clean; make depend; make</span> mantra. This approach tends to work
quite well as long as all the files sit in a single directory and there is only
one stage of pre-processing. If there are two or more stages, then dependency
extracting tools must be run two or more times - and this means multiple
invocations of <span class="c007">make</span>. Also, if one distributes the modules of a large
project into multiple subdirectories, it becomes difficult to distribute the
makefiles themselves, because the language of <span class="c007">make</span> was not conceived
to be modular; the only two mechanisms permitted, inclusion of makefile
fragments, and invocation of other make instances, must be skillfully
coordinated with phony target names (<span class="c007">depend1, depend2...</span>) to insure
inclusion of generated dependencies with multi-stage programming; changes in
the structure of the project must be reflected by hand and the order of
variable definitions must be well-thought ahead to avoid long afternoons spent
combinatorially fiddling makefiles until it works but no one understands why.</p><p>These problems become especially apparent with OCaml: to ensure type safety and
to allow a small amount of cross-unit optimization when compiling native code,
interface and object files include cryptographical digests of interfaces they
are to be linked with. This means that linking is safer, but that makefile sloppiness
leads to messages such as:
</p><pre>Files foo.cmo and bar.cmo
make inconsistent assumptions over interface Bar
</pre><p>
The typical reaction is then to issue the mantra <span class="c007">make clean; make
depend; make</span> and everything compiles just fine... from the beginning. Hence
on medium projects, the programmer often has to wait for minutes instead of the
few seconds that would be taken if <span class="c007">make</span> could correctly guess the
small number of files that really had to be recompiled.</p><p>It is not surprising that hacking a build tool such as <span class="c007">make</span> to include
a programming language while retaining the original syntax and semantics gives
an improvised and cumbersome macro language of dubious expressive power. For
example, using GNU make, suppose you have a list of <span class="c007">.ml</span>s that you want
to convert into a list including both <span class="c007">.cmo</span>s and <span class="c007">.cmi</span>s, that
is you want to transform <span class="c007">a.ml b.ml c.ml</span> into <span class="c007">a.cmi a.cmo b.cmi
b.cmo c.cmi c.cmo</span> while preserving the dependency order which must be hand
specified for linking <sup><a id="text4" href="#note4">2</a></sup>.
Unfortunately <span class="c007">$patsubst %.ml, %.cmi %.cmo, a.ml b.ml c.ml</span> won’t
work since the %-sign in the right-hand of a <span class="c007">patsubst</span> gets
substituted only once. You then have to delve into something that is hardly
lambda calculus: an intricate network of <span class="c007">foreach</span>, <span class="c007">eval</span>,
<span class="c007">call</span> and <span class="c007">define</span>s may get you the job done, unless you chicken
out and opt for an external <span class="c007">awk</span>, <span class="c007">sed</span> or <span class="c007">perl</span> call.
People who at this point have not lost their temper or sanity usually resort to
metaprogramming by writing Makefile generators using a mixture of shell and m4.
One such an attempt gave something that is the nightmare of wannabe package
maintainers: it’s called <span class="c007">autotools</span>.</p><p>Note that it is also difficult to write <span class="c007">Makefiles</span> to build object
files in a separate directory. It is not impossible since the language of
<span class="c007">make</span> is Turing-complete, a proof of which is left as an exercise.
Note that building things in a separate directory is not necessarily a young
enthusiast’s way of giving a different look and feel to his projects – it may
be a good way of telling the computer that <span class="c007">foo.mli</span> is generated by
<span class="c007">ocamlyacc</span> using <span class="c007">foo.mly</span> and can thus be removed.
</p>
<h2 class="section" id="sec403">5&nbsp;&nbsp;Appendix: Summary of default rules</h2>
<p>
The contents of this table give a summary of the most important default rules.
To get the most accurate and up-to-date information, launch <span class="c007">ocamlbuild</span> with the
<span class="c007">-documentation</span> option.
</p><div class="center">
<table class="c000 cellpadding1" border="1"><tbody><tr><td class="c029"><span class="c020"> Tags</span></td><td class="c029"><span class="c020">Dependencies</span></td><td class="c028"><span class="c020">Targets </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.itarget</span></td><td class="c028"><span class="c012">%.otarget </span></td></tr>
<tr><td class="c029"><span class="c012"> ocaml</span></td><td class="c029"><span class="c012">%.mli %.mli.depends</span></td><td class="c028"><span class="c012">%.cmi </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, debug, ocaml</span></td><td class="c029"><span class="c012">%.mlpack %.cmi</span></td><td class="c028"><span class="c012">%.d.cmo </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, ocaml</span></td><td class="c029"><span class="c012">%.mlpack</span></td><td class="c028"><span class="c012">%.cmo %.cmi </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, ocaml</span></td><td class="c029"><span class="c012">%.mli %.ml %.ml.depends %.cmi</span></td><td class="c028"><span class="c012">%.d.cmo </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, ocaml</span></td><td class="c029"><span class="c012">%.mli %.ml %.ml.depends %.cmi</span></td><td class="c028"><span class="c012">%.cmo </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml, profile</span></td><td class="c029"><span class="c012">%.mlpack %.cmi</span></td><td class="c028"><span class="c012">%.p.cmx %.p.o </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml</span></td><td class="c029"><span class="c012">%.mlpack %.cmi</span></td><td class="c028"><span class="c012">%.cmx %.o </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml, profile</span></td><td class="c029"><span class="c012">%.ml %.ml.depends %.cmi</span></td><td class="c028"><span class="c012">%.p.cmx %.p.o </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml</span></td><td class="c029"><span class="c012">%.ml %.ml.depends %.cmi</span></td><td class="c028"><span class="c012">%.cmx %.o </span></td></tr>
<tr><td class="c029"><span class="c012"> debug, ocaml</span></td><td class="c029"><span class="c012">%.ml %.ml.depends %.cmi</span></td><td class="c028"><span class="c012">%.d.cmo </span></td></tr>
<tr><td class="c029"><span class="c012"> ocaml</span></td><td class="c029"><span class="c012">%.ml %.ml.depends</span></td><td class="c028"><span class="c012">%.cmo %.cmi </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, debug, ocaml, program</span></td><td class="c029"><span class="c012">%.d.cmo</span></td><td class="c028"><span class="c012">%.d.byte </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, ocaml, program</span></td><td class="c029"><span class="c012">%.cmo</span></td><td class="c028"><span class="c012">%.byte </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml, profile, program</span></td><td class="c029"><span class="c012">%.p.cmx %.p.o</span></td><td class="c028"><span class="c012">%.p.native </span></td></tr>
<tr><td class="c029"><span class="c012"> native, ocaml, program</span></td><td class="c029"><span class="c012">%.cmx %.o</span></td><td class="c028"><span class="c012">%.native </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, debug, library, ocaml</span></td><td class="c029"><span class="c012">%.mllib</span></td><td class="c028"><span class="c012">%.d.cma </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, library, ocaml</span></td><td class="c029"><span class="c012">%.mllib</span></td><td class="c028"><span class="c012">%.cma </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, debug, library, ocaml</span></td><td class="c029"><span class="c012">%.d.cmo</span></td><td class="c028"><span class="c012">%.d.cma </span></td></tr>
<tr><td class="c029"><span class="c012"> byte, library, ocaml</span></td><td class="c029"><span class="c012">%.cmo</span></td><td class="c028"><span class="c012">%.cma </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">lib%(libname).clib</span></td><td class="c028"><span class="c012">lib%(libname).a dll%(libname).so </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%(path)/lib%(libname).clib</span></td><td class="c028"><span class="c012">%(path)/lib%(libname).a %(path)/dll%(libname).so </span></td></tr>
<tr><td class="c029"><span class="c012"> library, native, ocaml, profile</span></td><td class="c029"><span class="c012">%.mllib</span></td><td class="c028"><span class="c012">%.p.cmxa %.p.a </span></td></tr>
<tr><td class="c029"><span class="c012"> library, native, ocaml</span></td><td class="c029"><span class="c012">%.mllib</span></td><td class="c028"><span class="c012">%.cmxa %.a </span></td></tr>
<tr><td class="c029"><span class="c012"> library, native, ocaml, profile</span></td><td class="c029"><span class="c012">%.p.cmx %.p.o</span></td><td class="c028"><span class="c012">%.p.cmxa %.p.a </span></td></tr>
<tr><td class="c029"><span class="c012"> library, native, ocaml</span></td><td class="c029"><span class="c012">%.cmx %.o</span></td><td class="c028"><span class="c012">%.cmxa %.a </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.ml</span></td><td class="c028"><span class="c012">%.ml.depends </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.mli</span></td><td class="c028"><span class="c012">%.mli.depends </span></td></tr>
<tr><td class="c029"><span class="c012"> ocaml</span></td><td class="c029"><span class="c012">%.mll</span></td><td class="c028"><span class="c012">%.ml </span></td></tr>
<tr><td class="c029"><span class="c012"> doc, ocaml</span></td><td class="c029"><span class="c012">%.mli %.mli.depends</span></td><td class="c028"><span class="c012">%.odoc </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.odocl</span></td><td class="c028"><span class="c012">%.docdir/index.html </span></td></tr>
<tr><td class="c029"><span class="c012"> ocaml</span></td><td class="c029"><span class="c012">%.mly</span></td><td class="c028"><span class="c012">%.ml %.mli </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.c</span></td><td class="c028"><span class="c012">%.o </span></td></tr>
<tr><td class="c029"><span class="c012">&nbsp;</span></td><td class="c029"><span class="c012">%.ml %.ml.depends</span></td><td class="c028"><span class="c012">%.inferred.mli </span></td></tr>
</tbody></table><span class="c012">
</span></div>
<hr class="ffootnoterule"><dl class="thefootnotes"><dt class="dt-thefootnotes">
<a id="note3" href="#text3">1</a></dt><dd class="dd-thefootnotes"><div class="footnotetext">The command must not contain newlines or parentheses.</div>
</dd><dt class="dt-thefootnotes"><a id="note4" href="#text4">2</a></dt><dd class="dd-thefootnotes"><div class="footnotetext">By the way, what’s the point of having a
declarative language if <span class="c007">make</span> can’t sort the dependencies in
topological order for giving them to <span class="c007">gcc</span> or whatever ?</div>
</dd></dl>
<hr>





<span class="authors c013">(Chapter written by Berke Durak and Nicolas Pouillard)</span><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>