---
layout: post
title: "Unraveling the Threat Landscape"
subtitle: "A Deep Dive into Cross-Site Request Forgery (CSRF) Attacks"
background: '/img/posts/CSRF.jpg'
---

## Background

Cross-Site Request Forgery (CSRF) stands as a pervasive and evolving threat in the realm of web security. As cyber threats continue to evolve, understanding CSRF attacks becomes paramount for developers, security professionals, and web administrators. This topic delves into the intricacies of CSRF attacks, exploring their mechanisms, detection methods, and preventive measures. From real-world examples to cutting-edge defense strategies, the discussion aims to empower the audience with insights to fortify web applications against CSRF vulnerabilities.

## Exploiting Security: CSRF POST Request Attack


![IMDb page](/img/posts/Src.jpg)

Cross-Site Request Forgery (CSRF), often referred to as CSRF or XSRF, is a deceptive attack wherein a user is manipulated into executing actions on a different site unintentionally, either through clicking a link or submitting a form. The name "Cross-Site" is derived from the attack's origin on one site but its execution on another, while "Request Forgery" highlights the deceptive nature of the attack, as it is not a legitimate user request.

When a request is sent to a website, the browser includes all stored cookies for that site with the request. If these cookies contain information such as
```
 "logged_in=true"
 ```
  the target server may interpret the request as originating from a currently logged-in user. This exploit capitalizes on the inherent trust the server places in the user's browser.

  Typically utilized for state-changing requests, CSRF attacks prompt actions on behalf of the user, even though the attacker may not have visibility into the outcomes of the request, as it remains a request facilitated by the user's browser. Understanding and mitigating CSRF vulnerabilities are essential for safeguarding web applications against unauthorized actions initiated by malicious actors.

## Understanding the Dynamics of CSRF Attacks via GET Requests

  A basic CSRF attack involves deceiving a user into initiating a GET request to a particular URL. Achieving this can be as straightforward as embedding the URL within a link that carries a misleading name. This deceptive link might be strategically placed in various locations, such as a blog comment (a method commonly exploited in WordPress vulnerabilities), a post on an online forum, or even within a phishing email.

  ```java
  <img src="http://hackermag.com/best_hacker/vote/48576" />
  ```

  Upon loading a page, the browser autonomously generates separate requests to fetch all images embedded in the HTML. In the context of a user viewing a forum page containing the mentioned image within a user post, the browser initiates a GET request to the corresponding URL. Importantly, no user interaction is required, as the potential harm occurs during the browser's interpretation of the HTML, without the need for the user to click any links.

## CSRF GET Request with User Authentication

The primary risk of a CSRF attack emerges when the targeted URL directs to a page on a website requiring user authentication, and the user's browser maintains their prior authentication state. The exploit capitalizes on the authenticated state stored in the browser.

Consider a scenario where a user logs into their bank website. The bank sets a cookie in the user's browser, signifying authorized access. Subsequent requests to any page on the bank's site include this cookie as proof of authorization.

This process is akin to attending a concert, receiving a wristband upon payment or ticket presentation. The wristband serves as proof of authorized status: Wristband equals authorized; no wristband equals not authorized.

Now, envision the user concluding their banking activities, closing the browser window without logging out. The user's browser still retains the bank authorization cookie – it still wears the wristband.

If an attacker manages to manipulate the user into making a request to the bank's website, the request carries the cookie with authorization, and the server considers it authenticated. From the bank's perspective, this appears as just another routine request from the user's browser.

```java
<img src="https://bank.com/transfer?amount=10000&to_account=2468013579" />
```


Should a user load a page featuring the provided image tag, it initiates a ``GET`` request to the URL indicated in the ``src`` attribute. In this situation, an unauthenticated user would be directed to bank.com's login page. However, for a user who was authenticated previously, access might be granted if the request is acknowledged by ``bank.com``.


CSRF attacks can manifest in various actions, with some prevalent examples being:

- Altering the password
- Modifying the email address
- Logging into a site
- Initiating fund transfers
- Downloading malware

## Exploiting Security: CSRF POST Request Attack

``GET`` requests aren't the sole method for initiating a CSRF attack. An alternative approach involves an attacker fabricating a form. Breaking down the process step by step can provide clarity on the construction of such an attack.

Consider a scenario where an attacker conducts research to understand the appearance of a genuine bank.

```java
<html>
  <head>
    <title>Bank Website</title>
  </head>
  <body>
    <form action="http://bank.com/transfer" method="POST" name="bank_form">
      <input type="text" name="amount" value="" />
      <input type="text" name="to_account" value="" />
      <input type="submit" value="submit" />
    </form>
  </body>
</html>>
```
The attacker can embed that HTML into a different page and deceive a user into submitting the form. This method can bypass any "allow POST requests only" safeguards that may be implemented, as it involves a ``POST`` request. Similar to a ``GET`` request, this ``POST`` request transmits any authorization cookies.

To accomplish this, the attacker simply needs to discover a means of tricking a user into submitting the concealed form. This can be achieved by employing CSS to hide the form and then utilizing JavaScript to automatically submit the form upon page loading.
    
```java
<html>
  <head>
    <title>Fake Form</title>
  </head>
  <body onload="document.bank_form.submit()">
    <form action="http://bank.com/transfer" method="POST" name="bank_form" style="display: none;">
      <input type="text" name="amount" value="10000" />
      <input type="text" name="to_account" value="2468013579" />
    </form>
  </body>
</html>
```

Take note that the body incorporates an ``onload`` attribute, prompting an immediate form submission, while the form employs a ``style`` attribute to keep itself hidden.

This process doesn't necessitate the user to click "Submit"; in fact, there isn't even a submit button on the form. Persuading a user to visit this page is adequate to trigger the request, and accomplishing this can be as simple as embedding a deceptive link in a phishing email.

However, there is a potential issue with this attack. After the form submission, the user might witness the outcomes, like a page on the bank's website confirming a "Funds transfer complete." If a user observes this, they may grow suspicious and likely contact their bank to annul the transaction.

To counter this, an attacker must conceal the results. Forms facilitate the transmission of their outcomes to an ``iframe`` by utilizing a ``target`` attribute.

```java
<html>
  <head>
    <title>Fake Form</title>
  </head>
  <body onload="document.bank_form.submit()">
    <form action="http://bank.com/transfer" method="POST" name="bank_form" style="display: none;" target="hidden_results" >
      <input type="text" name="amount" value="10000" />
      <input type="text" name="to_account" value="2468013579" />
    </form>
    <iframe name="hidden_results" style="display: none;"></iframe>
  </body>
</html>
```

Observe the inclusion of the ``iframe`` tag, set to "``display: none``," and the addition of a new ``target`` attribute to the ``form`` tag.

By concealing an ``iframe`` and directing the form results to it, the user will remain unaware that a CSRF attack has transpired.