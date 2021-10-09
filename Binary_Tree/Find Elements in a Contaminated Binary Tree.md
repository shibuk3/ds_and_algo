# Find Elements in a Contaminated Binary Tree
## Leetcode Problem no. - 1261 [Problem link](https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree/)
### Problem:
Given a binary tree with the following rules:

root.val == 0
If treeNode.val == x and treeNode.left != null, then treeNode.left.val == 2 * x + 1
If treeNode.val == x and treeNode.right != null, then treeNode.right.val == 2 * x + 2
Now the binary tree is contaminated, which means all treeNode.val have been changed to -1.

Implement the FindElements class:

FindElements(TreeNode* root) Initializes the object with a contaminated binary tree and recovers it.
bool find(int target) Returns true if the target value exists in the recovered binary tree.
 

Example 1:


Input
["FindElements","find","find"]
[[[-1,null,-1]],[1],[2]]
Output
[null,false,true]
Explanation
FindElements findElements = new FindElements([-1,null,-1]); 
findElements.find(1); // return False 
findElements.find(2); // return True 
Example 2:


Input
["FindElements","find","find","find"]
[[[-1,-1,-1,-1,-1]],[1],[3],[5]]
Output
[null,true,true,false]
Explanation
FindElements findElements = new FindElements([-1,-1,-1,-1,-1]);
findElements.find(1); // return True
findElements.find(3); // return True
findElements.find(5); // return False
Example 3:


Input
["FindElements","find","find","find","find"]
[[[-1,null,-1,-1,null,-1]],[2],[3],[4],[5]]
Output
[null,true,false,false,true]
Explanation
FindElements findElements = new FindElements([-1,null,-1,-1,null,-1]);
findElements.find(2); // return True
findElements.find(3); // return False
findElements.find(4); // return False
findElements.find(5); // return True
 

Constraints:

TreeNode.val == -1
The height of the binary tree is less than or equal to 20
The total number of nodes is between [1, 104]
Total calls of find() is between [1, 104]
0 <= target <= 106

### Solution: 
BFS approach:
Putting the value in nodes according to rule and also storing it in vector in sorted manner the use bianry search to find element
```
class FindElements {
public:
    vector<int> v;
    FindElements(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        root->val=0;
        v.push_back(0);
        while(!q.empty()){
            TreeNode* temp=q.front();
            q.pop();
            if(temp->left!=nullptr){
                temp->left->val=2*temp->val+1;
                q.push(temp->left);
                v.push_back(temp->left->val);
            }
            if(temp->right!=nullptr){
                temp->right->val=2*temp->val+2;
                q.push(temp->right);
                v.push_back(temp->right->val);
            }
        }
    }
    
    bool find(int target) {
        int i=0,j=v.size()-1;
        int mid;
        while(i<=j){
            mid=(j+i)/2;
            if(v[mid]==target) return true;
            if(v[mid]>target) j=mid-1;
            else i=mid+1;
        }
        return false;
    }
};
```
DFS approach:
```
class FindElements {
public:
    set<int> s;
    void dfs(TreeNode* root,int value){
        if(root==nullptr) return;
        root->val=value;
        s.insert(value);
        dfs(root->left,2*value+1);
        dfs(root->right,2*value+2);
    }
    FindElements(TreeNode* root) {
        dfs(root,0);
    }
    
    bool find(int target) {
        return s.find(target)!=s.end();
    }
};
```
