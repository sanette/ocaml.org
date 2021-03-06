<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.03</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Bytes</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Bytes.html">Bytes</a></h1>

<pre><span class="keyword">module</span> Bytes: <code class="code"><span class="keyword">sig</span></code> <a href="Bytes.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
Byte sequence operations.
<p>

   A byte sequence is a mutable data structure that contains a
   fixed-length sequence of bytes. Each byte can be indexed in
   constant time for reading or writing.
</p><p>

   Given a byte sequence <code class="code">s</code> of length <code class="code">l</code>, we can access each of the
   <code class="code">l</code> bytes of <code class="code">s</code> via its index in the sequence. Indexes start at
   <code class="code">0</code>, and we will call an index valid in <code class="code">s</code> if it falls within the
   range <code class="code">[0...l-1]</code> (inclusive). A position is the point between two
   bytes or at the beginning or end of the sequence.  We call a
   position valid in <code class="code">s</code> if it falls within the range <code class="code">[0...l]</code>
   (inclusive). Note that the byte at index <code class="code">n</code> is between positions
   <code class="code">n</code> and <code class="code">n+1</code>.
</p><p>

   Two parameters <code class="code">start</code> and <code class="code">len</code> are said to designate a valid
   range of <code class="code">s</code> if <code class="code">len &gt;= 0</code> and <code class="code">start</code> and <code class="code">start+len</code> are valid
   positions in <code class="code">s</code>.
</p><p>

   Byte sequences can be modified in place, for instance via the <code class="code">set</code>
   and <code class="code">blit</code> functions described below.  See also strings (module
   <a href="String.html"><code class="code"><span class="constructor">String</span></code></a>), which are almost the same data structure, but cannot be
   modified in place.
</p><p>

   Bytes are represented by the OCaml type <code class="code">char</code>.<br>
<b>Since</b> 4.02.0<br>
</p></div>
<hr width="100%">

<pre><span id="VALlength"><span class="keyword">val</span> length</span> : <code class="type">bytes -&gt; int</code></pre><div class="info ">
Return the length (number of bytes) of the argument.<br>
</div>

<pre><span id="VALget"><span class="keyword">val</span> get</span> : <code class="type">bytes -&gt; int -&gt; char</code></pre><div class="info ">
<code class="code">get s n</code> returns the byte at index <code class="code">n</code> in argument <code class="code">s</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">n</code> not a valid index in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALset"><span class="keyword">val</span> set</span> : <code class="type">bytes -&gt; int -&gt; char -&gt; unit</code></pre><div class="info ">
<code class="code">set s n c</code> modifies <code class="code">s</code> in place, replacing the byte at index <code class="code">n</code>
    with <code class="code">c</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">n</code> is not a valid index in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALcreate"><span class="keyword">val</span> create</span> : <code class="type">int -&gt; bytes</code></pre><div class="info ">
<code class="code">create n</code> returns a new byte sequence of length <code class="code">n</code>. The
    sequence is uninitialized and contains arbitrary bytes.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">n &lt; 0</code> or <code class="code">n &gt; </code><a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a>.<br>
</p></div>

<pre><span id="VALmake"><span class="keyword">val</span> make</span> : <code class="type">int -&gt; char -&gt; bytes</code></pre><div class="info ">
<code class="code">make n c</code> returns a new byte sequence of length <code class="code">n</code>, filled with
    the byte <code class="code">c</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">n &lt; 0</code> or <code class="code">n &gt; </code><a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a>.<br>
</p></div>

<pre><span id="VALinit"><span class="keyword">val</span> init</span> : <code class="type">int -&gt; (int -&gt; char) -&gt; bytes</code></pre><div class="info ">
<code class="code"><span class="constructor">Bytes</span>.init n f</code> returns a fresh byte sequence of length <code class="code">n</code>, with
    character <code class="code">i</code> initialized to the result of <code class="code">f i</code> (in increasing
    index order).
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">n &lt; 0</code> or <code class="code">n &gt; </code><a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a>.<br>
</p></div>

