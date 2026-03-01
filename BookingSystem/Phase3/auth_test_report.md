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


### ❌ Cannot do
* **Access reservation page** — `/reservation`
  * *Observation:* Blocked. Redirects to back home.

### ⚠️ Vulnerabilities (GDPR Violation)
* **Access API endpoints** — `/api/reservations`
  * *Observation:* print all information of other register.

---

## 🧑‍💼 Reserver
*Logged in as: `john@doe.com`*

### ✅ Can do
* **Book a resource** — `/reservation`
  * *Observation:* Accessible. User can book on an hourly basis (Spec 7).
  * *Note:* Requires user to be over 15 years old (Spec 6).
* **List available resources** — `/resources`
  * *Observation:* Accessible. User can creat ressources.

### ❌ Cannot do
* **View other user profile** 
  * *Observation:* no indication in the URL


### ⚠️ Vulnerabilities (GDPR Violation)
* **IDOR on Bookings** — `/reservation?id=X`
    * *Observation:* Users can access and modify bookings belonging to others by changing the ID in the URL.
* **Privilege Escalation** — `/api/resources/:id`
  * *Observation:* Users can take ownership of another user's booking by changing the "Reserver" field in the form, and subsequently delete it.
* **GDPR Compliance**
  * *Observation:* Users cannot delete their own accounts (Violation of GDPR "Right to be Forgotten").

---

## 🧑‍💼🛡️ Administrator
*High-privilege account with full control. Logged in as: `mari@doe.com`*

### ✅ Can do
* **Full System Management** 
  * *Observation:* Full control over resource management (Spec 4).
* **Delete a reserver** — `/reservation?id=X`
  * *Observation:* Functional (Spec 5).
* **Manage all reservations** — `/reservations`
  * *Observation:* Can view and modify any booking (Spec 4).

### ❌ Cannot do


---

## ⚠️ Findings
*(Note ici si quelque chose ne respecte pas les specs du prof)*
* **Example:** "Spec 8 says no identity for Guest, but identity is visible in API response."
