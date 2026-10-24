# CIT 386 — Serving a Page (Documentation-Only Simulation)

> **Simulation disclosure:** The shared course server was unavailable. The commands below are a **proposed procedure**, not a transcript of commands executed. No service was installed, started, or verified for this submission. Paths, usernames, hostnames, and ports must be adapted to the instructor-assigned environment. Obtain instructor approval before using this as a substitute for the live lab.

## Environment and scope

- Example platform: isolated Ubuntu VM running Nginx (not the shared course server).
- Example document root: `/home/<your-user>/cit386-site`.
- Example port: `8080`, selected for an isolated practice instance; not an instructor-assigned port.
- **Do not install, start, stop, or reconfigure a global service on the shared server without explicit permission.**

## Planned command sequence (not executed)

These steps assume a private Ubuntu VM where you have administrative rights. They are **not** safe to apply verbatim to a shared host.

```bash
# 1. Identify the session and current directory
whoami
hostname
pwd

# 2. Refresh package metadata and install Nginx (private VM only)
sudo apt update
sudo apt install -y nginx

# 3. Record status BEFORE starting the service
sudo systemctl status nginx --no-pager

# 4. Start and recheck the service
sudo systemctl start nginx
sudo systemctl status nginx --no-pager

# 5. Prepare the page in your own directory
mkdir -p "$HOME/cit386-site"
cp module03/index.html "$HOME/cit386-site/index.html"
```

The example Nginx configuration below would require an **approved, isolated** site configuration. It is not installed by the commands above. Therefore the page would **not** yet be served at the proposed URL until an authorized configuration is created and enabled.

### Example Nginx site configuration (illustrative, not deployed)

```nginx
server {
    listen 8080;
    server_name localhost;
    root /home/<your-user>/cit386-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

For a real exercise, replace `<your-user>` with your actual username, obtain approval for the port and document root, and ensure Nginx can traverse and read the directory. On a private VM, validate and enable the configuration before testing. Do not assume the course server uses Nginx or this document root.

## Verification procedure (not executed)

After the approved site is configured and enabled, use:

```bash
sudo nginx -t
sudo systemctl reload nginx
curl -i http://127.0.0.1:8080/
```

Then open `http://<private-vm-address>:8080/` in a browser **if networking and firewall settings permit**. These are proposed checks, not successful test results.

## Actual observations

- Pre-start service status: **Not captured**.
- Post-start service status: **Not captured**.
- Browser result: **Not tested**.
- Instructor notification: **Not sent**.

## Page source

The full sample page source is committed as [`index.html`](index.html) in this directory. It identifies the student and course and explicitly labels the page as a simulation.

## AI assistance disclosure

ChatGPT assisted with drafting this simulation-only command plan, sample HTML, and documentation structure. No server observations were generated or interpreted by AI.