<pre><span id="VALempty"><span class="keyword">val</span> empty</span> : <code class="type">bytes</code></pre><div class="info ">
A byte sequence of size 0.<br>
</div>

<pre><span id="VALcopy"><span class="keyword">val</span> copy</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a new byte sequence that contains the same bytes as the
    argument.<br>
</div>

<pre><span id="VALof_string"><span class="keyword">val</span> of_string</span> : <code class="type">string -&gt; bytes</code></pre><div class="info ">
Return a new byte sequence that contains the same bytes as the
    given string.<br>
</div>

<pre><span id="VALto_string"><span class="keyword">val</span> to_string</span> : <code class="type">bytes -&gt; string</code></pre><div class="info ">
Return a new string that contains the same bytes as the given byte
    sequence.<br>
</div>

<pre><span id="VALsub"><span class="keyword">val</span> sub</span> : <code class="type">bytes -&gt; int -&gt; int -&gt; bytes</code></pre><div class="info ">
<code class="code">sub s start len</code> returns a new byte sequence of length <code class="code">len</code>,
    containing the subsequence of <code class="code">s</code> that starts at position <code class="code">start</code>
    and has length <code class="code">len</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">start</code> and <code class="code">len</code> do not designate a
    valid range of <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALsub_string"><span class="keyword">val</span> sub_string</span> : <code class="type">bytes -&gt; int -&gt; int -&gt; string</code></pre><div class="info ">
Same as <code class="code">sub</code> but return a string instead of a byte sequence.<br>
</div>

<pre><span id="VALextend"><span class="keyword">val</span> extend</span> : <code class="type">bytes -&gt; int -&gt; int -&gt; bytes</code></pre><div class="info ">
<code class="code">extend s left right</code> returns a new byte sequence that contains
    the bytes of <code class="code">s</code>, with <code class="code">left</code> uninitialized bytes prepended and
    <code class="code">right</code> uninitialized bytes appended to it. If <code class="code">left</code> or <code class="code">right</code>
    is negative, then bytes are removed (instead of appended) from
    the corresponding side of <code class="code">s</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if the result length is negative or
    longer than <a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a> bytes.<br>
</p></div>

<pre><span id="VALfill"><span class="keyword">val</span> fill</span> : <code class="type">bytes -&gt; int -&gt; int -&gt; char -&gt; unit</code></pre><div class="info ">
<code class="code">fill s start len c</code> modifies <code class="code">s</code> in place, replacing <code class="code">len</code>
    characters with <code class="code">c</code>, starting at <code class="code">start</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">start</code> and <code class="code">len</code> do not designate a
    valid range of <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALblit"><span class="keyword">val</span> blit</span> : <code class="type">bytes -&gt; int -&gt; bytes -&gt; int -&gt; int -&gt; unit</code></pre><div class="info ">
<code class="code">blit src srcoff dst dstoff len</code> copies <code class="code">len</code> bytes from sequence
    <code class="code">src</code>, starting at index <code class="code">srcoff</code>, to sequence <code class="code">dst</code>, starting at
    index <code class="code">dstoff</code>. It works correctly even if <code class="code">src</code> and <code class="code">dst</code> are the
    same byte sequence, and the source and destination intervals
    overlap.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">srcoff</code> and <code class="code">len</code> do not
    designate a valid range of <code class="code">src</code>, or if <code class="code">dstoff</code> and <code class="code">len</code>
    do not designate a valid range of <code class="code">dst</code>.<br>
</p></div>

<pre><span id="VALblit_string"><span class="keyword">val</span> blit_string</span> : <code class="type">string -&gt; int -&gt; bytes -&gt; int -&gt; int -&gt; unit</code></pre><div class="info ">
<code class="code">blit src srcoff dst dstoff len</code> copies <code class="code">len</code> bytes from string
    <code class="code">src</code>, starting at index <code class="code">srcoff</code>, to byte sequence <code class="code">dst</code>,
    starting at index <code class="code">dstoff</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">srcoff</code> and <code class="code">len</code> do not
    designate a valid range of <code class="code">src</code>, or if <code class="code">dstoff</code> and <code class="code">len</code>
    do not designate a valid range of <code class="code">dst</code>.<br>
