# Music Festival Lineup Optimization

**Course:** Computational Intelligence for Optimization  
**Group J**  
**Authors:** Bárbara Capitão, Carolina Silvestre, Francisco Pontes, Lara Leandro

---

## Project Overview

This project focuses on optimizing the lineup of a music festival by scheduling 35 unique artists across 5 stages and 7 time slots. The objective is to maximize audience satisfaction by:

- Minimizing conflicts between artists with overlapping fan bases
- Promoting genre diversity throughout the schedule
- Maximizing overall artist popularity during the final (prime) time slot

This is framed as a combinatorial optimization problem, approached using an evolutionary algorithm.

---

## Solution Representation

Each candidate solution is represented as a 5×7 matrix:

- Rows represent the 5 stages  
- Columns represent the 7 time slots  
- Each cell contains a unique artist ID (0 to 34)  

This structure ensures that every artist performs exactly once, with no repeats or omissions.

---

## Fitness Function

A precomputed conflict matrix is used to measure audience overlap between artists. For each time slot, we compute the sum of conflicts between the five artists performing simultaneously.

The final fitness score is normalized between 0 and 1:

- A score of 1 indicates no conflicts  
- Lower scores indicate higher levels of conflict  

The higher the fitness, the better the lineup in terms of audience satisfaction.

---

## Genetic Algorithm Components

### Selection Methods

- **Tournament Selection:** Selects the best individual from a random subset of size 3.  
- **Rank-Based Selection:** Assigns selection probability based on rank, reducing sensitivity to outliers.

### Crossover Operators

- **Row-wise crossover:** Exchanges stage lineups between two parents.  
- **Column-wise crossover:** Swaps entire time slots between parents.  

In both cases, a repair mechanism ensures no artist is repeated or omitted.

### Mutation Operators

- **Block Move Mutation:** Moves a group of artists to a new position in the lineup.  
- **Scramble Mutation:** Randomizes the order of artists within a rectangular region.  
- **Conflict Reduction Mutation:** Swaps artists to reduce fanbase overlap, based on the conflict matrix.

---

## Performance Summary

The algorithm was evaluated under various settings. Key observations:

- Column-wise crossover consistently outperformed row-wise crossover.  
- Conflict reduction and scramble mutations gave better results than block move.  
- Selection method (tournament vs. rank-based) and elitism had minimal performance impact.

The best configuration achieved a **median fitness of 0.82**, using:

- Crossover probability: 0.99 (column-wise)  
- Mutation probability: 0.44 (conflict reduction)

---

## Repository Structure
/src
├── main.py # Main script
├── selection.py # Selection functions
├── crossover.py # Crossover functions
├── mutation.py # Mutation functions
├── fitness.py # Fitness evaluation
/data
└── conflict_matrix.csv # Artist conflict matrix
/results
└── performance_graphs.png # Result visualizations
README.md
requirements.txt

yaml
Copiar
Editar

---

## How to Run

Clone the repository and install dependencies:

```bash
git clone https://github.com/yourusername/music-festival-optimization.git
cd music-festival-optimization
pip install -r requirements.txt
Run the optimization script:

bash
Copiar
Editar
python src/main.py
Conclusions
This project demonstrates the effectiveness of genetic algorithms in solving complex real-world scheduling problems. Despite not reaching an ideal conflict-free solution, the algorithm produced solid results with high fitness scores.

Future work could explore alternative methods (e.g., hill-climbing) or refine the conflict model with more realistic fanbase data.
