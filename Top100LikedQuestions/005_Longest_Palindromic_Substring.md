# 005. Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.

[LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)

### Example 1:
```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
### Example 2:
```
Input: s = "cbbd"
Output: "bb"
```
### Example 3:
```
Input: s = "a"
Output: "a"
```
### Example 4:
```
Input: s = "ac"
Output: "a"
```

#  無重覆字符的最長子串
給定一個字符串，請你找出s中最長的回文子串

# Solution  

## C

```
void expansion(int *left, int *right, int *len, int *tmp_len, int *max_len, int *min_left, int *max_right, char *s, int *found)
{
    int max_move = (*left < *len - *right) ? *left : *len - *right;
    for (int offset = 0; offset <= max_move; offset++)
    {
        if (s[*left - offset] == s[*right + offset])
        {
            *tmp_len = (*right + offset) - (*left - offset) + 1;
            if (*tmp_len > *max_len)
            {
                *max_len = *tmp_len;
                *min_left = *left - offset;
                *max_right = *right + offset;
            }
        }
        else
        {
            *found = 0;
            break;
        }
    }
}

char *longestPalindrome(char *s)
{
    int len = strlen(s);
    int left = 0;
    int right = 0;
    int found = 0;
    int max_move = 0;
    int max_len = 0;
    int tmp_len = 0;
    int min_left = 0;
    int max_right = 0;

    /* for even windown expansion*/
    for (int i = 1; i < len; i++)
    {
        if ((i >= 1) && (s[i] == s[i - 1]))
        {
            left = i - 1;
            right = i;
            found = 1;
            tmp_len = 2;
        }

        if (found == 1)
        {
            expansion(&left, &right, &len, &tmp_len, &max_len, &min_left, &max_right, s, &found);
        }
    }

    found = 0;
    /* for odd windown expansion*/
    for (int i = 1; i < len; i++)
    {
        /* decide the square is odd or even*/
        if (((i - 1) >= 0) && ((i + 1) < len) && (s[i - 1] == s[i + 1]))
        {
            left = i - 1;
            right = i + 1;
            found = 1;
            tmp_len = 3;
        }

        if (found == 1)
        {
            expansion(&left, &right, &len, &tmp_len, &max_len, &min_left, &max_right, s, &found);
        }
    }

    s[max_right + 1] = '\0';
    s += min_left;

    return s;
}
```


