![Blackout Logo](2.svg)

# BLACKOUT — GTM behavior you can verify

**Blackout is a GTM Compliance platform** (RegTech × MarTech) that verifies what actually runs in the browser after **“Reject All”** and certifies it against the **Blackout Trust Standard (BTS)**.  
We don’t grade influence. **We verify behavior.**

---

## What is Ƀłⱥȼҟꝋᵾⱦ?

**Continuous, disclosure-grade verification** for hidden tracking and white-label surveillance.  
Detect what’s really running, diff it against what’s disclosed, and **auto-generate the receipts**.

---

## Why Blackout exists

- Everyone understands **SOC2/ISO**. Security earned its standard.  
- **Sales & marketing never did.** Vendors hid behind cookie banners and pay-to-play rankings while identity tech, session replay, and ad pixels still fire **after “Reject All.”**  
- Blackout makes GTM conduct **legible, testable, and enforceable**—with receipts.

> We don’t argue intent. **We publish timing and URLs.**

---

## What Blackout does (at a glance)

1. **Detect** — Capture post-consent timelines (initiator chains, request URLs, timestamps).  
2. **Diff** — Compare runtime vendors to your **subprocessor list** and stated policy.  
3. **Prove** — Hash the evidence pack and issue (or deny) a **BTS badge** (Bronze/Silver/Gold).  
4. **Enforce** — Badges can be **suspended or revoked** on critical drift. Public log.

All verification is performed **offline**. This site runs **no third-party trackers**.

---

## The Blackout Trust Standard (BTS)

**BTS is the evidence-based compliance standard for go-to-market behavior online.**

**Controls (evidence, not opinions):**  
- **Consent governance** — no identity/replay/ads fire post-reject  
- **Disclosure parity** — your policy ↔ your runtime  
- **De-anonymization** — explicit, verifiable opt-in or it’s out  
- **Proof** — initiator chains, request URLs, timestamps  
- **Attestation** — host a manifest at `/.well-known/blackout.json`  
- **Enforcement** — badge can be **suspended or revoked**

**Badge tiers:**  
- **BTS-Bronze (≥70)** — No identity/replay/ads post-reject; GPC honored; substantial subprocessor parity  
- **BTS-Silver (≥80)** — Bronze + no de-anon without explicit opt-in; full disclosure parity  
- **BTS-Gold (≥90)** — Silver + no session replay or fingerprinting; regional consent gating verified

**Badge label (alt):**  
`Blackout Trust Standard — {Tier} — Last verified: YYYY-MM-DD`

---

# BLK — The Blackout Compliance Framework (v0.1)

Operational controls, scoring, and schemas for verifying GTM runtime behavior against the **Blackout Trust Standard (BTS)**.

---

Control Library (v0.1)

IDs → Check → Suggested remediation.
Use these controls to detect runtime–policy gaps and fix disclosure, consent, and claims drift across your GTM stack.

**BLK-001 — Undisclosed Subprocessor**

- **CHECK:** Vendor in detections ∉ disclosures.
- **REMEDIATE:** Add vendor to subprocessor list; republish policy with version/date.

**BLK-002 — De-anonymization Without Notice**

- **CHECK:** category = "deanonymization" detected; no explicit identity-resolution notice/basis in policy.
- **REMEDIATE:** Add clear notice, lawful basis (opt-in/opt-out), retention, DPA references.

**BLK-003 — Session Recording Without Consent**

- **CHECK:** category = "session-replay" loads before recorded consent.
- **REMEDIATE:** Gate behind CMP; honor region logic and GPC.

**BLK-004 — Enrichment on PII Without Basis**

- **CHECK:** Enrichment calls after form submit; disclosures omit enrichment vendors/uses.
- **REMEDIATE:** Disclose enrichment purpose, vendors, retention; update DPA/ROPA.

**BLK-005 — Shadow Cookies / CNAME Cloak**

- **CHECK:** Third-party tracking via first-party CNAME; cookies set pre-consent.
- **REMEDIATE:** Disable until consent; document vendor + purpose; adjust DNS/CSP.

**BLK-006 — “Instant Outreach” from Web Events**

- **CHECK:** Webhook to SDR/LLM using visit-level signals; no disclosure of automated decisioning.
- **REMEDIATE:** Disclose automated processing; provide opt-out and escalation path.

