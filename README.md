Lab 3: Writing Specifications
====


An outcome of CPEN 221 is to help you develop software that is:
* **Safe from bugs:** Correct today and correct in the unknown future.
* **Easy to understand:** Communicating clearly with future programmers, including future you.
* **Ready for change:** Designed to accommodate change without rewriting.

### Specifications

Specifications help us achieve all three of our primary objectives in software design. The goal of this lab exercise is to give you more experience understanding, formulating, and evaluating method specifications.

This lab activity can contribute a grade maximum of 0.5% towards **MP1**.

### Formulating Specifications

**What are the elements of a good specification?**

* **For methods**: name, argument names and types, return type, exception types
* **Preconditions** (what the specification requires): require neither too little nor too much
* **Postconditions** (what the specification guarantees): frame conditions (what the specification guarantees about mutation), guarantee neither too little nor too much
* Declarative, not operational
* Unambiguous

### `splitString`

We would like to use the following `splitString` method to split some strings as follows:

```
splitString("alice,bob,chloe", ",") → [ "alice", "bob", "chloe" ]
splitString("Boston to London to Sochi", " to ") → [ "Boston", "London", "Sochi" ]
splitString("bandana", "nda") → [ "ba", "na" ]
```

The method header would look like this:
```
 // Split a string around instances of another string
public static String[] splitString(String text, String delim) {
    ...
}
```

With your partner:
* Choose preconditions (requires) and postconditions (effects) for this specification.
* Write the specification in Javadoc format.

### `splitString`, take 2

Here’s one attempt to write a splitString spec:

```
 /**
 * Split text into an array a = [ a_0, a_1, ..., a_k ] such that
 * a_0 + delim + a_1 + delim + ... + delim + a_k is equal to text.
 *
 * @param text String to be split
 * @param delim String to split on
 * @return array of substrings of text appearing between instances of delim
 */
public static String[] splitString(String text, String delim) {
    ...
}
```

* Alice says the postcondition of the method isn’t strong enough. Fix it so return `new String[] { text };` is no longer a valid implementation.
* Can we guarantee that no `a_i` contains `delim` as a substring?
* Bob wants to use this method, but he feels like the postcondition still isn’t strong enough. Can you help him out?

The specification must remain coherent.

### `splitString` and `splitString` and `splitString` …

Examine several alternatives for the specification of:

`public static String[] splitString(String text, String delim)`

In all of the postconditions below, the return value is an array a such that 

`a[0] + delim + a[1] + delim + ... + delim + a[a.length-1]` equals `text`.

#### Option A

* _requires_: `delim` is not empty 
* _effects_: returns `a`

#### Option B

* _requires_: `delim` is not empty 
* _effects_: returns `a` where none of `a[i]` contain substring `delim`

#### Option C

* _requires_: `text` contains `delim`, and `delim` is not empty 
* _effects_: returns `a` where none of `a[i]` contain substring `delim`

#### Option D
* _requires_: `delim` is not empty 
* _effects_: throws `NoSplitsException` if and only if `text` does not contain `delim`; otherwise, returns `a` where none of `a[i]` contain substring `delim`

### Stronger and Weaker

#### What is the relationship between A and B?
* A’s precondition is equal to B’s precondition.
* A’s postcondition is _ _ _ _ _ _ B’s postcondition.
* Therefore: A is _ _ _ _ _ _ B.

#### What is the relationship between C and the previous two specs?
* C’s precondition is _ _ _ _ _ _.
* C’s postcondition is _ _ _ _ _ _.
* Therefore?

### Exceptions

**What about D?**

* D’s postcondition requires different behavior – throwing an exception in some cases – than both A’s and B’s, with the same precondition. An implementation cannot satisfy both. Therefore… ?
* D’s postcondition is equal to C’s for inputs that satisfy C’s precondition. Therefore… ?

### Choosing and Refining Specifications

When writing specifications that others will rely on, you must also carefully consider the specifications you will rely on. For this part of the lab activity, you should read the provided source code.

With your partner, write a specification for each method in the provided skeleton code, based on what you think this method ought to do. Write the simplest specification you can, but include all the details someone would need to be completely confident about the specification for your method. As part of the spec, you’ll need to choose input and return types.

For word frequencies, consider using a `Map`. When you use `Map`, you specify the types of the keys and values using generics. So a dictionary that maps integers to Clowns is a `Map<Integer,Clown>`.

Look at the skeleton code for `MostCommonWord`.

When we write the specification for `mostCommonWord`:
* If the specifications for the other methods are given, that will change how difficult it might be to implement different specifications of `mostCommonWord`.
* If we are writing specifications for the other methods, we choose specifications that both make sense on their own and make `mostCommonWord` easier to specify, implement, read, and debug.

Why might we break `mostCommonWord` into `splitIntoWords`, `countOccurrences`, and `findMax`?

If we didn’t choose to break those steps into methods, our specification problems would not disappear – why not?

Review your specifications for each of the three methods (you may discuss with a few others groups in the lab). Then, given the sketched specification for `mostCommonWord`:
* **Complete the specification for `mostCommonWord`.**
* Revise and agree on specifications for all three helper methods.
* Sketch the code for `mostCommonWord` to verify that your specifications will work.

### Discussion
* How easy or difficult was it to agree on specifications for the helper methods?
* How much did you have to revise your specifications during the discussion?
* Are the specifications declarative, as opposed to operational?
* Are they designed to make sense on their own?
* Are they designed to make our code easier to implement, read, and debug?

### Submission

Answer the questions posed in this lab activity, create a PDF file with the answers and upload it to **Lab 3** on [Gradescope](https://gradescope.com). If you want any credit for the work, you should submit your answers by 6:00 p.m. on Oct/5/2015.