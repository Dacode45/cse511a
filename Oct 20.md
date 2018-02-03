# Probability Review

Define __random variable__ *(RV)* as some aspect of the world with uncertainty.
Define __domain__ *(D)* as the set of values a random variable can assume.
Define __probability distribution__ as an assignment of probability value to the domain.
Define __Event__ *(E)* as the subset of valid assignments to a set of RV
  Pr(E) is the sum of the probability of all assignments in the event

## Conditional Probability:
Pr(X|Y) = P(X,Y)/P(Y)

## Chain Rule
Pr(X1,X2,X3) = Pr(X1)Pr(X2|X1)Pr(X3|X1,X2)
Pr(X) = the sum for all Y of Pr(X,Y)
      = the sum for all Y of Pr(Y)Pr(X|Y)

## Bayes Rule:
Pr(X,Y) = Pr(X)Pr(Y|X)
Pr(X|Y) = Pr(X)Pr(Y|X)/Pr(Y)
