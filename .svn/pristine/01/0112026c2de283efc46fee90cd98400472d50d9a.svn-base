# Conditional independence

P(x,y | z) = P(x|z)P(y|z)
or
P(x | z, y) = P(x|z)

Proof
P(x|z,y) = P(x,y,z)/P(y,z)
        = P(z) * P(x,y|z) / P(y, z)
        = P(z) * P(x|z) * P(y|z) / (P(z) * P(y|z))
        = P(x|z)

## Chain Rule
P(X1,X2,X3, ...) = P(X1)P(X2|X1)P(X3|X1,X2)...
n factorial ways to order.

Ex
P(Traffic, Rain, Umbrella) =
  P(Rain)P(Traffic|Rain)P(Umbrella|Rain, Traffic)

With assumption of conditional independence:
= P(Rain)P(Traffic|Rain)P(Umbrella|Rain)

### Ghost Busters Chain Rule
T: Top square is red
B: Bottom square is red
G: Ghost is in the top

P(+g) = .5
P(-g) = .5
P(+t|+g) = .8
P(-t|-g) = .4
P(-b|+g) = .8
P(+b|-g) = .4

P(G,B,T) = P(G) * P(T|G) * P (B | G, T)
          = P(G) * P(T|G) * P (B | G)

# Bayes Nets
**Nodes** Random Variables. Assigned(observed) or unassigned(unobserved)

**Arcs** Interactions. Similar to CSP constraints. Indicate "direct influence" between variables. Formally  encode conditional independence.

**Conditional Distribution for Each Node**
P(X|a1...an)

## Probabilities
Bayes' nets implicitly encode joint distributions.
- As a product of local conditional distributions
- To see what probability a BN gives to full assignment, multiply all relevant conditionals together.

P(x1,x2,x...) = Cartesian_Sum(P(xi|parents(xi)))
This distrubution assumes conditional independences:
P(xi|x1..xn) = P(xi|parents(xi))

### Causual Chains
X->Y->Z

is X independent of Z given Y?

Prove
P(z|x,y) = P(x,y,z)/P(x,y) = P(z|y)
        = P(x)P(y|x)P(z|y)/P(x)P(y|x)
        = P(z|y)

### Common Cause
X<-Y->Z
P(x,y,z) = P(y)P(x|y)P(z|y)

Guarenteed X independent of Z? NO

Guarenteed X and Z independent given Y

Proof
P(z|x,y) = P(x,y,z)/P(x,y) = P(z|y)
        = P(y)P(x|y)P(z|y)/P(y)P(x|y)
        = P(z|y)

### Common Effect
X->Z<-Y

Are X and Y independent? Yes!
P(X,Y,Z) = P(X)P(Y)P(Z|X,Y)

sum over z (P(X,Y,Z)) = sum over z (P(X)P(Y)P(Z|X,Y))
                      = P(X)P(Y) * 1

Are X and Y independent given Z? No

Seeing Z puts X and Z in competition of Explanation.
