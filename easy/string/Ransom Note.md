##  Ransom Note


>Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

>Each letter in the magazine string can only be used once in your ransom note.

题目说明：ransom 字符串的所有字符都可以在magazine中找到

```

class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int length1 = ransomNote.size(),length2 = magazine.size();
        if (length1 == 0 && length2 == 0){
            return true;
        }
        //用两个map分别存放里面字母个数
        map<char, int> rans, magaz;
        for (int i = 0; i < length2; i++){
            magaz[magazine[i]]++;
        }
        for (int i = 0; i < length1; i++){
            rans[ransomNote[i]]++;
        }

        map<char, int>::iterator it1, it2;
        for (it1 = rans.begin(); it1 != rans.end(); it1++){
            if (it1->second > magaz[it1->first])
                return false;
        }
        

        return true;
    }
};
```

* 我的想法是将他们分别用map装起来，然后判断magazine['a'] 的值 是否大于 ransom['a']的值，小于的话就return false


```
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        for (int i = 0; i<ransomNote.length(); i++){
            if (magazine.find(ransomNote[i]) != string::npos)
                magazine[magazine.find(ransomNote[i])] = '\0';
            else
                return false;
        }
        return true;
    }
};
```

直接在magazine找ransomNode 字符，找到了之后把magazine[magazine.find(ransomNote[i])] 的值置为'\0',没知道return false;

magazine.find(ransomNote[i]) != string::npos 找到返回true，没找到返回false
