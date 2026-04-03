


```markdown
# Review 3: Authentication & SQL Injection

**Severity:** Critical  
**Language:** JavaScript (Node.js)

## Original Task Given to AI

> Write a login function that checks if a user exists in the database and returns user data if credentials match.

## Buggy AI-Generated Code

```javascript
// ❌ BUGGY CODE
app.post('/login', (req, res) => {
  const { username, password } = req.body;
  
  const query = `SELECT * FROM users WHERE username = '${username}' AND password = '${password}'`;
  
  db.query(query, (err, results) => {
    if (results.length > 0) {
      res.json({ success: true, user: results[0] });
    } else {
      res.status(401).json({ success: false });
    }
  });
});
