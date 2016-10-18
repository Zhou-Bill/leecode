
##

```
#include <iostream>
using namespace std;

/**
* Definition for singly-linked list.
* struct ListNode {
*     int val;
*     ListNode *next;
*     ListNode(int x) : val(x), next(NULL) {}
* };
*/


 struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *result,*node,*p,*listPoint1,*listPoint2;
        int flag = 0,addResult,list1,list2;
        p = result = new ListNode(-1);
        result->next = NULL;
        listPoint1 = l1->next;
        listPoint2 = l2->next;
        //遍历两个链表
        while (listPoint1 != NULL || listPoint2!=NULL){
            node = new ListNode(-1);
            list1 = listPoint1 == NULL ? 0 : listPoint1->val;
            list2 = listPoint2 == NULL ? 0 : listPoint2->val;
            //cout << list1;
            if (flag){
                addResult = list1 + list2 + 1;
            }
            else{
                addResult = list1 + list2;
            }
            
            if (addResult >= 10){
                node->val = addResult - 10;
                flag = 1;
            }
            else{
                node->val = addResult;
                flag = 0;
            }
            
            p->next = node;
            p = node;
            if (list1)
                listPoint1 = listPoint1->next;
            if (list2)
            listPoint2 = listPoint2->next;
        }
        if (flag){
            node = new ListNode(-1);
            node->val = 1;
            p->next = node;
            p = node;
        }
        p->next = NULL;
            
        
        return result;

    }

};
void displayList(ListNode *list){
    ListNode *n = list->next;
    while (n != NULL)
    {
        cout << n->val << "  ";
        n = n->next;
    }
    cout << endl;
}
int main() {
    ListNode *p, *s, *lhead,*r;
    r = p = new ListNode(-1); //建立一个头结点
    p->next = NULL;
    int data[] = { 1};
    int data2[] = { 9,9};
    int i = 0;
    for ( i = 0; i < 1; i++){
        s = new ListNode(-1);
        s->val = data[i];
        r -> next = s;
        r = s;
    }
    r->next = NULL;
    displayList(p);
    r = lhead = new ListNode(-1); //新建第二条链表
    for (i = 0; i < 2; i++){
        s = new ListNode(-1);
        s->val = data2[i];
        r->next = s;
        r = s;
    }
    r->next = NULL;
    displayList(lhead);


    Solution solution;
    ListNode *res = solution.addTwoNumbers(p, lhead);
    displayList(res);


}



```


>　２

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *result,*node,*p,*listPoint1,*listPoint2;
        int flag = 0,addResult,list1,list2;
        p = result = new ListNode(-1);
        result->next = NULL;
        listPoint1 = l1;
        listPoint2 = l2;
        //遍历两个链表
        while (listPoint1 != NULL || listPoint2!=NULL){
            node = new ListNode(-1);
            list1 = listPoint1 == NULL ? 0 : listPoint1->val;
            list2 = listPoint2 == NULL ? 0 : listPoint2->val;
            //cout << list1;
            if (flag){
                addResult = list1 + list2 + 1;
            }
            else{
                addResult = list1 + list2;
            }
            
            if (addResult >= 10){
                node->val = addResult - 10;
                flag = 1;
            }
            else{
                node->val = addResult;
                flag = 0;
            }
            
            p->next = node;
            p = node;
            if (listPoint1 != NULL)
                listPoint1 = listPoint1->next;
            if (listPoint2 != NULL)
            listPoint2 = listPoint2->next;
        }
        if (flag){
            node = new ListNode(-1);
            node->val = 1;
            p->next = node;
            p = node;
        }
        p->next = NULL;
            
        
        return result->next;

    }

};
```

> 第一个是完整程序，第二个是提交leecode的程序

* 这道题目其实也不难，主要是考察链表的使用
* 就是两个链表中的节点相加，如果大于10，那么就向后面一位+1，
* 一开始没有想到[1],[9,9] 这种特殊情况，一直想的是[5,4,3] [2,6,4] 节点长度相同的情况
* 于是有了新想法，就是对比两个链表的长度，用链表中比较长的做循环，等拧一个链表为null的时候，取值为0，但这样做过于麻烦，改进成判断两个链表有一个不为空的时候继续循环下去
* 因为写的时候有一个头指针，所以在返回链表的时候返回头指针的下一个