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
    *   Web Server Flow
    *   User-Agent Flow
    *   Client Credentials flow
    *   JWT Bearer Token Flow
    *   Refresh Token Flow
    *   Device Flow
    *   SAML Assertion Flow
*   **Hybrid Flows**:
    *   Hybrid Web Server Flow
    *   Hybrid User Agent Token Flow (formerly Hybrid App Token Flow)
*   **Server-to-Server Flows**

These flows can be used in various combinations depending on the specific use case and security requirements. For example, a user might authenticate using SSO with MFA, and then be authorized to access certain resources through an OAuth 2.0 flow.  
It's worth noting that Salesforce provides flexibility in implementing these flows, allowing organizations to choose the most appropriate methods for their security needs and user experience requirements.

**User-Agent Flow:**  Implicit grant type

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

**Web Server Flow:** : Authorization Code Flow

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

**Client Credentials flow:**

```mermaid
sequenceDiagram
    participant Client
    participant AuthServer as Authorization Server
    participant ResourceServer as Resource Server

    Client->>AuthServer: 1. Token Request (client_id, client_secret)
    AuthServer->>AuthServer: 2. Validate client credentials
    AuthServer->>Client: 3. Access Token
    Client->>ResourceServer: 4. API Request with Access Token
    ResourceServer->>ResourceServer: 5. Validate Access Token
    ResourceServer->>Client: 6. Protected Resource
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

*   **Hybrid Web Server Flow:**  
    This flow combines elements of both the web server flow and the user-agent flow.  
    It provides direct management of web sessions for hybrid apps.  
    The authorization server grants both an authorization code and an access token in a single response.  
    The client can use the authorization code to obtain a refresh token, providing better long-term access management.
*   **Hybrid User Agent Token Flow:**  
    This flow was formerly known as the Hybrid App Token Flow.  
    It's designed for hybrid apps that need direct management of web sessions.  
    The flow returns both an access token and an ID token.  
    It provides a higher level of security compared to the standard user-agent flow, as tokens are not exposed in the URL.  
    Both of these hybrid flows offer enhanced security and flexibility for applications that combine elements of web and native apps. They allow for better session management and can provide a smoother user experience while maintaining robust security measures

The **OAuth 2.0 implicit grant type** is used in the Implicit Flow. This flow is specifically designed for public clients, such as mobile applications or pure JavaScript front-end applications, where the access token is returned immediately without an extra authorization code exchange step.  
Implicit Flow

*   The Implicit Flow is characterized by the following steps:
*   Initiate Login: The user initiates the login process.
*   Authorization Request: The client application sends an authorization request to the authorization server.
*   Login Prompt: The authorization server prompts the user to log in.
*   User Provides Credentials: The user provides their credentials.
*   Consent Screen: The authorization server displays a consent screen to the user.
*   Grant Consent: The user grants consent.
*   Access Token in URL Fragment: The authorization server redirects the user back to the client application with an access token in the URL fragment.
*   API Request with Access Token: The client application uses the access token to make API requests to the resource server.
*   Protected Resource: The resource server returns the protected resource to the client application.

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

*   Initiate Login: The user initiates the login process.
*   Authorization Request with Code Challenge: The client application sends an authorization request to the authorization server, including a code challenge.
*   Login Prompt: The authorization server prompts the user to log in.
*   User Provides Credentials: The user provides their credentials.
*   Consent Screen: The authorization server displays a consent screen to the user.
*   Grant Consent: The user grants consent.
*   Authorization Code: The authorization server redirects the user back to the client application with an authorization code.
*   Token Request with Code Verifier: The client application sends a token request to the authorization server, including the code verifier.
*   Access Token & Refresh Token: The authorization server returns an access token and a refresh token to the client application.
*   API Request with Access Token: The client application uses the access token to make API requests to the resource server.
*   Protected Resource: The resource server returns the protected resource to the client application.

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

There are several technical reasons **why the Authorization Code flow is preferred over the Implicit flow:**

*   **Security of Access Token:**  
    In the Authorization Code flow, the access token is not exposed in the browser's URL or history, reducing the risk of token leakage .

**The Implicit flow passes the access token directly in the URL fragment, making it more vulnerable to interception.**

**Client Authentication:**

*   **The Authorization Code flow allows for client authentication using a client secret**, which is not possible with the Implicit flow .  
    This additional layer of security helps prevent unauthorized clients from obtaining access tokens.

**Refresh Tokens:**  
\- **The Authorization Code flow can return refresh tokens**, allowing for longer sessions and better user experience .  
The Implicit flow typically does not provide refresh tokens due to security concerns.  
Token Storage:

*   **In the Authorization Code flow**, tokens can be securely stored on the server-side, reducing the risk of client-side exposure .

**PKCE Support:**

You can optionally implement PKCE by including code_challenge and code_verifier parameters when you build variations of the authorization code flow with Salesforce. **These flows support PKCE.**

     -Web server flow
    - Hybrid web server flow
    - All variations of the Authorization Code and Credentials Flow, including headless registration, headless passwordless login, and headless guest flows.

*   PKCE helps mitigate authorization code interception attacks, which is particularly important for mobile and single-page applications.  
    Separation of Concerns:

**Compliance with Best Practices:**  
Current security best practices recommend using the Authorization Code flow with PKCE instead of the Implicit flow, especially for single-page applications and mobile apps .

*   **Reduced Token Exposure:**  
    In the Authorization Code flow, the access token is exchanged server-side, reducing exposure to potentially malicious client-side scripts .
*   **Better Support for Mobile and Desktop Apps:**  
    The Authorization Code flow with PKCE is better suited for mobile and desktop applications, where secure storage of client secrets may be challenging .  
    These technical reasons make the Authorization Code flow (especially when combined with PKCE) a more secure and flexible choice compared to the Implicit flow for most modern application scenarios.

**Overview of MFA, SSO, SAML, and OpenID**  
\- **Multi-Factor Authentication (MFA)**  
Multi-Factor Authentication (MFA) is a security mechanism that requires users to provide two or more verification factors to gain access to a resource such as an application, online account, or VPN. MFA combines two or more independent credentials: what the user knows (password), what the user has (security token), and what the user is (biometric verification).  
\- **Single Sign-On (SSO)**  
Single Sign-On (SSO) is an authentication process that allows a user to access multiple applications with one set of login credentials. This improves user experience by reducing the number of times a user has to log in and enhances security by centralizing authentication.  
\- **Security Assertion Markup Language (SAML)**  
SAML is an open standard for exchanging authentication and authorization data between parties, specifically between an identity provider (IdP) and a service provider (SP). SAML is primarily used for enterprise and government applications to provide SSO access to web applications. It uses XML for its identity data format and supports HTTP or SOAP for data transport mechanisms.  
\- **Key Points about SAML:**  
     - Mature Technology: Established in 2005, widely trusted.  
     - XML-Based: Uses XML for data interchange.  
    - Enterprise Use: Commonly used in enterprise and government settings.  
   -  SSO: Provides SSO capabilities.  
    -Federated Identity: Supports identity federation, allowing trust between different organizations' authentication systems.

*   \- **OpenID Connect (OIDC**)  
    OpenID Connect (OIDC) is an authentication protocol built on top of OAuth 2.0. It allows clients to verify the identity of the end-user based on the authentication performed by an authorization server, as well as to obtain basic profile information about the end-user in an interoperable and REST-like manner.  
    \- Key Points about OIDC:  
        - Modern Protocol: Developed in 2014, newer than SAML.  
        - JSON-Based: Uses JSON for data interchange.  
        - OAuth 2.0 Foundation: Extends OAuth 2.0 with an identity layer.  
       -  Mobile and Web Apps: Ideal for mobile and single-page applications.
*   **SSO: Provides SSO capabilities.**
*   Lightweight: Easier to implement compared to SAML, especially for developers.
*   Comparison: SAML vs. OpenID Connect (OIDC)
*   Similarities:
*   Both enable SSO.
*   Both are secure, well-documented, and mature.
*   Both involve an identity provider (IdP) and service provider (SP).
*   **Differences:**
*   Data Format: SAML uses XML, while OIDC uses JSON.
*   Implementation Complexity: OIDC is generally simpler to implement due to the absence of XML handling.
*   Use Cases: SAML is more feature-rich and suited for enterprise environments, while OIDC is more lightweight and suitable for mobile and web applications.
*   Decentralization: OIDC supports decentralized authentication, while SAML typically involves centralized identity management.
*   API Workloads: OIDC is designed to secure APIs, whereas SAML is more focused on web-based SSO.

**Use Cases**

*   **SAML:**  
    Enterprise and government applications.  
    Scenarios requiring extensive identity data exchange.  
    Environments where XML handling is not an issue.
*   **OIDC:**  
    Consumer applications, especially mobile and single-page web apps.  
    Scenarios requiring lightweight and easy-to-implement authentication.  
    Applications needing to secure APIs.
*   **Conclusion**  
    Both SAML and OpenID Connect (OIDC) serve crucial roles in identity and access management, providing SSO capabilities and enhancing security. The choice between them depends on specific use cases, technical requirements, and the environment in which they will be deployed. For enterprise-level, feature-rich identity management, SAML remains a strong choice. For modern, lightweight, and developer-friendly implementations, especially in mobile and web applications, OIDC is often preferred.
*   The Authorization Code flow separates the authentication and token issuance steps\*\*, allowing for better security practices and easier implementation of additional security measures .
*   The Authorization Code flow can be enhanced with Proof Key for Code Exchange (PKCE)\*\*, which adds an extra layer of security for public clients .


```mermaid
sequenceDiagram
    participant User
    participant Client
    participant AuthServer as Salesforce Auth Server
    participant MFAProvider as MFA Provider
    participant ResourceServer as Salesforce Resource Server

    Client->>Client: 1. Generate code verifier and code challenge
    User->>Client: 2. Initiate login
    Client->>AuthServer: 3. Authorization request with code challenge
    AuthServer->>User: 4. Login prompt
    User->>AuthServer: 5. Provide credentials
    AuthServer->>MFAProvider: 6. Trigger MFA
    MFAProvider->>User: 7. MFA challenge (e.g., SMS, Authenticator App)
    User->>MFAProvider: 8. Provide MFA response
    MFAProvider->>AuthServer: 9. Validate MFA response
    AuthServer->>Client: 10. Authorization code
    Client->>AuthServer: 11. Token request with authorization code and code verifier
    AuthServer->>AuthServer: 12. Verify code challenge and code verifier
    AuthServer->>Client: 13. Access token & refresh token
    Client->>ResourceServer: 14. API request with access token
    ResourceServer->>Client: 15. Protected resource
