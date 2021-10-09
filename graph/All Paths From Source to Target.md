# All Paths From Source to Target
## Leetcode Problem No.-797 [Problem Link](https://leetcode.com/problems/all-paths-from-source-to-target/)
### Problem:

Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.

The graph is given as follows: graph[i] is a list of all nodes you can visit from node i (i.e., there is a directed edge from node i to node graph[i][j]).

 

Example 1:


Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
Example 2:


Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
Example 3:

Input: graph = [[1],[]]
Output: [[0,1]]
Example 4:

Input: graph = [[1,2,3],[2],[3],[]]
Output: [[0,1,2,3],[0,2,3],[0,3]]
Example 5:

Input: graph = [[1,3],[2],[3],[]]
Output: [[0,1,2,3],[0,3]]
 

Constraints:

n == graph.length
2 <= n <= 15
0 <= graph[i][j] < n
graph[i][j] != i (i.e., there will be no self-loops).
All the elements of graph[i] are unique.
The input graph is guaranteed to be a DAG.

### Solution:
used concept of DFS and backtracking
visit node , then add it to current path vector c and then visit its child then child of child and keep adding it to the current path vector c.
when we hit (n-1)th node then add it our solution path and return.
or return when node does not have any child.

```
class Solution {
public:
    void help(vector<vector<int>>& graph,vector<int> &c,vector<vector<int>> &v,int k){
        if(k==graph.size()-1){
            c.push_back(k);
            v.push_back(c);
            c.pop_back();
            return;
        }
        c.push_back(k);
        for(int i:graph[k]){
            help(graph,c,v,i);
        }
        c.pop_back();
    }
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> v;
        vector<int> c;
        help(graph,c,v,0);
        return v;
    }
};
```
