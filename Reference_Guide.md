# Security Assessment Cheat Sheet

*Not exactly to be used as a check list, just a rough guide.*
	
*Character String= < ! # = / . “ - >*

## Passive:	
- [ ] Click through entire website. Get a feel for the cookies, URLs and areas that require authorization. 	
- [ ] Identify web server type.	
- [ ] Check robots.txt	
- [ ] Check comments in source of all pages	
- [ ] Identify all parameters. Document which parameters are used for GET and POST.	
- [ ] Identify where cookies are set, modified or added to.	
- [ ] Identify where redirects, 400 and 500 type responses are returned during normal operations.	
- [ ] Note any strange headers.	
- [ ] Use a spider and look for paths to important functions.	
- [ ] Fingerprint the Application Framework	
  * Look at x-powered-by: header, cookies, or source code, or ask the developer.	
  * Run whatweb	
  * dirb	
- [ ] Map application architecture
- [ ] Review logs from Splunk, access.log etc

## Active:	
- [ ] Append .old or .bak to files	
- [ ] Run Nikto	
- [ ] If possible, ask for file system access to view directories of web server	
  *	If not possible, run word lists against web server with things like .jsp, .aspx etc and then again with .bak, .txt, .old etc appended to the end of those	
- [ ] Check for directory listing (dirb should note this)	
- [ ] Test HTTP Options, use arbitrary method names to attempt to bypass authentication pages	
- [ ] Verify HSTS (HTTP Strict Transport Security)	
  *	Look for Strict-Transport-Security header	
- [ ] Check for crossdomain.xml and clientaccesspolicy.xml for overly permissive rules.	
- [ ] Request or build a user roles vs permissions matrix	
- [ ] Check user registration for alignment with business policies.	
  * Can users register for different roles?	
  * Can the same user register multiple times?	
  * Can user info be manipulated on creation?	
- [ ] Verify that only admins can provision accounts. 	
  * Test for indirect resources etc.	
- [ ] Check for messages upon failed logins, can an attacker enumerate usernames?	
- [ ] Possible enumerate by URI probing	
- [ ] Possible enumerate by forgot password function	
- [ ] Test for default credentials.	
- [ ] Check for account lock out mechanisms	
- [ ] Check site map with no authentication vs authenticated. See if any internal pages are reachable through forced browsing.	
  * Replay adduser requests etc as non-authenticated user and low priv user and verify whether or not the new user was created.	
  * Check for privilege escalation this way as well.	
- [ ] Check session cookie randomness.	
- [ ] If any pages have sensitive information, check for no-cache directive	
- [ ] Check password policy	
- [ ] Check reset password functionality.	
  * Make sure it requires previous password or information required is secret.	
- [ ] Test for directory traversal in URI parameters and in cookies	
  * Use Burp or dotdotpwn	
- [ ] Test for session fixation. Does cookie change upon login? What about logout?	
- [ ] Verify no session tokens are transmitted outside of the header	
- [ ] Verify tokens are sent via https when making an http request	
- [ ] Verify anti-CSRF functions are on sensitive pages.	
- [ ] Check for XSS	
  * Reflected	
  * Stored	
  * DOM	
- [ ] Submit multiple URL parameters with the same name and investigate output.	
- [ ] Make a list of all parameters that make use of SQL Queries and test for SQL injection	
- [ ] Test for LDAP Injection	
  * Look at Testing Guide for example	
- [ ] Test for XML Injection	
- [ ] Test for SSI Injection	
  * In headers: <!--#include virtual=”/etc/passwd” -->	
- [ ] Test for XPath Injection.	
- [ ] Test for IMAP/SMTP Injection. 	
- [ ] Test for code injection/command injection/LFI/RFI	
- [ ] Test upload for malicious files	
- [ ] Check URL redirects	
- [ ] Decompile .swf and other client side scripts.	

**O. W. A. S. P., “OWASP Testing Guide v4 Table of Contents,” OWASP Testing Guide v4. [Online]. Available: https://www.owasp.org/index.php/OWASP_Testing_Guide_v4_Table_of_Contents. [Accessed: 16-Jun-2017].**