```

**Steps in the MFA Flow with PKCE:**
  - Generate PKCE Parameters: The client generates a code verifier and derives a code challenge from it.
  - Initiate Login: The user starts the login process.
  - Authorization Request with PKCE: The client sends an authorization request to the Salesforce Auth Server, including the code challenge. 
  - Login Prompt: The Auth Server prompts the user for credentials.
  - Provide Credentials: The user submits their primary credentials.
  - Trigger MFA: The Auth Server triggers an MFA challenge.
  - MFA Challenge: The MFA provider sends a challenge to the user.
  - Provide MFA Response: The user responds to the MFA challenge.
  - Validate MFA Response: The MFA provider validates the user's response.
  - Authorization Code: The Auth Server issues an authorization code to the client.
  - Token Request with PKCE: The client sends a token request, including the authorization code and the original code verifier.
  - Verify PKCE: The Auth Server verifies that the code challenge (from step 3) matches the provided code verifier.
  - Access Token & Refresh Token: The Auth Server issues tokens to the client.
  - API Request: The client uses the access token for API requests.
  - Protected Resource: The Resource Server returns the requested resource.
This updated flow incorporates PKCE, which provides additional protection against authorization code interception attacks. The code verifier, known only to the legitimate client, ensures that even if an attacker intercepts the authorization code, they cannot exchange it for tokens without knowing the code verifier.
Thank you for pointing out the missing PKCE component. This version of the diagram more accurately represents a secure OAuth 2.0 flow with MFA in Salesforce, especially for public clients.


**Salesforce Identity Connect** is a solution that integrates Microsoft Active Directory (AD) with Salesforce, allowing for seamless user authentication and synchronization between the two systems. Here are some key points about Identity Connect:

    1. Purpose: It bridges the gap between on-premises Active Directory and Salesforce's cloud-based identity management.
    2. User Synchronization: Identity Connect keeps user information in sync between Active Directory and Salesforce, ensuring that changes in AD are reflected in Salesforce.
    3. Single Sign-On (SSO): It enables SSO capabilities, allowing users to log in to Salesforce using their Active Directory credentials.
    4. Just-in-Time Provisioning: When a user authenticates for the first time, Identity Connect can automatically create or update the user's account in Salesforce.
    5. Password Synchronization: It can optionally synchronize passwords between AD and Salesforce, though this is generally not recommended for security reasons.
    6. Scheduled Synchronization: Administrators can set up scheduled sync jobs to ensure that user data remains up-to-date.
    7. Attribute Mapping: It allows for flexible mapping of AD attributes to Salesforce fields.
    8. Security: Identity Connect supports secure communication protocols and can be configured to work with firewalls and proxies.
    9. Licensing: It's a separately licensed product from Salesforce, not included in standard Salesforce licenses.
    10. Deployment: It's typically installed on-premises, close to the Active Directory servers for optimal performance.
    11. Identity Connect is particularly useful for organizations that want to maintain Active Directory as their primary source of truth for user identities while leveraging Salesforce's cloud capabilities. It simplifies user management and enhances security by reducing the number of separate credentials users need to maintain.



**SAML Sequence Diagrams for Service Provider (SP) Initiated and Identity Provider (IdP) Initiated Setups**
1. **Service Provider (SP) Initiated SSO**
In an SP-initiated SSO setup, the authentication process is initiated by the Service Provider (e.g., Salesforce). Here is the sequence diagram for this flow:
```mermaid
sequenceDiagram
    participant User
    participant SP as Service Provider (SP)
    participant IdP as Identity Provider (IdP)

    User->>SP: 1. Access protected resource
    SP->>IdP: 2. SAML Authentication Request
    IdP->>User: 3. Redirect to IdP login page
    User->>IdP: 4. Provide credentials
    IdP->>IdP: 5. Authenticate user
    IdP->>User: 6. Redirect to SP with SAML Response
    User->>SP: 7. Submit SAML Response
    SP->>SP: 8. Validate SAML Response
    SP->>User: 9. Grant access to protected resource
