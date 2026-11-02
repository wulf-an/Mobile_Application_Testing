# Mobile Application Security Testing – Theory

## 1. Introduction to Mobile Application Security Testing

Mobile Application Security Testing is the process of identifying, analysing and validating security weaknesses in mobile applications to ensure the confidentiality, integrity and availability of application data and functionality.

Mobile applications interact with device resources, local storage, backend servers and external APIs. Improper implementation of security controls can expose sensitive information and allow unauthorized access.

Objectives of mobile application security testing:

* Identify vulnerabilities in application code and configuration.
* Examine how sensitive information is stored and transmitted.
* Evaluate authentication and authorization mechanisms.
* Identify insecure communication and data-handling practices.
* Assess application components and runtime behaviour.
* Recommend appropriate security improvements.

## 2. Android Application Structure

An Android application is generally distributed as an APK (Android Package Kit). An APK contains compiled code, resources, configuration files and other components required to install and execute the application.

| Component           | Description                                                                          |
| ------------------- | ------------------------------------------------------------------------------------ |
| AndroidManifest.xml | Contains application metadata, permissions and component declarations.               |
| classes.dex         | Contains compiled Dalvik bytecode executed by the Android Runtime (ART).             |
| res/                | Contains application resources such as layouts, images, strings and XML files.       |
| assets/             | Stores raw application files accessed through the AssetManager.                      |
| lib/                | Contains native libraries, generally compiled as .so files.                          |
| META-INF/           | Contains APK metadata and, depending on the signing scheme, signature-related files. |
| resources.arsc      | Contains the compiled resource table.                                                |

Major Android application components:

* Activities: Represent application screens and user interactions.
* Services: Perform operations that can continue without a user interface.
* Broadcast Receivers: Respond to broadcast messages from the system or applications.
* Content Providers: Manage and expose structured application data through a defined interface.

These components communicate through Android mechanisms such as Intents and Binder-based IPC.

## 3. OWASP Mobile Application Security Resources

OWASP provides security standards, testing methodologies and vulnerability references for mobile application security assessments.

### OWASP MASVS – Mobile Application Security Verification Standard

MASVS defines security requirements for mobile applications. It helps developers and security testers evaluate whether appropriate security controls are implemented.

Major verification areas include:

* Architecture, Design and Threat Modeling.
* Data Storage and Privacy.
* Cryptography.
* Authentication and Authorization.
* Network Communication.
* Platform Interaction.
* Code Quality.
* Resilience Against Reverse Engineering and Tampering.
* Privacy.

Reference: OWASP MASVS

### OWASP MASTG – Mobile Application Security Testing Guide

MASTG provides practical testing procedures, techniques and guidance for evaluating mobile application security.

It covers:

* Static analysis.
* Dynamic analysis.
* Data storage testing.
* Network communication testing.
* Authentication and authorization testing.
* Platform interaction testing.
* Reverse engineering and runtime instrumentation.

Reference: OWASP MASTG

### OWASP MASWE – Mobile Application Security Weakness Enumeration

MASWE is a catalogue of common mobile application security weaknesses. It provides descriptions of weaknesses and helps security professionals understand and classify security issues identified during testing.

Reference: OWASP MASWE

### OWASP Mobile Top 10

The OWASP Mobile Top 10 highlights significant mobile application security risk categories and provides awareness of common security problems.

The 2024 edition includes:

1. M1 – Improper Credential Usage
2. M2 – Inadequate Supply Chain Security
3. M3 – Insecure Authentication/Authorization
4. M4 – Insufficient Input/Output Validation
5. M5 – Insecure Communication
6. M6 – Inadequate Privacy Controls
7. M7 – Insufficient Binary Protections
8. M8 – Security Misconfiguration
9. M9 – Insecure Data Storage
10. M10 – Insufficient Cryptography

Reference: OWASP Mobile Top 10

## 4. Types of Mobile Application Security Testing

Mobile application security assessments commonly use two complementary approaches.

### Static Analysis

Static analysis examines an application's files, configuration and code without executing the application.

Main objective: Identify security weaknesses within the application's structure, source code and configuration.

Examples:

* Hardcoded credentials.
* Insecure cryptographic implementations.
* Excessive permissions.
* Insecure application configurations.
* Sensitive information in application resources.
* Insecure coding practices.

### Dynamic Analysis

Dynamic analysis examines an application while it is executing in a controlled testing environment.

Main objective: Identify security weaknesses through observing and interacting with the application's runtime behaviour.

Examples:

* Sensitive information exposed during execution.
* Insecure local data storage.
* Weak authentication and session management.
* Insecure network communication.
* Improper component exposure.
* Runtime security-control weaknesses.

Both approaches complement each other. Static analysis identifies potential weaknesses in implementation, while dynamic analysis helps validate how the application behaves during execution.

## 5. Static Analysis – Methodology and Tools

Static analysis involves examining the internal structure, configuration and reconstructed code of an Android application without executing it.

### Static analysis methodology

