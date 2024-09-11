# IMPORTANT-ALOGIRTHMS-WITH-PRACTICE-QUESTIONS

**SORTING ALGORITHMS**
 
 
1. Bubble Sort
   
Description: Bubble sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. It continues until the array is sorted.
Time Complexity: O(n²)
Space Complexity: O(1) (in-place)

```
public class BubbleSort {
    public void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j + 1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
}
```

2. Selection Sort
Description: Selection sort repeatedly finds the minimum element from the unsorted part and swaps it with the first unsorted element.
Time Complexity: O(n²)
Space Complexity: O(1)

```
public class SelectionSort {
    public void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIdx]) minIdx = j;
            }
            // Swap arr[minIdx] and arr[i]
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }
}
```

3. Insertion Sort
Description: Insertion sort builds the final sorted array one item at a time. It works similarly to the way you sort playing cards.
Time Complexity: O(n²)
Space Complexity: O(1)
```
public class InsertionSort {
    public void insertionSort(int[] arr) {
        int n = arr.length;
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
}
```
4. Merge Sort
Description: Merge sort divides the array into two halves, sorts them recursively, and then merges them. It is an efficient, stable, divide-and-conquer sorting algorithm.
Time Complexity: O(n log n)
Space Complexity: O(n)

```
public class MergeSort {
    public void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] L = new int[n1];
        int[] R = new int[n2];

        System.arraycopy(arr, left, L, 0, n1);
        System.arraycopy(arr, mid + 1, R, 0, n2);

        int i = 0, j = 0, k = left;
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

    public void sort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            sort(arr, left, mid);
            sort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }
}
```

5. Quick Sort
Description: Quick sort selects a pivot element and partitions the array into elements smaller and larger than the pivot, then recursively sorts the subarrays.
Time Complexity: O(n log n) (average), O(n²) (worst)
Space Complexity: O(log n)
```
public class QuickSort {
    public int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        return i + 1;
    }

    public void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
}
```

6. Heap Sort
Description: Heap sort uses a binary heap to sort an array. It is an in-place sorting algorithm and works by maintaining a max-heap structure.
Time Complexity: O(n log n)
Space Complexity: O(1)
```
public class HeapSort {
    public void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && arr[left] > arr[largest]) largest = left;
        if (right < n && arr[right] > arr[largest]) largest = right;

        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;
            heapify(arr, n, largest);
        }
    }

    public void heapSort(int[] arr) {
        int n = arr.length;
        for (int i = n / 2 - 1; i >= 0; i--) heapify(arr, n, i);
        for (int i = n - 1; i > 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            heapify(arr, i, 0);
        }
    }
}
```
7. Radix Sort
Description: Radix sort sorts numbers digit by digit from the least significant digit to the most significant digit using counting sort as a subroutine.
Time Complexity: O(nk), where k is the number of digits in the largest number
Space Complexity: O(n + k)
```
public class RadixSort {
    public void countSort(int[] arr, int n, int exp) {
        int[] output = new int[n];
        int[] count = new int[10];
        
        for (int i = 0; i < n; i++)
            count[(arr[i] / exp) % 10]++;
        
        for (int i = 1; i < 10; i++)
            count[i] += count[i - 1];
        
        for (int i = n - 1; i >= 0; i--) {
            output[count[(arr[i] / exp) % 10] - 1] = arr[i];
            count[(arr[i] / exp) % 10]--;
        }
        
        for (int i = 0; i < n; i++)
            arr[i] = output[i];
    }

    public void radixSort(int[] arr) {
        int max = Arrays.stream(arr).max().getAsInt();
        for (int exp = 1; max / exp > 0; exp *= 10)
            countSort(arr, arr.length, exp);
    }
}
```
8. Counting Sort
Description: Counting sort counts the occurrence of each distinct element in the array and uses this count to compute the final position of each element.
Time Complexity: O(n + k)
Space Complexity: O(k), where k is the range of input elements
```

public class CountingSort {
    public void countingSort(int[] arr) {
        int max = Arrays.stream(arr).max().getAsInt();
        int min = Arrays.stream(arr).min().getAsInt();
        int range = max - min + 1;

        int[] count = new int[range];
        int[] output = new int[arr.length];

        for (int i = 0; i < arr.length; i++) {
            count[arr[i] - min]++;
        }

        for (int i = 1; i < count.length; i++) {
            count[i] += count[i - 1];
        }

        for (int i = arr.length - 1; i >= 0; i--) {
            output[count[arr[i] - min] - 1] = arr[i];
            count[arr[i] - min]--;
        }

        for (int i = 0; i < arr.length; i++) {
            arr[i] = output[i];
        }
    }
}
```
9. Bucket Sort
Description: Bucket sort distributes the elements into buckets, sorts each bucket, and then concatenates them.
Time Complexity: O(n + k)
Space Complexity: O(n + k)

