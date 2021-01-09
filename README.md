# "Hallo Linux" - PAM-Demos

(c) 2019 Jürgen Schmidt aka ju

Changes (c) 2021 Marc Saric

All the details are in "Entspannt entsperrt, Linux-Authentifizierung mit mehr Komfort", c't 10/2019 Seite 132ff

Further ideas (globally enable U2F even with encrypted home dirs), see
https://askubuntu.com/questions/1071027/how-to-configure-a-u2f-keysuch-as-a-yubikey-for-system-wide-2-factor-authentic

These are PAM configuration files for demonstration purposes. They always allow authentication with your Linux system password as a last resort.

## Globally enable U2F for login

Extensions show changes to the sudo and common-auth files in ```/etc/pam.d```.

Make sure you know what you are doing, this can lock you out of your system permanently!

The U2F keyfile must reside outside of an encrypted home-directory, e.g. we could use ```/etc```.

```bash
pamu2fcfg -u$USER | sudo tee /etc/u2f_keys
```

The modified setup has been tested with Ubuntu Linux 18.04 LTS.

## General setup

Attention: For Authentication with face recognition, U2F token and PIN you have to install and configure the respective PAM libraries first. The details are explained in the articles.

```tsv
inc-pin+howdy-pw	PIN+Face / Password
inc-pin+u2f-pw		PIN+U2F-Token / Password
inc-u2f+howdy-pw	U2F+Face / Password
inc-u2f-pw		U2F-Token / Passwort
```

For demo installation purposes, copy these files to /etc/pam.d:

```bash
cd pam-demos/
sudo cp inc-* /etc/pam.d/
```

and replace for example in /etc/pam.d/sudo the line with "common-auth":

```diff
-@include common-auth

+@include inc-u2f-pw
+# @include common-auth
```

Afterwards, test with e.g. ```sudo -k id``` if things work (both U2F and normal password should work).

## Global initialization

If you are satisfied, you can transfer the changes to common-auth as shown in the example file in this repository. If you just want to enable U2F globally, just copy the contained common-auth to the /etc/pam.d/ directory.

Good luck.
