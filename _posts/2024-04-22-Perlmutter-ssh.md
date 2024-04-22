---
title: Perlmutter ssh script
author: suranap
date: 2024-04-22 11:00:00
categories: [HPC]
tags: [tips]
---

Perlmutter offers a script called [sshproxy](https://docs.nersc.gov/connect/mfa/#sshproxy) to grab a 24-hr ssh certificate. This is great, but then you need to login with your OTP code. Instead, I use 1Password to store the password and OTP seed. Then I replaced the line `read -r -p "Enter the password+OTP for ${user}: " -s pw` with:

```
# Automatically grab password & OTP from 1Password
pw1=$(op item get 'Perlmutter' --fields label=password)
otp=$(op item get 'Perlmutter' --otp)
pw="$pw1$otp"
```

Now I can run the script and login with my fingerprint on a Mac. To make this better, you can setup your terminal to always try the script before ssh into Perlmutter. Then add a check for the `nersc` file timestamp. If it's less than 24 hours it's still valid, so abort the script. 
