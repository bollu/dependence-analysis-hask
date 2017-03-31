# Dependence Analysis of Haskell programs

The aim is to try and use Haskell's strong type system to encode
dependence information. This will hopefully allow for parallelsiation, of at
least the strict subset of Haskell, if not the entire langugage.


### Applications

- General Haskell programs without modification can be parallelised. This is unlike Data Parallel Haskell, which requires the use of custom, strict, finite lists, etc.

- Check if the techniques are useful in other problem domains. Eg: Tobias Grosser
mentioned that the same techniques might help with FFT computations

### Current Idea

- Integer polyhedral capture the "context" of loops with quasi affine
bounds. This representation allows us to perform dependence analysis.

- Similarly, we need a "context" for data structres in functional languages.

- Trying to use the "one hole context" to represent the current location
in a data structure.

- Represent functions that de-structure data as maps between contexts

### References

- Analytic combinatorics
- [Differentiating data structures](http://www.cs.nott.ac.uk/~psztxa/publ/jpartial.pdf)
- [Derivative of regular type is Type of one-hole context](http://strictlypositive.org/diff.pdf)

