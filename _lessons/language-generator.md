---
title: Language Generator
nav_order: 5
has_children: true
has_toc: false
summary: Due Nov 5
---

# Language Generator
{: .no_toc .mb-2 }

Generating sentences with recursion and randomness.[^1]
{: .fs-6 .fw-300 }

[^1]: Julie Zelenski. 1999. Random Sentence Generator. In Nifty Assignments 1999. <https://www-cs-faculty.stanford.edu/~zelenski/rsg/>

In syntactocentric linguistics, **recursive syntax** (embedding phrases within phrases) has been hypothesized to be the critical feature of human language capacity. Although this claim has been challenged in recent decades, generating understandable human language remains a key challenge for computer programming given the infinite expressiveness of human language. Can we define a program to generate all possible English sentences?

{% assign module = site.modules | where: 'title', page.title | first %}
{{ module }}

Most (if not all) human languages involve combining words in certain ways that correspond to valid sentences. The rules that determine valid and invalid sentences are part of the language's grammar.

Formal language
: A set of words and symbols along with a set of production rules defining how those symbols may be used together. For example, "A boy threw the ball." is a valid sentence, but "A threw boy ball the" makes no sense, because the words were put together in an invalid manner.

Grammar
: A way of describing the syntax and symbols of a formal language. When constructing sentences, words are put together in grammatically-correct ways using structures such as sentences, noun phrases, and objects. Grammars consist of two types of **symbols** that represent either individual words (**terminal**) or combinations of words such as phrases and sentences (**non-terminal**).

**Generative grammar** is a linguistic theory that supposes a system of rules can be followed to generate every possible grammatical expression in a formal language. For example, consider this formal language with the following terminals and non-terminals.

Terminals
: the, a, boy, girl, runs, walks

Non-terminals
: - A **sentence** consists of an **article** followed by an **object** followed by a **verb**.
  - An **article** consists of either "the" or "a".
  - An **object** consists of either "boy" or "girl".
  - A **verb** consists of either "runs" or walks".

{::comment}
digraph {
    ranksep=0.5
    nodesep=0.75
    node[shape=rectangle fontname=Roboto height=0]
    {
        node[shape=none]
        the
        girl
        runs
    }
    sentence:w -> article:n
    article -> the
    sentence -> object -> girl
    sentence:e -> verb:n
    verb -> runs
}
{:/comment}

<svg width="auto" viewBox="0.00 0.00 278.00 154.40">
<g id="graph0" class="graph" transform="scale(1 1) rotate(0) translate(4 150.4)">
<polygon fill="#ffffff" stroke="transparent" points="-4,4 -4,-150.4 274,-150.4 274,4 -4,4"/>
<!-- the -->
<g id="node1" class="node">
<text text-anchor="middle" x="27" y="-8.2" font-family="Roboto" font-size="14.00" fill="#000000">the</text>
</g>
<!-- girl -->
<g id="node2" class="node">
<text text-anchor="middle" x="135" y="-8.2" font-family="Roboto" font-size="14.00" fill="#000000">girl</text>
</g>
<!-- runs -->
<g id="node3" class="node">
<text text-anchor="middle" x="243" y="-8.2" font-family="Roboto" font-size="14.00" fill="#000000">runs</text>
</g>
<!-- sentence -->
<g id="node4" class="node">
<polygon fill="none" stroke="#000000" points="167.1939,-146.3008 102.8061,-146.3008 102.8061,-121.6992 167.1939,-121.6992 167.1939,-146.3008"/>
<text text-anchor="middle" x="135" y="-129.8" font-family="Roboto" font-size="14.00" fill="#000000">sentence</text>
</g>
<!-- article -->
<g id="node5" class="node">
<polygon fill="none" stroke="#000000" points="54,-85.5008 0,-85.5008 0,-60.8992 54,-60.8992 54,-85.5008"/>
<text text-anchor="middle" x="27" y="-69" font-family="Roboto" font-size="14.00" fill="#000000">article</text>
</g>
<!-- sentence&#45;&gt;article -->
<g id="edge1" class="edge">
<path fill="none" stroke="#000000" d="M103,-134C66.4649,-134 33.4779,-126.8275 27.8454,-95.2736"/>
<polygon fill="#000000" stroke="#000000" points="31.3242,-94.8722 27,-85.2 24.3487,-95.4577 31.3242,-94.8722"/>
</g>
<!-- object -->
<g id="node6" class="node">
<polygon fill="none" stroke="#000000" points="162,-85.5008 108,-85.5008 108,-60.8992 162,-60.8992 162,-85.5008"/>
<text text-anchor="middle" x="135" y="-69" font-family="Roboto" font-size="14.00" fill="#000000">object</text>
</g>
<!-- sentence&#45;&gt;object -->
<g id="edge3" class="edge">
<path fill="none" stroke="#000000" d="M135,-121.6962C135,-114.3769 135,-104.857 135,-96.1922"/>
<polygon fill="#000000" stroke="#000000" points="138.5001,-95.904 135,-85.904 131.5001,-95.9041 138.5001,-95.904"/>
</g>
<!-- verb -->
<g id="node7" class="node">
<polygon fill="none" stroke="#000000" points="270,-85.5008 216,-85.5008 216,-60.8992 270,-60.8992 270,-85.5008"/>
<text text-anchor="middle" x="243" y="-69" font-family="Roboto" font-size="14.00" fill="#000000">verb</text>
</g>
<!-- sentence&#45;&gt;verb -->
<g id="edge5" class="edge">
<path fill="none" stroke="#000000" d="M167,-134C203.5351,-134 236.5221,-126.8275 242.1546,-95.2736"/>
<polygon fill="#000000" stroke="#000000" points="245.6513,-95.4577 243,-85.2 238.6758,-94.8722 245.6513,-95.4577"/>
</g>
<!-- article&#45;&gt;the -->
<g id="edge2" class="edge">
<path fill="none" stroke="#000000" d="M27,-60.8962C27,-53.5769 27,-44.057 27,-35.3922"/>
<polygon fill="#000000" stroke="#000000" points="30.5001,-35.104 27,-25.104 23.5001,-35.1041 30.5001,-35.104"/>
</g>
<!-- object&#45;&gt;girl -->
<g id="edge4" class="edge">
<path fill="none" stroke="#000000" d="M135,-60.8962C135,-53.5769 135,-44.057 135,-35.3922"/>
<polygon fill="#000000" stroke="#000000" points="138.5001,-35.104 135,-25.104 131.5001,-35.1041 138.5001,-35.104"/>
</g>
<!-- verb&#45;&gt;runs -->
<g id="edge6" class="edge">
<path fill="none" stroke="#000000" d="M243,-60.8962C243,-53.5769 243,-44.057 243,-35.3922"/>
<polygon fill="#000000" stroke="#000000" points="246.5001,-35.104 243,-25.104 239.5001,-35.1041 246.5001,-35.104"/>
</g>
</g>
</svg>

