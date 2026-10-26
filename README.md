# Security Fundamentals Assessment

**Internship Task:** Task 1
**Submitted to:** SWYNEX Technologies
**Project:** Security Fundamentals Assessment
**Testing Environment:** Local OWASP Juice Shop Lab
**Tools Used:** Burp Suite Community Edition, Docker Desktop
**Operating System:** Windows

---

## 1. Introduction

Cybersecurity is important for protecting websites, user accounts, and personal information.

In this assessment, I tested the login security of OWASP Juice Shop in my own local lab environment. I used Burp Suite Community Edition to inspect login requests and observe server responses.

The main purpose of this assessment was to understand how a security weakness could allow unauthorized access to a user account.

## 2. Objectives

The objectives of this assessment were:

* To understand basic web application security.
* To inspect HTTP login requests using Burp Suite.
* To test a login request using a SQL Injection payload.
* To identify possible security risks.
* To document the results and recommend security improvements.

## 3. Testing Environment

I created a local testing environment using the following tools:

* **OWASP Juice Shop:** An intentionally vulnerable web application designed for security practice.
* **Docker Desktop:** Used to run the Juice Shop application locally.
* **Burp Suite Community Edition:** Used to inspect and modify HTTP requests.
* **Windows:** The operating system used for testing.

The application was accessed through `http://localhost:3000`.

All tests described in this report were performed in my own local lab environment.

## 4. Scope of Testing

The assessment focused on the login functionality of the OWASP Juice Shop application.

**Tested endpoint:** `POST /rest/user/login`

The testing was limited to my local lab. No external websites or real user accounts were tested.

## 5. Testing Methodology

I followed these steps during the assessment:

1. Started OWASP Juice Shop using Docker Desktop.
2. Opened the application in the Burp Suite browser.
3. Submitted invalid login details.
4. Used Burp Suite HTTP history to identify the login request.
5. Sent the login request to the Repeater tool.
6. Inspected the request body containing the email and password fields.
7. Tested the login request with a SQL Injection payload.
8. Observed the server response and recorded the result.
9. Captured screenshots as evidence.

**Test payload used:**

`' OR 1=1--`

This payload was tested only against the local OWASP Juice Shop application.

## 6. Security Finding

### Finding 1: Possible SQL Injection and Login Authentication Bypass

**Affected Component:** Login API
**Endpoint:** `POST /rest/user/login`

**Observed Result:**

When I sent the modified login request, the server returned:

`HTTP/1.1 200 OK`

The response also contained the email address:

`admin@juice-sh.op`

An authentication token was also returned in the response.

This result indicates that the modified login request was accepted and an authentication token associated with the admin account was returned, even though I did not provide the correct admin password.

This is evidence of a possible login authentication bypass consistent with SQL Injection. However, the underlying cause has not been independently confirmed by reviewing the application's query handling or authentication logic.

## 7. Evidence

### Evidence 1: Invalid Login Attempt

The first screenshot shows the login request in Burp Suite HTTP history and the server response.

The response returned `401 Unauthorized` when invalid login details were submitted.

**Screenshot 1:** Invalid login attempt using Burp Suite.

<!-- The screenshot will be displayed here after you upload it to the evidence folder. -->

### Evidence 2: Modified Login Request

The second screenshot shows the modified login request in Burp Suite Repeater and the server response.

The response returned `200 OK` and included the admin account email address.

**Screenshot 2:** Modified login request and authentication response.

<!-- The screenshot will be displayed here after you upload it to the evidence folder. -->

**Evidence safety:** Authentication tokens, cookies, session values, and other sensitive information must be hidden in screenshots before they are uploaded to a public repository.

## 8. Risk and Impact

If a similar weakness exists in a real application, an attacker may be able to bypass the login process without knowing the correct password.

Possible impacts include:

* Unauthorized access to user accounts.
* Unauthorized access to administrator functions.
* Exposure of information available to the accessed account.
* Loss of confidentiality and trust.

The actual impact depends on the application's permissions and the access available to the affected account.

**Provisional Risk Level: High — Requires Further Validation**

This provisional rating is based on the observed response associated with the admin account. The final risk rating should be confirmed after further validation of the vulnerability and its impact.

## 9. Recommended Mitigation

The following security improvements are recommended:

1. Use parameterized queries or prepared statements when interacting with the database.
2. Never build SQL queries by directly joining user input into query strings.
3. Validate and safely handle user input on the server.
4. Review the login authentication logic to ensure that a valid password is always required.
5. Apply proper access controls to administrator accounts.
6. Avoid exposing sensitive authentication information unnecessarily.
7. Test the login functionality regularly for security weaknesses.

These measures can help reduce the risk of SQL Injection and unauthorized account access.

## 10. Conclusion

In this assessment, I used Burp Suite Community Edition to test the login functionality of OWASP Juice Shop in a local lab.

I submitted invalid login details and observed the server response. I then tested a modified login request using a SQL Injection payload.

The modified request returned `200 OK` and an authentication token associated with the admin account. This result indicates a possible login authentication bypass and highlights the importance of secure database queries and authentication logic.

Through this task, I gained practical experience in inspecting HTTP requests, using Burp Suite Repeater, identifying potential security risks, collecting evidence, and recommending mitigation measures.

This assessment improved my understanding of web application security and the importance of conducting security testing in an authorized environment.
