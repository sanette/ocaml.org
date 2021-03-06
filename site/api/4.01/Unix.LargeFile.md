<!-- ((! set title API !)) ((! set documentation !)) ((! set api !)) ((! set nobreadcrumb !)) -->
<div class="api"><header><nav class="toc brand"><a class="brand" href="https://ocaml.org/"><img src="colour-logo-gray.svg" class="svg" alt="OCaml"></a></nav><nav class="toc"><div class="toc_version"><a href="/docs" id="version-select">API Version 4.01</a></div><a href="index.html">&lt; General Index</a><div class="api_search"><input type="text" name="apisearch" id="api_search" oninput="mySearch(false);" onkeypress="this.oninput();" onclick="this.oninput();" onpaste="this.oninput();">
<img src="search_icon.svg" alt="Search" class="svg" onclick="mySearch(false)"></div>
<div id="search_results"></div><div class="toc_title"><a href="#top">Unix.LargeFile</a></div><ul></ul></nav></header>

<h1>Module <a href="type_Unix.LargeFile.html">Unix.LargeFile</a></h1>

<pre><span class="keyword">module</span> LargeFile: <code class="code"><span class="keyword">sig</span></code> <a href="Unix.LargeFile.html">..</a> <code class="code"><span class="keyword">end</span></code></pre><div class="info module top">
File operations on large files.
  This sub-module provides 64-bit variants of the functions
  <a href="Unix.html#VALlseek"><code class="code"><span class="constructor">Unix</span>.lseek</code></a> (for positioning a file descriptor),
  <a href="Unix.html#VALtruncate"><code class="code"><span class="constructor">Unix</span>.truncate</code></a> and <a href="Unix.html#VALftruncate"><code class="code"><span class="constructor">Unix</span>.ftruncate</code></a> (for changing the size of a file),
  and <a href="Unix.html#VALstat"><code class="code"><span class="constructor">Unix</span>.stat</code></a>, <a href="Unix.html#VALlstat"><code class="code"><span class="constructor">Unix</span>.lstat</code></a> and <a href="Unix.html#VALfstat"><code class="code"><span class="constructor">Unix</span>.fstat</code></a> (for obtaining
  information on files).  These alternate functions represent
  positions and sizes by 64-bit integers (type <code class="code">int64</code>) instead of
  regular integers (type <code class="code">int</code>), thus allowing operating on files
  whose sizes are greater than <code class="code">max_int</code>.<br>
</div>
<hr width="100%">

<pre><span id="VALlseek"><span class="keyword">val</span> lseek</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; int64 -&gt; <a href="Unix.html#TYPEseek_command">Unix.seek_command</a> -&gt; int64</code></pre>
<pre><span id="VALtruncate"><span class="keyword">val</span> truncate</span> : <code class="type">string -&gt; int64 -&gt; unit</code></pre>
<pre><span id="VALftruncate"><span class="keyword">val</span> ftruncate</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; int64 -&gt; unit</code></pre>
<pre><code><span id="TYPEstats"><span class="keyword">type</span> <code class="type"></code>stats</span> = {</code></pre><table class="typetable">
<tbody><tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_dev">st_dev</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Device number</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_ino">st_ino</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Inode number</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_kind">st_kind</span>&nbsp;: <code class="type"><a href="Unix.html#TYPEfile_kind">Unix.file_kind</a></code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Kind of the file</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_perm">st_perm</span>&nbsp;: <code class="type"><a href="Unix.html#TYPEfile_perm">Unix.file_perm</a></code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Access rights</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_nlink">st_nlink</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Number of links</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_uid">st_uid</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">User id of the owner</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_gid">st_gid</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Group ID of the file's group</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_rdev">st_rdev</span>&nbsp;: <code class="type">int</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Device minor number</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_size">st_size</span>&nbsp;: <code class="type">int64</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Size in bytes</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_atime">st_atime</span>&nbsp;: <code class="type">float</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Last access time</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_mtime">st_mtime</span>&nbsp;: <code class="type">float</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Last modification time</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr>
<tr>
<td align="left" valign="top">
<code>&nbsp;&nbsp;</code></td>
<td align="left" valign="top">
<code><span id="TYPEELTstats.st_ctime">st_ctime</span>&nbsp;: <code class="type">float</code>;</code></td>
<td class="typefieldcomment" align="left" valign="top"><code>(*</code></td><td class="typefieldcomment" align="left" valign="top">Last status change time</td><td class="typefieldcomment" align="left" valign="bottom"><code>*)</code></td>
</tr></tbody></table>
}



<pre><span id="VALstat"><span class="keyword">val</span> stat</span> : <code class="type">string -&gt; <a href="Unix.LargeFile.html#TYPEstats">stats</a></code></pre>
<pre><span id="VALlstat"><span class="keyword">val</span> lstat</span> : <code class="type">string -&gt; <a href="Unix.LargeFile.html#TYPEstats">stats</a></code></pre>
<pre><span id="VALfstat"><span class="keyword">val</span> fstat</span> : <code class="type"><a href="Unix.html#TYPEfile_descr">Unix.file_descr</a> -&gt; <a href="Unix.LargeFile.html#TYPEstats">stats</a></code></pre><div class="copyright">The present documentation is copyright Institut National de Recherche en Informatique et en Automatique (INRIA). A complete version can be obtained from <a href="http://caml.inria.fr/pub/docs/manual-ocaml/">this page</a>.</div></div>