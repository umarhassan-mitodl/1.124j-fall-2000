---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Sorting
uid: 99a23bcb-0d8c-e738-f2e1-2cf8e3a06179
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Introduction](#Introduction)
2.  [Performance Criteria](#Performance)
3.  [Selection Sort](#Selection)
4.  [Insertion Sort](#Insertion)
5.  [Shell Sort](#Shell)
6.  [Quicksort](#Quick)
7.  [Choosing a Sorting Algorithm](#Algorithm)

{{< anchor "Introduction" >}}{{< /anchor >}}1\. Introduction
------------------------------------------------------------

Sorting techniques have a wide variety of applications. Computer-Aided Engineering systems often use sorting algorithms to help reason about geometric objects, process numerical data, rearrange lists, etc. In general, therefore, we will be interested in sorting a set of _records_ containing _keys_, so that the keys are ordered according to some well defined ordering rule, such as numerical or alphabetical order. Often, the keys will form only a small part of the record. In such cases, it will usually be more efficient to sort a list of keys without physically rearranging the records.

{{< anchor "Performance" >}}{{< /anchor >}}2\. Performance Criteria
-------------------------------------------------------------------

There are several criteria to be used in evaluating a sorting algorithm:

*   _Running time_. Typically, an elementary sorting algorithm requires _O(N{{< sup "2" >}})_ steps to sort _N_ randomly arranged items. More sophisticated sorting algorithms require _O(N log N)_ steps on average. Algorithms differ in the constant that appears in front of the _N{{< sup "2" >}}_ or _N log N_. Furthermore, some sorting algorithms are more sensitive to the nature of the input than others. Quicksort, for example, requires _O(N log N)_ time in the average case, but requires _O(N{{< sup "2" >}})_ time in the worst case. 
*   _Memory requirements_. The amount of extra memory required by a sorting algorithm is also an important consideration. _In place_ sorting algorithms are the most memory efficient, since they require practically no additional memory. _Linked list_ representations require an additional _N_ words of memory for a list of pointers. Still other algorithms require sufficent memory for another copy of the input array. These are the most inefficient in terms of memory usage. 
*   _Stability_. This is the ability of a sorting algorithm to preserve the relative order of equal keys in a file.

Examples of elementary sorting algorithms are: selection sort, insertion sort, shell sort and bubble sort. Examples of sophisticated sorting algorithms are quicksort, radix sort, heapsort and mergesort. We will consider a selection of these algorithms which have widespread use. In the algorithms given below, we assume that the array to be sorted is stored in the memory locations _a\[1\],a\[2\],...,a\[N\]_. The memory location _a\[0\]_ is reserved for special keys called _sentinels_, which are described below.

{{< anchor "Selection" >}}{{< /anchor >}}3\. Selection Sort
-----------------------------------------------------------

This "brute force'' method is one of the simplest sorting algorithms.

Approach
--------

*   Find the smallest element in the array and exchange it with the element in the first position.
*   Find the second smallest element in the array and exchange it with the element in the second position.
*   Continue this process until done.

Here is the code for selection sort:

**Selection.cpp**

_#include "Selection.h"     // Typedefs ItemType._

_inline void swap(ItemType a\[\], int i, int j) {_  
 _ItemType t = a\[i\];_  
 _a\[i\] = a\[j\];_  
 _a\[j\] = t;_  
_}_

_void selection(ItemType a\[\], int N) {_  
 _int i, j, min;_

 _for (i = 1; i \< N; i++) {_  
 _min = i;_  
 _for (j = i+1; j \<= N; j++)_  
 _if (a\[j\] \< a\[min\])_  
 _min = j;_  
 _swap(a,min,i);_  
 _}_  
_}_

Selection sort is easy to implement; there is little that can go wrong with it. However, the method requires _O(N{{< sup "2" >}})_ comparisons and so it should only be used on small files. There is an important exception to this rule. When sorting files with large records and small keys, the cost of exchanging records controls the running time. In such cases, selection sort requires _O(N_) time since the number of exchanges is at most _N_.

{{< anchor "Insertion" >}}{{< /anchor >}}4\. Insertion Sort
-----------------------------------------------------------

This is another simple sorting algorithm, which is based on the principle used by card players to sort their cards.

Approach
--------

*   Choose the second element in the array and place it in order with respect to the first element.
*   Choose the third element in the array and place it in order with respect to the first two elements.
*   Continue this process until done.

Insertion of an element among those previously considered consists of moving larger elements one position to the right and then inserting the element into the vacated position.

Here is the code for insertion sort:

**Insertion.cpp**

_#include "Insertion.h"         // Typedefs ItemType._

_void insertion(ItemType a\[\], int N) {_  
 _int i, j;_  
 _ItemType v;_

 _for (i = 2; i \<= N; i++) {_  
 _v = a\[i\];_  
 _j = i;_  
 _while (a\[j-1\] > v) {_  
 _a\[j\] = a\[j-1\];_  
 _j--;_  
 _}_  
 _a\[j\] = v;_  
 _}_  
_}_

It is important to note that there is no test in the while loop to prevent the index _j_ from running out of bounds. This could happen if _v_ is smaller than _a\[1\],a\[2\],...,a\[i-1\]_. To remedy this situation, we place a _sentinel_ key in _a\[0\]_, making it at least as small as the smallest element in the array. The use of a sentinel is more efficient than performing a test of the form _while (j > 1 &&  a\[j-1\] > v)_. Insertion sort is an _O(N{{< sup "2" >}})_ method both in the average case and in the worst case. For this reason, it is most effectively used on files with roughly _N \< 20_. However, in the special case of an almost sorted file, insertion sort requires only _linear_ time.

{{< anchor "Shell" >}}{{< /anchor >}}5\. Shell Sort
---------------------------------------------------

This is a simple, but powerful, extension of insertion sort, which gains speed by allowing exchanges of _non-adjacent_ elements.

Definition
----------

An _h-sorted_ file is one with the property that taking every _h_th element (starting anywhere) yields a sorted file.

Approach
--------

*   Choose an initial large step size, _h{{< sub "K" >}}_, and use insertion sort to produce an _h{{< sub "K" >}}_\-sorted file.
*   Choose a smaller step size, _h{{< sub "K-1" >}}_, and use insertion sort to produce an _h{{< sub "K-1" >}}_\-sorted file, using the _h{{< sub "K" >}}_\-sorted file as input.
*   Continue this process until done. The last stage uses insertion sort, with a step size _h{{< sub "1" >}} = 1_, to produce a sorted file.

Each stage in the sorting process brings the elements closer to their final positions. The method derives its efficiency from the fact that insertion sort is able to exploit the order present in a partially sorted input file; input files with more order to them require a smaller number of exchanges. It is important to choose a good sequence of increments. A commonly used sequence is _(3{{< sup "K" >}}\-1)/2,...,121,40,13,4,1_, which is obtained from the recurrence _h{{< sub "k" >}} = 3 h{{< sub "k+1" >}}+1_. Note that the sequence obtained by taking powers of 2 leads to bad performance because elements in odd positions are not compared with elements in even positions until the end.

Here is the complete code for shell sort:

**Shell.cpp**

_#include "Shell.h"         // Typedefs ItemType._

_void shell(ItemType a\[\], int N) {_  
 _int i, j, h;_  
 _ItemType v;_

 _for (h = 1; h \< = N/9; h = 3\*h+1);_

 _for (; h > 0; h /= 3)_  
 _for (i = h+1; i \<= N; i++) {_  
 _v = a\[i\];_  
 _j = i;_  
 _while (j > h && a\[j-h\] > v) {_  
 _a\[j\] = a\[j-h\];_  
 _j -= h;_  
 _}_  
 _a\[j\] = v;_  
 _}_  
_}_

Shell sort requires _O(N{{< sup "3/2" >}})_ operations in the worst case, which means that it can be quite effectively used even for moderately large files (say _N \< 5000_).

{{< anchor "Quick" >}}{{< /anchor >}}6\. Quicksort
--------------------------------------------------

This _divide and conquer_ algorithm is, in the average case, the fastest known sorting algorithm for large values of _N_. Quicksort is a good general purpose method in that it can be used in a variety of situations. However, some care is required in its implementation. Since the algorithm is based on recursion, we assume that the array (or subarray) to be sorted is stored in the memory locations _a\[left\],a\[left+1\],...,a\[right\]_. In order to sort the full array, we simply initialize the algorithm with _left = 1_ and _right = N_.

Approach
--------

*   Partition the subarray _a\[left\],a\[left+1\],...,a\[right\]_ into two parts, such that
    *   element _a\[i\]_ is in its final place in the array for some _i_ in the interval _\[left,right\]_.
    *   none of the elements in _a\[left\],a\[left+1\],...,a\[i-1\]_ are greater than _a\[i\]_.
    *   none of the elements in _a\[i+1\],a\[i+2\],...,a\[right\]_ are less than _a\[i\]_.
*   Recursively partition the two subarrays, _a\[left\],a\[left+1\],...,a\[i-1\]_ and _a\[i+1\],a\[i+2\],...,a\[right\]_, until the entire array is sorted.

How to partition the subarray _a\[left\],a\[left+1\],...,a\[right\]_:

*   Choose _a\[right\]_ to be the element that will go into its final position.
*   Scan from the left end of the subarray until an element greater than _a\[right\]_ is found.
*   Scan from the right end of the subarray until an element less than _a\[right\]_ is found.
*   Exchange the two elements which stopped the scans.
*   Continue the scans in this way. Thus, all the elements to the left of the left scan pointer will be less than _a\[right\]_ and all the elements to the right of the right scan pointer will be greater than _a\[right\]_.
*   When the scan pointers cross we will have two new subarrays, one with elements less than _a\[right\]_ and the other with elements greater than _a\[right\]_. We may now put _a\[right\]_ in its final place by exchanging it with the _leftmost_ element in the right subarray.

Here is the complete code for quicksort:

**Quicksort.cpp**

_// inline void swap() is the same as for selection sort._

_void quicksort(ItemType a\[\], int left, int right) {_  
 _int i, j;_  
 _ItemType v;_

 _if (right > left) {_  
 _v = a\[right\];_  
 _i = left - 1;_  
 _j = right;_  
 _for (;;) {_  
 _while (a\[++i\] \< v);_  
 _while (a\[--j\] > v);_  
 _if (i >= j) break;_  
 _swap(a,i,j);_  
 _}_  
 _swap(a,i,right);_  
 _quicksort(a,left,i-1);_  
 _quicksort(a,i+1,right);_  
 _}_  
_}_

Note that this code requires a sentinel key in _a\[0\]_ to stop the right-to-left scan in case the partitioning element is the smallest element in the file. Quicksort requires _O(N log N)_ operations in the average case. However, its worst case performance is O(N{{< sup "2" >}}), which occurs in the case of an already sorted file! There are a number of improvements which can be made to the basic quicksort algorithm.  
 

*   Using the _median of three_ partitioning method makes the worst case far less probable, and it eliminates the need for sentinels. The basic idea is as follows. Choose three elements, _a\[left\]_, _a\[middle\]_ and _a\[right\]_, from the left, middle and right of the array. Sort them (by direct comparison) so that the median of the three is in _a\[middle\]_ and the largest is in _a\[right\]_. Now exchange _a\[middle\]_ with _a\[right-1\]_. Finally, we run the partitioning algorithm on the subarray _a\[left+1\],a\[left+2\],...,a\[right-2\]_ with _a\[right-1\]_ as the partitioning element.
*   Another improvement is to _remove recursion_ from the algorithm by using an explicit stack. The basic idea is as follows. After partitioning, push the larger subfile onto the stack. The smaller subfile is processed immediately by simply resetting the parameters _left_ and _right_ (this is known as _end-recursion removal_). With the explicit stack implementation, the maximum stack size is about _log{{< sub "2" >}} N_. On the other hand, with the recursive implementation, the underlying stack could be as large as _N_.
*   A third improvement is to use a cutoff to insertion sort whenever small subarrays are encountered. This is because insertion sort, albeit an _O(N{{< sup "2" >}})_ algorithm, has a sufficiently small constant in front of the _N{{< sup "2" >}}_ to be more efficient than quicksort for small _N_. A suitable value for the cutoff subarray size would be approximately in the range _5  ~ 25_.

{{< anchor "Algorithm" >}}{{< /anchor >}}7\. Choosing a Sorting Algorithm
-------------------------------------------------------------------------

Table 1 summarizes the performance characteristics of some common sorting algorithms. Shell sort is usually a good starting choice for moderately large files _N \< 5000_, since it is easily implemented. Bubble sort, which is included in Table 1 for comparison purposes only, is generally best avoided. Insertion sort requires linear time for _almost sorted_ files, while selection sort requires linear time for files with large records and small keys. Insertion sort and selection sort should otherwise be limited to small files. Quicksort is the method to use for very large sorting problems. However, its performance may be significantly affected by subtle implementation errors. Furthermore, quicksort performs badly if the file is already sorted. Another possible disadvantage is that quicksort is not stable i.e. it does not preserve the relative order of equal keys. All of the above sorting algorithms are in-place methods. Quicksort requires a small amount of additional memory for the auxiliary stack. There are a few other sorting methods which we have not considered. Heapsort requires _O(N log N)_ steps both in the average case and the worst case, but it is about twice as slow as quicksort on average. Mergesort is another _O(N log N)_ algorithm in the average and worst cases. Mergesort is the method of choice for sorting _linked lists_, where sequential access is required.

Table 1: Approximate running times for various sorting algorithms

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
METHOD
{{< thclose >}}
{{< thopen >}}
\# COMPARISONS - AVERAGE CASE
{{< thclose >}}
{{< thopen >}}
\# COMPARISONS - WORST CASE
{{< thclose >}}
{{< thopen >}}
\# EXCHANGES - AVERAGE CASE
{{< thclose >}}
{{< thopen >}}
\# EXCHANGES - WORST CASE
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
Selection sort  
Insertion sort  
Bubble sort  
Shell sort  
Quicksort
{{< tdclose >}}
{{< tdopen >}}
N{{< sup "2" >}}/2  
N{{< sup "2" >}}/4  
N{{< sup "2" >}}/2  
~N{{< sup ".1.25" >}}  
2 N ln N   
(1.38 N log{{< sub "2" >}} N)
{{< tdclose >}}
{{< tdopen >}}
N{{< sup "2" >}}/2  
N{{< sup "2" >}}/2  
N{{< sup "2" >}}/2  
N{{< sup "3/2" >}}  
N{{< sup "2" >}}/2
{{< tdclose >}}
{{< tdopen >}}
N  
N{{< sup "2" >}}/8  
N{{< sup "2" >}}/2  
?  
N
{{< tdclose >}}
{{< tdopen >}}
N  
N{{< sup "2" >}}/4  
N{{< sup "2" >}}/2  
?  
N
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}