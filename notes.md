# Lecture 1

<!-- center mermaid diagrams -->
<style>
  .mermaid { display: flex; justify-content: center; }
</style>

## Reasoning

- Deduction:
  - What is implied by what we know?
- Belief Revision:
  - What beliefs to give up in case of a contradiction?
- Causality:
  - What is the cause of an event?

## NLP (Processing vs. Understanding)

- Syntactic Ambiguity:
  - "They are cooking apples" (The apples are for cooking or "they" are cooking
    them?)
- Semantic Ambiguity:
  - "She ran to the bank" (River bank or monetary bank?)
- Pragmatic ambiguity:
  - "Can you open the door?" (Is this a question or a request?)

## Prompt Engineering

# Lecture 2

## Problem Solving Using Search

### Knowledge Representation & Reasoning

1. Problem Solving using Search
2. Symbolic (logic)
3. Numeric (probability)
4. Machine Learning

```mermaid
flowchart LR
A[Problem] --> B(Search Formulas)
B --> C(Search Engine)
C --> Solution
A --> D[[1. Initial State\n2. Final State\n3. Actions\n4. Heuristic]]
E[[Search Strategy]] --> C
```

Examples: Two-player games, constant satisfaction problem

Initial State

| 1 | 4 | 3 |
| - | - | - |
| 5 | 2 | 6 |
|   | 8 | 7 |

$\downarrow$ Action: Move 5 down

| 1 | 4 | 3 |
| - | - | - |
|   | 2 | 6 |
| 5 | 8 | 7 |

We represent all next possible states with a tree. Tree is potentially
infinitely large (can repeat same moves over and over again).

### Optimal Search Strategy

1. Cost of a solution
2. Cost of finding an (optimal) solution

### Things to consider

1. **State Space:** Number of states
2. **Branching Factor:** Max amount of children a node can have
3. **Depth of Optimal Solution:** Number of steps required to solve optimally

### Constraint Satisfaction

Example: Place 8 queens on a chess board such that none of them attack each
other. Can't give final state immediately (this is the solution!) but we can
give a test (function) to tell us if a state is a solution or not.

# Lecture 3

## Search Problem

### Successor Function

```mermaid
flowchart LR
A[Problem] --> B(Search Formulas)
B --> C(Search Engine)
C --> Solution
A --> D[[1. Initial State\n2. Final State\n3. Actions\n4. Heuristic]]
E[[Search Strategy\n1. Uninformed search\n2. Informed search]] --> C
```

<br>

```mermaid
flowchart LR
A[Successor Function] --> B(Actions)
```

## The Search Process

```mermaid
flowchart TD
A((15)) --> B((1))
A --> C((2))
A --> D((3))
B --> E((4))
B --> F((5))
B --> G((6))
B --> H((7))
C --> I((8))
C --> J((9))
```

**The Fringe (Frontier)**: Leaf nodes

**Generation:** Applying the successor function to the fringe to create more
nodes (possible choices). (This is a subpart of expanding a node.)

**Expand:**

1. Check if node is good
2. Generate its children

_Nodes on the fringe are waiting to be expanded._

### Evaluating Search Strategies

**Complete:** Does it always find a solution if one exists? (i.e. it doesn't
enter an infinite loop)

**Optimal:** Does it always find the least-cost solution?

**Time complexity:** Number of nodes generated/expanded

**Space complexity:** Maximum number of nodes in memory

_**Parameters:**_

1. **`b`**: Branching factor `b` is when you apply the successor function, and
   you get a set of nodes, how many nodes can that be (that you get back)?
2. **`d`**: Depth `d` of optimal solution (depth of tree)
3. **`m`**: Total (maximum) depth `m` of the search tree

_**Example:**_

```mermaid
flowchart TD
A((d = 0)) --> B((d = 1))
A --> C((d = 1))
B --> D((d = 2))
B --> E((d = 2))
C --> F((d = 2))
C --> G((d = 2))
```

`b` = 2

`d` = 2 (0-indexed)

$N(b,d) = \frac{b}{b-1}b^d = O(b^d)$

### Breadth First Search

Expand fringe nodes that have smallest depth. Use a queue.

- Optimal? Yes
- Complete? Yes
- Time? $O(b^d)$
- Space? $O(b^d)$

### Depth First Search

Expand child nodes recursively, or using a stack.

- Optimal? No (tree could search deeper nodes when goal node is at a lower
  depth)
- Complete? No (tree could be infinite)
- Time? $O(b^m)$
- Space? $O(b\cdot m)$

### Check layer by layer?

- Time? $b^d (\frac{b}{b-1})^2 = O(b^d)$
