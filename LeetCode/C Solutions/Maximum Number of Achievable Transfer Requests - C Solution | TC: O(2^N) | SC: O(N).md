# Approach
1. Initialization:

- The variable m is set to the number of requests.
- An array named building is created with a size of n+1, where n is the number of buildings. This array is initialized with zeros and it keeps track of the number of units in each building.

2. Recursive Depth-First Search (DFS):

- The dfs function is used to check all possible combinations of fulfilling the requests. The dfs function is called with the initial index of 0, requests array, building array, and the number of buildings.
- Inside the dfs function, if the index equals m (the number of requests), the function checks whether all buildings have 0 units. If any building does not have 0 units, it returns INT_MIN (the minimum integer), which indicates an invalid state. If all buildings have 0 units, it returns 0, which means no more requests to process.
- If the index does not equal m, the function continues to process the requests. It first tries to ignore the current request (by just going to the next index) and then tries to fulfill the current request (by decreasing the unit from the source building and increasing the unit in the destination building). It then recursively calls the dfs function for the next request.
- After checking both possibilities (fulfilling and ignoring the request), it returns the maximum of the two results. This is because we want to fulfill the maximum number of requests.

3. Finally, the maximumRequests function calls the dfs function and returns the maximum number of requests that can be fulfilled. Before returning, it frees the memory allocated for the building array.


# Complexity
- Time complexity: O(2^N)
- Space complexity: O(N) 


# Code
```c
#include <limits.h>

int m;

int dfs(int idx, int** requests, int* building, int n)
{
    if(idx == m)
    {
        for(int i = 0; i < n; i++)
        {
            if(building[i] != 0)
                return INT_MIN;
        }
        return 0;
    }
    int val1 = dfs(idx+1, requests, building, n);
    building[requests[idx][0]]--;
    building[requests[idx][1]]++;
    int val2 = 1 + dfs(idx+1, requests, building, n);
    building[requests[idx][0]]++;
    building[requests[idx][1]]--;
    return max(val1, val2);
}

int max(int a, int b) 
{
    return (a > b) ? a : b;
}

int maximumRequests(int n, int** requests, int requestsSize, int* requestsColSize)
{
    int *building = (int *)calloc(n+1,sizeof(int));
    m = requestsSize;
    int result = dfs(0, requests, building, n);
    free(building);
    return result;
}

```
