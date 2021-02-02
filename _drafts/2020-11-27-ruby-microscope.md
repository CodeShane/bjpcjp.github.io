---
title: Ruby Under the Microscope - book notes
tags: ruby
date: 2020-11-27
layout: post
---

<a href="https://nostarch.com/rum">
	<img src="/px/ruby/ruby-microscope-book-cover.png" width="98%">
</a>

<div style="columns: 2;">

<div class="textcard">
<strong>Intro</strong>
<details>
	<summary>Who the Book is For</summary></details>
<details>
	<summary>Using Ruby to Test Itself</summary></details>
<details>
	<summary>Which Implementation?</summary></details>
<details>
	<summary>Overview</summary></details>
</div>

<div class="textcard">
<strong>1) Tokenization & Parsing</strong>
<details>
	<summary>How Ruby converts source code to tokens</summary>
</details>

<details>
	<summary>Ripper & script tokenization</summary>
	*test</summary>
</details>

<details>
	<summary>Parsing</summary>
	- Ruby uses Bison (a version of Yacc) for parsing.</summary>
	- parse.y is Ruby grammar rule source file.</summary>
	- <img src="/px/ruby/tokenization.png"></summary>
	- LALR (lookahead left reversed rightmost derivation) parsing algorithm</summary>
	- Examples of Ruby grammar rules</summary>
</details>

<details>
	<summary>Ripper & script parsing</summary>
	- AST node structure: see with <code>$ruby --dump parsetree script.rb</code></summary>
</details>

</div>

<!--
CHAPTER 2
-->

<div class="textcard">
<summary><strong>2) Compilation</strong></summary>
	<p class="outline">Ruby’s compiler is no different. It translates your Ruby code into another language that Ruby’s virtual machine understands. The only difference is that you don’t use Ruby’s compiler directly; unlike in C or Java,Ruby’s compiler runs automatically without you ever knowing.</p>

<details>
	<summary>v1.8: no compiler</summary>
	<p class="outline">Ruby 1.8 immediately executes your code after tokenizing & parsing.</p>
	<img src="/px/ruby/no-compiler-in-1.8.png">
</details>
<details>
	<summary>v1.9: compiler introduced</summary>
	<p class="outline">Ruby 1.9 uses <em>YARV</em> (Yet Another Ruby Virtual Machine), similar to the Java Virtual Machine. YARV compiles source to bytecodes for much faster execution.</p>
</details>
<details>
	<summary>Simple script compilation</summary>
	<p class="outline">Important: YARV is <em>stack-oriented</em>. It recursively compiles an AST structure into the stack. <em>NODE_SCOPE</em> tells the compiler to build a new <em>scope</em>. <em>NODE_FCALL</em> represents a function call.<br>
	Ruby also replaces some YARV codes with specialized primitives.</p>
</details>
<details>
	<summary>Compiling a Call to a Block</summary>
	<p class="outline">
		
	</p>
</details>
<details>
	<summary>Displaying YARV instructions</summary>
</details>
<details>
	<summary>Local table</summary>
</details>
<details>
	<summary>Local table displays</summary>
</details>
</div>

<!--
CHAPTER 3
-->

<div class="textcard">
<strong>3) How Ruby Executes Your Code</strong></summary>

<details>
	<summary>YARV stack & your Ruby stack</summary></details>

<details>
	<summary>Ruby 2.0/1.9/1.8 Benchmarking</summary></details>
	
<details>
	<summary>Local & Dynamic variable access</summary></details>

<details>
	<summary>Special variables</summary></details>
</div>

<!--
CHAPTER 4
-->

<div class="textcard">
<strong>4) Control Structures & Method Dispatch</strong></summary>
<details>
	<summary>If statements</summary></details>
<details>
	<summary>Jumping from one Scope to Another</summary></details>
<details>
	<summary>For loops</summary></details>
<details>
	<summary>Send</summary></details>
<details>
	<summary>Method calls</summary></details>
<details>
	<summary>Calling built-in Methods</summary></details>
<details>
	<summary>How Ruby implements Keyword arguments</summary></details>
</div>

<!--
CHAPTER 5
-->

<div class="textcard">
<strong>5) Objects & Classes</strong></summary>
<details>
	<summary>Internals</summary></details>
