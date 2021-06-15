# Ant_Colony_Optimization_TSP


### Performance of the population over iterations
This is the graph of populations average performance over iterations;
The performance is not stable during iterations


![image](https://user-images.githubusercontent.com/41572446/122047889-f0b9aa00-cde0-11eb-9008-3bd49bafa4b2.png)


This is the graph of populations best individual’s performance over iterations;
The performance is not stable during iterations

![image](https://user-images.githubusercontent.com/41572446/122047938-fe6f2f80-cde0-11eb-8131-55cccf6828b7.png)



### Important Operations of the Algorithm

Genetic algorithm mimics the natural process of evolution. In order to represent it, code uses a population and tries to find solution over generations by using natural biologic phenomena such as;

*  **Creation of the Population**
> A population created in order to calculate different possible solutions in one iteration. Since new road selected regardless of the next roads in the vector, there is no need to create random individuals since all individuals will move randomly in first iteration.

*  **Fitness function**
> Fitness function has an essential important for the algorithm since it defines if an individual is successful or not. Fitness is calculated according to distance traveled by individual

*  **Heuristic table**
> Heuristic table contains the information of distance between cities and each ant decides whether go in a way or not by some weights obtained by this table. This table is static and does not change during iterations

*  **Pheromone table**
> Pheromone tab contains the pheromone valuesbetween cities and every values is same when it started first. During iterations, ants updates this pheromones if they chose this path and the table also updated after iteration according to ants fitness value.

*  **Choosing path**
> This is one of the most important operation of the algorithm since individual decides which way to go in this operation. Here ant finds available cities and checks both their heuristic and pheromone values. This values weighted by alpha and beta values by powering the table values. After calculation of the each routes desirability, ant selects a path with weighted randomness according to calculated path desires.

*  **Updating pheromone table**
> This table is updated during iteration and after iteration. During iteration, if ant choses this pathit puts some pheromone. After iteration, every ant puts extra pheromone on their way during iteration with reversed ratio of their fitness value. If an ants fitness is smaller than its pheromone is bigger than others.Also during this phase, there is an evaporation operation in order to prevent extra pheromone accumulation and forget bad fitness




### Comparison of Results

Thefinalresultsare nearly the same with genetic algorithm but there is a huge fluctuation in ant colony optimization besides genetic algorithm is more stable. Also ant colony optimization is more tended to converge local minimum and it makes hared to find global minimum. Even the randomness in ACO seems higher it is actually hard to escape from a local minimum since there is pheromone accumulation. The performance of GA is better than ACO in terms of consistency and speed. ACO is inconsistent to keep best individuals to the next iteration while GA is pretty good in that by depending selection technique. Also,GA runs faster and tries more solution in a unit time which makes it more efficient for this specific problem.