**BLK-007 — Consent Timing Violation**

- **CHECK:** Any identity/replay/ads request timestamp < first consent accept; or persists after “Reject All.”
- **REMEDIATE:** Enforce true prior consent; block scripts until state is known.

**BLK-008 — GPC / DNT Not Honored**

- **CHECK:** Global Privacy Control or browser DNT ignored in regions where honored/claimed.
- **REMEDIATE:** Respect signals consistently; update policy to match behavior.

**BLK-009 — Region Gating Failure**

- **CHECK:** EU/UK/CA visitors receive identity/replay/ads despite regional gating claims.
- **REMEDIATE:** Fix geo logic; add region tests to CI; update manifests.

**BLK-010 — Fingerprinting / Evasion**

- **CHECK:** Canvas/audio/font fingerprinting or S3/CDN alias evasion (e.g., b2bjsstore S3).
- **REMEDIATE:** Remove non-essential fingerprinting; stop alias evasion; disclose unavoidable signals.

**BLK-011 — Policy–Runtime Mismatch**

- **CHECK:** Policy states “no X” but runtime shows X (or stale subprocessor revision).
- **REMEDIATE:** Bring runtime into compliance or update policy; date/version the change.

**BLK-012 — Unattributed Pixel / Unknown Vendor**

- **CHECK:** Network host not listed in disclosures or vendor registry.
- **REMEDIATE:** Identify owner; disclose or remove; add to vendor inventory.

**BLK-013 — Server-Side Bypass of Consent**

- **CHECK:** Server-to-server (CAPI/Segment/RudderStack/etc.) forwarding identity or event data while CMP state is Reject/Unknown.
- **REMEDIATE:** Enforce consent state in server pipelines; block enrichment/ads destinations until consent.

**BLK-014 — Hashed Email Matching Without Disclosure**

- **CHECK:** Outbound HEM (e.g., SHA-256 emails to ads/ID partners) with no explicit policy mention.
- **REMEDIATE:** Disclose hashed matching explicitly; add opt-out and retention.

**BLK-015 — Data Retention & Purpose Drift**

- **CHECK:** Policy lacks retention for identity/enrichment/session-replay OR runtime shows storage > N days with no stated purpose.
- **REMEDIATE:** Define retention windows per category; enforce TTL; update policy/ROPA.

**BLK-016 — CMP Misclassification / Dark Patterns**

- **CHECK:** Trackers labeled “strictly necessary” when they’re ads/analytics; reject path requires more clicks than accept; consent is bundled.
- **REMEDIATE:** Correct categories; equal friction; per-purpose toggles.

**BLK-017 — Opt-Out / Suppression Not Propagated**

- **CHECK:** User opt-out or GPC acknowledged, but downstream vendors continue processing (detected via follow-up pings).
- **REMEDIATE:** Implement suppression propagation to subprocessors; document SLA.

**BLK-018 — Cross-Border Transfer Without Basis**

- **CHECK:** Runtime shows transfer to non-adequacy region (e.g., US) without SCC/appropriate safeguards disclosed.
- **REMEDIATE:** Add transfer basis (SCCs/Art.49), update DPA; or regionalize.

**BLK-019 — Webhook/LLM Data Leakage**

- **CHECK:** Webhooks to Slack/LLM endpoints include raw PII or sensitive fields not minimized.
- **REMEDIATE:** Minimize payload; mask PII; add field allow-list and secrets management.

**BLK-020 — “Respect for Signals” Scope Mismatch**

- **CHECK:** Policy claims “we honor GPC/DNT,” but only some categories are suppressed at runtime.
- **REMEDIATE**: Honor signals across all relevant categories (ads, identity, replay); update policy if scope is narrower.

**BLK-021 — “Compliant” Claim vs. Reality**

- **CHECK:** Public claims like “GDPR/CCPA compliant,” “privacy-first,” “no cookies,” “cookieless analytics.” Runtime shows tracking or consent patterns that contradict.
- **REMEDIATE:** Remove absolute compliance claims; replace with specific controls (“gated by consent,” “opt-out honored incl. GPC”); update creatives/LPs.

**BLK-022 — “Anonymized” Claim, Person-Level Behavior**

- **CHECK:** Ads/posts/LPs say “anonymous” or “no PII,” while identity resolution, hashed email matching, or outreach tied to visit is detected.
- **REMEDIATE:** Change language to “pseudonymous” with scope/basis/retention, or stop person-level processing.

