# Website security configuration

## Important hosting limitation
This portfolio is a static HTML website. It does not have a server-side plugin system, database, login area, or application backend. The `_headers` file is applied by Cloudflare Pages and some other static hosts, but **GitHub Pages does not apply custom response headers from `_headers`**. If you continue hosting on GitHub Pages, configure security headers at a reverse proxy/CDN such as Cloudflare (DNS proxy enabled) using Response Header Transform Rules or a Cloudflare Worker. Do not assume this file is active on GitHub Pages.

## Included in this package
- `_headers`: recommended HTTP security headers for hosts that support this format.
- `index.html`: conservative browser-side deterrents against image dragging, image context menus, and a few common save/source shortcuts. Normal text selection and copy remain enabled for accessibility.
- `SECURITY-LIMITATIONS.txt`: explains the limits of copy deterrents.

## Recommended deployment controls
1. Put the custom domain behind Cloudflare proxy; enable SSL/TLS **Full (strict)** and Always Use HTTPS.
2. Enable managed WAF rules and bot protection available on your Cloudflare plan. Add rate limiting only for actual dynamic endpoints; this site currently has none.
3. Enable registrar and GitHub account MFA/passkeys. Use a unique password and secure recovery codes.
4. In GitHub, protect the production branch, require review where practical, and limit repository write access.
5. Keep the repository free of API keys, passwords, private documents, customer data, and confidential files. Rotate any credential accidentally committed.
6. Keep local copies and repository history backed up; review dependency/security alerts if dependencies are introduced later.
7. Test headers after deployment with a security-header scanner and inspect browser developer tools for CSP violations before tightening policies.

## What cannot be guaranteed
No browser script or CSS can prevent a visitor from taking screenshots, using OCR, viewing page source, downloading public assets, or retrieving files from a public GitHub repository. These deterrents are not DRM and cannot stop hacking. Real protection comes from securing the GitHub account/repository, DNS/domain, hosting configuration, and any future backend. Never place secrets or sensitive information on a public static website.

## Protecting the CEO portrait and repository

The CEO portrait is stored as `ceo-profile.jpeg` and displayed in the homepage hero. Browser-level image deterrents are enabled, but they cannot prevent copying from a public website.

For stronger protection of the source content:
1. Keep the GitHub source repository **Private** and grant write access only to trusted maintainers.
2. Enable GitHub two-factor authentication or passkeys for every account with repository access.
3. Protect the deployment branch (`main`): require pull requests, restrict who can push, and disable force pushes/deletions where available.
4. Keep credentials, private documents, unpublished images, and API keys out of the repository.
5. If GitHub Pages publishing requires a public repository on your current plan, a private source repository with a separate controlled deployment workflow or a host supporting private source repositories is preferable.

A private repository protects the source repository from public browsing; it does not stop visitors from copying files that the public website itself serves. GitHub Pages and browser scripts cannot provide DRM or absolute anti-copy protection.
