SQL injection happens when the attacker uses SQL commands by inserting malicious scripts inside of input. It is the result of incorrectly filtered or escaped input and can lead to authentication bypass.

## Types of SQL Injection:
1.  Classic
2.  Blind
3.  NoSQL

## Concepts:

*   **The Comment (`--`):** One of the most famous injections uses `--` (comment in SQL). The attacker can escape the password part of the authentication using only the username.
    *   *Payload:* `admin';--`
    *   *Logic:* `SELECT Id FROM users WHERE username ='admin';--'&password='password';` (The rest is ignored).
*   **Syntax:** Knowing SQL commands is a must (select, union, update, set, etc.).
*   **First vs Second Order:**
    *   *First Order:* Direct execution.
    *   *Second Order SQL Injection:* Input is filtered and stored safely in the database, but retrieved unsafely later. The server trusts the data as safe.

**Second Order Scenario:**
Attacker inputs: `name' UNION SELECT Username, password From Users;--`
When the server retrieves this name later for a query like `SELECT title, body FROM emails WHERE username='[Input]'`, it executes the malicious union select.

## Techniques:
*   **Wildcards:** Use `%` to specify starting/ending targets.
    *   `SELECT * FROM users WHERE username LIKE 'a%'` (Returns users starting with 'a').
*   **Blind Injection:**
    *   Use time stamps or logic errors.
    *   Example: `' OR SLEEP(100);--` or `pg_sleep(100);--`

## Prevention:
1.  **Prepared Statements:** The developer specifies the logic and structure of the SQL query first. The user input is added before execution and treated as **plain text** instead of a logical flow.
2.  **Allow Lists:** Allows the user to use only specific statements that are known to be safe, blocking harmful logic.

## PortSwigger Labs Walkthrough:

1.  **Lab 1 (Retrieval):** No input field, so check filters (e.g., categories).
    *   Inject `'` into the category parameter. If it returns "Internal Server Error", it's vulnerable.
    *   Payload: `/filter?category=' OR 1=1 --`
2.  **Lab 2 (Login):** Injection in the login field.
    *   Payload: `administrator'--` (Comments out the password check).

## Hunting for SQL Injection:
1.  Check every user input field by adding `'`. If the site is protected, nothing happens (plain text). If not, an error appears.
2.  If no error occurs, try Blind SQLi using time delays (`SLEEP`).
3.  Use **SQLMap** for automation (though manual verification is recommended).
4.  If there are no visible parameters, use tools like **Arjun** to fuzz for hidden parameters.