</p></div>

<pre><span id="VALconcat"><span class="keyword">val</span> concat</span> : <code class="type">bytes -&gt; bytes list -&gt; bytes</code></pre><div class="info ">
<code class="code">concat sep sl</code> concatenates the list of byte sequences <code class="code">sl</code>,
    inserting the separator byte sequence <code class="code">sep</code> between each, and
    returns the result as a new byte sequence.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if the result is longer than
    <a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a> bytes.<br>
</p></div>

<pre><span id="VALcat"><span class="keyword">val</span> cat</span> : <code class="type">bytes -&gt; bytes -&gt; bytes</code></pre><div class="info ">
<code class="code">cat s1 s2</code> concatenates <code class="code">s1</code> and <code class="code">s2</code> and returns the result
     as new byte sequence.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if the result is longer than
    <a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a> bytes.<br>
</p></div>

<pre><span id="VALiter"><span class="keyword">val</span> iter</span> : <code class="type">(char -&gt; unit) -&gt; bytes -&gt; unit</code></pre><div class="info ">
<code class="code">iter f s</code> applies function <code class="code">f</code> in turn to all the bytes of <code class="code">s</code>.
    It is equivalent to <code class="code">f (get s 0); f (get s 1); ...; f (get s
    (length s - 1)); ()</code>.<br>
</div>

<pre><span id="VALiteri"><span class="keyword">val</span> iteri</span> : <code class="type">(int -&gt; char -&gt; unit) -&gt; bytes -&gt; unit</code></pre><div class="info ">
Same as <a href="Bytes.html#VALiter"><code class="code"><span class="constructor">Bytes</span>.iter</code></a>, but the function is applied to the index of
    the byte as first argument and the byte itself as second
    argument.<br>
</div>

<pre><span id="VALmap"><span class="keyword">val</span> map</span> : <code class="type">(char -&gt; char) -&gt; bytes -&gt; bytes</code></pre><div class="info ">
<code class="code">map f s</code> applies function <code class="code">f</code> in turn to all the bytes of <code class="code">s</code>
    (in increasing index order) and stores the resulting bytes in
    a new sequence that is returned as the result.<br>
</div>

<pre><span id="VALmapi"><span class="keyword">val</span> mapi</span> : <code class="type">(int -&gt; char -&gt; char) -&gt; bytes -&gt; bytes</code></pre><div class="info ">
<code class="code">mapi f s</code> calls <code class="code">f</code> with each character of <code class="code">s</code> and its
    index (in increasing index order) and stores the resulting bytes
    in a new sequence that is returned as the result.<br>
</div>

<pre><span id="VALtrim"><span class="keyword">val</span> trim</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, without leading and trailing
    whitespace. The bytes regarded as whitespace are the ASCII
    characters <code class="code"><span class="string">' '</span></code>, <code class="code"><span class="string">'\012'</span></code>, <code class="code"><span class="string">'\n'</span></code>, <code class="code"><span class="string">'\r'</span></code>, and <code class="code"><span class="string">'\t'</span></code>.<br>
</div>

<pre><span id="VALescaped"><span class="keyword">val</span> escaped</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, with special characters represented
    by escape sequences, following the lexical conventions of OCaml.
    All characters outside the ASCII printable range (32..126) are
    escaped, as well as backslash and double-quote.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if the result is longer than
    <a href="Sys.html#VALmax_string_length"><code class="code"><span class="constructor">Sys</span>.max_string_length</code></a> bytes.<br>
</p></div>

<pre><span id="VALindex"><span class="keyword">val</span> index</span> : <code class="type">bytes -&gt; char -&gt; int</code></pre><div class="info ">
<code class="code">index s c</code> returns the index of the first occurrence of byte <code class="code">c</code>
    in <code class="code">s</code>.
