# Test Plan — Swag Labs (saucedemo.com)

**Tester:** [Your Name]  
**Date:** August 14, 2026  
**Type:** Manual QA Testing

---

## 1. Scope — What I'm Testing

| Feature | Included |
|---|---|
| Login page | ✅ Yes |
| Product catalog | ✅ Yes |
| Shopping cart | ✅ Yes |
| Checkout flow | ✅ Yes |
| Navigation & menus | ✅ Yes |
| Payment processing | ❌ No — simulated only |

---

## 2. Types of Testing

**Functional Testing** — Does each feature actually work as expected?  
**Negative Testing** — What happens when I do something wrong (wrong password, empty fields)?  
**UI Testing** — Does the page look correct? Are images, labels and buttons right?  
**Security Testing** — Can I brute force login? Does the site reveal too much information?  
**Edge Case Testing** — What happens at the boundaries (empty cart checkout, special characters in fields)?

---

## 3. Test Environment

| Item | Details |
|---|---|
| Browser | Google Chrome (latest) |
| OS | Windows 11 |
| Device | Desktop |
| Internet | Standard broadband |
| Test URL | https://www.saucedemo.com |

---

## 4. Test Data

| Username | Password | Expected Behavior |
|---|---|---|
| standard_user | secret_sauce | Normal login, everything works |
| locked_out_user | secret_sauce | Should show locked account error |
| problem_user | secret_sauce | Has intentional bugs |
| performance_glitch_user | secret_sauce | Slow loading times |

---

## 5. Test Cases

---

### TC-001 — Login with Valid Credentials

**Area:** Login  
**Type:** Functional

**Steps:**
1. Go to https://www.saucedemo.com
2. Enter `standard_user` in username
3. Enter `secret_sauce` in password
4. Click Login

**Expected:** User is taken to the Products page successfully  
**Actual:** ✅ Pass — redirected to products page  

---

### TC-002 — Login with Locked Out Account

**Area:** Login  
**Type:** Functional / Negative

**Steps:**
1. Go to https://www.saucedemo.com
2. Enter `locked_out_user` in username
3. Enter `secret_sauce` in password
4. Click Login

**Expected:** Clear error message saying the account is locked  
**Actual:** ✅ Pass — error message appears (though with unprofessional "Epic sadface" prefix)

---

### TC-003 — Login with Empty Fields

**Area:** Login  
**Type:** Negative / Edge Case

**Steps:**
1. Go to https://www.saucedemo.com
2. Leave both fields empty
3. Click Login
4. Then try username only, then password only

**Expected:** Only the empty field should be highlighted red  
**Actual:** ❌ Fail — both fields turn red even when only one is empty (see BUG-001)

---

### TC-004 — Login with Wrong Password Multiple Times

**Area:** Login  
**Type:** Security / Negative

**Steps:**
1. Go to https://www.saucedemo.com
2. Enter `standard_user` in username
3. Enter wrong password
4. Click Login 10 times repeatedly

**Expected:** Account should lock or CAPTCHA should appear after 3–5 attempts  
**Actual:** ❌ Fail — no lockout, no CAPTCHA, unlimited attempts allowed (see BUG-003)

---

### TC-005 — Product Images Display Correctly

**Area:** Product Catalog  
**Type:** UI / Functional

**Steps:**
1. Login as `problem_user` / `secret_sauce`
2. Look at the product catalog
3. Check if each product shows its own unique image

**Expected:** Each product displays its own relevant image  
**Actual:** ❌ Fail — all products show the same dog photo (see BUG-004)

---

### TC-006 — Sort Products by Price

**Area:** Product Catalog  
**Type:** Functional

**Steps:**
1. Login as `problem_user` / `secret_sauce`
2. On the products page click the sort dropdown
3. Select "Price (low to high)"
4. Check if products reorder

**Expected:** Products reorder from cheapest to most expensive  
**Actual:** ❌ Fail — products do not reorder at all (see BUG-005)

---

### TC-007 — Add Item to Cart

**Area:** Shopping Cart  
**Type:** Functional

**Steps:**
1. Login as `standard_user` / `secret_sauce`
2. Click "Add to Cart" on any product
3. Check the cart icon in the top right

**Expected:** Cart icon shows a badge with count "1", button changes to "Remove"  
**Actual:** To be tested

---

### TC-008 — Complete Full Checkout

**Area:** Checkout  
**Type:** Functional / End-to-End

**Steps:**
1. Login as `standard_user` / `secret_sauce`
2. Add an item to cart
3. Click cart icon
4. Click Checkout
5. Fill in first name, last name, zip code
6. Click Continue then Finish

**Expected:** Order completes successfully, confirmation page shown  
**Actual:** To be tested

---

## 6. Risk Assessment — Where Bugs Are Most Likely

| Area | Risk Level | Reason |
|---|---|---|
| Login security | 🔴 High | No rate limiting, revealing error messages |
| Product catalog (problem_user) | 🔴 High | Images and sorting both broken |
| Checkout price calculation | 🟡 Medium | Easy to miscalculate tax or totals |
| Cart persistence | 🟡 Medium | Cart may not save when navigating away |
| Navigation / back button | 🟡 Medium | Back button after checkout may cause issues |
| Standard user login | 🟢 Low | Works as expected |
