# DisjointSet

[![Build Status](https://ci.appveyor.com/api/projects/status/github/byhill/DisjointSet.jl?svg=true)](https://ci.appveyor.com/project/byhill/DisjointSet-jl)

An implementation of the Disjoint-set data structure for Julia.
This package is based on JuliaCollections's implementation of the Disjoint-set data structure in
[DataStructures.jl](https://github.com/JuliaCollections/DataStructures.jl).
However, this package uses union-by-size rather than union-by-rank,
which allows one to find the size of any given set in near-constant time.

## Usage

```julia
s = IntDisjointSets(10)  # creates a forest comprised of 10 singletons
union!(s, 3, 5)          # merges the sets that contain 3 and 5 into one and returns the root of the new set
root_union!(s, x, y)     # merges the sets that have root x and y into one and returns the root of the new set
                         # (assumes x != y)
find_root!(s, 3)         # finds the root element of the subset that contains 3
in_same_set(s, x, y)     # determines whether x and y are in the same set
num_sets(s)              # returns the number of sets in s
set_size(s, x)           # find the size of the set that x is in
elem = push!(s)          # adds a single element in a new set; returns the new element
                         # (this operation is often called MakeSet)
```

One may also use other element types:

```julia
a = DisjointSets{AbstractString}(["a", "b", "c", "d"])
union!(a, "a", "b")
in_same_set(a, "c", "d")
push!(a, "f")
```
etc...
