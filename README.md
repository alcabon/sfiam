Salesforce offers a comprehensive Identity and Access Management (IAM) service known as Salesforce Customer Identity. This service is designed to enhance interactions with customers and partners by providing robust identity and access management capabilities. Key features of Salesforce Customer Identity include:

*   **User Identification and Access Management:** Salesforce Customer Identity helps manage user identities and access across various applications, improving engagement with customers and partners.
*   **Authentication and Security**: The service supports multiple authentication methods, including Multi-Factor Authentication (MFA), Single Sign-On (SSO), and various protocols such as SAML, OpenID, and OAuth.
*   **User Lifecycle Management**: Salesforce IAM includes user provisioning and de-provisioning, ensuring that access is granted appropriately as users join, move within, or leave the organization.
*   **Identity Governance**: It provides tools for managing access and authorization, ensuring that users have the appropriate level of access to resources.
*   **Audit and Compliance**: The service includes monitoring and reporting features to help with regulatory compliance and security audits.  
    These features make Salesforce Customer Identity a powerful tool for managing user identities and securing access to applications, both on-premises and in the cloud.

**Authentication Flows:**  
Authentication verifies the identity of a user or system.

*   Username-Password Authentication
*   Multi-Factor Authentication (MFA)
*   Single Sign-On (SSO)
*   SAML (Security Assertion Markup Language)
*   OpenID Connect

**Authorization Flows**_:_  
Authorization determines what resources an authenticated user or system can access.

*   **OAuth 2.0 Flows:**
     - Web Server Flow  
     - User-Agent Flow  
     - JWT Bearer Token Flow
     - Refresh Token Flow
     - Device Flow
     - SAML Assertion Flow
*   **Hybrid Flows**:
    - Hybrid Web Server Flow  
    - Hybrid User Agent Token Flow (formerly Hybrid App Token Flow)
*   **Server-to-Server Flows**

These flows can be used in various combinations depending on the specific use case and security requirements. For example, a user might authenticate using SSO with MFA, and then be authorized to access certain resources through an OAuth 2.0 flow.  
It's worth noting that Salesforce provides flexibility in implementing these flows, allowing organizations to choose the most appropriate methods for their security needs and user experience requirements.


**Web Server Flow:**
```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    User->>Client: 1. Initiate login
    Client->>AuthServer: 2. Authorization request
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>Client: 7. Authorization code
    Client->>AuthServer: 8. Token request with auth code
    AuthServer->>Client: 9. Access token & refresh token
    Client->>ResourceServer: 10. API request with access token
    ResourceServer->>Client: 11. Protected resource
```

**User-Agent Flow:**
```mermaid
sequenceDiagram
    participant User
    participant UserAgent as User Agent (Browser)
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    User->>UserAgent: 1. Initiate login
    UserAgent->>AuthServer: 2. Authorization request
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>UserAgent: 7. Access token in URL fragment
    UserAgent->>ResourceServer: 8. API request with access token
    ResourceServer->>UserAgent: 9. Protected resource
```

**JWT Bearer Token Flow:**
```mermaid
sequenceDiagram
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    Client->>Client: 1. Generate JWT
    Client->>AuthServer: 2. Token request with JWT
    AuthServer->>AuthServer: 3. Validate JWT
    AuthServer->>Client: 4. Access token
    Client->>ResourceServer: 5. API request with access token
    ResourceServer->>Client: 6. Protected resource
```

**Refresh Token Flow:**
```mermaid
sequenceDiagram
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    Client->>AuthServer: 1. Token request with refresh token
    AuthServer->>AuthServer: 2. Validate refresh token
    AuthServer->>Client: 3. New access token
    Client->>ResourceServer: 4. API request with new access token
    ResourceServer->>Client: 5. Protected resource
```

**Device Flow:**
```mermaid
sequenceDiagram
    participant Device
    participant User
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    Device->>AuthServer: 1. Request device code
    AuthServer->>Device: 2. Device code & user code
    Device->>User: 3. Display user code & URL
    User->>AuthServer: 4. Navigate to URL, enter user code
    AuthServer->>User: 5. Login prompt
    User->>AuthServer: 6. Provide credentials
    AuthServer->>User: 7. Consent screen
    User->>AuthServer: 8. Grant consent
    Device->>AuthServer: 9. Poll for access token
    AuthServer->>Device: 10. Access token
    Device->>ResourceServer: 11. API request with access token
    ResourceServer->>Device: 12. Protected resource
```

**SAML Assertion Flow:**
```mermaid
sequenceDiagram
    participant Client
    participant IdP as Identity Provider
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    Client->>IdP: 1. Request SAML assertion
    IdP->>Client: 2. SAML assertion
    Client->>AuthServer: 3. Token request with SAML assertion
    AuthServer->>AuthServer: 4. Validate SAML assertion
    AuthServer->>Client: 5. Access token
    Client->>ResourceServer: 6. API request with access token
    ResourceServer->>Client: 7. Protected resource
```
**Hybrid Web Server Flow:**
```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    User->>Client: 1. Initiate login
    Client->>AuthServer: 2. Authorization request
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>Client: 7. Authorization code & access token
    Client->>AuthServer: 8. Token request with auth code
    AuthServer->>Client: 9. Refresh token
    Client->>ResourceServer: 10. API request with access token
    ResourceServer->>Client: 11. Protected resource
```

