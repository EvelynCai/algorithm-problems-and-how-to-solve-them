# Quick Select

```text
public int findKthLargest (int[] nums, int k) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    
    return quickSelect(nums, 0, nums.length - 1, nums.length - k);
}

private int quickSelect(int[] nums, int left, int right, int kSmallest) {
    if (left == right) {
        return nums[left];
    }
    
    int pivot = left + (right - left) / 2;
    pivot = partition(nums, left, right, pivot);
    if (pivot == kSmallest) {
        return nums[pivot];
    } else if (pivot < kSmallest) {
        return quickSelect(nums, pivot + 1, right, kSmallest);
    } else {
        return quickSelect(nums, left, pivot - 1, kSmallest);
    }
}

private int partition(int[] nums, int left, int right, int pivot) {
    int pivotVal = nums[pivot];
    swap(nums, pivot, right);
    
    int res = left;
    
    for (int i = left; i <= right; i++) {
        if (nums[i] < pivotVal) {
            swap(nums, i, res++);
        }
    }
    
    swap(nums, right, res);
    return res;
}

private void swap(int[] nums, int a, int b) {
    int tmp = nums[a];
    nums[a] = nums[b];
    nums[b] = tmp;
}
```

