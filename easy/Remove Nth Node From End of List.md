#Remove Nth Node From End of List

#####Given a linked list, remove the nth node from the end of list and return its head.

>    Given linked list: 1->2->3->4->5, and n = 2.

>  After removing the second node from the end, the linked list becomes 1->2->3->5


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

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL){}
};

class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* node, *p;
        int i = 0,index;
        node = head;
        //现获取到链表的长度
        while (node != NULL)
        {
            i++;
            node = node->next;
        }
    
        node = p = head;
        //n是反向回来的那个下标，那么正向就是长度-n，就是反向n的前一个，比如链表长度为5，我要删除的是n=2,那么正向顺序就是5-2+1
        index = i - n;
        //如果是等于0，那么就是删除头指针
        if (index){
            while (--index>0)
            {
                p = p->next;
            }
            node = p->next;
            p->next = node->next;
            node->next = NULL;
            
        }
        else{
            head = head->next;
            node->next = NULL;
        }
        return head;
        
    }
    void display_list(ListNode* head){
        while (head !=NULL)
        {
            cout << head->val << "  ";
            head = head->next;
        }
    }
};

int main() {
    int i = 0, array[] = { 1 };
    ListNode* head=new ListNode(array[0]),*list;
    list = head;

    for (i = 1; i < 1; i++){
        ListNode* Node = new ListNode(array[i]);
        head->next = Node;
        head = Node;
    }
    Solution solution;
    solution.display_list(list);
    head = solution.removeNthFromEnd(list, 1);
    solution.display_list(head);

}

```