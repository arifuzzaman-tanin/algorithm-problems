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
rhythm   → rhythmay
```

### Solution

```javascript
function toPigLatin(word) {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']);

  for (let i = 0; i < word.length; i++) {
    if (vowels.has(word[i])) {
      return word.substring(i) + word.substring(0, i) + 'ay';
    }
  }

  return word + 'ay';
}

console.log(toPigLatin("school"));    // oolschay
console.log(toPigLatin("computer"));  // omputercay
console.log(toPigLatin("string"));    // ingstray
console.log(toPigLatin("apple"));     // appleay
console.log(toPigLatin("rhythm"));    // rhythmay
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
