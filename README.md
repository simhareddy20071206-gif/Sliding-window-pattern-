

Here are **Sliding Window – Problem 1 Notes** written in a clean, professional GitHub-friendly format **(markdown style)**.

---

# 📘 **Sliding Window – Problem 1: Max Sum Subarray of Size K**

## 🚀 **1. Problem Statement**

Given an array `nums` and an integer `k`, find the **maximum sum** of any **contiguous subarray** of size **k**.

Example:

```
nums = [2, 1, 5, 1, 3, 2], k = 3  
Answer = 9   (subarray = [5, 1, 3])
```

---

# 🧠 **2. Why Sliding Window Works**

A window of size `k` slides over the array, and instead of calculating the sum again and again:

* Add the new element entering the window
* Remove the old element leaving the window

This makes the solution **O(n)** instead of **O(n*k)**.

---

# 🪟 **3. Sliding Window Approach**

### **Steps**

1. Initialize two pointers `i = 0`, `j = 0`
2. Expand window by adding `nums[j]` until window size becomes `k`
3. Once window size is `k`:

   * Update `maxSum`
   * Slide window → remove `nums[i]`, increment `i`, `j`
4. Continue while `j < n`

---

# 🧩 **4. Algorithm**

1. Start with `sum = 0`.
2. Add first `k` elements.
3. Set `maxSum = sum`.
4. For each new index:

   * `sum -= nums[i]` (remove leftmost)
   * `sum += nums[j]` (add rightmost)
   * `maxSum = max(maxSum, sum)`
   * move both pointers
5. Return `maxSum`.

---

# 💻 **5. C++ Code**

```cpp
int maximumSubarraySum(vector<int>& arr, int k) {
    int n = arr.size();
    int i = 0, j = 0;
    int sum = 0;
    
    // Build first window
    while (j < k) {
        sum += arr[j];
        j++;
    }
    
    int maxSum = sum;
    
    // Slide the window
    while (j < n) {
        sum = sum - arr[i] + arr[j];
        maxSum = max(maxSum, sum);
        i++;
        j++;
    }
    
    return maxSum;
}
```

---

# ⏱️ **6. Time & Space Complexity**

| Complexity | Value    |
| ---------- | -------- |
| Time       | **O(n)** |
| Space      | **O(1)** |

---

# 🧪 **7. Testcases**

### ✅ Basic

```
nums = [2,1,5,1,3,2], k = 3  
Output = 9
```

### ✅ All positive

```
nums = [1,2,3,4,5], k = 2  
Output = 9
```

### ✅ Contains negatives

```
nums = [-1, 4, -2, 5, -3], k = 2  
Output = 3
```

### ✅ Decreasing sequence

```
nums = [9,8,7,6,5], k = 3  
Output = 24
```

---

# 🏁 **8. Summary**

* Fixed-size sliding window
* Maintain running sum
* Sliding removes leftmost, adds rightmost
* Works in O(n)

--