**BLK-023 — “Cookieless” Claim, Fingerprinting/Server-Side**

- **CHECK:** “Cookieless” marketing while canvas/WebGL/device fingerprints or server-side forwarding (CAPI/Segment/Rudder) run pre-consent.
- **REMEDIATE:** Disclose fingerprinting/server-side uses; gate by consent or remove non-essential signals; align copy.

**BLK-024 — “We Don’t Retarget/Share” vs. Pixels/HEM**

- **CHECK:** “No retargeting/sharing” claim while Meta/LinkedIn/Google pixels or hashed email matching (HEM) are active.
- **REMEDIATE:** Disclose destinations & purposes or disable; add opt-out and suppression propagation.

**BLK-025 — Automated Decisioning Omission in Ads**

- **CHECK:** Ads/LPs pitch “instant outreach,” “AI routing,” or “self-driving SDR,” but provide no disclosure of automated decisioning or escalation path.
- **REMEDIATE:** Add plain-English notice of automated processing, human review path, and opt-out on the LP and policy.

**BLK-026 — Influencer/Founder Posts Without Disclosure**

- **CHECK:** Paid/affiliated posts (employees, creators, partners) lack material-connection disclosure (#ad, “paid partnership,” etc.).
- **REMEDIATE:** Mandate disclosure in all creator briefs; approve copy; archive proof.

**BLK-027 — Badge/Seal/Logo Misrepresentation**

- **CHECK:** Use of “GDPR,” “CCPA” badges, certification logos, or customer logos implying endorsement when none exists or scope is misstated.
- **REMEDIATE:** Remove badges/logos or add accurate scope; maintain rights/ROE docs.

**BLK-028 — Opt-Out/Do-Not-Sell Claim vs. Journey**

- **CHECK:** Ads/promos promise “easy opt-out,” but landing & downstream flows require dark-pattern steps or don’t propagate suppression to vendors.
- **REMEDIATE:** Equal-friction opt-out; propagate to subprocessors; show confirmation.

**BLK-029 — Sensitive-Category Targeting**

- **CHECK:** Ad sets target or infer sensitive attributes (health, children, sexual life, precise location) while public copy claims “no sensitive data.”
- **REMEDIATE:** Remove sensitive targeting; update targeting policy and public claims.

**BLK-030 — “Security/Privacy Certified” Scope Creep**

- **CHECK:** Claims like “SOC 2 / ISO certified” used to imply privacy compliance for ads/ID tech that’s out of certification scope.
- **REMEDIATE:** Limit claims to the certified system and scope; add explicit scope statements and caveats; remove misleading badges from ads/LPs; link to current report dates.

Implementation note: Add these to docs/CONTROLS.md and reference from the main README under Blackout Enterprise → Control Library.
---

## Risk & Scoring

- **Severity (S):** 1–5 (user harm / regulatory exposure)  
- **Exposure (E):** pages affected × traffic class `{WEBSITE|APP|AUTH}` ⇒ weight `{1|2|3}`  
- **Remediation Difficulty (R):** 1–3 (effort/time/risk)

**Non-Compliance Score = (S × E) + R** (per control, capped by control policy)

**Critical flags:**  
- If **BLK-001** or **BLK-002** present → mark **CRITICAL**.  
- If **BLK-007** present with identity/replay/ads → mark **CRITICAL**.

**Badge guidance (map to BTS):**
- `Score < 10` and **no Critical** → candidate **BTS-Bronze** (if all identity/replay/ads post-reject = none)  
- `10–19` and **no Critical** → candidate **BTS-Silver** after remediation of disclosure gaps  
- `≥20` or **any Critical** → **BTS-Denied** until fixes verified  
- **BTS-Gold** requires **no** session-replay/fingerprinting and clean region gating

---

## Minimal UI (week one)

- **Projects:** domain · last scan · score · critical flags · “Download Pack”  
- **Findings:** detections list & gaps list with evidence chips `{script|network|global|cookie|inline}`  
- **Controls:** pass/fail by BLK ID with remediation copy & owners

---

## Data Model (JSON Schemas)

### Detection
```json
{
  "id": "det_01HZZ7N...",
  "domain": "example.com",
  "vendor_id": "warmly",
  "category": "deanonymization",
  "artifact": { "type": "script", "value": "https://cdn.../warmly.js" },
  "consent_state": "reject", 
  "ts_first_seen": "2025-11-05T03:12:30.120Z",
  "ts_last_seen": "2025-11-05T03:12:30.120Z",
  "confidence": 0.96,
  "signals": ["network", "script", "global"]
}
```


## The Blackout Ecosystem

**One mission: rebuild trust with evidence—not influence.**

### 🏢 Blackout for Teams — *The Console (available)*
Private audits for Legal/RevOps. Consent timelines, initiator chains, **disclosure-vs-runtime** diffs, and counsel-ready exports. Every vendor called by name in your report.

### 🛡️ Blackout Sensor — *The Shield (roadmap)*
Opt-in **Proof Cards** and alerts so individuals can see who’s watching before the pitch—and correlate outreach to detections they can share.

### 🔗 BLK — *Blackout Ledger (roadmap)*
Evidence-hash registry and attestation APIs for CI/security controls. Public **revocation log** and open signature sets.

> **No on-site scanner.** Verification is offline; evidence packs are shareable with counsel.

---

## How it works (verify & certify, not block)

**Observe** — Capture post-consent timelines: initiator chains, request URLs, timestamps.  
**Compare** — Diff runtime vendors against subprocessor/privacy disclosures.  
**Attest** — Hash the evidence pack (SHA-256); issue **BTS** or remediation.  
**Enforce** — Badges are **revocable**; critical drift triggers suspension & re-verification.

### Detection signals (multi-layer)
- Script hosts & loader patterns (incl. CDN → **S3** fallbacks)  
- Window globals & inline init calls  
- Network patterns (hosts, paths, cache-busting)  
- Consent timing vs first request  
- Fingerprinting/replay surfaces

**Example evidence line:**  
+186 ms post-reject → s3-us-west-2.amazonaws.com/b2bjsstore/.../reb2b.js.gz

---

## What Blackout is **not**

- Not a browser, ad-blocker, or on-site widget  
- Not pay-to-play rankings or “magic shapes”  
- Not a legal opinion—**we provide counsel-ready evidence**, not promises

---

## Manifest (attestation)

Publish a machine-readable manifest so buyers can self-check basics.

`/.well-known/blackout.json`
```json
{
  "bts_version": "0.1",
  "badge": { "tier": "silver", "score": 83, "last_verified": "2025-11-07" },
  "disclosures": {
    "policy_url": "https://example.com/privacy",
    "subprocessors_url": "https://example.com/subprocessors"
  },
  "runtime": {
    "region_gating": true,
    "consent_gpc_honored": true
  },
  "evidence": {
    "pack_sha256": "7b2c...c1a9",
    "report_url": "https://example.com/blackout/report.pdf"
  }
}
```
R## Responsible disclosure & revocation

- **Private remediation window** for badged companies  
- **Dispute → re-scan → logged outcome**  
- **Critical breach** (e.g., identity/replay firing post-reject) → **72-hour** remediation or **public suspension**  
- **Public revocation log** keeps the badge honest

---

## RFP clause (copy/paste)

> Vendor must maintain **BTS-Silver or higher** and host a valid `/.well-known/blackout.json`. Buyer may perform independent runtime verification prior to award and quarterly thereafter. Badge suspension is grounds for reassessment.

---

## Roadmap (high-level)

- Public **revocation log**  
- **Open signatures** for vendor detection (PRs welcome)  
- **BLK** attestation & evidence-hash APIs  
- Partner labs for adversarial testing and signature hardening

---

## Contributing

- Propose vendor signatures (host/path regex, function-chain fingerprints, consent-timing rules)  
- Submit redacted **Proof Cards** (URLs + timings only; no PII)  
- File issues with reproducible steps and timestamps

---

## Ethics & privacy posture

- We store **observable runtime facts** (timelines, URLs, initiators).  
- **No PII. No fingerprinting. No cookie planting.**  
- Sensor (when available) will be strictly **opt-in**; users choose what to share.

---

## Get certified / Get involved

- **Founding Cohort** — Priority audits & early steering input  
- **Request an Enterprise Audit** — Legal/RevOps ready  
- **Join the Sensor Waitlist** — Personal Proof Cards & alerts

**Site:** https://www.deployblackout.com  
**Contact:** hello@deployblackout.com
