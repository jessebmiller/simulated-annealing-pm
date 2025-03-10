# simulated-annealing-pm
A decentralized product manager following a simulated annealing algorithm

How do we keep all the wild ideas on the table while also coordinating a decentralized organization to find valuable progress? How do we identify the right product for a decentralized product organization to work on and fund? How do we make the decisions about what direction to take throughout the process?

## Simulated Annealing
As an efficient probabilistic technique for solving hard optimization problems, simulated annealing (SA) has the potential to be the answer. 

Here is the algorithm and how it might be used for managing software product development

"""
At each step, the simulated annealing heuristic considers some neighboring state s* of the current state s, and probabilistically decides between moving the system to state s* or staying in-state s. These probabilities ultimately lead the system to move to states of lower energy. Typically this step is repeated until the system reaches a state that is good enough for the application, or until a given computation budget has been exhausted.

- Wikipedia, Simulated Annealing
"""

Some initial budget would be put into a contract that would use the following algorithm to incentivise work and exploration of the solution space, with rewards for contributing iterations on a set of previous states. It would evaluate whether the current state or some other state should be used as the base for more increments on each iteration, eagerly trying lots of ideas early in the process but becoming more conservative sticking with better ideas as the schedule progresses and the budget runs out.

Given: 
States s are products in their current state of development
Kmax is the max number of steps available in the development budget
temperature(x) = 1-x
“Lower energy” represents higher expected value to the participants
Neighbors are iterations of s, submitted by developers, following a preset development process
 P is a function that determines the likelihood of switching to the new state, given the expected values or E(snew), and the current state, E(s), and the current temperature of the system T such that When T tends to zero, P must tend to zero if E(snew)>E(s) and to a positive value otherwise

Let s = s0
For k = 0 through kmax (exclusive):
T ← temperature( (k+1)/kmax )
Pick a random neighbor, snew ← neighbor(s)
If P(E(s), E(snew), T) ≥ random(0, 1):
s ← snew
Output: the final state s

The Expected Value Oracle (E)
Some method (to be experimented with and further evaluated) to determine the expected value of the various states the system could move to. Options might include.
A designated individual product manager or owner who independently makes the determination
A voting scheme, perhaps:
Weighted by contribution to initial budget
Weighted by some contribution based reputation system like Sourcecred
Some curved bond scheme that shares value with bond holders when the contributor of the state gets paid.
This could be a way to continue to fund projects as long as they continue to show promise 
Sufficiently Near Neighbors
A project would be created with a definition of neighbors by providing a product development process that defines a tree or directed acyclic graph (DAG) structure. For example: Brainstormed ideas -> Sketch -> Mockup -> Prototype -> Production Product. Perhaps allowing nodes to be children from any node at higher levels.

Near neighbors would be defined as both sibling, child, and parent nodes, perhaps probabilistically allowing more than one hop.
Example
A grantmaker, Gina, decides to fund a software platform for “decentralized zero interest, zero collections, local small business loans”. She has a few vague ideas about how that might work but nothing she is very confident in. She creates a SA project using the dapp, selecting a project process (Brainstorm ideas -> Mockup -> Prototype -> Production Product), a cooling schedule (Two weeks per iteration) and grants the project 50,000 DAI. She designates a 5,000 DAI budget per iteration. She decides to use the default P(e, e’, T) function defined as 1 when e>e’ and T otherwise. She sets a date for the first iteration to start a few weeks in the future.

Before the start date she gets feedback on the prompt and may make changes for clarity or any other reason.

Before the first iteration, the system calculates kmax and in this case there is enough budget for 10 iterations so kmax=10 then sets s0 to some default with zero value like “don’t do anything”.

s = s0
k = 0
First iteration

There is a 2 week period for contributors (Alice, Bob, and Carol) to submit neighbors to any existing state. Alice, Bob, and Carol each submit 3 or 4 brainstormed ideas relating to s0 and Gina submits expected value estimates for each. Carol also submits a mockup combining two of the ideas as well, she sets it as a child of both ideas then Gina submits an expected value for the mockup. Sam submits some spam ideas and mockups that Gina marks as spam and removes from the system.

At the end of the two weeks, the system executes the calculations and transitions to the next iteration.

T = 0.9 = 1 - ((k + 1)/kmax)
snew = neighbor(s)
If P(E(s), E(snew), T) ≥ random(0, 1)
s = snew
k = k+1

In this case no matter which snew was chosen the system will move to it because the expected value of s0 is zero, and P is 1 when the new state it’s evaluating is greater than the current state.

Some scheme is used to decide how much of the iteration budget is paid out to which contributors, a naive scheme is to pay the contributor who’s state was chosen by the algorithm, though some sharing scheme is more interesting. Perhaps some portion of the iteration budget is reserved for the state the system moves to, and the rest is distributed to the others weighted by their expected value. Some of the budget could also be awarded to the parents of any (and some of that to the parent’s parents and so on)

Iterations for k 1-9 are executed as above, 2 weeks each.
