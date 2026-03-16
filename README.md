# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** Krishnaveni Pola  
**Student ID    :** 2310040013  
**Date Submitted:** 16-03-2026 

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

```
The fitness() function returns the total value of all items included in a potential solution.
If a solution is overweight, it violates the constraint of the knapsack problem, making it invalid. Assigning it a fitness score of 0 is to ensure that these invalid solutions are not selected.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

```
Tournament selection picks a few random individuals from the population and selects the one with the best fitness from that small group to be a parent.
Higher-fitness individuals are more likely to be chosen because they will win any tournament they are entered into against less-fit individuals.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

```
This line is implementing "elitism," where the best individual from the current generation is copied directly into the next generation. This is important because crossover and mutation are random processes that might accidentally discard the best solution found so far. Elitism guarantees that the quality of the population's best solution will never decrease from one generation to the next.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 | 60 |
| Final best value | 77 |
| Total weight of best solution (kg) | 14.4/15.0 kg |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
Best Packing List
--------------------------------------
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
--------------------------------------
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
```
The plot shows a rapid increase in the best value during the first few generations, which is where the biggest improvement happens. 
After this initial phase, the curve begins to flatten out, indicating that the algorithm has found an optimal solution and further improvements are smaller and less frequent.
```

---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         |      75         |    14.9     |  Yes   | Flattens quickly, gets stuck in a local optimum. |
| 0.05         |      77         |    14.4     |  Yes   | Steep initial rise, then converges smoothly. |
| 0.30         |      78         |    14.1     |  Yes   | More jagged and unstable, but finds a higher peak. |

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
```
When the mutation rate is too low (0.01), the algorithm lacks diversity and moves to a non-optimal solution, getting stuck. A high rate (0.30) makes the search more random, while this can disrupt good solutions, it also helps escape local optima, which in this case led to the best result. 
```

**Which mutation_rate gave the best result? Why do you think that is?**
```
The mutation rate of 0.30 gave the best result (a value of 78).
This high rate likely provided enough randomness to get the algorithm out of a local optimum. It allowed the search to explore a wider, more diverse area of the solution space.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | A balanced mutation rate provides good, consistent convergence to a near-optimal solution. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | A higher mutation rate can sometimes escape local optima to find an even better solution. |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
```
A low rate exploits good solutions but risks getting stuck, while a high rate explores new areas but can be chaotic. These experiments demonstrate that there's no single perfect parameter, and the best setting depends on the problem. Elitism is also important, as it ensures that the random nature of the algorithm doesn't accidentally discard the best solution found so far.
```

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, packing list pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
