
# Review 2: JavaScript Array Mutation & Pure Functions

Severity:** Medium  Language:JavaScript

## Original Task Given to AI

> Create a function that removes duplicate items from an array and returns a new array without modifying the original.

## Buggy AI-Generated Code

```javascript
// ❌ BUGGY CODE
function removeDuplicates(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) {
        arr.splice(j, 1);
        j--;
      }
    }
  }
  return arr;
}
