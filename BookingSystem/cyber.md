# 🔐 Authorization Test Report - Phase 3

## 📋 Project Overview
This report documents the authorization testing for the resource booking system. The goal is to verify if the actual implementation matches the official specifications (Specs 1–8) and follows the Principle of Least Privilege (PoLP).

---

## 🧑‍🦲 Guest
*Unauthenticated user. Should only access public resources.*

### ✅ Can do
* **View public resource list** — `/`
  * *Observation:* Accessible without login. Matches Spec 8.
* **Access login form** — `/login`
  * *Observation:* Accessible.
* **Access registration form** — `/register`
  * *Observation:* Accessible (Spec 2).
* **View booked resources** — `/`
  * *Observation:* Displays booked resources without revealing reserver identity (Spec 8).
* **Access API endpoints** — `/api/reservations`
  * *Observation:* print all information of other register.

### ❌ Cannot do
* **Access profile page** — `/profile`
  * *Observation:* Blocked. Print 'not found'.
* **Access reservation page** — `/reservation`
  * *Observation:* Blocked. Redirects to back home.
* **Access reservation page** — `/reservation`
  * *Observation:* Correctly blocked when age is under 15 years.Redirects to back home.


---

## 🧑‍💼 Reserver
*Logged in as: `john@doe.com`*

### ✅ Can do
* **Book a resource** — `/reservation`
  * *Observation:* Accessible. User can book on an hourly basis (Spec 7).
  * *Note:* Requires user to be over 15 years old (Spec 6).
* **View own profile** — `/profile`
  * *Observation:* Displays personal profile information.
* **List available resources** — `/resources`
  * *Observation:* Accessible.

### ❌ Cannot do
* **Access admin dashboard** — `/admin`
  * *Observation:* [REMPLIR : Bloqué par le serveur ?]
* **Delete other users** — `/api/admin/users/:id`
  * *Observation:* Correctement bloqué (Spec 4 & 5 réservés à l'admin).
* **Modify/Delete resources** — `/api/resources/:id`
  * *Observation:* Devrait être réservé à l'administrateur uniquement.

---

## 🧑‍💼🛡️ Administrator
*High-privilege account with full control.*

### ✅ Can do
* **Add/Remove/Modify resources** — `/admin/resources`
  * *Observation:* Full control over resource management (Spec 4).
* **Delete a reserver** — `/admin/users/delete/:id`
  * *Observation:* Functional (Spec 5).
* **Manage all reservations** — `/admin/reservations`
  * *Observation:* Can view and modify any booking (Spec 4).

### ❌ Cannot do
* **Excessive data exposure**
  * *Observation:* Check if Admin has access to data not required by GDPR or PbD principles.

---

## 🔍 Tools Used & Methodology
* **Manual Browser Testing:** Verification of UI elements, forms, and redirects.
* **Gobuster (Windows):** Discovery of unreferenced endpoints and hidden directories.
* **Burp Suite:** Intercepting requests to test for IDOR (Insecure Direct Object Reference) and backend authorization.
* **ZAP (Collaborator):** Automated vulnerability scan results integrated from `zap_report_round4.md`.

---

## ⚠️ Discrepancies & Findings
*(Note ici si quelque chose ne respecte pas les specs du prof)*
* **Example:** "Spec 8 says no identity for Guest, but identity is visible in API response."