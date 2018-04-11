[克隆图](https://leetcode.com/problems/clone-graph/description/)

```
Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.


OJ's undirected graph serialization:
Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
Second node is labeled as 1. Connect node 1 to node 2.
Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
Visually, the graph looks like the following:

       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

##### 灌水法

which/how many nodes? + parent->children: relationships

```java
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) return node;

        // Graph Traversal
        List<UndirectedGraphNode> nodes = new ArrayList<>();
        Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<>();
        
        // get all nodes and Mapping: [old, new] store in a HashMap in the meantime
        // because you need to grab nb for every Vertex in the old graph to put in the new Vertex
        // 1. node -> nodes && 2. copy -> node
        nodes = bfs(node, map); // old ones
        
        // 3. copy -> edges
        for (UndirectedGraphNode old: nodes) {
            UndirectedGraphNode newNode = map.get(old);
            List<UndirectedGraphNode> newList = newNode.neighbors;
            for (UndirectedGraphNode nb: old.neighbors) {
                newList.add(map.get(nb));
            }
        }
        
        return map.get(node);
    }
    private List<UndirectedGraphNode> bfs(UndirectedGraphNode start, Map<UndirectedGraphNode, UndirectedGraphNode> map) {
        Queue<UndirectedGraphNode> q = new LinkedList<>();
        Set<UndirectedGraphNode> vis = new HashSet<>();
        q.offer(start);
        vis.add(start);
        
        while (!q.isEmpty()) {
            UndirectedGraphNode curr = q.poll();
            UndirectedGraphNode newNode = new UndirectedGraphNode(curr.label);
            map.put(curr, newNode); //旧->新
            
            for (UndirectedGraphNode nb: curr.neighbors) {
                if (!vis.contains(nb)) {
                    q.offer(nb);
                    vis.add(nb);
                }
            }
        }
        return new ArrayList<UndirectedGraphNode>(vis);
    }
}
```
