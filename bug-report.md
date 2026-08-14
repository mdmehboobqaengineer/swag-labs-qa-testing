# Bug Report — Swag Labs (saucedemo.com)

**Tester:** Muhammad Mehboob  
**Date:** August 14, 2026  
**Browser:** Chrome (latest)  
**Test URL:** https://www.saucedemo.com  
**Evidence Folder:** See `/evidence` folder for screenshots

---

## BUG-001 — Both Fields Turn Red When Only One Field is Wrong

**Area:** Login Page  
**Severity:** Medium  
**Status:** Open

**What happened:**  
When I left the username empty and clicked Login, both the username AND password fields turned red with error icons. The password field was fine — I hadn't touched it. Same thing happened when I filled in the username but left the password empty. Both fields still went red.

**Steps to reproduce:**
1. Go to https://www.saucedemo.com
2. Leave both fields empty and click Login
3. Notice both fields turn red
4. Now type `standard_user` in username, leave password empty, click Login
5. Both fields are still red — even though username is correct

**Expected:** Only the field that actually has a problem should turn red  
**Actual:** Both fields always turn red no matter which one is wrong

**Evidence:** `evidence/bug-001-both-fields-red.png`

---

## BUG-002 — Error Message Tells You If a Username Exists (Security Risk)

**Area:** Login Page  
**Severity:** High  
**Status:** Open

**What happened:**  
When I typed a valid username (`standard_user`) but the wrong password, the error message said:

> *"Epic sadface: Username and password do not match any user in this service"*

This message is basically telling anyone that the username is real but the password is wrong. A hacker can use this to figure out which usernames exist on the platform.

**Steps to reproduce:**
1. Go to https://www.saucedemo.com
2. Type `standard_user` in username
3. Type any wrong password
4. Click Login
5. Read the error message carefully

**Expected:** A vague message like `"Invalid credentials. Please try again."` — never confirm which part is wrong  
**Actual:** The message indirectly confirms the username is valid

**Why this matters:**  
An attacker can try hundreds of usernames and use the error messages to build a list of real accounts, then target them.

**Evidence:** `evidence/bug-002-username-disclosure.png`

---

## BUG-003 — You Can Try Wrong Passwords Forever (No Lockout)

**Area:** Login Page  
**Severity:** High  
**Status:** Open

**What happened:**  
I typed the wrong password and clicked Login 10+ times in a row. Nothing changed — no warning, no lockout, no delay, no CAPTCHA. The site just kept letting me try.

**Steps to reproduce:**
1. Go to https://www.saucedemo.com
2. Type `standard_user` in username
3. Type any wrong password
4. Click Login 10 times repeatedly
5. Notice nothing changes — you can keep trying forever

**Expected:** After 3–5 wrong attempts, the site should either:
- Lock the account temporarily
- Show a CAPTCHA
- Add a delay between attempts
- Show "X attempts remaining" warning

**Actual:** Unlimited attempts with no restriction at all

**Why this matters:**  
This allows automated tools to try thousands of passwords until they get in. Combined with BUG-002 (knowing which usernames are valid), this is a serious security hole.

**Evidence:** `evidence/bug-003-no-rate-limiting.png`

---

## BUG-004 — All Products Show a Dog Photo Instead of Product Images

**Area:** Product Catalog  
**Severity:** Critical  
**Status:** Open  
**User:** problem_user / secret_sauce

**What happened:**  
After logging in as `problem_user`, every single product on the catalog page shows the same image — a photo of a dog (pug) with a tennis ball in its mouth. The Backpack, Bike Light, T-Shirt, Fleece Jacket — all of them show this same dog photo.

**Steps to reproduce:**
1. Go to https://www.saucedemo.com
2. Login with username: `problem_user`, password: `secret_sauce`
3. Look at the product catalog
4. Notice every product has the same dog photo

**Expected:** Each product should display its own relevant product image  
**Actual:** All products display the same unrelated dog photo

**Why this matters:**  
In a real online store, product images are how customers decide what to buy. If every product looks the same, customers can't tell what they're purchasing. This would kill sales and destroy trust immediately.

**Evidence:** `evidence/bug-004-wrong-product-images.png`

---

## BUG-005 — Sorting Products Does Nothing

**Area:** Product Catalog  
**Severity:** High  
**Status:** Open  
**User:** problem_user / secret_sauce

**What happened:**  
On the product catalog page, there is a sort dropdown in the top right corner. When I clicked it and selected "Price (low to high)", the products did not reorder at all. The dropdown works visually — it opens and lets you select — but the actual sorting never happens.

**Steps to reproduce:**
1. Go to https://www.saucedemo.com
2. Login with username: `problem_user`, password: `secret_sauce`
3. On the products page, click the sort dropdown (top right, says "Name A to Z")
4. Select "Price (low to high)"
5. Notice the products do not reorder

**Expected:** Products should reorder from cheapest ($9.99) to most expensive  
**Actual:** Products stay in the exact same order — sorting has no effect

**Why this matters:**  
Sorting is one of the most used features on any shopping site. Customers use it to find the cheapest option or the best rated item. If sorting is broken, users get frustrated and leave.

**Evidence:** `evidence/bug-005-sorting-broken.png`

---

## Summary

| ID | Bug | Severity | Area |
|---|---|---|---|
| BUG-001 | Both fields turn red on single field error | Medium | Login UI |
| BUG-002 | Error message reveals if username exists | High | Login Security |
| BUG-003 | No lockout after repeated wrong passwords | High | Login Security |
| BUG-004 | All products show wrong dog image | Critical | Product Catalog |
| BUG-005 | Sort dropdown does nothing | High | Product Catalog |
