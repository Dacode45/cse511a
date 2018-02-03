# General Tree Search

## Depth First Search

Uses a stack
Ex:
```javascript
function dfs(node) {
  search(node)
  node.children.forEach(dfs)
}
```

## Breath First Search

Uses a queue
Ex:
```javascript
function bfs() {
  // initialize all nodes to an infinite cost
  queue = new Queue(costFunc)
  queue.Add(root)
  for current = queue.Pop(); current; current = queue.Pop() {
    search(current)    
    current.children.forEach( child =>{
      queue.Add(child)
    })
  }
}
```

## Uniform Cost Search (aka Djikstra)

Expand a cheapest cost node first.
*Use a Priority Queue (aka Heap)*

Ex:
```javascript
function ucs(rootnode) {
  // initialize all nodes to an infinite cost
  queue = new PriorityQueue(costFunc)
  queue.Add(root)
  root.cost = 0; // cost is new
  for current = queue.Pop(); current; current = queue.Pop() {
    search(current)

    current.children.forEach( child =>{
      child.cost = Math.Min(current.cost + cost(current, child), child.cost)
      queue.Add(child)
    })
  }
}
```

### Problems
- Explores options in every direction if they are cheap.
- No information about goal location
- Think about circular search radius.
- *Essentially adds every single square to the fringe*

## Informed Search

### Summary

#### Informed Search
- Heuristics
- Greedy Search
- A* Search

#### Graph Search (refinement of Tree Search Algo)

### Recap: Search

#### Search problem:
Encodes *Actions*, *States*, *Cost*, *Successor Function*, *Start state and goal*

#### Search Tree:
- Nodes represent plans.


### The One Queue
All these search algorithms are the same except for finge strategies.
- Conceptually, all firnges are priority queues.
- Practically you can avoid the log(n) overhead from actual priority queue by
using stacks.

### Search Heuristics.
`h(state) = c`
function that estimates how close a state is to a goal.
Designed for a particular search problem

#### Euclidean distance.
For pacman to get to the food, he must walk at least the distances from him to
the pellet

#### Manhattan distance (slightly better).
The number of squares pacman must walk vertically and horizontally to get there.

### Greedy Search
- Expand the node that seems closest (based on heuristic)
- heuristic is known as _forward-cost_
In traveling problem, go from city to city where you visit the city closest to
the destination.
- *May end up going in circles around the thing.*

### A* Search (best of UCS and Greedy)
use f(n) = g(n) + h(n) _backward vs forward cost_
*h(n) can screw up the cost function*

# September 8th

#### Proof of Optimality fo A* search
| ---- | ------|
| ucs  | `g(n)` "backwards cost S->q" Used |
|greedy | `h(n)` forward cost n-> G is closest to goal |
|A*   | `f(n) = g(n) + h(n)`, estimate of total cost |

We define `admissible heuristic` h(n) <= g(n -> G) where h(n) is true cost to get to G

Proof:
1. Imagine B is on the fringe
2. Some ancestor n of A is on the fringe, (maybe A)
3. Must Prove n will be expended before B.

1. f(n) is less or equal to f(A)
  f(A) = g(A) + h(A) // Because A is a goal, h(A) = 0
  f(A) = g(A)
  // Since the total cost to get to B is higher than A
  f(A) < f(B)
  // Since B is also a goal
  f(b) = g(B) + h(B) or
  f(A) < f(B)
  f(n) <= f(A) < f(B)

  f(A) = g(A)
       = g(n) + g(n -> A)
       =>= g(n) + h(n)
       = f(n)

### Creating admissible Heuristics
- Most of the work in solving hard search problems optimally is in coming up with admisible Heuristics
- Often, admissible heuritics are solutions to relaxted problems with new actions.
Pacman:
  Manhattan distance: Relaxed problem is assuming walls aren't in the way.

#### Tile Matching Puzzle
Design Heuristics.
- Relaxed Problem: (Pick up and place tiles)
  Heuristic = Number of tiles misplaced
- Relaxed Problem: (Tiles Slide over each other)
  Heuristic = total Manhattan distance of all tiles.

#### Trivial Heuristics, Dominance
- Dominance: h-a >= h-c if for every n h-a(n) >= h-c(n)
- Heuristics form a semi-latice. (combine them all together)
 h(n) = max(h-a(n), h-b(n)) // Always dominantes

# Graph Search
Idea: never expand a state twice
Implementation
- Tree search + set of expanded states("closed set")