<details>
	<summary>How Long to Save a New Instance Variable?</summary></details>
<details>
	<summary>RClass Internals</summary></details>
<details>
	<summary>Where does Ruby save Class Methods?</summary></details>
</div>

<!--
CHAPTER 6
-->

<div class="textcard">
<strong>6) Method & Constant Lookups</strong></summary>
<details>
	<summary>Ruby Modules</summary></details>
<details>
	<summary>Ruby Method Lookups</summary></details>
<details>
	<summary>Modifying Modules after Including them</summary></details>
</div>

<!--
CHAPTER 7
-->

<div class="textcard">
<strong>7) Hash Tables = the Ruby Workhorse</strong></summary>
<details>
	<summary>Hashes in Ruby</summary></details>
<details>
	<summary>Getting Values from Hashes with Varying Sizes</summary></details>
<details>
	<summary>Hash Table Expansions</summary></details>
<details>
	<summary>Inserting Elements into Hashes with Varying Sizes</summary></details>
<details>
	<summary>How Ruby Implements Hashes</summary></details>
<details>
	<summary>Using Objects as Hash Keys</summary></details>
</div>

<!--
CHAPTER 8
-->

<div class="textcard">
<strong>8) Ruby Borrowed from Lisp</strong></summary>
<details>
	<summary>Blocks</summary></details>
<details>
	<summary>While vs Block Passing: Which is Faster?</summary></details>
<details>
	<summary>Lambdas & Procs</summary></details>
<details>
	<summary>Changing local vars after calling Lambdas</summary></details>
</div>

<!--
CHAPTER 9
-->

<div class="textcard">
<strong>9) Metaprogramming</strong></summary>
<details>
	<summary>Alternative Ways to Define Methods</summary></details>
<details>
	<summary>self & Lexical Scope</summary></details>
<details>
	<summary>Closures</summary></details>
<details>
	<summary>Using Closures to Define Methods</summary></details>
</div>

<!--
CHAPTER 10
-->

<div class="textcard">
<strong>10) Jruby: Ruby on JVM</strong></summary>
<details>
	<summary>Running Programs</summary></details>
<details>
	<summary>JIT Compiler Monitoring</summary></details>
<details>
	<summary>Strings</summary></details>
<details>
	<summary>Copy-on-Write Performance</summary></details>
</div>

<!--
CHAPTER 11
-->

<div class="textcard">
<strong>11) Rubinius: Ruby Implemented with Ruby</strong></summary>
<details>
	<summary>Kernel & VM</summary></details>
<details>
	<summary>Backtraces</summary></details>
<details>
	<summary>Arrays</summary></details>
<details>
	<summary>Array#shift</summary></details>

</div>

<!--
CHAPTER 12
-->

<div class="textcard">
<strong>12) Garbage Collection</strong></summary>

<details>
	<summary>Three Problems to Solve</summary>
	<summary>Allocating memory for new objects</summary>
	<summary>ID'ing stale objects</summary>
	<summary>Reclaiming memory from stale objects</summary>
	</summary>
</details>

<details>
	<summary>Mark & Sweep</summary>
	<p class="outline">Finds memory for new objects until the <em>heap</em> (available memory) is exhausted, marks <em>live</em> objects, then sweeps remainder into available memory. Ruby resumes program execution once complete.</p>
	<summary>The Free List</summary>
	<img src="/px/ruby/gc-free-list.png">
	<p class="outline">Ruby objects are represented by <em>RVALUE</em> (a C struct). Each object's contents are often stored in a separate location.</p>
	<p class="outline">The initial value of the free memory list is ~10K RVALUE structures. MRI allocates more memory <em>heaps</em> as needed, ~16Kb in size, with 24 free lists of 407 objects per heap.</p>
	<summary>Marking</summary>
	<p class="outline">MRI marks stale objects by traversing an <em>object graph</em> & marking live objects in a <em>free bitmap</em>.
	<img src="/px/ruby/gc-free-bitmap.png"> This technique leverages Unix's <em>copy-on-write</em> to maximize memory utilization.</p>
	<summary>Sweeping</summary>
	<p class="outline">MRI moves ID'd garbage objects back into a free list by adjusting the pointers in each <em>RVALUE</em>.</p>
	<summary>Lazy Sweeping</summary>
	<p class="outline">LS sweeps the garbage RVALUE objects in only one heap back to the free list. This reduces the amount of time used in each GC operation.</p>
	<summary>Disadvantages</summary>
	<p class="outline">1) program must stop & wait; 2) mark & sweep time = proportional to total heap size; 3) all free list elements must be the same size.</p>
	<summary>Multiple Free Lists</summary>
	<summary>Marking</summary>
	<summary>MRI & Marking Live Objects</summary>
	<summary>Sweeping</summary>
	<summary>Lazy Sweeping</summary>
	<summary>RVALUE</summary>
	<summary>Disadvantages</summary>