This language contains the following valid sentences.

- the boy runs
- the boy walks
- a boy runs
- a boy walks
- the girl runs
- the girl walks
- a girl runs
- a girl walks

## Specification

Implement a `LanguageGenerator` class that generates valid strings according to the production rules defined by the given `Grammar`. A `Grammar` consists of a `Supplier` field with a `get()` method that returns a `Map<String, String[]>` representing the production rules.

`LanguageGenerator(Grammar grammar)`
: Constructs a new `LanguageGenerator` for the given grammar.

`LanguageGenerator(Grammar grammar, Random random)`
: Constructs a new `LanguageGenerator` for the given grammar and source of randomness.

`Iterable<String> nonterminals()`
: Returns an iterable containing all non-terminal symbols in the grammar.

`String generate(String target)`
: Returns a string generated by following the production rule for the given `target`. The resulting string should be compact: there should be exactly one space between each terminal and no leading or trailing spaces. Choose between potential production rules for the given `target` by calling `random.nextInt` so that each possibility is equally likely to be chosen.

## Development strategy

The `generate` method is an example of **generative recursion**: we're modeling a real-life recursive process by writing a corresponding recursive algorithm in Java. The base case occurs when given a terminal symbol. Otherwise, in the recursive case (a non-terminal symbol):

1. Choose a random expansion rule for the given non-terminal `target`.
1. For each symbol in the expansion rule, recursively `generate` an occurrence of that symbol.

## Splitting text

Split each string on one or more whitespace characters by calling `split("\\s+")`.

```java
String text = input.nextLine();
String[] terms = text.split("\\s+");
```

## Trimming whitespace

Use the `trim` method to remove leading and trailing whitespace. Consider introducing a public/private pair to trim leading or trailing spaces from the final result.

```java
String text = "   lots   of  spaces    ";
String trimmed = str.trim();
// "lots   of  spaces"
```

## Web app

To launch the web app, **Open Terminal** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 82" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="terminal"><path d="M44.518 70.139H100v11.097H44.518z"></path><path d="M7.845 73.347L0 65.502l28.826-28.828L0 7.845 7.845 0l36.673 36.674L7.845 73.347z" fill-rule="nonzero"></path></svg>, paste the following command, and press Enter.

```sh
javac -cp ".:/course/lib/*" Server.java && java -cp ".:/course/lib/*" Server; rm *.class
```

Then, open the **Network** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 71" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="wifi"><path d="M0 20.693l9.091 9.091c22.592-22.592 59.225-22.592 81.818 0L100 20.693c-27.593-27.59-72.363-27.59-100 0zm36.364 36.364L50 70.693l13.637-13.637c-7.502-7.545-19.727-7.545-27.273.001zM18.182 38.875l9.091 9.091c12.544-12.544 32.91-12.544 45.455 0l9.091-9.091c-17.544-17.545-46.046-17.545-63.637 0z" fill-rule="nonzero"></path></svg> dropdown and select host 0.0.0.0:8000.

## Grading

**Mark** the program to submit it for grading. In addition to the automated tests, the final submission will also undergo code review for [internal correctness]({{ site.baseurl }}{% link quality/index.md %}) on comments, variable names, indentation, data fields, and code quality.

Control structure errors
: [Extra recursive cases or extra base cases that are not needed.]({{ site.baseurl }}{% link quality/zen.md %}#recursion-zen) For example, introducing additional "arm's length" base cases that solve the problem preemptively.

Method errors
: [Unnecessary parameters with redundant information when it could be accessed from another source.]({{ site.baseurl }}{% link quality/class-design.md %}#parameters)

Data structure errors
: Excessive inefficiency when using collections. For example, using a for-each loop to find a value in a map when `get` would return the value directly.
