"Hallo Linux" - PAM-Demos
--------------------------
(c) 2019 Jürgen Schmidt aka ju

All the details are in "Entspannt entsperrt,
Linux-Authentifizierung mit mehr Komfort", 
c't 10/2019 Seite 132ff

This are PAM configuration files for demonstration
purposes. They always allow authentication with your
Linux system password as a last resort.

Attention: For Authentication with face recognition,
U2F token and PIN you have to install and configure the
respective PAM libraries first. The details are
explained in the articles.


inc-pin+howdy-pw	PIN+Face / Password
inc-pin+u2f-pw		PIN+U2F-Token / Password
inc-u2f+howdy-pw	U2F+Face / Password
inc-u2f-pw		U2F-Token / Passwort

For installation copy the files to /etc/pam.d:

cd pam-demos/
sudo cp inc-* /etc/pam.d/

and replace for example in /etc/pam.d/sudo the line with "common-auth":

-@include common-auth

+@include inc-u2f-pw
+# @include common-auth