1. Application Acquisition: Obtain the APK from an authorized source and calculate its cryptographic hash.
2. APK Extraction: Decode the APK and extract its resources and configuration files.
3. Metadata Analysis: Examine package information, version, SDK requirements and permissions.
4. Manifest Analysis: Investigate application components and security configurations.
5. Code Analysis: Examine reconstructed code to understand application logic and security implementations.
6. Resource Analysis: Investigate embedded resources, assets and native libraries.
7. Weakness Identification: Identify potential security weaknesses and validate findings where possible.
8. Documentation: Record observations, evidence and recommendations.

### Static analysis tools

| Tool            | Purpose                                                |
| --------------- | ------------------------------------------------------ |
| JADX / JADX-GUI | Reconstruct DEX bytecode into readable Java-like code. |
| APKTool         | Decode APK resources, manifest and Smali code.         |
| AAPT            | Extract APK metadata and package information.          |
| MobSF           | Automate static mobile application security analysis.  |
| APKSigner       | Examine APK signing information and verify signatures. |

### Areas of investigation

#### 1. Reconstructed code analysis

Examines Java-like code reconstructed from DEX bytecode to understand application functionality and identify insecure implementations.

#### 2. AndroidManifest.xml analysis

Investigates:

* Application permissions.
* Exported activities, services and receivers.
* Content provider configuration.
* Debugging configuration.
* Backup settings.
* Intent filters and deep-link declarations.

#### 3. Hardcoded credentials and sensitive information

Examines application code and resources for:

* API keys.
* Passwords.
* Authentication tokens.
* Cryptographic keys.
* Backend URLs.
* Sensitive configuration values.

#### 4. Application logic analysis

Examines authentication mechanisms, authorization checks, input validation, cryptographic operations and sensitive data handling.

#### 5. Resource and asset analysis

Investigates the res/ and assets/ directories for sensitive configuration values, embedded files, certificates, databases and other potentially exposed information.

#### 6. Native library analysis

Examines .so files within the lib/ directory to identify potentially insecure native code implementations and embedded sensitive information.

## 6. Dynamic Analysis – Methodology and Tools

Dynamic analysis involves executing an Android application in a controlled environment to observe its behaviour, interactions and security controls during runtime.

### Dynamic analysis methodology

1. Environment Setup: Configure an Android emulator or testing device.
2. Application Installation: Install the APK and verify that it functions correctly.
3. Runtime Observation: Monitor application behaviour and interactions.
4. Application Interaction: Explore different functionalities, workflows and input scenarios.
5. Runtime Instrumentation: Use instrumentation tools to inspect methods, classes and application behaviour.
6. Network Monitoring: Capture and analyse application network communication.
7. Storage Investigation: Examine local application data and sensitive information.
8. Security Validation: Test suspected weaknesses and assess their potential impact.
9. Evidence Collection: Document the results and prepare security findings.

### Dynamic analysis tools

| Tool       | Purpose                                                               |
| ---------- | --------------------------------------------------------------------- |
| Genymotion | Provides an Android virtual testing environment.                      |
| ADB        | Interacts with Android devices and application processes.             |
| Frida      | Provides dynamic instrumentation and runtime method interaction.      |
| Objection  | Supports runtime exploration and mobile application security testing. |
| Burp Suite | Intercepts and analyses application network traffic.                  |
| Logcat     | Monitors Android system and application logs.                         |
| mitmproxy  | Intercepts and analyses HTTP/HTTPS communication.                     |

## 7. Dynamic Analysis – Areas of Investigation

### 7.1 Deep Link Testing

Deep links allow external URLs to open specific application screens or functionality.

Security testing examines:

* Improper URL validation.
* Unauthorized access through deep links.
* Exposure of sensitive information.
* Improper handling of user-supplied parameters.
* Authentication and authorization enforcement.

### 7.2 Intent Testing

Intents facilitate communication between Android application components and other applications.

Security testing examines:

* Improperly exposed components.
* Unvalidated Intent data.
* Unauthorized component invocation.
* Sensitive information passed through Intent extras.
* Improper use of implicit and explicit Intents.

### 7.3 WebView Security Testing

WebView allows applications to display web content within their interfaces.

Security testing examines:

* JavaScript execution settings.
* JavaScript interfaces.
* URL validation.
* Insecure file access configurations.
* Untrusted content loading.
* Improper SSL error handling.

### 7.4 Application Component Analysis

Android applications use Activities, Services, Broadcast Receivers and Content Providers to implement functionality.

Testing evaluates whether these components have appropriate permissions, access controls and input validation.

### 7.5 Runtime Code Logic Analysis

Examines application behaviour during execution to identify weaknesses in authentication, authorization, input validation, business logic and security-control implementation.

## 8. Network Traffic Analysis

Network traffic analysis examines communication between a mobile application and its backend servers or external services.

The objective is to identify sensitive information exposure, insecure communication and weaknesses in request and response handling.

Areas of investigation:

* HTTP and HTTPS communication.
* Request and response parameters.
* Authentication headers and cookies.
* Session tokens.
* Sensitive information transmitted over the network.
* Improper TLS configuration.
* Unexpected or insecure API communication.

