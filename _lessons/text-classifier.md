---
title: Text Classifier
nav_order: 7
has_children: true
has_toc: false
summary: Due Nov 19
---

# Text Classifier
{: .no_toc .mb-2 }

Implementing a decision tree data type for text classification.
{: .fs-6 .fw-300 }

Online abuse and harassment stops people from engaging in conversation. One area of focus is the study of negative online behaviors, such as **toxic comments**: user-written comments that are rude, disrespectful or otherwise likely to make someone leave a discussion. Platforms struggle to effectively facilitate conversations, leading many communities to [limit](https://meta.stackexchange.com/q/342779) or [completely shut down](https://en.wikipedia.org/wiki/R/The_Donald#Quarantine,_restriction,_ban_and_successor) user comments. In 2018, the [Conversation AI](https://conversationai.github.io/) team, a research initiative founded by [Jigsaw](https://jigsaw.google.com/) and Google (both part of Alphabet), organized a public competition called the [Toxic Comment Classification Challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge) to build better machine learning systems for detecting different types of of toxicity like threats, obscenity, insults, and identity-based hate.[^1]

[^1]: When the Conversation AI team first built toxicity models, they found that the models [incorrectly learned to associate](https://medium.com/the-false-positive/unintended-bias-and-names-of-frequently-targeted-groups-8e0b81f80a23) the names of frequently attacked identities with toxicity. In 2019, the Conversation AI team ran another competition about [Unintended Bias in Toxicity Classification](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification), focusing on building models that detect toxicity across a range of diverse conversations.

{% assign module = site.modules | where: 'title', page.title | first %}
{{ module }}

Toxic comment classification is a special case of a more general problem in machine learning known as **text classification**. Discussion forums use text classification to determine whether comments should be flagged as inappropriate. Email software uses text classification to determine whether incoming mail is sent to the inbox or filtered into the spam folder.[^2]

![Spam email classifier]({{ site.baseurl }}{% link assets/images/spam-classifier.png %})

[^2]: Google Developers. Oct 1, 2018. Text classification. In Machine Learning Guides. <https://developers.google.com/machine-learning/guides/text-classification>

Warning

: Machine learning models are trained on human-selected and human-generated datasets. Such models encode and reproduce the implicit bias inherent in the datasets. This model is not meant to generalize beyond the toy training datasets. Don't use this in a real system!

  The included vectorization algorithms also encode explicit bias. The vectorization ignores all grammar and syntax, treating each occurrence of a word as independent from all other words in the text. Any usage of a word, no matter the context, is considered equally toxic or spammy.

  The provided datasets contain text that may be considered profane, vulgar, or offensive.

## Specification

Implement a `TextClassifier` data type, a binary classification tree for text documents.

`TextClassifier(Vectorizer vectorizer, Splitter splitter)`
: Constructs a new `TextClassifier` given a fitted `vectorizer` for transforming data points and a `splitter` for determining the splits in the tree.

`boolean classify(String text)`
: Returns a boolean representing the predicted label for the given `text`.

`void print()`
: Prints a Java code representation of this tree in if/else statement format with proper braces and indentation, 1 space per indent level. Leaf nodes should print "return true;" or "return false;" depending on the label value.

`void prune(int depth)`
: Prunes this tree to the given `depth`. Each pruned subtree is replaced with a new node with the subtree's majority label.

Three helper classes are provided to interface between the binary tree data structure and the data representation of the `TextClassifier`. The most useful methods are described below.

### Splitter

The `Splitter` class computes the best split of the data into left and right subsets.

`Splitter.Result split()`
: Returns the best split and the left and right splitters, or null if no good split exists.

`boolean label()`
: Returns the majority label for this splitter.

### Split

The `Split` class represents a decision rule for splitting vector data.

`boolean goLeft(double[] vector)`
: Returns true if and only if the given vector lies to the left of this decision rule.

`String toString()`
: Returns a string representation of this decision rule.

### Vectorizer

The `Vectorizer` interface defines data representation algorithms transforming English text into `double[][]` matrices for the `Splitter` class.

`double[][] transform(String... texts)`
: Returns the design matrix for the given texts. Given a single `text`, `transform(text)[0]` evaluates to a `double[] vector` that can be passed to `Split.goLeft`.

The `TextClassifier.from` method creates a `Splitter` and a `BM25Vectorizer`. We also provide an optional `LSAVectorizer` that improves the accuracy of the model but requires more processing power.

<details markdown="1">
<summary>Optionally, learn how to run LSAVectorizer from your computer terminal.</summary>

Make sure that you have JDK 11 or later installed on your system and accessible from the terminal. Download and unzip your assessment workspace from Ed. You'll also need to download and unzip a copy of the [Statistical Machine Intelligence and Learning Engine](https://haifengl.github.io/) library for Java. We built the program for [smile-2.5.2.zip](https://github.com/haifengl/smile/releases/download/v2.5.2/smile-2.5.2.zip). Copy the `lib` directory containing all of the `jar` files into your project.

To use the `LSAVectorizer`, modify the `from` method to construct a new `LSAVectorizer`. Then, navigate to your project directory in the terminal and compile and run the `Main` class with the `lib` directory in the classpath.

```sh
javac -cp ".:lib/*" Main.java
java -cp ".:lib/*" Main
```
</details>

## Web app

To launch the web app, **Open Terminal** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 82" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="terminal"><path d="M44.518 70.139H100v11.097H44.518z"></path><path d="M7.845 73.347L0 65.502l28.826-28.828L0 7.845 7.845 0l36.673 36.674L7.845 73.347z" fill-rule="nonzero"></path></svg>, paste the following command, and press Enter.

```sh
javac -cp ".:/course/lib/*" Server.java && java -cp ".:/course/lib/*" Server toxic.tsv; rm *.class
```

Then, open the **Network** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 71" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="wifi"><path d="M0 20.693l9.091 9.091c22.592-22.592 59.225-22.592 81.818 0L100 20.693c-27.593-27.59-72.363-27.59-100 0zm36.364 36.364L50 70.693l13.637-13.637c-7.502-7.545-19.727-7.545-27.273.001zM18.182 38.875l9.091 9.091c12.544-12.544 32.91-12.544 45.455 0l9.091-9.091c-17.544-17.545-46.046-17.545-63.637 0z" fill-rule="nonzero"></path></svg> dropdown and select host 0.0.0.0:8000.

## Grading

**Mark** the program to submit it for grading. In addition to the automated tests, the final submission will also undergo code review for [internal correctness]({{ site.baseurl }}{% link quality/index.md %}) on comments, variable names, indentation, data fields, and code quality.

Data structure errors
: Not using `x = change(x)` when appropriate to simplify code.
: Poor choice of constructors when designing a node class. For example, including unused constructors, missing helpful constructors that eliminate redundancy, or not having a fitting constructor for a reoccuring type of node.
