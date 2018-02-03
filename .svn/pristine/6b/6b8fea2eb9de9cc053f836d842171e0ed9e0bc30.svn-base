# Constraint Satisfaction problems.

## What is Search for?
Planning a sequence of actions from start state to some Global

### Identification: assignment to variables.
- The goal itself is important, not the path
- All paths at the same depth/length (for some formulations)

## CSPs

- Standard Search problems
  1. State is a "black box": arbitrary data structure
  2. Goal test can be any function over states
  3. Successor function can also be anything

- Constraint Satisfaction problems
  1. A special subset
  2. State is defined by variables Xi with values from domain D
  3. Goal test is set of constraints spsecifiying allowable combinations of values
    for subsets of variables

## Examples

1. Map Coloring
  Problem:
    Variables: WA, NT, Q, NSW, V, SA, T // regions of Australia
    Domains: D = { red, green, blue }
  Constraints: adjacent rejions must have different colors
    implicit: WA =/= NT
    Explicit: (WA, NT) is subset of {(red,green),(red,blue),...}
  Solutions are asignments satisfying all constraints, e.g.:
  {WA=red, NT=green, Q=red, NSW=green ...}

2. N-Queens problem
  Problem:
    Variables: Qk //k is the row, Q is column
    Domain: {1,2,3,...N}
  Constraints: Place 4 queens on a 4x4 board such that no two queens attack
    each other
    Implicit Forall i,j non-threathening(Qi, Qj)
    Explicit: (Q1, Q2) contained in {(1,3),(1,3),...}

3. Example: The Waltz Algorithm
  Problem:
    Intepreting line drawings of solid polyhedra as 3D objects
    An early example of an AI computation posed as a CSPs

    Each intersection is a variable.
    Adjacent intersections impose constraints on each other
    Solutions: physically realizable 3D interpretations
