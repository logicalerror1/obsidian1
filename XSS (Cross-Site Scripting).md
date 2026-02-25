
XSS happens when the website can't distinguish the difference between the original user input and the malicious script injected by the attacker.

## 5 Types of XSS:

1.  **Stored XSS:**
    *   Happens when the data stored on the server is retrieved unsafely. The famous example for this is the comment section or forum posts.
2.  **Blind XSS:**
    *   Blind XSS is a type of stored XSS where the malicious input is stored in the server but executed on another part of the application or another application entirely (e.g., admin panels).
3.  **Reflected XSS:**
    *   Happens when the website processes the user input only on the client side/server without storing it into a database.
4.  **DOM-based XSS:**
    *   Is much like Reflected XSS; the difference is that the DOM uses the browser rendering without the data reaching any server for processes. JavaScript libraries like **jQuery** are the most vulnerable to DOM XSS as they dynamically alter DOM elements.
5.  **Self XSS:**
    *   Requires more effort as the attacker must trick the user into changing the parameter of the URL himself or by using code. It usually requires Social Engineering skills and is not really accepted in bug bounty as it's not considered Technical.

## Prevention:

To prevent XSS there are two things to implement:

1.  **Robust Input Validation:**
    *   Applications must not allow any user input to go through the application into the server without sanitation and filtration.
    *   Applications should have a keyword filter for a wordlist that contains the commonly used keywords for XSS such as `()` which are clearly a sign of an XSS payload, so the application can ignore the execution of the code and maybe block the user IP.
2.  **Contextual Output Escaping and Encoding:**
    *   Another method to be used is Escaping, which refers to the application encoding special characters so that they are interpreted literally by the program rather than as code.
    *   **DOM XSS Prevention:** Requires different methods as it doesn't go through the server and won't go through server validations. The application must also use Client-side input Validation before going to the DOM.