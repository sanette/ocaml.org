<!-- ((! set title Manual !)) ((! set documentation !)) ((! set manual !)) ((! set nobreadcrumb !)) -->
<div class="manual content"><ul class="part_menu"><li><a href="core.html">The core library</a></li><li><a href="stdlib.html">The standard library</a></li><li><a href="libunix.html">The unix library: Unix system calls</a></li><li><a href="libnum.html">The num library: arbitrary-precision rational arithmetic</a></li><li><a href="libstr.html">The str library: regular expressions and string processing</a></li><li><a href="libthreads.html">The threads library</a></li><li><a href="libgraph.html">The graphics library</a></li><li><a href="libdynlink.html">The dynlink library: dynamic loading and linking of object files</a></li><li><a href="liblabltk.html">The LablTk library: Tcl/Tk GUI interface</a></li><li class="active"><a href="libbigarray.html">The bigarray library</a></li></ul>




<h1 class="chapter" id="sec477"><span>Chapter 29</span>&nbsp;&nbsp;The bigarray library</h1>
<header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">Version 4.01</a></div><div class="toc_title"><a href="#">The bigarray library</a></div><ul><li class="top"><a href="#">Top</a></li>
<li><a href="libbigarray.html#sec478">Module <span class="c007">Bigarray</span>: large, multi-dimensional, numerical arrays</a>
</li><li><a href="libbigarray.html#sec479">Big arrays in the OCaml-C interface</a>
</li></ul></nav></header>
<p>The <span class="c007">bigarray</span> library implements large, multi-dimensional, numerical
arrays. These arrays are called “big arrays” to distinguish them
from the standard OCaml arrays described in
<a href="../../api/4.01/Array.html">Module <span class="c007">Array</span></a>.
The main differences between “big arrays” and standard OCaml arrays
are as follows:
</p><ul class="itemize"><li class="li-itemize">
Big arrays are not limited in size, unlike OCaml arrays
(<span class="c007">float array</span> are limited to 2097151 elements on a 32-bit platform,
other <span class="c007">array</span> types to 4194303 elements).
</li><li class="li-itemize">Big arrays are multi-dimensional. Any number of dimensions
between 1 and 16 is supported. In contrast, OCaml arrays are
mono-dimensional and require encoding multi-dimensional arrays as
arrays of arrays.
</li><li class="li-itemize">Big arrays can only contain integers and floating-point
numbers, while OCaml arrays can contain arbitrary OCaml data types.
However, big arrays provide more space-efficient storage of integer
and floating-point elements, in particular because they support
“small” types such as single-precision floats and 8 and 16-bit
integers, in addition to the standard OCaml types of double-precision
floats and 32 and 64-bit integers.
</li><li class="li-itemize">The memory layout of big arrays is entirely compatible with that
of arrays in C and Fortran, allowing large arrays to be passed back
and forth between OCaml code and C / Fortran code with no data copying
at all.
</li><li class="li-itemize">Big arrays support interesting high-level operations that normal
arrays do not provide efficiently, such as extracting sub-arrays and
“slicing” a multi-dimensional array along certain dimensions, all
without any copying.
</li></ul><p>
Programs that use the <span class="c007">bigarray</span> library must be linked as follows:
</p><pre>        ocamlc <span class="c013">other options</span> bigarray.cma <span class="c013">other files</span>
        ocamlopt <span class="c013">other options</span> bigarray.cmxa <span class="c013">other files</span>
</pre><p>
For interactive use of the <span class="c007">bigarray</span> library, do:
</p><pre>        ocamlmktop -o mytop bigarray.cma
        ./mytop
