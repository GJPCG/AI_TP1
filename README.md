# 🎬 Degrees of Separation

> **AI Assignment TP1**

A Python application that finds the **path** between two Hollywood actors using the concept of [Six Degrees of Kevin Bacon](https://en.wikipedia.org/wiki/Six_Degrees_of_Kevin_Bacon). Two actors are "connected" if they have starred in a film together. This project implements and compares two search strategies — **BFS** and **DFS** — each on its own Git branch.

---

## 📖 Background

This project is inspired by the *Six Degrees of Kevin Bacon* game, in which any Hollywood actor can be connected to Kevin Bacon within six steps through shared movie appearances.

The problem is modelled as a **graph search problem**:
- **Nodes** represent actors/people.
- **Edges** represent movies in which two actors both starred.
- The goal is to find a path between a source and a target actor, using either BFS or DFS.

---

## 🗂️ Project Structure

```
AI_TP1/
├── degrees/
│   ├── degrees.py          # Main program — search logic
│   ├── util.py             # Node, StackFrontier, QueueFrontier classes
│   ├── small/              # Small dataset for quick testing
│   │   ├── people.csv
│   │   ├── movies.csv
│   │   └── stars.csv
│   └── large/              # Full IMDB-derived dataset
│       ├── people.csv
│       ├── movies.csv
│       └── stars.csv
└── README.md
```

### Key Files

| File | Description |
|------|-------------|
| `degrees.py` | Loads CSV data, handles user input, and runs the shortest-path search |
| `util.py` | Data structures: `Node`, `StackFrontier` (DFS), `QueueFrontier` (BFS) |
| `small/` | Lightweight dataset — ideal for development and testing |
| `large/` | Full dataset with thousands of actors and movies |

---

## 🧠 Algorithms & Git Branches

Two search strategies are implemented, each living on its own Git branch:

| Branch | Algorithm | Frontier | Guarantees shortest path? |
|--------|-----------|----------|---------------------------|
| `BFS`  | Breadth-First Search | `QueueFrontier` (FIFO) | ✅ Yes |
| `DFS`  | Depth-First Search   | `StackFrontier` (LIFO) | ❌ No  |

Each search state is a `(movie_id, person_id)` pair representing one step in the connection chain.

```bash
# Switch between implementations
git checkout BFS
git checkout DFS
```

---

## 🚀 How to Run

### Prerequisites

- Python **3.x**

### Usage

```bash
# Navigate into the project directory
cd degrees

# Run with the small dataset (recommended for testing)
python degrees.py small

# Run with the large dataset
python degrees.py large

# Defaults to 'large' if no argument is provided
python degrees.py
```

### Example: Tom Cruise → Mandy Patinkin (`small` dataset)

The following example was run on **both branches** using the small dataset. Both methods find the same connection chain for this pair:

**`BFS` branch** — guaranteed shortest path:

```
$ python degrees.py small
Loading data...
Data loaded.
Name: tom cruise
Name: mandy patinkin
4 degrees of separation.
1: Tom Cruise and Kevin Bacon starred in A Few Good Men
2: Kevin Bacon and Gary Sinise starred in Apollo 13
3: Gary Sinise and Robin Wright starred in Forrest Gump
4: Robin Wright and Mandy Patinkin starred in The Princess Bride
```

**`DFS` branch** — path found (may not be shortest in general):

```
$ python degrees.py small
Loading data...
Data loaded.
Name: tom cruise
Name: mandy patinkin
4 degrees of separation.
1: Tom Cruise and Kevin Bacon starred in A Few Good Men
2: Kevin Bacon and Gary Sinise starred in Apollo 13
3: Gary Sinise and Robin Wright starred in Forrest Gump
4: Robin Wright and Mandy Patinkin starred in The Princess Bride
```

> **Note:** For this particular pair on the small dataset, BFS and DFS happen to return the same path. In general, DFS does **not** guarantee the shortest path.

---

## 📦 Dataset Format

Each dataset directory contains three CSV files:

- **`people.csv`** — Actor records: `id`, `name`, `birth`
- **`movies.csv`** — Movie records: `id`, `title`, `year`
- **`stars.csv`** — Linking table: `person_id`, `movie_id`

---

## 🛠️ Implementation Notes

The `shortest_path(source, target)` function in `degrees.py` is the core of this assignment. It must return a list of `(movie_id, person_id)` pairs representing the path from source to target, or `None` if no connection exists.

---

## 👤 Author

**Guilherme Glória** — a71327
**Rodrigo Fraga** — a89825

---

## 📄 License

This project is for academic purposes only.
