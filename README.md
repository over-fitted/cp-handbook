# cp-handbook
notes taken from the CP handbook https://cses.fi/book/book.pdf

## Binary Search
Only works with sorted lists

# method 1
Find middle, then reduce the search field to either everything above or below, then repeat
The focus is on changing the seach field with the middle being calculated each time
'''cpp
int a = 0, b = n-1;
while (a <= b) {
  int k = (a+b)/2;
  if (array[k] == x) {// x found at index k}
  if (array[k] > x) b = k-1;
  else a = k+1;
}
'''
O(logn)

# method 2
1) jump from start to middle of array, then halve the jump size
2) if current value > target, jump from start again, else change start location to here and jump again
3) repeat till jump size = 0 (not in array) or found

'''cpp
int k = 0;
for (int b = n/2; b >= 1; b /= 2) {
  while (k+b < n && array[k+b] <= x) k += b;
}
if (array[k] == x) {// x found at index k}
'''