```

Steps:
- Access Protected Resource: The user attempts to access a protected resource on the Service Provider.
- SAML Authentication Request: The SP generates a SAML authentication request and redirects the user to the Identity Provider (IdP).
- Redirect to IdP Login Page: The IdP receives the request and redirects the user to its login page.
- Provide Credentials: The user provides their credentials to the IdP.
- Authenticate User: The IdP authenticates the user.
- Redirect to SP with SAML Response: Upon successful authentication, the IdP generates a SAML response and redirects the user back to the SP with this response.
- Submit SAML Response: The user submits the SAML response to the SP.
- Validate SAML Response: The SP validates the SAML response.
- Grant Access: If the validation is successful, the SP grants the user access to the protected resource.

**Note:** Setting up your current SAML SSO integration to work within Salesforce Mobile Applications may require changes to both your Identity Provider (IDP) and Salesforce Organization. **Salesforce Mobile Applications will only work with Service Provider Initiated setups.**  If you currently use IDP Initiated authentication, you need to change to Service Provider Initiated for mobile SSO Best Practice.

**2. Identity Provider (IdP) Initiated SSO**
In an IdP-initiated SSO setup, the authentication process is initiated by the Identity Provider. Here is the sequence diagram for this flow:

```mermaid
sequenceDiagram
    participant User
    participant IdP as Identity Provider (IdP)
    participant SP as Service Provider (SP)

    User->>IdP: 1. Access IdP login page
    IdP->>User: 2. Provide credentials
    User->>IdP: 3. Submit credentials
    IdP->>IdP: 4. Authenticate user
    IdP->>User: 5. Redirect to SP with SAML Response
    User->>SP: 6. Submit SAML Response
    SP->>SP: 7. Validate SAML Response
    SP->>User: 8. Grant access to protected resource
