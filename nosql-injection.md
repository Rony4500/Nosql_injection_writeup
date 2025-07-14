NoSQL Injection Walkthrough — Login Bypass via MongoDB

🧠 Scenario:

This walkthrough demonstrates how a poorly secured login form using MongoDB can be bypassed using NoSQL injection techniques. The application accepts raw JSON input in the login form and directly queries the database, making it vulnerable.


✅ Step 1: Accessing the Login Page

We begin by accessing a login page of a target web application that uses MongoDB for backend authentication. The form contains fields for username and password.

❌ Step 2: Standard Login Attempt

We try logging in using dummy credentials:

Username: test  
Password: test

As expected, login fails since the credentials are invalid.


⚠️ Step 3: Injecting Malicious Payload

Next, we inject a NoSQL payload to manipulate the backend MongoDB query logic:

Username: {"$ne": null}  
Password: {"$ne": null}

This payload takes advantage of MongoDB’s $ne operator, which means “not equal.” When passed directly into the query, it effectively transforms the logic into:

db.users.find({
  username: { $ne: null },
  password: { $ne: null }
})

This condition returns true for every document where both username and password are not null — which is true for all users. As a result, the application logs us in without verifying actual credentials.


🟢 Step 4: Authentication Bypassed

After submitting the payload, we gain unauthorized access to a valid user account. We’ve successfully bypassed the login authentication mechanism.


🔒 Step 5: How to Prevent This

To protect against NoSQL Injection:

Input Validation: Ensure only expected data types are accepted (e.g., enforce strings, disallow objects).

Use ODMs/ORMs: Use libraries like Mongoose with built-in query sanitization.

Avoid Raw Queries: Never pass user input directly into queries.

Rate Limiting & Logging: Detect unusual login patterns and respond accordingly.

Web Application Firewall (WAF): Filter out malicious requests at the edge.

🧠 Conclusion

NoSQL Injection is a powerful technique that can easily bypass authentication in MongoDB-backed applications if inputs are not strictly validated. Always treat user input as untrusted and adopt secure coding practices to protect your application.


---

📌 Tags

#NoSQLInjection #CyberSecurity #BugBounty #MongoDB #InfoSec #OWASP #WebSecurity #TryHackMe
