

We can get files like `/etc/passwd` on any server (e.g., using Kali). This is done by manipulating a request that reads a file.

*   **Concept:** Change `file=image.png` to `file=/etc/passwd`.
*   **Recon:** Use `nmap -O` or `whatweb` to identify the OS.
*   **Bypasses:**
    1.  **Basic:** `../../../../etc/passwd` (Goes to root).
    2.  **Nested/Stripped Sequence:** If developers remove `../`, use `....//`.
        *   *Logic:* `....//` -> remove inner `../` -> results in `../`.
    3.  **Encoding:** URL encode the `../` part.
    4.  **Double Encoding:** URL encode the string twice. The backend decodes once (bypassing the filter) and then decodes again to execute the traversal.
*   **Relationship:** Path traversal is strongly linked to **File Inclusion**.