# quickPow 快速幕





### C++ 

```
#include <iostream> 

using namespace std; 
 

template <typename T> 
T fastPow(T base, T exp, T mod) 

{ 

    T result = 1; 

    while (exp > 0) 

    { 

        if (exp & 1) 

            result = (result * base) % mod; 

 

        base = (base * base) % mod; 

        exp = exp / 2; 

    } 

    return result; 

} 

 

int main(){ 

    int base; 

    int exp, mod; 

    cout << "Enter base, exponent, and modulo: "; 

    cin >> base >> exp >> mod; 

    cout << "Result: " << fastPow(base, exp, mod) << endl; 

     
    return 0; 
} 
```