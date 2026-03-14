# Symmetry Reduction in combinatorial optimization

This repository explores the application of symmetry reduction techniques to combinatorial optimization (CO) problems. Many such problems exhibit structural symmetries, that is, transformations of the solution space that preserve both feasibility and objective value. The presence of symmetry partitions the feasible region into equivalence classes called orbits, where all solutions within an orbit share the same objective value. From an optimization perspective, exploring multiple solutions in the same orbit is redundant, and identifying a single canonical representative per orbit suffices.

The notebooks in this repository present classical combinatorial optimization problems formulated as integer linear programs, analyze their symmetry structures, and apply symmetry reduction techniques to decrease the effective solution space. The goal is to illustrate how exploiting symmetry can reduce computational effort in solution enumeration and analysis.

This repository is intended as a pedagogical resource and a foundation for extending these techniques to other combinatorial problems.

## Repository Structure

```
symmetry-reduction-CO/
├── README.md
├── CO_problems_notebooks/
│   ├── shortest_path.ipynb
│   ├── graph_coloring.ipynb (planned)
│   ├── max_cut.ipynb (planned)
│   └── traveling_salesman.ipynb (planned)
└── references/
    └── bibliography.bib
```

## Notebooks Overview

- **shortest_path.ipynb:** Applies *static lexicographic symmetry breaking* to the shortest path problem on undirected graphs. Presents the ILP formulation with flow conservation constraints, introduces graph automorphisms and solution orbits, and implements lexicographic ordering constraints over symmetric nodes adjacent to the source. Two examples are developed: a diamond graph (4 nodes, |Aut(G)| = 2) and a symmetric ladder graph (8 nodes, Aut(G) ≅ ℤ₂×ℤ₂×ℤ₂). Solution enumeration is performed with and without symmetry breaking to quantify the reduction in equivalent optimal solutions.

- **graph_coloring.ipynb:** Applies *static lexicographic symmetry breaking* to the graph coloring problem, where the goal is to assign colors to vertices such that no two adjacent vertices share the same color. This problem exhibits two independent symmetry sources: color permutation symmetry (any relabeling of colors yields an equivalent solution, generating k! redundant solutions for chromatic number k) and vertex symmetry induced by graph automorphisms. Lexicographic ordering constraints on color activation variables are used to eliminate redundant colorings.

- **max_cut.ipynb** *(planned)*: Will address the maximum cut problem, which seeks to partition the vertices of a graph into two sets such that the number of edges between the sets is maximized. This problem is of particular interest due to its connection with QUBO formulations.

- **traveling_salesman.ipynb** *(planned)*: Will examine the traveling salesman problem (TSP), where a salesman must visit each city exactly once and return to the starting city with minimum total distance.

## Implementation

### Prerequisites

- [Julia 1.9](https://julialang.org/downloads/) or higher 
- [Jupyter Notebook](https://jupyter.org/install) with [IJulia](https://github.com/JuliaLang/IJulia.jl)

### Required Julia Packages

```julia
using Pkg; Pkg.add(["JuMP", "HiGHS"])
```

### Modeling and Solver

The optimization models are formulated using [JuMP](https://jump.dev/), a domain-specific algebraic modeling language for mathematical optimization in Julia. The choice of solver depends on the problem formulation; linear and mixed-integer programs are solved using [HiGHS](https://highs.dev/), interfaced through the [HiGHS.jl](https://github.com/jump-dev/HiGHS.jl) package, while other formulations may require alternative solvers.

### Running the Notebooks

- Launch Jupyter:
```bash
jupyter notebook
```
- Navigate to the ```CO_problems_notebooks/``` directory and select the desired notebook.

Each notebook covers:
1. Formulating the problem as a mathematical program
2. Identifying and characterizing structural symmetries
3. Applying symmetry reduction techniques
4. Analyzing the impact on the solution space

## Contributing

Contributions to this repository are welcome. Please open an issue or submit a pull request for suggestions, improvements, or bug fixes.

## License

This project is licensed under the MIT License.
