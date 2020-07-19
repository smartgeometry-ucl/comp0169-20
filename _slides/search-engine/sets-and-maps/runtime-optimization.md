---
title: Runtime optimization
nav_order: 0
---

Earlier, we saw that the worst-case order of growth of the runtime for `countUnique` with an `ArrayList` is in Θ(N<sup>2</sup>), where N is the length of the list. The `ArrayList.contains` algorithm may need to scan over the entire list on each iteration of the `while` loop.

```java
public static int countUnique(Scanner input) {
    List<String> words = new ArrayList<String>();
    int count = 0;
    while (input.hasNext()) {
        String word = input.next();
        if (!words.contains(word)) {
            count++;
        }
        words.add(word);
    }
    return count;
}
```
{: overlay="Client" }

On a real dataset containing all of Shakespeare's words, it takes about 3.5 minutes to determine that Shakespeare used 33,505 unique words.[^1] Designing programs for data on the internet might require dealing with even more data every second!

[^1]: This is an overcount since `Scanner` splits tokens on whitespace, so words can include punctuation.

One way to speed up the `countUnique` method is to use a **set** abstract data type instead of a **list** for the same reason why we introduced stacks and queues even though lists have more capabilities. By restricting the public methods (capabilities), implementers can design more efficient data structures to implement each method.