<p>

    Raise <code class="code"><span class="constructor">Not_found</span></code> if <code class="code">c</code> does not occur in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALrindex"><span class="keyword">val</span> rindex</span> : <code class="type">bytes -&gt; char -&gt; int</code></pre><div class="info ">
<code class="code">rindex s c</code> returns the index of the last occurrence of byte <code class="code">c</code>
    in <code class="code">s</code>.
<p>

    Raise <code class="code"><span class="constructor">Not_found</span></code> if <code class="code">c</code> does not occur in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALindex_from"><span class="keyword">val</span> index_from</span> : <code class="type">bytes -&gt; int -&gt; char -&gt; int</code></pre><div class="info ">
<code class="code">index_from s i c</code> returns the index of the first occurrence of
    byte <code class="code">c</code> in <code class="code">s</code> after position <code class="code">i</code>.  <code class="code"><span class="constructor">Bytes</span>.index s c</code> is
    equivalent to <code class="code"><span class="constructor">Bytes</span>.index_from s 0 c</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">i</code> is not a valid position in <code class="code">s</code>.
    Raise <code class="code"><span class="constructor">Not_found</span></code> if <code class="code">c</code> does not occur in <code class="code">s</code> after position <code class="code">i</code>.<br>
</p></div>

<pre><span id="VALrindex_from"><span class="keyword">val</span> rindex_from</span> : <code class="type">bytes -&gt; int -&gt; char -&gt; int</code></pre><div class="info ">
<code class="code">rindex_from s i c</code> returns the index of the last occurrence of
    byte <code class="code">c</code> in <code class="code">s</code> before position <code class="code">i+1</code>.  <code class="code">rindex s c</code> is equivalent
    to <code class="code">rindex_from s (<span class="constructor">Bytes</span>.length s - 1) c</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">i+1</code> is not a valid position in <code class="code">s</code>.
    Raise <code class="code"><span class="constructor">Not_found</span></code> if <code class="code">c</code> does not occur in <code class="code">s</code> before position <code class="code">i+1</code>.<br>
</p></div>

<pre><span id="VALcontains"><span class="keyword">val</span> contains</span> : <code class="type">bytes -&gt; char -&gt; bool</code></pre><div class="info ">
<code class="code">contains s c</code> tests if byte <code class="code">c</code> appears in <code class="code">s</code>.<br>
</div>

<pre><span id="VALcontains_from"><span class="keyword">val</span> contains_from</span> : <code class="type">bytes -&gt; int -&gt; char -&gt; bool</code></pre><div class="info ">
<code class="code">contains_from s start c</code> tests if byte <code class="code">c</code> appears in <code class="code">s</code> after
    position <code class="code">start</code>.  <code class="code">contains s c</code> is equivalent to <code class="code">contains_from
    s 0 c</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">start</code> is not a valid position in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALrcontains_from"><span class="keyword">val</span> rcontains_from</span> : <code class="type">bytes -&gt; int -&gt; char -&gt; bool</code></pre><div class="info ">
<code class="code">rcontains_from s stop c</code> tests if byte <code class="code">c</code> appears in <code class="code">s</code> before
    position <code class="code">stop+1</code>.
<p>

    Raise <code class="code"><span class="constructor">Invalid_argument</span></code> if <code class="code">stop &lt; 0</code> or <code class="code">stop+1</code> is not a valid
    position in <code class="code">s</code>.<br>
</p></div>

<pre><span id="VALuppercase"><span class="keyword">val</span> uppercase</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
<span class="warning">Deprecated.</span>Functions operating on Latin-1 character set are deprecated.<br>
Return a copy of the argument, with all lowercase letters
   translated to uppercase, including accented letters of the ISO
   Latin-1 (8859-1) character set.<br>
</div>