</pre><p>
or (if dynamic linking of C libraries is supported on your platform),
start <span class="c007">ocaml</span> and type <span class="c007">#load "bigarray.cma";;</span>.</p>
<h2 class="section" id="sec478">1&nbsp;&nbsp;Module <span class="c007">Bigarray</span>: large, multi-dimensional, numerical arrays</h2>
<ul class="ftoc2"><li class="li-links">
<a href="../../api/4.01/Bigarray.html">Module <span class="c007">Bigarray</span></a>
</li></ul>
<h2 class="section" id="sec479">2&nbsp;&nbsp;Big arrays in the OCaml-C interface</h2>
<p>C stub code that interface C or Fortran code with OCaml code, as
described in chapter&nbsp;<a href="intfc.html#c%3Aintf-c">19</a>, can exploit big arrays as
follows.</p>
<h3 class="subsection" id="sec480">2.1&nbsp;&nbsp;Include file</h3>
<p>The include file <span class="c007">&lt;caml/bigarray.h&gt;</span> must be included in the C stub
file. It declares the functions, constants and macros discussed
below.</p>
<h3 class="subsection" id="sec481">2.2&nbsp;&nbsp;Accessing an OCaml bigarray from C or Fortran</h3>
<p>If <span class="c013">v</span> is a OCaml <span class="c007">value</span> representing a big array, the expression
<span class="c007">Caml_ba_data_val(</span><span class="c013">v</span><span class="c007">)</span> returns a pointer to the data part of the array.
This pointer is of type <span class="c007">void *</span> and can be cast to the appropriate C
type for the array (e.g. <span class="c007">double []</span>, <span class="c007">char [][10]</span>, etc).</p><p>Various characteristics of the OCaml big array can be consulted from C
as follows:
</p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">C expression</span></td><td class="c021"><span class="c019">Returns</span> </td></tr>
<tr><td class="c023">
<span class="c007">Caml_ba_array_val(</span><span class="c013">v</span><span class="c007">)-&gt;num_dims</span></td><td class="c023">number of dimensions </td></tr>
<tr><td class="c023"><span class="c007">Caml_ba_array_val(</span><span class="c013">v</span><span class="c007">)-&gt;dim[</span><span class="c013">i</span><span class="c007">]</span></td><td class="c023"><span class="c013">i</span>-th dimension </td></tr>
<tr><td class="c023"><span class="c007">Caml_ba_array_val(</span><span class="c013">v</span><span class="c007">)-&gt;flags &amp; BIGARRAY_KIND_MASK</span></td><td class="c023">kind of array elements </td></tr>
</tbody></table></div><p>
The kind of array elements is one of the following constants:
</p><div class="center"><table class="c001 cellpadding1" border="1"><tbody><tr><td class="c021"><span class="c019">Constant</span></td><td class="c021"><span class="c019">Element kind</span> </td></tr>
<tr><td class="c023">
<span class="c007">CAML_BA_FLOAT32</span></td><td class="c023">32-bit single-precision floats </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_FLOAT64</span></td><td class="c023">64-bit double-precision floats </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_SINT8</span></td><td class="c023">8-bit signed integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_UINT8</span></td><td class="c023">8-bit unsigned integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_SINT16</span></td><td class="c023">16-bit signed integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_UINT16</span></td><td class="c023">16-bit unsigned integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_INT32</span></td><td class="c023">32-bit signed integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_INT64</span></td><td class="c023">64-bit signed integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_CAML_INT</span></td><td class="c023">31- or 63-bit signed integers </td></tr>
<tr><td class="c023"><span class="c007">CAML_BA_NATIVE_INT</span></td><td class="c023">32- or 64-bit (platform-native) integers </td></tr>
</tbody></table></div><p>
The following example shows the passing of a two-dimensional big array
to a C function and a Fortran function.
</p><pre>    extern void my_c_function(double * data, int dimx, int dimy);
    extern void my_fortran_function_(double * data, int * dimx, int * dimy);

    value caml_stub(value bigarray)
    {
      int dimx = Caml_ba_array_val(bigarray)-&gt;dim[0];
      int dimy = Caml_ba_array_val(bigarray)-&gt;dim[1];
      /* C passes scalar parameters by value */
      my_c_function(Caml_ba_data_val(bigarray), dimx, dimy);
      /* Fortran passes all parameters by reference */
      my_fortran_function_(Caml_ba_data_val(bigarray), &amp;dimx, &amp;dimy);
      return Val_unit;
    }
</pre>
<h3 class="subsection" id="sec482">2.3&nbsp;&nbsp;Wrapping a C or Fortran array as an OCaml big array</h3>
<p>A pointer <span class="c013">p</span> to an already-allocated C or Fortran array can be
wrapped and returned to OCaml as a big array using the <span class="c007">caml_ba_alloc</span>
or <span class="c007">caml_ba_alloc_dims</span> functions.
</p><ul class="itemize"><li class="li-itemize">
<span class="c007">caml_ba_alloc(</span><span class="c013">kind</span> <span class="c007">|</span> <span class="c013">layout</span>, <span class="c013">numdims</span>, <span class="c013">p</span>, <span class="c013">dims</span><span class="c007">)</span><p>Return an OCaml big array wrapping the data pointed to by <span class="c013">p</span>.
<span class="c013">kind</span> is the kind of array elements (one of the <span class="c007">CAML_BA_</span>
kind constants above). <span class="c013">layout</span> is <span class="c007">CAML_BA_C_LAYOUT</span> for an
array with C layout and <span class="c007">CAML_BA_FORTRAN_LAYOUT</span> for an array with
Fortran layout. <span class="c013">numdims</span> is the number of dimensions in the
array. <span class="c013">dims</span> is an array of <span class="c013">numdims</span> long integers, giving
the sizes of the array in each dimension.</p></li><li class="li-itemize"><span class="c007">caml_ba_alloc_dims(</span><span class="c013">kind</span> <span class="c007">|</span> <span class="c013">layout</span>, <span class="c013">numdims</span>,
<span class="c013">p</span>, <span class="c007">(long) </span><span class="c013">dim</span><sub>1</sub>, <span class="c007">(long) </span><span class="c013">dim</span><sub>2</sub>, …, <span class="c007">(long) </span><span class="c013">dim</span><sub><span class="c013">numdims</span></sub><span class="c007">)</span><p>Same as <span class="c007">caml_ba_alloc</span>, but the sizes of the array in each dimension
are listed as extra arguments in the function call, rather than being
passed as an array.
</p></li></ul><p>
The following example illustrates how statically-allocated C and
Fortran arrays can be made available to OCaml.
</p><pre>    extern long my_c_array[100][200];
    extern float my_fortran_array_[300][400];

    value caml_get_c_array(value unit)
    {
      long dims[2];
      dims[0] = 100; dims[1] = 200;
      return caml_ba_alloc(CAML_BA_NATIVE_INT | CAML_BA_C_LAYOUT,
                           2, my_c_array, dims);
    }

    value caml_get_fortran_array(value unit)
    {
      return caml_ba_alloc_dims(CAML_BA_FLOAT32 | CAML_BA_FORTRAN_LAYOUT,
                                2, my_fortran_array_, 300L, 400L);
    }
</pre>
<hr>





<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>