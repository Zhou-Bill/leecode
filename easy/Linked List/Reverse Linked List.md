##Reverse Linked List


> 翻转链表


```
#include<iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
    
};

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *p;
        p = head;
        if (head == NULL)
            return head;
        //程序思想把每个节点插入到头部，然后改变头指针变化，p保持不变，p一开始
        //指向的是head，head的下一位经过一次循环后已经变成了头，
        //比如1,2,3，现在head，跟p一开始就指向了1，然后经过一次循环，变成了2,1,3,
        //p现在仍然指向1，但他的下一位已经是3了，知道他1的下一位为Null，他就停止循环，链表已经发生了反向   
        while (p->next)
        {
            ListNode *q = p->next;
            p->next = p->next->next;
            q->next = head;
            head = q;

        }
        display(head);
        return head;

    }

    void display(ListNode *head) {
        while (head)
        {
            cout << head->val<<"   ";
            head = head->next;

        }
    }
};


int main() {
    int array[] = { 1, 2, 3, 4, 5 };
    ListNode *head, *p;
    head = new ListNode(array[0]);
    p = head;
    for (int i = 1; i < sizeof(array) / sizeof(int); i++){
        ListNode *Node = new ListNode(array[i]);
        p->next = Node;
        p = p->next;
    }
    Solution solution;
    solution.display(head);
    solution.reverseList(head);
}
```

* 程序思想就是把他后一位节点插到头部