```
import java.util.*;

public class BucketSort {
    public void bucketSort(float[] arr, int n) {
        if (n <= 0) return;

        List<Float>[] buckets = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            buckets[i] = new ArrayList<>();
        }

        for (float value : arr) {
            int bucketIdx = (int) (n * value);
            buckets[bucketIdx].add(value);
        }

        for (List<Float> bucket : buckets) {
            Collections.sort(bucket);
        }

        int index = 0;
        for (List<Float> bucket : buckets) {
            for (float value : bucket) {
                arr[index++] = value;
            }
        }
    }
}
```
10. Tim Sort (Python's Built-In Sorting Algorithm)
Description: TimSort is a hybrid sorting algorithm derived from merge sort and insertion sort. It is stable and works well on real-world data. Java's Arrays.sort() for objects also uses TimSort.
Note: There's no direct Java implementation of TimSort, but you can use Java's Arrays.sort().
```
import java.util.Arrays;

public class TimSortExample {
    public static void main(String[] args) {
        int[] arr = {5, 21, 7, 23, 19};
        Arrays.sort(arr);  // Uses TimSort for non-primitive types
        System.out.println(Arrays.toString(arr));
    }
}
```

**Summary of Sorting Algorithms**
| Algorithm        | Time Complexity        | Space Complexity | Stability |
|------------------|------------------------|------------------|-----------|
| Bubble Sort      | O(n²)                  | O(1)             | Yes       |
| Selection Sort   | O(n²)                  | O(1)             | No        |
| Insertion Sort   | O(n²)                  | O(1)             | Yes       |
| Merge Sort       | O(n log n)             | O(n)             | Yes       |
| Quick Sort       | O(n log n) avg, O(n²)  | O(log n)         | No        |
| Heap Sort        | O(n log n)             | O(1)             | No        |
| Radix Sort       | O(nk)                  | O(n + k)         | Yes       |
| Counting Sort    | O(n + k)               | O(k)             | Yes       |
| Bucket Sort      | O(n + k)               | O(n + k)         | Yes       |
| Tim Sort         | O(n log n)             | O(n)             | Yes       |

**Problems to practice**

| Algorithm        | LeetCode Problem Number | Title                                              |
|------------------|-------------------------|----------------------------------------------------|
| Bubble Sort      | 1122                    | Relative Sort Array                                |
| Selection Sort   | 912                     | Sort an Array                                      |
| Insertion Sort   | 147                     | Insertion Sort List                                |
| Merge Sort       | 912                     | Sort an Array                                      |
| Merge Sort       | 327                     | Count of Range Sum                                 |
| Quick Sort       | 912                     | Sort an Array                                      |
| Heap Sort        | 215                     | Kth Largest Element in an Array                    |
| Heap Sort        | 973                     | K Closest Points to Origin                         |
| Radix Sort       | 164                     | Maximum Gap                                        |
| Counting Sort    | 75                      | Sort Colors                                        |
| Counting Sort    | 1122                    | Relative Sort Array                                |
| Bucket Sort      | 164                     | Maximum Gap                                        |
| Tim Sort         | 56                      | Merge Intervals                                    |


**Searching Algorithms**


1. Linear Search
Description: Linear search sequentially checks each element of the array until it finds the target value. It's simple but inefficient for large datasets.
Time Complexity: O(n)
Space Complexity: O(1)
```
public class LinearSearch {
    
    // Function to perform linear search
    public int linearSearch(int[] arr, int target) {
        // Loop through the array
        for (int i = 0; i < arr.length; i++) {
            // If the current element matches the target, return its index
            if (arr[i] == target) {
                return i;
            }
        }
        // Return -1 if the target is not found
        return -1;
    }
}
```

2. Binary Search (Divide and Conquer)
Description: Binary search works on sorted arrays by repeatedly dividing the search interval in half. It compares the middle element with the target, and then narrows down the search.
Time Complexity: O(log n)
Space Complexity: O(1)

```
public class BinarySearch {
    
    // Function to perform binary search (iterative)
    public int binarySearch(int[] arr, int target) {
        int left = 0, right = arr.length - 1;
        
        // Loop while the search space is valid
        while (left <= right) {
            // Find the middle element
            int mid = left + (right - left) / 2;
            
            // Check if target is present at mid
            if (arr[mid] == target) {
                return mid;
            }
            // If target is greater, ignore the left half
            if (arr[mid] < target) {
                left = mid + 1;
            }
            // If target is smaller, ignore the right half
            else {
                right = mid - 1;
            }
        }
        // Target is not present
        return -1;
    }
}
```
3. Ternary Search
Description: Ternary search is similar to binary search but it divides the array into three parts and checks which part the target might lie in. It's used less frequently than binary search.
Time Complexity: O(log₃ n)
Space Complexity: O(1)

```
public class TernarySearch {
    
    // Function to perform ternary search
    public int ternarySearch(int[] arr, int target, int left, int right) {
        if (right >= left) {
            // Find the two mid points
            int mid1 = left + (right - left) / 3;
            int mid2 = right - (right - left) / 3;

            // Check if the target is at any mid
            if (arr[mid1] == target) return mid1;
            if (arr[mid2] == target) return mid2;

            // Narrow down the search to one of the three regions
            if (target < arr[mid1]) {
                return ternarySearch(arr, target, left, mid1 - 1);
            } else if (target > arr[mid2]) {
                return ternarySearch(arr, target, mid2 + 1, right);
            } else {
                return ternarySearch(arr, target, mid1 + 1, mid2 - 1);
            }
        }
        // Target is not present
        return -1;
    }
}

```

4. Jump Search
Description: Jump search works by jumping ahead by fixed steps and then performing a linear search within that block. The optimal step size is √n.
Time Complexity: O(√n)
Space Complexity: O(1)

```
public class JumpSearch {
    
    // Function to perform jump search
    public int jumpSearch(int[] arr, int target) {
        int n = arr.length;
        int step = (int) Math.sqrt(n);  // Optimal step size
        
        int prev = 0;
        // Jump through the array
        while (arr[Math.min(step, n) - 1] < target) {
            prev = step;
            step += (int) Math.sqrt(n);
            if (prev >= n) return -1;  // If target is greater than the largest element
        }

        // Perform linear search within the block
        while (arr[prev] < target) {
            prev++;
            if (prev == Math.min(step, n)) return -1;
        }
        
        if (arr[prev] == target) return prev;
        return -1;  // Element not found
    }
}
```

5. Exponential Search
Description: Exponential search starts by finding the range where the element could exist by doubling the range, and then performs a binary search within that range.
Time Complexity: O(log n) (for binary search)
Space Complexity: O(1)

```
public class ExponentialSearch {

    // Function to perform binary search within the range
    public int binarySearch(int[] arr, int left, int right, int target) {
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) return mid;
            if (arr[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }

    // Function to perform exponential search
    public int exponentialSearch(int[] arr, int target) {
        int n = arr.length;

        // Check if target is at the first position
        if (arr[0] == target) return 0;

        // Find the range by doubling the index
        int i = 1;
        while (i < n && arr[i] <= target) i *= 2;

        // Perform binary search in the found range
        return binarySearch(arr, i / 2, Math.min(i, n - 1), target);
    }
}
```

6. Fibonacci Search
Description: Fibonacci search is based on dividing the array using Fibonacci numbers. It narrows the range of possible locations for the target in a manner similar to binary search.
Time Complexity: O(log n)
Space Complexity: O(1)

```
public class FibonacciSearch {

    // Function to perform Fibonacci search
    public int fibonacciSearch(int[] arr, int target) {
        int n = arr.length;
        int fibM2 = 0;  // (m-2)'th Fibonacci number
        int fibM1 = 1;  // (m-1)'th Fibonacci number
        int fibM = fibM2 + fibM1;  // m'th Fibonacci number

        // Find the smallest Fibonacci number greater than or equal to n
        while (fibM < n) {
            fibM2 = fibM1;
            fibM1 = fibM;
            fibM = fibM1 + fibM2;
        }

        int offset = -1;  // Marks the eliminated range from the front

        // While there are elements to be checked
        while (fibM > 1) {
            int i = Math.min(offset + fibM2, n - 1);

            // If target is greater than the value at index i, cut the subarray after i
            if (arr[i] < target) {
                fibM = fibM1;
                fibM1 = fibM2;
                fibM2 = fibM - fibM1;
                offset = i;
            }
            // If target is less than the value at index i, cut the subarray before i
            else if (arr[i] > target) {
                fibM = fibM2;
                fibM1 = fibM1 - fibM2;
                fibM2 = fibM - fibM1;
            }
            // Element found
            else return i;
        }

        // Check if the last element is the target
        if (fibM1 == 1 && arr[offset + 1] == target) return offset + 1;
        return -1;  // Element not found
    }
}
```

