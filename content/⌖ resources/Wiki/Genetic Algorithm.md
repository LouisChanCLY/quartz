---
tag: todo
date: 2022-07-19
github: https://github.com/DEAP/deap
---

## Metadata
- Association:
- Domain: [[Domain Root - Data Science]]

## Genetic Algorithm

Inspired by [[Charles Darwin]]’s [[Theory of Evolution]], the Genetic Algorithm is an iterative process for search the global optimal solution to a problem statement. To better understand how a genetic algorithm works, here is a short crash course of the key concepts:

-   **Gene:** This refers to a parameter/variable of the solution. It is quite usual for a gene to be represented as a bit (i.e. 0 or 1), but that can be changed based on the underlying problem statement.
-   **Individual / Chromosome:** A string of genes that represents a solution.
-   **Population:** One generation of individuals.
-   **[[Fitness Function]]:** A function for calculating how successful (**Fitness Score**) an individual is. Depending on the underlying problem statement, we can search for individuals with the highest fitness score or the lowest. To embrace the concept of survival of the fittest, the better the fitness score, the higher the chance that an individual can survive and reproduce to form the next generation.
-   **[[Selection Strategy]]:** This defines how we compare individuals against each other for selection the seeds for the next generation. Some common examples are [**[[Tournament Selection Strategy]]**](https://en.wikipedia.org/wiki/Tournament_selection) (a random sample of individuals face each other 1 v 1, and the winner wins a place in the next generation), [**[[Roulette Proportionate Selection Strategy]]**](https://en.wikipedia.org/wiki/Fitness_proportionate_selection) (probability be chosen is proportional to the fitness score), or **double tournaments** for more complex scenarios
-   **[[Crossover Strategy]]:** This is essentially how parent genes are passed to offspring when reproducing. Crossover is supposed to mimic sexual reproduction, where two parents are needed for reproducing. Genes of the parents will then be recombined to form offspring. Although different strategies are depending on scenario and data types, the most common two are [[K-Point Crossover]] and [[Uniform Crossover]] In the [[K-Point Crossover]], k _crossover point(s)_ will be selected randomly, where the genes to the right of a point are swapped. [[Uniform Crossover]] is relatively more straightforward: instead of having sections of genes swapped, every gene will have the same chance to be swapped.
![[Pasted image 20220719222606.png]]
![[Pasted image 20220719222614.png]]
-   **[[Mutation Strategy]]:** As a way to maintain gene diversity and prevent premature convergence, genes of the children will have a random chance of mutating, meaning that the actual value will deviate from that of the parents. Mutation usually comes in the form of [**[[Bit-Flipping Mutation Strategy]]**](https://deap.readthedocs.io/en/master/api/tools.html#deap.tools.mutFlipBit), [**[[Index-Shuffling Mutation Strategy]]**](https://deap.readthedocs.io/en/master/api/tools.html#deap.tools.mutShuffleIndexes), or **[[Bounded Mutation Strategy]]** and **[[Unbounded Mutation Strategy]]**.

## Flow of Genetic Algorithm

These key concepts will then be combined to form an iterative algorithm:

1.  Parameterise the problem statement
2.  Define a [[Fitness Function]]
3.  Define a [[Crossover Strategy]], a [[Mutation Strategy]], and a [[Selection Strategy]]
4.  Generate initial population
5.  Evaluate the fitness of the individuals of the population
6.  Select the individuals, crossover and mutate to form the next generation of population
7.  Repeat step 5, and 6 until convergence or until end conditions are met

## Github Library
- [DEAP](https://github.com/DEAP/deap)