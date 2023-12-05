# Genetic-NQueen
An implementation of the N-Queen problem using genetic algorithms

### Chromosome Definition:
In order to solve any problem with a genetic algorithm we must first find an optimal way to show the answers to the problem as chromosomes.
As discussed in class, we define the chromosomes as a $1$-dimensional array of length n (assuming that the board is $n*n$). This is because we can be sure that when we want to place $n$ queens in an $n$ by $n$ table, since there can only and only be a single queen in each column (note that the count of the queens and the size of the table both match - $n$). As a result, we shall only have one metric for each column's queen: what row that queen is located in.
so we know what our chromosomes look like. now we should think about a fitness function.

### Fitness function:
As we also have discussed in class, we define the fitness function as the numbre of collisions a formation of queens have. meaning that if we put all the queens in a row, then the number of collisions will be $C(n, 2)$. However, we want to make the fitness give a higher score when the solution is more optimal, thus we invert the asnwers by substracting them from the +inf. we can also define +inf as the maximum score available in the problem (with some extra addition for good measure).
As a result, the fitness function will be:
$$fitness(chromosome) = maximumPossibleFitness - number Of Collisions (chromosome)$$

Thus, when simplified:
$$fitness(chromosome) = + (C(n, 2) + n) - row Collisions (chromosome) - column Collisions (chromosome) - diagonal Collisions (chromosome)$$

But, we also from the definition of chromosome we know that the column collisions are ZERO (since there is exactly one queen in each column). So the new formula will be:
$$fitness(chromosome) = (C(n, 2) + n) - row Collisions (chromosome) - diagonal Collisions (chromosome)$$

### Crossover:

In order to do crossover, we stick to the solution we found in the class. First choose 2 parents and give as an input, then choose a random position such as i, and make child by using the first untill i-th position of the first parent and i+1-th untill the end of the second parent.
This is one of the ways to do crossover between two arrays that might be permutations and since it's decent and it works for out problem.

### Mutation:
We should also define mutation. The easiest solution that comes to mind is to choose two queens and swap their columns (because the solution of the problem will be a chromosome which is a permutation of 0 to n-1). However, while we are searching for the answer, there is no guarantee that the current chromosome is a permutation. Thus we code the permutation to change a random queens position to a random position on its column.

## Inference:
Finally, we should now start initializing the population. In order to do so, we make a population of random permutations using random shuffle function available in python.

We should now define the steps we need to take in each generation (Or if you are familiar with ML terms, we should define what steps to take in each epoch). We use random selection of parents as it is good balance between exploitation and exploration, we then choose the 90-best chromosomes based on their fitness and fill the rest of the population from the losing chromosomes randomly.
In order to have a fair compromise between exploration and exploitaiton, I decided to set a variable mutation probablity to encourage muatations early on, and set it to be a constant 10% later on. However, still set a random 90% chance every 1000 steps to help avoid local extermums.
