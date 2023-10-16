---
title: Change to yes to enable challenge-response passwords (beware issues with
tags: [Import-6cdc]
created: '2023-02-10T12:13:29.000Z'
modified: '2023-03-21T10:48:47.809Z'
---

> [!INFO] >
> Besteede tijd 15 minuten
> 

Gebruikte handleiding:
https://ubuntu.com/tutorials/configure-ssh-2fa#2-installing-and-configuring-required-packages


```

Oud:
# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
ChallengeResponseAuthentication no # CHANGE THIS TO YES

# Change to no to disable tunnelled clear text passwords
#PasswordAuthentication yes

nieuw:
# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
KbdInteractiveAuthentication yes

```

  ```

Nood codes

  97333849
  10560472
  60937990
  87562229
  27240741

```
