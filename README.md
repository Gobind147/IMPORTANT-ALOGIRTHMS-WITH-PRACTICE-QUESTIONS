# IMPORTANT-ALOGIRTHMS-WITH-PRACTICE-QUESTIONS
# TOPIC COVERED
1. Sorting
2. Searching
3. Tree
4. 

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

| Problem Number | Title                                                   |
|----------------|---------------------------------------------------------|
| 1346           | Check if N and its Double Exist                          |
| 202            | Happy Number                                             |
| 4              | Median of Two Sorted Arrays                              |
| 704            | Binary Search                                            |
| 33             | Search in Rotated Sorted Array                           |
| 154            | Find Minimum in Rotated Sorted Array II                  |
| 410            | Split Array Largest Sum                                  |
| 1231           | Divide Chocolate                                         |
| 350            | Intersection of Two Arrays II                            |
| 287            | Find the Duplicate Number                                |
| 352            | Data Stream as Disjoint Intervals                        |
| 367            | Valid Perfect Square                                     |
| 1060           | Missing Element in Sorted Array                          |
| 702            | Search in a Sorted Array of Unknown Size                 |
| 278            | First Bad Version                                        |
| 658            | Find K Closest Elements                                  |
| 668            | Kth Smallest Number in Multiplication Table              |



**TREE ALGORITHMS**

1. Preorder Traversal (DFS)
Description: Preorder traversal visits the root node first, then recursively visits the left subtree, and finally the right subtree.

Time Complexity: O(n), where n is the number of nodes.
Space Complexity: O(h), where h is the height of the tree (O(n) in the worst case).
```
public void preorderTraversal(TreeNode node) {
    if (node == null) return;
    // Visit the root
    preorderTraversal(node.left);
    preorderTraversal(node.right);
}
```
2. Inorder Traversal (DFS)
Description: Inorder traversal recursively visits the left subtree, then visits the root node, and finally visits the right subtree.

Time Complexity: O(n), where n is the number of nodes.
Space Complexity: O(h), where h is the height of the tree (O(n) in the worst case).
```
public void inorderTraversal(TreeNode node) {
    if (node == null) return;
    inorderTraversal(node.left);
    // Visit the root
    inorderTraversal(node.right);
}
```


3. Postorder Traversal (DFS)
Description: Postorder traversal recursively visits the left subtree, then the right subtree, and finally visits the root node.

Time Complexity: O(n), where n is the number of nodes.
Space Complexity: O(h), where h is the height of the tree (O(n) in the worst case).
```
public void postorderTraversal(TreeNode node) {
    if (node == null) return;
    postorderTraversal(node.left);
    postorderTraversal(node.right);
    // Visit the root
}
```
4. Level Order Traversal (BFS)
Description: Level-order traversal visits nodes level by level from left to right, using a queue.

Time Complexity: O(n), where n is the number of nodes.
Space Complexity: O(n) (queue size can be up to the number of nodes).
```
public void levelOrderTraversal(TreeNode node) {
    if (node == null) return;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(node);

    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        if (current.left != null) queue.add(current.left);
        if (current.right != null) queue.add(current.right);
    }
}
```
5. Binary Search Tree (BST) - Insertion
Description: Insertion in a BST follows the rule that left children are smaller than the parent and right children are larger.

Time Complexity: O(h), where h is the height of the tree.
Space Complexity: O(h), for the recursive stack.
```
public TreeNode insertIntoBST(TreeNode root, int key) {
    if (root == null) return new TreeNode(key);
    if (key < root.val) root.left = insertIntoBST(root.left, key);
    else root.right = insertIntoBST(root.right, key);
    return root;
}
```
6. Binary Search Tree (BST) - Deletion
Description: Deletion in a BST involves three cases: removing a node with no children, one child, or two children. In the case of two children, the inorder successor (smallest in the right subtree) replaces the deleted node.

Time Complexity: O(h), where h is the height of the tree.
Space Complexity: O(h), for the recursive stack.
```
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val) root.left = deleteNode(root.left, key);
    else if (key > root.val) root.right = deleteNode(root.right, key);
    else {
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode successor = findMin(root.right);
        root.val = successor.val;
        root.right = deleteNode(root.right, successor.val);
    }
    return root;
}

private TreeNode findMin(TreeNode node) {
    while (node.left != null) node = node.left;
    return node;
}
```
7. Binary Search Tree (BST) - Search
Description: Searching in a BST follows the rule of checking the left subtree if the target is smaller and the right subtree if the target is larger.

