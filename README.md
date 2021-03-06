# Algorithms, Part I by Princeton University (via Coursera)

This course covers the essential information that every serious programmer needs to know about algorithms and data structures, with emphasis on applications and scientific performance analysis of Java implementations. Part I covers elementary data structures, sorting, and searching algorithms. Part II focuses on graph- and string-processing algorithms.

https://www.coursera.org/learn/algorithms-part1/home/welcome

- [Order of growth](#order-of-growth)
- [Binary search](#binary-search)
- [Stack and Queue](#stack-and-queue)
    * [Stack](#stack)
    * [Queue](#queue)
- [Sorting](#sorting)
    * [Bubble sort](#bubble-sort) 
    * [Selection sort](#selection-sort)
    * [Insertion sort](#insertion-sort)
    * [Shell sort](#shell-sort)
    * [Merge sort](#merge-sort)
    * [Quick sort](#quick-sort)
- [Priority queue](#priority-queue)
    * [Binary heap](#binary-heap)
    * [Heapsort](#heapsort)
- [Symbol tables](#symbol-tables)
    * [Elementary implementations](#elementary-implementations)
    * [Binary search trees](#binary-search-trees)
    * [2-3 trees](#2-3-trees)
    * [Red black trees](#red-black-trees)
    * [B-trees](#b-trees)
- [Hash tables](#hash-tables)
    * [Separate chaining](#separate-chaining)
    * [Linnear probing](#linnear-probing)
- [Grades](#grades)


# Order of growth


![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/order1.png)

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/order2.png)


# Binary search


![bseacrh](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bsearch.png)

```
     public static int binarySearch(int[] a, int key) {
         int lo = 0, hi = a.length - 1;
         while (lo <= hi) {
             int mid = lo + (hi - lo) / 2;
 
             if (key < a[mid]) hi = mid - 1;
             
             else if (key > a[mid]) lo = mid + 1;
             
             else return mid;
         }
         return -1;
     }
    
    public static int binarySearchRecursive(int search, int[] array, int start, int end){
    
            int middle = (start + end)/2;
    
            if(end < start)
                return -1;
            
            if (search < array[middle])
                return binarySearchRecursive(search, array, start, middle - 1);
            
            if (search > array[middle])
                return binarySearchRecursive(search, array, middle + 1, end);
            
            if (search == array[middle])
                return middle;
            
            return -1;
    }
    
```

# Stack and Queue

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/s1.png)


## Stack


![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/s2.png)


```
public class LinkedStackOfStrings {
        private Node first = null;

        private class Node {
            String item;
            Node next;
        }

        public boolean isEmpty() {
            return first == null;
        }

        public void push(String item) {
            Node oldfirst = first;
            first = new Node();
            first.item = item;
            first.next = oldfirst;
        }

        public String pop() {
            String item = first.item;
            first = first.next;
            return item;
        }
    }
```


![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/s3.png)

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/s4.png)

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/s5.png)


## Queue

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/q1.png)

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/q2.png)

![order](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/q3.png)


# Sorting

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort1.png)

## Bubble sort

In bubble sort algorithm, array is traversed from first element to last element. Here, current element is compared with the next element. If current element is greater than the next element, it is swapped.

```
    static void bubbleSort(int[] arr) {  
        int n = arr.length;  
        int temp = 0;  
         for(int i=0; i < n; i++){  
                 for(int j=1; j < (n-i); j++){  
                          if(arr[j-1] > arr[j]){  
                                 //swap elements  
                                 temp = arr[j-1];  
                                 arr[j-1] = arr[j];  
                                 arr[j] = temp;  
                         }             
                 }  
         }  
    }  
````

**PROPERTIES:**

* Stable
* O(1) extra space
* O(n2) comparisons and swaps
* Adaptive: O(n) when nearly sorted

## Selection sort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort4.png)

```
/**
 * Selection sort:
 * 
 * 1. In iteration i, find index min of smallest remaining entry.
 * 2. Swap a[i] and a[min].
 */
public class SelectionSort {
    public static void sort(Comparable[] a) {
        int N = a.length;

        for (int i = 0; i < N; i++) {
            int min = i;

            for (int j = i + 1; j < N; j++)
                if (less(a[j], a[min]))
                    min = j;

            exchange(a, i, min);
        }
    }
}
```

From the comparions presented here, one might conclude that selection sort should never be used. It does not adapt to the data in any way (notice that the four animations above run in lock step), so its runtime is always quadratic.

However, selection sort has the property of minimizing the number of swaps. In applications where the cost of swapping items is high, selection sort very well may be the algorithm of choice.

**PROPERTIES:**

* Not stable
* O(1) extra space
* Θ(n2) comparisons
* Θ(n) swaps
* Not adaptive

https://www.toptal.com/developers/sorting-algorithms/selection-sort

## Insertion sort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/sort7.png)

```
/**
 * In iteration i, swap a[i] with each larger entry to its left.
 */
public class InsertionsSort {
    public static void sort(Comparable[] a) {
        int N = a.length;
        
        for (int i = 0; i < N; i++)
            
            for (int j = i; j > 0; j--)
                if (less(a[j], a[j - 1]))
                    exchange(a, j, j - 1);
                else break;
    }
}
```
Although it is one of the elementary sorting algorithms with O(n2) worst-case time, insertion sort is the algorithm of choice either when the data is nearly sorted (because it is adaptive) or when the problem size is small (because it has low overhead).

For these reasons, and because it is also stable, insertion sort is often used as the recursive base case (when the problem size is small) for higher overhead divide-and-conquer sorting algorithms, such as merge sort or quick sort

**PROPERTIES:**

* Stable
* O(1) extra space
* O(n2) comparisons and swaps
* Adaptive: O(n) time when nearly sorted
* Very low overhead

https://www.toptal.com/developers/sorting-algorithms/insertion-sort

## Shell sort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/shell1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/shell2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/shell3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/shell4.png)

The worse-case time complexity of shell sort depends on the increment sequence. For the increments 1 4 13 40 121…, which is what is used here, the time complexity is O(n3/2). For other increments, time complexity is known to be O(n4/3) and even O(n·lg2(n)). Neither tight upper bounds on time complexity nor the best increment sequence are known.

Because shell sort is based on insertion sort, shell sort inherits insertion sort’s adaptive properties. The adapation is not as dramatic because shell sort requires one pass through the data for each increment, but it is significant. For the increment sequence shown above, there are log3(n) increments, so the time complexity for nearly sorted data is O(n·log3(n)).

Because of its low overhead, relatively simple implementation, adaptive properties, and sub-quadratic time complexity, shell sort may be a viable alternative to the O(n·lg(n)) sorting algorithms for some applications when the data to be sorted is not very large.

**PROPERTIES:**

* Not stable
* O(1) extra space
* O(n3/2) time as shown (see below)
* Adaptive: O(n·lg(n)) time when nearly sort

https://www.toptal.com/developers/sorting-algorithms/shell-sort


## Merge sort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/merge7.png)

Merge sort is very predictable. It makes between 0.5lg(n) and lg(n) comparisons per element, and between lg(n) and 1.5lg(n) swaps per element. The minima are achieved for already sorted data; the maxima are achieved, on average, for random data. If using Θ(n) extra space is of no concern, then merge sort is an excellent choice: It is simple to implement, and it is the only stable O(n·lg(n)) sorting algorithm. Note that when sorting linked lists, merge sort requires only Θ(lg(n)) extra space (for recursion).

Merge sort is the algorithm of choice for a variety of situations: when stability is required, when sorting linked lists, and when random access is much more expensive than sequential access (for example, external sorting on tape).

There do exist linear time in-place merge algorithms for the last step of the algorithm, but they are both expensive and complex. The complexity is justified for applications such as external sorting when Θ(n) extra space is not available.

**PROPERTIES:**

* Stable
* Θ(n) extra space for arrays (as shown)
* Θ(lg(n)) extra space for linked lists
* Θ(n·lg(n)) time
* Not adaptive
* Does not require random access to data

https://www.toptal.com/developers/sorting-algorithms/merge-sort

## Quick sort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick7.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick8.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/quick9.png)


When carefully implemented, quick sort is robust and has low overhead. When a stable sort is not needed, quick sort is an excellent general-purpose sort – although the 3-way partitioning version should always be used instead.

The 2-way partitioning code shown above is written for clarity rather than optimal performance; it exhibits poor locality, and, critically, exhibits O(n2) time when there are few unique keys. A more efficient and robust 2-way partitioning method is given in Quicksort is Optimal by Robert Sedgewick and Jon Bentley. The robust partitioning produces balanced recursion when there are many values equal to the pivot, yielding probabilistic guarantees of O(n·lg(n)) time and O(lg(n)) space for all inputs.

With both sub-sorts performed recursively, quick sort requires O(n) extra space for the recursion stack in the worst case when recursion is not balanced. This is exceedingly unlikely to occur, but it can be avoided by sorting the smaller sub-array recursively first; the second sub-array sort is a tail recursive call, which may be done with iteration instead. With this optimization, the algorithm uses O(lg(n)) extra space in the worst case.

**PROPERTIES:**

* Not stable
* O(lg(n)) extra space (see discussion)
* O(n2) time, but typically O(n·lg(n)) time
* Not adaptive

# Priority queue

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/pr1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/pr2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/pr3.png)

## Binary heap

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh7.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bh8.png)

## Heapsort

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/hs1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/hs2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/hs3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/hs5.png)

Heap sort is simple to implement, performs an O(n·lg(n)) in-place sort, but is not stable.

The first loop, the Θ(n) “heapify” phase, puts the array into heap order. The second loop, the O(n·lg(n)) “sortdown” phase, repeatedly extracts the maximum and restores heap order.

The sink function is written recursively for clarity. Thus, as shown, the code requires Θ(lg(n)) space for the recursive call stack. However, the tail recursion in sink() is easily converted to iteration, which yields the O(1) space bound.

Both phases are slightly adaptive, though not in any particularly useful manner. In the nearly sorted case, the heapify phase destroys the original order. In the reversed case, the heapify phase is as fast as possible since the array starts in heap order, but then the sortdown phase is typical. In the few unique keys case, there is some speedup but not as much as in shell sort or 3-way quicksort.

**PROPERTIES:**

* Not stable
* O(1) extra space (see discussion)
* O(n·lg(n)) time
* Not really adaptive

# Symbol tables

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st2.png)

## Elementary implementations

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/st7.png)

## Binary search trees

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bst7.png)

## 2-3 trees

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t5.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t7.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/2-3t8.png)

## Red black trees

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/rbt1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/rbt2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/rbt3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/rbt4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/rbt5.png)

## B trees

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bt1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bt2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/bt3.png)

# Hash tables

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht1.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht2.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht3.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht4.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht5.png)

## Separate chaining

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht6.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht7.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht8.png)

## Linear probing

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht9.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht10.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht11.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht12.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht13.png)

![sort](https://github.com/rgederin/coursera-algorithms-first/blob/master/img/ht14.png)

# Grades

5/5 Assignments Passed
94.8% Final Grade

  1. Union-Find -                     Programming Assignment: Percolation -       95%
  2. Stacks and Queues -              Deques and Randomized Queues -              95%
  3. Mergesort -                      Programming Assignment: Collinear Points -  97%
  4. Priority Queues -                Programming Assignment: 8 Puzzle -          87 %
  5. Geometric Applications of BSTs - Programming Assignment: Kd-Trees -          100%

