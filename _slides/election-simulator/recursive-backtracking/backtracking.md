---
title: Backtracking
nav_order: 1
---

For some problems, exhaustive search is our best bet. If a problem requires printing out all combinations of numbers in a list, then an algorithm must generate every combination along the way.

But other problems don't necessary require generating all possible solutions. **Recursive backtracking** is a recursive problem-solving approach that speeds-up exhaustive search by backtracking whenever the algorithm reaches a dead-end. Consider the recursive method `sumDice` that's similar to `rollDice`, but only prints the dice roll outcomes that sum up to a given `total`.

```java
public static void sumDice(int dice, int total) {
    rollDice(dice, total, new ArrayList<Integer>());
}

private static void sumDice(int dice, int total, List<Integer> chosen) {
    if (total == 0 && dice == 0) {
        // Successful combination
        System.out.println(chosen);
    } else if (total >= dice && total <= 6 * dice) {
        // Only continue searching if it's possible to sum up to total
        for (int value = 1; value <= 6; value++) {
            chosen.add(value);
            sumDice(dice - 1, total - value, chosen);
            chosen.remove(chosen.size() - 1);
        }
    }
}
```

In the recursive case, we introduced a new condition: only continue searching if the `total` is feasible with the given number of remaining `dice`. For example, if the value of the first dice is 6, we know that's it's impossible to roll two more dice such that the two sums to 5. In the recursion tree below, combinations that won't lead to any valid solutions are filled red.

{::comment}
digraph {
    ranksep=0.5
    nodesep=0.25
    graph[splines=line]
    node[fontname=Roboto]
    {
        node[style=filled fillcolor=lightcoral]
        4
        5
        6
        14
        15
        16
        111
        112
        114
        115
        116
    }
    {
        node[style=filled fillcolor=mediumspringgreen]
        113
    }
    root[label="sumDice(3, 5)"]
    root -> 1
    1 -> 11
    11 -> 111
    11 -> 112
    11 -> 113
    11 -> 114
    11 -> 115
    11 -> 116
    1 -> 12
    1 -> 13
    1 -> 14
    1 -> 15
    1 -> 16
    root -> 2
    root -> 3
    root -> 4
    root -> 5
    root -> 6
    {
        rank=same
        rankdir=LR
        1 -> 2 -> 3 -> 4 -> 5 -> 6[style=invis]
    }
    {
        rank=same
        rankdir=LR
        11 -> 12 -> 13 -> 14 -> 15 -> 16[style=invis]
    }
    {
        rank=same
        rankdir=LR
        111 -> 112 -> 113 -> 114 -> 115 -> 116[style=invis]
    }
}
{:/comment}

