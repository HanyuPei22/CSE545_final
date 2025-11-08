# Bin Packing Problem Solver using GA+WoC Algorithm

A sophisticated solution to the Bin Packing Problem using a hybrid approach combining **Genetic Algorithm (GA)** with **Wisdom of Crowds (WoC)**. The project includes a user-friendly GUI built with tkinter for interactive problem solving and visualization.

## 🎯 Overview

The **Bin Packing Problem** is a classic combinatorial optimization problem where the goal is to pack items of different sizes into a finite number of bins, minimizing the number of bins used. This implementation uses an advanced hybrid algorithm that combines:

- **Genetic Algorithm (GA)**: Evolutionary optimization technique that mimics natural selection
- **Wisdom of Crowds (WoC)**: Running multiple parallel populations and combining their solutions for better results

## ✨ Features

- **Hybrid GA+WoC Algorithm**: Combines genetic algorithm with wisdom of crowds for superior solutions
- **Interactive GUI**: Easy-to-use graphical interface with real-time visualization
- **Flexible Input**: Support for both random item generation and custom item sets
- **Visual Analytics**: 
  - Bin packing visualization showing item distribution
  - Fitness evolution graph tracking algorithm progress
- **Customizable Parameters**: Full control over algorithm parameters (population size, generations, mutation rate, etc.)
- **Detailed Results**: Comprehensive solution statistics and bin utilization metrics

## 🚀 Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Setup

1. Clone the repository:
```bash
git clone https://github.com/liuup/CSE545_final.git
cd CSE545_final
```



## 📖 Usage

### Running the GUI Application

Simply run the GUI application:

```bash
python gui_binpacking.py
```

### Using the GUI

1. **Configure Problem Parameters**:
   - Set bin capacity (default: 1.0)
   - Choose number of items to generate
   - Set min/max item sizes
   - Or enter custom items manually

2. **Configure Algorithm Parameters**:
   - Population Size: Number of individuals in each generation (default: 100)
   - Generations: Number of evolution iterations (default: 200)
   - Mutation Rate: Probability of mutation (default: 0.1)
   - Crossover Rate: Probability of crossover (default: 0.8)
   - Crowd Size: Number of parallel populations (default: 5)

3. **Generate Items**:
   - Click "Generate Random Items" for random test cases
   - Or click "Enter Custom Items" to input specific item sizes

4. **Solve**:
   - Click "Solve with GA+WoC" to run the algorithm
   - View results in real-time
   - Explore visualizations in the tabs

### Command-Line Usage

You can also use the algorithm directly in Python:

```python
from ga_woc_binpacking import BinPackingGAWoC, generate_random_items

# Generate test items
items = generate_random_items(50, min_size=0.1, max_size=0.8)
bin_capacity = 1.0

# Create and run solver
solver = BinPackingGAWoC(
    items=items,
    bin_capacity=bin_capacity,
    population_size=100,
    generations=200,
    mutation_rate=0.1,
    crossover_rate=0.8,
    crowd_size=5
)

# Solve the problem
bins, num_bins, fitness_history = solver.solve(verbose=True)

# Display results
print(f"Number of bins used: {num_bins}")
for i, bin_items in enumerate(bins):
    print(f"Bin {i+1}: {bin_items} (Load: {sum(bin_items):.2f})")
```

## 🧬 Algorithm Details

### Genetic Algorithm Components

1. **Chromosome Representation**: Each solution is represented as a list where each gene indicates which bin an item belongs to

2. **Fitness Function**: 
   - Primary: Number of bins used (minimize)
   - Secondary: Wasted space penalty (minimize unused capacity)

3. **Selection**: Tournament selection for choosing parents

4. **Crossover**: Two-point crossover with repair mechanism

5. **Mutation**: Random bin reassignment with validation

6. **Elitism**: Best solution is always preserved

### Wisdom of Crowds Enhancement

The algorithm runs multiple independent populations (crowds) in parallel:
- Each crowd evolves independently for diversity
- Every 10 generations, a consensus solution is created from the best solutions of all crowds
- The consensus is injected back into each crowd to guide exploration
- This approach balances exploration and exploitation

### Key Optimizations

- **First Fit Decreasing**: Items sorted in descending order
- **Repair Mechanism**: Invalid solutions are automatically fixed
- **Adaptive Penalty**: Solutions violating bin capacity are heavily penalized
- **Efficient Fitness**: Fast evaluation using dictionary-based bin tracking

## 📊 Example Results

For 50 random items (sizes 0.1-0.8) with bin capacity 1.0:
- **Number of bins**: ~35-40 bins (varies with random seed)
- **Average bin utilization**: ~70-80%
- **Convergence**: Usually within 100-150 generations

## 🎨 GUI Screenshots

The GUI provides:
- **Configuration Panel**: Set all problem and algorithm parameters
- **Results Panel**: View detailed solution statistics
- **Bin Visualization**: Bar chart showing item distribution across bins
- **Fitness Evolution**: Line graph showing algorithm convergence

## 🛠️ File Structure

```
CSE545_final/
│
├── ga_woc_binpacking.py    # Core GA+WoC algorithm implementation
├── gui_binpacking.py        # GUI application
└── README.md               # This file
```

## 🔧 Customization

### Adding New Heuristics

You can modify the `_create_individual()` method in `ga_woc_binpacking.py` to incorporate different packing heuristics:
- Best Fit
- Worst Fit
- Next Fit

### Adjusting Fitness Function

Modify `_calculate_fitness()` to implement custom fitness metrics, such as:
- Balancing bin loads
- Minimizing maximum bin load
- Considering item fragility or priority

## 📝 Algorithm Parameters Guide

- **Population Size** (50-200): Larger populations explore more solutions but are slower
- **Generations** (100-500): More generations allow better convergence but take longer
- **Mutation Rate** (0.05-0.2): Higher rates increase exploration but may prevent convergence
- **Crossover Rate** (0.6-0.9): Higher rates increase solution mixing
- **Crowd Size** (3-10): More crowds provide diversity but increase computation

## 🙏 Acknowledgments

- Genetic Algorithm concepts from classical evolutionary computation literature
- Wisdom of Crowds approach inspired by ensemble learning methods
- Bin packing problem formulation from combinatorial optimization research

