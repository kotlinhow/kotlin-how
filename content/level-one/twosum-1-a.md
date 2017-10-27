+++
title = "Two Sum"
weight = 15
+++

### Description: 

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
You may assume that each input would have **_exactly_** one solution, and you may not use the same element twice.

### Solution

This is an example of a Brute Force solution in Java. It loops through each element `x` and find if there is another value that equals `target - x`

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

Here's the same brute force solution in Kotlin

```kotlin
fun twoSum(nums: IntArray, target: Int): IntArray {
    for (i in nums.indices) {
        (i + 1 until nums.size)
            .asSequence()
            .filter { nums[it] == target - nums[i] }
            .forEach { return intArrayOf(i, it) }
        }
    throw IllegalArgumentException("No two sum solution")
}
```