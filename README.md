 <h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name:     BHARATHI P                  </h3>
<h3>Register Number/Staff Id:        212224060043</h3>
<H3>Aim:</H3>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>
<h1>Problem Description</h1>
<hr>
<h2>Wumpus World</h2>
<hr>
The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>
<p>
This is a python program that uses propositional logic sentences to check which rooms are safe. 

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.
</p>

# program

```
from collections import deque

SIZE = 4
dirs = [(-1,0),(1,0),(0,-1),(0,1)]

pits = {(2,3)}
wumpus = {(3,1)}
breeze = {(1,3),(2,2),(3,3),(2,4)}
stench = {(2,1),(3,2),(4,1)}

knowledge = {(r,c): 'Unknown' for r in range(1,SIZE+1) for c in range(1,SIZE+1)}
knowledge[(1,1)] = 'Safe'

def adj(r,c):
    return [(r+dr,c+dc) for dr,dc in dirs if 1 <= r+dr <= SIZE and 1 <= c+dc <= SIZE]

def infer():
    changed = True
    while changed:
        changed = False
        for r in range(1,SIZE+1):
            for c in range(1,SIZE+1):
                if knowledge[(r,c)] == 'Unknown':
                    adj_cells = adj(r,c)
                    if not any(cell in breeze for cell in adj_cells) and not any(cell in stench for cell in adj_cells):
                        knowledge[(r,c)] = 'Safe'
                        changed = True

def bfs():
    start, goal = (1,1), (4,4)
    q = deque([start])
    visited = {start}
    parent = {start: None}
    while q:
        cur = q.popleft()
        if cur == goal:
            path = []
            while cur:
                path.append(cur)
                cur = parent[cur]
            return path[::-1]
        for nbr in adj(*cur):
            if knowledge.get(nbr) == 'Safe' and nbr not in visited:
                visited.add(nbr)
                parent[nbr] = cur
                q.append(nbr)
    return None

infer()

print("Knowledge Base:")
for r in range(SIZE,0,-1):
    for c in range(1,SIZE+1):
        print(f"{knowledge[(r,c)]:^7}", end=" ")
    print()

path = bfs()
if path:
    print("\nSafe Path:", " -> ".join(str(p) for p in path))
else:
    print("\nNo safe path found.")

def bfs():
    start, goal = (1,1), (4,4)
    q = deque([start])
    visited = {start}
    parent = {start: None}
    while q:
        cur = q.popleft()
        if cur == goal:
            path = []
            while cur:
                path.append(cur)
                cur = parent[cur]
            return path[::-1]
 

<hr>
```

# output
<img width="460" height="228" alt="image" src="https://github.com/user-attachments/assets/14279a6f-5780-4441-9389-f2cad7ab635b" />

<h1>Sample Input and Output:</h1>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)

