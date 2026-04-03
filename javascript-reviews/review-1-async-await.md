Review 1: JavaScript Async/Await & Error Handling

Severity:** High  
Language:** JavaScript

 Original Task Given to AI

> Write a function that fetches user data from an API, then fetches their posts, and returns both. Handle any errors that occur.

## Buggy AI-Generated Code

```javascript
// ❌ BUGGY CODE
async function getUserWithPosts(userId) {
  const userResponse = fetch(`/api/users/${userId}`);
  const user = userResponse.json();
  
  const postsResponse = fetch(`/api/users/${userId}/posts`);
  const posts = postsResponse.json();
  
  return { user, posts };
}
