
# 🔑 VPN Authentication Methods

Authentication is how the VPN server confirms who is connecting. The method decides how secure the VPN is, and it also decides what a technician checks when a user cannot connect.

---

## 🔐 Authentication Factors

A factor is a type of proof. Stronger sign-ins combine more than one factor.

| Factor | Meaning | Examples |
|--------|---------|----------|
| **Something you know** | A secret in the user's head | Password, PIN |
| **Something you have** | A device or item the user owns | Phone, hardware token, certificate on a laptop or smart card |
| **Something you are** | A physical trait | Fingerprint, face recognition |

---

## 1. Username and Password

The most basic method, and the first factor. The user enters the credentials in the VPN client login screen. The VPN server checks them, often through an authentication server such as Active Directory, NPS or a RADIUS server. If they are correct, authentication succeeds.

| | Detail |
|---|--------|
| **Factor** | Something you know |
| **Security level** | Basic |
| **Weakness** | If the password is stolen or guessed, an attacker can use the VPN, unless MFA or another control is also required |

---

## 2. Certificate-Based Authentication

A digital certificate is installed on the user's device or stored on a smart card. The certificate proves the user's or device's identity and builds trust with the VPN server. It is common in enterprise and high-security environments.

| | Detail |
|---|--------|
| **Factor** | Something you have |
| **Security level** | High |
| **Advantage** | More secure than a password alone, because the certificate cannot be guessed |
| **Weakness** | Certificates expire, can be revoked and must be issued and renewed. A stolen device with a certificate and no other control is a risk |

> Certificates are often combined with a password or MFA, so the connection needs more than one factor.

---

## 3. Multi-Factor Authentication (MFA)

MFA asks for a **second factor** after the password. Even if the password is compromised, an attacker cannot sign in without the second factor.

| MFA method | How it works | Notes |
|------------|--------------|-------|
| **Push notification** | The user approves the sign-in in an app | Examples: Microsoft Authenticator, Duo. Use number matching if available, because users can approve a prompt by mistake |
| **One-time password (OTP)** | A temporary code that expires after a short period | The code comes from an authenticator app or a token |
| **SMS code** | A verification code is sent to the user's phone | Less secure than app-based MFA, because phone numbers can be hijacked |
| **Hardware security token** | A physical device that generates or approves sign-ins | Examples: RSA SecurID, FIDO2 security keys |

| | Detail |
|---|--------|
| **Factors** | Something you know, plus something you have |
| **Security level** | High, and lower for SMS |

---

## 4. Single Sign-On (SSO)

The user is already signed in to the company's identity system. The VPN uses that existing session, so no separate VPN username and password may be needed. It gives a smooth sign-in and is common in enterprise environments and some Always On VPN setups.

| | Detail |
|---|--------|
| **Security level** | Depends on the identity provider and on whether it enforces MFA |
| **Weakness** | If the central account is compromised, every connected service is exposed, so protect it with MFA |

> SSO is about **convenience**, not an extra factor. It reuses a sign-in that already happened.

---

## 5. Pre-Shared Key (PSK)

A secret value that both the VPN client and the server know. It is used to set up an IPsec tunnel, mainly with L2TP/IPsec and some site-to-site VPNs. It does **not** identify the user, so it is normally combined with a username and password.

| | Detail |
|---|--------|
| **Weakness** | The same key is shared by everyone who uses it. If it leaks, change it on the server and on every client |
| **Common issue** | The key on the client and on the server do not match |

---

## 🔑 Authentication Summary

| Method | Security level | Common issues | What to check |
|--------|----------------|---------------|---------------|
| **Username + password** | Basic | Wrong or expired password, account locked or disabled | The account in ADUC. Unlock or reset it |
| **Certificate** | High | Certificate expired, revoked, missing or not trusted | The certificate store on the device and its expiry date |
| **MFA push** | High | Notification not received, app problem, approval timed out | The phone's internet connection and notifications, and the MFA enrolment |
| **MFA OTP** | High | Code expired or wrong, time out of sync | The device time and time zone, then a new code |
| **MFA SMS** | Medium | Message delayed or not received | The phone number on the account and the signal |
| **Hardware token** | High | Token lost, battery empty, token not registered | Re-register or replace the token |
| **SSO** | Depends on the identity provider | Token or session problem, identity provider outage | Sign out and in again, and check the identity provider status |
| **Pre-shared key** | Medium | Key mismatch between client and server | The key on both sides |

---

## 🛠️ Tip for Troubleshooting

When a user says "VPN authentication failed", find out which method is in use first, then:

1. Check that the **account** works: it is enabled, not locked out and the password has not expired. See [Unlock a User Account](./unlock-user-account.md) and [Event ID 4740](./event-id-4740.md).
2. Check the **second factor**: the phone, the app and the device time.
3. Check the **certificate or key**, if one is used.
4. Check the **authentication server logs**. On a Windows NPS server, Event ID **6272** means access was granted and **6273** means access was denied, with a reason code.

---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)



































