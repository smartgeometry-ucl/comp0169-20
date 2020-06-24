---
title: Search Engine
nav_order: 3
has_children: true
has_toc: false
summary: Due Oct 22
---

# Search Engine
{: .no_toc .mb-2 }

Building a search engine with maps and sets.[^1]
{: .fs-6 .fw-300 }

[^1]: Chris Piech and Mehran Sahami. 2020. Bajillion Search Engine. In CS 106A Spring 2020. <https://web.stanford.edu/class/archive/cs/cs106a/cs106a.1206/assn/15-assignment7.pdf>

Web search engines are software systems that organize information on the internet so that users can discover web pages related to a search query. We can implement a basic web search engine by building an **inverted index** (also known as an **index**) that maps each term (word) to the set of web pages in which it appears. A search query, which is a sequence of one or more keywords, can be answered by returning the web pages that contain all of the terms in a given query.

{% assign module = site.modules | where: 'title', page.title | first %}
{{ module }}

## Specification

Implement a `SearchEngine` class that represents an inverted index.

`SearchEngine()`
: Constructs an empty `SearchEngine` instance.

`void index(String title, String contents)`
: Adds each term in **both** the `title` and the `contents` to the inverted index.

`Map<String, String> search(String query)`
: Returns a map from titles to snipped contents for each web page that contains all of the keywords in the given `query` ignoring any unknown keywords before the first matching keyword. The contents should be snipped based on the first matching keyword. If there are no matching keywords or if the `query` is empty, then an empty map is returned.

## Splitting text

Split each string on one or more whitespace characters by calling `split("\\s+")`.

```java
String[] terms = text.split("\\s+");
```

## Normalizing text

Many web pages include punctuation marks and other special characters that make it harder for users to search for relevant information. For example, the last line of `test2.txt` contains several terms with unusual punctuation.

```
!carrot! ,!Dog*&
```

Splitting on whitespace characters would yield two terms, `"!carrot!"` and `",!Dog*&"`. Neither of these terms match common search queries for `"carrot"` or `"dog"`. To improve the quality of search results, the `normalize` method returns a standardized, lowercase representation for the given string. For example, `normalize(",!Dog*&")` returns `"dog"`. **Normalize each term in the inverted index and each keyword in the search query.**

## Snipping text

The `search` method should return snips of the verbatim, original (not normalized) web page contents. `snip` is relatively slow, so if the automated external correctness tests are timing out, make sure that `snip` is only called once for each of the web pages returned in the final state of the map.

## Web app

To launch the web app, **Open Terminal** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 82" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="terminal"><path d="M44.518 70.139H100v11.097H44.518z"></path><path d="M7.845 73.347L0 65.502l28.826-28.828L0 7.845 7.845 0l36.673 36.674L7.845 73.347z" fill-rule="nonzero"></path></svg>, paste the following command, and press Enter.

```sh
javac Server.java && java Server bbcnews/*.txt; rm *.class
```

Then, open the **Network** <svg class="inline-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 71" fill-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2" id="wifi"><path d="M0 20.693l9.091 9.091c22.592-22.592 59.225-22.592 81.818 0L100 20.693c-27.593-27.59-72.363-27.59-100 0zm36.364 36.364L50 70.693l13.637-13.637c-7.502-7.545-19.727-7.545-27.273.001zM18.182 38.875l9.091 9.091c12.544-12.544 32.91-12.544 45.455 0l9.091-9.091c-17.544-17.545-46.046-17.545-63.637 0z" fill-rule="nonzero"></path></svg> dropdown and select host 0.0.0.0:8000.

## Grading

**Mark** the program to submit it for grading. In addition to the automated tests, the final submission will also undergo code review for [internal correctness]({{ site.baseurl }}{% link quality/index.md %}) on comments, variable names, indentation, data fields, and code quality.

Method errors
: [Non-exception code should not be in an else branch.]({{ site.baseurl }}{% link quality/formatting.md %}#exceptions)
: Not decomposing complex methods into logical subtasks that each have their own method. Create `private` "helper" methods to capture repeated code. A good rule of thumb for this assignment is that no method should have more than 20 lines of code in its body.

Data structure errors
: Excessive inefficiency when using collections. For example, using a for-each loop to find a value of a map when a call to `get` would return the value.
: [Using a collection when not necessary, or using the wrong colelction type.]({{ site.baseurl }}{% link quality/data-types.md %}#prefer-simple-data-types) For example, using a list instead of a set when we only want to maintain unique elements.
