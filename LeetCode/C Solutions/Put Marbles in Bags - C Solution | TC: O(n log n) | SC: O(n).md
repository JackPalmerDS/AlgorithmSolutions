# Approach:

The main function here is putMarbles(). The function accepts an integer array representing the weights of marbles, the size of this array, and an integer k representing the number of bags. The function then divides the marbles into the k bags following certain rules and calculates the score. The score is the difference between the maximum and minimum scores of marble distributions.

- Two heaps are created: a max heap and a min heap. Both heaps are essentially priority queues with the max heap returning the maximum value and the min heap returning the minimum value. These heaps will be used to track the highest and lowest cost of the bags.

- We then iterate through the weights array. For each pair of weights (i and i+1), we calculate the sum and push this sum into both heaps.

- We then subtract 1 from k and run a loop k-1 times. In each iteration, we pop the top elements from both heaps, add the top of max heap and subtract the top of min heap to/from the ans variable.

- The function finally returns the ans variable which contains the difference between the maximum and minimum score.

# Complexity
- Time complexity: O(n log n)
- Space complexity: O(n) 


# Code
```c
#include <stdlib.h>
#include <string.h>

typedef struct {
    int* data;
    int size;
    int capacity;
    int (*cmp)(int a, int b);
} Heap;

Heap* heapCreate(int capacity, int (*cmp)(int a, int b)) {
    Heap* h = (Heap*)malloc(sizeof(Heap));
    h->data = (int*)malloc(sizeof(int) * capacity);
    h->size = 0;
    h->capacity = capacity;
    h->cmp = cmp;
    return h;
}

void heapDestroy(Heap* h) {
    free(h->data);
    free(h);
}

void heapPush(Heap* h, int x) {
    h->data[h->size] = x;
    int i = h->size++;
    while (i > 0) {
        int p = (i - 1) / 2;
        if (h->cmp(h->data[p], h->data[i]) <= 0) break;
        int temp = h->data[i];
        h->data[i] = h->data[p];
        h->data[p] = temp;
        i = p;
    }
}

int heapPop(Heap* h) {
    int ret = h->data[0];
    h->data[0] = h->data[--h->size];
    int i = 0;
    while (1) {
        int l = i * 2 + 1, r = i * 2 + 2;
        if (l >= h->size) break;
        int j = (r < h->size && h->cmp(h->data[r], h->data[l]) < 0) ? r : l;
        if (h->cmp(h->data[i], h->data[j]) <= 0) break;
        int temp = h->data[i];
        h->data[i] = h->data[j];
        h->data[j] = temp;
        i = j;
    }
    return ret;
}

int cmpMax(int a, int b) {
    return b - a;
}

int cmpMin(int a, int b) {
    return a - b;
}

long long putMarbles(int* weights, int weightsSize, int k){
    Heap* maxHeap = heapCreate(weightsSize, cmpMax);
    Heap* minHeap = heapCreate(weightsSize, cmpMin);
        
    long long ans = 0;
    for(int i = 0; i < weightsSize - 1; i++) {
        heapPush(maxHeap, weights[i] + weights[i+1]);    
        heapPush(minHeap, weights[i] + weights[i+1]);    
    }
    int x = k - 1;
    while(x--) {
        ans += (1LL * heapPop(maxHeap));
        ans -= (1LL * heapPop(minHeap));
    }
    heapDestroy(maxHeap);
    heapDestroy(minHeap);
    return ans;
}

```
