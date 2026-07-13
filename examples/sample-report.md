# Competitor Research Report: SaaS Billing Portal

* **Generated On:** 2026-07-13T12:00:00Z
* **Target Audience:** B2B SaaS Founders and Finance Teams
* **Focus Areas:** Checkout Flow, Billing Portal

---

## 📋 Executive Summary
This report analyzes Stripe Billing, Paddle, and Lago to identify UX best practices for B2B billing portals. Standard checkout forms prioritize multi-step wizard layouts to reduce form anxiety, whereas developer-focused tools (Lago) emphasize open-source self-hosting configurations and simple tables.

---

## 👥 Competitor Landscape

### 1. Stripe Billing
* **Website:** https://stripe.com/billing
* **Market Share:** Leader
* **Strengths:** Unmatched API flexibility, robust developer ecosystem, smooth standard checkout.
* **Weaknesses:** Complex setup for customized enterprise multi-metric usage billing.

### 2. Paddle
* **Website:** https://www.paddle.com
* **Market Share:** Leader / Merchant of Record (MoR)
* **Strengths:** Handles international tax/VAT compliance automatically out of the box.
* **Weaknesses:** Higher transaction fees, less layout customization.

---

## 📊 Feature Comparison Matrix

| Feature | Stripe Billing | Paddle | Lago | Our Product (Opportunity) |
| :--- | :---: | :---: | :---: | :---: |
| **VAT/Tax Management** | ⚠️ (Stripe Tax) | ✅ (Inbuilt) | ❌ | **✅ (Inbuilt Partner)** |
| **Usage Metering API** | ✅ | ⚠️ | ✅ | **✅ (Real-time Edge)** |
| **Self-hostable Option**| ❌ | ❌ | ✅ | **❌ (Cloud Only)** |

*Legend: ✅ Fully Supported | ⚠️ Partially Supported | ❌ Not Supported*

---

## 🖼️ UX Pattern Library: Checkout Flow

#### 🔍 Pattern Overview
* **Competitor:** Stripe Billing
* **Objective:** Streamline multi-payment method checkouts.

#### 📸 Step-by-Step Flow Evidence
```carousel
![Step 1: Payment Method Choice](assets/screenshots/competitor-stripe-checkout-1.png)
* **Description:** Auto-detects region and displays local payment methods (Card, Link, Apple Pay) in order of popularity.
* **Selectors:** `iframe.stripe-element`

<!-- slide -->

![Step 2: 1-Click Verification](assets/screenshots/competitor-stripe-checkout-2.png)
* **Description:** Link autofills card details upon entering verification code.
* **Selectors:** `input#verification-code`
```

---

## 💡 Product Opportunities & Action Plan

We prioritized opportunities using a standard Impact/Effort matrix:

| Opportunity | Type | Impact | Effort | Priority |
| :--- | :--- | :---: | :---: | :---: |
| **One-click Checkout Autofill** | UX Improvement | High | Medium | **P0** |
| **Global Tax Partner Integration** | Feature Gap | High | High | **P1** |

---

*Report generated automatically by the Antigravity Competitor Analysis Agent.*
