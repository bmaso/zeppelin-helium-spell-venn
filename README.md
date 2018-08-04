# zeppelin-helium-spell-venn

Apache Zeppelin plugin DSL to describe Venn diagrams. This "spell" (a.k.a. parser) translates
a simple description of sets into a table that the `zeppelin-helium-d3-venn` visualization
will render as a Venn diagram.

The grammar is pretty simple: one per line, describe the size of a set of an intersection of sets.
The Venn visualization will do the heavy work of figuring out cirles and their relative positioning
and overlap.

## Simple Example

```
%zeppelin-helium-spell-venn
A: 50
B: 25
A intersect B: 10
C: 60
A i C: 30
B ∩ C: 5
A i B ∩ C: 3
```

Note that there's three different ways to represent "intersection" in this DSL:
* "intersect" as in `A intersect B: 10`
* "i" as in `A i B: 10`
* "∩" as in `A ∩ B: 10`

The numbers are unitless and describe relative set size.

Note that the Venn visualization assumes unlisted sets (including intersection sets) are size 0.

## Translation to Table Data

The equivalent table has two columns: *name* and *size*. *name* can be any label, with the caveat that "i"/"intersect"/"∩"
are interpreted specially as described above. For example, the equivalent table to the example Venn diagram text above would be:

```
%table
name\tsize
A\t50
B\t25
A intersect B\t10
C\t60
A i C\t30
B ∩ C\t5
A i B ∩ C\t3
```
