# web-security
# Project 7 - WordPress Pentesting

Time spent: 8-9 hours spent in total

> Objective: Find, analyze, recreate, and document at least three vulnerabilities affecting an old version of WordPress

## Pentesting Report

1. Large File Upload Error XSS (WordPress 3.3-4.7.4)

  - [ ] Summary: 
    - Vulnerability types: XSS 
    - Tested in version: 4.2
    - Fixed in version: 4.2.15
    
  - [ ] GIF Walkthrough:
  <img src="https://github.com/ksoliman/web-security/blob/master/GIFs/Large_File_Upload_Error_XSS.gif" width="800">
  
  - [ ] Steps to recreate: 
    - Create a ~20Mb file
      - In this walkthrough, a 17Mb picture was downloaded with a google search "20Mb picture"
    - Rename the file ``` *insert_any_string_here*<img src=x onerror=alert(1)>.png```
      - The ```alert(1)``` would be replaced with a malicious script in an actual attack
    - Logged in as the admin, navigate to "Dashboard" > "Media" > "Add New", then upload the target file
      - In an actual attack, the use of social engineering would be required to get an admin to upload the file injected with malicious code
    - After receiving the "exceeds the maximum upload size" error message, the script will run   
    
  - [ ] Affected source code:
    - [Link 1](https://hackerone.com/reports/203515)
    
2. DOM Cross-Site Scripting XSS (Twenty Fifteen Theme <= 1.1)
  - [ ] Summary: 
    - Vulnerability types: XSS 
    - Tested in version: 4.2
    - Fixed in version: Twenty Fifteen Theme 1.2
    
  - [ ] GIF Walkthrough:
  <img src="https://github.com/ksoliman/web-security/blob/master/GIFs/DOM_Cross_Site_Scripting%20.gif" width="800">
  
  - [ ] Steps to recreate:
    - As a contributor, create a post containing this link: 
    ```http://*WP_site*.com/wordpress/wp-content/themes/twentyfifteen/genericons/example.html#<img/src/onerror=alert(123)>```
      - In an actual attack, the use of social engineering would be required for an unsuspecting admin to click the link
    - As an admin, view the post and click the link containing the script
      - In an actual attack, ```alert(123)``` would be replaced with a malicious script
    - The alert (or malicious script) will appear 
  
  - [ ] Affected source code:
      - [Link 1](https://wpvulndb.com/vulnerabilities/7965)
    
3. User-Enumeration

  - [ ] Summary: 
    - Vulnerability types: User Enumeration
    - Tested in version: 4.2, Most Recent
    - Fixed in version: N/A
    
  - [ ] GIF Walkthrough:
  <img src="https://github.com/ksoliman/web-security/blob/master/GIFs/User_Enumeration.gif" width="800">
  
  - [ ] Steps to recreate:
    - On the log in page of the target site, enter a username that is likely non-existent
    - Enter any random characters in the password field
    - Examine the error message
      - The message should read ```ERROR: Invalid username.```
    - Clear the username and password field and enter a username that may exist on the target site
    - Enter any random characters in the password field
    - Examine the error message
      - The message should read ```ERROR: The password you entered for the username *entered_username* is incorrect.```
    - Now, with knowledge of the username, a hacker can brute-force his/her way to the correct password  
  
  - [ ] Affected source code:
    - Not Found

## Assets

- The 17Mb picture used in vulnerability 1 came from: https://www.flickr.com/photos/jimbo_in_jersey/8466462590

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Experienced challenges during the "DOM Cross-Site Scripting XSS" test, as the malicious link found on a site acquired from WPScan did not run the onerror script. The ```/wordpress``` had to be removed from the link in order for the script to run.

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
