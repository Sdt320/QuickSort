# QuickSort
Sure, I'll walk you through the QuickSort algorithm step by step. QuickSort is a popular sorting algorithm known for its efficiency and is based on the divide-and-conquer strategy.

### QuickSort Algorithm:

1. **Partitioning**:
   - **Choose a Pivot**: Select an element from the array as the pivot (commonly the last element, but can be any element).
   - **Partitioning**: Rearrange the array such that all elements less than the pivot are on its left, and all elements greater than the pivot are on its right. After partitioning, the pivot element is in its correct position.

2. **Recursively Apply**:
   - Apply QuickSort recursively on the left sub-array (elements less than the pivot).
   - Apply QuickSort recursively on the right sub-array (elements greater than the pivot).

3. **Base Case**:
   - The recursion terminates when the sub-array has fewer than two elements (i.e., when `low >= high`).

### Detailed Steps:

#### Step 1: Choosing a Pivot
- Select the pivot element. It can be chosen in different ways (first element, last element, median of three elements, etc.). For simplicity, we often choose the last element in the array.

#### Step 2: Partitioning the Array
- **Partition Function**: This function rearranges the array such that all elements smaller than the pivot are moved to the left of the pivot, and all elements greater than the pivot are moved to the right of the pivot.

```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];  // Choosing the last element as pivot
    int i = (low - 1);      // Index of smaller element

    for (int j = low; j <= high - 1; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++;    // Increment index of smaller element
            swap(&arr[i], &arr[j]); // Swap arr[i] and arr[j]
        }
    }
    swap(&arr[i + 1], &arr[high]); // Swap arr[i + 1] and arr[high] (pivot)
    return (i + 1);  // Return the partitioning index
}
```

#### Step 3: Recursive QuickSort
- **QuickSort Function**: Recursively sort the sub-arrays before and after the pivot.

```c
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        // pi is partitioning index, arr[pi] is now at right place
        int pi = partition(arr, low, high);

        // Recursively sort elements before partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

#### Step 4: Putting It All Together
- **Main Function**: Initialize the array and call `quickSort` to sort the entire array.

```c
int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    quickSort(arr, 0, n - 1);

    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    return 0;
}
```

### Example Output:
For the array `{10, 7, 8, 9, 1, 5}`, the output of the `quickSort` function will be:
```
Sorted array: 1 5 7 8 9 10
```

### Summary:
QuickSort is efficient with an average time complexity of \(O(n \log n)\) and operates in place with a space complexity of \(O(\log n)\). It is widely used in practice due to its speed and versatility. Understanding the partitioning step is crucial for mastering QuickSort, as it defines how the array is split and sorted recursively.
