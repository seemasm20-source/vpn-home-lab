# 🔑 VPN Authentication Methods

## Username and Password

```text
Most basic authentication method - first factor

Entered in the VPN client login screen.

VPN server verifies the credentials,
often through Active Directory.

If the username and password are correct,
authentication succeeds.

Weakness:
If the password is compromised, an attacker
may be able to access the VPN unless additional
security such as MFA is enabled.
```







## 🔐 Certificate-Based Authentication

```text
Digital certificate is installed on the user's device
or stored on a smart card.

The certificate is used to prove the user's identity
and establish trust with the VPN server.

Commonly used in enterprise and high-security environments.

Advantage:
More secure than relying only on a username and password.
```




## 🔐 Multi-Factor Authentication (MFA)

```text
Second authentication factor required after the password.

MFA provides an additional layer of security even if
the user's password is compromised.

Common MFA methods:

→ Push notification
  Example: Microsoft Authenticator, Duo

→ OTP (One-Time Password)
  Temporary code that expires after a short period

→ SMS code
  Verification code sent to the user's phone
  Less secure than app-based MFA

→ Hardware security token
  Physical device used to generate or approve authentication
  Example: RSA SecurID
```







## 🔐 Single Sign-On (SSO)

```text
User is already authenticated with the company's identity system.

VPN uses the user's existing authentication session
or credentials to authenticate the VPN connection.

No separate VPN username/password may be required.

Provides a seamless login experience for users.

Common in enterprise environments and some
Always-On VPN solutions.
```





## 🔑 Authentication Summary

| **Authentication Method** | **Security Level** | **Common Issues** |
|---------------------------|--------------------|-------------------|
| **Username + Password** | Basic | Wrong or expired password, account locked |
| **Certificate** | High | Certificate expired, revoked or not trusted |
| **MFA Push** | High | Push notification not received, app issue |
| **MFA OTP** | High | Code expired, incorrect code, time synchronization issue |
| **SSO** | High | Authentication/token issue, domain or identity provider issue |
