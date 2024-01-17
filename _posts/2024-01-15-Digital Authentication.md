---
layout: post
title: "Advancing Beyond Passwords with Digital Authentication Systems"
subtitle: "Addressing Password Challenges, Exploring the Potential of Passwordless Authentication, and the Emerging Technologies Enabling Adoption"
background: '/img/posts/Sudo.jpg'
---

## Challenges with Passwords

*Weak, reused, and compromised passwords* were persistent challenges for both users and security personnel in 2016. Fast forward seven years, and little has changed; passwords remain a substantial security concern. Fortunately, numerous technologies that were emerging back then have now become mainstream, providing organizations with more choices and flexibility to eliminate passwords while still enhancing—not just maintaining—security and user experience in many cases.

Although passwords can safeguard a user's identity and personal data, achieving 100% security in today's digitally interconnected world is an unattainable goal when online. Regrettably, the requirement for customers, business associates, frontline employees, and executives to remember and input increasingly complex passwords hampers the user experience. Furthermore, in terms of security, **passwords persist as one of the weakest links.**

![IMDb page](/img/posts/BinaryHeart.jpg)

#### Biometrics

In 2016, a variety of contemporary authentication methods and technologies had surfaced, and many of them continue to be in use today:

**Multi-factor authentication (MFA)**

Commencing in the early 2000s, the adoption of two-factor authentication became widespread. In this scenario, users receive a one-time code on their mobile phones, which they enter in addition to the traditional password displayed on their laptop screens. This added layer of security stems from the authentication occurring across multiple channels.

**Biometrics implementation**

Around 2013, primarily driven by the popularity of the latest smartphone models, biometric authentication entered the mainstream. These technologies eliminate the need for memorizing complex combinations of letters, numbers, and symbols by leveraging distinct characteristics of the user—such as fingerprints, voice, face, heartbeat, and common movements. The most prevalent biometrics captured by smartphone cameras and voice recorders include fingerprint, heartbeat, voice, and face recognition. These approaches fall under the umbrella of "what you are". The preferred approach involves checking biometric data against a trusted device that the user owns, rather than a central repository. For instance, a user could scan their retina via the camera on a laptop or smartphone, utilizing biometric identification as the first step to access their online bank account. In a second step, the bank could then send a challenge via text message to the user's mobile phone, requiring them to reply with a text message to complete the authentication process.

#### Strategies for reducing risk

For organizations contemplating the transition away from passwords as their primary authentication method, various options are at their disposal. The most suitable choice for your organization hinges on your objectives and specific use cases. The following content offers a comprehensive overview.

**Account recovery features:**

- Support multiple methods for account recovery in case of primary authentication failure.
- Options include out-of-band one-time passwords, PINs, bypass codes, presenting a driver’s license via a camera, or user biometrics.
- Organizations should consider specific account recovery needs when selecting a passwordless option.

**Support for application programming interfaces (APIs):**

- Applications must support universal login or embed the API with the passwordless authentication login flow.
- Compatibility with cloud portals, Kerberos web single-sign-on (SSO) applications, etc., should be assessed.

**Devices support:**

- Passwordless authentication should be compatible with various device types, including tablets, mobiles, and computers.
- Organizations need to ensure compatibility with the devices in their environment.

**Change management:**

- Adoption involves using SaaS solutions and understanding identity protocols like OpenID connect and SAML.
- Effective change management and training plans are crucial for user acceptance.
- Crafting a streamlined enrollment process is important for a smooth rollout.

**Identity proofing:**

- For high-value transactions, compliance with NIST and FIDO2 specifications is necessary.
- Passwordless authentication achieves high-level identity assurance.
- Identity-proofing requirements should be considered when selecting a passwordless option.

**Fraud detection:**

- Transaction-based security and a robust fraud policy are essential for end-to-end fraud prevention.
- Organizations should consider fraud detection requirements in the selection of a passwordless option.

**FIDO2 and other open standards ability:**

- Web and SaaS applications are well-supported through identity federation and the Web authentication API.
- Relevant open standards should be considered in the choice of a passwordless option.

**Inconvenience of carrying physical devices:**

- Device-bound user certificates with keys stored in software or secure elements offer convenient passwordless authentication.
- Consider user experience when choosing a passwordless option.

**Co-existence strategy for faster adoption:**

- Speed of adoption depends on application providers supporting SSO, authentication plugins, or authentication proxies.
- Acquiring passwordless authentication platforms can facilitate integration and support additional authentication methods.

**Skillset and Experience:**

- Assess whether the organization has the required resources, subject matter knowledge, and skill set to support a transition to passwordless authentication.
- Consider external support needed for a successful implementation.