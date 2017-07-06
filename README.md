# Dependence Analysis of Haskell programs

The aim is to try and use Haskell's strong type system to encode
dependence information. This will hopefully allow for parallelsiation, of at
least the strict subset of Haskell, if not the entire langugage. Ideally, such a transformation should
yield a representation that can be represented as an affine space: That way, we can reuse the
machinery developed by the [polyhedral compilation community](http://polyhedral.info/) to optimise
programs.


### Applications

- General Haskell programs without modification can be parallelised. This is unlike Data Parallel Haskell, which requires the use of custom, strict, finite lists, etc.

- Check if the techniques are useful in other problem domains. Eg: Tobias Grosser
mentioned that the same techniques might help with FFT computations

### Follow up on - Polyhedral signal processing
- Arrp: A Functional Language with Multi-dimensional Signals and Recurrence Equations.
- Contains information about using polyhedral to model infinite signals.
- Should have ideas.
### Current Idea - Copatterns
- Allows one to analyze infinite data types as "experiements"
- Interesting viewpoint, perhaps we can rewrite polyhedral descriptions
  in terms of copatterns


### Current Idea - Runtime Polyhedra

- Clearly, we cannot generate affine maps for things by look-ahead. Eg. trees
- However, we _can_ keep polyhedral info attached to objects in the **runtime**.
- Runtime can understand parallelism and try to extract parallelism.


### Current Idea - Fix, Recursion schemes

- any function `f` that applies to a constructor is trivially parallelisable across
  constructor arguments.
- any non-recursive function `f` can similarly be analysed immediately, given the `LHS` and the `RHS`.

- This is because the only thing a pure function can do is destructure on the `LHS` and build up
  structures using constructors / primops on the `RHS`
  
- Only problem is recursive functions.

- Force language such that recursive functions can only be return as recursion schemes, and
  recursive structures can only be written using `Fix`.
  
- This enables us to "study" the recursion separately from the data.

- Can build up polyhedra corresponding to any ADT.

- Need to see what happens to recursion schemes. `[TODO]`

### Old Idea (One Hole Context)

- Integer polyhedral capture the "context" of loops with quasi affine
bounds. This representation allows us to perform dependence analysis.

- Similarly, we need a "context" for data structres in functional languages.

- Trying to use the "one hole context" to represent the current location
in a data structure.

- Represent functions that de-structure data as maps between contexts


- `Foldable` is derivable for any ADT. Can use `Fodable ~= toList ~= N` to
generate index expressions over `N`. However, these will be non-polynomial
in the general case.

- Tobias suggested trying to generate code for affine expressions first by
using the `N` bijection. That way, we understand how to *code generate* from
haskell programs.

### References

- Analytic combinatorics
- [Differentiating data structures](http://www.cs.nott.ac.uk/~psztxa/publ/jpartial.pdf)
- [Derivative of regular type is Type of one-hole context](http://strictlypositive.org/diff.pdf)
- [Copatterns](http://www2.tcs.ifi.lmu.de/~abel/popl13.pdf)

