+++
title = "Two Sum"
weight = 15
+++

### Description 

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
You may assume that each input would have **_exactly_** one solution, and you may not use the same element twice.

#### Example

```
Given nums = [1, 3, 7, 12], target = 8,

Because nums[0] + nums[2] = 1 + 7 = 8,
return [0, 2].
```

### Solution

#### Java: Brute Force 
This is an example of a brute force solution in Java. It takes _O(n^2)_ in terms of time complexity and _O(1)_ for space. 
It loops through each element `x` and find if there is another value that equals `target - x`

```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

#### Kotlin: Brute Force
Here's the same brute force solution in Kotlin, using lamdas for a more functional style:

```java
fun twoSum(nums: IntArray, target: Int): IntArray {
     nums.indices.forEach { i ->
         (i + 1 until nums.size)
            .asSequence()
            .filter { nums[it] == target - nums[i] }
            .forEach { return intArrayOf(i, it) }
    }
    throw IllegalArgumentException("No two sum solution")
}
```

#### Java (Two-pass Hash Table)

It is possible to improve on the first brute force solution by using an implementation that allows us to trade space for speed. 
It turns time complexity in _O(n)_ and space complexity also to _O(n)_
This implementation involves the introduction of a hash table that allows us for fast look up of the complement 
in near constant time. A classic implementation uses two iterations. In the first iteration, we add each element's value and its index to the table. 
Then, in the second iteration we check if each element's complement `(target - nums[i]target−nums[i])` exists in the table. 
We must also remember the special case where the `complement` must not be `nums[i]`itself!

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

#### Kotlin (Two-pass Hash Table)


```java
In Kotlin, this turns into the following code.

        fun twoSum(nums: IntArray, target: Int): IntArray {
            val map = HashMap<Int, Int>()
            for (i in nums.indices) {
                map.put(nums[i], i)
            }
            for (i in nums.indices) {
                val complement = target - nums[i]
                if (map.containsKey(complement) && map.get(complement) != i) {
                    return intArrayOf(i, map[complement]!!)
                }
            }
            throw IllegalArgumentException("No two sum solution")
        }
```