<pre><span id="VALlowercase"><span class="keyword">val</span> lowercase</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
<span class="warning">Deprecated.</span>Functions operating on Latin-1 character set are deprecated.<br>
Return a copy of the argument, with all uppercase letters
   translated to lowercase, including accented letters of the ISO
   Latin-1 (8859-1) character set.<br>
</div>

<pre><span id="VALcapitalize"><span class="keyword">val</span> capitalize</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
<span class="warning">Deprecated.</span>Functions operating on Latin-1 character set are deprecated.<br>
Return a copy of the argument, with the first character set to uppercase,
   using the ISO Latin-1 (8859-1) character set..<br>
</div>

<pre><span id="VALuncapitalize"><span class="keyword">val</span> uncapitalize</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
<span class="warning">Deprecated.</span>Functions operating on Latin-1 character set are deprecated.<br>
Return a copy of the argument, with the first character set to lowercase,
   using the ISO Latin-1 (8859-1) character set..<br>
</div>

<pre><span id="VALuppercase_ascii"><span class="keyword">val</span> uppercase_ascii</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, with all lowercase letters
   translated to uppercase, using the US-ASCII character set.<br>
<b>Since</b> 4.03.0<br>
</div>

<pre><span id="VALlowercase_ascii"><span class="keyword">val</span> lowercase_ascii</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, with all uppercase letters
   translated to lowercase, using the US-ASCII character set.<br>
<b>Since</b> 4.03.0<br>
</div>

<pre><span id="VALcapitalize_ascii"><span class="keyword">val</span> capitalize_ascii</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, with the first character set to uppercase,
   using the US-ASCII character set.<br>
<b>Since</b> 4.03.0<br>
</div>

<pre><span id="VALuncapitalize_ascii"><span class="keyword">val</span> uncapitalize_ascii</span> : <code class="type">bytes -&gt; bytes</code></pre><div class="info ">
Return a copy of the argument, with the first character set to lowercase,
   using the US-ASCII character set.<br>
<b>Since</b> 4.03.0<br>
</div>

<pre><span id="TYPEt"><span class="keyword">type</span> <code class="type"></code>t</span> = <code class="type">bytes</code> </pre>
<div class="info ">
An alias for the type of byte sequences.<br>
</div>


<pre><span id="VALcompare"><span class="keyword">val</span> compare</span> : <code class="type"><a href="Bytes.html#TYPEt">t</a> -&gt; <a href="Bytes.html#TYPEt">t</a> -&gt; int</code></pre><div class="info ">
The comparison function for byte sequences, with the same
    specification as <a href="Pervasives.html#VALcompare"><code class="code">compare</code></a>.  Along with the type <code class="code">t</code>,
    this function <code class="code">compare</code> allows the module <code class="code"><span class="constructor">Bytes</span></code> to be passed as
    argument to the functors <a href="Set.Make.html"><code class="code"><span class="constructor">Set</span>.<span class="constructor">Make</span></code></a> and <a href="Map.Make.html"><code class="code"><span class="constructor">Map</span>.<span class="constructor">Make</span></code></a>.<br>
</div>

<pre><span id="VALequal"><span class="keyword">val</span> equal</span> : <code class="type"><a href="Bytes.html#TYPEt">t</a> -&gt; <a href="Bytes.html#TYPEt">t</a> -&gt; bool</code></pre><div class="info ">
The equality function for byte sequences.<br>
<b>Since</b> 4.03.0<br>
</div>
<br>
<h4 id="4_Unsafeconversionsforadvancedusers">Unsafe conversions (for advanced users)</h4>
<p>

    This section describes unsafe, low-level conversion functions
    between <code class="code">bytes</code> and <code class="code">string</code>. They do not copy the internal data;
    used improperly, they can break the immutability invariant on
    strings provided by the <code class="code">-safe-string</code> option. They are available for
    expert library authors, but for most purposes you should use the
    always-correct <a href="Bytes.html#VALto_string"><code class="code"><span class="constructor">Bytes</span>.to_string</code></a> and <a href="Bytes.html#VALof_string"><code class="code"><span class="constructor">Bytes</span>.of_string</code></a> instead.<br>