Time Complexity: O(h), where h is the height of the tree.
Space Complexity: O(h), for the recursive stack.
```
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    return val < root.val ? searchBST(root.left, val) : searchBST(root.right, val);
}
```
8. Lowest Common Ancestor (LCA)
Description: The lowest common ancestor of two nodes is the deepest node that is an ancestor of both. In a BST, this can be done by recursively traversing the tree.

Time Complexity: O(h), where h is the height of the tree.
Space Complexity: O(h), for the recursive stack.
```
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return null;
    if (p.val < root.val && q.val < root.val) return lowestCommonAncestor(root.left, p, q);
    if (p.val > root.val && q.val > root.val) return lowestCommonAncestor(root.right, p, q);
    return root;
}
```
9. AVL Tree (Balanced Tree) - Insertion
Description: AVL trees are self-balancing binary search trees. After insertion, you update the balance factor and rotate if necessary.

Time Complexity: O(log n)
Space Complexity: O(log n)
```
public TreeNode insertAVL(TreeNode node, int key) {
    if (node == null) return new TreeNode(key);
    if (key < node.val) node.left = insertAVL(node.left, key);
    else if (key > node.val) node.right = insertAVL(node.right, key);

    node.height = 1 + Math.max(height(node.left), height(node.right));
    int balance = getBalance(node);

    if (balance > 1 && key < node.left.val) return rotateRight(node);
    if (balance < -1 && key > node.right.val) return rotateLeft(node);
    if (balance > 1 && key > node.left.val) {
        node.left = rotateLeft(node.left);
        return rotateRight(node);
    }
    if (balance < -1 && key < node.right.val) {
        node.right = rotateRight(node.right);
        return rotateLeft(node);
    }

    return node;
}
```
10. Segment Tree (Range Queries)
Description: Segment trees allow for efficient range queries and updates in an array.

Time Complexity: O(log n) for range queries and updates.
Space Complexity: O(n)
```
public void buildSegmentTree(int[] arr, int[] segTree, int low, int high, int pos) {
    if (low == high) {
        segTree[pos] = arr[low];
        return;
    }
    int mid = (low + high) / 2;
    buildSegmentTree(arr, segTree, low, mid, 2 * pos + 1);
    buildSegmentTree(arr, segTree, mid + 1, high, 2 * pos + 2);
    segTree[pos] = segTree[2 * pos + 1] + segTree[2 * pos + 2];
}
```
11. Fenwick Tree (Binary Indexed Tree, BIT)
Description: Fenwick Tree is used for efficiently computing prefix sums and updates.

Time Complexity: O(log n) for both updates and queries.
Space Complexity: O(n)
```
public void updateBIT(int[] BITree, int n, int index, int val) {
    index = index + 1;
    while (index <= n) {
        BITree[index] += val;
        index += index & (-index);
    }
}

public int getSumBIT(int[] BITree, int index) {
    int sum = 0;
    index = index + 1;
    while (index > 0) {
        sum += BITree[index];
        index -= index & (-index);
    }
    return sum;
}
```

| Algorithm                    | Time Complexity | Space Complexity |
|------------------------------|-----------------|------------------|
| Preorder Traversal            | O(n)            | O(h)             |
| Inorder Traversal             | O(n)            | O(h)             |
| Postorder Traversal           | O(n)            | O(h)             |
| Level Order Traversal         | O(n)            | O(n)             |
| BST - Insertion               | O(h)            | O(h)             |
| BST - Deletion                | O(h)            | O(h)             |
| BST - Search                  | O(h)            | O(h)             |
| Lowest Common Ancestor (LCA)  | O(h)            | O(h)             |
| AVL Tree - Insertion          | O(log n)        | O(log n)         |
| Segment Tree (Range Queries)  | O(log n)        | O(n)             |
| Fenwick Tree (BIT)            | O(log n)        | O(n)             |


| Problem Number | Title                                                       |
|----------------|-------------------------------------------------------------|
| 94             | Binary Tree Inorder Traversal                               |
| 144            | Binary Tree Preorder Traversal                              |
| 145            | Binary Tree Postorder Traversal                             |
| 102            | Binary Tree Level Order Traversal                           |
| 700            | Search in a Binary Search Tree                              |
| 701            | Insert into a Binary Search Tree                            |
| 450            | Delete Node in a BST                                        |
| 235            | Lowest Common Ancestor of a Binary Search Tree              |
| 236            | Lowest Common Ancestor of a Binary Tree                     |
| 199            | Binary Tree Right Side View                                 |
| 222            | Count Complete Tree Nodes                                   |
| 337            | House Robber III                                            |
| 543            | Diameter of


