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

************
* gpg.conf *
************

* Take the gpg.conf.sample and copy it to your $GNUPG_HOME (usually this is `C:\Users\UserName\gnupg` (Windows) OR `/home/username/.gnupg/` (MacOS/Linux)) directory and save it as gpg.conf
        
	-	This sample config file is a generally accepted defacto secure configuration, which at a minimum needs replacing 
`#default-key 0xlong` to `default-key your_keyid` 
        
for example:
```
        #default-key 0xLONG
becomes
        default-key 0xD0C33581852FCCC7 (however this would be _YOUR_ long format keyid)
```

* Grab your long (16 digit keyid) often noted as `0xLONG`, or `0xYourKeysDeadBeef` or `0xYour Keys Dead Beef' format, if you are unsure of this keyid you can use gpg2 -K --keyid-format 0xlong OR gpg2 --edit-key somename@email.xyz 

        for example:

```
        user@localhost $ gpg2 -K -keyid-format 0xlong
                ------------------------------
sec   ed25519/0xD0C33581852FCCC7 2017-06-04 [C] [expires: 2018-06-04]
      Key fingerprint = 4700 FD6D 3EC2 54F9 46BB  9404 D0C3 3581 852F CCC7
uid                   [ultimate] Corey Sheldon (Official Personal 2017 Key -- ALL Previous & Future Keys not expirign in July are invalid) <sheldon.corey@openmailbox.org>
uid                   [ultimate] [jpeg image of size 60284]
(snipped for brevity)
```

OR 

```
        user@localhost $ gpg2 --edit-key sheldon.corey@openmailbox.org
sec  ed25519/0xD0C3 3581 852F CCC7
(snipped for brevity)
```
 
******************************
*  gitconfig || .git/config: *
******************************
