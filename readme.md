# JavaScript Problem Solving

## Problem 1: Count Pairs With Target Difference

### Problem

Given an array of project costs and a target number, count how many unique pairs have a difference equal to the target.

### Example

```text
projectCosts = [1, 3, 5]
target = 2
```

Valid pairs:

```text
(1, 3)
(3, 5)
```

Output:

```text
2
```

### Solution

```javascript
function pairCount(projectCosts, target) {
  const costs = new Set(projectCosts);
  let count = 0;

  for (const cost of costs) {
    if (costs.has(cost + target)) {
      count++;
    }
  }

  return count;
}

const projectCosts1 = [1, 3, 5];
const projectCosts2 = [1, 3, 5, 7, 9];
const projectCosts3 = [2, 4, 6, 8, 10];
const projectCosts4 = [1, 1, 3, 3, 5, 5];
const projectCosts5 = [10, 20, 30, 40, 50];

console.log(pairCount(projectCosts1, 2));
console.log(pairCount(projectCosts2, 2));
console.log(pairCount(projectCosts3, 2));
console.log(pairCount(projectCosts4, 2));
console.log(pairCount(projectCosts5, 10));
```

### Output

```text
2
4
4
2
4
```

## Problem 2: First Non-Repeating Number

### Problem

Given an array of numbers, find the **first number that appears only once**.

If every number appears more than once, return `-1`.

### Example

```javascript
const numbers = [4, 5, 1, 2, 1, 4, 5];
```

The counts are:

```text
4 -> 2 times
5 -> 2 times
1 -> 2 times
2 -> 1 time
```

So the answer is:

```text
2
```

### Solution

```javascript
function firstNonRepeatingNumber(numbers) {
  const counts = new Map();

  for (const number of numbers) {
    let count = counts.get(number) || 0;
    count++;

    counts.set(number, count);
  }

  for (const number of numbers) {
    if (counts.get(number) === 1) {
      return number;
    }
  }

  return -1;
}

const numbers = [4, 5, 1, 2, 1, 4, 5];

console.log(firstNonRepeatingNumber(numbers));
```

### Output

```text
2
```

### Complexity

- Time: **O(n)**
- Space: **O(n)**

## Problem 3: Convert a Word to Pig Latin

### Problem

Given a word, convert it to **Pig Latin** using these rules:

- Find the first vowel: `a, e, i, o, u`
- Treat `y` as a vowel only when it is not the first letter
- Move all letters before the first vowel to the end
- Add `"ay"`
- If the word starts with a vowel, just add `"ay"`
- If the word has no vowel, just add `"ay"` to the end

### Examples

```text
school   → oolschay
computer → omputercay
string   → ingstray
apple    → appleay
rhythm   → ythmrhay
```

### Solution

```javascript
function toPigLatin(word) {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']);
  const isVowel = (ch, index) => vowels.has(ch) || (ch === 'y' && index > 0);

  for (let i = 0; i < word.length; i++) {
    if (isVowel(word[i], i)) {
      return word.slice(i) + word.slice(0, i) + 'ay';
    }
  }

  return word + 'ay';
}

console.log(toPigLatin("school"));    // oolschay
console.log(toPigLatin("computer"));  // omputercay
console.log(toPigLatin("string"));    // ingstray
console.log(toPigLatin("apple"));     // appleay
console.log(toPigLatin("rhythm"));    // ythmrhay
```

### How it works

For `"school"`:

```text
s c h o o l
0 1 2 3 4 5
      ↑
first vowel
```

So:

```text
word.substring(3)    // "ool"
word.substring(0, 3) // "sch"
```

Then:

```text
"ool" + "sch" + "ay"
= "oolschay"
```

### Complexity

- Time: **O(n)**
- Space: **O(1)** ignoring the returned string.

## Problem 4: Binary Search

### Problem

Given a sorted array of numbers, find a target value using binary search.

If the target is found, return the target value. Otherwise, return `-1`.

### Example

```javascript
const arr = [10, 20, 30, 40, 50, 60, 70, 90];
const result = binarySearch(arr, 60);
```

Output:

```text
60
```

### Solution

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const half = Math.floor((left + right) / 2);
    const mid = arr[half];

    if (mid === target) {
      return mid;
    }

    if (mid > target) {
      right = half - 1;
    }
    else {
      left = half + 1;
    }
  }

  return -1;
}

const arr = [10, 20, 30, 40, 50, 60, 70, 90];
const result = binarySearch(arr, 60);

console.log(result);
```

### Output

```text
60
```

### Complexity

- Time: **O(log n)**
- Space: **O(1)**

## Problem 5: Check Palindrome Text

### Problem

Given a text string, check whether it reads the same forward and backward.

### Solution

```javascript
function isPalindromeText(text) {
  let left = 0;
  let right = text.length - 1;

  while (left < right) {
    if (text[left] !== text[right]) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}

console.log(isPalindromeText('madam'));      // true
console.log(isPalindromeText('hello'));      // false
console.log(isPalindromeText('racecar'));    // true
console.log(isPalindromeText('javascript')); // false
console.log(isPalindromeText('abba'));       // true
console.log(isPalindromeText('apple'));      // false
console.log(isPalindromeText('noon'));       // true
console.log(isPalindromeText('world'));      // false
```

### Output

```text
true
false
true
false
true
false
true
false
```

### Complexity

- Time: **O(n)**
- Space: **O(1)**

## Problem 6: Find Pairs With Target Sum

### Problem

Given a sorted array of numbers and a target value, find all pairs whose sum is equal to the target.

### Example

```javascript
const arr = [1, 2, 4, 6, 8, 10];
const target = 10;
```

Valid pairs:

```text
(2, 8)
(4, 6)
```

### Solution

```javascript
function findPairsWithTargetSum(arr, target) {
  const pairs = [];
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const sum = arr[left] + arr[right];

    if (sum === target) {
      pairs.push([arr[left], arr[right]]);

      left++;
      right--;
    }
    else if (sum > target) {
      right--;
    }
    else {
      left++;
    }
  }

  return pairs;
}

const arr = [1, 2, 4, 6, 8, 10];
const target = 10;

console.log(findPairsWithTargetSum(arr, target));
```

### Output

```text
[ [ 2, 8 ], [ 4, 6 ] ]
```

### Complexity

- Time: **O(n)**
- Space: **O(k)** where `k` is the number of pairs found.