</p><pre><span id="VALunsafe_to_string"><span class="keyword">val</span> unsafe_to_string</span> : <code class="type">bytes -&gt; string</code></pre><div class="info ">
Unsafely convert a byte sequence into a string.
<p>

    To reason about the use of <code class="code">unsafe_to_string</code>, it is convenient to
    consider an "ownership" discipline. A piece of code that
    manipulates some data "owns" it; there are several disjoint ownership
    modes, including:</p><ul>
<li>Unique ownership: the data may be accessed and mutated</li>
<li>Shared ownership: the data has several owners, that may only
      access it, not mutate it.</li>
</ul>

    Unique ownership is linear: passing the data to another piece of
    code means giving up ownership (we cannot write the
    data again). A unique owner may decide to make the data shared
    (giving up mutation rights on it), but shared data may not become
    uniquely-owned again.
<p>

   <code class="code">unsafe_to_string s</code> can only be used when the caller owns the byte
   sequence <code class="code">s</code> -- either uniquely or as shared immutable data. The
   caller gives up ownership of <code class="code">s</code>, and gains ownership of the
   returned string.
</p><p>

   There are two valid use-cases that respect this ownership
   discipline:
</p><p>

   1. Creating a string by initializing and mutating a byte sequence
   that is never changed after initialization is performed.
</p><p>

   </p><pre class="codepre"><code class="code"><span class="keyword">let</span>&nbsp;string_init&nbsp;len&nbsp;f&nbsp;:&nbsp;string&nbsp;=
&nbsp;&nbsp;<span class="keyword">let</span>&nbsp;s&nbsp;=&nbsp;<span class="constructor">Bytes</span>.create&nbsp;len&nbsp;<span class="keyword">in</span>
&nbsp;&nbsp;<span class="keyword">for</span>&nbsp;i&nbsp;=&nbsp;0&nbsp;<span class="keyword">to</span>&nbsp;len&nbsp;-&nbsp;1&nbsp;<span class="keyword">do</span>&nbsp;<span class="constructor">Bytes</span>.set&nbsp;s&nbsp;i&nbsp;(f&nbsp;i)&nbsp;<span class="keyword">done</span>;
&nbsp;&nbsp;<span class="constructor">Bytes</span>.unsafe_to_string&nbsp;s
&nbsp;&nbsp;&nbsp;</code></pre>
<p>

   This function is safe because the byte sequence <code class="code">s</code> will never be
   accessed or mutated after <code class="code">unsafe_to_string</code> is called. The
   <code class="code">string_init</code> code gives up ownership of <code class="code">s</code>, and returns the
   ownership of the resulting string to its caller.
</p><p>

   Note that it would be unsafe if <code class="code">s</code> was passed as an additional
   parameter to the function <code class="code">f</code> as it could escape this way and be
   mutated in the future -- <code class="code">string_init</code> would give up ownership of
   <code class="code">s</code> to pass it to <code class="code">f</code>, and could not call <code class="code">unsafe_to_string</code>
   safely.
</p><p>

   We have provided the <a href="String.html#VALinit"><code class="code"><span class="constructor">String</span>.init</code></a>, <a href="String.html#VALmap"><code class="code"><span class="constructor">String</span>.map</code></a> and
   <a href="String.html#VALmapi"><code class="code"><span class="constructor">String</span>.mapi</code></a> functions to cover most cases of building
   new strings. You should prefer those over <code class="code">to_string</code> or
   <code class="code">unsafe_to_string</code> whenever applicable.
</p><p>

   2. Temporarily giving ownership of a byte sequence to a function
   that expects a uniquely owned string and returns ownership back, so
   that we can mutate the sequence again after the call ended.
</p><p>

   </p><pre class="codepre"><code class="code"><span class="keyword">let</span>&nbsp;bytes_length&nbsp;(s&nbsp;:&nbsp;bytes)&nbsp;=
