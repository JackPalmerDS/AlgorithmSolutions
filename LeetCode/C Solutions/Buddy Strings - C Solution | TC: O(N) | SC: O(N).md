# Approach
The C program takes two input strings and checks whether it is possible to swap exactly one pair of characters in the first string to make it equal to the second string. If yes, the function buddyStrings returns true, otherwise false. This problem is also known as the "Buddy Strings" problem.

Here's a step-by-step breakdown of the approach:

1. First, it checks if the length of the two strings is the same. If the lengths are different, it directly returns false because it is not possible for strings of different lengths to be equal.

2. If the two strings are the same, it checks if there are any duplicate characters in the string using the hasDuplicateChars function. If there are duplicates, it means that it's possible to swap two identical characters in the string without changing the string, so it returns true.

3. If the two strings are not the same, it compares each character of the two strings. For every pair of characters that differ, it keeps track of their index in an array v.

4. If there are exactly two indices in v (meaning exactly two characters are different), and swapping the characters at these indices in the first string makes it equal to the second string, it returns true. Otherwise, it returns false.

5. The function hasDuplicateChars works by maintaining an array of 256 elements (representing all possible ASCII characters). It goes through each character in the string and increments the corresponding element in the array. If any element is incremented more than once, it means the character appears more than once in the string, so the function returns true.

This approach ensures that we only make a single pass through each string, which gives the algorithm a time complexity of O(n), where n is the length of the strings. The space complexity is also O(n) due to the space required to store the array of differing indices.


# Complexity
- Time complexity: O(N)
- Space complexity: O(N) 

# Code
```c
#include <stdbool.h>
#include <string.h>
#include <stdlib.h>

bool hasDuplicateChars(char* s) {
    int chars[256] = {0};
    while(*s) {
        if(chars[(unsigned char)*s]++ > 0) 
            return true;
        s++;
    }
    return false;
}

bool buddyStrings(char* s, char* goal) {
    if(strlen(s) != strlen(goal)) 
        return false;

    if(strcmp(s, goal) == 0)
        return hasDuplicateChars(s);

    int* v = (int*) malloc(strlen(s) * sizeof(int));
    int vSize = 0;
    for(int i = 0; i < strlen(s); i++) {
        if(s[i] != goal[i])
            v[vSize++] = i;
    }

    bool result = vSize == 2 && s[v[0]] == goal[v[1]] && s[v[1]] == goal[v[0]];
    free(v);
    return result;
}

```
