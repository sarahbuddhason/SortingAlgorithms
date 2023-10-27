# Sorting Algorithms

1. [Bubble Sort](#bubble-sort)

2. [Selection Sort](#selection-sort)

3. [Insertion Sort](#insertion-sort)

4. [Merge Sort](#merge-sort)

5. [Quick Sort](#quick-sort)

6. [Heap Sort](#heap-sort)

---

## Bubble Sort
   - **Idea**: Repeatedly swap adjacent elements if they are in the wrong order.
   - **Time**: O(n^2)
   - **Space**: O(1)
  
```
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (arr[j] > arr[j+1])
                std::swap(arr[j], arr[j+1]);
}
```

## Selection Sort
   - **Idea**: Repeatedly find the minimum (or maximum) element and place it at the beginning (or end).
   - **Time**: O(n^2)
   - **Space**: O(1)
  
```
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i;
        for (int j = i+1; j < n; j++)
            if (arr[j] < arr[min_idx])
                min_idx = j;
        std::swap(arr[min_idx], arr[i]);
    }
}
```

## Insertion Sort
   - **Idea**: Build the final sorted array one item at a time, placing each element in its correct position.
   - **Time**: O(n^2)
   - **Space**: O(1)

```
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
```

## Merge Sort
   - **Idea**: Divide the unsorted list into n sublists, merge sublists to produce new sorted sublists until only one remains.
   - **Time**: O(nlogn)
   - **Space**: O(n)

```
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];
    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```

## Quick Sort
   - **Idea**: Select a 'pivot' element and partition the array so elements smaller than pivot are on the left and elements greater are on the right. Recursively sort the sub-arrays.
   - **Time**: O(nlogn) average, O(n^2) worst
   - **Space**: O(logn) (when using in-place partitioning)

```
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }
    std::swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

## Heap Sort
   - **Idea**: Convert the array into a max-heap structure, then repeatedly remove the largest element from the heap and reconstruct the heap.
   - **Time**: O(nlogn)
   - **Space**: O(1)

```
void heapify(int arr[], int n, int i) {
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < n && arr[l] > arr[largest])
        largest = l;
    if (r < n && arr[r] > arr[largest])
        largest = r;
    if (largest != i) {
        std::swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
    for (int i = n - 1; i > 0; i--) {
        std::swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
```
