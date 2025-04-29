# mastering-XSS-attacks

A TryHackMe room for mastering Cross-Site Scripting (XSS) vulnerabilities with hands-on tasks including Reflected, Stored, and DOM-Based XSS in a simulated blog environment.
Reflected XSS Challenge Write-Up

Introduction

Welcome to the Reflected XSS challenge in the "Mastering Cross-Site Scripting (XSS) Attacks" TryHackMe room! This practical challenge introduces you to Reflected Cross-Site Scripting (XSS), a common web vulnerability where attackers inject malicious scripts into a web page that are executed in a victim’s browser. Your task is to identify and exploit a Reflected XSS vulnerability in a simulated blog application’s search feature to capture a hidden flag, learning the risks and mechanics of XSS along the way. In this lab, the search feature fails to sanitize user input, allowing script injection directly into the HTML context.

Challenge Setup

The challenge provides a web page (search.html) with a search functionality that takes a q parameter from the URL (e.g., file:///path/to/search.html?q=books). The application reflects the user’s input directly into the page without proper sanitization, resulting in a Reflected XSS vulnerability. When a search query is submitted, the input appears in the HTML response, making it possible to inject and execute JavaScript code. Your goal is to exploit this vulnerability to retrieve the hidden flag, THM{XSS_REFLECTED}.
Objective

Locate the Reflected XSS vulnerability in the search feature.
Inject a JavaScript payload to trigger an alert box.
Use the vulnerability to extract the hidden flag, THM{XSS_REFLECTED}.

Step-by-Step Solution
Step 1: Inspect the Web Application

Access the search page provided in the TryHackMe room (e.g., via the link ReflectedXSS.ct.ws or a local search.html file).
Locate the search input field and test it with a harmless query, such as books.
Submit the form and observe the URL update to include the q parameter (e.g., file:///path/to/search.html?q=books).
Check the page’s response, which displays: You searched for: books. This indicates that the user input is reflected directly into the HTML without sanitization.

Step 2: Inject a Basic XSS Payload

Since the input is reflected without sanitization, test for a Reflected XSS vulnerability by injecting a simple JavaScript payload.
Manually modify the URL in your browser’s address bar to set the q parameter to: <script>alert('XSS')</script>. For example: file:///path/to/search.html?q=<script>alert('XSS')</script>.
Press Enter to load the page. If the vulnerability is present, a pop-up alert box will display XSS, confirming that the Reflected XSS vulnerability can be exploited.

Step 3: Capture the Flag

With the vulnerability confirmed, use a payload to extract the hidden flag. The flag is embedded in the page and revealed when a successful XSS payload is executed.
Modify the URL’s q parameter to include a payload that triggers the flag display, such as: <script>alert('THM{XSS_REFLECTED}')</script>. For example: file:///path/to/search.html?q=<script>alert('THM{XSS_REFLECTED}')</script>.
Load the page. The alert box will display THM{XSS_REFLECTED}, which is the hidden flag for this challenge.

Example Output
After injecting the payload <script>alert('THM{XSS_REFLECTED}')</script>, the alert box will show:
THM{XSS_REFLECTED}

Remediation

To prevent Reflected XSS vulnerabilities in real-world applications, implement the following strategies:

Input Validation: Sanitize user input by rejecting or escaping special characters like <, >, &, and ".
Output Encoding: Encode user input before rendering it in HTML, converting characters like < to &lt; to prevent script execution.
Content Security Policy (CSP): Use CSP headers to restrict script execution, e.g., Content-Security-Policy: script-src 'self';, to block inline scripts.
Secure Frameworks: Leverage frameworks like React or Angular, which automatically sanitize inputs and outputs to mitigate XSS risks.

Conclusion

This challenge demonstrates the dangers of Reflected XSS, where unsanitized user input in a search feature allows attackers to execute malicious scripts in a victim’s browser. By exploiting the vulnerability, you retrieved the flag THM{XSS_REFLECTED} and learned how attackers can use XSS for malicious purposes like cookie theft or phishing. Implementing robust input validation, output encoding, and security headers like CSP is critical to securing web applications against XSS attacks. Great job completing this challenge and advancing your web security skills!

References

OWASP XSS Prevention Cheat Sheet
Mozilla Developer Network (MDN) - Cross-Site Scripting (XSS)
TryHackMe - Mastering Cross-Site Scripting (XSS) Attacks

Try hack me room link: https://tryhackme.com/jr/masteringcrosssitescriptingV2
