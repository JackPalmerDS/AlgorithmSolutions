# Approach
- Check if the number of bags is equal to the number of children. If so, return the maximum number of cookies in a bag, as each child will receive exactly one bag.

- If the number of bags is more than the number of children, we need to distribute the bags among children in such a way that unfairness (maximum cookies a child gets) is minimized. To achieve this, we use a backtracking approach where we try all possible distributions of cookie bags among children and return the minimum unfairness from all distributions.

- We start with an empty path array (indicating no bags assigned to any child yet) and begin the distribution from the first bag (i=0). The path array is of size 'k' (number of children) and path[j] represents the total number of cookies assigned to the jth child.

- In function 'bt', for each bag of cookies (index 'i'), we iterate through each child (index 'j') and assign the current bag to the child. We recursively call the function 'bt' with the next bag (i+1) and updated path.

- After returning from the recursive call, we remove the current bag from the jth child (backtracking step). This allows us to explore other possible distributions.

- For each bag, we calculate the maximum cookies a child gets after assigning the bag. We then keep track of the minimum such maximum number of cookies across all possible distributions. This minimum represents the minimum unfairness possible.

- After exploring all distributions, we return the minimum unfairness.

# Complexity
- Time complexity: O(K^N)
- Space complexity: O(N) 

# Code
```
#include <limits.h>
#include <stdlib.h>

int min(int a, int b){
    return (a < b) ? a : b;
}

int max(int* arr, int k){
    int max_val = arr[0];
    for(int i = 1; i < k; i++)
        if(arr[i] > max_val)
            max_val = arr[i];
    return max_val;
}

int bt(int* cookies, int cookiesSize, int i, int* path, int k){
    if(i == cookiesSize){
        return max(path, k);
    }
    int res = INT_MAX;
    for(int j = 0; j < k; j++){
        path[j] += cookies[i];
        res = min(res, bt(cookies, cookiesSize, i+1, path, k));
        path[j] -= cookies[i];
    }
    return res;
}

int distributeCookies(int* cookies, int cookiesSize, int k){
    if(cookiesSize == k){
        return max(cookies, k);
    }
    int* path = (int*)calloc(k, sizeof(int));
    int result = bt(cookies, cookiesSize, 0, path, k);
    free(path);
    return result;
}

```
