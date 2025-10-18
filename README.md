# LEETCODE-Greedy-3397
---

### 🔹 Code Recap

```java
class Solution {
    public int maxDistinctElements(int[] nums, int k) {
        Arrays.sort(nums);
        int count = 0;
        int prev = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int minval = nums[i] - k;
            if (prev < minval) {
                prev = minval;
                count++;
            } else if (prev < nums[i] + k) {
                prev = prev + 1;
                count++;
            }
        }
        return count;
    }
}
```

---

### 🔹 Purpose

This function tries to find the **maximum number of distinct integers** you can create by adjusting each number in `nums` within a range of `±k`.

For each element, you can shift it anywhere between `[nums[i] - k, nums[i] + k]` such that all final values are **distinct**.

---

### 🔹 Example Dry Run

Let’s take an example:

```
nums = [1, 3, 5]
k = 1
```

#### Step 1: Sort `nums`

`nums = [1, 3, 5]` (already sorted)

#### Step 2: Initialize

```
count = 0
prev = -∞
```

#### Step 3: Iterate

---

**i = 0 → nums[0] = 1**

```
minval = 1 - 1 = 0
if (prev < minval) → (-∞ < 0) ✅
    prev = minval = 0
    count = 1
```

✅ Result so far → distinct values used: [0]

---

**i = 1 → nums[1] = 3**

```
minval = 3 - 1 = 2
if (prev < minval) → (0 < 2) ✅
    prev = 2
    count = 2
```

✅ Result so far → distinct values used: [0, 2]

---

**i = 2 → nums[2] = 5**

```
minval = 5 - 1 = 4
if (prev < minval) → (2 < 4) ✅
    prev = 4
    count = 3
```

✅ Result so far → distinct values used: [0, 2, 4]

---

✅ **Return count = 3**

---

### 🔹 Another Case (where else-if triggers)

```
nums = [1, 2, 2]
k = 1
```

After sorting → `[1, 2, 2]`

```
count = 0
prev = -∞
```

**i = 0 → nums[0] = 1**

```
minval = 0
prev < minval → (-∞ < 0) ✅
→ prev = 0, count = 1
```

**i = 1 → nums[1] = 2**

```
minval = 1
prev < minval → (0 < 1) ✅
→ prev = 1, count = 2
```

**i = 2 → nums[2] = 2**

```
minval = 1
prev < minval → (1 < 1) ❌
else if (prev < nums[i] + k) → (1 < 3) ✅
→ prev = prev + 1 = 2
→ count = 3
```

✅ Final result → `count = 3`

Distinct adjusted values used → [0, 1, 2]

---

### 🔹 Summary of Logic

* Sort the array to handle smaller numbers first.
* For each element:

  * Try to assign the smallest possible new distinct value within `[nums[i] - k, nums[i] + k]` that’s **greater than `prev`**.
  * If `minval` is too small (conflicts), increment `prev` by 1 to stay distinct.
* Keep track of `count` for each distinct value assigned.

---

### 🔹 Example Outputs

| nums      | k | Output | Explanation        |
| --------- | - | ------ | ------------------ |
| [1,3,5]   | 1 | 3      | shifted to [0,2,4] |
| [1,2,2]   | 1 | 3      | shifted to [0,1,2] |
| [4,4,4]   | 1 | 3      | can pick [3,4,5]   |
| [1,10,20] | 5 | 3      | already distinct   |

---
