---
layout: post
title: "Algorithm and Data Structure"
category: jekyll update
---

### Algorithm

#### Complexity
- Big(O) - upper bound
- Big Omega - lower bound
- Big theta - both upper and lower bound that is to say tight bound

amortized time → it is a way to express that an algorithm have a very bad time complexity once in a while but most of the time it have a different and less bad time complexity. A dynamically resizable list have O(2X) for X number of insertions but amortized time for each insertion is O(1).

some notes - 
- drop the constant →  Big O describes the rate of increase and thus any constant can be dropped. O(2N) ~ O(N)
- drop non-dominant terms →  for example O(N^2 + N^2) will be O(N^2) so it is logical that O(N^2 + N) will be O(N^2). But not all sums are not shorted this way, for example O(A^2 + B) - B cannot be dropped without knowledge of A and B.  

Best case, worst case and expected case

#### Search
##### Binary Search
Be careful of determining the middle point. If we use floor -
{% highlight c %}
binarySearch(int low, int high){
  int middle = (low + high) / 2;
  if(..) low = middle + 1;
  else high = middle;
}
{% endhighlight %}

On the other hand if we use ceil - 
{% highlight c %}
binarySearch(int low, int high){
  int middle = ceil((low + high) / 2.0);
  if(..) low = middle;
  else high = middle - 1;
}
{% endhighlight %}

#### Sorting
##### Quick Sort
##### Merge Sort
##### Heap Sort
##### Bubble Sort
##### Insertion Sort

### Data Structure
#### String
substring → contiguous sequence of characters within an array.

#### Array
#### Hash Table
Collision Resolution → 1. Open Addressing 2. Separate Chaining 

{% highlight c %}
unordered_multimap<int, int> ummap;

ummap.insert(pair<int, int>(1, 100));
ummap.insert(pair<int, int>(1, 110));
ummap.insert(pair<int, int>(2, 200));
ummap.insert(pair<int, int>(2, 225));

pair<unordered_multimap<int, int>::iterator, unordered_multimap<int, int>::iterator> ret;
ret = ummap.equal_range(1);
unordered_multimap<int, int> it;
for(it = ret.first; it != ret.second; it++) cout << it->second;
{% endhighlight %}