# 🎓 Final assignment for the project and course
---
## 🛡️ PortSwigger : 
![PortSwigger Progress](https://i.ibb.co/G4V2HwqP/Capture-d-cran-2026-03-03-193748.png)### SQL injection
1. **SQL injection vulnerability in WHERE clause allowing retrieval of hidden data ➔** Add `OR 1=1--` to see private items.
2. **SQL injection vulnerability allowing login bypass ➔** Use `admin'--` to login without password.
### Access control vulnerabilities
3. **Unprotected admin functionality ➔** Go to `/admin` manually.
4. **Unprotected admin functionality with unpredictable URL ➔** Find hidden `/admin-xxxx` in HTML source.
5. **User role controlled by request parameter ➔** Change `Admin=false` to true in proxy.
6. **User role can be modified in user profile ➔** Add `"role": "admin"` to your profile JSON.
7. **User ID controlled by request parameter ➔** Change `id=123` to `id=124` in URL.
8. **User ID controlled by request parameter, with unpredictable user IDs ➔** Use the user's long ID found in posts.
9. **User ID controlled by request parameter with data leakage in redirect ➔** Read the body of the 302 response.
10. **User ID controlled by request parameter with password disclosure ➔** Find the admin password in their profile HTML.
11. **Insecure direct object references ➔** Change the filename in the download URL.
### Authentication
12. **Username enumeration via different responses ➔** Find usernames via different error messages.
13. **2FA simple bypass ➔** Skip code by going to `/account` directly.
14. **Password reset broken logic ➔** Change `username` in the reset request.
15. **Brute-forcing a stay-logged-in cookie ➔** Test many Base64 cookies to guess sessions.
### WebSockets
16. **Manipulating WebSocket messages to exploit vulnerabilities ➔** Inject a script into the chat message.
### Business logic vulnerabilities
17. **Excessive trust in client-side controls ➔** Change the `price` value in the request.
### API testing
18. **Exploiting an API endpoint using documentation ➔** Find DELETE/POST methods in `/api/docs`.
---
## 💻 The Booking system project

### Phase 1 

- **What was done:** I found 11 issues of the system that let me understand better the expected behavior for Guest, Reserver, and Administrator roles. 
- **What worked/didn't work:** Mapping the "intended" security vs. actual implementation worked well; however, identifying subtle logic gaps in the age verification (Spec 6) initially required a more detailed reading.

- **What took the most time:** Installing and understanding the environment like docker, burp suit, using mardown file and interpreting the specific access rights for each role to ensure the baseline for the audit was accurate.

- **What I learned:** I learn that even the registration step can be a breach in cybersecurity.

### Phase 2

- **What was done:** I performed a "white-box" atack to crack password in the docker database.

- **What worked/didn't work:** I had a glitch with my environment, the apt command doesn't work anymore, so I tried to crack password with burp suit but it was to long. that's why, to my side, i used some web site that use dictionary or decrypte hash like md5.

- **What took the most time:** understand the difference between dictionnary attack and non-dictionairy attack

- **What I learned:** there is different type of hash, not all are good one and we also can crack password with pre-made list of most common one but also by just use every combinaison.

### Phase 3

- **What was done:** I used tools like Gobuster to discover hidden pages.

- **What worked/didn't work:** Brute-forcing directories with Gobuster worked perfectly, revealing the /api/users leak; however, exploiting the IDOR (Insecure Direct Object Reference) required precise manual manipulation of request IDs in Burp.

- **What took the most time:** Manipulating API requests to bypass role-based restrictions and proving that a Reserver could delete others' bookings.

- **What I learned:** This phase taught me the "Attacker Mindset". I learned that a functional UI often hides significant backend vulnerabilities that can only be found through manual interception.

### Phase 4

- **What was done:** I used WASP ZAP and drafted the missing legal documentation (privacypolicy.md, termsofservice.md, cookiepolicy.md).

- **What worked/didn't work:** The ZAP scan successfully confirmed the presence of CSRF tokens, the last point I wasn't sure by testing the site itself. However, interpreting the "False Positives" in the report needed cross-referencing with manual tests, which was very long.

- **What took the most time:** Translating technical findings into compliant GDPR documentation that properly addresses data subjects' rights.

- **What I learned:** I learned that cybersecurity is not just technical; it is also a matter of governance and transparency. Proper documentation is a legal shield that must match the technical reality.

### Conclusion
This project was very interesting in several aspects. First, it clearly showed different phases and parts of the security audit:

- **Specifications Analysis:** Understanding the rules, like the age limitation (15 years here).

- **Static Analysis (SAST):** The analysis of the code and Docker files.

- **Dynamic Analysis (DAST):** Using tools like Burp Suite and Gobuster to test breaches online.

- **Compliance Phase:** Using automatic scanners like OWASP ZAP to check protections like CSRF or HSTS and for the legal documentation.

Second, the binome work was also an interesting part. Indeed, this let me learn how to separate the work and learn about how my colleague understood the goal of the phases and what was asked. This collaboration let me understand this course better thanks to the different points of view on the work.

---
## 📝 Logbook

[My Logbook](https://github.com/rockmane78/CybersecurityAndDataPrivacySpring2026/blob/patch-1/logbook.md)
&bull; Total hours : 83h
&bull; Hours per topic : 

| Subject  | Used hours | 
| :--- | :---: |
| Booking System | 45h |
| PortSwigger | 15h |
| Cisco "Introduction to Cybersecurity" | 9h |
| lecture + organisation | 7h |
| Final assignment | 7h |

