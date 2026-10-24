# CIT 386 — Two Failures (Documentation-Only Simulation)

> **Simulation disclosure:** The instructor did not stage failures for this document, and no server logs were collected. The two cases below are **hypothetical troubleshooting exercises**, not diagnoses of real incidents. Under the course AI policy, the student must independently select and interpret any real log lines. Do not paste shared-server logs into AI tools.

## Hypothetical failure 1 — Page not found

**Scenario setup (hypothetical):** An otherwise reachable web server is configured to serve a document root, but the requested page is absent from that location.

**Symptom to record before diagnosis (not observed):**
- Browser: **Not observed**. In a real lab, record the exact page or HTTP error displayed.
- Service status: **Not observed**. Record the exact output before changing anything.

**Read-only investigation commands (run only on an authorized environment):**

```bash
sudo systemctl status nginx --no-pager
sudo journalctl -u nginx -n 30 --no-pager
# For an authorized Nginx instance, inspect its configured error log:
# sudo tail -n 30 /var/log/nginx/error.log
```

**One identifying log line (student-selected, exact quotation):** **Not available — no logs collected.**

**Resource named and reason (student's independent interpretation):** **Not completed — requires a real log line.**

**Possible corrective action to test, only after diagnosis:** Verify that the requested filename and the configured document root match. Restore or place the page in the authorized document root, if the evidence supports a missing-file cause.

**Confirmation:** **Not performed**. In a real test, repeat the browser request and record the actual result.

**What I would check first on an unfamiliar system:** I would verify the requested URL and the web server's configured document root before making changes.

## Hypothetical failure 2 — Configuration prevents service startup

**Scenario setup (hypothetical):** A syntax error is introduced into a private VM's Nginx site configuration, so the service cannot successfully apply that configuration.

**Symptom to record before diagnosis (not observed):**
- Browser: **Not observed**. Record exactly what the browser displays.
- Service status: **Not observed**. Record the exact output before fixing anything.

**Read-only investigation commands (run only on an authorized environment):**

```bash
sudo systemctl status nginx --no-pager
sudo nginx -t
sudo journalctl -u nginx -n 30 --no-pager
```

**One identifying log line (student-selected, exact quotation):** **Not available — no logs collected.**

**Resource named and reason (student's independent interpretation):** **Not completed — requires a real log line.**

**Possible corrective action to test, only after diagnosis:** Correct only the site configuration that you own, validate it with `nginx -t`, and reload or start the service only if you have authorization and doing so will not affect others.

**Confirmation:** **Not performed**. In a real test, capture the validation result, service status, and browser response.

**What I would check first on an unfamiliar system:** I would check service status and run a configuration syntax test before attempting a restart.

## AI assistance disclosure

ChatGPT helped organize these hypothetical scenarios and explain general troubleshooting and possible fixes. It did **not** select or interpret any real log lines; those graded diagnostic steps remain uncompleted.
