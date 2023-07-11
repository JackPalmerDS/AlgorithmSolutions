# Approach:

- Given that every number appears three times except for one, we can use bitwise operations to try to "cancel out" the bits in the numbers that appear three times.
- Let's consider the array as a sequence of 32 bits, and for each bit, count the number of 1s in the array. Since every number (except one) appears three times, for each bit, the count of 1s should be a multiple of 3, if the single number has a 0 in that bit.
- If the count is not a multiple of 3, the single number must have a 1 in that bit. So, we can find the single number bit by bit.

# Algorithm:

- Initialize an integer result to 0, which will hold our final result.
For each bit from 0 to 31:
- Initialize a count to 0.
- For each number in the array, if that bit in the number is 1, increment the count.
- If the count mod 3 is not 0, set that bit in result to 1.


# Complexity
- Time complexity: O(n)
- Space complexity: O(1) 

# Code
```c
#include <stdlib.h>

int compareInts(const void* a, const void* b) {
    int int_a = *((int*)a);
    int int_b = *((int*)b);

    if (int_a < int_b) return -1;
    if (int_a > int_b) return 1;
    return 0;
}

int singleNumber(int* nums, int numsSize) {
    qsort(nums, numsSize, sizeof(int), compareInts);

    for(int i = 0; i < numsSize - 1; i = i + 3) {
        if(nums[i] != nums[i+1]) {
            return nums[i];
        }
    }

    return nums[numsSize-1];
}

```
