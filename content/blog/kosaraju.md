+++
title = "Kosaraju's Algorithm is My Favorite"
date = 2025-07-08
description = "Kosaraju's Algorithm"
katex = true
mermaid = true

[taxonomies]
tags = ["algorithms", "graphs", "connectivity"]
+++

# Introduction

Occasionally, people will ask me if I have a favorite algorithm. Of course, the answer is yes! Kosaraju's algorithm is
an algorithm for determing the strongly connected components of a directed graph. 

```python,name=kosaraju
#!/usr/bin/env python3

from typing import Literal

from graph_helper import DirectedGraph, Edge, Node, TraversalData


def kosaraju(graph: DirectedGraph) -> list[list[Node]]:
    def dfs(root: Node, visited: list[Node]) -> None:
        trv.mark_visited(root)
        for neighbor in graph.neighbors(root):
            if not trv.already_visited(neighbor):
                dfs(neighbor, visited)
        visited.append(root)

    trv = TraversalData(graph.nodes)
    stack: list[Node] = []
    for v in graph.nodes:
        if not trv.already_visited(v):
            dfs(v, stack)

    trv.reset()
    graph.reverse_edges()
    strongly_connected_components: list[list[Node]] = []
    for v in reversed(stack):
        if not trv.already_visited(v):
            strongly_connected_components.append([])
            dfs(v, strongly_connected_components[-1])
    return strongly_connected_components


def main() -> Literal[0]:
    return 0


if __name__ == "__main__":
    main()
```
