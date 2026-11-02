# Accepting donations in India on WordPress: 80G, Form 10BD and 10BE

A practical reference for anyone building or running a donation page for an Indian nonprofit on WordPress or WooCommerce. Written because almost every donation plugin is built for US 501(c)(3) organisations, and Indian NGOs only discover the gap at audit.

Maintained by [Discounly](https://discounly.com). Corrections welcome — open an issue.

> Not legal or tax advice. Rules change; verify against the Income Tax Department before you rely on anything here.

## Contents

- [What an Indian donor actually needs](#what-an-indian-donor-actually-needs)
- [Form 10BD and Form 10BE](#form-10bd-and-form-10be)
- [What you have to capture at donation time](#what-you-have-to-capture-at-donation-time)
- [Where most plugins fall short](#where-most-plugins-fall-short)
- [Payment methods that matter in India](#payment-methods-that-matter-in-india)
- [FCRA, briefly](#fcra-briefly)
- [Implementation checklist](#implementation-checklist)

## What an Indian donor actually needs

A donor claiming a deduction under **Section 80G** needs a receipt from the organisation and, since the 2021 amendments, a **Form 10BE certificate** that the organisation issues after filing its annual **Form 10BD** statement. The donor's claim is matched against what the organisation reported. If the organisation never filed, the donor's deduction fails — regardless of what the receipt said.

This is the structural difference from the US model. A US nonprofit issues a receipt and the transaction ends. An Indian nonprofit issues a receipt **and** must report every donation back to the tax department, per donor, annually.

## Form 10BD and Form 10BE

| | |
|---|---|
| **Form 10BD** | A statement of donations received, filed by the organisation, listing every donor individually |
| **Form 10BE** | The certificate the organisation then issues to each donor, generated from the 10BD filing |
| **Who files** | Any organisation approved under 80G or registered under 35(1) |
| **Deadline** | 31 May following the end of the financial year |
| **Consequence of not filing** | Late fees, and donors lose their deduction |

The practical implication for software: **every donation needs donor identification captured at the moment of payment**, because reconstructing it ten months later from a payment gateway export is painful and often impossible.

## What you have to capture at donation time

Form 10BD requires, per donor:

- **Name** and **address**
- **Identification type and number** — PAN, Aadhaar, passport, voter ID, driving licence or ration card, in that order of preference
- **Donation type** — corpus, specific grant, or other
- **Mode** — cash, cheque, electronic, kind
- **Section** under which the donation qualifies
- **Amount**

A donation form that collects name, email and amount has already lost the data. PAN in particular is the one donors expect to be asked for and the one plugins built elsewhere never ask.

## Where most plugins fall short

| Gap | Why it bites |
|---|---|
| No identification field | Form 10BD cannot be filed without it; retrofitting means emailing every donor |
| Receipts without 80G details | A receipt that omits the organisation's 80G registration number and validity isn't usable |
| No 10BD-shaped export | Finance ends up rebuilding the statement by hand from a gateway CSV |
| Corpus not distinguished | Corpus donations are reported differently; if it wasn't captured, it can't be separated |
| Financial year assumed Jan–Dec | India's runs April–March, which breaks every annual total |
| Anonymous donations unflagged | Treated differently under Section 115BBC |

## Payment methods that matter in India

- **UPI** dominates one-time giving. Donation flows that assume card entry lose most mobile donors.
- **UPI Autopay** is the mechanism for recurring giving. Card-based subscriptions see high failure rates on Indian cards after the RBI's recurring-payment rules; e-mandate via UPI Autopay is the practical path for monthly donors.
- **Razorpay and Cashfree** are the common gateways. Stripe's India availability is narrower than international plugin documentation usually implies.
- **Net banking** still matters for larger donations.

## FCRA, briefly

Accepting foreign contributions requires **FCRA registration** and, since 2020, routing through the designated **FCRA account at State Bank of India, New Delhi Main Branch**. Foreign donations cannot be mixed with domestic ones.

For a donation page this means foreign and domestic giving are **two different flows into two different accounts**, not one form with a currency switcher. Plugins that treat currency as a display option get this wrong by default.

## Implementation checklist

- [ ] Capture name, address, identification type and number at donation time
- [ ] Make PAN collection prominent, with an explanation of why
- [ ] Distinguish corpus from general donations on the form
- [ ] Put the 80G registration number and validity on every receipt
- [ ] Generate receipts immediately, not in a monthly batch
- [ ] Export in Form 10BD's column order and shape
- [ ] Run totals on an April–March financial year
- [ ] Flag anonymous donations separately
- [ ] Offer UPI for one-time and UPI Autopay for recurring
- [ ] Keep foreign contributions in a separate flow if FCRA-registered
- [ ] Store donor records where they can be produced at audit

## Contributing

Corrections, clarifications and citations are welcome — especially from people who have actually filed a 10BD. Open an issue or a pull request.

## Related

Discounly builds [Discounly Donate](https://discounly.com), a self-hosted WordPress donation plugin that handles 80G receipts and Form 10BD for Indian NGOs. This document is a reference, not a sales page; it is correct whether or not you use that plugin.
