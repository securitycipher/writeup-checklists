---
id: e889e9c7eded
title: "The Art of Business Logic - When the Checkout Got the Price Wrong"
source_url: https://zuksh.medium.com/the-art-of-business-logic-when-the-checkout-got-the-price-wrong-4d548971b4a3
author: "Zuksh"
publication_date: 2026-08-22
category: business-logic
category_label: "Business Logic"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "web-security"
  - "application-security"
  - "business-logic"
  - "bug-bounty"
  - "cybersecurity"
tools:
  - "Burp Suite"
quick_test: "Test if modifying cart state during the checkout process can lead to an incorrect final amount being calculated by the server."
---

## Use case

The e-commerce application had a business logic flaw that allowed an attacker to manipulate the cart state, resulting in an incorrect checkout price that was lower than the legitimate product price. This vulnerability could lead to financial loss for the business if exploited.

## Steps to test

1. Select a product by sending a GET request to /api/products/1337.
2. Add the product to the cart by sending a POST request to /api/cart/items with { 'productId': 1337, 'quantity': 1 }.
3. Confirm the normal checkout price by sending a POST request to /api/checkout/preview with { 'cartId': 'CART-12345' }.
4. Intercept the cart-state request and modify the relevant state parameter.
5. Send the modified cart state back to the server.
6. Trigger the checkout calculation again by sending a POST request to /api/checkout/preview with { 'cartId': 'CART-12345' }.

## Commands

```text
GET /api/products/1337 HTTP/2
POST /api/cart/items HTTP/2
Host: shop.example
Content-Type: application/json
{ 'productId': 1337, 'quantity': 1 }
POST /api/checkout/preview HTTP/2
Host: shop.example
Content-Type: application/json
{ 'cartId': 'CART-12345' }
POST /api/cart/<cart-action> HTTP/2
Host: shop.example
Content-Type: application/json
{ 'cartId': 'CART-12345', '...' }
Product
↓
Cart
↓
Discount / Promotion
↓
Checkout
↓
Payment
GET /api/products/1337 HTTP/2
Host: shop.example
Accept: application/json
{
"id": 1337,
"name": "Premium Product",
"price": 999,
"currency": "EUR"
}
POST /api/cart/items HTTP/2
Host: shop.example
Content-Type: application/json
{
"productId": 1337,
"quantity": 1
}
{
"cartId": "CART-12345",
"items": [
{
"productId": 1337,
"quantity": 1,
"unitPrice": 999,
"total": 999
}
],
"total": 999,
"currency": "EUR"
}
```

## Source

- Author: Zuksh
- Writeup: https://zuksh.medium.com/the-art-of-business-logic-when-the-checkout-got-the-price-wrong-4d548971b4a3

_For authorized testing only. Credit the original author._
