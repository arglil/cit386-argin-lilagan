# CIT 386 — Module 4: Issue a Token, and Prove What It Does

**Submission type:** Documentation-only simulation; **not a completed live SAS test**  
**Platform:** Azure Blob Storage (illustrative configuration)  
**Reason:** Prepared as an alternative exercise; instructor approval is required before this can substitute for the live assignment.

## 1. Proposed SAS parameters (recorded before issuance)

| Parameter | Proposed setting | Notes |
|---|---|---|
| Resource | A blob containing my own course page, inside my assigned storage area | Use the exact blob path assigned to me; do not access other students' data. |
| SAS type | Blob-level service SAS | Limits the token to one blob; a blob SAS does not grant container listing. |
| Signed resource (`sr`) | `b` (blob) | Not `c` (container). |
| Permissions (`sp`) | `r` (read) | Do not select list, write, add, create, or delete. |
| Protocol (`spr`) | `https` | Require HTTPS. |
| Start time (`st`) | **[NOT SET — choose UTC date/time when testing]** | Allow for clock skew if needed. |
| Expiry (`se`) | **[NOT SET — choose UTC date/time within the course term]** | Set a bounded expiration. |
| IP range (`sip`) | Not restricted in this example | If restricting IPs, document the exact approved range. |
| Signing method | **[NOT SELECTED]** | Record whether account-key-signed or user-delegation SAS is used. |
| Signature (`sig`) | **[REDACTED — NEVER RECORD]** | A SAS URL is a bearer credential. |

**Execution status:** No SAS was generated for this document. These are proposed settings, not actual Azure portal selections.

## 2. What does the token permit?

**Expected behavior:** A browser session not signed into Azure should be able to download or display the specifically named blob over HTTPS while the read-only SAS is valid. It should not need portal authentication because the SAS URL itself authorizes the request.

**Actual evidence:** Not collected. To verify, open an InPrivate/Incognito window, load the **own-blob** SAS URL, and record the visible result without exposing `sig`.

- Browser test date/time (UTC): **[NOT TESTED]**
- Requested blob (redacted URL): `https://<storage-account>.blob.core.windows.net/<container>/<own-blob>?...&sig=[REDACTED]`
- Browser result: **[NOT TESTED]**
- Screenshot: **[NOT CAPTURED]**

## 3. What does the token forbid?

**Expected behavior:** A blob-scoped read SAS does not grant permission to enumerate the container or modify the blob. A container listing request made with the same SAS should be rejected, but the exact service error depends on the request and its parameters.

**Actual refused-operation evidence:** Not collected. Test only the container holding your own blob, and do not inspect anyone else's content.

- Attempted operation: Container listing using the blob SAS, e.g. a request with `restype=container&comp=list` against the **own container**.
- Browser or HTTP response: **[NOT TESTED]**
- Exact Azure error code: **[NOT OBSERVED — DO NOT INVENT]**
- Screenshot: **[NOT CAPTURED]**

## 4. From where can the token be used?

**Proposed restriction:** HTTPS only (`spr=https`), with no IP address restriction in this example. Possession of the URL is sufficient for access within its scope and validity window; the SAS is not tied to the recipient's Azure portal account. A recipient must use a network path that can reach the storage endpoint and comply with any separate storage firewall restrictions.

**Actual test:** Not performed.

## 5. Between which two moments does access work?

**Proposed normal token:** Starts at **[UTC START NOT SET]** and expires at **[UTC END NOT SET]**, within the course term.

**Short-lived second token:** Create a separate read-only, HTTPS-only blob SAS expiring a few minutes after issuance. Test the same own blob before expiry, then again after expiry.

| Test | Expected | Actual observation | Exact error code |
|---|---|---|---|
| Before expiry | Blob opens | **[NOT TESTED]** | Not applicable until tested |
| After expiry | Access refused | **[NOT TESTED]** | **[NOT OBSERVED — DO NOT INVENT]** |

**Evidence note:** A screenshot taken after expiry must redact the `sig` query parameter and any other sensitive credentials. Record UTC times so the comparison is clear.

## 6. If a recruiter needs six months of access

I would first confirm that six months is necessary and permitted by the organization's SAS expiration policy. If allowed, I would set an appropriately bounded expiry, ideally use a revocable access approach, and consider a more controlled sharing mechanism rather than a long-lived bearer URL. A six-month token increases the time during which a copied or leaked link can be misused; it also makes accidental sharing harder to contain. For a service SAS, a stored access policy can support revocation where applicable; a user delegation SAS has its own validity limits and cannot simply be issued for an arbitrary six-month period.

## 7. Why not share the storage account key?

A storage account key can enable much broader access to the storage account than a read-only SAS for one blob. If the key is leaked, someone may be able to generate additional SAS tokens or access and alter unrelated data, depending on configuration. A narrowly scoped, HTTPS-only, expiring SAS limits the recipient to the intended operation and resource, even if I trust the recipient.

## 8. Evidence and AI-use disclosure

**Evidence status:** This file is an educational simulation only. No real token was issued, no unauthenticated browser test was performed, no forbidden operation was attempted, and no expiry test was observed. It **does not meet the assignment's live-evidence grading requirements** without additional work and instructor approval.

**AI assistance:** ChatGPT produced the illustrative parameter table, expected-behavior explanations, test placeholders, and draft risk paragraphs. No actual Azure evidence or error codes were generated or claimed.

**Suggested Git commit message:**

`Add simulated SAS access documentation; ChatGPT drafted parameter examples and explanatory text, no live token tests performed`

**Credential safety:** Never commit a real SAS URL, `sig` value, account key, or unredacted screenshot.
