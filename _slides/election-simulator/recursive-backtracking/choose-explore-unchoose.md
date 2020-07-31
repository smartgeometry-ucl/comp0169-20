---
title: Choose-explore-unchoose
nav_order: 0
---

Many of our exhaustive search problems will involve using a data structure to keep track of progress and build toward solutions. However, working with data structures is more complicated than working with numbers and strings. Consider the recursive method `rollDice` that prints out all of the possible outcomes of rolling 4 dice. Instead of representing the partial solution state as a string, this stores data in a list.

```java
public static void rollDice(int dice) {
    rollDice(dice, new ArrayList<Integer>());
}

private static void rollDice(int dice, List<Integer> chosen) {
    if (dice == 0) {
        System.out.println(chosen);
    } else {
        for (int value = 1; value <= 6; value++) {
            // Add the dice roll value to the chosen outcomes
            chosen.add(value);
            rollDice(dice - 1, chosen);
        }
    }
}
```

However, this algorithm has a critical bug due to Java reference semantics!

<details markdown="1">
<summary>Describe the bug in your own words.</summary>

Remember that there is only a single list of `chosen` outcomes shared between every recursive call!

Consider what happens after rolling the first dice and add 1 to the `chosen` list of outcomes. The recursion here makes sense: we want to pass the updated list of `chosen` outcomes to the next recursive call.

ut when we return from the `rollDice` call, the `chosen` list has been totally changed in the process! In addition to adding 1 to the `chosen` list of outcomes, each recursive call also has to "clean-up" after itself by undoing its choice so that the next recursive call won't be affected by the choices made in the first recursive branch.
</details>

In order to address the unintended changes to the `chosen` list, we need to remove the choice that the current recursive method call was responsible for adding: the most recent outcome.

Choose-explore-unchoose pattern
: For each option:
  1. **Choose** the option.
  1. **Explore** the option.
  1. **Unchoose** the option.

```java
public static void rollDice(int dice) {
    rollDice(dice, new ArrayList<Integer>());
}

private static void rollDice(int dice, List<Integer> chosen) {
    if (dice == 0) {
        System.out.println(chosen);
    } else {
        for (int value = 1; value <= 6; value++) {
            chosen.add(value);                // Choose
            rollDice(dice - 1, chosen);       // Explore
            chosen.remove(chosen.size() - 1); // Unchoose
        }
    }
}
```
