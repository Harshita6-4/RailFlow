# RailFlow 🚆 — Smart Track & Platform Mapping

A real-time railway scheduling simulation built in C++17. RailFlow models a station network as a weighted graph, routes multiple trains using Dijkstra's algorithm, detects and resolves track conflicts automatically, and visualises the full schedule through an interactive HTML dashboard.

---

## Features

- **Graph-based station network** — 8 stations, 10 weighted track connections
- **Dijkstra routing** — shortest path assignment for every train
- **Conflict detection** — identifies trains occupying the same track within a 2-minute safety window
- **Automatic conflict resolution** — reroutes lower-priority trains; falls back to time delay if no alternate path exists
- **ETA calculation** — physics-based (distance ÷ speed × 60)
- **Platform allocation** — greedy, priority-aware scheduler across 4 platforms
- **JSON export** — all data written to `output.json` for the dashboard
- **Interactive dashboard** — open `index.html` in any browser to view the full schedule

---

## Project Structure

```
RAIL/
├── main.cpp        # Entry point — wires all modules
├── graph.h         # Data structures, clock utility, RailwayGraph (Harshita)
├── conflict.h      # Dijkstra routing & conflict engine (Anant)
├── platform.h      # ETA calculator & platform allocator (Anany)
├── export.h        # JSON serialiser (Kavya)
├── output.json     # Generated at runtime — consumed by dashboard
├── index.html      # Interactive browser dashboard
└── railflow.exe    # Pre-compiled Windows binary
```

---

## How to Build & Run

**Requirements:** g++ with C++17 support

```bash
g++ -std=c++17 -O2 -o railflow main.cpp
./railflow
```

Or on Windows:
```
g++ -std=c++17 -O2 -o railflow.exe main.cpp
railflow.exe
```

After running, open `index.html` in your browser to see the visual schedule.

---

## Team

| Member | Role | Module |
|--------|------|--------|
| Harshita | Team Lead — System Design & Integration | graph.h |
| Anant | Algorithms — Routing & Conflict Detection | conflict.h |
| Anany | Algorithms — ETA & Platform Allocation | platform.h |
| Kavya | Frontend & Validation — Dashboard & JSON Export | export.h |

**Institution:** Graphic Era University (GEU)

---

## How It Works

1. A railway graph is constructed with 8 stations and weighted edges representing track distances.
2. Each train is assigned the shortest route via Dijkstra's algorithm.
3. The conflict detector checks every pair of trains for overlapping track usage within a time window.
4. Conflicting trains are resolved by priority — the lower-priority train is rerouted using a blocked-edge Dijkstra, or delayed if no alternate path exists.
5. Platforms are allocated greedily, sorted by arrival time, with priority trains getting first pick.
6. Everything is exported to `output.json` and rendered in the browser dashboard.

---

## Sample Output

```
=========================================
 RailFlow: Smart Track & Platform Mapping
 Simulation base time: 6:00 AM
=========================================

[Routing] Assigning routes via Dijkstra...
[ConflictDetector] Checking for conflicts...
[PlatformAllocator] Assigning platforms...

ID  Name            Priority  Arrives     Departs     Platform  Status
------------------------------------------------------------------------
1   Rajdhani-12     HIGH      8:12 AM     8:22 AM     P-1       On Time
2   Shatabdi-04     HIGH      8:24 AM     8:34 AM     P-2       On Time
3   Express-07      NORMAL    8:48 AM     8:58 AM     P-1       On Time
...
```
