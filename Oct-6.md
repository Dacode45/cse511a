#Reinforcement Learning

**Big Idea #1** to estimate an expected value E(x)[f(x)] = Sum(x)Pr(X=x)f(x)
wit samples : draw x..xN from probability distribution Pr(x) then
Q is appox equal to 1/N * sum f(x) __the weighted average of f(x)__

Example?

T(s, a, s') = Pr(s' | a,s) // The transition function is the probability of s' given action at state

**Big Idea #2** keep playing the game maintain running average

enter Q-state(s,a)
- have a guess for Q(s,a)
- observe sample
  r + gamma*max(Q(s',a'))
- update guess with both sources of information.

Q(s, a) <- (1-alpha)Q(s,a') + alpha[r + gamma*Q(s',a')] where alpha is the learning rate
