<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.04</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Index of types</a></div><ul></ul></nav></header>

<h1>Index of types</h1>
<table>
<tbody><tr><td align="left"><br>A</td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEacc">acc</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEacc_formatting_gen">acc_formatting_gen</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEaccess_permission">access_permission</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Flags for the <a href="UnixLabels.html#VALaccess"><code class="code"><span class="constructor">UnixLabels</span>.access</code></a> call.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEaccess_permission">access_permission</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Flags for the <a href="Unix.html#VALaccess"><code class="code"><span class="constructor">Unix</span>.access</code></a> call.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEaddr_info">addr_info</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Address information returned by <a href="Unix.html#VALgetaddrinfo"><code class="code"><span class="constructor">Unix</span>.getaddrinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEaddr_info">addr_info</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Address information returned by <a href="Unix.html#VALgetaddrinfo"><code class="code"><span class="constructor">Unix</span>.getaddrinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Gc.html#TYPEalarm">alarm</a> [<a href="Gc.html">Gc</a>]</td>
<td><div class="info">
An alarm is a piece of data that calls a user function at the end of
   each major GC cycle.
</div>
</td></tr>
<tr><td><a href="Arg.html#TYPEanon_fun">anon_fun</a> [<a href="Arg.html">Arg</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEarg_label">arg_label</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEattribute">attribute</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEattributes">attributes</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Ast_helper.html#TYPEattrs">attrs</a> [<a href="Ast_helper.html">Ast_helper</a>]</td>
<td></td></tr>
<tr><td align="left"><br>B</td></tr>
<tr><td><a href="Sys.html#TYPEbackend_type">backend_type</a> [<a href="Sys.html">Sys</a>]</td>
<td><div class="info">
Currently, the official distribution only supports <code class="code"><span class="constructor">Native</span></code> and
    <code class="code"><span class="constructor">Bytecode</span></code>, but it can be other backends with alternative
    compilers, for example, javascript.
</div>
</td></tr>
<tr><td><a href="Printexc.html#TYPEbacktrace_slot">backtrace_slot</a> [<a href="Printexc.html">Printexc</a>]</td>
<td><div class="info">
The abstract type <code class="code">backtrace_slot</code> represents a single slot of
    a backtrace.
</div>
</td></tr>
<tr><td><a href="Big_int.html#TYPEbig_int">big_int</a> [<a href="Big_int.html">Big_int</a>]</td>
<td><div class="info">
The type of big integers.
</div>
</td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEblock_type">block_type</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Depend.html#TYPEbound_map">bound_map</a> [<a href="Depend.html">Depend</a>]</td>
<td></td></tr>
<tr><td align="left"><br>C</td></tr>
<tr><td><a href="Bigarray.html#TYPEc_layout">c_layout</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td><div class="info">
See <a href="Bigarray.html#VALfortran_layout"><code class="code"><span class="constructor">Bigarray</span>.fortran_layout</code></a>.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEcase">case</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Event.html#TYPEchannel">channel</a> [<a href="Event.html">Event</a>]</td>
<td><div class="info">
The type of communication channels carrying values of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEchar_set">char_set</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_declaration">class_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_description">class_description</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_expr">class_expr</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_expr_desc">class_expr_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_field">class_field</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_field_desc">class_field_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_field_kind">class_field_kind</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_infos">class_infos</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_signature">class_signature</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_structure">class_structure</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_type">class_type</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_type_declaration">class_type_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_type_desc">class_type_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_type_field">class_type_field</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEclass_type_field_desc">class_type_field_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEclosed_flag">closed_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEclosure">closure</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Color.html#TYPEcolor">color</a> [<a href="Misc.Color.html">Misc.Color</a>]</td>
<td></td></tr>
<tr><td><a href="Graphics.html#TYPEcolor">color</a> [<a href="Graphics.html">Graphics</a>]</td>
<td><div class="info">
A color is specified by its R, G, B components.
</div>
</td></tr>
<tr><td><a href="Timings.html#TYPEcompiler_pass">compiler_pass</a> [<a href="Timings.html">Timings</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEcomplex32_elt">complex32_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEcomplex64_elt">complex64_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Strongly_connected_components.S.html#TYPEcomponent">component</a> [<a href="Strongly_connected_components.S.html">Strongly_connected_components.S</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEconstant">constant</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEconstant">constant</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEconstructor_arguments">constructor_arguments</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEconstructor_declaration">constructor_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Gc.html#TYPEcontrol">control</a> [<a href="Gc.html">Gc</a>]</td>
<td><div class="info">
The GC parameters are given as a <code class="code">control</code> record.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEcore_type">core_type</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEcore_type_desc">core_type_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEcounter">counter</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEcustom_arity">custom_arity</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td align="left"><br>D</td></tr>
<tr><td><a href="Weak.S.html#TYPEdata">data</a> [<a href="Weak.S.html">Weak.S</a>]</td>
<td><div class="info">
The type of the elements stored in the table.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEdir_handle">dir_handle</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of descriptors over opened directories.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEdir_handle">dir_handle</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of descriptors over opened directories.
</div>
</td></tr>
<tr><td><a href="Strongly_connected_components.S.html#TYPEdirected_graph">directed_graph</a> [<a href="Strongly_connected_components.S.html">Strongly_connected_components.S</a>]</td>
<td><div class="info">
If (a -&gt; set) belongs to the map, it means that there are edges
      from <code class="code">a</code> to every element of <code class="code">set</code>.
</div>
</td></tr>
<tr><td><a href="Asttypes.html#TYPEdirection_flag">direction_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEdirective_argument">directive_argument</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Arg.html#TYPEdoc">doc</a> [<a href="Arg.html">Arg</a>]</td>
<td></td></tr>
<tr><td><a href="Docstrings.html#TYPEdocs">docs</a> [<a href="Docstrings.html">Docstrings</a>]</td>
<td></td></tr>
<tr><td><a href="Docstrings.html#TYPEdocstring">docstring</a> [<a href="Docstrings.html">Docstrings</a>]</td>
<td><div class="info">
Documentation comments
</div>
</td></tr>
<tr><td align="left"><br>E</td></tr>
<tr><td><a href="MoreLabels.Set.S.html#TYPEelt">elt</a> [<a href="MoreLabels.Set.S.html">MoreLabels.Set.S</a>]</td>
<td></td></tr>
<tr><td><a href="Set.S.html#TYPEelt">elt</a> [<a href="Set.S.html">Set.S</a>]</td>
<td><div class="info">
The type of the set elements.
</div>
</td></tr>
<tr><td><a href="Ephemeron.GenHashTable.html#TYPEequal">equal</a> [<a href="Ephemeron.GenHashTable.html">Ephemeron.GenHashTable</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEerror">error</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of error codes.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEerror">error</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of error codes.
</div>
</td></tr>
<tr><td><a href="Syntaxerr.html#TYPEerror">error</a> [<a href="Syntaxerr.html">Syntaxerr</a>]</td>
<td></td></tr>
<tr><td><a href="Location.html#TYPEerror">error</a> [<a href="Location.html">Location</a>]</td>
<td></td></tr>
<tr><td><a href="Lexer.html#TYPEerror">error</a> [<a href="Lexer.html">Lexer</a>]</td>
<td></td></tr>
<tr><td><a href="Dynlink.html#TYPEerror">error</a> [<a href="Dynlink.html">Dynlink</a>]</td>
<td></td></tr>
<tr><td><a href="Attr_helper.html#TYPEerror">error</a> [<a href="Attr_helper.html">Attr_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Graphics.html#TYPEevent">event</a> [<a href="Graphics.html">Graphics</a>]</td>
<td><div class="info">
To specify events to wait for.
</div>
</td></tr>
<tr><td><a href="Event.html#TYPEevent">event</a> [<a href="Event.html">Event</a>]</td>
<td><div class="info">
The type of communication events returning a result of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEexpression">expression</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEexpression_desc">expression_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEextension">extension</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEextension_constructor">extension_constructor</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEextension_constructor_kind">extension_constructor_kind</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Marshal.html#TYPEextern_flags">extern_flags</a> [<a href="Marshal.html">Marshal</a>]</td>
<td><div class="info">
The flags to the <code class="code"><span class="constructor">Marshal</span>.to_*</code> functions below.
</div>
</td></tr>
<tr><td align="left"><br>F</td></tr>
<tr><td><a href="Timings.html#TYPEfile">file</a> [<a href="Timings.html">Timings</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEfile_descr">file_descr</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The abstract type of file descriptors.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEfile_descr">file_descr</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The abstract type of file descriptors.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEfile_kind">file_kind</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEfile_kind">file_kind</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="Scanf.Scanning.html#TYPEfile_name">file_name</a> [<a href="Scanf.Scanning.html">Scanf.Scanning</a>]</td>
<td><div class="info">
A convenient alias to designate a file name.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEfile_perm">file_perm</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of file access rights, e.g.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEfile_perm">file_perm</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of file access rights, e.g.
</div>
</td></tr>
<tr><td><a href="Bigarray.html#TYPEfloat32_elt">float32_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEfloat64_elt">float64_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEfloat_conv">float_conv</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEflow_action">flow_action</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEflow_action">flow_action</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEflush_queue">flush_queue</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEflush_queue">flush_queue</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEfmt">fmt</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td><div class="info">
List of format elements.
</div>
</td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEfmt_ebb">fmt_ebb</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEfmtty">fmtty</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEfmtty_rel">fmtty_rel</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Pervasives.html#TYPEformat">format</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td></td></tr>
<tr><td><a href="Pervasives.html#TYPEformat4">format4</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td></td></tr>
<tr><td><a href="Pervasives.html#TYPEformat6">format6</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEformat6">format6</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Format.html#TYPEformatter">formatter</a> [<a href="Format.html">Format</a>]</td>
<td><div class="info">
Abstract data corresponding to a pretty-printer (also called a
  formatter) and all its machinery.
</div>
</td></tr>
<tr><td><a href="Format.html#TYPEformatter_out_functions">formatter_out_functions</a> [<a href="Format.html">Format</a>]</td>
<td></td></tr>
<tr><td><a href="Format.html#TYPEformatter_tag_functions">formatter_tag_functions</a> [<a href="Format.html">Format</a>]</td>
<td><div class="info">
The tag handling functions specific to a formatter:
  <code class="code">mark</code> versions are the 'tag marking' functions that associate a string
  marker to a tag in order for the pretty-printing engine to flush
  those markers as 0 length tokens in the output device of the formatter.
</div>
</td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEformatting_gen">formatting_gen</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEformatting_lit">formatting_lit</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEfortran_layout">fortran_layout</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td><div class="info">
To facilitate interoperability with existing C and Fortran code,
   this library supports two different memory layouts for big arrays,
   one compatible with the C conventions,
   the other compatible with the Fortran conventions.
</div>
</td></tr>
<tr><td><a href="Pervasives.html#TYPEfpclass">fpclass</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td><div class="info">
The five classes of floating-point numbers, as determined by
   the <a href="Pervasives.html#VALclassify_float"><code class="code">classify_float</code></a> function.
</div>
</td></tr>
<tr><td align="left"><br>G</td></tr>
<tr><td><a href="UnixLabels.html#TYPEgetaddrinfo_option">getaddrinfo_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Options to <a href="Unix.html#VALgetaddrinfo"><code class="code"><span class="constructor">Unix</span>.getaddrinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEgetaddrinfo_option">getaddrinfo_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Options to <a href="Unix.html#VALgetaddrinfo"><code class="code"><span class="constructor">Unix</span>.getaddrinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEgetnameinfo_option">getnameinfo_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Options to <a href="Unix.html#VALgetnameinfo"><code class="code"><span class="constructor">Unix</span>.getnameinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEgetnameinfo_option">getnameinfo_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Options to <a href="Unix.html#VALgetnameinfo"><code class="code"><span class="constructor">Unix</span>.getnameinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEgroup_entry">group_entry</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">groups</code> database.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEgroup_entry">group_entry</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">groups</code> database.
</div>
</td></tr>
<tr><td align="left"><br>H</td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEheter_list">heter_list</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.html#TYPEhook_info">hook_info</a> [<a href="Misc.html">Misc</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEhost_entry">host_entry</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">hosts</code> database.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEhost_entry">host_entry</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">hosts</code> database.
</div>
</td></tr>
<tr><td align="left"><br>I</td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEignored">ignored</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Graphics.html#TYPEimage">image</a> [<a href="Graphics.html">Graphics</a>]</td>
<td><div class="info">
The abstract type for images, in internal representation.
</div>
</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEimpl">impl</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Scanf.Scanning.html#TYPEin_channel">in_channel</a> [<a href="Scanf.Scanning.html">Scanf.Scanning</a>]</td>
<td><div class="info">
The notion of input channel for the <code class="code"><span class="constructor">Scanf</span></code> module:
   those channels provide all the machinery necessary to read from any source
   of characters, including a <code class="code">!<span class="constructor">Pervasives</span>.in_channel</code> value.
</div>
</td></tr>
<tr><td><a href="Pervasives.html#TYPEin_channel">in_channel</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td><div class="info">
The type of input channel.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEinclude_declaration">include_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEinclude_description">include_description</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEinclude_infos">include_infos</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEinet_addr">inet_addr</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The abstract type of Internet addresses.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEinet_addr">inet_addr</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The abstract type of Internet addresses.
</div>
</td></tr>
<tr><td><a href="Docstrings.html#TYPEinfo">info</a> [<a href="Docstrings.html">Docstrings</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEinit_table">init_table</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Clflags.html#TYPEinlining_arguments">inlining_arguments</a> [<a href="Clflags.html">Clflags</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint16_signed_elt">int16_signed_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint16_unsigned_elt">int16_unsigned_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint32_elt">int32_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint64_elt">int64_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint8_signed_elt">int8_signed_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint8_unsigned_elt">int8_unsigned_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEint_conv">int_conv</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEint_elt">int_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEinterval_timer">interval_timer</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The three kinds of interval timers.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEinterval_timer">interval_timer</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The three kinds of interval timers.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEinterval_timer_status">interval_timer_status</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type describing the status of an interval timer
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEinterval_timer_status">interval_timer_status</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type describing the status of an interval timer
</div>
</td></tr>
<tr><td><a href="Ast_iterator.html#TYPEiterator">iterator</a> [<a href="Ast_iterator.html">Ast_iterator</a>]</td>
<td><div class="info">
A <code class="code">iterator</code> record implements one "method" per syntactic category,
    using an open recursion style: each method takes as its first
    argument the iterator to be applied to children in the syntax
    tree.
</div>
</td></tr>
<tr><td align="left"><br>K</td></tr>
<tr><td><a href="MoreLabels.Map.S.html#TYPEkey">key</a> [<a href="MoreLabels.Map.S.html">MoreLabels.Map.S</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.SeededS.html#TYPEkey">key</a> [<a href="MoreLabels.Hashtbl.SeededS.html">MoreLabels.Hashtbl.SeededS</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.S.html#TYPEkey">key</a> [<a href="MoreLabels.Hashtbl.S.html">MoreLabels.Hashtbl.S</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.SeededS.html#TYPEkey">key</a> [<a href="Hashtbl.SeededS.html">Hashtbl.SeededS</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.S.html#TYPEkey">key</a> [<a href="Hashtbl.S.html">Hashtbl.S</a>]</td>
<td></td></tr>
<tr><td><a href="Map.S.html#TYPEkey">key</a> [<a href="Map.S.html">Map.S</a>]</td>
<td><div class="info">
The type of the map keys.
</div>
</td></tr>
<tr><td><a href="Arg.html#TYPEkey">key</a> [<a href="Arg.html">Arg</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPEkind">kind</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td><div class="info">
To each element kind is associated an OCaml type, which is
   the type of OCaml values that can be stored in the big array
   or read back from it.
</div>
</td></tr>
<tr><td align="left"><br>L</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPElabel">label</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPElabel">label</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPElabel_declaration">label_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Bigarray.html#TYPElayout">layout</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Lexing.html#TYPElexbuf">lexbuf</a> [<a href="Lexing.html">Lexing</a>]</td>
<td><div class="info">
The type of lexer buffers.
</div>
</td></tr>
<tr><td><a href="Ast_helper.html#TYPElid">lid</a> [<a href="Ast_helper.html">Ast_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Ccomp.html#TYPElink_mode">link_mode</a> [<a href="Ccomp.html">Ccomp</a>]</td>
<td></td></tr>
<tr><td><a href="Dynlink.html#TYPElinking_error">linking_error</a> [<a href="Dynlink.html">Dynlink</a>]</td>
<td></td></tr>
<tr><td><a href="Location.html#TYPEloc">loc</a> [<a href="Location.html">Location</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEloc">loc</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Ast_helper.html#TYPEloc">loc</a> [<a href="Ast_helper.html">Ast_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Printexc.html#TYPElocation">location</a> [<a href="Printexc.html">Printexc</a>]</td>
<td><div class="info">
The type of location information found in backtraces.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPElock_command">lock_command</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Commands for <a href="UnixLabels.html#VALlockf"><code class="code"><span class="constructor">UnixLabels</span>.lockf</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPElock_command">lock_command</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Commands for <a href="Unix.html#VALlockf"><code class="code"><span class="constructor">Unix</span>.lockf</code></a>.
</div>
</td></tr>
<tr><td align="left"><br>M</td></tr>
<tr><td><a href="Depend.html#TYPEmap_tree">map_tree</a> [<a href="Depend.html">Depend</a>]</td>
<td></td></tr>
<tr><td><a href="Ast_mapper.html#TYPEmapper">mapper</a> [<a href="Ast_mapper.html">Ast_mapper</a>]</td>
<td><div class="info">
A mapper record implements one "method" per syntactic category,
    using an open recursion style: each method takes as its first
    argument the mapper to be applied to children in the syntax
    tree.
</div>
</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEmeth">meth</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_binding">module_binding</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_declaration">module_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_expr">module_expr</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_expr_desc">module_expr_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_type">module_type</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_type_declaration">module_type_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEmodule_type_desc">module_type_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEmsg_flag">msg_flag</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEmsg_flag">msg_flag</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEmutable_char_set">mutable_char_set</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEmutable_flag">mutable_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td align="left"><br>N</td></tr>
<tr><td><a href="UnixLabels.html#TYPEname_info">name_info</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Host and service information returned by <a href="Unix.html#VALgetnameinfo"><code class="code"><span class="constructor">Unix</span>.getnameinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEname_info">name_info</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Host and service information returned by <a href="Unix.html#VALgetnameinfo"><code class="code"><span class="constructor">Unix</span>.getnameinfo</code></a>.
</div>
</td></tr>
<tr><td><a href="Bigarray.html#TYPEnativeint_elt">nativeint_elt</a> [<a href="Bigarray.html">Bigarray</a>]</td>
<td></td></tr>
<tr><td><a href="Num.html#TYPEnum">num</a> [<a href="Num.html">Num</a>]</td>
<td><div class="info">
The type of numbers.
</div>
</td></tr>
<tr><td align="left"><br>O</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEobj">obj</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Obj.Ephemeron.html#TYPEobj_t">obj_t</a> [<a href="Obj.Ephemeron.html">Obj.Ephemeron</a>]</td>
<td><div class="info">
alias for <a href="Obj.html#TYPEt"><code class="code"><span class="constructor">Obj</span>.t</code></a>
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEopen_description">open_description</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEopen_flag">open_flag</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The flags to <a href="UnixLabels.html#VALopenfile"><code class="code"><span class="constructor">UnixLabels</span>.openfile</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEopen_flag">open_flag</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The flags to <a href="Unix.html#VALopenfile"><code class="code"><span class="constructor">Unix</span>.openfile</code></a>.
</div>
</td></tr>
<tr><td><a href="Pervasives.html#TYPEopen_flag">open_flag</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td><div class="info">
Opening modes for <a href="Pervasives.html#VALopen_out_gen"><code class="code">open_out_gen</code></a> and
  <a href="Pervasives.html#VALopen_in_gen"><code class="code">open_in_gen</code></a>.
</div>
</td></tr>
<tr><td><a href="Pervasives.html#TYPEout_channel">out_channel</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td><div class="info">
The type of output channel.
</div>
</td></tr>
<tr><td><a href="Asttypes.html#TYPEoverride_flag">override_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td align="left"><br>P</td></tr>
<tr><td><a href="Parsetree.html#TYPEpackage_type">package_type</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEpad_option">pad_option</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEpadding">padding</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEpadty">padty</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormat.html#TYPEparam_format_ebb">param_format_ebb</a> [<a href="CamlinternalFormat.html">CamlinternalFormat</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEparams">params</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Clflags.Float_arg_helper.html#TYPEparse_result">parse_result</a> [<a href="Clflags.Float_arg_helper.html">Clflags.Float_arg_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Clflags.Int_arg_helper.html#TYPEparse_result">parse_result</a> [<a href="Clflags.Int_arg_helper.html">Clflags.Int_arg_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Arg_helper.Make.html#TYPEparse_result">parse_result</a> [<a href="Arg_helper.Make.html">Arg_helper.Make</a>]</td>
<td></td></tr>
<tr><td><a href="Clflags.Float_arg_helper.html#TYPEparsed">parsed</a> [<a href="Clflags.Float_arg_helper.html">Clflags.Float_arg_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Clflags.Int_arg_helper.html#TYPEparsed">parsed</a> [<a href="Clflags.Int_arg_helper.html">Clflags.Int_arg_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Arg_helper.Make.html#TYPEparsed">parsed</a> [<a href="Arg_helper.Make.html">Arg_helper.Make</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEpasswd_entry">passwd_entry</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">passwd</code> database.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEpasswd_entry">passwd_entry</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">passwd</code> database.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEpattern">pattern</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEpattern_desc">pattern_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEpayload">payload</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Lexing.html#TYPEposition">position</a> [<a href="Lexing.html">Lexing</a>]</td>
<td><div class="info">
A value of type <code class="code">position</code> describes a point in a source file.
</div>
</td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEprec_option">prec_option</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalFormatBasics.html#TYPEprecision">precision</a> [<a href="CamlinternalFormatBasics.html">CamlinternalFormatBasics</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEprivate_flag">private_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEprocess_status">process_status</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The termination status of a process.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEprocess_status">process_status</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The termination status of a process.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEprocess_times">process_times</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The execution times (CPU times) of a process.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEprocess_times">process_times</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The execution times (CPU times) of a process.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEprotocol_entry">protocol_entry</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">protocols</code> database.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEprotocol_entry">protocol_entry</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">protocols</code> database.
</div>
</td></tr>
<tr><td align="left"><br>R</td></tr>
<tr><td><a href="Ratio.html#TYPEratio">ratio</a> [<a href="Ratio.html">Ratio</a>]</td>
<td></td></tr>
<tr><td><a href="Printexc.html#TYPEraw_backtrace">raw_backtrace</a> [<a href="Printexc.html">Printexc</a>]</td>
<td><div class="info">
The abstract type <code class="code">raw_backtrace</code> stores a backtrace in
    a low-level format, instead of directly exposing them as string as
    the <code class="code">get_backtrace()</code> function does.
</div>
</td></tr>
<tr><td><a href="Printexc.html#TYPEraw_backtrace_slot">raw_backtrace_slot</a> [<a href="Printexc.html">Printexc</a>]</td>
<td><div class="info">
This type allows direct access to raw backtrace slots, without any
    conversion in an OCaml-usable data-structure.
</div>
</td></tr>
<tr><td><a href="Asttypes.html#TYPErec_flag">rec_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Pervasives.html#TYPEref">ref</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td><div class="info">
The type of references (mutable indirection cells) containing
   a value of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Misc.html#TYPEref_and_value">ref_and_value</a> [<a href="Misc.html">Misc</a>]</td>
<td></td></tr>
<tr><td><a href="Str.html#TYPEregexp">regexp</a> [<a href="Str.html">Str</a>]</td>
<td><div class="info">
The type of compiled regular expressions.
</div>
</td></tr>
<tr><td><a href="Pervasives.html#TYPEresult">result</a> [<a href="Pervasives.html">Pervasives</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPErow_field">row_field</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td align="left"><br>S</td></tr>
<tr><td><a href="Scanf.Scanning.html#TYPEscanbuf">scanbuf</a> [<a href="Scanf.Scanning.html">Scanf.Scanning</a>]</td>
<td><div class="info">
The type of scanning buffers.
</div>
</td></tr>
<tr><td><a href="Scanf.html#TYPEscanner">scanner</a> [<a href="Scanf.html">Scanf</a>]</td>
<td><div class="info">
The type of formatted input scanners: <code class="code">(<span class="keywordsign">'</span>a,&nbsp;<span class="keywordsign">'</span>b,&nbsp;<span class="keywordsign">'</span>c,&nbsp;<span class="keywordsign">'</span>d)&nbsp;scanner</code>
    is the type of a formatted input function that reads from some
    formatted input channel according to some format string; more
    precisely, if <code class="code">scan</code> is some formatted input function, then <code class="code">scan<br>
&nbsp;&nbsp;&nbsp;&nbsp;ic&nbsp;fmt&nbsp;f</code> applies <code class="code">f</code> to all the arguments specified by format
    string <code class="code">fmt</code>, when <code class="code">scan</code> has read those arguments from the
    <code class="code">!<span class="constructor">Scanning</span>.in_channel</code> formatted input channel <code class="code">ic</code>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEseek_command">seek_command</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Positioning modes for <a href="UnixLabels.html#VALlseek"><code class="code"><span class="constructor">UnixLabels</span>.lseek</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEseek_command">seek_command</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Positioning modes for <a href="Unix.html#VALlseek"><code class="code"><span class="constructor">Unix</span>.lseek</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEservice_entry">service_entry</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">services</code> database.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEservice_entry">service_entry</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Structure of entries in the <code class="code">services</code> database.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsetattr_when">setattr_when</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEsetattr_when">setattr_when</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Color.html#TYPEsetting">setting</a> [<a href="Misc.Color.html">Misc.Color</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalMod.html#TYPEshape">shape</a> [<a href="CamlinternalMod.html">CamlinternalMod</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEshutdown_command">shutdown_command</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of commands for <code class="code">shutdown</code>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEshutdown_command">shutdown_command</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of commands for <code class="code">shutdown</code>.
</div>
</td></tr>
<tr><td><a href="Sys.html#TYPEsignal_behavior">signal_behavior</a> [<a href="Sys.html">Sys</a>]</td>
<td><div class="info">
What to do when receiving a signal: <code class="code"><span class="constructor">Signal_default</span></code>: take the default behavior
     (usually: abort the program), <code class="code"><span class="constructor">Signal_ignore</span></code>: ignore the signal, <code class="code"><span class="constructor">Signal_handle</span>&nbsp;f</code>: call function <code class="code">f</code>, giving it the signal
   number as argument.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEsignature">signature</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEsignature_item">signature_item</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEsignature_item_desc">signature_item_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEsigprocmask_command">sigprocmask_command</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEsigprocmask_command">sigprocmask_command</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEsockaddr">sockaddr</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEsockaddr">sockaddr</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_bool_option">socket_bool_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="UnixLabels.html#VALgetsockopt"><code class="code"><span class="constructor">UnixLabels</span>.getsockopt</code></a>
   and modified with <a href="UnixLabels.html#VALsetsockopt"><code class="code"><span class="constructor">UnixLabels</span>.setsockopt</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_bool_option">socket_bool_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="Unix.html#VALgetsockopt"><code class="code"><span class="constructor">Unix</span>.getsockopt</code></a>
   and modified with <a href="Unix.html#VALsetsockopt"><code class="code"><span class="constructor">Unix</span>.setsockopt</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_domain">socket_domain</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of socket domains.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_domain">socket_domain</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of socket domains.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_float_option">socket_float_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="UnixLabels.html#VALgetsockopt_float"><code class="code"><span class="constructor">UnixLabels</span>.getsockopt_float</code></a>
   and modified with <a href="UnixLabels.html#VALsetsockopt_float"><code class="code"><span class="constructor">UnixLabels</span>.setsockopt_float</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_float_option">socket_float_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="Unix.html#VALgetsockopt_float"><code class="code"><span class="constructor">Unix</span>.getsockopt_float</code></a>
   and modified with <a href="Unix.html#VALsetsockopt_float"><code class="code"><span class="constructor">Unix</span>.setsockopt_float</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_int_option">socket_int_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="UnixLabels.html#VALgetsockopt_int"><code class="code"><span class="constructor">UnixLabels</span>.getsockopt_int</code></a>
   and modified with <a href="UnixLabels.html#VALsetsockopt_int"><code class="code"><span class="constructor">UnixLabels</span>.setsockopt_int</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_int_option">socket_int_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="Unix.html#VALgetsockopt_int"><code class="code"><span class="constructor">Unix</span>.getsockopt_int</code></a>
   and modified with <a href="Unix.html#VALsetsockopt_int"><code class="code"><span class="constructor">Unix</span>.setsockopt_int</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_optint_option">socket_optint_option</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="Unix.html#VALgetsockopt_optint"><code class="code"><span class="constructor">Unix</span>.getsockopt_optint</code></a>
   and modified with <a href="Unix.html#VALsetsockopt_optint"><code class="code"><span class="constructor">Unix</span>.setsockopt_optint</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_optint_option">socket_optint_option</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The socket options that can be consulted with <a href="Unix.html#VALgetsockopt_optint"><code class="code"><span class="constructor">Unix</span>.getsockopt_optint</code></a>
   and modified with <a href="Unix.html#VALsetsockopt_optint"><code class="code"><span class="constructor">Unix</span>.setsockopt_optint</code></a>.
</div>
</td></tr>
<tr><td><a href="UnixLabels.html#TYPEsocket_type">socket_type</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type of socket kinds, specifying the semantics of
   communications.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEsocket_type">socket_type</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type of socket kinds, specifying the semantics of
   communications.
</div>
</td></tr>
<tr><td><a href="Timings.html#TYPEsource_provenance">source_provenance</a> [<a href="Timings.html">Timings</a>]</td>
<td></td></tr>
<tr><td><a href="Pprintast.html#TYPEspace_formatter">space_formatter</a> [<a href="Pprintast.html">Pprintast</a>]</td>
<td></td></tr>
<tr><td><a href="Arg.html#TYPEspec">spec</a> [<a href="Arg.html">Arg</a>]</td>
<td><div class="info">
The concrete type describing the behavior associated
   with a keyword.
</div>
</td></tr>
<tr><td><a href="Str.html#TYPEsplit_result">split_result</a> [<a href="Str.html">Str</a>]</td>
<td></td></tr>
<tr><td><a href="Gc.html#TYPEstat">stat</a> [<a href="Gc.html">Gc</a>]</td>
<td><div class="info">
The memory management counters are returned in a <code class="code">stat</code> record.
</div>
</td></tr>
<tr><td><a href="Warnings.html#TYPEstate">state</a> [<a href="Warnings.html">Warnings</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.html#TYPEstatistics">statistics</a> [<a href="MoreLabels.Hashtbl.html">MoreLabels.Hashtbl</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.html#TYPEstatistics">statistics</a> [<a href="Hashtbl.html">Hashtbl</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.LargeFile.html#TYPEstats">stats</a> [<a href="UnixLabels.LargeFile.html">UnixLabels.LargeFile</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEstats">stats</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The information returned by the <a href="UnixLabels.html#VALstat"><code class="code"><span class="constructor">UnixLabels</span>.stat</code></a> calls.
</div>
</td></tr>
<tr><td><a href="Unix.LargeFile.html#TYPEstats">stats</a> [<a href="Unix.LargeFile.html">Unix.LargeFile</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEstats">stats</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The information returned by the <a href="Unix.html#VALstat"><code class="code"><span class="constructor">Unix</span>.stat</code></a> calls.
</div>
</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEstats">stats</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Terminfo.html#TYPEstatus">status</a> [<a href="Terminfo.html">Terminfo</a>]</td>
<td></td></tr>
<tr><td><a href="Graphics.html#TYPEstatus">status</a> [<a href="Graphics.html">Graphics</a>]</td>
<td><div class="info">
To report events.
</div>
</td></tr>
<tr><td><a href="Ast_helper.html#TYPEstr">str</a> [<a href="Ast_helper.html">Ast_helper</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEstructure">structure</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEstructure_item">structure_item</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEstructure_item_desc">structure_item_desc</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Color.html#TYPEstyle">style</a> [<a href="Misc.Color.html">Misc.Color</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Color.html#TYPEstyles">styles</a> [<a href="Misc.Color.html">Misc.Color</a>]</td>
<td></td></tr>
<tr><td align="left"><br>T</td></tr>
<tr><td><a href="Weak.S.html#TYPEt">t</a> [<a href="Weak.S.html">Weak.S</a>]</td>
<td><div class="info">
The type of tables that contain elements of type <code class="code">data</code>.
</div>
</td></tr>
<tr><td><a href="Weak.html#TYPEt">t</a> [<a href="Weak.html">Weak</a>]</td>
<td><div class="info">
The type of arrays of weak pointers (weak arrays).
</div>
</td></tr>
<tr><td><a href="Warnings.html#TYPEt">t</a> [<a href="Warnings.html">Warnings</a>]</td>
<td></td></tr>
<tr><td><a href="Uchar.html#TYPEt">t</a> [<a href="Uchar.html">Uchar</a>]</td>
<td><div class="info">
The type for Unicode characters.
</div>
</td></tr>
<tr><td><a href="Thread.html#TYPEt">t</a> [<a href="Thread.html">Thread</a>]</td>
<td><div class="info">
The type of thread handles.
</div>
</td></tr>
<tr><td><a href="Tbl.html#TYPEt">t</a> [<a href="Tbl.html">Tbl</a>]</td>
<td></td></tr>
<tr><td><a href="String.html#TYPEt">t</a> [<a href="String.html">String</a>]</td>
<td><div class="info">
An alias for the type of strings.
</div>
</td></tr>
<tr><td><a href="Stream.html#TYPEt">t</a> [<a href="Stream.html">Stream</a>]</td>
<td><div class="info">
The type of streams holding values of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="StringLabels.html#TYPEt">t</a> [<a href="StringLabels.html">StringLabels</a>]</td>
<td><div class="info">
An alias for the type of strings.
</div>
</td></tr>
<tr><td><a href="Stack.html#TYPEt">t</a> [<a href="Stack.html">Stack</a>]</td>
<td><div class="info">
The type of stacks containing elements of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Spacetime.Series.html#TYPEt">t</a> [<a href="Spacetime.Series.html">Spacetime.Series</a>]</td>
<td><div class="info">
Type representing a file that will hold a series of heap snapshots
      together with additional information required to interpret those
      snapshots.
</div>
</td></tr>
<tr><td><a href="Random.State.html#TYPEt">t</a> [<a href="Random.State.html">Random.State</a>]</td>
<td><div class="info">
The type of PRNG states.
</div>
</td></tr>
<tr><td><a href="Queue.html#TYPEt">t</a> [<a href="Queue.html">Queue</a>]</td>
<td><div class="info">
The type of queues containing elements of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Printexc.Slot.html#TYPEt">t</a> [<a href="Printexc.Slot.html">Printexc.Slot</a>]</td>
<td></td></tr>
<tr><td><a href="Obj.Ephemeron.html#TYPEt">t</a> [<a href="Obj.Ephemeron.html">Obj.Ephemeron</a>]</td>
<td><div class="info">
an ephemeron cf <a href="Ephemeron.html"><code class="code"><span class="constructor">Ephemeron</span></code></a>
</div>
</td></tr>
<tr><td><a href="Obj.html#TYPEt">t</a> [<a href="Obj.html">Obj</a>]</td>
<td></td></tr>
<tr><td><a href="Nativeint.html#TYPEt">t</a> [<a href="Nativeint.html">Nativeint</a>]</td>
<td><div class="info">
An alias for the type of native integers.
</div>
</td></tr>
<tr><td><a href="Mutex.html#TYPEt">t</a> [<a href="Mutex.html">Mutex</a>]</td>
<td><div class="info">
The type of mutexes.
</div>
</td></tr>
<tr><td><a href="Set.OrderedType.html#TYPEt">t</a> [<a href="Set.OrderedType.html">Set.OrderedType</a>]</td>
<td><div class="info">
The type of the set elements.
</div>
</td></tr>
<tr><td><a href="MoreLabels.Set.S.html#TYPEt">t</a> [<a href="MoreLabels.Set.S.html">MoreLabels.Set.S</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Map.S.html#TYPEt">t</a> [<a href="MoreLabels.Map.S.html">MoreLabels.Map.S</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.SeededS.html#TYPEt">t</a> [<a href="MoreLabels.Hashtbl.SeededS.html">MoreLabels.Hashtbl.SeededS</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.S.html#TYPEt">t</a> [<a href="MoreLabels.Hashtbl.S.html">MoreLabels.Hashtbl.S</a>]</td>
<td></td></tr>
<tr><td><a href="MoreLabels.Hashtbl.html#TYPEt">t</a> [<a href="MoreLabels.Hashtbl.html">MoreLabels.Hashtbl</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.HookSig.html#TYPEt">t</a> [<a href="Misc.HookSig.html">Misc.HookSig</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.LongString.html#TYPEt">t</a> [<a href="Misc.LongString.html">Misc.LongString</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Stdlib.Option.html#TYPEt">t</a> [<a href="Misc.Stdlib.Option.html">Misc.Stdlib.Option</a>]</td>
<td></td></tr>
<tr><td><a href="Misc.Stdlib.List.html#TYPEt">t</a> [<a href="Misc.Stdlib.List.html">Misc.Stdlib.List</a>]</td>
<td></td></tr>
<tr><td><a href="Map.OrderedType.html#TYPEt">t</a> [<a href="Map.OrderedType.html">Map.OrderedType</a>]</td>
<td><div class="info">
The type of the map keys.
</div>
</td></tr>
<tr><td><a href="Longident.html#TYPEt">t</a> [<a href="Longident.html">Longident</a>]</td>
<td></td></tr>
<tr><td><a href="Location.html#TYPEt">t</a> [<a href="Location.html">Location</a>]</td>
<td></td></tr>
<tr><td><a href="Lazy.html#TYPEt">t</a> [<a href="Lazy.html">Lazy</a>]</td>
<td><div class="info">
A value of type <code class="code"><span class="keywordsign">'</span>a&nbsp;<span class="constructor">Lazy</span>.t</code> is a deferred computation, called
   a suspension, that has a result of type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Int64.html#TYPEt">t</a> [<a href="Int64.html">Int64</a>]</td>
<td><div class="info">
An alias for the type of 64-bit integers.
</div>
</td></tr>
<tr><td><a href="Int32.html#TYPEt">t</a> [<a href="Int32.html">Int32</a>]</td>
<td><div class="info">
An alias for the type of 32-bit integers.
</div>
</td></tr>
<tr><td><a href="Identifiable.S.html#TYPEt">t</a> [<a href="Identifiable.S.html">Identifiable.S</a>]</td>
<td></td></tr>
<tr><td><a href="Identifiable.Thing.html#TYPEt">t</a> [<a href="Identifiable.Thing.html">Identifiable.Thing</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.SeededHashedType.html#TYPEt">t</a> [<a href="Hashtbl.SeededHashedType.html">Hashtbl.SeededHashedType</a>]</td>
<td><div class="info">
The type of the hashtable keys.
</div>
</td></tr>
<tr><td><a href="Hashtbl.HashedType.html#TYPEt">t</a> [<a href="Hashtbl.HashedType.html">Hashtbl.HashedType</a>]</td>
<td><div class="info">
The type of the hashtable keys.
</div>
</td></tr>
<tr><td><a href="Hashtbl.SeededS.html#TYPEt">t</a> [<a href="Hashtbl.SeededS.html">Hashtbl.SeededS</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.S.html#TYPEt">t</a> [<a href="Hashtbl.S.html">Hashtbl.S</a>]</td>
<td></td></tr>
<tr><td><a href="Hashtbl.html#TYPEt">t</a> [<a href="Hashtbl.html">Hashtbl</a>]</td>
<td><div class="info">
The type of hash tables from type <code class="code"><span class="keywordsign">'</span>a</code> to type <code class="code"><span class="keywordsign">'</span>b</code>.
</div>
</td></tr>
<tr><td><a href="Ephemeron.Kn.html#TYPEt">t</a> [<a href="Ephemeron.Kn.html">Ephemeron.Kn</a>]</td>
<td><div class="info">
an ephemeron with an arbitrary number of keys
                      of the same type
</div>
</td></tr>
<tr><td><a href="Ephemeron.K2.html#TYPEt">t</a> [<a href="Ephemeron.K2.html">Ephemeron.K2</a>]</td>
<td><div class="info">
an ephemeron with two keys
</div>
</td></tr>
<tr><td><a href="Ephemeron.K1.html#TYPEt">t</a> [<a href="Ephemeron.K1.html">Ephemeron.K1</a>]</td>
<td><div class="info">
an ephemeron with one key
</div>
</td></tr>
<tr><td><a href="Digest.html#TYPEt">t</a> [<a href="Digest.html">Digest</a>]</td>
<td><div class="info">
The type of digests: 16-character strings.
</div>
</td></tr>
<tr><td><a href="Map.S.html#TYPEt">t</a> [<a href="Map.S.html">Map.S</a>]</td>
<td><div class="info">
The type of maps from type <code class="code">key</code> to type <code class="code"><span class="keywordsign">'</span>a</code>.
</div>
</td></tr>
<tr><td><a href="Set.S.html#TYPEt">t</a> [<a href="Set.S.html">Set.S</a>]</td>
<td><div class="info">
The type of sets.
</div>
</td></tr>
<tr><td><a href="Consistbl.html#TYPEt">t</a> [<a href="Consistbl.html">Consistbl</a>]</td>
<td></td></tr>
<tr><td><a href="Condition.html#TYPEt">t</a> [<a href="Condition.html">Condition</a>]</td>
<td><div class="info">
The type of condition variables.
</div>
</td></tr>
<tr><td><a href="Complex.html#TYPEt">t</a> [<a href="Complex.html">Complex</a>]</td>
<td><div class="info">
The type of complex numbers.
</div>
</td></tr>
<tr><td><a href="Char.html#TYPEt">t</a> [<a href="Char.html">Char</a>]</td>
<td><div class="info">
An alias for the type of characters.
</div>
</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEt">t</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="BytesLabels.html#TYPEt">t</a> [<a href="BytesLabels.html">BytesLabels</a>]</td>
<td><div class="info">
An alias for the type of byte sequences.
</div>
</td></tr>
<tr><td><a href="Bytes.html#TYPEt">t</a> [<a href="Bytes.html">Bytes</a>]</td>
<td><div class="info">
An alias for the type of byte sequences.
</div>
</td></tr>
<tr><td><a href="Buffer.html#TYPEt">t</a> [<a href="Buffer.html">Buffer</a>]</td>
<td><div class="info">
The abstract type of buffers.
</div>
</td></tr>
<tr><td><a href="Bigarray.Array3.html#TYPEt">t</a> [<a href="Bigarray.Array3.html">Bigarray.Array3</a>]</td>
<td><div class="info">
The type of three-dimensional big arrays whose elements have
     OCaml type <code class="code"><span class="keywordsign">'</span>a</code>, representation kind <code class="code"><span class="keywordsign">'</span>b</code>, and memory layout <code class="code"><span class="keywordsign">'</span>c</code>.
</div>
</td></tr>
<tr><td><a href="Bigarray.Array2.html#TYPEt">t</a> [<a href="Bigarray.Array2.html">Bigarray.Array2</a>]</td>
<td><div class="info">
The type of two-dimensional big arrays whose elements have
     OCaml type <code class="code"><span class="keywordsign">'</span>a</code>, representation kind <code class="code"><span class="keywordsign">'</span>b</code>, and memory layout <code class="code"><span class="keywordsign">'</span>c</code>.
</div>
</td></tr>
<tr><td><a href="Bigarray.Array1.html#TYPEt">t</a> [<a href="Bigarray.Array1.html">Bigarray.Array1</a>]</td>
<td><div class="info">
The type of one-dimensional big arrays whose elements have
     OCaml type <code class="code"><span class="keywordsign">'</span>a</code>, representation kind <code class="code"><span class="keywordsign">'</span>b</code>, and memory layout <code class="code"><span class="keywordsign">'</span>c</code>.
</div>
</td></tr>
<tr><td><a href="Bigarray.Genarray.html#TYPEt">t</a> [<a href="Bigarray.Genarray.html">Bigarray.Genarray</a>]</td>
<td><div class="info">
The type <code class="code"><span class="constructor">Genarray</span>.t</code> is the type of big arrays with variable
     numbers of dimensions.
</div>
</td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEtable">table</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEtables">tables</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="Format.html#TYPEtag">tag</a> [<a href="Format.html">Format</a>]</td>
<td></td></tr>
<tr><td><a href="CamlinternalOO.html#TYPEtag">tag</a> [<a href="CamlinternalOO.html">CamlinternalOO</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEterminal_io">terminal_io</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td></td></tr>
<tr><td><a href="Unix.html#TYPEterminal_io">terminal_io</a> [<a href="Unix.html">Unix</a>]</td>
<td></td></tr>
<tr><td><a href="Docstrings.html#TYPEtext">text</a> [<a href="Docstrings.html">Docstrings</a>]</td>
<td></td></tr>
<tr><td><a href="UnixLabels.html#TYPEtm">tm</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
The type representing wallclock time and calendar date.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEtm">tm</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
The type representing wallclock time and calendar date.
</div>
</td></tr>
<tr><td><a href="Parser.html#TYPEtoken">token</a> [<a href="Parser.html">Parser</a>]</td>
<td></td></tr>
<tr><td><a href="Genlex.html#TYPEtoken">token</a> [<a href="Genlex.html">Genlex</a>]</td>
<td><div class="info">
The type of tokens.
</div>
</td></tr>
<tr><td><a href="Parsetree.html#TYPEtoplevel_phrase">toplevel_phrase</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEtype_declaration">type_declaration</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEtype_extension">type_extension</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEtype_kind">type_kind</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td align="left"><br>U</td></tr>
<tr><td><a href="Arg.html#TYPEusage_msg">usage_msg</a> [<a href="Arg.html">Arg</a>]</td>
<td></td></tr>
<tr><td align="left"><br>V</td></tr>
<tr><td><a href="Parsetree.html#TYPEvalue_binding">value_binding</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEvalue_description">value_description</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEvariance">variance</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td><a href="Asttypes.html#TYPEvirtual_flag">virtual_flag</a> [<a href="Asttypes.html">Asttypes</a>]</td>
<td></td></tr>
<tr><td align="left"><br>W</td></tr>
<tr><td><a href="UnixLabels.html#TYPEwait_flag">wait_flag</a> [<a href="UnixLabels.html">UnixLabels</a>]</td>
<td><div class="info">
Flags for <a href="UnixLabels.html#VALwaitpid"><code class="code"><span class="constructor">UnixLabels</span>.waitpid</code></a>.
</div>
</td></tr>
<tr><td><a href="Unix.html#TYPEwait_flag">wait_flag</a> [<a href="Unix.html">Unix</a>]</td>
<td><div class="info">
Flags for <a href="Unix.html#VALwaitpid"><code class="code"><span class="constructor">Unix</span>.waitpid</code></a>.
</div>
</td></tr>
<tr><td><a href="GraphicsX11.html#TYPEwindow_id">window_id</a> [<a href="GraphicsX11.html">GraphicsX11</a>]</td>
<td></td></tr>
<tr><td><a href="Parsetree.html#TYPEwith_constraint">with_constraint</a> [<a href="Parsetree.html">Parsetree</a>]</td>
<td></td></tr>
</tbody></table>

<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>