###Same Tree

判断两个二叉树是否相同

```
#include<iostream>
using namespace std;
int i = 0;
struct  TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        //遍历p 跟q
        if (p == NULL&&q == NULL)
        {
            return true;
        }
        else if (p != NULL&&q != NULL)
        {
            if (p->val == q->val)
            {
                return isSameTree(p->left, q->left)*isSameTree(p->right, q->right);
            }
            else{
                return false;
            }
        }
        else{
            return false;
        }
    
        
    }

    //创建二叉树
    void createTree(TreeNode* &T,int a[],int length,int index){
        
        if (index >= length)
            return;
        T = new TreeNode(a[index]);
        createTree(T->left, a, length, 2 * index + 1);
        createTree(T->right, a, length, 2 * index + 2);

    }
};

int main() {
    Solution solution;
    TreeNode *T,*N;
    int data[] = { 1, 2, 3, 4, 5 }, data2[] = {1,2,3,4,5};
    solution.createTree(T,data,5,0);
    solution.createTree(N, data2, 5, 0);

    cout<<solution.isSameTree(T,N);
    
}


```