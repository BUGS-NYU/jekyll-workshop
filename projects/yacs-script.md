---
layout: page
---
<style> pre { padding: 10px; background: black; } code span.c, code span.c1 { color: #828997; } code span.c:hover, code span.c1:hover { color: auto; } code span.nt, code span.n, code span.p, code span.o { color: #ABB2BF; } code span.nt:hover, code span.n:hover, code span.p:hover, code span.o:hover { color: auto; } code span.na, code span.bp, code span.mi { color: #D19A66; } code span.na:hover, code span.bp:hover, code span.mi:hover { color: auto; } code span.s { color: #98C379; } code span.s:hover { color: auto; } code span.nf { color: #61AFEF; } code span.nf:hover { color: auto; } code span.k, code span.ow { color: #C678DD; } code span.k:hover, code span.ow:hover { color: auto; } code span.nc { color: #E5C07B; } code span.nc:hover { color: auto; } </style>

# General&nbsp;Proposal&nbsp;for Course&nbsp;Prerequisites Language
<small>Evan Silverman and Albert Liu</small> <br />
This document proposes syntax and conventions for specifying the prerequisites of a
course. In some cases the proposals are general, i.e. "the syntax should have *this*
property", and in other cases it is specific, i.e. "we should use *this* keyword".
Note that the tone used here is mostly declarative; this is just for convenience.
All of these are suggestions, and the language is not yet defined.

<a name="sec-1"></a>
### 1. Variables <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Variables represent objects and are the bread and butter of this language.

<a name="sec-1-1"></a>
#### 1.1 Variable Identifiers can Contain Whitespace <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
For convenience, variable identifiers should include whitespace. For example,
`MATH-UA 123 Calculus III` would be handled as follows<sup>\*</sup>:

* Whitespace has no inherent meaning:<br />
e.g. <code>MATH-UA &nbsp;123 Calculus &nbsp; III</code> means the same thing
* ...except as a separator of non-whitespace:<br />
e.g. `MATH -UA 123 Calculus III` means something different
* Also, identifiers are stripped of additional whitespace:<br />
e.g. <code>&nbsp; MATH-UA 123 Calculus III &nbsp;</code> means the same thing

<small><sup>\*</sup> see [section 2.3](#sec-2-3) for an exception to this rule.</small>

<a name="sec-1-2"></a>
#### 1.2 "Name" is the Term for Variables <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Instead of variables, since we're operating on objects that have very concrete
real-world analogues, I think we should call variables *names*. `MATH-UA 123 Calculus III`
isn't a variable that holds a course boolean as much as it is the *name* of a course,
which we evaluate to be a course we have or haven't taken. The remainder of this
document will use the term "name" to refer to variables.

<a name="sec-1-3"></a>
#### 1.3 Assignment with `=` <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Name assignment should be done using `=`:

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 =</span>
  <span class="s">MATH-UA 123
  Calculus III</span></code></pre>
</div>

Note that this example is valid because whitespace is meaningless<sup>\*</sup>.

<small><sup>\*</sup> see [section 2.3](#sec-2-3) for an exception to this rule.</small>

<a name="sec-1-4"></a>
#### 1.4 "Naming" is the Term for Assignment <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Although we're assigning a value to a namespace, that doesn't really make sense
in natural language. Instead, I think we should call assignment "naming", so in
the above example we don't assign `calc 3` the value `MATH-UA 123 Calculus III`,
we instead give `MATH-UA 123 Calculus III` the name `calc 3`.

<a name="sec-2"></a>
### 2. The Punctuation is Almost English <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Because this language's target audience isn't necessarily familiar with the idioms
of computer science, and because, more generally, plain-text is easier to read, the
syntax of this language should be as close as possible to english.

<a name="sec-2-1"></a>
#### 2.1 Programs are Made of Sentences <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
A program is comprised of sentences, which are each executed in order. These sentences
can be separated by a period `.`, a semicolon `;`, or the
end of the file.

<a name="sec-2-2"></a>
#### 2.2 Programs are Organized into Paragraphs <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Code is organized into paragraphs; which are groups of sentences separated by
two or more newline characters. This isn't necessary for 95% of use cases, but
both simplifies parsing and improves readability.

<a name="sec-2-3"></a>
#### 2.3 Double Newline **Always** Means New Paragraph <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
A double newline indicates the end of the expression, regardless of context. For
example, this would be a syntax error:

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 =</span> <span class="s">MATH-UA 123

Calculus III</span></code></pre>
</div>

The reason is simple: in English, paragraphs always end with a complete idea. When
a paragraph ends on a quote, if that quote continues to the next paragraph it is
first ended, then restarted. Paragraphs denote a completion of a group of ideas
in English, and thus should do the same here. The above should instead be written
as

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 =</span> <span class="s">MATH-UA 123</span><span class="n">.</span>

<span class="s">Calculus III</span></code></pre>
</div>

to mean two separate paragraphs, or as

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 =</span> <span class="s">MATH-UA 123 Calculus III</span></code></pre>
</div>

to mean a single sentence.

<a name="sec-2-4"></a>
#### 2.4 The Last Sentence of the Program is its Final Value <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The last sentence of the program is the ultimate decider of whether or not the
course prerequisites are met or not. If the last sentence is a tautology, then
regardless of what happens before that, the course has no prerequisites, as students
will always qualify for it.

<a name="sec-2-5"></a>
#### 2.5 Leading and Trailing Whitespace is Ignored <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The last sentence is the last sentence, and the first sentence is the first sentence,
regardless of whitespace before or after. The above subsection applies even if the
file looks like this:

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 =</span> <span class="s">MATH-UA 123 Calculus III</span>

</code></pre>
</div>

<a name="sec-2-6"></a>
#### 2.6 Comments are Enclosed in Square Brackets <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Text that shouldn't be considered part of the program code, but is still useful to
include in the program, should be enclosed in `[Square Brackets]`. Doing so will
add a comment to the program at that location, and act the same as if you had just
typed a space there. For example,

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 = </span><span class="s">MATH-UA 123</span><span class="c">[Level 100 course]</span><span class="s">Calculus III</span></code></pre>
</div>

is interpreted the same as

<div class="highlight">
<pre class="highlight"><code><span class="n">calc 3 = </span><span class="s">MATH-UA 123 Calculus III</span></code></pre>
</div>

**Note:** Comments cannot contain double newlines. That shouldn't be necessary.

<a name="sec-3"></a>
### 3. Keywords are Plain Text <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
As stated above, we want the syntax of this language to be similar to English.
Part of that means ensuring that syntax uses *words, not symbols,* to denote
relationships between names.

<a name="sec-3-1"></a>
#### 3.1 Boolean Operators <code><span class="ow">AND</span></code>, <code><span class="ow">OR</span></code>, <code><span class="ow">NOT</span></code>
Booleans allow us to manipulate courses and start describing course prerequisites.
For example, if a student needs to take `JOUR-UA 50` and one of either `CORE-UA 711`
or `CORE-UA 724`, we could express that as

<div class="highlight">
<pre class="highlight"><code><span class="s">JOUR-UA 50 </span><span class="ow">AND</span><span class="n"> (</span><span class="s">CORE-UA 711 </span><span class="ow">OR</span><span class="s"> CORE-UA 724</span><span class="n">)</span></code></pre>
</div>

If a course can only be taken if an equivalent has not already been taken, we
can use <code><span class="ow">NOT</span></code> to express that. For example,

<div class="highlight">
<pre class="highlight"><code><span class="ow">NOT</span> <span class="s">JOUR-UA 50 </span><span class="ow">AND</span> <span class="ow">NOT</span> <span class="s">JOUR-UA 101 </span><span class="ow">AND</span> <span class="ow">NOT</span> <span class="s">JOUR-UA 102 </span></code></pre>
</div>

describes a course whose prerequisites only accepts students that have *not*
started down the journalism track at NYU.

<a name="sec-3-2"></a>
#### 3.2 Plain Text Keywords can Clash with Names <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Since names can contain whitespace, the language parser needs to do a lot more work
to prevent names from being misinterpreted. The following subsections propose
potential solutions to this problem, and the remaining sections will follow all
of them.

<a name="sec-3-3"></a>
#### 3.3 Keywords are Uppercase <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
while words like <code><span class="ow">and</span></code> and <code><span class="ow">or</span></code> are used in course names, their uppercase variants
really aren't. Thus, requiring keywords to be uppercase prevents namespace clashing.

<a name="sec-3-4"></a>
#### 3.4 Quotation Escapes Keywords <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Single and Double quotation can be used to indicate that a keyword is being used
as part of a name, and not as a keyword. For example, all of the following are
valid names, and mean the same thing:

<div class="highlight">
<pre class="highlight"><code><span class="s">JOUR-"UA" 50 Investigating "Journalism: Ethics AND "Practice</span><span class="n">.</span>
<span class="s">JOUR-'UA' 50 Investigating 'Journalism: Ethics AND 'Practice</span><span class="n">.</span>
<span class="s">JOUR-UA 50 Investigating 'J'"o"urnalism:'' E'thics 'AND' 'Practice</span></code></pre>
</div>

Additionally though, quotation escapes quotation, so the following would be different
from the previous examples:

<div class="highlight">
<pre class="highlight"><code><span class="s">"'JOUR-UA 50 Investigating Journalism: Ethics"</span> <span class="ow">AND</span> <span class="s">"Practice'"</span><span class="n">.</span>
<span class="s">"'JOUR-UA 50 Investigating Journalism: "Ethics" AND Practice'"</span></code></pre>
</div>

<a name="sec-3-5"></a>
#### 3.5 Syntax is Context-Dependent <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Words mean different things in different contexts. By restricting the meaning of
a keyword to a specific context or set of contexts, we can allow for some flexibility
in the use of keywords in names.
For example, the following might be permissible, if we don't include the left-hand side
of naming in the keyword context of <code><span class="ow">AND</span></code>:

<div class="highlight">
<pre class="highlight"><code><span class="n">CULTURES AND CONTEXTS = (</span><span class="s">CORE-UA 500</span><span class="n">, </span><span class="s">CORE-UA 509</span><span class="n">, </span><span class="s">CORE-UA 514</span><span class="n">, </span><span class="s">CORE-UA 515</span><span class="n">)</span></code></pre>
</div>

This kind of approach should be used conservatively; the use cases of keywords
should be **restricted to their intended use and nothing more.**

<a name="sec-4"></a>
### 4. Sets and Booleans are the Main Types <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The foundation of this section is the idea that the ultimate function of any prerequisite
specification is to, given an arbitrary set of a student's previous courses, return
a boolean value, either `prerequisites have been met`, or `prerequisites have not been met`.
For example, the prerequisite

```
Prerequisite: one introductory course
```

checks whether the courses that a student has taken contains at least one of
the introductory courses, and returns true if it does. Because booleans and sets
are the two types visible to the student, and to the writer, to minimize complexity
they should be the *only* types in the language.

Additionally, we should assume that collection order is irrelevant.
The order of taking courses is an emergent feature of the prerequisite
graph itself; it shouldn't be hard-coded in.

<a name="sec-4-1"></a>
#### 4.1 "List" is the Term for Unordered Sets <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
While the internal representation may be a set, the language's target audience is
not programmers, and thus the idea of an unordered set isn't necessarily a useful
name. The remainder of this document will use the term "list" to refer to an
unordered set.

<a name="sec-4-2"></a>
#### 4.2 List Builder Notation <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The following notation should be used to construct lists:

<div class="highlight">
<pre class="highlight"><code><span class="n">intro courses</span><span class="n"> = </span><span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span><span class="n">.</span>
<span class="n">intro courses</span><span class="n"> again = </span><span class="n">(</span>
  <span class="s">PHIL-UA 001</span><span class="n">, </span>
  <span class="s">PHIL-UA 003</span><span class="n">, </span>
  <span class="s">PHIL-UA 006</span><span class="n">, </span>
  <span class="s">PHIL-UA 007</span>
<span class="n">,)</span><span class="n">.</span><span class="c1">[One extra comma can be at the end but not the beginning]</span>
<span class="n">empty list = (,).</span>
<span class="n">another empty list = ().</span>
<span class="n">small course list = (</span><span class="s">PHIL-UA 001</span><span class="n">,)</span><span class="c1">[without the comma this is just a name]</span></code></pre>
</div>

<a name="sec-4-3"></a>
#### 4.3 Names are Duck-Typed <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
In the above example, we *named* the list <code><span class="n">intro courses</span></code>.
A name can refer to an arbitrary object, in the same sense that a name can be
given to anything. If it is used incorrectly later, an error will be raised at
that point.

<a name="sec-5"></a>
### 5. Quantifiers Make Lists into Booleans <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Quantifiers are a way to specify *how many* courses we'd like. They provide a simple
way to convert lists into booleans. For example, to give the above list a truth
value, we might want to use a quantifier such as *has taken at least 2 of the above
courses.* For the sake of this language, we will use the following quantifiers:

* At least *how many*
* At most *how many*
* Exactly *how many*

<a name="sec-5-1"></a>
#### 5.1 Quantifier Notation <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The above can be expressed with the following notation:

<div class="highlight">
<pre class="highlight"><code><span class="ow">AT LEAST</span> <span class='mi'>1</span> <span class='ow'>OF </span><span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span></code></pre>
</div>

Similarly, we can also write both of the following:

<div class="highlight">
<pre class="highlight"><code><span class="n">intro courses =</span> <span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span><span class='n'>.</span>
<span class="ow">AT MOST</span> <span class='mi'>1</span> <span class="ow">OF</span><span class="n"> intro courses</span><span class='n'>.</span>
<span class="ow">EXACTLY</span> <span class='mi'>1</span> <span class="ow">OF</span><span class="n"> intro courses</span></code></pre>
</div>

<a name="sec-5-2"></a>
#### 5.2 <code><span class="ow">AT LEAST</span></code> is Implicit <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
When reading the prerequisite `one introductory course`, we assume that having
taken 2 introductory courses is also perfectly fine; the equivalent is true in
this language. The following sentences are equivalent:

<div class="highlight">
<pre class="highlight"><code><span class="ow">AT LEAST</span> <span class='mi'>1</span> <span class="ow">OF</span><span class="n"> intro courses</span><span class='n'>.</span>
<span class='mi'>1</span> <span class="ow">OF</span><span class="n"> intro courses</span></code></pre>
</div>

<a name="sec-5-3"></a>
#### 5.3 Special Cases of Quantifier Notation <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Boolean logic can be considered a special case of quantifier notation; i.e.

```sql
"PHIL-UA 001" AND "PHIL-UA 003" AND "PHIL-UA 006" AND "PHIL-UA 007"
```

is the same thing as

<div class="highlight">
<pre class="highlight"><code><span class="ow">AT LEAST</span> <span class='mi'>4</span> <span class="ow">OF</span> <span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span></code></pre>
</div>

and

```sql
"PHIL-UA 001" OR "PHIL-UA 003" OR "PHIL-UA 006" OR "PHIL-UA 007"
```

is the same thing as

<div class="highlight">
<pre class="highlight"><code><span class="ow">AT LEAST</span> <span class='mi'>1</span> <span class="ow">OF</span> <span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span></code></pre>
</div>

<a name="sec-5-4"></a>
#### 5.4 Lists Have an Implicit Truth Value <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Lists implicitly have a truth value equivalent to chaining <code><span class="ow">AND</span></code> for
all of their elements; when at least one course hasn't been taken, the list is false,
and only when all courses have been taken is the list true.

<a name="sec-5-5"></a>
#### 5.5 <code><span class="ow">NOT</span></code> and <code><span class="ow">EXACTLY</span></code> Make Implicit Conversion Explicit <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
<code><span class="ow">EXACTLY</span></code> explicitly casts a list to its implicit truth value, and
<code><span class="ow">NOT</span></code> explicitly casts a list to the negation of its implicit truth
value.

<a name="sec-6"></a>
### 6. Other Operations on Lists <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
To reduce the work necessary to specify categorical requirements for a course,
we should allow for more complex operations on lists, beyond simply quantifying
the number of courses taken in them.

<a name="sec-6-1"></a>
#### 6.1 <code><span class="ow">AND</span></code> Combines Lists <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
<code><span class="ow">AND</span></code> acts as a union when used between lists, combining all the unique
elements of both lists into a new list.

For example, the following two lists are identical:

<div class="highlight">
<pre class="highlight"><code><span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span><span class="n">.</span>
<span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">)</span> <span class="ow">AND</span> <span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span></code></pre>
</div>

<a name="sec-6-2"></a>
#### 6.2 <code><span class="ow">WITHOUT</span></code> Finds List Differences <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
<code><span class="ow">WITHOUT</span></code> finds all the names in the list to its left which are not contained
in the list to its right. For example, to filter out `PHIL-UA 001` from the list
of introductory philosophy courses, you would do

<div class="highlight">
<pre class="highlight"><code><span class="n">intro courses</span> <span class="ow">WITHOUT</span> <span class="s">PHIL-UA 001</span></code></pre>
</div>

Notice that even though `PHIL-UA 001` is just a name for a course, and not a name
itself, <code><span class="ow">WITHOUT</span></code> automatically puts it in its own list. However, the
same can't be said the other way around:

<div class="highlight">
<pre class="highlight"><code><span class="s">PHIL-UA 001</span> <span class="ow">WITHOUT</span> <span class="n">intro courses</span><span class="c1">[This isn't correct grammar.]</span></code></pre>
</div>

<a name="sec-6-3"></a>
#### 6.3 <code><span class="ow">AND</span></code> Behavior Favors List Evaluation <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
When doing performing <code><span class="ow">AND</span></code> between a list and a boolean, the result
is the union of the list and a one-element list containing the boolean.
For example, the result of

<div class="highlight">
<pre class="highlight"><code><span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">)</span> <span class="ow">AND</span> <span class="s">PHIL-UA 007</span></code></pre>
</div>

is the list

<div class="highlight">
<pre class="highlight"><code><span class="n">(</span><span class="s">PHIL-UA 001</span><span class="n">, </span><span class="s">PHIL-UA 003</span><span class="n">, </span><span class="s">PHIL-UA 006</span><span class="n">, </span><span class="s">PHIL-UA 007</span><span class="n">)</span></code></pre>
</div>

<a name="sec-6-4"></a>
#### 6.4 <code><span class="ow">OR</span></code> Behavior Favors Boolean Evaluation <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
When performing <code><span class="ow">OR</span></code> with a list and another list, or a list and a boolean,
the list(s) are first implicitly turned into booleans, and then the result is
evaluated as a regular <code><span class="ow">OR</span></code>.

<a name="sec-7"></a>
### 7. Miscellaneous <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The above information should cover the vast majority of use cases. The following
subsections introduce concepts that will aid in the use and adoption of this language,
as well as allow for arbitrarily complex prerequisite systems without the need for
all professors to learn a database query language. Of the remaining subsections,
only 7.1 and 7.4 might be important for most users to know.

<a name="sec-7-1"></a>
#### 7.1 <code><span class="ow">READ</span></code> Gets Names From Other Programs <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
<code><span class="ow">READ</span></code> makes names from other programs available. If one or more <code><span class="ow">READ</span></code>
statements are used in a program, they must be in the first paragraph of the program,
and that paragraph may not contain anything but read statements and comments.

<a name="sec-7-2"></a>
#### 7.2 Boolean Literals <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The boolean literals are represented as <code><span class="mi">TRUE</span></code>
and <code><span class="mi">FALSE</span></code>. Determining the semantic meaning
of each symbol is left as an exercise to the reader.

<a name="sec-7-3"></a>
#### 7.3 System Administrators Use a Different Syntax to Create Meta-Files <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
A separate syntax can be used to create name-only programs that only exist to provide
other users with pre-made lists of courses. The syntax for this will be more technical,
as its purpose is to create larger pre-made lists from database queries.

<a name="sec-7-4"></a>
#### 7.4 Name Resolution Can be Customized <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The evaluation of a name to a truth value is an implementation detail. Resolving
names to actual courses in the database should be done through the implementation
of the language, and specified on a per-school basis.

<a name="sec-7-5"></a>
#### 7.5 The Final Line of a Prerequisites Program is Visible to Students <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
The syntax of this language may be cleaner than that of existing prerequisite descriptions.
Thus, it may be beneficial to use the last line of the program for a specific course
as the message displayed to students when registering. This message would also
include comments (with brackets omitted).

<a name="sec-7-6"></a>
#### 7.6 Title Comments Give Names to Paragraphs <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
Single-line names that begin after a paragraph break and end with a colon and line
break are title comments. They only differ from normal comments in syntax, and
the fact that they can only be one line.

<a name="sec-7-7"></a>
#### 7.7 Generalization of Language to Degree Requirements <small><small><code class="no-style">[</code><a href="#">back to top</a><code class="no-style">]</code></small></small>
By the organizing sections of degree requirements into paragraphs, we can use this
language to specify degree requirements as well as course requirements.
