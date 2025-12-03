

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




# 📘 **Sliding Window – Problem 3: Longest Subarray With Sum ≤ K**

## 🚀 **1. Problem Statement**

Given an array `nums` (non-negative integers) and an integer `k`,
find the **length of the longest contiguous subarray** whose **sum is ≤ k**.

Example:

```
nums = [2, 1, 5, 1, 3, 2], k = 7
Output = 3     (subarray = [2, 1, 4] or [5, 1, 1])
```

---

# 🧠 **2. Why Sliding Window Works**

This problem works with sliding window **because all numbers are non-negative**.

➡️ When you add elements, sum increases
➡️ When you remove elements from the left, sum decreases

This creates a natural **two-pointer expanding/shrinking window**.

---

# 🪟 **3. Sliding Window Approach**

### Key idea:

* Expand the window as long as the sum remains ≤ k
* If adding the next element breaks the condition (sum > k),
  shrink the window from the left
* Keep track of the maximum valid window length

---

# 🧩 **4. Algorithm**

1. Initialize:

   ```
   i = 0, j = 0
   sum = 0
   maxLen = 0
   ```
2. While `j < n`:

   * Add `nums[j]` to running sum
   * While `sum > k` → shrink from left (`i++`)
   * Once valid (`sum <= k`) → update `maxLen`
   * Move `j` right
3. Return `maxLen`

The window only moves forward → total complexity **O(n)**.

---

# 💻 **5. C++ Code**

```cpp
int longestSubarray(vector<int>& arr, int k) {
    int n = arr.size();
    int i = 0, j = 0;
    long long sum = 0;
    int maxLen = 0;

    while (j < n) {
        // expand window
        sum += arr[j];

        // shrink from left while invalid
        while (i <= j && sum > k) {
            sum -= arr[i];
            i++;
        }

        // valid window => update answer
        maxLen = max(maxLen, j - i + 1);

        j++;
    }

    return maxLen;
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
nums = [2, 1, 5, 1, 3, 2], k = 7
Output = 3
```

### ✅ Full valid window

```
nums = [1,1,1,1], k = 10
Output = 4
```

### ❌ No valid subarray

```
nums = [8,9,10], k = 5
Output = 0
```

### ⚠️ Single element

```
nums = [5], k = 5
Output = 1
```

### 🔥 Large values

```
nums = [3, 3, 3, 3], k = 6
Output = 2
```

---

# 🏁 **8. Summary**

Sliding window works because:

* expanding window only increases sum
* shrinking window removes elements until valid
* window moves only forward → O(n)

This is a **core dynamic sliding-window pattern** used in many subarray problems involving constraints like sum ≤ k.

---

If you want, I can now prepare **Problem 4 notes (Character Replacement)** or the **Sliding Window Cheatsheet**.



# 📘 **Minimum Window Substring — Sliding Window (Hard)**

## 🚀 **Problem**

Given strings `s` and `t`, return the **smallest substring of `s`** that contains **all characters of `t`** (including duplicates).
If no such substring exists, return `""`.

---

## 🧠 **Core Idea (High-Level)**

We use a **dynamic sliding window** and track:

* `need[c]` → how many of each char we still need
* `required` → total characters still missing
* When `required == 0` → window is VALID
* Shrink from the left to make it as small as possible

This is the **reverse** of normal sliding window:
Expand → shrink → update minimum.

---

## 🪟 **Algorithm (Short)**

1. Build frequency array `need` for string `t`.
2. Expand window using `j++`:

   * Decrease `need[s[j]]`.
   * If `need[s[j]] > 0` before decreasing → reduce `required`.
3. When `required == 0`:

   * Window is valid → try shrinking with `i++`.
   * Update `minLen` and `start` if smaller window found.
   * If shrinking breaks validity → `required++`.
4. Return `s.substr(start, minLen)`.

---

## 💻 **Code (clean + optimal)**

```cpp
string minWindow(string s, string t) {
    if (t.size() > s.size()) return "";

    vector<int> need(128, 0);
    for (char c : t) need[c]++;

    int required = t.size();
    int i = 0, j = 0;
    int minLen = INT_MAX, start = 0;

    while (j < s.size()) {
        if (need[s[j]] > 0) required--;
        need[s[j]]--;
        j++;

        while (required == 0) {
            if (j - i < minLen) {
                minLen = j - i;
                start = i;
            }
            need[s[i]]++;
            if (need[s[i]] > 0) required++;
            i++;
        }
    }

    return minLen == INT_MAX ? "" : s.substr(start, minLen);
}
```

---

## ⏱️ **Complexity**

| Part  | Value                                       |
| ----- | ------------------------------------------- |
| Time  | **O(n)** — each index visited at most twice |
| Space | **O(1)** — only 128-sized arrays            |

---

## 🧪 **Good Testcases**

```
Input:  s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"

Input:  s = "a", t = "a"
Output: "a"

Input:  s = "a", t = "aa"
Output: ""

Input:  s = "aa", t = "aa"
Output: "aa"

Input:  s = "abc", t = "cba"
Output: "abc"
```

---


