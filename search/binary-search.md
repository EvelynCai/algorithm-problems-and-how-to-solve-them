---
description: search
---

# Binary Search

### Overview

Principle: rule out half of the candidates each round.

Complexity:

* time: O\(logn\)
* space: O\(1\)

N.B.

* In most arrays, we need them to be **sorted** in \(mostly ascending\) order to rule out half of the candidates, but it's not necessary.



### Variations

**1-D: binary search in an sorted array**

```text
public int binarySearch(int[] array, int target) {
    if (array == null || array.length == 0) {
      return -1;
    }

    int left = 0;
    int right = array.length - 1;
    while (left <= right) {
      int mid = left + (right - left) / 2; // to prevent int overflow
      if (array[mid] == target) {
        return mid;
      } else if (array[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }

    return -1;
  }
```

**2-D: binary search in an sorted matrix**

N.B. the first element in each row is larger than the last element in last row.

```text
public int[] search(int[][] matrix, int target) {
    int m = matrix.length;
    int n = matrix[0].length;
    if (m == 0 && n == 0) {
      return new int[]{-1, -1};
    }

    int start = 0;
    int end = m * n - 1;
    while (start <= end) {
      int mid = start + (end - start) / 2;
      int midR = mid / n;
      int midC = mid % n;
      if (matrix[midR][midC] == target) {
        return new int[]{midR, midC};
      } else if (matrix[midR][midC] < target) {
        start = mid + 1;
      } else {
        end = mid - 1;
      }
    }

    return new int[]{-1, -1};
  }
```

**binary search the first occurence of target**

```text
public int firstOccur(int[] array, int target) {
   if (array == null || array.length == 0) {
       return -1;
   }
   
   int left = 0;
   int right = array.length - 1;
   while (left + 1 < right) { // termination condition: when left and right point to two neighbors
       int mid = left + (right - left) / 2;
       if (array[mid] == target) {
           right = mid; // look at mid's left to find the first occurence
       } else if (array[mid] < target) {
           left = mid + 1;
       } else {
           right = mid - 1;
       }
   }
   
   // validate if left/right is the first occurence
   if (array[left] == target) {
       return left;
   } else if (array[right] == target) {
       return right;
   }
   
   return -1;
 }
```

**binary search the last occurence of target**

```text
public int lastOccur(int[] array, int target) {
   if (array == null || array.length == 0) {
       return -1;
   }
   
   int left = 0;
   int right = array.length - 1;
   while (left + 1 < right) { // termination condition: when left and right point to two neighbors
       int mid = left + (right - left) / 2;
       if (array[mid] == target) {
           left = mid; // look at mid's right to find the last occurence
       } else if (array[mid] < target) {
           left = mid + 1;
       } else {
           right = mid - 1;
       }
   }
   
   // validate if right/left is the last occurence
   if (array[right] == target) {
       return right;
   } else if (array[left] == target) {
       return left;
   }
   
   return -1;
 }
```

**binary search total occurence of target**

```text
public int totalOccurrence(int[] array, int target) {
    if (array == null || array.length == 0) {
      return 0;
    }

    int first = firstOccur(array, target);
    int last = lastOccur(array, target);
    if (first == -1 || last == -1) {
      return 0;
    } else {
      return last - first + 1;
    }
}
```

**binary search the closest element of target**

```text
public int closest(int[] array, int target) {
    if (array == null || array.length == 0) {
      return -1;
    }

    int left = 0;
    int right = array.length - 1;
    while (left + 1 < right) {
      int mid = left + (right - left) / 2;
      if (target == array[mid]) {
        return mid;
      } else if (array[mid] < target) {
        left = mid;
      } else {
        right = mid;
      }
    }

    if (Math.abs(array[left] - target) < Math.abs(array[right] - target)) {
      return left;
    } else {
      return right;
    }
}
```

**binary search the closest k elements of target**

```text
public int[] kClosest(int[] array, int target, int k) {
    if (array.length == 0 || k == 0) {
      return new int[]{};
    }
    
    int closestIndex = closest(array, target);
    int[] res = new int[k];
    int i = 0;
    res[i++] = array[closestIndex];

    int left = closestIndex - 1;
    int right = closestIndex + 1;
    while (left >= 0 && right < array.length && i < res.length) {
      int leftDiff = Math.abs(array[left] - target);
      int rightDiff = Math.abs(array[right] - target);
      if (leftDiff <= rightDiff) {
        res[i++] = array[left--];
      } else {
        res[i++] = array[right++];
      }
    } 

    while (i < res.length) {
      res[i++] = left >= 0 ? array[left--] : array[right++];
    }

    return res;
}
```

**binary search in unknown sized sorted array**

```text

```

