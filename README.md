# Swag Labs — QA Testing Assignment

**Tester:** Muhammad Mehboob 
**Website tested:** https://www.saucedemo.com  
**Type:** Manual QA Testing  
**Date:** August 14, 2026

---

## What's in This Repo

```
swag-labs-qa/
│
├── README.md          ← you are here
├── test-plan.md       ← full test plan with test cases
├── bug-report.md      ← 5 bugs found with steps to reproduce
│
└── evidence/          ← upload your screenshots here
    ├── bug-001-both-fields-red.png
    ├── bug-002-username-disclosure.png
    ├── bug-003-no-rate-limiting.png
    ├── bug-004-wrong-product-images.png
    └── bug-005-sorting-broken.png
```

---

## How I Tested

I tested this site manually using Chrome browser. No automation tools were used — this is pure manual QA testing.

**Test accounts used:**
| Username | Password | Purpose |
|---|---|---|
| standard_user | secret_sauce | Normal user flow |
| locked_out_user | secret_sauce | Locked account behavior |
| problem_user | secret_sauce | Bug hunting — most bugs here |
| performance_glitch_user | secret_sauce | Performance testing |

---

## What I Found

- **5 bugs** documented in `bug-report.md`
- **2 bugs are security related** (no rate limiting, username disclosure)
- **1 critical bug** (wrong images on all products)
- All bugs were found on the Login page and Product Catalog

---

## Documents

| File | What it contains |
|---|---|
| `test-plan.md` | Test scope, test cases, risk assessment |
| `bug-report.md` | 5 detailed bug reports with steps to reproduce |
| `evidence/` | Screenshots proving each bug |
