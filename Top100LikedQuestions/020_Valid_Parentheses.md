# 020. Valid Parentheses
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  

An input string is valid if:  

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.  

[LeetCode](https://leetcode.com/problems/valid-parentheses/)  

### Example 1:
```
Input: s = "()"
Output: true
```
### Example 2:
```
Input: s = "([)]"
Output: false
```

#
給定一個只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判斷字符串是否有效。  

有效字符串需滿足：  

左括號必須用相同類型的右括號閉合。  
左括號必須以正確的順序閉合。  
注意空字符串可被認為是有效字符串。  

# Solution
## C

```
bool isValid(char * s){
    int len = strlen(s);
    if (len%2 == 1 || len == 0)
        return false;

    char stack[len+1];
    int stack_i = 0;

    for(int i = 0; i < len; i++)
    {   char a = s[i];
        if (s[i] == '(' || s[i] == '[' || s[i] == '{')
        {
            stack[stack_i++] = s[i];
        }
        else{
            if( i == 0 || stack_i == 0)
                return false;        
            else if (     (s[i] == ')' && stack[stack_i-1] =='(')
                       || (s[i] == ']' && stack[stack_i-1] =='[') 
                       || (s[i] == '}' && stack[stack_i-1] =='{')
                    )                             
                stack_i --; 
            else
                return false;
        }           
        
    }
    if (stack_i == 0)
        return true;
    else
        return false;
 }
```
