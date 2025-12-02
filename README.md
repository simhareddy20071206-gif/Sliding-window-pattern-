

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




Welcome back 🔥
Perfect — short breaks keep your brain sharp.

Now we move to:

# ⭐ **Sliding Window – Problem 2: Longest Substring Without Repeating Characters**

This is one of the **core** dynamic sliding window problems used in FAANG.

I’ll give you proper GitHub-ready **NOTES** in Markdown style, just like the previous problem.

---

# 📘 **Sliding Window – Problem 2: Longest Substring Without Repeating Characters**

## 🚀 **1. Problem Statement**

Given a string `s`, return the **length of the longest substring** without repeating characters.

Example:

```
Input:  "abcabcbb"
Output: 3   ("abc")
```

---

# 🧠 **2. Why Sliding Window?**

We expand the window (`j`) until a duplicate character appears.
When a duplicate enters → shrink from the left (`i`) until the window becomes valid again.

This gives us **O(n)** time instead of checking all substrings (O(n²)).

---

# 🪟 **3. Sliding Window Approach**

### **Key Idea**

Maintain a window where **all characters are unique**.

### **To do this:**

* Use a `set` or `map` to track characters
* Expand window until you hit a duplicate
* When duplicate found → remove from left until duplicate is removed
* Update `maxLen` whenever window is valid

---

# 🧩 **4. Algorithm Steps**

1. Create a set `st` to store characters in the current window
2. Initialize `i = 0`, `j = 0`
3. While `j < n`:

   * If `s[j]` not in set → insert it, update `maxLen`
   * Else (duplicate found):

     * Remove characters starting from `i` until duplicate is removed
   * Move `j`
4. Return `maxLen`

---

# 💻 **5. C++ Code**

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_set<char> st;
    int i = 0, j = 0, maxLen = 0;
    int n = s.length();

    while (j < n) {
        if (st.find(s[j]) == st.end()) {
            // Expand window
            st.insert(s[j]);
            maxLen = max(maxLen, j - i + 1);
            j++;
        } else {
            // Shrink window
            st.erase(s[i]);
            i++;
        }
    }
    return maxLen;
}
```

---

# ⏱️ **6. Time & Space Complexity**

| Complexity | Value                                 |
| ---------- | ------------------------------------- |
| Time       | **O(n)**                              |
| Space      | **O(k)** (max unique chars in window) |

---

# 🧪 **7. Testcases**

### ✅ Basic

```
s = "abcabcbb"
Output = 3
```

### ✅ All characters same

```
s = "bbbbbb"
Output = 1
```

### ✅ Long unique substring

```
s = "pwwkew"
Output = 3   ("wke")
```

### ✅ Single character

```
s = "a"
Output = 1
```

### ✅ Empty string

```
s = ""
Output = 0
```

---

# 🏁 **8. Summary**

Sliding window expands until a duplicate appears →
shrink from left until the window becomes unique again.

This is the **foundation** for advanced dynamic sliding window problems.