**Graph**

1. Breadth-First Search (BFS)
   Description: BFS is an algorithm for traversing or searching tree or graph data structures. It starts at a given node and explores all its neighbors at the present
   depth before moving on to nodes at the next depth level.
   Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges.
   Space Complexity: O(V), for the queue and visited list.
```
import java.util.*;

public void BFS(int start, List<List<Integer>> graph, boolean[] visited) {
    Queue<Integer> queue = new LinkedList<>();
    queue.add(start);
    visited[start] = true;
    
    while (!queue.isEmpty()) {
        int node = queue.poll();
        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                queue.add(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}
```
2. Depth-First Search (DFS)
Description: DFS is an algorithm for traversing or searching tree or graph structures. The algorithm starts at the root node and explores as far as possible along each branch before backtracking.
Time Complexity: O(V + E)
Space Complexity: O(V), for the recursion stack and visited list.
```
public void DFS(int node, List<List<Integer>> graph, boolean[] visited) {
    visited[node] = true;
    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            DFS(neighbor, graph, visited);
        }
    }
}
```
4. Dijkstra’s Algorithm (Single Source Shortest Path)
Description: Dijkstra’s algorithm finds the shortest path from a source node to all other nodes in a graph with non-negative edge weights.
Time Complexity: O((V + E) log V), with a priority queue.
Space Complexity: O(V), for the distance array and priority queue.
```
import java.util.*;

public int[] dijkstra(int V, List<List<int[]>> graph, int src) {
    int[] dist = new int[V];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;

    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.add(new int[] {src, 0});

    while (!pq.isEmpty()) {
        int[] current = pq.poll();
        int node = current[0];
        int currDist = current[1];

        if (currDist > dist[node]) continue;

        for (int[] neighbor : graph.get(node)) {
            int nextNode = neighbor[0];
            int edgeWeight = neighbor[1];
            if (dist[node] + edgeWeight < dist[nextNode]) {
                dist[nextNode] = dist[node] + edgeWeight;
                pq.add(new int[] {nextNode, dist[nextNode]});
            }
        }
    }

    return dist;
}
```
4. Bellman-Ford Algorithm (Single Source Shortest Path with Negative Weights)
Description: The Bellman-Ford algorithm computes the shortest paths from a single source vertex to all other vertices in a weighted graph. It handles negative weight edges.
Time Complexity: O(V * E)
Space Complexity: O(V), for the distance array.
```
public int[] bellmanFord(int V, List<int[]> edges, int src) {
    int[] dist = new int[V];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;

    for (int i = 1; i < V; i++) {
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
            }
        }
    }

    // Check for negative-weight cycles
    for (int[] edge : edges) {
        int u = edge[0];
        int v = edge[1];
        int weight = edge[2];
        if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
            System.out.println("Graph contains negative-weight cycle");
            return null;
        }
    }

    return dist;
}
```
5. Floyd-Warshall Algorithm (All-Pairs Shortest Path)
Description: Floyd-Warshall algorithm is used for finding the shortest paths between all pairs of vertices in a weighted graph.
Time Complexity: O(V³)
Space Complexity: O(V²), for the distance matrix.
```
public int[][] floydWarshall(int V, int[][] graph) {
    int[][] dist = new int[V][V];

    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != Integer.MAX_VALUE && dist[k][j] != Integer.MAX_VALUE) {
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }

    return dist;
}
```
7. Kruskal’s Algorithm (Minimum Spanning Tree)
Description: Kruskal’s algorithm finds the minimum spanning tree by sorting all edges and adding them to the tree if they don’t form a cycle.
Time Complexity: O(E log E), because of sorting edges.
Space Complexity: O(V), for storing the parent and rank arrays for the union-find.
```
public int kruskal(int V, List<int[]> edges) {
    Collections.sort(edges, (a, b) -> a[2] - b[2]);
    UnionFind uf = new UnionFind(V);
    int mstWeight = 0;

    for (int[] edge : edges) {
        int u = edge[0];
        int v = edge[1];
        int weight = edge[2];
        if (uf.find(u) != uf.find(v)) {
            uf.union(u, v);
            mstWeight += weight;
        }
    }

    return mstWeight;
}
```
7. Prim’s Algorithm (Minimum Spanning Tree)
Description: Prim’s algorithm constructs a minimum spanning tree by starting with an arbitrary vertex and growing the tree one edge at a time.
Time Complexity: O((V + E) log V), using a priority queue.
Space Complexity: O(V), for the priority queue and visited array.
```
public int prims(int V, List<List<int[]>> graph) {
    boolean[] visited = new boolean[V];
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.add(new int[]{0, 0});  // start from node 0 with 0 cost
    int mstWeight = 0;

    while (!pq.isEmpty()) {
        int[] current = pq.poll();
        int node = current[0];
        int weight = current[1];

        if (visited[node]) continue;
        visited[node] = true;
        mstWeight += weight;

        for (int[] neighbor : graph.get(node)) {
            if (!visited[neighbor[0]]) {
                pq.add(neighbor);
            }
        }
    }

    return mstWeight;
}
```
8. Topological Sort
Description: Topological Sort is used for ordering the vertices of a directed acyclic graph (DAG). It orders the vertices such that for every directed edge (u, v), vertex u comes before vertex v.
Time Complexity: O(V + E)
Space Complexity: O(V), for the recursion stack and visited array.
```
public void topologicalSort(int node, List<List<Integer>> graph, boolean[] visited, Stack<Integer> stack) {
    visited[node] = true;
    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            topologicalSort(neighbor, graph, visited, stack);
        }
    }
    stack.push(node);
}
```
10. Tarjan’s Algorithm (Strongly Connected Components)
Description: Tarjan’s Algorithm finds all strongly connected components in a directed graph.
Time Complexity: O(V + E)
Space Complexity: O(V), for the stack, low-link, and discovery arrays.
```
public void tarjanSCC(int u, int[] disc, int[] low, Stack<Integer> stack, boolean[] stackMember, List<List<Integer>> graph) {
    static int time = 0;
    disc[u] = low[u] = ++time;
    stack.push(u);
    stackMember[u] = true;

    for (int v : graph.get(u)) {
        if (disc[v] == -1) {
            tarjanSCC(v, disc, low, stack, stackMember, graph);
            low[u] = Math.min(low[u], low[v]);
        } else if (stackMember[v]) {
            low[u] = Math.min(low[u], disc[v]);
        }
    }

    if (low[u] == disc[u]) {
        while (stack.peek() != u) {
            int w = stack.pop();
            stackMember[w] = false;
        }
        stack.pop();
        stackMember[u] = false;
    }
}
```
10. Kosaraju’s Algorithm (Strongly Connected Components)
Description: Kosaraju’s algorithm is another method for finding strongly connected components by performing two passes of DFS.
Time Complexity: O(V + E)
Space Complexity: O(V), for the visited array and the stack.
```
public void kosarajuDFS(int node, List<List<Integer>> graph, boolean[] visited, Stack<Integer> stack) {
    visited[node] = true;
    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            kosarajuDFS(neighbor, graph, visited, stack);
        }
    }
    stack.push(node);
}

public void reverseDFS(int node, List<List<Integer>> reverseGraph, boolean[] visited) {
    visited[node] = true;
    for (int neighbor : reverseGraph.get(node)) {
        if (!visited[neighbor]) {
            reverseDFS(neighbor, reverseGraph, visited);
        }
    }
}
```
11. Union-Find (Disjoint Set Union, DSU)
Description: Union-Find is a data structure that supports union and find operations efficiently. It’s used for detecting cycles in a graph, particularly in Kruskal’s algorithm.
Time Complexity: O(α(n)), where α is the inverse Ackermann function.
Space Complexity: O(V), for the parent and rank arrays.
```
class UnionFind {
    int[] parent, rank;

    public UnionFind(int size) {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) parent[i] = i;
    }

    public int find(int node) {
        if (parent[node] != node) parent[node] = find(parent[node]);
        return parent[node];
    }

    public void union(int u, int v) {
        int rootU = find(u);
        int rootV = find(v);

        if (rootU != rootV) {
            if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU;
            } else if (rank[rootU] < rank[rootV]) {
                parent[rootU] = rootV;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++;
            }
        }
    }
}
```


Summary of Time and Space Complexities:
