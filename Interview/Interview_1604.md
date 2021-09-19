# 面試金典 1604 井字遊戲

設計一個算法，判斷玩家是否贏了井字遊戲。輸入是一個 N x N 的數組棋盤，由字符" "，"X"和"O"組成，其中字符" "代表一個空位。

以下是井字遊戲的規則：

* 玩家輪流將字符放入空位（" "）中。
* 第一個玩家總是放字符"O"，且第二個玩家總是放字符"X"。
* "X"和"O"只允許放置在空位中，不允許對已放有字符的位置進行填充。
* 當有N個相同（且非空）的字符填充任何行、列或對角線時，遊戲結束，對應該字符的玩家獲勝。
* 當所有位置非空時，也算為遊戲結束。
* 如果遊戲結束，玩家不允許再放置字符。
* 如果遊戲存在獲勝者，就返回該遊戲的獲勝者使用的字符（"X"或"O"）；如果遊戲以平局結束，則返回 "Draw"；如果仍會有行動（遊戲未結束），則返回 "Pending"。
 
[LeetCode](https://leetcode-cn.com/problems/words-frequency-lcci/)

### Example 1

```
Input:  board = ["O X"," XO","X O"]
Output:  "X"
```

### C++ 

* 時間複雜度 O(n)

* 空間複雜度 O(n)

```
class Solution
{
private:
    int size{0};
    bool empty{false};

    bool checkRowColDia(const vector<string> &board, char symbol)
    {
        /* check row and col*/
        int diaCount1 = 0;
        int diaCount2 = 0;
        for (int i = 0; i < size; i++)
        {
            /* diagnoal*/

            if (board[i][i] == symbol)
                diaCount1++;

            if (board[i][size - i - 1] == symbol)
                diaCount2++;

            int rowCount = 0;
            int colCount = 0;
            for (int j = 0; j < size; j++)
            {
                /* each row and col*/
                if (board[i][j] == symbol)
                    rowCount++;
                if (board[j][i] == symbol)
                    colCount++;

                if (empty != true && board[i][j] == ' ')
                    empty = true;
            }

            if (rowCount == size || colCount == size)
                return true;
        }

        if (diaCount1 == size || diaCount2 == size)
            return true;

        return false;
    }

public:
    string tictactoe(vector<string> &board)
    {
        size = board.size();
        string ret;

        if (checkRowColDia(board, 'O') == true)
            return "O";

        if (checkRowColDia(board, 'X') == true)
            return "X";

        if (empty == false)
            return "Draw";
        else
            return "Pending";
    }
};
```