Tools: Burp Suite, mitmproxy and Wireshark.

## 9. API Security Testing

API security testing evaluates the security of endpoints accessed by mobile applications.

Areas of investigation:

* API authentication.
* Authorization and access control.
* Input validation.
* Improper exposure of sensitive information.
* Insecure direct object references (IDOR).
* Excessive data exposure.
* Rate limiting and abuse prevention.
* Server-side business logic.

The objective is to ensure that backend APIs properly validate requests and enforce security controls independently of the mobile application.

## 10. SSL/TLS Certificate Analysis

SSL/TLS certificate analysis evaluates how an application establishes secure network communication with backend services.

Areas of investigation:

* Certificate validity and expiration.
* Certificate issuer and trust chain.
* Hostname verification.
* TLS protocol versions.
* Certificate validation.
* Secure cipher configuration.
* Improper handling of certificate errors.

The objective is to verify that the application establishes trusted and encrypted communication with its intended servers.

## 11. Certificate Pinning Analysis and Bypass

Certificate pinning is a security mechanism that restricts an application's trust to specific certificates or public keys associated with the intended server.

It provides an additional layer of protection against certain man-in-the-middle attacks.

Security testing includes:

* Identifying whether certificate pinning is implemented.
* Examining the certificate or public-key validation mechanism.
* Observing application behaviour when an untrusted certificate is presented.
* Testing the effectiveness of pinning controls.
* Performing authorized runtime bypass experiments to understand the implementation.

Tools: Frida, Objection and Burp Suite.

## 12. Android Local Storage Analysis

Android applications use different storage mechanisms to save application data locally.

Security testing examines whether sensitive information is stored and protected appropriately.

| Storage mechanism | Purpose                                                                  |
| ----------------- | ------------------------------------------------------------------------ |
| SharedPreferences | Stores key-value configuration and application preferences.              |
| SQLite            | Stores structured relational data.                                       |
| Internal Storage  | Stores private application files.                                        |
| External Storage  | Stores files in shared or external storage locations.                    |
| Cache             | Stores temporary application data.                                       |
| Android Keystore  | Provides facilities for secure cryptographic key storage and management. |

Areas of investigation:

* Plaintext credentials.
* Authentication and session tokens.
* Sensitive user information.
* Insecure database storage.
* Unprotected application files.
* Improper handling of temporary data.

## 13. Session Management Testing

Session management maintains an authenticated user's state across application interactions.

Security testing examines:

* Session token generation.
* Secure token storage.
* Session expiration.
* Token renewal.
* Logout functionality.
* Session invalidation.
* Session fixation and hijacking risks.
* Concurrent session handling.

The objective is to ensure that authenticated sessions are appropriately protected and invalidated when required.

## 14. Authentication and Authorization Testing

Authentication testing evaluates how an application verifies the identity of its users.

Areas of investigation:

* Login mechanisms.
* Password handling.
* Multi-factor authentication.
* Account recovery.
* Authentication bypass.
* Session establishment.

Authorization testing evaluates whether authenticated users can access only the resources and functionality they are permitted to access.

Areas of investigation:

* Horizontal privilege escalation.
* Vertical privilege escalation.
* IDOR vulnerabilities.
* Role-based access control.
* Unauthorized API access.
* Improper access to application components.

Authentication determines who the user is, while authorization determines what the user is allowed to access.

## 15. Application Component Security Testing

This testing evaluates whether Android application components are securely configured and protected.

| Component           | Security testing focus                        |
| ------------------- | --------------------------------------------- |
| Activities          | Exported access and unauthorized invocation.  |
| Services            | Access restrictions and improper exposure.    |
| Broadcast Receivers | Unauthorized broadcasts and input validation. |
| Content Providers   | Data exposure and permission enforcement.     |
| Intents             | Untrusted data and component communication.   |
| Deep Links          | URL validation and access control.            |
| WebView             | JavaScript interfaces and content handling.   |

The objective is to prevent unauthorized applications or users from accessing sensitive functionality or information through improperly configured components.

## 16. Vulnerability Assessment and Reporting

After completing static and dynamic testing, identified weaknesses should be validated and documented in a structured security report.

A professional security finding should contain:

1. Vulnerability title.
2. Severity and risk rating.
3. Affected application component.
4. Vulnerability description.
5. Steps to reproduce.
6. Proof of concept and evidence.
7. Potential security impact.
8. Remediation recommendations.

Findings should be classified based on their actual impact and validated evidence rather than assumptions.

## 17. Conclusion

Mobile application security testing requires a combination of static and dynamic analysis to evaluate application code, configuration, runtime behaviour, data storage and communication mechanisms.

By following established security standards such as OWASP MASVS and practical testing procedures from OWASP MASTG, security testers can systematically identify weaknesses, validate their impact and provide recommendations to improve mobile application security.

### Official references

* OWASP MASVS
* OWASP MASTG
* OWASP MASWE
* OWASP Mobile Top 10
* Android Security Documentation
