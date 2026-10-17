Name - shruti santosh varekar
PRN - 25UAM058
DIVISION - A
PART A: Architecture Decision Record (ADR)
ADR Title: Use a Visited Set and Separate BFS/DFS Search Logic
Status: Accepted     Date: 11 October 2026
1.	Context

My project is a graph search system that implements Breadth First Search (BFS) and Depth First Search (DFS). In SLE-2, I profiled both algorithms over three recorded runs using the same small test case of 7 nodes. The measured times were different across runs, so profiling helped me compare the observed behaviour rather than assume that one algorithm is always faster. In SLE-3, I represented the system with the four C4 levels and separated input, search, visited/memory, path/traversal, and output responsibilities.

2.	Decision

I chose to keep BFS and DFS as separate search functions and use a visited set to track already explored nodes. I also kept the system organised into clear modules so that input, search processing, memory tracking, and output can be understood and tested separately.
3.	Alternatives Considered

•	Alternative 1 – Use only BFS: simple and suitable when a shortest path is needed in an unweighted graph, but it does not show DFS behaviour.
•	Alternative 2 – Use only DFS: can explore deeply with a stack/recursion, but it does not guarantee the shortest path in an unweighted graph.
•	Alternative 3 – Search without a visited set: possible for some tree-shaped inputs, but cycles or repeated connections can cause repeated work or non-termination.
•	
4. Rationale / Justification

The SLE-2 profiling runs recorded the following times for the 7-node test case:

Algorithm	Run 1 (ms)	Run 2 (ms)	Run 3 (ms)
BFS	185.41	194.96	197.0244
DFS	225.55	386.27	229.533

Recorded averages: BFS = 192.4648 ms; DFS = 280.451 ms.

1.	In these recorded runs, BFS had the lower average time (about 192.46 ms) than DFS (about 280.45 ms). This is an observation for this test and environment, not a guarantee that BFS is always faster.
2.	DFS showed a larger variation between its recorded runs, especially the 386.27 ms run, which makes repeated measurements important.
3.	Keeping both algorithms lets the project demonstrate two standard graph-traversal strategies instead of claiming one is best for every problem.
4.	The visited set prevents the same node from being repeatedly explored and is important when a graph contains cycles.
5.	The SLE-3 C4 design makes these responsibilities clear: the Search Engine performs traversal, the Visited/Memory module tracks explored nodes, and the Output module presents the result.
6.	The modular design makes it easier to test, explain, and extend the project if the graph size or search requirements increase.

5. Consequences
Positive:
•	The visited set reduces repeated processing and helps avoid infinite traversal on cyclic graphs.
•	Keeping BFS and DFS separate makes the implementation and comparison easier to understand.
•	The C4 modules provide a clear structure for explaining and maintaining the system.


Negative / Trade-offs:

•	The visited set uses additional memory to store explored nodes.
•	Maintaining two algorithms means there is some duplicated control logic and both functions need testing.
•	The SLE-2 test used only 7 nodes, so the timings should not be treated as a benchmark for large graphs.
PART B: Short Summary of My SLE Journey

In SLE-1, I worked on the search-system code and its supporting README/documentation. In SLE-2, I profiled BFS and DFS and compared three recorded runtime measurements for each algorithm on a 7-node test case. BFS had a recorded average of 192.4648 ms and DFS had a recorded average of 280.451 ms. In SLE-3, I documented the architecture using all four C4 levels: Context, Container, Component, and Code. The architecture separates input, search, visited/memory tracking, traversal/path handling, and output. For SLE-4, I recorded why I kept BFS and DFS separate and used a visited set, based on the observed profiling and the modular architecture.
PART C: AI Contribution Note

AI tools used: ChatGPT.
What AI helped with: Understanding the ADR structure, organising the justification, and preparing possible viva questions in simple language.
What I did myself: I worked on the BFS/DFS project, reviewed the profiling results and C4 diagrams, and should verify the final report against my own code and submitted SLE-2/SLE-3 files.
PART D: Viva Preparation Notes

Why use a visited set? It records nodes already explored so the search does not repeatedly process the same nodes, especially when the graph contains cycles.
Why keep BFS and DFS both? They demonstrate different traversal strategies. BFS uses a queue and explores level by level; DFS uses a stack or recursion and explores deeper first.
What did SLE-2 profiling show? For the recorded 7-node test, BFS averaged 192.4648 ms and DFS averaged 280.451 ms. These results describe my test runs only.
How does SLE-3 architecture help? It separates input, search, visited-node tracking, path/traversal handling, and output, making the system easier to explain and test.
What are the limitations? The test case was small, timings can vary between runs, and larger graphs may require more time and memory.
Reference: SLE-2 BFS/DFS profiling report and SLE-3 C4 architecture diagrams / repository (add the exact GitHub URL if required by your faculty).