**Hybrid User Agent Token Flow (formerly Hybrid App Token Flow):**
```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant ResourceServer as Salesforce Resource Server

    User->>Client: 1. Initiate login
    Client->>AuthServer: 2. Authorization request
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>Client: 7. Access token & ID token
    Client->>Client: 8. Store tokens securely
    Client->>ResourceServer: 9. API request with access token
    ResourceServer->>Client: 10. Protected resource
```

**Key points about these hybrid flows:**
- **Hybrid Web Server Flow:**
This flow combines elements of both the web server flow and the user-agent flow.
It provides direct management of web sessions for hybrid apps.
The authorization server grants both an authorization code and an access token in a single response.
The client can use the authorization code to obtain a refresh token, providing better long-term access management.
- **Hybrid User Agent Token Flow:**
This flow was formerly known as the Hybrid App Token Flow.
It's designed for hybrid apps that need direct management of web sessions.
The flow returns both an access token and an ID token.
It provides a higher level of security compared to the standard user-agent flow, as tokens are not exposed in the URL.
Both of these hybrid flows offer enhanced security and flexibility for applications that combine elements of web and native apps. They allow for better session management and can provide a smoother user experience while maintaining robust security measures


The **OAuth 2.0 implicit grant type** is used in the Implicit Flow. This flow is specifically designed for public clients, such as mobile applications or pure JavaScript front-end applications, where the access token is returned immediately without an extra authorization code exchange step.
Implicit Flow
- The Implicit Flow is characterized by the following steps:
- Initiate Login: The user initiates the login process.
- Authorization Request: The client application sends an authorization request to the authorization server.
- Login Prompt: The authorization server prompts the user to log in.
- User Provides Credentials: The user provides their credentials.
- Consent Screen: The authorization server displays a consent screen to the user.
- Grant Consent: The user grants consent.
- Access Token in URL Fragment: The authorization server redirects the user back to the client application with an access token in the URL fragment.
- API Request with Access Token: The client application uses the access token to make API requests to the resource server.
- Protected Resource: The resource server returns the protected resource to the client application.

```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Authorization Server
    participant ResourceServer as Resource Server

    User->>Client: 1. Initiate login
    Client->>AuthServer: 2. Authorization request
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>Client: 7. Access token in URL fragment
    Client->>ResourceServer: 8. API request with access token
    ResourceServer->>Client: 9. Protected resource
```

**Non-Implicit Type: Authorization Code Flow with PKCE**
The non-implicit type that is recommended as a replacement for the implicit grant type is the Authorization Code Flow with **PKCE (Proof Key for Code Exchange)**. This flow is more secure and is recommended for public clients, including single-page applications (SPAs) and native apps.
The Authorization Code Flow with PKCE involves the following steps:
* Initiate Login: The user initiates the login process.
* Authorization Request with Code Challenge: The client application sends an authorization request to the authorization server, including a code challenge.
* Login Prompt: The authorization server prompts the user to log in.
* User Provides Credentials: The user provides their credentials.
* Consent Screen: The authorization server displays a consent screen to the user.
* Grant Consent: The user grants consent.
* Authorization Code: The authorization server redirects the user back to the client application with an authorization code.
* Token Request with Code Verifier: The client application sends a token request to the authorization server, including the code verifier.
* Access Token & Refresh Token: The authorization server returns an access token and a refresh token to the client application.
* API Request with Access Token: The client application uses the access token to make API requests to the resource server.
* Protected Resource: The resource server returns the protected resource to the client application.

```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Authorization Server
    participant ResourceServer as Resource Server

    User->>Client: 1. Initiate login
    Client->>AuthServer: 2. Authorization request with code challenge
    AuthServer->>User: 3. Login prompt
    User->>AuthServer: 4. Provide credentials
    AuthServer->>User: 5. Consent screen
    User->>AuthServer: 6. Grant consent
    AuthServer->>Client: 7. Authorization code
    Client->>AuthServer: 8. Token request with code verifier
    AuthServer->>Client: 9. Access token & refresh token
    Client->>ResourceServer: 10. API request with access token
    ResourceServer->>Client: 11. Protected resource
```

In summary, the Implicit Flow is used for public clients where the access token is returned directly, but it is no longer recommended due to security concerns. The Authorization Code Flow with PKCE is the preferred alternative, providing enhanced security by including an additional step of exchanging an authorization code for tokens.


The traditional **User-Agent Flow** does not use PKCE. It typically uses the OAuth 2.0 implicit grant type, which has some security vulnerabilities .
Due to security issues with the User-Agent Flow, it is recommended to use the Authorization Code Flow with Proof Key for Code Exchange (PKCE) instead .
The transition from User-Agent Flow to Authorization Code Flow with PKCE is considered an enhancement in security, especially for mobile and desktop applications 
PKCE was introduced to address the security vulnerabilities in the implicit grant type used by the User-Agent Flow .
Starting with **Salesforce Mobile SDK 11.0**, the default authentication on both iOS and Android platforms uses the OAuth 2.0 Web Server Flow with PKCE for increased security, replacing the previous User-Agent Flow .
While it's possible to continue using the User-Agent Flow in newer versions of the Salesforce Mobile SDK, it's not recommended due to security concerns .
In summary, **the User-Agent Flow itself does not use PKCE**. Instead, the recommendation is to transition from the User-Agent Flow to the Authorization Code Flow with PKCE for improved security, especially in mobile and desktop applications. This transition represents a shift from the implicit grant type to a more secure authorization code grant type with the added protection of PKCE.
