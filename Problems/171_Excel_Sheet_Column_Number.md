#  Excel Sheet Column Number
Given a column title as appear in an Excel sheet, return its corresponding column number.

[LeetCode](https://leetcode.com/problems/excel-sheet-column-number/)

### Example 1:
```
  A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```

# Excel表列序號
給定一個Excel表格中的列名稱，返回其相應的列序號


# Solution  
## iterate over an array
  
## C

```
int titleToNumber(char * s){
    if( s == NULL || *s < 65 || *s > 90)
        return 0;

    int ret = 0;
    while(*s != 0){
        ret = ret*26 + (*s-64);
        s++;
    }
        
    return ret;
}
```


