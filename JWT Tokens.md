
*   **Structure:** Starts with `ey`. Contains 3 parts: Header, Payload, Signature.
*   **Impact:** Bugs can lead to privilege escalation and account takeover.
*   **Tools:** `token.dev`, `jwt.io`, `jwt editor` (Burp extension).

## Scenarios:

1.  **No Signature Verification:**
    *   The server might not verify the signature.
    *   *Attack:* Change the user to `admin` in the payload and send it. (First lab in PortSwigger).
2.  **None Algorithm:**
    *   The developer checks if the signature is valid, but fails to validate if the algorithm is "None".
    *   *Attack:* Set the algorithm to `None` and remove the signature (send null).
3.  **Weak Signature (Cracking):**
    *   The signature is weak and can be cracked using tools like **Hashcat** or **John the Ripper**.
    *   *Attack:* Crack the secret key. Use JWT Editor to sign a new token with the cracked key, changing the `sub` (subject) to `admin`.
4.  **JWK Header Injection:**
    *   Add a JWK (JSON Web Key) header where the server checks for the first algorithm only, bypassing verification.
5.  **Cookie Expiration:**
    *   Edit the expiration date to extend the validity of the token.
    * 