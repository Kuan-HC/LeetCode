# Valid Parentheses
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
```