<hr>
</details>

<details>
	<summary>MRI in Action</summary>
	<summary>Lazy Sweep</summary>
	<summary>Full Collection</summary>
	<summary>GC Profile Reports</summary>
</details>

<details>
	<summary>GC in JRuby & Rubinius</summary>
</details>

<details>
	<summary>Copying GC</summary>
	<summary>Bump Allocation</summary>
	<summary>Semi-Space Algorithm</summary>
	<summary>Eden Heap</summary>
</details>

<details>
	<summary>Generational GC</summary>
	<p class="outline">A technique that treats new & old objects differently.</p>
	<summary>Weak Generational Hypothesis</summary>
	<p class="outline">An assumption that new & old objects have <em>different life expectancies</em>.</p>
	<summary>Semi-Space Algorithm</summary>
	<p class="outline">Ideal for young objects b/c is copies only live objects.</p>
	<summary>Promoting Objects</summary>
	<img src="/px/ruby/gc-promoting.png">
	<p class="outline">An object is <em>promoted</em> (copied into the mature generation heap) when it survives a given # of GC runs.</p>
	<summary>GC for Mature Objects</summary>
	<p class="outline">Runs much less frequently. The JVM has cmndline options for configuring relative or absolute sizes of young & mature generation heaps.</p>
</details>

<details>
	<summary>Concurrent GC</summary>
	<p class="outline">When the GC runs <em>at the same time</em> as the application in a separate thread. Made easier in CPUs with multiple cores.</p>
	<summary>Marking while Object Graph Changes</summary>
	<p class="outline">Happens when an application adds a new object as a child of a previously marked object.</p>
	<img src="/px/ruby/gc-mark-graph-chgs.png">
	<summary>Tricolor Marking</summary>
	<p class="outline">Solves the above problem with a <em>mark stack</em>. As the GC marks objects it moves them from the mark stack to the list of marked objects (left).</p>
	<img src="/px/ruby/gc-mark-stack.png">
	<summary>3 GCs in JVM</summary>
	<p class="outline">Allows optimization based on the type of CPU hardware being used. 1) Serial; 2) Parallel (using separate thread); 3) Concurrent (optimized to reduce operation "pauses").</p>
</details>

<details>
	<summary>Verbose GC in JRuby</summary>
	<p class="outline">Experiment 12-2: use the JVM (install with <em>sudo apt install juby</em>) to show heap info while creating objects.</p>
	<summary>Triggering Major Collections with Mature Objects</summary>
	<p class="outline">repeat above experiment with new objects saved in an array.</p>
	<summary>Further Reading</summary>
	<p class="outline">
		<a href="https://www.amazon.com/Garbage-Collection-Handbook-Management-Algorithms/dp/1420082795">Garbage Collection Handbook (Jones, Hosking, Moss)</a></summary>
		<a href="https://www.amazon.com/Garbage-Collection-Algorithms-Automatic-Management/dp/0471941484">Garbage Collection Algorithms (Jones, Lins)</a></summary>
		<a href="ttp://www.oracle.com/technetwork/java/
javase/gc-tuning-6-140523.html">JVM GC Algorithm & Command Line Reference (Oracle)</a></summary>
	</p>
</details>

<details>
	<summary>Resources</summary>
</details>

</div>

<!--
(MORE)
-->

<div class="textcard">
<strong>More Ruby VMs</strong></summary>
<details>
	<summary>YARV</summary></details>
<details>
	<summary>Design Principles</summary></details>
<details>
	<summary>Prehistory</summary></details>
<details>
	<summary>Yet More</summary></details>
</div>

</div>