<svg width="auto" viewBox="0.00 0.00 782.00 260.00">
<g id="graph0" class="graph" transform="scale(1 1) rotate(0) translate(4 256)">
<polygon fill="#ffffff" stroke="transparent" points="-4,4 -4,-256 778,-256 778,4 -4,4"/>
<!-- 4 -->
<g id="node1" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="603" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="603" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">4</text>
</g>
<!-- 5 -->
<g id="node2" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="675" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="675" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">5</text>
</g>
<!-- 4&#45;&gt;5 -->
<!-- 6 -->
<g id="node3" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="747" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="747" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">6</text>
</g>
<!-- 5&#45;&gt;6 -->
<!-- 14 -->
<g id="node4" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="423" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="423" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">14</text>
</g>
<!-- 15 -->
<g id="node5" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="495" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="495" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">15</text>
</g>
<!-- 14&#45;&gt;15 -->
<!-- 16 -->
<g id="node6" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="567" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="567" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">16</text>
</g>
<!-- 15&#45;&gt;16 -->
<!-- 111 -->
<g id="node7" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="27" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="27" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">111</text>
</g>
<!-- 112 -->
<g id="node8" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="99" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="99" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">112</text>
</g>
<!-- 111&#45;&gt;112 -->
<!-- 113 -->
<g id="node12" class="node">
<ellipse fill="#00fa9a" stroke="#000000" cx="171" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="171" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">113</text>
</g>
<!-- 112&#45;&gt;113 -->
<!-- 114 -->
<g id="node9" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="243" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="243" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">114</text>
</g>
<!-- 115 -->
<g id="node10" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="315" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="315" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">115</text>
</g>
<!-- 114&#45;&gt;115 -->
<!-- 116 -->
<g id="node11" class="node">
<ellipse fill="#f08080" stroke="#000000" cx="387" cy="-18" rx="27" ry="18"/>
<text text-anchor="middle" x="387" y="-13.8" font-family="Roboto" font-size="14.00" fill="#000000">116</text>
</g>
<!-- 115&#45;&gt;116 -->
<!-- 113&#45;&gt;114 -->
<!-- root -->
<g id="node13" class="node">
<ellipse fill="none" stroke="#000000" cx="567" cy="-234" rx="66.0531" ry="18"/>
<text text-anchor="middle" x="567" y="-229.8" font-family="Roboto" font-size="14.00" fill="#000000">sumDice(3, 5)</text>
</g>
<!-- root&#45;&gt;4 -->
<g id="edge16" class="edge">
<path fill="none" stroke="#000000" d="M576.0843,-215.8314C580.2274,-207.5451 585.2137,-197.5727 589.7626,-188.4748"/>
<polygon fill="#000000" stroke="#000000" points="592.9495,-189.9273 594.2911,-179.4177 586.6885,-186.7967 592.9495,-189.9273"/>
</g>
<!-- root&#45;&gt;5 -->
<g id="edge17" class="edge">
<path fill="none" stroke="#000000" d="M592.0488,-217.3008C608.6046,-206.2636 630.3151,-191.7899 647.3724,-180.4184"/>
<polygon fill="#000000" stroke="#000000" points="649.4372,-183.2484 655.8162,-174.7892 645.5542,-177.4241 649.4372,-183.2484"/>
</g>
<!-- root&#45;&gt;6 -->
<g id="edge18" class="edge">
<path fill="none" stroke="#000000" d="M604.2961,-219.0816C636.7247,-206.1101 683.2485,-187.5006 714.2601,-175.096"/>
<polygon fill="#000000" stroke="#000000" points="715.7613,-178.2652 723.7462,-171.3015 713.1615,-171.7658 715.7613,-178.2652"/>
</g>
<!-- 1 -->
<g id="node14" class="node">
<ellipse fill="none" stroke="#000000" cx="387" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="387" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">1</text>
</g>
<!-- root&#45;&gt;1 -->
<g id="edge1" class="edge">
<path fill="none" stroke="#000000" d="M529.7039,-219.0816C497.2753,-206.1101 450.7515,-187.5006 419.7399,-175.096"/>
<polygon fill="#000000" stroke="#000000" points="420.8385,-171.7658 410.2538,-171.3015 418.2387,-178.2652 420.8385,-171.7658"/>
</g>
<!-- 2 -->
<g id="node18" class="node">
<ellipse fill="none" stroke="#000000" cx="459" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="459" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">2</text>
</g>
<!-- root&#45;&gt;2 -->
<g id="edge14" class="edge">
<path fill="none" stroke="#000000" d="M541.9512,-217.3008C525.3954,-206.2636 503.6849,-191.7899 486.6276,-180.4184"/>
<polygon fill="#000000" stroke="#000000" points="488.4458,-177.4241 478.1838,-174.7892 484.5628,-183.2484 488.4458,-177.4241"/>
</g>
<!-- 3 -->
<g id="node19" class="node">
<ellipse fill="none" stroke="#000000" cx="531" cy="-162" rx="27" ry="18"/>
<text text-anchor="middle" x="531" y="-157.8" font-family="Roboto" font-size="14.00" fill="#000000">3</text>
</g>
<!-- root&#45;&gt;3 -->
<g id="edge15" class="edge">
<path fill="none" stroke="#000000" d="M557.9157,-215.8314C553.7726,-207.5451 548.7863,-197.5727 544.2374,-188.4748"/>
<polygon fill="#000000" stroke="#000000" points="547.3115,-186.7967 539.7089,-179.4177 541.0505,-189.9273 547.3115,-186.7967"/>
</g>
<!-- 1&#45;&gt;14 -->
<g id="edge11" class="edge">
<path fill="none" stroke="#000000" d="M395.7146,-144.5708C399.9597,-136.0807 405.1536,-125.6929 409.8663,-116.2674"/>
<polygon fill="#000000" stroke="#000000" points="413.024,-117.7782 414.3657,-107.2687 406.763,-114.6477 413.024,-117.7782"/>
</g>
<!-- 1&#45;&gt;15 -->
<g id="edge12" class="edge">
<path fill="none" stroke="#000000" d="M406.3082,-149.1278C423.3555,-137.763 448.4019,-121.0654 467.5344,-108.3104"/>
<polygon fill="#000000" stroke="#000000" points="469.4799,-111.2199 475.8589,-102.7607 465.5969,-105.3956 469.4799,-111.2199"/>
</g>
<!-- 1&#45;&gt;16 -->
<g id="edge13" class="edge">
<path fill="none" stroke="#000000" d="M410.1634,-152.7347C441.6687,-140.1325 498.2073,-117.5171 534.1018,-103.1593"/>
<polygon fill="#000000" stroke="#000000" points="535.6556,-106.3075 543.6404,-99.3438 533.0558,-99.8081 535.6556,-106.3075"/>
</g>
<!-- 11 -->
<g id="node15" class="node">
<ellipse fill="none" stroke="#000000" cx="207" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="207" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">11</text>
</g>
<!-- 1&#45;&gt;11 -->
<g id="edge2" class="edge">
<path fill="none" stroke="#000000" d="M363.8366,-152.7347C332.3313,-140.1325 275.7927,-117.5171 239.8982,-103.1593"/>
<polygon fill="#000000" stroke="#000000" points="240.9442,-99.8081 230.3596,-99.3438 238.3444,-106.3075 240.9442,-99.8081"/>
</g>
<!-- 12 -->
<g id="node16" class="node">
<ellipse fill="none" stroke="#000000" cx="279" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="279" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">12</text>
</g>
<!-- 1&#45;&gt;12 -->
<g id="edge9" class="edge">
<path fill="none" stroke="#000000" d="M367.6918,-149.1278C350.6445,-137.763 325.5981,-121.0654 306.4656,-108.3104"/>
<polygon fill="#000000" stroke="#000000" points="308.4031,-105.3956 298.1411,-102.7607 304.5201,-111.2199 308.4031,-105.3956"/>
</g>
<!-- 13 -->
<g id="node17" class="node">
<ellipse fill="none" stroke="#000000" cx="351" cy="-90" rx="27" ry="18"/>
<text text-anchor="middle" x="351" y="-85.8" font-family="Roboto" font-size="14.00" fill="#000000">13</text>
</g>
<!-- 1&#45;&gt;13 -->
<g id="edge10" class="edge">
<path fill="none" stroke="#000000" d="M378.2854,-144.5708C374.0403,-136.0807 368.8464,-125.6929 364.1337,-116.2674"/>
<polygon fill="#000000" stroke="#000000" points="367.237,-114.6477 359.6343,-107.2687 360.976,-117.7782 367.237,-114.6477"/>
</g>
<!-- 1&#45;&gt;2 -->
<!-- 11&#45;&gt;111 -->
<g id="edge3" class="edge">
<path fill="none" stroke="#000000" d="M183.8366,-80.7347C152.3313,-68.1325 95.7927,-45.5171 59.8982,-31.1593"/>
<polygon fill="#000000" stroke="#000000" points="60.9442,-27.8081 50.3596,-27.3438 58.3444,-34.3075 60.9442,-27.8081"/>
</g>
<!-- 11&#45;&gt;112 -->
<g id="edge4" class="edge">
<path fill="none" stroke="#000000" d="M187.6918,-77.1278C170.6445,-65.763 145.5981,-49.0654 126.4656,-36.3104"/>
<polygon fill="#000000" stroke="#000000" points="128.4031,-33.3956 118.1411,-30.7607 124.5201,-39.2199 128.4031,-33.3956"/>
</g>
<!-- 11&#45;&gt;114 -->
<g id="edge6" class="edge">
<path fill="none" stroke="#000000" d="M215.7146,-72.5708C219.9597,-64.0807 225.1536,-53.6929 229.8663,-44.2674"/>
<polygon fill="#000000" stroke="#000000" points="233.024,-45.7782 234.3657,-35.2687 226.763,-42.6477 233.024,-45.7782"/>
</g>
<!-- 11&#45;&gt;115 -->
<g id="edge7" class="edge">
<path fill="none" stroke="#000000" d="M226.3082,-77.1278C243.3555,-65.763 268.4019,-49.0654 287.5344,-36.3104"/>
<polygon fill="#000000" stroke="#000000" points="289.4799,-39.2199 295.8589,-30.7607 285.5969,-33.3956 289.4799,-39.2199"/>
</g>
<!-- 11&#45;&gt;116 -->
<g id="edge8" class="edge">
<path fill="none" stroke="#000000" d="M230.1634,-80.7347C261.6687,-68.1325 318.2073,-45.5171 354.1018,-31.1593"/>
<polygon fill="#000000" stroke="#000000" points="355.6556,-34.3075 363.6404,-27.3438 353.0558,-27.8081 355.6556,-34.3075"/>
</g>
<!-- 11&#45;&gt;113 -->
<g id="edge5" class="edge">
<path fill="none" stroke="#000000" d="M198.2854,-72.5708C194.0403,-64.0807 188.8464,-53.6929 184.1337,-44.2674"/>
<polygon fill="#000000" stroke="#000000" points="187.237,-42.6477 179.6343,-35.2687 180.976,-45.7782 187.237,-42.6477"/>
</g>
<!-- 11&#45;&gt;12 -->
<!-- 12&#45;&gt;13 -->
<!-- 13&#45;&gt;14 -->
<!-- 2&#45;&gt;3 -->
<!-- 3&#45;&gt;4 -->
</g>
</svg>

