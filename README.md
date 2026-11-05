# SAHAYAK

**A voice-first AI assistant that connects Scheduled Caste beneficiaries to the right skilling trade, the right government scheme, and a safe way to report discrimination — in their own language.**

Smart India Hackathon 2026 · Problem Statement **SIH26097**
Ministry of Social Justice and Empowerment (MoSJE) · PM-AJAY, Grant-in-Aid (GIA) component
Team **Hacksphire 2.0** · Team ID 140037

---

## The problem

PM-AJAY's GIA component exists to lift Scheduled Caste communities out of poverty through skilling, livelihood and enterprise support. But on the ground:

- **People are enrolled in trades that don't fit them.** Training is often chosen without understanding a person's interests, family occupation or local job market, so dropout is high and placement is low.
- **The people who need help most are the hardest to reach digitally.** Many beneficiaries have low literacy, speak regional dialects, and cannot navigate text-heavy forms or portals.
- **Scheme information goes stale.** Schemes change, deadlines pass, and people miss benefits simply because nobody told them in time.
- **Officials lack a live picture.** Tracking enrolment, dropout and placement across districts is slow and manual.

Some numbers behind this (public sources; verify before citing):

| Indicator | Figure |
|---|---|
| PMKVY trained candidates with recorded placement | ~7% (Business Today) |
| Enrolled candidates who dropped out, FY 2024-25 | ~35% (Business Today) |
| Digital literacy, rural vs urban households | ~25% vs ~60% |
| Internet penetration, rural vs urban | ~37% vs ~67% (TRAI, Dec 2022) |

## The idea

SAHAYAK replaces forms with a **conversation**. A beneficiary speaks naturally — in Hindi or a regional dialect — about their education, family trade, current work, interests, mobility and whether they want a job or their own enterprise. SAHAYAK then:

1. **Understands** the profile from that conversation.
2. **Matches** it to NSQF-aligned training trades and to government schemes that are currently active.
3. **Explains** every recommendation in plain language, so nothing is a black-box score.
4. **Tracks** the journey for GIA officials on a live dashboard.

It works on a **website** and on **WhatsApp**, so a person with a smartphone can use whichever channel they already know.

## What it does

### Voice-first, empathetic interview
No typing and no forms. The assistant asks short, friendly questions and builds the beneficiary's profile as they talk. The same conversation runs identically on the website and on WhatsApp.

### Explainable semantic matching
People rarely use official trade names. Someone who says *"darzi"* has never said *"tailoring"*. SAHAYAK expands what a person says into shared concepts (Hindi, Hinglish and English variants), tolerates spelling differences, and then ranks NSQF trades and schemes against the profile.

Every result comes with a reason, for example:

> *Tailoring & Fashion Design — because "darzi" maps to the Tailoring concept cluster.*

If the answers don't support a confident match, SAHAYAK says so and routes the person to a human counsellor instead of guessing.

### Live government scheme layer
Scheme data is meant to be refreshed on a schedule from public sources (MyScheme, PM-AJAY) so recommendations don't go stale. If a source can't be reached, SAHAYAK keeps the last good data and shows the **real** last-synced time — it never claims a sync that didn't happen.

### GIA official dashboard
Officials get a live view of enrolment, matches, channel usage and dropout risk, instead of compiling spreadsheets. Roles are designed for Beneficiary, GIA Official, Skill Partner and Administrator.

### Grievance support
A beneficiary can raise and track a complaint about caste-based discrimination through the same simple interface. This is an **assisted intake and routing layer** towards the appropriate channel under the existing SC/ST (Prevention of Atrocities) Act, 1989 framework. It does not replace a formal legal complaint.

## How it works (at a glance)

```
Beneficiary speaks  →  profile builds up  →  concept-expansion matching
   (Website / WhatsApp)                            │
                                                   ├→ NSQF trades (ranked, with reasons)
                                                   └→ Active schemes (live-synced)
                                                   │
                                       GIA dashboard · grievance routing
```

## Technology

React, Node.js and Express; SQLite for the prototype (PostgreSQL and Redis planned for scale); Twilio for WhatsApp; Whisper and Bhashini for speech; a custom concept-expansion matching engine that runs fully offline; JWT, AES-256 and DPDP Act 2023-aligned consent by design; cloud deployment on AWS or MeghRaj.

## Why this approach

- **Inclusion first.** Voice and WhatsApp meet people where they already are, instead of asking them to learn a new portal.
- **Explainable by design.** A recommendation that can't say *why* is hard to trust and hard to audit. SAHAYAK shows its reasoning.
- **Honest about uncertainty.** "No clear match" is a valid, safe answer.
- **Built on public infrastructure.** Bhashini, MyScheme and NSQF are reused rather than reinvented.

## Where the project stands

Being upfront about maturity:

| Area | Status |
|---|---|
| Conversational interview flow (website + WhatsApp logic) | Built; WhatsApp needs a live Twilio account to run |
| Concept-expansion matching with explanations | Built; **48% on a small held-out test set of unseen phrasings** (100% on the set it was built from, which is not a fair measure) |
| "No clear match" handling | Built |
| Scheme sync with honest timestamps | Pipeline built; real MyScheme source access not yet working (site is JavaScript-rendered) |
| GIA dashboard | Prototype |
| Grievance filing | Prototype UI only; no backend yet |
| Voice transcription (Whisper / Bhashini) | Planned, not implemented |
| Authentication, encryption at rest, consent and audit logs | Designed, not implemented |
| IVR for feature phones | Roadmap |

The matching vocabulary is small and hand-written, so accuracy on real village speech is the main open question. The next step is collecting real beneficiary utterances and expanding coverage, or moving to a multilingual embedding model.

## Roadmap

1. Validate matching on real beneficiary speech and widen the vocabulary.
2. Connect a real, permitted scheme data source.
3. Voice-note transcription for WhatsApp in regional languages.
4. Authentication, consent capture and audit trail.
5. Grievance backend with accountable routing and status tracking.
6. IVR for feature-phone users.
7. Pilot with one district and measure match quality, completion and placement.

## Impact we're aiming for

Better-matched enrolment, lower dropout, fewer missed schemes, access for low-literacy and low-connectivity users, an easier route to report discrimination, and real-time data for officials. These are goals to be proven in a pilot, not measured results today.

---

*Built for Smart India Hackathon 2026.*
