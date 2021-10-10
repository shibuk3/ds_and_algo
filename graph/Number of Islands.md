# Number of Islands
## Leetcode Problem No.- 200 [Problem Link](https://leetcode.com/problems/number-of-islands/)
### Problem :

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
Example 2:

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
 

Constraints:

m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] is '0' or '1'.

### Solution:
DFS approach
```
class Solution {
public:
    int dx[4]={-1,0,1,0};
    int dy[4]={0,1,0,-1};
    int vis[301][301];
    bool isValid(vector<vector<char>>& grid,int x,int y){
        int n=grid.size();
        int m=grid[0].size();
        if(x<0 ||x>n-1 || y<0 || y>m-1 || vis[x][y]==1 ||grid[x][y]=='0') return false;
        return true;
    }
    void bfs(vector<vector<char>>& grid,int x,int y){
        vis[x][y]=1;
        for(int i=0;i<4;i++){
            int currX=x+dx[i];
            int currY=y+dy[i];
            if(isValid(grid,currX,currY)) bfs(grid,currX,currY);
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int n=grid.size();
        int m=grid[0].size();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++) vis[i][j]=0;
        }
        int count=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(vis[i][j]==0 && grid[i][j]=='1'){
                    bfs(grid,i,j);
                    count++;
                }
            }
        }
        return count;
    }
};
```
