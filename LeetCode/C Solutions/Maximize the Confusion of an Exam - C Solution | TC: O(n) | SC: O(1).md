# Approach:

- Initialize two pointers i and j to 0 which represent the start and end of the window respectively.
- Create an array mp to keep track of frequency of each character in the window.
- Iterate over the answerKey string using the end pointer j.
- For each character, increment its count in the frequency array mp and update the maxCount, which is the count of the most frequent character in the window.
- If the difference between the window's length (j-i+1) and maxCount is greater than k, it means we can't make all the answers same in the window by flipping k answers. So, decrement the count of the character at start of the window in mp and increment the start pointer i.
- Update len to keep track of maximum length of the window seen so far.
- Continue the process until all characters in the answerKey have been processed.
- Return the maximum length of the window which is the maximum consecutive answers that can be achieved.

# Complexity
- Time complexity: O(n)
- Space complexity: O(1) 


# Code
```c
#include <string.h>
#include <stdlib.h>

#define max(a, b) ((a) > (b) ? (a) : (b))

int maxConsecutiveAnswers(char* answerKey, int k) {
    int i = 0, j = 0;
    int mp[128] = {0}; // Create a map for all ASCII characters
    int len = 0, maxCount = 0;
    int answerKeyLength = strlen(answerKey);

    while (j < answerKeyLength) {
        mp[(int)answerKey[j]]++;
        maxCount = max(maxCount, mp[(int)answerKey[j]]);
        while (j - i + 1 - maxCount > k) {
            mp[(int)answerKey[i]]--;
            i++;
        }
        len = max(len, j - i + 1);
        j++;
    }
    return len;
}

```