```

Steps:
- Access IdP Login Page: The user navigates directly to the IdP's login page.
- Provide Credentials: The IdP prompts the user to provide their credentials.
- Submit Credentials: The user submits their credentials to the IdP.
- Authenticate User: The IdP authenticates the user.
- Redirect to SP with SAML Response: Upon successful authentication, the IdP generates a SAML response and redirects the user to the SP with this response.
- Submit SAML Response: The user submits the SAML response to the SP.
- Validate SAML Response: The SP validates the SAML response.
- Grant Access: If the validation is successful, the SP grants the user access to the protected resource.
Summary
- Both SP-initiated and IdP-initiated SSO setups involve the exchange of SAML authentication requests and responses between the Service Provider and - the Identity Provider. The key difference lies in where the authentication process is initiated:
- SP-Initiated SSO: The process starts at the Service Provider, which redirects the user to the Identity Provider for authentication.
- IdP-Initiated SSO: The process starts at the Identity Provider, which authenticates the user and then redirects them to the Service Provider with a SAML response.
These sequence diagrams illustrate the typical steps involved in each flow, highlighting the interactions between the user, the Service Provider, and the Identity Provider.

|Flow|User Type|Grant Type|Type|Use Case|Application Type|
|----|---------|----------|----|--------|----------------|
|JWT Bearer Token Flow|Internal|JWT|Server-to-Server|Server-to-server communication|Server|
|Client Credentials Flow|Internal|Client Credentials|Server-to-Server|Server-to-server communication|Server|
|Web Server Flow|Internal/External|Authorization Code||Web and mobile applications with server-side components (with PKCE for mobile)|Desktop/Mobile|
|User-Agent Flow|Internal/External|Implicit||Single-page or client-side applications|Desktop/Mobile|
|Refresh Token Flow|Internal/External|Refresh||Long-lived sessions|Desktop/Mobile|
|Device Flow|Internal/External|Authorization Code (modified)||Devices with limited input capabilities|Desktop/IoT|
|SAML Assertion Flow|Internal/External|SAML||Federated identity scenarios|Desktop/Mobile|
|Headless Identity Flows|External|Authorization Code and Credentials Flow||Apps that complement a customer-facing Experience Cloud site Standalone apps. Users interact with and log in to your app, but not an Experience Cloud site.|Headless Login API|



**"headless" in the context of headless flows typically means:**
- **No User Interface**: Headless flows operate without a graphical user interface (GUI). They are designed to run in the background without direct user interaction .
- **Automation Without Screens:** In Salesforce, headless flows allow triggering of flows from workflows without the need for screens, essentially enabling declarative programming .
- **Backend Processing:** These flows are used for backend processes and integrations where visual interaction is not necessary or possible .    
- **API-Driven:** Headless flows are often controlled and executed through API calls rather than through a user interface .
- **Separation of Logic from Presentation:** In content management systems (CMS), headless flows allow for the separation of content management logic from the presentation layer 
- **Server-Side Execution:** Headless flows typically run on the server-side, making them suitable for automation tasks, background processes, and integrations with other systems .
- **Used by Non-UI Clients:** The headless flow executor is used by clients that don't have access to the web interface, such as LDAP and Radius outposts for user authentication .
**In essence, "headless" in this context refers to the ability to execute processes, workflows, or authentication flows without a user-facing interface, focusing on backend operations and integrations.**
