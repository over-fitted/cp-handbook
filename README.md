# cp-handbook
notes taken from the CP handbook https://cses.fi/book/book.pdf

# Binary Search
Only works with sorted lists

### method 1
Find middle, then reduce the search field to either everything above or below, then repeat
The focus is on changing the seach field with the middle being calculated each time
```cpp
int a = 0, b = n-1;
while (a <= b) {
  int k = (a+b)/2;
  if (array[k] == x) {// x found at index k}
  if (array[k] > x) b = k-1;
  else a = k+1;
}
```
O(logn)

### method 2
1) jump from start to middle of array, then halve the jump size
2) if current value > target, jump from start again, else change start location to here and jump again
3) repeat till jump size = 0 (not in array) or found

~~~cpp
int k = 0;
for (int b = n/2; b >= 1; b /= 2) {
  while (k+b < n && array[k+b] <= x) k += b;
}
if (array[k] == x) {// x found at index k}
~~~

# Finding all subsets

### method 1 - backtracking
1) create recursive function with parameters (input_array, current_index, current_subset)
2) if current index == input_array.size(), process current_subset
3) process the 2 possibilities in steps 4-5 which are to ignore the current element, or to add it into the subset
4) to ignore the current element, call recursive function on the current_index + 1
  a) first iteration should ignore all elements and have current_subset be {}
5) to add the current element, do current_subset.push_back(current_element), then call recursive function on the current_index+1
  a) second iteration should only have the last element pushed into the subset, with all the previous indexes choosing to ignore their elements
6) cleanup - remove current element with current_subset.pop_back(), then resolve the current recursive call
``` C++
void search(int k) {
  if (k == n) {
    // process subset
  } else {
    search(k+1);
    subset.push_back(k);
    search(k+1);
    subset.pop_back();
  }
}
```