&nbsp;&nbsp;<span class="constructor">String</span>.length&nbsp;(<span class="constructor">Bytes</span>.unsafe_to_string&nbsp;s)
&nbsp;&nbsp;&nbsp;</code></pre>
<p>

   In this use-case, we do not promise that <code class="code">s</code> will never be mutated
   after the call to <code class="code">bytes_length s</code>. The <a href="String.html#VALlength"><code class="code"><span class="constructor">String</span>.length</code></a> function
   temporarily borrows unique ownership of the byte sequence
   (and sees it as a <code class="code">string</code>), but returns this ownership back to
   the caller, which may assume that <code class="code">s</code> is still a valid byte
   sequence after the call. Note that this is only correct because we
   know that <a href="String.html#VALlength"><code class="code"><span class="constructor">String</span>.length</code></a> does not capture its argument -- it could
   escape by a side-channel such as a memoization combinator.
</p><p>

   The caller may not mutate <code class="code">s</code> while the string is borrowed (it has
   temporarily given up ownership). This affects concurrent programs,
   but also higher-order functions: if <code class="code"><span class="constructor">String</span>.length</code> returned
   a closure to be called later, <code class="code">s</code> should not be mutated until this
   closure is fully applied and returns ownership.<br>
</p></div>

<pre><span id="VALunsafe_of_string"><span class="keyword">val</span> unsafe_of_string</span> : <code class="type">string -&gt; bytes</code></pre><div class="info ">
Unsafely convert a shared string to a byte sequence that should
    not be mutated.
<p>

    The same ownership discipline that makes <code class="code">unsafe_to_string</code>
    correct applies to <code class="code">unsafe_of_string</code>: you may use it if you were
    the owner of the <code class="code">string</code> value, and you will own the return
    <code class="code">bytes</code> in the same mode.
</p><p>

    In practice, unique ownership of string values is extremely
    difficult to reason about correctly. You should always assume
    strings are shared, never uniquely owned.
</p><p>

    For example, string literals are implicitly shared by the
    compiler, so you never uniquely own them.
</p><p>

    </p><pre class="codepre"><code class="code"><span class="keyword">let</span>&nbsp;incorrect&nbsp;=&nbsp;<span class="constructor">Bytes</span>.unsafe_of_string&nbsp;<span class="string">"hello"</span>
<span class="keyword">let</span>&nbsp;s&nbsp;=&nbsp;<span class="constructor">Bytes</span>.of_string&nbsp;<span class="string">"hello"</span>
&nbsp;&nbsp;&nbsp;&nbsp;</code></pre>
<p>

    The first declaration is incorrect, because the string literal
    <code class="code"><span class="string">"hello"</span></code> could be shared by the compiler with other parts of the
    program, and mutating <code class="code">incorrect</code> is a bug. You must always use
    the second version, which performs a copy and is thus correct.
</p><p>

    Assuming unique ownership of strings that are not string
    literals, but are (partly) built from string literals, is also
    incorrect. For example, mutating <code class="code">unsafe_of_string (<span class="string">"foo"</span> ^ s)</code>
    could mutate the shared string <code class="code"><span class="string">"foo"</span></code> -- assuming a rope-like
    representation of strings. More generally, functions operating on
    strings will assume shared ownership, they do not preserve unique
    ownership. It is thus incorrect to assume unique ownership of the
    result of <code class="code">unsafe_of_string</code>.
</p><p>

    The only case we have reasonable confidence is safe is if the
    produced <code class="code">bytes</code> is shared -- used as an immutable byte
    sequence. This is possibly useful for incremental migration of
    low-level programs that manipulate immutable sequences of bytes
    (for example <a href="Marshal.html#VALfrom_bytes"><code class="code"><span class="constructor">Marshal</span>.from_bytes</code></a>) and previously used the
    <code class="code">string</code> type for this purpose.<br>
</p></div>
<div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>