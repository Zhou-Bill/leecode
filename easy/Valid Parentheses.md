####Valid Parentheses

> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

> The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

```
#include <iostream>
#include <stack>
#include <string>

using namespace std;

class Solution {
public:
    bool isValid(string s) {
        int length = s.size(), i = 0, k = 0, j;
        char temp;
        stack<char> mystack;
        if (length % 2 != 0 || length < 1 || s[0] == ')' || s[0] == ']' || s[0] == '}')
            return false;

        for (i = 0; i < length; i++){
            if (s[i] == '{' || s[i] == '[' || s[i] == '('){
                mystack.push(s[i]);
            }
            else
            {
                switch (mystack.top())
                {
                case '{':
                    if (s[i] == '}')
                    {
                        mystack.pop();
                        continue;
                    }
                    else
                        return false;
                    break;
                case '[':
                    if (s[i] == ']')
                    {
                        mystack.pop();
                        continue;
                    }
                    else
                        return false;
                    break;
                case '(':
                    if (s[i] == ')')
                    {
                        mystack.pop();
                        continue;
                    }
                    else
                        return false;
                    break;
                }
            
            }
        }
        if (i == length && mystack.empty()){
            return true;
        }
        else{
            return false;
        }

    }

};

int main(){
    //string str = "[({(())}{()})]";
    //string str = "((";
    //string str = "[][]()(){}{}";
    //string str = "[{[]}()]";
    //string str = "([)]";
    string str = "[([]])";
    Solution solution;
    bool result = solution.isValid(str);
    cout << result;
}
```


* 这道题很简单就是判断左括号 入栈的问题
* 如果是左括号就入栈，不是的话就判定栈顶元素的左括号与当前string[index] 右括号是否匹配，如果匹配那么就出栈，不匹配那么就直接返回false
* 最后就是判断i == length 和 栈内是否是空栈，以上条件都符合就返回true