Recursive backtracking algorithms (and exhaustive search in general) can be used to solve many problems in **combinatorial optimization** given certain constraints, such as:

- Determine whether a solution exists.
- Find a solution.
- Find the best solution.
- Count the number of solutions.
- Find all solutions.

`rollDice` and `sumDice` are two examples of finding all solutions by printing them out to the console. There are two common variations on this problem.

Returning a collection rather than printing to console
: To make the output easier for client programmers to process, real-world algorithms will collect results in a container such as a list.
  1. Introduce a public/private pair to carry the collection type as a parameter.
  1. In the public method, call the private helper method passing in a new collection.
  1. In each recursive call, pass on a reference to the collection as an argument.
  1. In each base case, instead of printing to the console, add the solution to the collection.

Choosing without replacement (bounded optimization)
: For dice rolling, we can repeatedly re-roll a 1. But problems that give a list of values as input might not allow reuse of values in a single solution, e.g. finding all subsets of a list.
  1. Introduce a public/private pair with a parameter representing elements unexamined by the current recursive branch.
  1. In the public method, call the private helper method passing in the complete collection.
  1. In the **choose** step, also remove the element from the collection.
  1. In the **explore** step, also pass on a reference to the collection as an argument.
  1. In the **unchoose** step, also add the element back to the collection.
