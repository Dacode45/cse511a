# Review

## search: states, actions, costs
  - perfect knowledge of dynamics
  - seek plan (sequence of actions)
  - from some start state -> goal state

## Algorithms: uniformed search: BFS, DFS
## Algorithms: informed search: A*, greedy.
  Using heuristics.
*heuristics requirements*
__admissibility__: h <= true cost
A* tree search is guaranteed **optimal** if heruistic is admissible
__consistency__: function that estimates the distance of a given state to a goal state, and that is always as most equal to the estimated distance from any neighboring vertex plus the step cost of reaching that neighbor.
*stronger than admissible*
h(p) <= h(n) + stepcost(p,n)

## Game playing. Adverserial.
- minimax (chess)
- expectimax (randomness)

## Markov decision processes (MDR)
**Bellman Equation**
Mathematical way to write expectimax

V(s): value of a state or expected utility achieved after entering state s under optimized pay.

T(s,a,s') probability of getting to state s' given action a at state s

V*(s) = choose the best action of the weighted average of states that action could take you.
      = max(sum_s'(T(s,a,s')[R(s, a, s') + gamma* V*(s')]))
Where gamma is the discount because you prefer rewards now vs those in the future.

### Policy iteration for policy (pi)
V(pi)(s) = fixed policy. don't take max
        = sum_s'(T(s,pi(s),s')[Reward(s,pi(s), s') + gamma*V(pi)(s')])

## Policy evaluation vs Policy extraction
*evaluation*: Run several times given a policy, retoactively assign utility of states
*extraction*: Create a new policy.
