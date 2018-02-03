~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Signing your Code and Documents:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This guide is about Signing Code snippets and Documents like emails and the like.

~~~~~~~~~~~~~~~~~~~~~~~~~
Rationale for this guide:
~~~~~~~~~~~~~~~~~~~~~~~~~

You write code and need to prove that it is created by your (and or your team) and that it has not been altered in any unauthorized manner, since it was created and/or hosted wherever you/your team or any mirror/partner site(s).

So how are you able to do this?, Long gone are the days where one could just assert a Gentleman's/Gentlewoman's Honor that your code was what you claimed it was.  Now there is a realm where things can be hosted on any number of sites and/or by any number of folks, whom may or may not be willing to pass along things as provided to them.  

This guide details how to sign individual files and commits and repositories/release binaries using GNUPG version2 (gpg2).

~~~~~~~~~~~~~~~~
What is needed?:
~~~~~~~~~~~~~~~~

## Minimal ##

*	Your code or Document
*	GNUPG version 1 or 2 (this guide assumes version 2, if you are using version 1 please read up on the differences that apply)
*	At least 1 (one) GPG Keypair

## Optional, but recommended ##

*	Configuration file for handling repository and binary signing 
*	A `gpg.conf` file for handling key(s) used to sign
*	At least one additional key for 'cross-signing' (more on this later in the guide)
 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Assumptions and conventions:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*	gpg.conf.sample uses the following options which are generally deemed common and useful, yet for has some insecure or excessively verbose options, namely among them:
	- 	use-agent 
	Which allows for use of gpg-agent which allows for enter once and reuse the --cached passphrase for subsquent requests during the after agent session, this however on a public machine is HIGHLY DISCOURAGED, as it allows for the possibility of a logged in user with an unattended session, allowing for a compromise of the session. This IS ONLY RECOMMENDED on a personal and securely managed machine/laptop.

	-	list-options | --verify-options 
		--show-uid-validity
		--show-photos
	Both options can be excessively noisy/verbose as it can show photos of all keys you have (for others AND any photo attached to your key(s))
	This can serve as a great way to validate you have the key you believe you have, but the verbosity can be excessive and should be used only as needed.

It is assumed that you have created at least one keypair for use with signing your code or documents. If you have no present keypair or wish to learn/read about best practices for creating such a keypair for this or other operations feel free to read any of these guides:

	*	Riseup.net: Create a Secure GPG Keypair
	*	gnupg.net: Best Practices for creating/using a GPG Keypair

## TODO:Add links and additional layperson friendly guides on keypair generation.


~~~~~~~~~~~~~~~~~
Basic Setup Info:
~~~~~~~~~~~~~~~~~

* Read the .readme files in conf-files/ for the respective files, especially if you have never seen or utilized such configuration files.

* Move the files into ~/.gnupg/gpg.conf and ~/$repo/.git/config respectively.

* If needed create a GPG keypair (or for more advanced tasks several keypairs for cross-signing)

* Decide which repo of tasks suits your needs/skill-level.  These sub-repos are setup in such a way that you can fork/clone them separately for your own use-cases.

~~~~~~~~~
Beginner:
~~~~~~~~~

-	Signing code commits
-	Creating and signing tarballs/zip files
-	Clear-signing documents like resumes and Letters of Reference

~~~~~~~~~~~~~
Intermediate:
~~~~~~~~~~~~~

-	Creating basic configurations that allow for pulling in signed setup files
-	Pulling in signed / validated files/configs into a bare system
-	Integrating 2FA (non-hardware) tokens into signing/validation process

~~~~~~~~~~~~~~~~
Advanced/Expert:
~~~~~~~~~~~~~~~~

-	Cross-signing Keys
-	Using 2FA (hardware) tokens to make for more secure management of Signing/Encrypting Keys


