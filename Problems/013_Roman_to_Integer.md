# Roman_to_Integer
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M. [LeetCode](https://leetcode.com/problems/roman-to-integer/)  
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

* I can be placed before V (5) and X (10) to make 4 and 9. 
* X can be placed before L (50) and C (100) to make 40 and 90. 
* C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

### Example 1:
```
Input: s = "III"
Output: 3
```

# Solution
## C

```
int romanToInt(char * s){

    int value = 0;

    while(*s != 0){
        
        if (*s == 'I')
            (*(s+1) == 'V' || *(s+1) == 'X')? (value += -1): (value += 1); 
        else if (*s == 'X')
            (*(s+1) == 'L' || *(s+1) == 'C')? (value += -10): (value += 10);
        else if (*s == 'C')
            (*(s+1) == 'D' || *(s+1) == 'M')? (value += -100): (value += 100);
        else if (*s == 'V')
            value += 5;        
        else if (*s == 'L')
            value += 50;                  
        else if (*s == 'D')
            value += 500;
        else if (*s == 'M')
            value += 1000;        
        s++;
    }    
    return value;
}


```


