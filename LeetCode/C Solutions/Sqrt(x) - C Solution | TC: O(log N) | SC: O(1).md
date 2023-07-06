# Approach
The equation to consider is (√x-√x)² = 0. We can substitute one of the √x terms with y, transforming the equation into (y-√x)², which simplifies to y² – 2y√x + x = 0. This can further be rewritten as √x = (y² + x) / 2y, which simplifies to √x = (y + x/y) / 2.

Next, we propose √x to be z in the equation. To find a precise decimal value, we can evaluate the difference between y and z against 10^-p (for accuracy up to 5 decimal places, compare the difference between y and z to 10^-5, which equals 0.00001). We continue this process of iteration until the absolute difference between y and z exceeds the specified limit.

# Complexity
- Time complexity: O(log N) 
- Space complexity: O(1) 

# Code
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int mySqrt(int x) {
    if (x < 2)
        return x;
 
    double y = x;
    double z = (y + (x / y)) / 2;
 
    while (fabs(y - z) >= 0.00001) {
        y = z;
        z = (y + (x / y)) / 2;
    }
    return z;
}
```
