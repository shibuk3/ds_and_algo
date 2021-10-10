# Regions Cut By Slashes
## Leetcode Problem No.- 959 [Problem Link](https://leetcode.com/problems/regions-cut-by-slashes/)
### Problem:
An n x n grid is composed of 1 x 1 squares where each 1 x 1 square consists of a '/', '\', or blank space ' '. These characters divide the square into contiguous regions.

Given the grid grid represented as a string array, return the number of regions.

Note that backslash characters are escaped, so a '\' is represented as '\\'.

 

Example 1:


Input: grid = [" /","/ "]
Output: 2
Example 2:


Input: grid = [" /","  "]
Output: 1
Example 3:


Input: grid = ["\\/","/\\"]
Output: 4
Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)
Example 4:


Input: grid = ["/\\","\\/"]
Output: 5
Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)
Example 5:


Input: grid = ["//","/ "]
Output: 3
 

Constraints:

n == grid.length
n == grid[i].length
1 <= n <= 30
grid[i][j] is either '/', '\', or ' '.
### Solution:
Using a 3X3 array to represent '/'

0 0 1

0 1 0

1 0 0

and '\\' by 

0 0 1

0 1 0

1 0 0

connected 0 will represent seprate region and now problem is similar to count no. of island.

cant be solved using 1x1 and 2x2 matrix 

example :
case 1: ["\\","/ "]

[\\/]-> have 3 seprate region 

1x1 array:

if we denote '\\' by 1 and '/' by 1 then 

[\\/]-> 1 1 it does not make sense , not able to respresent seprated spaces.

2x2 array:

if we denote '\\' by

1 0

0 1

and '/' by 

0 1 

1 0


[\\/]-> 

1 0 0 1

0 1 1 0
       
you may feel like it working fine as we get 3 seprate region which correct but now try for next case.

case 2 : ["//","/ "]

[/ /]     

[/  ]

will be represented as 

0 1 0 1

1 0 1 0

0 1 0 0

1 0 0 0

it will give 5 region but we only 3 separate region.
Now try for larger size matrix it will be clear 3x3 or more than array size will work.
```
class Solution {
public:
    int dx[4]={-1,0,1,0};
    int dy[4]={0,1,0,-1};
    int vis[91][91];
    bool isValid(int n,vector<vector<int>> &g,int x,int y){
        if(x<0 || y<0 || x>n-1 || y>n-1 || g[x][y]==1 || vis[x][y]==1) return false;
        return true;
    }
    void dfs(int n,vector<vector<int>> &g,int x,int y){
        vis[x][y]=1;
        for(int i=0;i<4;i++){
            if(isValid(n,g,x+dx[i],y+dy[i])){
                dfs(n,g,x+dx[i],y+dy[i]);
            }
        } 
    }
    int regionsBySlashes(vector<string>& grid) {
        int n=grid.size();
        vector<vector<int>> g(n*3,vector<int>(n*3,0));
        memset(vis,0,sizeof(vis));
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]=='/'){
                    g[i*3][j*3+2]=1;
                    g[i*3+1][j*3+1]=1;
                    g[i*3+2][j*3]=1;
                }
                else if(grid[i][j]=='\\'){
                    g[i*3][j*3]=1;
                    g[i*3+1][j*3+1]=1;
                    g[i*3+2][j*3+2]=1;
                }
            }
        }
        int count=0;
        for(int i=0;i<n*3;i++){
            for(int j=0;j<n*3;j++){
                if(vis[i][j]==0 && g[i][j]==0){
                    dfs(n*3,g,i,j);
                    count++;
                }
            }
        }
        return count;
    }
};
```
