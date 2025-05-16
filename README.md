# Job Shop Scheduling with a Genetic Algorithm

Efficiently allocating jobs to machines is a classic **Job Shop Scheduling Problem (JSSP)**—and it’s NP‑hard.

To tackle such a vast combinatorial space we borrow ideas from evolutionary biology and apply a **Genetic Algorithm (GA)**.

> **Why a GA?**  GAs maintain a *population* of candidate schedules (chromosomes) instead of a single point. Through iterative **selection** (preferring shorter makespans), **crossover** (recombining segments from two parent schedules), and **mutation** (randomly swapping operations within a machine), the population steadily drifts toward high‑quality, feasible solutions while still exploring new regions of the search landscape.  *Elitism* keeps the very best chromosomes untouched so improvements are never lost.

Each chromosome encodes **the exact ordering and start time of every operation on every machine**.  A validation step ensures every candidate respects both machine capacity and job‑precedence constraints before it is allowed to compete.

Fitness is simply the inverse makespan: `fitness = 1 / longest machine completion time`.  Natural selection therefore directly rewards chromosomes that finish the entire shop earlier.

After the specified number of generations the fittest chromosome—our best schedule—is rendered as an intuitive Gantt chart so you can visually inspect machine utilisation and bottlenecks.

---

## ✨ Key Features

| Feature                      | Details                                                                                           |
| ---------------------------- | ------------------------------------------------------------------------------------------------- |
| **Flexible text input**      | Enter any number of jobs in the form `Job_1: M1[10] -> M2[5] -> M4[12]` (blank line = done).      |
| **Pure‑Python GA**           | Selection → Crossover → Mutation → Elitism⁠—all parameters are editable at the top of the script. |
| **Feasibility checks**       | Each chromosome is validated to respect machine capacity and job order constraints.               |
| **Interactive Gantt chart**  | Matplotlib visualises the best schedule so you can eyeball machine utilisation.                   |
| **No external dependencies** | Only standard Python 3, `pandas`, and `matplotlib`.                                               |

---

## 🚀 Quick Start

### 1 · Clone

```bash
git clone https://github.com/Taleen-Abuzulof/JobShopSchedulingAlogorithm.git
cd JobShopSchedulingAlogorithm
```

### 2 · Install

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install pandas matplotlib
```

### 3 · Run

```bash
python main.py
```

Then paste one job per line, e.g.:

```
Job_1: M1[10] -> M2[5]  -> M3[12]
Job_2: M2[7]  -> M3[15] -> M1[8]
Job_3: M1[5]  -> M4[10] -> M2[7]
```

Hit **Enter on an empty line** to start the GA.

You’ll see generation logs in the console and a Gantt chart on completion.

---

## 🔧 Configuration

Edit the constants at the top of *main.py*:

| Constant               | Meaning                                                   | Default |
| ---------------------- | --------------------------------------------------------- | ------- |
| `population_size`      | Number of chromosomes per generation                      | `50`    |
| `num_generations`      | GA epochs                                                 | `50`    |
| `mutation_probability` | Probability (0‑1) of swapping two operations on a machine | `0.01`  |

Feel free to tune these for exploration vs. exploitation.

---

## 🧬 Algorithm Pipeline

1. **Initial Population** – Random yet *feasible* schedules are generated.
2. **Fitness** – Makespan (= longest machine completion time) is minimised; fitness = 1/ makespan.
3. **Selection** – Roulette‑wheel sampling proportional to fitness.
4. **Crossover** – One‑point crossover swaps machine assignment slices between parents.
5. **Mutation** – With prob `p`, two operations on the same machine are swapped and start times recomputed.
6. **Elitism** – Two fittest chromosomes pass unchanged to the next generation.
7. **Termination** – After `num_generations`, the best chromosome is plotted.

---

## 📊 Interpreting the Gantt Chart

* **Bars** – Each coloured bar represents a job segment on a machine.
* **Y‑axis** – Machines ordered numerically (M1…Mx).
* **X‑axis** – Time units (your input durations).
* **Colour mapping** – Same colour across machines ↔ same job.

Long bars late on the timeline indicate bottlenecks; adjust job sequences or GA parameters to improve makespan.

---

## 🗂️ Project Structure

```
JobShopSchedulingAlogorithm/
├── main.py       # main script (this repo)
└── README.md           # you are here
```

---

## 📚 Further Reading

* **Genetic Algorithms** – Mitchell, “M. Mitchell (1998) *An Introduction to Genetic Algorithms*.”
* **Job Shop Scheduling** – Pinedo, *Scheduling: Theory, Algorithms, and Systems*, 5th ed.

---

## ⚖️ License

Released under the MIT License – see `LICENSE` for details.

---

### 🙏 Acknowledgements

Built with ☕ and curiosity by Taleen Abuzulof.
Feel free to open issues or PRs to make it better!
